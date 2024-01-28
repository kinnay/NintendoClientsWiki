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
| 0x10 | 2 | Port |

## StationAddress
*Up to 4.10:*

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 6 | [Inet address](#inetaddress) |
| 0x6 | 2 | Extension id |

*5.2 - 5.44:*

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

| Type | Description |
| --- | --- |
| [StationAddress](#stationaddress) | Station address |
| Uint32 | [Constant id] (PID) |
| Uint32 | [Variable id] (CID) |
| Uint32 | [Service variable id] (RVCID) |
| Uint8 | [URL type](#nex-url-type) |
| Uint8 | NEX stream id (sid) |
| Uint8 | NEX stream type (stream) |
| Uint8 | [NAT mapping](#nat-mapping) (natm) |
| Uint8 | [NAT filtering](#nat-filtering) (natf) |
| Uint8 | [NAT flags](#nat-flags) (type) |
| Uint8 | probeinit |

*5.2 - 5.9:*

| Type | Description |
| --- | --- |
| [StationAddress](#stationaddress) | Station address |
| Uint64 | [Constant id] (PID) |
| Uint32 | [Variable id] (CID) |
| Uint32 | [Service variable id] (RVCID) |
| Uint8 | [URL type](#nex-url-type) |
| Uint8 | NEX stream id (sid) |
| Uint8 | NEX stream type (stream) |
| Uint8 | [NAT mapping](#nat-mapping) (natm) |
| Uint8 | [NAT filtering](#nat-filtering) (natf) |
| Uint8 | [NAT flags](#nat-flags) (type) |
| Uint8 | probeinit |
| [InetAddress](#inetaddress) | Relay address |

*5.10:*

| Type | Description |
| --- | --- |
| [InetAddress](#inetaddress) | Public address |
| [InetAddress](#inetaddress) | Private address |
| [InetAddress](#inetaddress) | Relay address |
| Uint64 | [Constant id] (PID) |
| Uint32 | [Variable id] (CID) |
| Uint32 | [Service variable id] (RVCID) |
| Uint8 | `0x3`: [NAT filtering](#nat-filtering) (natf)<br>`0xC`: [NAT mapping](#nat-mapping) (natm)<br>`0xF0`: [NAT type](#nat-type) |
| Uint8 | [NAT flags](#nat-flags) (type) |
| Uint8 | probeinit |
| Uint8 | Is private address available |

*5.11 - 5.44:*

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
| Uint8 | [NAT flags](#nat-flags) (type) |
| Uint8 | probeinit |
| Uint8 | Is private address available |

*6.16 - 6.30:*

| Type | Description |
| --- | --- |
| Uint8 | Address size |
| [StationAddress](#stationaddress) | Address |
| Uint64 | [Constant id] |
| Uint16 | [Variable id] |
| Uint8 | `0x3`: [NAT filtering](#nat-filtering)<br>`0xC`: [NAT mapping](#nat-mapping)<br>`0x10`: Is IPv6 |

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

### NAT Flags
| Flag | Description |
| --- | --- |
| 1 | Is behind NAT |
| 2 | Is public |

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

**NEX** *(Up to 5.44):*

The constant id is the same as your principal id (pid).

**LAN** *(Up to 5.9):*

The constant id is generated from your local IP address and port: `ip << 32 | port`

**LDN** *(Up to 5.9):*

The constant id is generated from your MAC address: `mac[2] << 56 | mac[4] << 48 | mac[5] << 40 | mac[3] << 32 | mac[1] << 24 | mac[0] << 16`.

## Variable ID
The variable id uniquely identifies a station in the current session. Unlike the [constant id](#constant-id), it may change across sessions. The variable id depends on the network type:

**NEX** *(Up to 5.44):*

The variable id is the same as your connection id (CID).

**LAN** *(Up to 5.9):*

The variable is set to the current system tick (`nn::os::GetSystemTick()`) at the start of the session.

**LDN** *(Up to 5.9):*

The variable is set to the current system tick (`nn::os::GetSystemTick()`) at the start of the session.

## Service Variable ID
Like the [variable id](#variable-id), the service variable id uniquely identifies a station in the current session and may change across sessions. The service variable id depends on the network type:

**NEX** *(Up to 5.44):*

The services variable id is your Rendez-Vous connection id (RVCID). This is received from the server when the client registers itself with the [secure connection protocol](Secure-Protocol).

**LAN** *(Up to 5.9):*

The service variable id is generated from your local IP address and port: `(ip & 0xFFFF) << 16 | port`.

**LDN** *(Up to 5.9):*

The service variable id is the CRC32 hash of your MAC address.

[Constant id]: #constant-id
[Variable id]: #variable-id
[Service variable id]: #service-variable-id