[[Pia Protocols]] > Stream Broadcast Reliable Protocol
---

The stream broadcast reliable protocol is meant for larger data streams. A console can request a certain data stream from another console, after which the other console will start transmitting the stream. A [reliable sliding window](Pia-Types#reliableslidingwindow) is used to ensure that all packets arrive in the correct order.

The payload contains the following data:

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 1 | [Packet type](#packet-types) |
| 0x1 | 1 | Requested stream id |
| 0x2 | 1 | Unknown |
| 0x3 | 4 | Requested stream size |
| 0x7 | 4 | Payload size |
| 0xB | | Payload |

### Packet Types
| Type | Description |
| --- | --- |
| 0 | Request stream |
| 3 | Request mismatch |