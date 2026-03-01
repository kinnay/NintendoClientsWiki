[Pia](Pia-Overview) > [Protocols](Pia-Protocols) > Session Protocol (new)
---

This page describes the session protocol that can be found in Pia version 6.x. It seems to be similar to the [[mesh protocol]] that was found in Pia 5.x.

*Added in 6.16 or earlier:*
| Type | Description |
| --- | --- |
| 0 | Join request |
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
| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 1 | Message type (0) |
| 0x1 | 1 | Number of protocols (N) |
| 0x2 | 2 * N | Protocol list (see below) |
| | ... | ... |

The protocol list contains the following for every available protocol.

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 1 | Protocol id |
| 0x1 | 1 | Protocol version |