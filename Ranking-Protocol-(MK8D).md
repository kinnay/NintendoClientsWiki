## [[NEX Protocols]] > [Ranking Protocol](Ranking-Protocol) > MK8 Deluxe (112)

This page describes the methods that are only seen in Mario Kart 8 Deluxe.

| Method ID | Method Name |
| --- | --- |
| 16 | [GetCompetitionRankingScore](#16-getcompetitionrankingscore) |
| 17 | [UploadCompetitionRankingScore](#17-uploadcompetitionrankingscore) |
| 18 | [GetCompetitionInfo](#18-getcompetitioninfo) |
| 19 | [UploadScorePack](#19-uploadscorepack) |
| 20 | [GetScorePack](#20-getscorepack) |
| 21 | ExecuteDeleteScoreJob |
| 22 | [GetCommonDataByPIDList](#22-getcommondatabypidlist) |

# (16) GetCompetitionRankingScore
## Request
| Type | Description |
| --- | --- |
| [CompetitionRankingGetScoreParam] | Param |

## Response
| Type | Description |
| --- | --- |
| [List]&lt;[CompetitionRankingScoreInfo]&gt; | Score info |

# (17) UploadCompetitionRankingScore
## Request
| Type | Description |
| --- | --- |
| [CompetitionRankingUploadScoreParam] | Param |

## Response
| Type | Description |
| --- | --- |
| Bool | Result |

# (18) GetCompetitionInfo
## Request
| Type | Description |
| --- | --- |
| [CompetitionRankingInfoGetParam] | Param |

## Request
| Type | Description |
| --- | --- |
| [List]&lt;[CompetitionRankingInfo]&gt; | Competition info |

# (19) UploadScorePack
## Request
| Type | Description |
| --- | --- |
| [RankingScoreData](Ranking-Protocol#rankingscoredata-structure) | Param |
| [qBuffer] | Metadata |

## Request
This method does not return anything.

# (20) GetScorePack
## Request
| Type | Description |
| --- | --- |
| [List]&lt;[PID]&gt; | Pids |
| Uint32 | Category |

## Response
| Type | Description |
| --- | --- |
| [ScorePack] | Score pack |

# (22) GetCommonDataByPIDList
## Request
| Type | Description |
| --- | --- |
| [List]&lt;[PID]&gt; | Pids |

## Response
| Type | Description |
| --- | --- |
| [CommonDataList] | Common data |

# Types
## CommonDataList ([Structure])
| Type | Description |
| --- | --- |
| [List]&lt;[qBuffer]&gt; | Common data |

## CompetitionRankingGetScoreParam ([Structure])
| Type | Description |
| --- | --- |
| Uint32 | Unknown |
| [ResultRange] | Result range |

## CompetitionRankingInfo ([Structure])
| Type | Description |
| --- | --- |
| Uint32 | Unknown |
| Uint32 | Unknown |
| [List]&lt;Uint32&gt; | Unknown |

## CompetitionRankingInfoGetParam ([Structure])
| Type | Description |
| --- | --- |
| Uint8 | Unknown |
| [ResultRange] | Result range |

## CompetitionRankingScoreData ([Structure])
| Type | Description |
| --- | --- |
| Uint32 | Unknown |
| [PID] | User id |
| Uint32 | Unknown |
| [DateTime] | Datetime |
| Uint8 | Unknown |
| [qBuffer] | Metadata |

## CompetitionRankingScoreInfo ([Structure])
| Type | Description |
| --- | --- |
| Uint32 | Unknown |
| [List]&lt;[CompetitionRankingScoreData]&gt; | Score data |
| Uint32 | Unknown |
| [List]&lt;Uint32&gt; | Unknown |

## CompetitionRankingUploadScoreParam ([Structure])
| Type | Description |
| --- | --- |
| Uint32 | Unknown |
| Uint32 | Unknown |
| Uint32 | Unknown |
| Uint32 | Unknown |
| Uint8 | Unknown |
| Uint32 | Unknown |
| Bool | Unknown |
| [qBuffer] | Metadata |

## ScorePack ([Structure])
| Type | Description |
| --- | --- |
| [List]&lt;[qBuffer]&gt; | Data |

[Result]: NEX-Common-Types#result
[String]: NEX-Common-Types#string
[Buffer]: NEX-Common-Types#buffer
[qBuffer]: NEX-Common-Types#qbuffer
[List]: NEX-Common-Types#list
[Map]: NEX-Common-Types#map
[DateTime]: NEX-Common-Types#datetime
[Structure]: NEX-Common-Types#structure
[Data]: NEX-Common-Types#anydataholder
[PID]: NEX-Common-Types#pid
[ResultRange]: NEX-Common-Types#resultrange-structure

[CommonDataList]: #commondatalist-structure
[CompetitionRankingInfo]: #competitionrankinginfo-structure
[CompetitionRankingInfoGetParam]: #competitionrankinginfogetparam-structure
[CompetitionRankingScoreData]: #competitionrankingscoredata-structure
[CompetitionRankingScoreInfo]: #competitionrankingscoreinfo-structure
[CompetitionRankingGetScoreParam]: #competitionrankinggetscoreparam-structure
[CompetitionRankingUploadScoreParam]: #competitionrankinguploadscoreparam-structure
[ScorePack]: #scorepack-structure