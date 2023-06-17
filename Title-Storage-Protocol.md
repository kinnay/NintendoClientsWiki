## [NEX-Protocols](https://github.com/kinnay/NintendoClients/wiki/NEX-Protocols) > TitleStorageProtocol

| Method ID | Method Name |
| --- | --- |
| 1 | [BrowseContents](#1-browsecontents) |
| 2 | [BrowseContentsByType](#2-browsecontentsbytype) |
| 3 | [GetContentDetails](#3-getcontentdetails) |
| 4 | [DownloadContent](#4-downloadcontent) |

# (1) BrowseContents

## Request
| Type | Name |
| --- | --- |
| Uint32 | flags |
| Uint8 | flagsMaskType |
| Uint32 | extendedFlags |
| Uint8 | extendedFlagsMaskType |

## Response
| Type | Name |
| --- | --- |
| [List](https://github.com/kinnay/NintendoClients/wiki/NEX-Common-Types#list)&#x3C;[TitleContent](#titlecontent-structure)&#x3E; | contents |

# (2) BrowseContentsByType

## Request
| Type | Name |
| --- | --- |
| [String](https://github.com/kinnay/NintendoClients/wiki/NEX-Common-Types#string) | contentType |
| Uint32 | flags |
| Uint8 | flagsMaskType |
| Uint32 | extendedFlags |
| Uint8 | extendedFlagsMaskType |

## Response
| Type | Name |
| --- | --- |
| [List](https://github.com/kinnay/NintendoClients/wiki/NEX-Common-Types#list)&#x3C;any&#x3E; | contents |

# (3) GetContentDetails

## Request
| Type | Name |
| --- | --- |
| Uint32 | contentID |

## Response
| Type | Name |
| --- | --- |
| [AnyDataHolder](https://github.com/kinnay/NintendoClients/wiki/NEX-Common-Types#anydataholder) | details |

# (4) DownloadContent

## Request
| Type | Name |
| --- | --- |
| Uint32 | contentID |

## Response
| Type | Name |
| --- | --- |
| [String](https://github.com/kinnay/NintendoClients/wiki/NEX-Common-Types#string) | proto |
| [String](https://github.com/kinnay/NintendoClients/wiki/NEX-Common-Types#string) | host |
| [String](https://github.com/kinnay/NintendoClients/wiki/NEX-Common-Types#string) | path |

# Types

## TitleContent ([Structure](https://github.com/kinnay/NintendoClients/wiki/NEX-Common-Types#structure))
> This structure inherits from [Data](https://github.com/kinnay/NintendoClients/wiki/NEX-Common-Types#data)

| Type | Name |
| --- | --- |
| Uint32 | id |
| [String](https://github.com/kinnay/NintendoClients/wiki/NEX-Common-Types#string) | name |
| [String](https://github.com/kinnay/NintendoClients/wiki/NEX-Common-Types#string) |
| Sint64 | size |
| [String](https://github.com/kinnay/NintendoClients/wiki/NEX-Common-Types#string) | contentType |
| Uint32 | flags |
| Uint32 | extendedFlags |