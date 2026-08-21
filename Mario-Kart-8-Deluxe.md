[Switch](Home#switch-games) > Mario Kart 8 Deluxe
---

This page contains information about Mario Kart 8 Deluxe.

* [Ranking](#ranking)
  * [Score](#score)
  * [Category ids](#category-ids)
  * [Common data](#common-data)

## Ranking
This section describes how Mario Kart 8 Deluxe uses the [ranking protocol](Ranking-Protocol).

### Score
The score that is uploaded on the leaderboards is simply the number of milliseconds that were taken by the run.

### Category IDs
The category ids are the same as the category ids of [Mario Kart 8](Mario-Kart-8) but with 16 subtracted from them.

| Cup | Track | ID (decimal) |
| --- | --- | --- |
| Mushroom | Mario Kart Stadium | 11 |
| Mushroom | Water Park | 12 |
| Mushroom | Sweet Sweet Canyon | 3 |
| Mushroom | Thwomp Ruins | 1 |
||
| Flower | Mario Circuit | 0 |
| Flower | Toad Harbor | 2 |
| Flower | Twisted Mansion | 4 |
| Flower | Shy Guy Falls | 5 |
||
| Star | Sunshine Airport | 10 |
| Star | Dolphin Shoals | 13 |
| Star | Electrodrome | 9 |
| Star | Mount Wario | 8 |
||
| Special | Cloudtop Cruise | 7 |
| Special | Bone-Dry Dunes | 6 |
| Special | Bowser's Castle | 14 |
| Special | Rainbow Road | 15 |
||
| Shell | Wii Moo Moo Meadows | 17 |
| Shell | GBA Mario Circuit | 22 |
| Shell | DS Cheep Cheep Beach | 20 |
| Shell | N64 Toad's Turnpike | 19 |
||
| Banana | GCN Dry Dry Desert | 26 |
| Banana | SNES Donut Plains 3 | 25 |
| Banana | N64 Royal Raceway | 18 |
| Banana | 3DS DK Jungle | 16 |
||
| Leaf | DS Wario Stadium | 30 |
| Leaf | GCN Sherbet Land | 21 |
| Leaf | 3DS Music Park | 23 |
| Leaf | N64 Yoshi Valley | 29 |
||
| Lightning | DS Tick-Tock Clock | 28 |
| Lightning | 3DS Piranha Plant Slide | 27 |
| Lightning | Wii Grumble Volcano | 24 |
| Lightning | N64 Rainbow Road | 31 |
||
| Egg | GCN Yoshi Circuit | 40 |
| Egg | Excitebike Arena | 37 |
| Egg | Dragon Driftway | 34 |
| Egg | Mute City | 33 |
||
| Triforce | Wii Wario's Gold Mine | 41 |
| Triforce | SNES Rainbow Road | 42 |
| Triforce | Ice Ice Outpost | 39 |
| Triforce | Hyrule Circuit | 35 |
||
| Crossing | GCN Baby Park | 45 |
| Crossing | GBA Cheese Land | 46 |
| Crossing | Wild Woods | 38 |
| Crossing | Animal Crossing | 36 |
||
| Bell | 3DS Neo Bowser City | 44 |
| Bell | GBA Ribbon Road | 43 |
| Bell | Super Bell Subway | 32 |
| Bell | Big Blue | 47 |

### Common Data
| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 4 | Unknown, seen values include `0`, `52460000` (`RF`), `584d0000` (`XM`) and `52420000` (`RB`) |
| 0x4 | 88 | [Mii data](Mii-Data-(Switch)) |
| 0x5C | 4 | Unknown |
| 0x60 | 36 | In-game nickname (UTF-8, null-terminated) |