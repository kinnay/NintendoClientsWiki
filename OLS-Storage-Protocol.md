## [NEX-Protocols](https://github.com/kinnay/NintendoClients/wiki/NEX-Protocols) > OLS Storage

| Method ID | Method Name |
| --- | --- |
| 1 | [LoadVersion](#1-loadversion) |
| 2 | [SaveLocale](#2-savelocale) |
| 3 | [SaveProfile](#3-saveprofile) |
| 4 | [LoadIDCard](#4-loadidcard) |
| 5 | [QueryFriendProfiles](#5-queryfriendprofiles) |
| 6 | [QueryUbisoftProfiles](#6-queryubisoftprofiles) |
| 7 | [CreateMessage](#7-createmessage) |
| 8 | [QueryMessage](#8-querymessage) |
| 9 | [QueryLeaderboard](#9-queryleaderboard) |
| 10 | [QuerySmartSelection](#10-querysmartselection) |
| 11 | [SaveScore](#11-savescore) |
| 12 | [SaveGhost](#12-saveghost) |
| 13 | [QueryCompetitionsInfos](#13-querycompetitionsinfos) |
| 14 | [QueryCompetitionsHistory](#14-querycompetitionshistory) |
| 15 | [QueryCompetitionOfTheDay](#15-querycompetitionoftheday) |
| 16 | [QueryCompetition](#16-querycompetition) |

# (1) LoadVersion

## Request
This method does not take any parameters

## Response
| Type | Name |
| --- | --- |
| Sint32 | version |
| [String](https://github.com/kinnay/NintendoClients/wiki/NEX-Common-Types#string) | sandboxName |

# (2) SaveLocale

## Request
| Type | Name |
| --- | --- |
| [String](https://github.com/kinnay/NintendoClients/wiki/NEX-Common-Types#string) | localeCode |

## Response
This method does not return anything

# (3) SaveProfile

## Request
| Type | Name |
| --- | --- |
| Uint32 | update_bitfield |
| Sint8 | level |
| Sint32 | currency |
| Uint32 | costume |
| Uint16 | bronze_medals |
| Uint16 | silver_medals |
| Uint16 | gold_medals |
| Uint16 | diamond_medals |
| Uint32 | run_distance |
| Uint16 | teensies_freed |
| Uint32 | jumps |
| Uint16 | unlocked_pets |
| Uint64 | pets |
| Uint16 | unlocked_costumes |

## Response
| Type | Name |
| --- | --- |
| Uint16 | competition_medals_0 |
| Uint16 | competition_medals_1 |
| Uint16 | competition_medals_2 |
| Uint16 | competition_medals_3 |

# (4) LoadIDCard

## Request
| Type | Name |
| --- | --- |
| Uint32 | pid |

## Response
| Type | Name |
| --- | --- |
| [OLSRichProfile](#olsrichprofile-structure) | profile |

# (5) QueryFriendProfiles

## Request
| Type | Name |
| --- | --- |
| [List](https://github.com/kinnay/NintendoClients/wiki/NEX-Common-Types#list)&#x3C;[OLSFriend](#olsfriend-structure)&#x3E; | friends |

## Response
| Type | Name |
| --- | --- |
| [List](https://github.com/kinnay/NintendoClients/wiki/NEX-Common-Types#list)&#x3C;[OLSProfile](#olsprofile-structure)&#x3E; | profiles |

# (6) QueryUbisoftProfiles

## Request
This method does not take any parameters

## Response
| Type | Name |
| --- | --- |
| [List](https://github.com/kinnay/NintendoClients/wiki/NEX-Common-Types#list)&#x3C;[OLSProfile](#olsprofile-structure)&#x3E; | profiles |

# (7) CreateMessage

## Request
| Type | Name |
| --- | --- |
| Uint32 | message_type |
| [List](https://github.com/kinnay/NintendoClients/wiki/NEX-Common-Types#list)&#x3C;Sint32&#x3E; | receivers |
| [List](https://github.com/kinnay/NintendoClients/wiki/NEX-Common-Types#list)&#x3C;[OLSAttribute](#olsattribute-structure)&#x3E; | attributes |

## Response
This method does not return anything

# (8) QueryMessage

## Request
This method does not take any parameters

## Response
| Type | Name |
| --- | --- |
| [List](https://github.com/kinnay/NintendoClients/wiki/NEX-Common-Types#list)&#x3C;[OLSMessage](#olsmessage-structure)&#x3E; | messages |

# (9) QueryLeaderboard

## Request
| Type | Name |
| --- | --- |
| Uint32 | id_leaderboard |

## Response
| Type | Name |
| --- | --- |
| [List](https://github.com/kinnay/NintendoClients/wiki/NEX-Common-Types#list)&#x3C;[OLSLdbRow](#olsldbrow-structure)&#x3E; | result |
| [List](https://github.com/kinnay/NintendoClients/wiki/NEX-Common-Types#list)&#x3C;Float&#x3E; | graduations |
| [List](https://github.com/kinnay/NintendoClients/wiki/NEX-Common-Types#list)&#x3C;Uint32&#x3E; | envelope |
| Uint32 | unit |
| Uint32 | my_country |
| Uint32 | participants |
| Bool | cacheable |

# (10) QuerySmartSelection

## Request
| Type | Name |
| --- | --- |
| Uint32 | id_leaderboard |

## Response
| Type | Name |
| --- | --- |
| [List](https://github.com/kinnay/NintendoClients/wiki/NEX-Common-Types#list)&#x3C;[OLSSelectionRow](#olsselectionrow-structure)&#x3E; | ghosts |
| [List](https://github.com/kinnay/NintendoClients/wiki/NEX-Common-Types#list)&#x3C;[OLSTomb](#olstomb-structure)&#x3E; | tombs |

# (11) SaveScore

## Request
| Type | Name |
| --- | --- |
| Uint32 | id_leaderboard |
| Bool | is_objective_reached |
| Float | score |
| Float | tomb_x |
| Float | tomb_y |
| Float | tomb_z |
| Uint32 | id_costume |

## Response
| Type | Name |
| --- | --- |
| Bool | save_score |
| Bool | retry |
| Uint32 | medal |
| [String](https://github.com/kinnay/NintendoClients/wiki/NEX-Common-Types#string) | message_medal |
| [String](https://github.com/kinnay/NintendoClients/wiki/NEX-Common-Types#string) | message_friends |

# (12) SaveGhost

## Request
| Type | Name |
| --- | --- |
| Uint64 | id_ghost |
| Uint32 | id_competition |
| Uint32 | id_costume |
| Float | score |

## Response
This method does not return anything

# (13) QueryCompetitionsInfos

## Request
This method does not take any parameters

## Response
| Type | Name |
| --- | --- |
| [List](https://github.com/kinnay/NintendoClients/wiki/NEX-Common-Types#list)&#x3C;[OLSCompetitionInfos](#olscompetitioninfos-structure)&#x3E; | infos |

# (14) QueryCompetitionsHistory

## Request
| Type | Name |
| --- | --- |
| Uint32 | begin |
| Uint32 | amount |
| Uint32 | id_competition_meta |

## Response
| Type | Name |
| --- | --- |
| [List](https://github.com/kinnay/NintendoClients/wiki/NEX-Common-Types#list)&#x3C;[OLSCompetitionResult](#olscompetitionresult-structure)&#x3E; | history |
| Uint32 | total |

# (15) QueryCompetitionOfTheDay

## Request
| Type | Name |
| --- | --- |
| Uint32 | id_competition_meta |

## Response
| Type | Name |
| --- | --- |
| [OLSCompetition](#olscompetition-structure) | competition |
| Uint32 | remaningSeconds |
| [OLSCompetition](#olscompetition-structure) | tomorrow |

# (16) QueryCompetition

## Request
| Type | Name |
| --- | --- |
| Uint32 | id_competition |

## Response
| Type | Name |
| --- | --- |
| [OLSCompetition](#olscompetition-structure) | competition |

# Types

## OLSProfile ([Structure](https://github.com/kinnay/NintendoClients/wiki/NEX-Common-Types#structure))
| Type | Name |
| --- | --- |
| Sint32 | PID |
| [String](https://github.com/kinnay/NintendoClients/wiki/NEX-Common-Types#string) | PlatformID |
| [String](https://github.com/kinnay/NintendoClients/wiki/NEX-Common-Types#string) | Name |
| Uint32 | costume |
| Uint32 | country |
| Sint8 | level |

## OLSRichProfile ([Structure](https://github.com/kinnay/NintendoClients/wiki/NEX-Common-Types#structure))
| Type | Name |
| --- | --- |
| Sint32 | PID |
| [String](https://github.com/kinnay/NintendoClients/wiki/NEX-Common-Types#string) | Name |
| [String](https://github.com/kinnay/NintendoClients/wiki/NEX-Common-Types#string) | PlatformID |
| Sint16 | Country |
| Uint32 | StatusIcon |
| Uint32 | lastCostume |
| Uint16 | totalChallengePlayed |
| Bool | dailyPlayed |
| Bool | weeklyPlayed |
| Bool | dailyExpertPlayed |
| Bool | weeklyExpertPlayed |
| Uint16 | DiamondMedals |
| Uint16 | GoldMedals |
| Uint16 | SilverMedals |
| Uint16 | BronzeMedals |
| Uint32 | GlobalMedalsRank |
| Uint32 | GlobalMedalsMaxRank |
| Float | distanceRun |
| Uint32 | rank_distanceRun |
| Float | lums |
| Uint32 | rank_lums |
| Float | pets |
| Uint32 | rank_pets |
| Float | teensies |
| Uint32 | rank_teensies |
| Float | jumps |
| Uint32 | rank_jumps |
| Float | costumes |
| Uint32 | rank_costumes |
| Float | stat_daily |
| Uint32 | rank_daily |
| Sint8 | unit_daily |
| Float | stat_weekly |
| Uint32 | rank_weekly |
| Sint8 | unit_weekly |
| Float | stat_daily_expert |
| Uint32 | rank_daily_expert |
| Sint8 | unit_daily_expert |
| Float | stat_weekly_expert |
| Uint32 | rank_weekly_expert |
| Sint8 | unit_weekly_expert |

## OLSAttribute ([Structure](https://github.com/kinnay/NintendoClients/wiki/NEX-Common-Types#structure))
| Type | Name |
| --- | --- |
| Sint8 | attribute_type |
| Uint32 | attribute_value |

## OLSMessage ([Structure](https://github.com/kinnay/NintendoClients/wiki/NEX-Common-Types#structure))
| Type | Name |
| --- | --- |
| Sint8 | message_type |
| Bool | message_prompt |
| Bool | message_drc |
| Bool | message_bloomberg |
| [DateTime](https://github.com/kinnay/NintendoClients/wiki/NEX-Common-Types#datetime) | message_date |
| Uint32 | message_duration |
| [String](https://github.com/kinnay/NintendoClients/wiki/NEX-Common-Types#string) | message_title |
| [String](https://github.com/kinnay/NintendoClients/wiki/NEX-Common-Types#string) | message_body |
| [List](https://github.com/kinnay/NintendoClients/wiki/NEX-Common-Types#list)&#x3C;[String](https://github.com/kinnay/NintendoClients/wiki/NEX-Common-Types#string)&#x3E; | message_buttons |
| [List](https://github.com/kinnay/NintendoClients/wiki/NEX-Common-Types#list)&#x3C;[OLSAttribute](#olsattribute-structure)&#x3E; | message_attributes |

## OLSCompetitionResult ([Structure](https://github.com/kinnay/NintendoClients/wiki/NEX-Common-Types#structure))
| Type | Name |
| --- | --- |
| Uint32 | id_leaderboard |
| [String](https://github.com/kinnay/NintendoClients/wiki/NEX-Common-Types#string) | name |
| [DateTime](https://github.com/kinnay/NintendoClients/wiki/NEX-Common-Types#datetime) | begin |
| [DateTime](https://github.com/kinnay/NintendoClients/wiki/NEX-Common-Types#datetime) | end |
| Uint32 | level |
| Uint32 | mode |
| Uint32 | rank |
| Uint32 | max_rank |

## OLSCompetition ([Structure](https://github.com/kinnay/NintendoClients/wiki/NEX-Common-Types#structure))
| Type | Name |
| --- | --- |
| [OLSCompetitionResult](#olscompetitionresult-structure) | result |
| [String](https://github.com/kinnay/NintendoClients/wiki/NEX-Common-Types#string) | message |
| Uint32 | seed |
| Float | objective |
| Float | score_validation |
| Uint32 | id_bricks |
| Float | score |

## OLSSelectionRow ([Structure](https://github.com/kinnay/NintendoClients/wiki/NEX-Common-Types#structure))
| Type | Name |
| --- | --- |
| Uint32 | ID |
| [String](https://github.com/kinnay/NintendoClients/wiki/NEX-Common-Types#string) | name |
| Uint64 | id_ghost |
| Uint32 | id_costume |
| Uint32 | country |
| Uint32 | level |
| Float | score |

## OLSCompetitionInfos ([Structure](https://github.com/kinnay/NintendoClients/wiki/NEX-Common-Types#structure))
| Type | Name |
| --- | --- |
| Uint32 | id_competition |
| Uint32 | participants |
| [List](https://github.com/kinnay/NintendoClients/wiki/NEX-Common-Types#list)&#x3C;Uint32&#x3E; | friends |
| Uint32 | level_id |
| Uint32 | mode |
| Uint32 | my_rank |
| Uint32 | remaining_seconds |
| [List](https://github.com/kinnay/NintendoClients/wiki/NEX-Common-Types#list)&#x3C;[OLSSelectionRow](#olsselectionrow-structure)&#x3E; | competitors |
| Uint32 | unit |

## OLSLdbRow ([Structure](https://github.com/kinnay/NintendoClients/wiki/NEX-Common-Types#structure))
| Type | Name |
| --- | --- |
| Uint32 | ID |
| [String](https://github.com/kinnay/NintendoClients/wiki/NEX-Common-Types#string) | name |
| Float | value |
| Uint32 | costume |
| Uint32 | statusIcon |
| Uint32 | country |

## OLSTomb ([Structure](https://github.com/kinnay/NintendoClients/wiki/NEX-Common-Types#structure))
| Type | Name |
| --- | --- |
| Sint32 | pid |
| [String](https://github.com/kinnay/NintendoClients/wiki/NEX-Common-Types#string) | name |
| Uint32 | id_costume |
| Float | x |
| Float | y |
| Float | z |

## OLSFriend ([Structure](https://github.com/kinnay/NintendoClients/wiki/NEX-Common-Types#structure))
| Type | Name |
| --- | --- |
| Sint32 | pid |
| Uint32 | relationship |