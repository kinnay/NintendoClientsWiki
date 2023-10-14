Most data is stored in little endian byte order.

## FFLStoreData
| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 0x5C | [FFLiMiiDataOfficial](#fflimiidataofficial) |
| 0x5C | 2 | Unknown |
| 0x5E | 2 | CRC-16 |

## FFLiMiiDataOfficial
| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 0x48 | [FFLiMiiDataCore](#fflimiidatacore) |
| 0x48 | 2 * 10 | Creator name |

## FFLiMiiDataCore
| Bytes | Size | Bits | Description |
| --- | --- | --- | --- |
| 0x0 | 4 | 31 - 28 | Birth platform |
| | | 27 - 24 | Unknown |
| | | 23 - 20 | Unknown |
| | | 19 - 16 | Unknown |
| | | 15 - 12 | Font region |
| | | 11 - 10 | Region move |
| | | 9 | Unknown |
| | | 8 | Is copyable |
| | | 7 - 0 | Mii version |
| 0x4 | 8 | ---| Author ID |
| 0xC | 10 | --- | Create ID |
| 0x16 | 2 | --- | Unknown |
| 0x18 | 2 | 15 | Unknown |
| | | 14 | Unknown |
| | | 13 - 10 | Mii color |
| | | 9 - 5 | Birth day |
| | | 4 - 1 | Birth month |
| | | 0 | Gender (0=male, 1=female) |
| 0x1A | 2 * 10 | --- | Mii name |
| 0x2E | 1 | --- | Size |
| 0x2F | 1 | --- | Fatness |
| 0x30 | 2 | 15 - 12 | Blush type |
| | | 11 - 8 | Face style |
| | | 7 - 5 | Face color |
| | | 4 - 1 | Face type |
| | | 0 | Local only |
| 0x32 | 2 | 15 - 11 | Is hair mirrored |
| | | 10 - 8 | Hair color |
| | | 7 - 0 | Hair type |
| 0x34 | 2 | 15 - 13 | Eye thickness |
| | | 12 - 9 | Eye scale |
| | | 8 - 6 | Eye color |
| | | 5 - 0 | Eye type |
| 0x36 | 2 | 15 - 9 | Eye height |
| | | 8 - 5 | Eye distance |
| | | 4 - 0 | Eye rotation |
| 0x38 | 2 | 15 - 12 | Eyebrow thickness |
| | | 11 - 8 | Eyebrow scale |
| | | 7 - 5 | Eyebrow color |
| | | 4 - 0 | Eyebrow type |
| 0x3A | 2 | 15 - 9 | Eyebrow height |
| | | 8 - 5 | Eyebrow distance |
| | | 4 - 0 | Eyebrow rotation |
| 0x3C | 2 | 15 - 9 | Nose height |
| | | 8 - 5 | Nose scale |
| | | 4 - 0 | Nose type |
| 0x3E | 2 | 15 - 13 | Mouth thickness |
| | | 12 - 9 | Mouth scale |
| | | 8 - 6 | Mouth color |
| | | 5 - 0 | Mouth type |
| 0x40 | 2 | 15 - 8 | Unknown |
| | | 7 - 5 | Mustache type |
| | | 4 - 0 | Mouth height |
| 0x42 | 2 | 15 - 10 | Mustache height |
| | | 9 - 6 | Mustache scale |
| | | 5 - 3 | Beard color |
| | | 2 - 0 | Beard type |
| 0x44 | 2 | 15 - 11 | Glasses height |
| | | 10 - 7 | Glasses scale |
| | | 6 - 4 | Glasses color |
| | | 3 - 0 | Glasses type |
| 0x46 | 2 | 15 | Unknown |
| | | 14 - 10 | Vertical mole position |
| | | 9 - 5 | Horizontal mole position |
| | | 4 - 1 | Mole scale |
| | | 0 | Is mole enabled | 