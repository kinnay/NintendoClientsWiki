This page contains information about the Wii U version of Donkey Kong Country: Tropical Freeze.

* [Ranking scores](#ranking-scores)
* [Ranking groups](#ranking-groups)
* [Ranking category ids](#ranking-category-ids)
* [Ranking common data](#ranking-common-data)

## Ranking Scores
The score that is uploaded on the [leaderboards](Ranking-Protocol) consists of the number of frames that were needed in the run, and whether the character got damaged: `(frames << 1) | damaged`. The lower the score, the better.

The game runs at 60 FPS, so the number of seconds that were needed by the run can be calculated by dividing the number of frames by 60.

## Ranking Groups
The first group of a leaderboard entry is unknown. The second group defines which character was used for the run:

| ID | Character |
| --- | --- |
| 0 | Donkey Kong |
| 1 | Diddy Kong |
| 2 | Dixie Kong |
| 3 | Cranky Kong |

## Ranking Category IDs
Donkey Kong identifies objects, including levels, with guids. The category id that is used for the [ranking protocol](Ranking-Protocol) is the first part of the level guid. This table lists all levels in DKC:TF and their category ids.

| Level | Name | Filename | ID |
| --- | --- | --- | --- |
| 1-BOSS | Big Top Bop | b00_mangrove_seaLion | `0x5DD7E214` |
| 1-1 | Mangrove Cove | l01_mangrove_diddy | `0x13759B11` |
| 1-2 | Shipwreck Shore | l02_mangrove_dixie | `0xE3123FD0` |
| 1-3 | Canopy Chaos | l03_mangrove_cranky | `0x912DF205` |
| 1-4 | Trunk Twister | l04_mangrove_minecart | `0x9E391E6D` |
| 1-A | Zip-line Shrine | l0a_mangrove_zips | `0x5B41DCD6` |
| 1-B | Busted Bayou | l0b_mangrove_silhouette | `0x403CF15E` |
| 3-BOSS | Triple Trouble | b00_savannah_baboons | `0x9A479BC2` |
| 3-1 | Grassland Groove | l01_savannah_parade | `0x5A8C9203` |
| 3-2 | Baobab Bonanza | l02_savannah_baobobs | `0x27E351EC` |
| 3-3 | Frantic Fields | l03_savannah_rambi | `0xB2F30301` |
| 3-4 | Scorch 'n' Torch | l04_savannah_fireWater | `0xC3701F2C` |
| 3-5 | Twilight Terror | l05_savannah_rocketBarrel | `0xC44FE9B2` |
| 3-6 | Cannon Canyon | l06_savannah_cannonCanyon | `0x169BCB49` |
| 3-A | Rickety Rafters | l0a_savannah_switches | `0x893EB726` |
| 3-B | Bramble Scramble | l0b_savannah_brambles | `0x1D46C990` |
| 2-BOSS | Mountaintop Tussle | b00_alps_owl | `0x428E1F5B` |
| 2-1 | Windmill Hills | l01_alps_windmills | `0x421F85DE` |
| 2-2 | Mountain Mania | l02_alps_rambi | `0x980638CD` |
| 2-3 | Horn Top Hop | l03_alps_horns | `0x9A9E4578` |
| 2-4 | Sawmill Thrill | l04_alps_minecart | `0x529F713C` |
| 2-5 | Alpine Incline | l05_alps_bridge | `0x229D4B34` |
| 2-6 | Wing Ding | l06_alps_ziplines | `0xDEB25266` |
| 2-A | Crumble Cavern | l0a_alps_cave | `0x9F206066` |
| 2-B | Rodent Ruckus | l0b_alps_rocketBarrel | `0xAD56AF59` |
| 4-BOSS | Fugu Face-off | b00_ocean_fugu | `0xDADEB14A` |
| 4-1 | Deep Keep | l01_ocean_temple | `0xA1137287` |
| 4-2 | High Tide Ride | l02_ocean_minecart | `0xC5BE4809` |
| 4-3 | Amiss Abyss | l03_ocean_silhouette | `0xFE7E5473` |
| 4-4 | Irate Eight | l04_ocean_octopus | `0x7FE2A8DC` |
| 4-5 | Sea Stack Attack | l05_ocean_seaStacks | `0x80469829` |
| 4-6 | Current Capers | l06_ocean_tentacles | `0xD26D5AAA` |
| 4-A | Rockin' Relics | l0a_ocean_poppers | `0xDC9C0EED` |
| 4-B | Shoal Atoll | l0b_ocean_maze | `0x997FB4A2` |
| 5-BOSS | Punch Bowl | b00_juice_polarBash | `0x12C3F595` |
| 5-1 | Harvest Hazards | l01_juice_picking | `0xC484D676` |
| 5-2 | Reckless Ride | l02_juice_rocketBarrel | `0xA002D295` |
| 5-3 | Fruity Factory | l03_juice_slices | `0xECC83B64` |
| 5-4 | Panicky Paddles | l04_juice_flippers | `0x8A33A8A9` |
| 5-5 | Jelly Jamboree | l05_juice_bounce | `0xF0E2800E` |
| 5-6 | Frosty Fruits | l06_juice_slippery | `0x431B4770` |
| 5-A | Beehive Brawl | l0a_juice_clingSwing | `0x6DBE41C2` |
| 5-B | Jammin' Jams | l0b_juice_JamminJams | `0x5CC03A6F` |
| 6-BOSS | Volcano Dome | b00_frozen_warusKing | `0x13AE214C` |
| 6-1 | Homecoming Hijinxs | l01_frozen_jungleHomecoming | `0x773204C6` |
| 6-2 | Seashore War | l02_frozen_beach | `0xC4262903` |
| 6-3 | Aqueduct Assault | l03_frozen_ruins | `0xFE5FD35F` |
| 6-4 | Blurry Flurry | l04_frozen_caveRocketBarrel | `0xE4CB3C45` |
| 6-5 | Forest Folly | l05_frozen_forest | `0xADBE9415` |
| 6-6 | Cliffside Slide | l06_frozen_cliff | `0xC0D23671` |
| 6-7 | Frozen Frenzy | l07_frozen_factory | `0xCBDC7006` |
| 6-8 | Meltdown Mayhem | l08_frozen_volcanoRambi | `0x4EEB52FF` |
| 6-A | Dynamite Dash | l0a_frozen_plungers | `0xF03B8ADE` |
| 6-B | Icicle Arsenal | l0b_frozen_stalactites | `0x6A46C6B5` |
| 7-1 | Levitation Station | l01_secret_jumpingBlocks | `0x3603775F` |
| 7-2 | Rocket Rails | l02_secret_rocketRails | `0x954ABE27` |
| 7-3 | Crazy Clouds | l03_secret_propellers | `0xCBB12D65` |
| 5-K | Platform Problems | l01_trophy_platformbeads | `0x4BEAF6F6` |
| 6-K | Slippy Spikes | l02_trophy_spikefesta | `0x37082275` |
| 4-K | Spinning Spines | l04_trophy_grinders | `0xD94FD2F6` |
| 3-K | Precarious Pendulums | l05_trophy_swingingarms | `0xB1C43F16` |
| 1-K | Swinger Flinger | l06_trophy_vines | `0xDE28ED26` |
| 2-K | Bopopolis | l07_trophy_bopopolis | `0xBC0CD164` |

## Ranking Common Data
The common data that is uploaded along with a score on the leaderboards contains the null-terminated player name.