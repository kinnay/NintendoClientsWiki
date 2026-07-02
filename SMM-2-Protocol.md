SMM 2 uses [ENL](ENL-Protocol).

### Application Data
| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 8 | Always 0 |
| 0x8 | 24 | Player name (UTF-16-LE) |
| 0x20 | 88 | [Mii](Mii-Data-(Switch)) |
| 0x78 | 16 | Padding |

### Matching Packet

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 4 | State |
| 0x4 | 4 | Padding |
| 0x8 | 8 | NSA ID |
| 0x10 | 16 | UUID |
| 0x20 | 11 x 2 | Name |
| 0x36 | 2 | Padding |
| 0x38 | 88 | [Mii](Mii-Data-(Switch)) |
| 0x90 | 2 | Top number |
| 0x92 | 2 | Bottom number |
| 0x94 | 2 | Headwear number |
| 0x96 | 2 | Anim number |
| 0x98 | 4 | Related to battle mode rating |
| 0x9C | 1 | Related to battle mode rating |
| 0x9D | 3 | Padding |
| 0xA0 | 4 | Unknown |
| 0xA4 | 4 | Unknown |
| 0xA8 | 4 | Unknown |
| 0xAC | 4 | Unknown |
| 0xB0 | 4 | Random value |
| 0xB4 | 1 | 0 = Battle, 1 = Coop |
| 0xB5 | 3 | Padding |
| 0xB8 | 4 | Always 4 |
| 0xBC | 4 | Unknown |

### Thumbnail Packet
| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 0x1BF9C | Thumbnail (JPEG) |
| 0x1BF9C | 4 | Thumbnail size (always 0x1BF9C) |
| 0x1BFA0 | 32 | HMAC-SHA256 of JPEG data |
| 0x1BFC0 | 16 | RNG state for key generation |
| 0x1BFD0 | 48 | Padding (always 0) |