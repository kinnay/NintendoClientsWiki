This page describes the protocol behind the Animal Crossing: New Horizons island transfer tool. The tool uses [ENL](ENL-Protocol) with the following custom record types:

| ID | Description |
| --- | --- |
| 2 | Peer info |
| 3 | Peer info ack |
| 4 | Network state |
| 5 | Streaming |
| 6 | Unknown |

Record type 0 and 1 seem to be unused.

In addition, the following stream ids are used for the [[stream broadcast reliable protocol]]:

| ID | Description |
| --- | --- |
| 17 | Save data |

Note: theoretically, the implementation seems to support stream id 0 up to 20. But only 17 seems to be used. This is likely because some of the code of the tool is shared with the real game.

## Application Data
The following application data is broadcasted by the Pia session:

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 2 | Version (1) |
| 0x2 | 129 | Device name (UTF-8) |
| 0x83 | 64 | `nn::oe::LaunchRequiredVersion` |
| 0xC3 | 5 | Padding |
| 0xC8 | 8 | Save data usable size |
| 0xD0 | 8 | Save data journal size |
| 0xD8 | 1 | Has land name |
| 0xD9 | 1 | Padding |
| 0xDA | 2 * 11 | Land name (UTF-16) |
| 0xF0 | 1 | Unknown value related to land name |
| 0xF1 | 7 | Padding |
| 0xF8 | 8 | Total file size |
| 0x100 | 4 | Number of files |
| 0x104 | 1 | Save data restore flag |
| 0x105 | 3 | Padding |

## Record Type 2
This record contains information about the peers that are connected to the network. Interestingly, this record has room for up to 8 peers, even though the underlying LDN network only allows two nodes to be connected at once. This is likely because some of the code of the tool is shared with the real game.

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

## Stream Type 17
This stream type transmits the save data. The data is encoded in little endian byte order.

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 4 | Murmur hash of payload |
| 0x4 | 4 | Always 120 (`x`) |
| 0x8 | 4 | Always 109 (`m`) |
| 0xC | 256 | Filename (ascii) |
| 0x10C | 1 | Is last file |
| 0x10D | 3 | Padding |
| 0x110 | | Payload |