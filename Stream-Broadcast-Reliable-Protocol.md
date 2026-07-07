[Pia](Pia-Overview) > [Protocols](Pia-Protocols) > Stream Broadcast Reliable Protocol
---

The stream broadcast reliable protocol is meant for larger data streams. A console can request a certain data stream from another console, after which the other console will start transmitting the stream. A [[reliable sliding window]] is used to ensure that all packets arrive in the correct order.

The following version numbers are advertised during the [connection request](Station-Protocol):

| Pia version | Version |
| --- | --- |
| 5.19 | 0 |
| 5.29 | 2 |
| 5.31 - 5.43 | 3 |
| 5.44 - 5.45 | 4 |

### Packet Types
| Type | Description |
| --- | --- |
| 0 | Request stream |
| 1 | Start data |
| 2 | Data |
| 3 | Request failure |
| 4 | Cancel send |
| 5 | Cancel request |
| 6 | Cancel request ack |

### Payload
*5.18 - 5.29:*

The payload contains the following data:

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 1 | [Packet type](#packet-types) |
| 0x1 | 1 | Requested stream id |
| 0x2 | 1 | Progress (in %) |
| 0x3 | 4 | Requested stream size |
| 0x7 | 4 | Payload size |
| 0xB | | Payload |
