[Pia](Pia-Overview) > Protocols
---

This page lists the protocols that may be implemented in the given Pia versions.

* [3.3 - 3.10](#33---310)
* [4.5](#45)
* [4.8 - 4.10](#48---410)
* [5.2](#52)
* [5.3 - 5.4](#53---54)
* [5.6 - 5.9](#56---59)
* [5.10](#510)
* [5.11](#511)
* [5.12](#512)
* [5.14](#514)
* [5.17 - 5.18](#517---518)
* [5.19](#519)
* [5.20 - 5.21](#520---521)
* [5.23](#523)
* [5.24 - 5.25](#524---525)
* [5.26 - 5.28](#526---528)
* [5.29 - 5.44](#529---544)
* [6.16 - 6.30](#616---630)
* [6.32 - 6.40](#632---640)
* [7.0](#70)

## 3.3 - 3.10
This is the earliest Pia version that we are aware of.

| ID | Protocol |
| --- | --- |
| 0x0080 | Relay Protocol |
| 0x00C0 | Keep Alive Protocol |
| 0x0100 | [[Station Protocol]] |
| 0x0200 | [Session Protocol](Mesh-Protocol) |
| 0x0210 | [Session Clock Protocol](Sync-Clock-Protocol) |
| 0x0400 | [NAT Protocol] |
| 0x0410 | Gateway Protocol |
| 0x0600 | [[RTT Protocol]] |
| 0x1800 | Sync Protocol (old) |
| 0x1810 | [[Sync Protocol]] |
| 0x2000 | [[Unreliable Protocol]] |
| 0x2100 | Roundrobin Unreliable Protocol |
| 0x2400 | [[Clone Protocol]] |
| 0x2800 | Voice Protocol |
| 0x3000 | [[Reliable Protocol]] |
| 0x7000 | Reliable Broadcast Protocol |
| 0x7200 | [Match Protocol](Session-Protocol) |
| 0x8000 | [Feedback Protocol] |
| 0x8200 | Relay Service Protocol |

## 4.5
A few protocols were renamed.

| ID | Protocol |
| --- | --- |
| 0x0080 | Relay Protocol |
| 0x00C0 | Keep Alive Protocol |
| 0x0100 | [[Station Protocol]] |
| 0x0200 | [[Mesh Protocol]] |
| 0x0210 | [[Sync Clock Protocol]] |
| 0x0400 | [NAT Protocol] |
| 0x0410 | Gateway Protocol |
| 0x0600 | [[RTT Protocol]] |
| 0x1800 | Sync Protocol (old) |
| 0x1810 | [[Sync Protocol]] |
| 0x2000 | [[Unreliable Protocol]] |
| 0x2100 | Roundrobin Unreliable Protocol |
| 0x2400 | [[Clone Protocol]] |
| 0x2800 | Voice Protocol |
| 0x3000 | [[Reliable Protocol]] |
| 0x7000 | Reliable Broadcast Protocol |
| 0x7200 | [[Session Protocol]] |
| 0x8000 | [Feedback Protocol] |
| 0x8200 | Relay Service Protocol |

## 4.8 - 4.10
The bandwidth check protocol was added.

| ID | Protocol |
| --- | --- |
| 0x0080 | Relay Protocol |
| 0x00C0 | Keep Alive Protocol |
| 0x0100 | [[Station Protocol]] |
| 0x0200 | [[Mesh Protocol]] |
| 0x0210 | [[Sync Clock Protocol]] |
| 0x0400 | [NAT Protocol] |
| 0x0410 | Gateway Protocol |
| 0x0500 | Bandwidth Check Protocol |
| 0x0600 | [[RTT Protocol]] |
| 0x1800 | Sync Protocol (old) |
| 0x1810 | [[Sync Protocol]] |
| 0x2000 | [[Unreliable Protocol]] |
| 0x2100 | Roundrobin Unreliable Protocol |
| 0x2400 | [[Clone Protocol]] |
| 0x2800 | Voice Protocol |
| 0x3000 | [[Reliable Protocol]] |
| 0x7000 | Reliable Broadcast Protocol |
| 0x7200 | [[Session Protocol]] |
| 0x8000 | [Feedback Protocol] |
| 0x8200 | Relay Service Protocol |

## 5.2
This is the first version in which the local and LAN protocol were seen.

| ID | Protocol |
| --- | --- |
| 0x0080 | Relay Protocol |
| 0x00C0 | Keep Alive Protocol |
| 0x0100 | [[Station Protocol]] |
| 0x0200 | [[Mesh Protocol]] |
| 0x0210 | [[Sync Clock Protocol]] |
| 0x0300 | [[Local Protocol]] |
| 0x0400 | [NAT Protocol] |
| 0x0410 | Gateway Protocol |
| 0x0420 | [[LAN Protocol]] |
| 0x0500 | Bandwidth Check Protocol |
| 0x0600 | [[RTT Protocol]] |
| 0x1810 | [[Sync Protocol]] |
| 0x2000 | [[Unreliable Protocol]] |
| 0x2400 | [[Clone Protocol]] |
| 0x2800 | Voice Protocol |
| 0x3000 | [[Reliable Protocol]] |
| 0x7000 | Reliable Broadcast Protocol |
| 0x7200 | [[Session Protocol]] |
| 0x8000 | [Feedback Protocol] |

## 5.3 - 5.4
The direct and net protocol were introduced.

| ID | Protocol |
| --- | --- |
| 0x0080 | Relay Protocol |
| 0x00C0 | Keep Alive Protocol |
| 0x0100 | [[Station Protocol]] |
| 0x0200 | [[Mesh Protocol]] |
| 0x0210 | [[Sync Clock Protocol]] |
| 0x0300 | [[Local Protocol]] |
| 0x0310 | Direct Protocol |
| 0x0320 | Net Protocol |
| 0x0400 | [NAT Protocol] |
| 0x0410 | Gateway Protocol |
| 0x0420 | [[LAN Protocol]] |
| 0x0500 | Bandwidth Check Protocol |
| 0x0600 | [[RTT Protocol]] |
| 0x1810 | [[Sync Protocol]] |
| 0x2000 | [[Unreliable Protocol]] |
| 0x2400 | [[Clone Protocol]] |
| 0x2800 | Voice Protocol |
| 0x3000 | [[Reliable Protocol]] |
| 0x7000 | Reliable Broadcast Protocol |
| 0x7200 | [[Session Protocol]] |
| 0x8000 | [Feedback Protocol] |

## 5.6 - 5.9
The protocol list was cleaned up and new ids were assigned.

| ID | Protocol |
| --- | --- |
| 0x08 | Keep Alive Protocol |
| 0x14 | [[Station Protocol]] |
| 0x18 | [[Mesh Protocol]] |
| 0x1C | [[Sync Clock Protocol]] |
| 0x24 | [[Local Protocol]] |
| 0x28 | Direct Protocol |
| 0x2C | Net Protocol |
| 0x34 | [NAT Protocol] |
| 0x44 | [[LAN Protocol]] |
| 0x54 | Bandwidth Check Protocol |
| 0x58 | [[RTT Protocol]] |
| 0x64 | [[Sync Protocol]] |
| 0x68 | [[Unreliable Protocol]] |
| 0x6C | Roundrobin Unreliable Protocol |
| 0x74 | [[Clone Protocol]] |
| 0x78 | Voice Protocol |
| 0x7C | [[Reliable Protocol]] |
| 0x84 | Reliable Broadcast Protocol |
| 0x94 | [[Session Protocol]] |
| 0xA4 | [Feedback Protocol] |
| 0xA8 | Relay Service Protocol |

## 5.10
The lobby protocols were introduced.

| ID | Protocol |
| --- | --- |
| 0x08 | Keep Alive Protocol |
| 0x14 | [[Station Protocol]] |
| 0x18 | [[Mesh Protocol]] |
| 0x1C | [[Sync Clock Protocol]] |
| 0x24 | [[Local Protocol]] |
| 0x28 | Direct Protocol |
| 0x2C | Net Protocol |
| 0x34 | [NAT Protocol] |
| 0x44 | [[LAN Protocol]] |
| 0x54 | Bandwidth Check Protocol |
| 0x58 | [[RTT Protocol]] |
| 0x64 | [[Sync Protocol]] |
| 0x68 | [[Unreliable Protocol]] |
| 0x6C | Roundrobin Unreliable Protocol |
| 0x6D | Lobby Unreliable Protocol |
| 0x74 | [[Clone Protocol]] |
| 0x78 | Voice Protocol |
| 0x7C | [[Reliable Protocol]] |
| 0x84 | Reliable Broadcast Protocol |
| 0x94 | [[Session Protocol]] |
| 0x98 | Lobby Protocol |
| 0xA4 | [Feedback Protocol] |
| 0xA8 | Relay Service Protocol |

## 5.11
The clone and sync protocol were split up into smaller protocols. The unreliable lobby protocol was removed.

| ID | Protocol |
| --- | --- |
| 0x08 | Keep Alive Protocol |
| 0x14 | [[Station Protocol]] |
| 0x18 | [[Mesh Protocol]] |
| 0x1C | [[Sync Clock Protocol]] |
| 0x24 | [[Local Protocol]] |
| 0x28 | Direct Protocol |
| 0x2C | Net Protocol |
| 0x34 | [NAT Protocol] |
| 0x44 | [[LAN Protocol]] |
| 0x54 | Bandwidth Check Protocol |
| 0x58 | [[RTT Protocol]] |
| 0x64 | [[Sync Protocol]] |
| 0x65 | Sync Protocol (event) |
| 0x68 | [[Unreliable Protocol]] |
| 0x6C | Roundrobin Unreliable Protocol |
| 0x73 | [[Clone Protocol]] |
| 0x74 | Clone Protocol (atomic) |
| 0x75 | Clone Protocol (event) |
| 0x77 | [Clone Protocol (clock)] |
| 0x78 | Voice Protocol |
| 0x7C | [[Reliable Protocol]] |
| 0x84 | Reliable Broadcast Protocol |
| 0x94 | [[Session Protocol]] |
| 0x98 | Lobby Protocol |
| 0xA4 | [Feedback Protocol] |
| 0xA8 | Relay Service Protocol |

## 5.12
The WAN NAT protocol was added.

| ID | Protocol |
| --- | --- |
| 0x08 | Keep Alive Protocol |
| 0x14 | [[Station Protocol]] |
| 0x18 | [[Mesh Protocol]] |
| 0x1C | [[Sync Clock Protocol]] |
| 0x24 | [[Local Protocol]] |
| 0x28 | Direct Protocol |
| 0x2C | Net Protocol |
| 0x34 | [NAT Protocol] |
| 0x44 | [[LAN Protocol]] |
| 0x54 | Bandwidth Check Protocol |
| 0x58 | [[RTT Protocol]] |
| 0x64 | [[Sync Protocol]] |
| 0x65 | Sync Protocol (event) |
| 0x68 | [[Unreliable Protocol]] |
| 0x6C | Roundrobin Unreliable Protocol |
| 0x73 | [[Clone Protocol]] |
| 0x74 | Clone Protocol (atomic) |
| 0x75 | Clone Protocol (event) |
| 0x77 | [Clone Protocol (clock)] |
| 0x78 | Voice Protocol |
| 0x7C | [[Reliable Protocol]] |
| 0x84 | Reliable Broadcast Protocol |
| 0x94 | [[Session Protocol]] |
| 0x98 | Lobby Protocol |
| 0xA4 | [Feedback Protocol] |
| 0xA8 | Relay Service Protocol |
| 0xAC | WAN NAT Protocol |

## 5.14
The broadcast reliable protocol was added, which is meant to replace the reliable broadcast protocol.

| ID | Protocol |
| --- | --- |
| 0x08 | Keep Alive Protocol |
| 0x14 | [[Station Protocol]] |
| 0x18 | [[Mesh Protocol]] |
| 0x1C | [[Sync Clock Protocol]] |
| 0x24 | [[Local Protocol]] |
| 0x28 | Direct Protocol |
| 0x2C | Net Protocol |
| 0x34 | [NAT Protocol] |
| 0x44 | [[LAN Protocol]] |
| 0x54 | Bandwidth Check Protocol |
| 0x58 | [[RTT Protocol]] |
| 0x64 | [[Sync Protocol]] |
| 0x65 | Sync Protocol (event) |
| 0x68 | [[Unreliable Protocol]] |
| 0x6C | Roundrobin Unreliable Protocol |
| 0x73 | [[Clone Protocol]] |
| 0x74 | Clone Protocol (atomic) |
| 0x75 | Clone Protocol (event) |
| 0x77 | [Clone Protocol (clock)] |
| 0x78 | Voice Protocol |
| 0x7C | [[Reliable Protocol]] |
| 0x80 | [[Broadcast Reliable Protocol]] |
| 0x84 | Reliable Broadcast Protocol |
| 0x94 | [[Session Protocol]] |
| 0x98 | Lobby Protocol |
| 0xA4 | [Feedback Protocol] |
| 0xA8 | Relay Service Protocol |
| 0xAC | WAN NAT Protocol |

## 5.17 - 5.18
The old sync protocol was removed. The stream broadcast reliable protocol was added.

| ID | Protocol |
| --- | --- |
| 0x08 | Keep Alive Protocol |
| 0x14 | [[Station Protocol]] |
| 0x18 | [[Mesh Protocol]] |
| 0x1C | [[Sync Clock Protocol]] |
| 0x24 | [[Local Protocol]] |
| 0x28 | Direct Protocol |
| 0x2C | Net Protocol |
| 0x34 | [NAT Protocol] |
| 0x44 | [[LAN Protocol]] |
| 0x54 | Bandwidth Check Protocol |
| 0x58 | [[RTT Protocol]] |
| 0x65 | Sync Protocol |
| 0x68 | [[Unreliable Protocol]] |
| 0x6C | Roundrobin Unreliable Protocol |
| 0x73 | [[Clone Protocol]] |
| 0x74 | Clone Protocol (atomic) |
| 0x75 | Clone Protocol (event) |
| 0x77 | [Clone Protocol (clock)] |
| 0x78 | Voice Protocol |
| 0x7C | [[Reliable Protocol]] |
| 0x80 | [[Broadcast Reliable Protocol]] |
| 0x81 | [[Stream Broadcast Reliable Protocol]] |
| 0x84 | Reliable Broadcast Protocol |
| 0x94 | [[Session Protocol]] |
| 0x98 | Lobby Protocol |
| 0xA4 | [Feedback Protocol] |
| 0xA8 | Relay Service Protocol |
| 0xAC | WAN NAT Protocol |

## 5.19
The voice protocol was assigned a different protocol id.

| ID | Protocol |
| --- | --- |
| 0x08 | Keep Alive Protocol |
| 0x14 | [[Station Protocol]] |
| 0x18 | [[Mesh Protocol]] |
| 0x1C | [[Sync Clock Protocol]] |
| 0x24 | [[Local Protocol]] |
| 0x28 | Direct Protocol |
| 0x2C | Net Protocol |
| 0x34 | [NAT Protocol] |
| 0x44 | [[LAN Protocol]] |
| 0x54 | Bandwidth Check Protocol |
| 0x58 | [[RTT Protocol]] |
| 0x65 | Sync Protocol |
| 0x68 | [[Unreliable Protocol]] |
| 0x6C | Roundrobin Unreliable Protocol |
| 0x73 | [[Clone Protocol]] |
| 0x74 | Clone Protocol (atomic) |
| 0x75 | Clone Protocol (event) |
| 0x77 | [Clone Protocol (clock)] |
| 0x7B | Voice Protocol |
| 0x7C | [[Reliable Protocol]] |
| 0x80 | [[Broadcast Reliable Protocol]] |
| 0x81 | [[Stream Broadcast Reliable Protocol]] |
| 0x84 | Reliable Broadcast Protocol |
| 0x94 | [[Session Protocol]] |
| 0x98 | Lobby Protocol |
| 0xA4 | [Feedback Protocol] |
| 0xA8 | Relay Service Protocol |
| 0xAC | WAN NAT Protocol |

## 5.20 - 5.21
The reliable broadcast protocol was removed.

| ID | Protocol |
| --- | --- |
| 0x08 | Keep Alive Protocol |
| 0x14 | [[Station Protocol]] |
| 0x18 | [[Mesh Protocol]] |
| 0x1C | [[Sync Clock Protocol]] |
| 0x24 | [[Local Protocol]] |
| 0x28 | Direct Protocol |
| 0x2C | Net Protocol |
| 0x34 | [NAT Protocol] |
| 0x44 | [[LAN Protocol]] |
| 0x54 | Bandwidth Check Protocol |
| 0x58 | [[RTT Protocol]] |
| 0x65 | Sync Protocol |
| 0x68 | [[Unreliable Protocol]] |
| 0x6C | Roundrobin Unreliable Protocol |
| 0x73 | [[Clone Protocol]] |
| 0x74 | Clone Protocol (atomic) |
| 0x75 | Clone Protocol (event) |
| 0x77 | [Clone Protocol (clock)] |
| 0x7B | Voice Protocol |
| 0x7C | [[Reliable Protocol]] |
| 0x80 | [[Broadcast Reliable Protocol]] |
| 0x81 | [[Stream Broadcast Reliable Protocol]] |
| 0x94 | [[Session Protocol]] |
| 0x98 | Lobby Protocol |
| 0xA4 | [Feedback Protocol] |
| 0xA8 | Relay Service Protocol |
| 0xAC | WAN NAT Protocol |

## 5.23
The bandwidth check protocol was removed.

| ID | Protocol |
| --- | --- |
| 0x08 | Keep Alive Protocol |
| 0x14 | [[Station Protocol]] |
| 0x18 | [[Mesh Protocol]] |
| 0x1C | [[Sync Clock Protocol]] |
| 0x24 | [[Local Protocol]] |
| 0x28 | Direct Protocol |
| 0x2C | Net Protocol |
| 0x34 | [NAT Protocol] |
| 0x44 | [[LAN Protocol]] |
| 0x58 | [[RTT Protocol]] |
| 0x65 | Sync Protocol |
| 0x68 | [[Unreliable Protocol]] |
| 0x6C | Roundrobin Unreliable Protocol |
| 0x73 | [[Clone Protocol]] |
| 0x74 | Clone Protocol (atomic) |
| 0x75 | Clone Protocol (event) |
| 0x77 | [Clone Protocol (clock)] |
| 0x7B | Voice Protocol |
| 0x7C | [[Reliable Protocol]] |
| 0x80 | [[Broadcast Reliable Protocol]] |
| 0x81 | [[Stream Broadcast Reliable Protocol]] |
| 0x94 | [[Session Protocol]] |
| 0x98 | Lobby Protocol |
| 0xA4 | [Feedback Protocol] |
| 0xA8 | Relay Service Protocol |
| 0xAC | WAN NAT Protocol |

## 5.24 - 5.25
The reckoning protocols were added. The feedback protocol was renamed to monitoring data protocol.

| ID | Protocol |
| --- | --- |
| 0x08 | Keep Alive Protocol |
| 0x14 | [[Station Protocol]] |
| 0x18 | [[Mesh Protocol]] |
| 0x1C | [[Sync Clock Protocol]] |
| 0x24 | [[Local Protocol]] |
| 0x28 | Direct Protocol |
| 0x2C | Net Protocol |
| 0x34 | [NAT Protocol] |
| 0x44 | [[LAN Protocol]] |
| 0x58 | [[RTT Protocol]] |
| 0x65 | Sync Protocol |
| 0x68 | [[Unreliable Protocol]] |
| 0x6C | Roundrobin Unreliable Protocol |
| 0x73 | [[Clone Protocol]] |
| 0x74 | Clone Protocol (atomic) |
| 0x75 | Clone Protocol (event) |
| 0x77 | [Clone Protocol (clock)] |
| 0x7B | Voice Protocol |
| 0x7C | [[Reliable Protocol]] |
| 0x80 | [[Broadcast Reliable Protocol]] |
| 0x81 | [[Stream Broadcast Reliable Protocol]] |
| 0x94 | [[Session Protocol]] |
| 0x98 | Lobby Protocol |
| 0xA4 | [[Monitoring Data Protocol]] |
| 0xA8 | Relay Service Protocol |
| 0xAC | WAN NAT Protocol |
| 0xB0 | Reckoning 1D Protocol |
| 0xB4 | Reckoning 3D Protocol |

## 5.26 - 5.28
Several protocols were removed.

| ID | Protocol |
| --- | --- |
| 0x08 | Keep Alive Protocol |
| 0x14 | [[Station Protocol]] |
| 0x18 | [[Mesh Protocol]] |
| 0x1C | [[Sync Clock Protocol]] |
| 0x24 | [[Local Protocol]] |
| 0x34 | [NAT Protocol] |
| 0x44 | [[LAN Protocol]] |
| 0x58 | [[RTT Protocol]] |
| 0x65 | Sync Protocol |
| 0x68 | [[Unreliable Protocol]] |
| 0x73 | [[Clone Protocol]] |
| 0x74 | Clone Protocol (atomic) |
| 0x75 | Clone Protocol (event) |
| 0x77 | [Clone Protocol (clock)] |
| 0x7B | Voice Protocol |
| 0x7C | [[Reliable Protocol]] |
| 0x80 | [[Broadcast Reliable Protocol]] |
| 0x81 | [[Stream Broadcast Reliable Protocol]] |
| 0x94 | [[Session Protocol]] |
| 0xA4 | [[Monitoring Data Protocol]] |
| 0xB0 | Reckoning 1D Protocol |
| 0xB4 | Reckoning 3D Protocol |

## 5.29 - 5.44
The broadcast event protocol was added to the clone protocol.

| ID | Protocol |
| --- | --- |
| 0x08 | Keep Alive Protocol |
| 0x14 | [[Station Protocol]] |
| 0x18 | [[Mesh Protocol]] |
| 0x1C | [[Sync Clock Protocol]] |
| 0x24 | [[Local Protocol]] |
| 0x34 | [NAT Protocol] |
| 0x44 | [[LAN Protocol]] |
| 0x58 | [[RTT Protocol]] |
| 0x65 | Sync Protocol |
| 0x68 | [[Unreliable Protocol]] |
| 0x73 | [[Clone Protocol]] |
| 0x74 | Clone Protocol (atomic) |
| 0x75 | Clone Protocol (event) |
| 0x76 | Clone Protocol (broadcast event) |
| 0x77 | [Clone Protocol (clock)] |
| 0x7B | Voice Protocol |
| 0x7C | [[Reliable Protocol]] |
| 0x80 | [[Broadcast Reliable Protocol]] |
| 0x81 | [[Stream Broadcast Reliable Protocol]] |
| 0x94 | [[Session Protocol]] |
| 0xA4 | [[Monitoring Data Protocol]] |
| 0xB0 | Reckoning 1D Protocol |
| 0xB4 | Reckoning 3D Protocol |

## 6.16 - 6.30
The Pia library was redesigned for NPLN.

| ID | Protocol |
| --- | --- |
| 0x08 | Keep Alive Protocol |
| 0x2C | [[Net Protocol]] |
| 0x30 | Turn Protocol |
| 0x58 | [[RTT Protocol]] |
| 0x65 | Sync Protocol |
| 0x68 | [[Unreliable Protocol]] |
| 0x74 | Clone Protocol (atomic) |
| 0x75 | Clone Protocol (event) |
| 0x76 | Clone Protocol (broadcast event) |
| 0x77 | [Clone Protocol (clock)] |
| 0x7B | Voice Protocol |
| 0x7C | [[Reliable Protocol]] |
| 0x80 | [[Broadcast Reliable Protocol]] |
| 0x81 | [[Stream Broadcast Reliable Protocol]] |
| 0x98 | [[Session Protocol (new)]] |
| 0xA0 | NAT Traversal Result Protocol |
| 0xA4 | [[Monitoring Data Protocol]] |
| 0xAC | WAN NAT Protocol |
| 0xB0 | Reckoning 1D Protocol |
| 0xB4 | Reckoning 3D Protocol |

## 6.32 - 6.40
All protocol ids were changed.

| ID | Protocol |
| --- | --- |
| 1 | [[Net Protocol]] |
| 2 | Turn Protocol |
| 3 | [[RTT Protocol]] |
| 4 | Sync Protocol |
| 5 | [[Unreliable Protocol]] |
| 6 | Clone Protocol (atomic) |
| 7 | Clone Protocol (event) |
| 8 | Clone Protocol (broadcast event) |
| 9 | Clone Protocol (clock) |
| 10 | [[Reliable Protocol]] |
| 11 | [[Broadcast Reliable Protocol]] |
| 12 | [[Stream Broadcast Reliable Protocol]] |
| 13 | [[Session Protocol (new)]] |
| 14 | NAT Traversal Result Protocol |
| 15 | [[Monitoring Data Protocol]] |
| 16 | WAN NAT Traversal Protocol |
| 17 | Reckoning 1D Protocol |
| 18 | Reckoning 3D Protocol |

## 7.0
Some protocol ids were changed.

| ID | Protocol |
| --- | --- |
| 0 | [[Net Protocol]] |
| 1 | [[Session Protocol (new)]] |
| 3 | [[RTT Protocol]] |
| 4 | Sync Protocol |
| 5 | [[Unreliable Protocol]] |
| 6 | Clone Protocol (atomic) |
| 7 | Clone Protocol (event) |
| 8 | Clone Protocol (broadcast event) |
| 9 | Clone Protocol (clock) |
| 10 | [[Reliable Protocol]] |
| 11 | [[Broadcast Reliable Protocol]] |
| 12 | [[Stream Broadcast Reliable Protocol]] |
| 13 | NAT Traversal Result Protocol |
| 14 | [[Monitoring Data Protocol]] |
| 15 | WAN NAT Traversal Protocol |
| 16 | Reckoning 1D Protocol |
| 17 | Reckoning 3D Protocol |

[Feedback Protocol]: Monitoring-Data-Protocol
[NAT Protocol]: NAT-Traversal-Protocol-(Pia)
[WAN NAT Protocol]: NAT-Traversal-Protocol-(Pia)
[Clone Protocol (clock)]: Clock-Protocol-(Clone)
