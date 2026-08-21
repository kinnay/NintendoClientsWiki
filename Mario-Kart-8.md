[Wii U](Home#wii-u-games) > Mario Kart 8
---

This page contains information about the Wii U version of Mario Kart 8.

* [Ranking](#ranking)
  * [Score](#score)
  * [Category ids](#category-ids)
* [Peer to peer](#peer-to-peer)

## Ranking
This section describes how Mario Kart 8 uses the [ranking protocol](Ranking-Protocol).

### Score
The score that is uploaded on the leaderboards is simply the number of milliseconds that were taken by the run.

### Category IDs
| Cup | Track | ID (decimal) |
| --- | --- | --- |
| Mushroom | Mario Kart Stadium | 27 |
| Mushroom | Water Park | 28 |
| Mushroom | Sweet Sweet Canyon | 19 |
| Mushroom | Thwomp Ruins | 17 |
||
| Flower | Mario Circuit | 16 |
| Flower | Toad Harbor | 18 |
| Flower | Twisted Mansion | 20 |
| Flower | Shy Guy Falls | 21 |
||
| Star | Sunshine Airport | 26 |
| Star | Dolphin Shoals | 29 |
| Star | Electrodrome | 25 |
| Star | Mount Wario | 24 |
||
| Special | Cloudtop Cruise | 23 |
| Special | Bone-Dry Dunes | 22 |
| Special | Bowser's Castle | 30 |
| Special | Rainbow Road | 31 |
||
| Shell | Wii Moo Moo Meadows | 33 |
| Shell | GBA Mario Circuit | 38 |
| Shell | DS Cheep Cheep Beach | 36 |
| Shell | N64 Toad's Turnpike | 35 |
||
| Banana | GCN Dry Dry Desert | 42 |
| Banana | SNES Donut Plains 3 | 41 |
| Banana | N64 Royal Raceway | 34 |
| Banana | 3DS DK Jungle | 32 |
||
| Leaf | DS Wario Stadium | 46 |
| Leaf | GCN Sherbet Land | 37 |
| Leaf | 3DS Music Park | 39 |
| Leaf | N64 Yoshi Valley | 45 |
||
| Lightning | DS Tick-Tock Clock | 44 |
| Lightning | 3DS Piranha Plant Slide | 43 |
| Lightning | Wii Grumble Volcano | 40 |
| Lightning | N64 Rainbow Road | 47 |
||
| Egg | GCN Yoshi Circuit | 56 |
| Egg | Excitebike Arena | 53 |
| Egg | Dragon Driftway | 50 |
| Egg | Mute City | 49 |
||
| Triforce | Wii Wario's Gold Mine | 57 |
| Triforce | SNES Rainbow Road | 58 |
| Triforce | Ice Ice Outpost | 55 |
| Triforce | Hyrule Circuit | 51 |
||
| Crossing | GCN Baby Park | 61 |
| Crossing | GBA Cheese Land | 62 |
| Crossing | Wild Woods | 54 |
| Crossing | Animal Crossing (1) | 52 |
| Crossing | Animal Crossing (2) | 64 |
| Crossing | Animal Crossing (3) | 65 |
| Crossing | Animal Crossing (4) | 66 |
||
| Bell | 3DS Neo Bowser City | 60 |
| Bell | GBA Ribbon Road | 59 |
| Bell | Super Bell Subway | 48 |
| Bell | Big Blue | 63 |

## Peer to Peer
Mario Kart 8 uses the [ENL framework](ENL-Protocol) for peer to peer communication.

| Record type | Description |
| --- | --- |
| 0 | [Menu](#menu-record) |
| 1 | [Player info](#player-info-record) |
| 2 | [All player info](#all-player-info-record) |
| 3 | Race |
| 4 | Drive |
| 6 | Item event |
| 7 | Battle event |
| 9 | [Flags](#flags-record) |
| 10 | Chat |

### Menu Record
This is record type 0.

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 12*12 | Player [votes](#vote) |
| 0x90 | 12 | [Vote](#vote) chosen by roulette |
| 0x9C | --- | End of record |

### Player Info Record
This is record type 1.

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 8 | Unknown |
| 0x8 | 256 | [Player info](#sysplayerinfo) |
| 0x108 | 4 | Unknown |
| 0x10C | --- | End of record |

### All Player Info Record
This is record type 2.

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 8*12 | Unknown |
| 0x60 | 4*4 | [Track options](Mario-Kart-8-Track-IDs) |
| 0x70 | 4 | Unknown |
| 0x74 | 4 | Unknown |
| 0x78 | 12*12 | [Votes](#vote) |
| 0x108 | 8*10 | Unknown |
| 0x158 | 2 | Unknown |
| 0x15A | 2 | Unknown |
| 0x15C | 4 | Unknown |
| 0x160 | --- | End of record |

### Flags Record
This is record type 9.

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 1 | Flags |
| 0x1 | --- | End of record |

### Vote
| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 8 | [Unique id](ENL-Protocol#uniqueid)
| 0x8 | 1 | `0xFE`: course id<br>`0x01`: unknown |
| 0x9 | 3 | Padding |

### sys::PlayerInfo
| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 212 | [Core](#sysplayerinfocore) |
| 0xD4 | 2*21 | Null-terminated name (UTF-16) |
| 0xFE | 2 | Padding |

### sys::PlayerInfo::Core
| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 4 | Unknown |
| 0x4 | 4 | Unknown |
| 0x8 | 4 | Unknown |
| 0xC | 4 | [Rate 1](#sysrate) |
| 0x10 | 4 | [Rate 2](#sysrate) |
| 0x14 | 96 | [Mii data](Mii-Data-(Wii-U)) |
| 0x74 | 16 | Unknown |
| 0x84 | 64 | [Open flag pack](#sysopenflagpack) |
| 0xC4 | 16 | Account UUID |

### sys::Rate
| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 4 | Value (float) |

### sys::OpenFlagPack
| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 0x40 | Unknown |