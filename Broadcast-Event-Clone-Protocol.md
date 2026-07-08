[Pia](Pia-Overview) > [Protocols](Pia-Protocols) > Broadcast Event (Clone)
---

This page describes the broadcast event protocol of Pia clone. Messages are wrapped in a [[reliable sliding window]].

The following version numbers are advertised during the [connection request](Station-Protocol):

| Pia Version | Version |
| --- | --- |
| 5.43 | 9 |

*7.0:*

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 1 | Message type |
| 0x1 | 2 | Unknown |
| 0x3 | 2 | Unknown |
| 0x5 | 2 | Payload size |
| 0x7 | 2 | Unknown |
| 0x9 | | Payload |