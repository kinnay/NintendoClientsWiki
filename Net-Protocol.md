[Pia](Pia-Overview) > [Protocols](Pia-Protocols) > Net Protocol
---

This page describes the net protocol that can be found in Pia 6.x.

This protocol is the successor of the [[local protocol]] that was found in Pia 5.x. Unlike the local protocol, the net protocol is used for all network types and not just LDN. Its feature set has also expanded a bit.

## Message Types
| Type | Description |
| --- | --- |
| 0x11 | [Update network connection status](#update-network-connection-status) |
| 0x12 | Update network connection status ack |
| 0x13 | Destroy network |
| 0x20 | Network property request |
| 0x21 | Network property response |
| 0x30 | Disconnect network |
| 0x31 | Disconnect network ack |
| 0x32 | Connect network |
| 0x33 | Connect network ack |
| 0x40 | Start host migration |
| 0x41 | Update network host |
| 0x50 | Update network property |
| 0x51 | Update network property ack
| 0x80 | Keep alive network |
| 0x81 | Keep alive network ack |

The network property request and response messages were later renamed to session property request and response.

## Net Message Header
| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 1 | Header version |
| 0x1 | 1 | [Message type](#message-types) |
| 0x2 | 2 | Payload size |

## Update Network Connection Status
| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 4 | [Net message header](#net-message-header) |
| 0x4 | 4 | Sequence id |
| 0x8 | 2 | Host [variable id] |
| 0xA | 8 | Host [constant id] |
| 0x12 | 8 | Network id |
| 0x1A | 1 | Is network open |
| 0x1B | 2 | Station list size |
| 0x1D | 1 | Is migrating host |
| 0x1E | | Payload |

[constant id]: Pia-Types#constant-id
[variable id]: Pia-Types#variable-id