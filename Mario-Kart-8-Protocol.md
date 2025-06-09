Mario Kart 8 uses the [ENL framework](ENL-Protocol).

| Record type | Description |
| --- | --- |
| 0 | [Menu](#record-type-0) |
| 1 | Player info |
| 2 | [All player info](#record-type-2) |
| 3 | Race |
| 4 | Drive |
| 6 | Item event |
| 7 | Battle event |
| 9 | [Flags](#record-type-9) |
| 10 | Chat |

## Record Type 0
| Offset | Type | Description |
| --- | --- | --- |
| 0x0 | [PlayerInfo](#playerinfo) (x12) | Players |
| 0x90 | [PlayerId](#playerid) | Unknown |
| 0x98 | Uint32 | Flags |
| 0x9C | --- | End of record |

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

## PlayerId
| Offset | Type | Description |
| --- | --- | --- |
| 0x0 | Uint32 | Station index |
| 0x4 | Unk (4) | Unknown |

## PlayerInfo
| Offset | Type | Description |
| --- | --- | --- |
| 0x0 | [UniqueID](ENL-Protocol#uniqueid) | Unique id |
| 0x8 | 1 | Voted course:<br>`0xFE`: voted course<br>`0x01`: unknown |
| 0x9 | 3 | Padding |