## Application Data
*Friend session (1.1.0 / v2):*

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 8 | Network service account id |
| 0x8 | 33 | Player name (null terminated) |
| 0x41 | 1 | Unknown |
| 0x42 | 6 | Padding |

*Local session (1.1.0 / v2):*

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 1 | Unknown |
| 0x1 | 33 | Player name (null terminated) |
| 0x22 | 2 | Padding |
| 0x24 | 4 | Unknown |