This page describes the protocol behind the Animal Crossing: New Horizons island transfer tool. The tool uses [ENL](ENL-Protocol) with the following custom record types:

| ID | Description |
| --- | --- |
| 2 | Peer info |
| 3 | Peer info ack |
| 4 | Network state |
| 5 | Streaming |
| 6 | Unknown |

Record type 0 and 1 seem to be unused. This suggests that they are either only present in a debug build, or they were present in an early version of the tool but later removed.

In addition, the following stream ids are used for the [[stream broadcast reliable protocol]]:

| ID | Description |
| --- | --- |
| 0 | Unknown |
| 1 | Unknown |
| 2 | Unknown |
| 3 | Unknown |
| 4 | Unknown |
| 5 | Unknown |
| 6 | Unknown |
| 7 | Unknown |
| 8 | Unknown |
| 9 | Unknown |
| 10 | Unknown |
| 11 | Unknown |
| 12 | Unknown |
| 13 | Unknown |
| 14 | Unknown |
| 15 | Unknown |
| 16 | Unknown |
| 17 | Unknown |
| 18 | Unknown |
| 19 | Unknown |
| 20 | Unknown |

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
This record seems to hold information about the state of the network.

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 1 | Unknown |
| 0x1 | 1 | Unknown |
| 0x2 | 1 | Unknown |

## Record Type 5
This record contains information about the [[stream broadcast reliable protocol]].

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 4 | Some kind of mask |
| 0x4 | 4 | Stream size |
| 0x8 | 1 | Unknown |
| 0x9 | 1 | Unknown |
| 0xA | 1 | Unknown |
| 0xB | 1 | Sequence id |

## Record Type 6
| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 4 | Unknown |
| 0x4 | 4 | Unknown |