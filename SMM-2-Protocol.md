SMM 2 uses [ENL](ENL-Protocol). After a client has joined the mesh, it sends the following packet to the master station through the [reliable protocol](Reliable-Protocol).

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 4 | Packet type (1) |
| 0x4 | 4 | Padding |
| 0x8 | 8 | NSA ID |
| 0x10 | 16 | UUID |
| 0x20 | 11 x 2 | Name |
| 0x36 | 2 | Padding |
| 0x38 | 88 | [Mii](Mii-Data-(Switch)) |
| 0x90 | 2 | Unknown |
| 0x92 | 2 | Unknown |
| 0x94 | 2 | Unknown |
| 0x96 | 2 | Unknown |
| 0x98 | 4 | Unknown |
| 0x9C | 1 | Unknown |
| 0x9D | 3 | Padding |
| 0xA0 | 4 | Unknown |
| 0xA4 | 4 | Unknown |
| 0xA8 | 4 | Unknown |
| 0xAC | 4 | Unknown |
| 0xB0 | 4 | Random value |
| 0xB4 | 1 | Always 1 |
| 0xB5 | 3 | Padding |
| 0xB8 | 4 | Always 4 |
| 0xBC | 4 | Unknown |