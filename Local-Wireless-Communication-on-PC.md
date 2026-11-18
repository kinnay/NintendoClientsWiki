This page is intended to provide a simple guide to get started with local wireless communication on PC (for [LDN](LDN-Protocol)).

It is written for Linux users and was tested on a system running Ubuntu 24.04. If you are using a different operating system, this guide is probably less useful for you.

1. [Enabling monitor mode](#enabling-monitor-mode)
2. [Switching channels](#switching-channels)
3. [Disabling monitor mode](#disabling-monitor-mode)
4. [Receiving packets with libpcap](#receiving-packets-with-libpcap)
5. [Emulating LDN with NL80211](#emulating-ldn-with-nl80211)

### Enabling monitor mode
By default, the network interface is in managed mode, which means that it only accepts packets that are intended for your PC:

```console
yannik@yannik:~$ iwconfig
wlp2s0    IEEE 802.11  ESSID:"Lothlorien"  
          Mode:Managed  Frequency:5.5 GHz  Access Point: 94:A7:B7:49:F6:F9   
          Bit Rate=520 Mb/s   Tx-Power=22 dBm   
          Retry short limit:7   RTS thr:off   Fragment thr:off
          Power Management:on
          Link Quality=31/70  Signal level=-79 dBm  
          Rx invalid nwid:0  Rx invalid crypt:0  Rx invalid frag:0
          Tx excessive retries:0  Invalid misc:165   Missed beacon:0
```

In monitor mode, the network interface receives all packets that are sent through the air:

```console
yannik@yannik:~$ sudo service NetworkManager stop
yannik@yannik:~$ sudo iw wlp2s0 set type monitor
yannik@yannik:~$ sudo ip link set wlp2s0 up
yannik@yannik:~$ iwconfig
wlp2s0    IEEE 802.11  Mode:Monitor  Frequency:2.462 GHz  Tx-Power=-2147483648 dBm   
          Retry short limit:7   RTS thr:off   Fragment thr:off
          Power Management:on
```

If you start wireshark now, you will probably see a huge number of packets, maybe even thousands of packets per second, because we are capturing ALL packets that are sent through the air.

### Switching channels
You can only capture packets on a specific channel, but LDN may operate on one out of [seven different channels](LDN-Protocol#wlan-channels). The following command changes the channel of your device:

```console
yannik@yannik:~$ sudo iw wlp2s0 set channel <channel>
```

This command can even be used while Wireshark is running (there is no need to turn it off).

### Disabling monitor mode
Because we had to disable the network-manager service, you cannot access the internet while in monitor mode. To disable monitor mode, run the following commands:

```console
yannik@yannik:~$ sudo ip link set wlp2s0 down
yannik@yannik:~$ sudo iw wlp2s0 set type managed
yannik@yannik:~$ sudo service NetworkManager start
yannik@yannik:~$ iwconfig
wlp2s0    IEEE 802.11  ESSID:"Lothlorien"  
          Mode:Managed  Frequency:5.5 GHz  Access Point: 94:A7:B7:49:F6:F9   
          Bit Rate=520 Mb/s   Tx-Power=22 dBm   
          Retry short limit:7   RTS thr:off   Fragment thr:off
          Power Management:on
          Link Quality=33/70  Signal level=-77 dBm  
          Rx invalid nwid:0  Rx invalid crypt:0  Rx invalid frag:0
          Tx excessive retries:0  Invalid misc:17   Missed beacon:0
```

### Receiving packets with libpcap
Libpcap provides low-level networking functions. Here's an example that scans for action frames sent by Nintendo devices in LDN mode. Make sure that the wireless interface is in monitor mode before running this, and [switch to a different channel](#switching-channels) if you do not see any action frames.

```c
#include <pcap.h>

#include <stdio.h>
#include <stdint.h>
#include <stdbool.h>

// See https://www.radiotap.org/
struct radiotap_header {
    uint8_t it_version;
    uint8_t it_pad;
    uint16_t it_len;
    uint32_t it_present;
};

// See IEEE 802.11 specification
struct ieee80211_header {
    uint16_t frame_control;
    uint16_t duration;
    uint8_t address1[6];
    uint8_t address2[6];
    uint8_t address3[6];
    uint16_t sequence;
};

#define IEEE80211_FTYPE_MGMT 0x0000
#define IEEE80211_STYPE_ACTION 0x00D0

enum ieee80211_category {
    WLAN_CATEGORY_VENDOR_SPECIFIC = 127
};

void process_ieee80211_packet(const uint8_t *data, size_t size) {
    size -= 4; // Remove frame checksum

    // Parse IEEE 802.11 frame header
    struct ieee80211_header *header = (struct ieee80211_header *)data;
    data += sizeof(struct ieee80211_header);
    size -= sizeof(struct ieee80211_header);

    // Check if we received an action frame
    if (header->frame_control == IEEE80211_FTYPE_MGMT | IEEE80211_STYPE_ACTION) {
        // Check if we received a vendor-specific action frame
        if (data[0] == WLAN_CATEGORY_VENDOR_SPECIFIC) {
            // Check if the organizationally unique identifier belongs to Nintendo
            if (data[1] == 0 && data[2] == 0x22 && data[3] == 0xAA) {
                printf("Received action frame from Nintendo device: ");
                for (size_t i = 0; i < size; i++) {
                    printf("%02x", data[i]);
                }
                printf("\n");
            }
        }
    }
}

void process_radiotap_packet(const uint8_t *data, size_t size) {
    struct radiotap_header *radio = (struct radiotap_header *)data;
    process_ieee80211_packet(data + radio->it_len, size - radio->it_len);
}

bool main_loop(pcap_t *p) {
    struct pcap_pkthdr header;
    while (true) {
        const uint8_t *data = pcap_next(p, &header);
        if (!data) {
            printf("pcap_next failed: %s\n", pcap_geterr(p));
            return false;
        }
        
        process_radiotap_packet(data, header.caplen);
    }
    return true;
}

pcap_t *init_pcap() {
    char error[PCAP_ERRBUF_SIZE];
    pcap_t *p = pcap_create("wlp2s0", error);
    if (!p) {
        printf("pcap_create failed: %s\n", error);
        return NULL;
    }
    
    int result = pcap_set_immediate_mode(p, 1);
    if (result != 0) {
        printf("pcap_set_immediate_mode failed: %s\n", pcap_geterr(p));
        pcap_close(p);
        return NULL;
    }
    
    result = pcap_activate(p);
    if (result < 0) {
        printf("pcap_activate failed: %s\n", pcap_geterr(p));
        pcap_close(p);
        return NULL;
    }
    
    return p;
}

int main() {
    pcap_t *p = init_pcap();
    if (p) {
        main_loop(p);
        pcap_close(p);
    }
    return 0;
}
```

### Emulating LDN with NL80211
While libpcap is useful for basic packet sniffing, it is not practical for LDN emulation because it would require you to implement your own network stack including 802.11, IPv4 and UDP.

For full LDN emulation it is better to use a library that implements [NL80211](https://wireless.wiki.kernel.org/en/developers/documentation/nl80211), which gives fine grained control over your WLAN hardware on Linux. With this approach one can become part of a LDN network like a normal wireless network, after which one can use normal UDP sockets to communicate with other Switches.

Unfortunately, there is little documentation on using NL80211, but a good place to get started are the [source code of the iw tool](https://git.kernel.org/pub/scm/linux/kernel/git/jberg/iw.git) and the [Linux kernel code](https://github.com/torvalds/linux/blob/master/net/wireless/nl80211.c).

You might also be interested in my Python package: https://github.com/kinnay/LDN.