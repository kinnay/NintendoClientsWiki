## [[NEX Protocols]] > Screening (124)

| Method ID | Method Name |
| --- | --- |
| 1 | [ReportDataStoreContent](#1-reportdatastorecontent) |
| 2 | ReportUser |

# (1) ReportDataStoreContent
## Request
| Type | Name |
| --- | --- |
| [ScreeningDataStoreContentParam] | pContentParam |
| [ScreeningUgcViolationParam] | pViolationParam |

## Response
This method does not return anything.

# Types
## ScreeningDataStoreContentParam ([Structure])
| Type | Name |
| --- | --- |
| Uint64 | dataId |
| Uint64 | contentDataId |
| [String] | ugcType |
| [String] | language |
| [String] | searchKey |

## ScreeningUgcViolationParam ([Structure])
| Type | Name |
| --- | --- |
| Uint32 | category |
| [String] | reason |
| [List]<[ScreeningContextInfo]> | context |
| Uint64 | screenshotDataId |

## ScreeningContextInfo ([Structure])
| Type | Name |
| --- | --- |
| [String] | key |
| [String] | value |

## ReportCategory ([Uint32])

| Name | Value |
| --- | --- |
| REPORT_CATEGORY_INVALID | 0 |
| REPORT_CATEGORY_MIN | 1 |
| REPORT_CATEGORY_PERSONAL | 1 |
| REPORT_CATEGORY_CRIMINAL | 2 |
| REPORT_CATEGORY_IMMORAL | 3 |
| REPORT_CATEGORY_HARASSMENT | 4 |
| REPORT_CATEGORY_COMMERCIAL | 5 |
| REPORT_CATEGORY_SEXUALLY_EXPLICIT | 6 |
| REPORT_CATEGORY_OTHER | 7 |
| REPORT_CATEGORY_MAX | 7 |

[String]: NEX-Common-Types#string
[List]: NEX-Common-Types#list
[Structure]: NEX-Common-Types#structure

[ScreeningDataStoreContentParam]: #screeningdatastorecontentparam-structure
[ScreeningUgcViolationParam]: #screeningugcviolationparam-structure
[ScreeningContextInfo]: #screeningcontextinfo-structure
