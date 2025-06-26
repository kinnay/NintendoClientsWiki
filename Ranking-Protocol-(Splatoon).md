## [[NEX Protocols]] > [Ranking Protocol](Ranking-Protocol) > Splatoon (112)

This page describes the methods that are only seen in Splatoon.

| Method ID | Method Name |
| --- | --- |
| 16 | [GetCompetitionRankingScore](#16-getcompetitionrankingscore) |
| 17 | GetcompetitionRankingScoreByPeriodList |
| 18 | [UploadCompetitionRankingScore](#18-uploadcompetitionrankingscore) |
| 19 | DeleteCompetitionRankingScore |

# (16) GetCompetitionRankingScore
## Request
| Type | Description |
| --- | --- |
| [CompetitionRankingGetParam] | Param |

## Response
| Type | Description |
| --- | --- |
| [List]&lt;[CompetitionRankingScoreInfo]&gt; | Score info |

# (18) UploadCompetitionRankingScore
## Request
| Type | Description |
| --- | --- |
| [CompetitionRankingUploadScoreParam] | Param |

## Response
| Type | Description |
| --- | --- |
| Bool | Success |

# Types
## CompetitionRankingGetParam ([Structure])
Revision 1:

| Type | Description |
| --- | --- |
| Uint32 | Unknown |
| [ResultRange] | Result range |
| [List]&lt;Uint32&gt; | Festival ids |

## CompetitionRankingScoreInfo ([Structure])
| Type | Description |
| --- | --- |
| Uint32 | Festival id |
| [List]&lt;[CompetitionRankingScoreData]&gt; | Score data |
| Uint32 | Unknown |
| [List]&lt;Uint32&gt; | Team wins |
| [List]&lt;Uint32&gt; | Team votes |

## CompetitionRankingScoreData ([Structure])
| Type | Description |
| --- | --- |
| Uint32 | Unknown |
| [PID] | User id |
| Uint32 | Score |
| [DateTime] | Modified date |
| Uint8 | Unknown |
| [qBuffer] | Application data |

## CompetitionRankingUploadScoreParam ([Structure])
| Type | Description |
| --- | --- |
| Uint32 | Unknown |
| Uint32 | Festival id |
| Uint32 | Unknown |
| Uint32 | Score |
| Uint8 | Team id |
| Uint32 | Team score |
| Bool | Is first upload |
| [qBuffer] | Application data |

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

[CompetitionRankingGetParam]: #competitionrankinggetparam-structure
[CompetitionRankingUploadScoreParam]: #competitionrankinguploadscoreparam-structure
[CompetitionRankingScoreInfo]: #competitionrankingscoreinfo-structure
[CompetitionRankingScoreData]: #competitionrankingscoredata-structure
