[Pia](Pia-Overview) > [Protocols](Pia-Protocols) > Session Protocol (new)
---

This page describes the session protocol that can be found in Pia version 6.x. It combines the functions of the [[station protocol]] and [[mesh protocol]] into one.

*Added in 6.16 or earlier:*
| Type | Description |
| --- | --- |
| 0 | [Join request](#join-request) |
| 1 | Join request ack |
| 2 | Join response |
| 3 | Leave request |
| 4 | ? |
| 5 | Update session |
| 6 | Update session ack |
| 7 | Left station sync |
| 8 | Left station sync ack |
| 9 | Start host migration |
| 10 | Start host migration ack |

*Added in 6.26 or earlier:*

| Type | Description |
| --- | --- |
| 11 | Detect keep alive timeout |
| 12 | Kick request |

*Added in 6.40 or earlier:*

| Type | Description |
| --- | --- |
| 13 | ? |
| 14 | ? |
| 15 | ? |
| 16 | ? |
| 17 | ? |

## Join Request
*6.26:*

| Type | Description |
| --- | --- |
| Uint8 | Message type (0) |
| Uint8 | Number of protocols (N) |
| [ProtocolInfo](#protocolinfo) (N) | Protocol info |
| Uint32 | Random value |
| Uint64 | Source constant id |
| Uint16 | Source variable id |
| Uint8 | NAT mapping |
| Uint8 | Is private IPv6 |
| Uint8 (32) | Identification token (ascii) |
| [StationAddress](#stationaddress) | Station address (IPv4 or IPv6) |
| Uint64 | Destination constant id |
| Uint16 | Destination variable id |
| Uint8 | Number of players (P) |
| Uint8 | Number of participants |
| [PlayerInfo](#playerinfo) (P) | Player info |

*6.39:*

| Type | Description |
| --- | --- |
| Uint8 | Message type (0) |
| Uint8 | Number of protocols (N) |
| [ProtocolInfo](#protocolinfo) (N) | Protocol info |
| Uint16 | Application communication version |
| Uint32 | Unknown |
| Uint64 | Source constant id |
| Uint16 | Source variable id |
| Uint8 | NAT mapping |
| Uint8 | Is private IPv6 |
| Uint8 (32) | Identification token (ascii) |
| Uint64 | Destination constant id |
| Uint16 | Destination variable id |
| Uint8 | Number of players (P) |
| Uint8 | Number of participants |
| [StationAddress](#stationaddress) | Station address (IPv4 or IPv6) |
| [PlayerInfo](#playerinfo) (P) | Player info |

## ProtocolInfo
| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 1 | Protocol id |
| 0x1 | 1 | Protocol version |

## StationAddress
This structure is a wrapper around the [InetAddress](Pia-Types#inetaddress) type, but includes information about whether the address is IPv4 or IPv6.

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 1 | 0 = IPv4, 1 = IPv6 |
| 0x1 | 6 or 18 | [InetAddress](Pia-Types#inetaddress), the size depends on whether it is IPv4 or IPv6 |

## PlayerInfo
The player name may consist of up to 20 characters.

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 16 | Player id |
| 0x10 | 4 | Player name size (in bytes) |
| 0x14 | 1 | Player name encoding (1 = UTF-8, 2 = UTF-16) |
| 0x15 | | Player name |