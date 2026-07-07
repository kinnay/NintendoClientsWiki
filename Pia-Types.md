[Pia](Pia-Overview) > Types
---

This page describes common data structures that are used by the Pia library.

1. [InetAddress](#inetaddress)
2. [StationAddress](#stationaddress)
3. [StationLocation](#stationlocation)
4. [StationConnectionInfo](#stationconnectioninfo)

The following ids are used in various places:

1. [Constant id](#constant-id)
2. [Variable id](#variable-id)
3. [Service variable id](#service-variable-id)
4. [Network id](#network-id)

## InetAddress
*Up to 5.10:*

This structure can only represent IPv4 addresses.

| Offset | Size | Description |
| --- | -- | --- |
| 0x0 | 4 | Address |
| 0x4 | 2 | Port |

*5.11 - 6.30:*

This structure can represent both IPv4 and IPv6 addresses. Which encoding is used depends on the context.

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 0, 4 or 16 | Address |
| | 2 | Port |

## StationAddress
*Up to 4.10:*

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 6 | [Inet address](#inetaddress) |
| 0x6 | 2 | Extension id |

*5.2 - 5.10:*

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 6 | [Inet address](#inetaddress) |

*5.11 - 5.45:*

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 2, 6 or 18 | [Inet address](#inetaddress) |

*6.16 - 6.30:*

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 16 | Address |
| 0x10 | 2 | Port |

## StationLocation
The station location holds information that allows Pia to connect to a given station. Many fields are directly taken from a [station url](NEX-Common-Types#stationurl), when NEX is used.

*Up to 4.10:*

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 8 | [Station address](#stationaddress) |
| 0x8 | 4 | [Constant id] (PID) |
| 0xC | 4 | [Variable id] (CID) |
| 0x10 | 4 | [Service variable id] (RVCID) |
| 0x14 | 1 | [URL type](#nex-url-type) |
| 0x15 | 1 | NEX stream id (sid) |
| 0x16 | 1 | NEX stream type (stream) |
| 0x17 | 1 | [NAT mapping](#nat-mapping) (natm) |
| 0x18 | 1 | [NAT filtering](#nat-filtering) (natf) |
| 0x19 | 1 | [NAT location](#nat-location) (type) |
| 0x1A | 1 | probeinit |

*5.2 - 5.9:*

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 6 | [Station address](#stationaddress) |
| 0x6 | 8 | [Constant id] (PID) |
| 0xE | 4 | [Variable id] (CID) |
| 0x12 | 4 | [Service variable id] (RVCID) |
| 0x16 | 1 | [URL type](#nex-url-type) |
| 0x17 | 1 | NEX stream id (sid) |
| 0x18 | 1 | NEX stream type (stream) |
| 0x19 | 1 | [NAT mapping](#nat-mapping) (natm) |
| 0x1A | 1 | [NAT filtering](#nat-filtering) (natf) |
| 0x1B | 1 | [NAT location](#nat-location) (type) |
| 0x1C | 1 | probeinit |
| 0x1D | 6 | Relay address ([InetAddress](#inetaddress)) |

*5.10:*

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 6 | Public address ([InetAddress](#inetaddress)) |
| 0x6 | 6 | Private address ([InetAddress](#inetaddress)) |
| 0xC | 6 | Relay address ([InetAddress](#inetaddress)) |
| 0x12 | 8 | [Constant id] (PID) |
| 0x1A | 4 | [Variable id] (CID) |
| 0x1E | 4 | [Service variable id] (RVCID) |
| 0x22 | 1 | `0x3`: [NAT filtering](#nat-filtering) (natf)<br>`0xC`: [NAT mapping](#nat-mapping) (natm)<br>`0xF0`: [NAT type](#nat-type) |
| 0x23 | 1 | [NAT location](#nat-location) (type) |
| 0x24 | 1 | probeinit |
| 0x25 | 1 | Is private address available |

*5.11 - 5.45:*

| Type | Description |
| --- | --- |
| Uint8 | Size of public address |
| Uint8 | Size of private address |
| [InetAddress](#inetaddress) | Public address |
| [InetAddress](#inetaddress) | Private address |
| [InetAddress](#inetaddress) | Relay address (IPv4) |
| Uint64 | [Constant id] (PID) |
| Uint32 | [Variable id] (CID) |
| Uint32 | [Service variable id] (RVCID) |
| Uint8 | `0x3`: [NAT filtering](#nat-filtering) (natf)<br>`0xC`: [NAT mapping](#nat-mapping) (natm)<br>`0xF0`: [NAT type](#nat-type) |
| Uint8 | [NAT location](#nat-location) (type) |
| Uint8 | probeinit |
| Uint8 | Is private address available |

*6.16 - 6.30:*

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 1 | Station address size (always 18) |
| 0x1 | 18 | [Station address](#stationaddress) |
| 0x13 | 8 | [Constant id] |
| 0x1B | 2 | [Variable id] |
| 0x1D | 1 | `0x3`: [NAT filtering](#nat-filtering)<br>`0xC`: [NAT mapping](#nat-mapping)<br>`0x10`: Is IPv6 |

### NEX URL Type
The URL type depends on the scheme of the given station url. It is always 0 or 1 in practice.

| Value | Scheme |
| --- | --- |
| 0 | Invalid |
| 1 | `prudp` |
| 2 | `prudps` |
| 3 | `udp` |

### NAT Mapping
| Value | Description |
| --- | --- |
| 0 | Unknown |
| 1 | Endpoint independent mapping |
| 2 | Endpoint dependent mapping |

### NAT Filtering
| Value | Description |
| --- | --- |
| 0 | Unknown |
| 1 | Port independent filtering |
| 2 | Port dependent filtering |

### NAT Location
| Value | Description |
| --- | --- |
| 0 | Unknown |
| 1 | Is behind NAT |
| 2 | Is public (not behind NAT) |

### NAT Type
The NAT type determines how well the Switch is able to set up peer-to-peer connections. A is the best and F is the worst. The NAT type is also shown in the system settings if you perform a connection test.

The NAT type is used during host migration, giving players with a better NAT type a higher priority.

| Value | Type |
| --- | --- |
| 0 | F |
| 1 | A |
| 2 | B |
| 3 | C |
| 4 | D |

## StationConnectionInfo
*Up to 5.9:*
| Type | Description |
| --- | --- |
| [StationLocation](#stationlocation) | Public location |
| [StationLocation](#stationlocation) | Private location |

In later Pia versions, the station connection info structure was removed.

## Constant ID
The constant id uniquely identifies a station, and never changes, even across sessions. The constant id depends on the network type.

**NEX** *(Up to 5.45):*

The constant id is the same as your principal id (pid).

**LAN** *(Up to 5.9):*

The constant id is generated from your local IP address and port: `ip << 32 | port`

**LDN** *(Up to 6.39):*

The constant id is generated from your MAC address: `mac[2] << 56 | mac[4] << 48 | mac[5] << 40 | mac[3] << 32 | mac[1] << 24 | mac[0] << 16`.

## Variable ID
The variable id uniquely identifies a station in the current session. Unlike the [constant id](#constant-id), it may change across sessions. The variable id depends on the network type. In old Pia versions, the variable id was called "connection id" instead.

Up to Pia version 5.45, the variable id is a 32-bit integer. In Pia version 6.16 and later, it is a 16-bit integer instead.

**NEX** *(Up to 5.45):*

The variable id is the same as your connection id (CID).

**LAN** / **LDN** *(Up to 6.39):*

The exact method with which the variable id is generated varies per Pia version, but it is indiscernible from a random value. In Pia 6.x, it is ensured that the variable id is always at least 2.

## Service Variable ID
Like the [variable id](#variable-id), the service variable id uniquely identifies a station in the current session and may change across sessions. The service variable id depends on the network type. In old Pia versions, the service variable id was called "service connection id (scid)" instead.

In Pia 6.x, the concept of the service variable id was removed.

**NEX** *(Up to 5.45):*

The services variable id is your Rendez-Vous connection id (RVCID). This is received from the server when the client registers itself with the [secure connection protocol](Secure-Protocol).

**LAN** *(Up to 5.45):*

The service variable id is generated from your local IP address and port: `(ip & 0xFFFF) << 16 | port`.

If IPv6 is used, the IP address is compressed into a 32-bit integer with a HMAC-SHA256 in a way that is indistinguishable from random noise.

**LDN** *(Up to 5.45):*

The service variable id is the CRC-32 hash of your MAC address.

## Network ID
The network id uniquely identifies a Pia network. Before Pia 6, the network id was called "session id" instead.

**NEX:**

The network id is the [gathering id](https://github.com/kinnay/NintendoClients/wiki/Match-Making-Types#gathering-structure) received from NEX.

**LAN** *(Up to 5.45):*

The network id is generated by the host from its local IP address and port: `((ip & 0xFFFF) << 16) | port`

For example, if the local IP address of the host is `192.168.178.215` and its port is `49154`, then the network id `0xB2D7C002`.

**LAN** *(6.16 - 6.40):*

The network id is generated by the host from its local IP address and a random value: `(random << 32) | ip`.

If IPv6 is used, the IP address is compressed into a 32-bit integer with a HMAC-SHA256 in a way that is indistinguishable from random noise.

**LDN** *(Up to 5.45):*

The network id is a random 32-bit integer that is generated by the host when the network is created. It is broadcasted as part of the [application data](LDN-Application-Data-(Pia)).

**LDN** *(6.16 - 6.42):*

The network id is the CRC-32 hash of all bytes of the SSID except for the first (`ssid[1:16]`).

[Constant id]: #constant-id
[Variable id]: #variable-id
[Service variable id]: #service-variable-id