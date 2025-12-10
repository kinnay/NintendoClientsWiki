## [[NEX Protocols]] > User Storage (53)

| Method ID | Method Name |
| --- | --- |
| 1 | [SearchContents](#1-searchcontents) |
| 2 | [SearchContentsWithTotal](#2-searchcontentswithtotal) |
| 3 | [DeleteContent](#3-deletecontent) |
| 4 | [SaveMetaData](#4-savemetadata) |
| 5 | [SaveContentDB](#5-savecontentdb) |
| 6 | [SaveContentAndGetUploadInfo](#6-savecontentandgetuploadinfo) |
| 7 | [UploadEnd](#7-uploadend) |
| 8 | [GetContentDB](#8-getcontentdb) |
| 9 | [GetContentURL](#9-getcontenturl) |
| 10 | [GetSlotCount](#10-getslotcount) |
| 11 | [GetMetaData](#11-getmetadata) |
| 12 | [Like](#12-like) |
| 13 | [Unlike](#13-unlike) |
| 14 | [IsLiked](#14-isliked) |
| 15 | [GetFavourites](#15-getfavourites) |
| 16 | [MakeFavourite](#16-makefavourite) |
| 17 | [RemoveFromFavourites](#17-removefromfavourites) |
| 18 | [ReportInappropriate](#18-reportinappropriate) |
| 19 | [IncrementPlayCount](#19-incrementplaycount) |
| 20 | [UpdateCustomStat](#20-updatecustomstat) |
| 21 | [GetOwnContents](#21-getowncontents) |
| 22 | [GetMostPopularTags](#22-getmostpopulartags) |
| 23 | [GetTags](#23-gettags) |
| 24 | [TagContent](#24-tagcontent) |
| 25 | [SearchContentsByPlayers](#25-searchcontentsbyplayers) |
| 26 | [SearchContentsByPlayersWithTotal](#26-searchcontentsbyplayerswithtotal) |

# (1) SearchContents
## Request
| Type | Name |
| --- | --- |
| [UserStorageQuery] | query |

## Response
| Type | Name |
| --- | --- |
| [List]&lt;[UserContent]&gt; | searchResults |

# (2) SearchContentsWithTotal
## Request
| Type | Name |
| --- | --- |
| [UserStorageQuery] | query |

## Response
| Type | Name |
| --- | --- |
| [List]&lt;[UserContent]&gt; | searchResults |
| Uint32 | totalResults |

# (3) DeleteContent
## Request
| Type | Name |
| --- | --- |
| [UserContentKey] | contentKey |

## Response
This method does not return anything.

# (4) SaveMetaData
## Request
| Type | Name |
| --- | --- |
| [List]&lt;[ContentProperty]&gt; | properties |
| [UserContentKey] | contentKey |

## Response
| Type | Name |
| --- | --- |
| [UserContentKey] | contentKey |

# (5) SaveContentDB
## Request
| Type | Name |
| --- | --- |
| [List]&lt;[ContentProperty]&gt; | properties |
| [Buffer] | data |
| [UserContentKey] | contentKey |

## Response
| Type | Name |
| --- | --- |
| [UserContentKey] | contentKey |

# (6) SaveContentAndGetUploadInfo
## Request
| Type | Name |
| --- | --- |
| [List]&lt;[ContentProperty]&gt; | properties |
| Uint32 | size |
| [UserContentKey] | contentKey |

## Response
| Type | Name |
| --- | --- |
| [UserContentURL] | uploadInfo |
| Uint64 | pendingID |
| [List]&lt;[String]&gt; | headers |

# (7) UploadEnd
## Request
| Type | Name |
| --- | --- |
| Uint64 | pendingID |
| Bool | result |
| [UserContentKey] | contentKey |

## Response
| Type | Name |
| --- | --- |
| [UserContentKey] | contentKey |

# (8) GetContentDB
## Request
| Type | Name |
| --- | --- |
| [UserContentKey] | contentKey |

## Response
| Type | Name |
| --- | --- |
| [Buffer] | data |

# (9) GetContentURL
## Request
| Type | Name |
| --- | --- |
| [UserContentKey] | contentKey |

## Response
| Type | Name |
| --- | --- |
| [UserContentURL] | downloadInfo |

# (10) GetSlotCount
## Request
| Type | Name |
| --- | --- |
| Uint32 | typeID |

## Response
| Type | Name |
| --- | --- |
| [UserSlotCount] | slotCount |

# (11) GetMetaData
## Request
| Type | Name |
| --- | --- |
| [UserContentKey] | contentKey |

## Response
| Type | Name |
| --- | --- |
| [UserContent] | content |

# (12) Like
## Request
| Type | Name |
| --- | --- |
| [UserContentKey] | contentKey |

## Response
This method does not return anything.

# (13) Unlike
## Request
| Type | Name |
| --- | --- |
| [UserContentKey] | contentKey |

## Response
This method does not return anything.

# (14) IsLiked
## Request
| Type | Name |
| --- | --- |
| [UserContentKey] | contentKey |

## Response
| Type | Name |
| --- | --- |
| Bool | liked |

# (15) GetFavourites
## Request
| Type | Name |
| --- | --- |
| [List]&lt;Uint32&gt; | contentTypes |

## Response
| Type | Name |
| --- | --- |
| [List]&lt;[UserContent]&gt; | favourites |

# (16) MakeFavourite
## Request
| Type | Name |
| --- | --- |
| [UserContentKey] | contentKey |

## Response
This method does not return anything.

# (17) RemoveFromFavourites
## Request
| Type | Name |
| --- | --- |
| [UserContentKey] | contentKey |

## Response
This method does not return anything.

# (18) ReportInappropriate
## Request
| Type | Name |
| --- | --- |
| [UserContentKey] | contentKey |
| [String] | reason |

## Response
This method does not return anything.

# (19) IncrementPlayCount
## Request
| Type | Name |
| --- | --- |
| [UserContentKey] | contentKey |

## Response
This method does not return anything.

# (20) UpdateCustomStat
## Request
| Type | Name |
| --- | --- |
| [UserContentKey] | contentKey |
| Uint16 | statID |
| Sint64 | incValue |

## Response
This method does not return anything.

# (21) GetOwnContents
## Request
| Type | Name |
| --- | --- |
| Uint32 | typeID |

## Response
| Type | Name |
| --- | --- |
| [List]&lt;[UserContent]&gt; | results |

# (22) GetMostPopularTags
## Request
| Type | Name |
| --- | --- |
| [UserContentKey] | contentKey |

## Response
| Type | Name |
| --- | --- |
| [List]&lt;[WeightedTag]&gt; | tags |
| Uint32 | totalNumberOfTaggings |

# (23) GetTags
## Request
| Type | Name |
| --- | --- |
| [UserContentKey] | contentKey |

## Response
| Type | Name |
| --- | --- |
| [List]&lt;Uint32&gt; | tagIds |

# (24) TagContent
## Request
| Type | Name |
| --- | --- |
| [UserContentKey] | contentKey |
| [List]&lt;Uint32&gt; | newTagIds |

## Response
This method does not return anything.

# (25) SearchContentsByPlayers
## Request
| Type | Name |
| --- | --- |
| [List]&lt;Uint32&gt; | pids |
| [UserStorageQuery] | query |

## Response
| Type | Name |
| --- | --- |
| [List]&lt;[UserContent]&gt; | searchResults |

# (26) SearchContentsByPlayersWithTotal
## Request
| Type | Name |
| --- | --- |
| [List]&lt;Uint32&gt; | pids |
| [UserStorageQuery] | query |

## Response
| Type | Name |
| --- | --- |
| [List]&lt;[UserContent]&gt; | searchResults |
| Uint32 | totalResults |

# Types
## ContentProperty ([Structure])
| Type | Name |
| --- | --- |
| Uint32 | m_ID |
| [Variant] | m_value |

## UserContentKey ([Structure])
| Type | Name |
| --- | --- |
| Uint32 | m_typeID |
| Uint64 | m_contentID |

## UserContent ([Structure])
| Type | Name |
| --- | --- |
| [UserContentKey] | m_key |
| Uint32 | m_pid |
| [List]&lt;[ContentProperty]&gt; | m_properties |

## UserStorageQuery ([Structure])
| Type | Name |
| --- | --- |
| Uint32 | m_typeID |
| Uint32 | m_queryID |
| [ResultRange](NEX-Common-Types#resultrange-structure) | m_resultRange |
| [List]&lt;[ContentProperty]&gt; | m_parameters |

## UserSlotCount ([Structure])
| Type | Name |
| --- | --- |
| Uint32 | m_pid |
| Uint32 | m_typeID |
| Uint32 | m_usedSlots |
| Uint32 | m_totalSlots |

## UserContentURL ([Structure])
| Type | Name |
| --- | --- |
| [String] | m_protocol |
| [String] | m_host |
| [String] | m_path |

## WeightedTag ([Structure])
| Type | Name |
| --- | --- |
| Uint32 | m_id |
| Uint32 | m_numberOfOccurences |

[Result]: NEX-Common-Types#result
[String]: NEX-Common-Types#string
[Buffer]: NEX-Common-Types#buffer
[qBuffer]: NEX-Common-Types#qbuffer
[List]: NEX-Common-Types#list
[Map]: NEX-Common-Types#map
[DateTime]: NEX-Common-Types#datetime
[Structure]: NEX-Common-Types#structure
[Data]: NEX-Common-Types#anydataholder
[StationURL]: NEX-Common-Types#stationurl
[Variant]: NEX-Common-Types#variant

[UserStorageQuery]: #userstoragequery-structure
[UserContent]: #usercontent-structure
[UserContentKey]: #usercontentkey-structure
[ContentProperty]: #contentproperty-structure
[UserContentURL]: #usercontenturl-structure
[UserSlotCount]: #userslotcount-structure
[WeightedTag]: #weightedtag-structure