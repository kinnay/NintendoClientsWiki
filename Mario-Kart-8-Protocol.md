Mario Kart 8 uses the [ENL framework](ENL-Protocol).

| Record type | Description |
| --- | --- |
| 0 | [Menu](#record-type-0) |
| 1 | [Player info](#record-type-1) |
| 2 | [All player info](#record-type-2) |
| 3 | Race |
| 4 | Drive |
| 6 | Item event |
| 7 | Battle event |
| 9 | [Flags](#record-type-9) |
| 10 | Chat |

## Record Type 0
| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 12*12 | Player [votes](#vote) |
| 0x90 | 12 | [Vote](#vote) chosen by roulette |
| 0x9C | --- | End of record |

## Record Type 1
| Offset | Type | Description |
| --- | --- | --- |
| 0x0 | Unk (0x10C) | Unknown |
| 0x10C | --- | End of record |

## Record Type 2
| Offset | Type | Description |
| --- | --- | --- |
| 0x0 | Unk (8*12) | Unknown |
| 0x60 | Uint32 (x4) | [Track options](Mario-Kart-8-Track-IDs) |
| 0x70 | Uint32 | Unknown |
| 0x74 | Uint32 | Unknown |
| 0x78 | [PlayerInfo](#playerinfo) (x12) | Players |
| 0x108 | Unk (8*10) | Unknown |
| 0x158 | Uint16 | Unknown |
| 0x15A | Uint16 | Unknown |
| 0x15C | Unk (4) | Unknown |
| 0x160 | --- | End of record |

## Record Type 9
| Offset | Type | Description |
| --- | --- | --- |
| 0x0 | Uint8 | Unknown |
| 0x1 | --- | End of record |

## Vote
| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 8 | [Unique id](ENL-Protocol#uniqueid)
| 0x8 | 1 | `0xFE`: course id<br>`0x01`: unknown |
| 0x9 | 3 | Padding |

## sys::PlayerInfo
| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 212 | [Core](#sysplayerinfocore) |
| 0xD4 | 2*21 | Null-terminated name (UTF-16) |
| 0xFE | 2 | Padding |

## sys::PlayerInfo::Core
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

## sys::Rate
| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 4 | Value (float) |

## sys::OpenFlagPack
| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 0x40 | Unknown |