## [NEX-Protocols](https://github.com/kinnay/NintendoClients/wiki/NEX-Protocols) > Title Storage Admin

| Method ID | Method Name |
| --- | --- |
| 1 | [GetContentTypesDescription](#1-getcontenttypesdescription) |
| 2 | [GetContentTypeDescription](#2-getcontenttypedescription) |
| 3 | [BrowseContents](#3-browsecontents) |
| 4 | [GetContentDetails](#4-getcontentdetails) |
| 5 | [CreateContentAndGetUploadInformation](#5-createcontentandgetuploadinformation) |
| 6 | [RemoveContent](#6-removecontent) |
| 7 | [UpdateContentMetaData](#7-updatecontentmetadata) |
| 8 | [ContentInsertionCompleted](#8-contentinsertioncompleted) |

# (1) GetContentTypesDescription

## Request
This method does not take any parameters

## Response
| Type | Name |
| --- | --- |
| [List](https://github.com/kinnay/NintendoClients/wiki/NEX-Common-Types#list)&#x3C;[ContentTypeDescription](#contenttypedescription-structure)&#x3E; | contentDescriptions |

# (2) GetContentTypeDescription

## Request
| Type | Name |
| --- | --- |
| [String](https://github.com/kinnay/NintendoClients/wiki/NEX-Common-Types#string) | contentType |

## Response
| Type | Name |
| --- | --- |
| [List](https://github.com/kinnay/NintendoClients/wiki/NEX-Common-Types#list)&#x3C;[ContentTypeExtensionField](#contenttypeextensionfield-structure)&#x3E; | extensionFields |

# (3) BrowseContents

## Request
This method does not take any parameters

## Response
| Type | Name |
| --- | --- |
| [List](https://github.com/kinnay/NintendoClients/wiki/NEX-Common-Types#list)&#x3C;[AdminTitleContent](#admintitlecontent-structure)&#x3E; | contents |

# (4) GetContentDetails

## Request
| Type | Name |
| --- | --- |
| Uint32 | contentId |

## Response
| Type | Name |
| --- | --- |
| [AnyDataHolder](https://github.com/kinnay/NintendoClients/wiki/NEX-Common-Types#anydataholder) | details |

# (5) CreateContentAndGetUploadInformation

## Request
| Type | Name |
| --- | --- |
| [String](https://github.com/kinnay/NintendoClients/wiki/NEX-Common-Types#string) | name |
| [String](https://github.com/kinnay/NintendoClients/wiki/NEX-Common-Types#string) | description |
| [String](https://github.com/kinnay/NintendoClients/wiki/NEX-Common-Types#string) | key |
| [DateTime](https://github.com/kinnay/NintendoClients/wiki/NEX-Common-Types#datetime) | dateAvailable |
| [DateTime](https://github.com/kinnay/NintendoClients/wiki/NEX-Common-Types#datetime) | dateExpired |
| Uint32 | flags |
| Uint32 | extendedFlags |
| [String](https://github.com/kinnay/NintendoClients/wiki/NEX-Common-Types#string) | contentType |
| [AnyDataHolder](https://github.com/kinnay/NintendoClients/wiki/NEX-Common-Types#anydataholder) | extension |
| [String](https://github.com/kinnay/NintendoClients/wiki/NEX-Common-Types#string) | mime |

## Response
| Type | Name |
| --- | --- |
| Uint32 | contentId |
| [String](https://github.com/kinnay/NintendoClients/wiki/NEX-Common-Types#string) | uploadURL |
| [String](https://github.com/kinnay/NintendoClients/wiki/NEX-Common-Types#string) | uploadMimeType |
| std_map&#x3C;string,string&#x3E; | uploadBody |

# (6) RemoveContent

## Request
| Type | Name |
| --- | --- |
| Uint32 | contentId |

## Response
| Type | Name |
| --- | --- |
| Bool | %retval% |

# (7) UpdateContentMetaData

## Request
| Type | Name |
| --- | --- |
| Uint32 | contentId |
| [String](https://github.com/kinnay/NintendoClients/wiki/NEX-Common-Types#string) | name |
| [String](https://github.com/kinnay/NintendoClients/wiki/NEX-Common-Types#string) | description |
| [DateTime](https://github.com/kinnay/NintendoClients/wiki/NEX-Common-Types#datetime) | dateAvailable |
| [DateTime](https://github.com/kinnay/NintendoClients/wiki/NEX-Common-Types#datetime) | dateExpired |
| Uint32 | flags |
| Uint32 | extendedFlags |
| [AnyDataHolder](https://github.com/kinnay/NintendoClients/wiki/NEX-Common-Types#anydataholder) | extension |

## Response
| Type | Name |
| --- | --- |
| Bool | %retval% |

# (8) ContentInsertionCompleted

## Request
| Type | Name |
| --- | --- |
| Uint32 | contentId |
| Uint32 | contentSize |

## Response
| Type | Name |
| --- | --- |
| Bool | %retval% |

# Types

## ContentTypeExtensionField ([Structure](https://github.com/kinnay/NintendoClients/wiki/NEX-Common-Types#structure))
| Type | Name |
| --- | --- |
| [String](https://github.com/kinnay/NintendoClients/wiki/NEX-Common-Types#string) | m_FieldName |
| [String](https://github.com/kinnay/NintendoClients/wiki/NEX-Common-Types#string) | m_FieldType |

## ContentTypeDescription ([Structure](https://github.com/kinnay/NintendoClients/wiki/NEX-Common-Types#structure))
| Type | Name |
| --- | --- |
| [String](https://github.com/kinnay/NintendoClients/wiki/NEX-Common-Types#string) | m_ContentType |
| [List](https://github.com/kinnay/NintendoClients/wiki/NEX-Common-Types#list)&#x3C;[ContentTypeExtensionField](#contenttypeextensionfield-structure)&#x3E; | m_extensionFields |

## ContentDescription ([Structure](https://github.com/kinnay/NintendoClients/wiki/NEX-Common-Types#structure))
| Type | Name |
| --- | --- |
| [String](https://github.com/kinnay/NintendoClients/wiki/NEX-Common-Types#string) | m_ContentDisplayName |
| [String](https://github.com/kinnay/NintendoClients/wiki/NEX-Common-Types#string) | m_ContentDescription |

## AdminTitleContent ([Structure](https://github.com/kinnay/NintendoClients/wiki/NEX-Common-Types#structure))
| Type | Name |
| --- | --- |
| Uint32 | m_id |
| [String](https://github.com/kinnay/NintendoClients/wiki/NEX-Common-Types#string) | m_name |
| [ContentDescription](#contentdescription-structure) | m_contentDescription |
| Uint32 | m_flags |
| Uint32 | m_extendedFlags |
| [DateTime](https://github.com/kinnay/NintendoClients/wiki/NEX-Common-Types#datetime) | m_dateAvailable |
| [DateTime](https://github.com/kinnay/NintendoClients/wiki/NEX-Common-Types#datetime) | m_dateExpired |
| [String](https://github.com/kinnay/NintendoClients/wiki/NEX-Common-Types#string) | m_contentType |
| [String](https://github.com/kinnay/NintendoClients/wiki/NEX-Common-Types#string) | m_downloadURL |