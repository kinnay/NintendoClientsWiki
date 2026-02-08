The reliable sliding window ensures that all packets arrive and in the correct order. Large messages are fragmented. The reliable sliding window is used by the following protocols:

* [[Mesh protocol]]
* Session protocol
* [[Reliable protocol]]
* [[Broadcast reliable protocol]]
* [[Stream broadcast reliable protocol]]

When a reliable sliding window is used, messages are wrapped as follows:

*Up to 5.12:*

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 2 | [Flags](#flags) |
| 0x2 | 2 | Payload size |
| 0x4 | 4 | Padding |
| 0x8 | 4 | Sequence id |
| 0xC | 4 | Acknowledgement id |
| 0x10 | 8 | Extra acknowledgements |
| 0x18 | | Payload |

*5.14:*
| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 2 | [Flags](#flags) |
| 0x2 | 2 | Payload size |
| 0x4 | 2 | Sequence id |
| 0x6 | 8 | Unknown |
| 0xE | 8 | Unknown |
| 0x16 | | Payload |

*5.17 - 5.19:*

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 1 | [Flags](#flags) |
| 0x1 | 1 | Stream id |
| 0x2 | 2 | Payload size |
| 0x4 | 2 | Sequence id |
| 0x6 | 2 | Lowest sequence id pending ack |
| 0x8 | 1 | Number of multicast constant ids (N) |
| 0x9 | 8*N | Multicast [constant ids](Pia-Types#constant-id) |
| | | Payload |

*5.29 - 5.31:*

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 1 | [Flags](#flags) |
| 0x1 | 1 | Stream id |
| 0x2 | 2 | Payload size |
| 0x4 | 2 | Sequence id |
| 0x6 | 2 | Lowest sequence id pending ack |
| 0x8 | 1 | Number of multicast constant ids (N) |
| 0x9 | 4*N | Multicast [constant ids](Pia-Types#constant-id) |
| | | Payload |

### Flags
| Flag | Description |
| --- | --- |
| 1 | Application data |
| 2 | Message start (first fragment) |
| 4 | Message end (last fragment) |
| 8 | Is initialized |
| 16 | The payload is zlib compressed |
| 32 | Reset |
| 64 | Reset ack |

## Ack Data
When the application data flag is not set, the payload contains bulk acknowledgement information.

*5.18:*

The payload contains 32 copies of the following struct:

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 1 | Stream id |
| 0x1 | 2 | Acknowledgement id |
| 0x3 | 16 | Acknowledgement mask |

All sequence ids up to the acknowledgement id are marked as received. In addition, the acknowledgement mask allows up to 128 sequence ids behind a gap to be acknowledged. If `ack_mask & (1 << index)` is set, then `ack_id + 1 + index` is marked as received.
