This page describes the protocol behind the Animal Crossing: New Horizons island transfer tool. The tool uses [ENL](ENL-Protocol) with the following custom record types:

| ID | Description |
| --- | --- |
| 2 | Peer info |
| 3 | Peer info ack |
| 4 | Unknown |
| 5 | Unknown |
| 6 | Unknown |

## Record Type 2
This record contains information about the peers that are connected to the network. Interestingly, this record has room for up to 8 peers, even though the underlying LDN network only allows two nodes to be connected at once.

The sequence id seems to be incremented whenever something changes.

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 4 | Sequence id |
| 0x4 | 9 * 8 | Peers (8x) |
| 0x4C | 1 * 8 | Flags (8x) |

Every peer entry has the following fields:

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 8 | [Constant id](Pia-Types#constant-id) |
| 0x8 | 1 | Unknown |

## Record Type 3
This record seems to be used to notify the host that the peer info has been received.

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 4 | Sequence id received from record type 2 |
| 0x4 | 1 | Always 0? |
| 0x5 | 3 | Padding |

## Record Type 4
| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 3 | Unknown |

## Record Type 5
| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 12 | Unknown |

## Record Type 6
| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 8 | Unknown |