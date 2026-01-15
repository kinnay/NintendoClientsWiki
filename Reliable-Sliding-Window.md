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
| 0x9 | 8*N | Multicast [constant ids](#constant-id) |
| | | Payload |

*5.29 - 5.31:*

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 1 | [Flags](#flags) |
| 0x1 | 1 | Stream id |
| 0x2 | 2 | Payload size |
| 0x4 | 2 | Sequence id |
| 0x6 | 2 | Unknown |
| 0x8 | 1 | Unknown |
| 0x9 | 4*N | Unknown |
| | | Payload |

### Flags
| Flag | Description |
| --- | --- |
| 1 | Has payload |
| 2 | First fragment |
| 4 | Last fragment |
| 8 | Is initialize |
| 16 | Is compressed |
| 32 | Reset |
| 64 | Reset ack |
