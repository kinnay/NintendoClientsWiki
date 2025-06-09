This page describes some data structures that are seen in Mario Kart 8.

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