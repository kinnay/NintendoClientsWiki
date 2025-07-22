## [[NEX Protocols]] > [Matchmake Extension](Matchmake-Extension-Protocol) > MK8 Deluxe (109)

This page describes the methods that are only seen in Mario Kart 8 Deluxe.

| Method ID | Method Name |
| --- | --- |
| 54 | [CreateSimpleSearchObject](#54-createsimplesearchobject) |
| 55 | [UpdateSimpleSearchObject](#55-updatesimplesearchobject) |
| 56 | [DeleteSimpleSearchObject](#56-deletesimplesearchobject) |
| 57 | [SearchSimpleSearchObject](#57-searchsimplesearchobject) |
| 58 | [SearchSimpleSearchObjectByObjectIds](#58-searchsimplesearchobjectbyobjectids) |
| 59 | JoinMatchmakeSessionWithExtraParticipants |
| 60 | [CustomGetSimplePlayingSession](#60-customgetsimpleplayingsession) |
| 61 | [CreateCompetition](#61-createcompetition) |
| 62 | [DeleteCompetition](#62-deletecompetition) |
| 63 | [RegisterFavoriteCompetition](#63-registerfavoritecompetition) |
| 64 | [UnregisterFavoriteCompetition](#64-unregisterfavoritecompetition) |
| 65 | [GetFavoriteCompetition](#65-getfavoritecompetition) |
| 66 | GetTeamParticipants |
| 67 | FindCommunityByOwner |
| 68 | ? |
| 69 | ? |

# (54) CreateSimpleSearchObject
## Request
| Type | Description |
| --- | --- |
| [SimpleSearchObject] | Object |

## Response
| Type | Description |
| --- | --- |
| Uint32 | Object id |

# (55) UpdateSimpleSearchObject
## Request
| Type | Description |
| --- | --- |
| Uint32 | Object id |
| [SimpleSearchObject] | New object |

## Response
This method does not return anything.

# (56) DeleteSimpleSearchObject
## Request
| Type | Description |
| --- | --- |
| Uint32 | Object id |

## Response
This method does not return anything.

# (57) SearchSimpleSearchObject
## Request
| Type | Description |
| --- | --- |
| [SimpleSearchParam] | Param |

## Response
| Type | Description |
| --- | --- |
| [List]&lt;[SimpleSearchObject]&gt; | Objects |

# (58) SearchSimpleSearchObjectByObjectIds
## Request
| Type | Description |
| --- | --- |
| [List]&lt;Uint32&gt; | Object ids |

## Response
| Type | Description |
| --- | --- |
| [List]&lt;[SimpleSearchObject]&gt; | Objects |

# (60) CustomGetSimplePlayingSession
## Request
| Type | Description |
| --- | --- |
| [List]&lt;[PID]&gt; | Pids |
| Uint8 | Unknown |
| Uint8 | Unknown |

## Response
| Type | Description |
| --- | --- |
| [List]&lt;[SimplePlayingSession]&gt; | Playing sessions |

# (61) CreateCompetition
## Request
| Type | Description |
| --- | --- |
| [SimpleSearchObject] | Competition |

## Response
| Type | Description |
| --- | --- |
| [SimpleSearchObject] | Competition |

# (62) DeleteCompetition
## Request
| Type | Description |
| --- | --- |
| Uint32 | Object id |

## Response
This method does not return anything.

# (63) RegisterFavoriteCompetition
## Request
| Type | Description |
| --- | --- |
| Uint32 | Object id |

## Response
This method does not return anything.

# (64) UnregisterFavoriteCompetition
## Request
| Type | Description |
| --- | --- |
| Uint32 | Object id |

## Response
This method does not return anything.

# (65) GetFavoriteCompetition
## Request
This method does not take any parameters.

## Response
| Type | Description |
| --- | --- |
| [List]&lt;[SimpleSearchObject]&gt; | Favorite competitions |

# Types
## SimpleSearchObject ([Structure])
| Type | Description |
| --- | --- |
| Uint32 | Object id |
| [PID] | Owner |
| [List]&lt;Uint32&gt; | Attributes |
| [qBuffer] | Metadata |
| Uint32 | Unknown |
| [String] | Code |
| [SimpleSearchDateTimeAttribute] | Datetime attribute |

Revision 1:

| Type | Description |
| --- | --- |
| Uint32 | Unknown |
| [DateTime] | Unknown |

## SimpleSearchDateTimeAttribute ([Structure])
| Type | Description |
| --- | --- |
| Uint32 | Unknown |
| Uint32 | Unknown |
| Uint32 | Unknown |
| Uint32 | Unknown |
| [DateTime] | Start time |
| [DateTime] | End time |

## SimpleSearchParam ([Structure])
| Type | Description |
| --- | --- |
| Uint32 | Object id |
| [PID] | Owner |
| [List]&lt;[SimpleSearchCondition]&gt; | Conditions |
| [String] | Code |
| [ResultRange] | Result range |
| [DateTime] | Datetime |

## SimpleSearchCondition ([Structure])
| Type | Description |
| --- | --- |
| Uint32 | Value |
| Uint32 | Comparison operator |

[SimpleSearchObject]: #simplesearchobject-structure
[SimpleSearchDateTimeAttribute]: #simplesearchdatetimeattribute-structure
[SimpleSearchParam]: #simplesearchparam-structure
[SimpleSearchCondition]: #simplesearchcondition-structure

[SimplePlayingSession]: Match-Making-Types#simpleplayingsession-structure

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