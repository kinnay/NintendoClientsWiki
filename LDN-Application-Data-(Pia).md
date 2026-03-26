The application data field allows the host of an [LDN network](LDN-Protocol) to encode game-specific information into the [advertisement frame](LDN-Protocol#advertisement-frame). This page describes how the application data is structured in games that use the [Pia framework](Pia-Overview).

The application data starts with a short header, which is followed by game-specific application data.

**Note:** in Pia 5.x, the values in this header seem to be stored in little-endian byte order. In Pia 6.x, they are stored in big-endian byte order.

5.2 - 5.7:

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 4 | Session id (random) |
| 0x4 | 4 | CRC32 of user password |
| 0x8 | 1 | [System communication version](#system-communication-version) |
| 0x9 | 3 | Padding |
| 0xC | 8 | Always 0 |
| 0x14 | | [Application data](#application-data) |

5.9 - 5.18:

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 4 | Session id (random) |
| 0x4 | 4 | CRC32 of user password |
| 0x8 | 1 | [System communication version](#system-communication-version) |
| 0x9 | 1 | Header size (24) |
| 0xA | 2 | Padding |
| 0xC | 4 | Session param (random) |
| 0x10 | 8 | Always 0 |
| 0x18 | | [Application data](#application-data) |

5.29 - 5.39:

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 4 | Session id (random) |
| 0x4 | 4 | CRC32 of user password |
| 0x8 | 1 | [System communication version](#system-communication-version) |
| 0x9 | 1 | Header size (16) |
| 0xA | 2 | Padding |
| 0xC | 4 | Session param (random) |
| 0x10 | | [Application data](#application-data) |

6.16 - 6.41:

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 2 | System property data size (0x5C) |
| 0x2 | 1 | [System communication version](#system-communication-version) |
| 0x3 | 2 | Application communication version |
| 0x5 | 16 | User password |
| 0x15 | 1 | Is player limit enabled |
| 0x16 | 1 | Number of players |
| 0x17 | 4 | Player name size |
| 0x1B | 1 | Player name encoding (1 =  UTF-8, 2 = UTF-16) |
| 0x1C | 64 | Player name |
| 0x5C | | [Application data](#application-data) |

### System Communication Version
| Version | Pia Version |
| --- | --- |
| 1 | 5.2 - 5.7 |
| 2 | 5.9 |
| 3 | 5.10 |
| 4 | 5.11 - 5.17 |
| 5 | 5.18 |
| 8 | 5.29 - 5.39 |
| 21 | 6.16 - 6.30 |
| 22 | 6.39 - 6.41 |

### Application Data
The application data depends on the game:

* [Mario Kart 8 Deluxe](#mario-kart-8-deluxe)
* [Super Mario Maker 2](#super-mario-maker-2)

## Mario Kart 8 Deluxe
| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 1 | Unknown |
| 0x1 | 33 | Nickname |
| 0x22 | 2 | Padding |
| 0x24 | 88 | [Mii info] |
| 0x7C | 4 | Unknown |

## Super Mario Maker 2
| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 8 | Network service account id |
| 0x8 | 11x2 | Nickname (wide chars) |
| 0x1E | 2 | Padding |
| 0x20 | 88 | [Mii info] |
| 0x78 | 16 | Unknown |

[Mii info]: Mii-Data-(Switch)