[Pia](Pia-Overview) > [Protocols](Pia-Protocols) > Net Protocol
---

This page describes the net protocol that can be found in Pia 6.x.

Every message starts with the following header:

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 1 | Header version |
| 0x1 | 1 | [Message type](#message-types) |
| 0x2 | 2 | Payload size |
| 0x4 | | Payload |

## Message Types
| Type | Description |
| --- | --- |
| 0x11 | Update network connection status |
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
