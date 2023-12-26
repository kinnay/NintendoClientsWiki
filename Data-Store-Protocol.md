## [[NEX Protocols]] > Data Store (115)

The following games have additional methods in the datastore protocol:
* [Miitopia 3DS](Data-Store-Protocol-(Miitopia-3DS))
* [Pokemon Bank](Data-Store-Protocol-(Pokemon-Bank))
* [Pokemon X / Y](Data-Store-Protocol-(Pokemon-XY))
* [Splatoon 2](Data-Store-Protocol-(Splatoon-2))
* [Super Mario Maker](Data-Store-Protocol-(SMM))
* [Super Mario Maker 2](Data-Store-Protocol-(SMM-2))
* [Super Mario Odyssey](Data-Store-Protocol-(SMO))
* [Super Smash Bros. 4](Data-Store-Protocol-(SSB4))
* [Super Smash Bros. Ultimate](Data-Store-Protocol-(SSBU))

This remainder of this page describes the methods that are not specific to any game.

| Method ID | Method Name |
| --- | --- |
| 1 | [PrepareGetObjectV1](#1-preparegetobjectv1) |
| 2 | [PreparePostObjectV1](#2-preparepostobjectv1) |
| 3 | [CompletePostObjectV1](#3-completepostobjectv1) |
| 4 | [DeleteObject](#4-deleteobject) |
| 5 | [DeleteObjects](#5-deleteobjects) |
| 6 | [ChangeMetaV1](#6-changemetav1) |
| 7 | [ChangeMetasV1](#7-changemetasv1) |
| 8 | [GetMeta](#8-getmeta) |
| 9 | [GetMetas](#9-getmetas) |
| 10 | [PrepareUpdateObject](#10-prepareupdateobject) |
| 11 | [CompleteUpdateObject](#11-completeupdateobject) |
| 12 | [SearchObject](#12-searchobject) |
| 13 | [GetNotificationUrl](#13-getnotificationurl) |
| 14 | [GetNewArrivedNotificationsV1](#14-getnewarrivednotificationsv1) |
| 15 | [RateObject](#15-rateobject) |
| 16 | [GetRating](#16-getrating) |
| 17 | [GetRatings](#17-getratings) |
| 18 | [ResetRating](#18-resetrating) |
| 19 | [ResetRatings](#19-resetratings) |
| 20 | [GetSpecificMetaV1](#20-getspecificmetav1) |
| 21 | [PostMetaBinary](#21-postmetabinary) |
| 22 | [TouchObject](#22-touchobject) |
| 23 | [GetRatingWithLog](#23-getratingwithlog) |
| 24 | [PreparePostObject](#24-preparepostobject) |
| 25 | [PrepareGetObject](#25-preparegetobject) |
| 26 | [CompletePostObject](#26-completepostobject) |
| 27 | [GetNewArrivedNotifications](#27-getnewarrivednotifications) |
| 28 | [GetSpecificMeta](#28-getspecificmeta) |
| 29 | [GetPersistenceInfo](#29-getpersistenceinfo) |
| 30 | [GetPersistenceInfos](#30-getpersistenceinfos) |
| 31 | [PerpetuateObject](#31-perpetuateobject) |
| 32 | [UnperpetuateObject](#32-unperpetuateobject) |
| 33 | [PrepareGetObjectOrMetaBinary](#33-preparegetobjectormetabinary) |
| 34 | [GetPasswordInfo](#34-getpasswordinfo) |
| 35 | [GetPasswordInfos](#35-getpasswordinfos) |
| 36 | [GetMetasMultipleParam](#36-getmetasmultipleparam) |
| 37 | [CompletePostObjects](#37-completepostobjects) |
| 38 | [ChangeMeta](#38-changemeta) |
| 39 | [ChangeMetas](#39-changemetas) |
| 40 | [RateObjects](#40-rateobjects) |
| 41 | [PostMetaBinaryWithDataId](#41-postmetabinarywithdataid) |
| 42 | [PostMetaBinariesWithDataId](#42-postmetabinarieswithdataid) |
| 43 | [RateObjectWithPosting](#43-rateobjectwithposting) |
| 44 | [RateObjectsWithPosting](#44-rateobjectswithposting) |
| 45 | [GetObjectInfos](#45-getobjectinfos) |
| 46 | [SearchObjectLight](#46-searchobjectlight) |

# (1) PrepareGetObjectV1
## Request
| Type | Name |
| --- | --- |
| [DataStorePrepareGetParamV1] | param |

## Response
| Type | Name |
| --- | --- |
| [DataStoreReqGetInfoV1] | pReqGetInfo |

# (2) PreparePostObjectV1
## Request
| Type | Name |
| --- | --- |
| [DataStorePreparePostParamV1] | param |

## Response
| Type | Name |
| --- | --- |
| [DataStoreReqPostInfoV1] | pReqPostInfo |

# (3) CompletePostObjectV1
## Request
| Type | Name |
| --- | --- |
| [DataStoreCompletePostParamV1] | param |

## Response
This method does not return anything.

# (4) DeleteObject
## Request
| Type | Name |
| --- | --- |
| [DataStoreDeleteParam] | param |

## Response
This method does not return anything.

# (5) DeleteObjects
## Request
| Type | Name |
| --- | --- |
| [List]&lt;[DataStoreDeleteParam]&gt; | params |
| Bool | transactional |

## Response
| Type | Name |
| --- | --- |
| [List]&lt;[Result]&gt; | pResults |

# (6) ChangeMetaV1
## Request
| Type | Name |
| --- | --- |
| [DataStoreChangeMetaParamV1] | param |

## Response
This method does not return anything.

# (7) ChangeMetasV1
## Request
| Type | Name |
| --- | --- |
| [List]&lt;Uint64&gt; | dataIds |
| [List]&lt;[DataStoreChangeMetaParamV1]&gt; | params |
| Bool | transactional |

## Response
| Type | Name |
| --- | --- |
| [List]&lt;[Result]&gt; | pResults |

# (8) GetMeta
## Request
| Type | Name |
| --- | --- |
| [DataStoreGetMetaParam] | param |

## Response
| Type | Name |
| --- | --- |
| [DataStoreMetaInfo] | pMetaInfo |

# (9) GetMetas
## Request
| Type | Name |
| --- | --- |
| [List]&lt;Uint64&gt; | dataIds |
| [DataStoreGetMetaParam] | param |

## Response
| Type | Name |
| --- | --- |
| [List]&lt;[DataStoreMetaInfo]&gt; | pMetaInfo |
| [List]&lt;[Result]&gt; | pResults |

# (10) PrepareUpdateObject
## Request
| Type | Name |
| --- | --- |
| [DataStorePrepareUpdateParam] | param |

## Response
| Type | Name |
| --- | --- |
| [DataStoreReqUpdateInfo] | pReqUpdateInfo |

# (11) CompleteUpdateObject
## Request
| Type | Name |
| --- | --- |
| [DataStoreCompleteUpdateParam] | param |

## Response
This method does not return anything.

# (12) SearchObject
## Request
| Type | Name |
| --- | --- |
| [DataStoreSearchParam] | param |

## Response
| Type | Name |
| --- | --- |
| [DataStoreSearchResult] | pSearchResult |

# (13) GetNotificationUrl
## Request
| Type | Name |
| --- | --- |
| [DataStoreGetNotificationUrlParam] | param |

## Response
| Type | Name |
| --- | --- |
| [DataStoreReqGetNotificationUrlInfo] | info |

# (14) GetNewArrivedNotificationsV1
## Request
| Type | Name |
| --- | --- |
| [DataStoreGetNewArrivedNotificationsParam] | param |

## Response
| Type | Name |
| --- | --- |
| [List]&lt;[DataStoreNotificationV1]&gt; | pResult |
| Bool | pHasNext |

# (15) RateObject
## Request
| Type | Name |
| --- | --- |
| [DataStoreRatingTarget] | target |
| [DataStoreRateObjectParam] | param |
| Bool | fetchRatings |

## Response
| Type | Name |
| --- | --- |
| [DataStoreRatingInfo] | pRating |

# (16) GetRating
## Request
| Type | Name |
| --- | --- |
| [DataStoreRatingTarget] | target |
| Uint64 | accessPassword |

## Response
| Type | Name |
| --- | --- |
| [DataStoreRatingInfo] | pRating |

# (17) GetRatings
## Request
| Type | Name |
| --- | --- |
| [List]&lt;Uint64&gt; | dataIds |
| Uint64 | accessPassword |

## Response
| Type | Name |
| --- | --- |
| [List]&lt;[List]&lt;[DataStoreRatingInfoWithSlot]&gt;&gt; | pRatings |
| [List]&lt;[Result]&gt; | pResults |

# (18) ResetRating
## Request
| Type | Name |
| --- | --- |
| [DataStoreRatingTarget] | target |
| Uint64 | updatePassword |

## Response
This method does not return anything.

# (19) ResetRatings
## Request
| Type | Name |
| --- | --- |
| [List]&lt;Uint64&gt; | dataIds |
| Bool | transactional |

## Response
| Type | Name |
| --- | --- |
| [List]&lt;[Result]&gt; | pResults |

# (20) GetSpecificMetaV1
## Request
| Type | Name |
| --- | --- |
| [DataStoreGetSpecificMetaParamV1] | param |

## Response
| Type | Name |
| --- | --- |
| [List]&lt;[DataStoreSpecificMetaInfoV1]&gt; | pMetaInfos |

# (21) PostMetaBinary
## Request
| Type | Name |
| --- | --- |
| [DataStorePreparePostParam] | param |

## Response
| Type | Name |
| --- | --- |
| Uint64 | dataId |

# (22) TouchObject
## Request
| Type | Name |
| --- | --- |
| [DataStoreTouchObjectParam] | param |

## Response
This method does not return anything.

# (23) GetRatingWithLog
## Request
| Type | Name |
| --- | --- |
| [DataStoreRatingTarget] | target |
| Uint64 | accessPassword |

## Response
| Type | Name |
| --- | --- |
| [DataStoreRatingInfo] | pRating |
| [DataStoreRatingLog] | pRatingLog |

# (24) PreparePostObject
## Request
| Type | Name |
| --- | --- |
| [DataStorePreparePostParam] | param |

## Response
| Type | Name |
| --- | --- |
| [DataStoreReqPostInfo] | pReqPostInfo |

# (25) PrepareGetObject
## Request
| Type | Name |
| --- | --- |
| [DataStorePrepareGetParam] | param |

## Response
| Type | Name |
| --- | --- |
| [DataStoreReqGetInfo] | pReqGetInfo |

# (26) CompletePostObject
## Request
| Type | Name |
| --- | --- |
| [DataStoreCompletePostParam] | param |

## Response
This method does not return anything.

# (27) GetNewArrivedNotifications
## Request
| Type | Name |
| --- | --- |
| [DataStoreGetNewArrivedNotificationsParam] | param |

## Response
| Type | Name |
| --- | --- |
| [List]&lt;[DataStoreNotification]&gt; | pResult |
| Bool | pHasNext |

# (28) GetSpecificMeta
## Request
| Type | Name |
| --- | --- |
| [DataStoreGetSpecificMetaParam] | param |

## Response
| Type | Name |
| --- | --- |
| [List]&lt;[DataStoreSpecificMetaInfo]&gt; | pMetaInfos |

# (29) GetPersistenceInfo
## Request
| Type | Name |
| --- | --- |
| [PID] | ownerId |
| Uint16 | persistenceSlotId |

## Response
| Type | Name |
| --- | --- |
| [DataStorePersistenceInfo] | pPersistenceInfo |

# (30) GetPersistenceInfos
## Request
| Type | Name |
| --- | --- |
| [PID] | ownerId |
| [List]&lt;Uint16&gt; | persistenceSlotIds |

## Response
| Type | Name |
| --- | --- |
| [List]&lt;[DataStorePersistenceInfo]&gt; | pPersistenceInfo |
| [List]&lt;[Result]&gt; | pResults |

# (31) PerpetuateObject
## Request
| Type | Name |
| --- | --- |
| Uint16 | persistenceSlotId |
| Uint64 | dataId |
| Bool | deleteLastObject |

## Response
This method does not return anything.

# (32) UnperpetuateObject
## Request
| Type | Name |
| --- | --- |
| Uint16 | persistenceSlotId |
| Bool | deleteLastObject |

## Response
This method does not return anything.

# (33) PrepareGetObjectOrMetaBinary
## Request
| Type | Name |
| --- | --- |
| [DataStorePrepareGetParam] | param |

## Response
| Type | Name |
| --- | --- |
| [DataStoreReqGetInfo] | pReqGetInfo |
| [DataStoreReqGetAdditionalMeta] | pReqGetAdditionalMeta |

# (34) GetPasswordInfo
## Request
| Type | Name |
| --- | --- |
| Uint64 | dataId |

## Response
| Type | Name |
| --- | --- |
| [DataStorePasswordInfo] | pPasswordInfo |

# (35) GetPasswordInfos
## Request
| Type | Name |
| --- | --- |
| [List]&lt;Uint64&gt; | dataIds |

## Response
| Type | Name |
| --- | --- |
| [List]&lt;[DataStorePasswordInfo]&gt; | pPasswordInfos |
| [List]&lt;[Result]&gt; | pResults |

# (36) GetMetasMultipleParam
## Request
| Type | Name |
| --- | --- |
| [List]&lt;[DataStoreGetMetaParam]&gt; | params |

## Response
| Type | Name |
| --- | --- |
| [List]&lt;[DataStoreMetaInfo]&gt; | pMetaInfo |
| [List]&lt;[Result]&gt; | pResults |

# (37) CompletePostObjects
## Request
| Type | Name |
| --- | --- |
| [List]&lt;Uint64&gt; | dataIds |

## Response
This method does not return anything.

# (38) ChangeMeta
## Request
| Type | Name |
| --- | --- |
| [DataStoreChangeMetaParam] | param |

## Response
This method does not return anything.

# (39) ChangeMetas
## Request
| Type | Name |
| --- | --- |
| [List]&lt;Uint64&gt; | dataIds |
| [List]&lt;[DataStoreChangeMetaParam]&gt; | params |
| Bool | transactional |

## Response
| Type | Name |
| --- | --- |
| [List]&lt;[Result]&gt; | pResults |

# (40) RateObjects
## Request
| Type | Name |
| --- | --- |
| [List]&lt;[DataStoreRatingTarget]&gt; | targets |
| [List]&lt;[DataStoreRateObjectParam]&gt; | params |
| Bool | transactional |
| Bool | fetchRatings |

## Response
| Type | Name |
| --- | --- |
| [List]&lt;[DataStoreRatingInfo]&gt; | pRatings |
| [List]&lt;[Result]&gt; | pResults |

# (41) PostMetaBinaryWithDataId
## Request
| Type | Name |
| --- | --- |
| Uint64 | dataId |
| [DataStorePreparePostParam] | param |

## Response
This method does not return anything.

# (42) PostMetaBinariesWithDataId
## Request
| Type | Name |
| --- | --- |
| [List]&lt;Uint64&gt; | dataIds |
| [List]&lt;[DataStorePreparePostParam]&gt; | params |
| Bool | transactional |

## Response
| Type | Name |
| --- | --- |
| [List]&lt;[Result]&gt; | pResults |

# (43) RateObjectWithPosting
## Request
| Type | Name |
| --- | --- |
| [DataStoreRatingTarget] | target |
| [DataStoreRateObjectParam] | rateParam |
| [DataStorePreparePostParam] | postParam |
| Bool | fetchRatings |

## Response
| Type | Name |
| --- | --- |
| [DataStoreRatingInfo] | pRating |

# (44) RateObjectsWithPosting
## Request
| Type | Name |
| --- | --- |
| [List]&lt;[DataStoreRatingTarget]&gt; | targets |
| [List]&lt;[DataStoreRateObjectParam]&gt; | rateParams |
| [List]&lt;[DataStorePreparePostParam]&gt; | postParams |
| Bool | transactional |
| Bool | fetchRatings |

## Response
| Type | Name |
| --- | --- |
| [List]&lt;[DataStoreRatingInfo]&gt; | pRatings |
| [List]&lt;[Result]&gt; | pResults |

# (45) GetObjectInfos
## Request
| Type | Name |
| --- | --- |
| [List]&lt;Uint64&gt; | dataIds |

## Response
| Type | Name |
| --- | --- |
| [List]&lt;[DataStoreReqGetInfo]&gt; | pInfos |
| [List]&lt;[Result]&gt; | pResults |

# (46) SearchObjectLight
## Request
| Type | Name |
| --- | --- |
| [DataStoreSearchParam] | param |

## Response
| Type | Name |
| --- | --- |
| [DataStoreSearchResult] | pSearchResult |

# Types
## DataStorePrepareGetParamV1 ([Structure])
| Type | Name |
| --- | --- |
| Uint32 | dataId |
| Uint32 | lockId |

## DataStorePrepareGetParam ([Structure])
| Type | Name |
| --- | --- |
| Uint64 | dataId |
| Uint32 | lockId |
| [DataStorePersistenceTarget] | persistenceTarget |
| Uint64 | accessPassword |
| [List]&lt;[String]&gt; | extraData |

## DataStoreReqGetInfoV1 ([Structure])
| Type | Name |
| --- | --- |
| [String] | url |
| [List]&lt;[DataStoreKeyValue]&gt; | requestHeaders |
| Uint32 | size |
| [Buffer] | rootCaCert |

## DataStoreReqGetInfo ([Structure])
| Type | Name |
| --- | --- |
| [String] | url |
| [List]&lt;[DataStoreKeyValue]&gt; | requestHeaders |
| Uint32 | size |
| [Buffer] | rootCaCert |
| Uint64 | dataId |

## DataStoreReqGetAdditionalMeta ([Structure])
| Type | Name |
| --- | --- |
| [PID] | ownerId |
| Uint16 | dataType |
| Uint16 | version |
| [qBuffer] | metaBinary |

## DataStorePreparePostParamV1 ([Structure])
| Type | Name |
| --- | --- |
| Uint32 | size |
| [String] | name |
| Uint16 | dataType |
| [qBuffer] | metaBinary |
| [DataStorePermission] | permission |
| [DataStorePermission] | delPermission |
| Uint32 | flag |
| Uint16 | period |
| Uint32 | referDataId |
| [List]&lt;[String]&gt; | tags |
| [List]&lt;[DataStoreRatingInitParamWithSlot]&gt; | ratingInitParams |

## DataStorePreparePostParam ([Structure])
| Type | Name |
| --- | --- |
| Uint32 | size |
| [String] | name |
| Uint16 | dataType |
| [qBuffer] | metaBinary |
| [DataStorePermission] | permission |
| [DataStorePermission] | delPermission |
| Uint32 | flag |
| Uint16 | period |
| Uint32 | referDataId |
| [List]&lt;[String]&gt; | tags |
| [List]&lt;[DataStoreRatingInitParamWithSlot]&gt; | ratingInitParams |
| [DataStorePersistenceInitParam] | persistenceInitParam |
| [List]&lt;[String]&gt; | extraData |

## DataStoreReqPostInfoV1 ([Structure])
| Type | Name |
| --- | --- |
| Uint32 | dataId |
| [String] | url |
| [List]&lt;[DataStoreKeyValue]&gt; | requestHeaders |
| [List]&lt;[DataStoreKeyValue]&gt; | formFields |
| [Buffer] | rootCaCert |

## DataStoreReqPostInfo ([Structure])
| Type | Name |
| --- | --- |
| Uint64 | dataId |
| [String] | url |
| [List]&lt;[DataStoreKeyValue]&gt; | requestHeaders |
| [List]&lt;[DataStoreKeyValue]&gt; | formFields |
| [Buffer] | rootCaCert |

## DataStoreCompletePostParamV1 ([Structure])
| Type | Name |
| --- | --- |
| Uint32 | dataId |
| Bool | isSuccess |

## DataStoreCompletePostParam ([Structure])
| Type | Name |
| --- | --- |
| Uint64 | dataId |
| Bool | isSuccess |

## DataStoreDeleteParam ([Structure])
| Type | Name |
| --- | --- |
| Uint64 | dataId |
| Uint64 | updatePassword |

## DataStoreChangeMetaParamV1 ([Structure])
| Type | Name |
| --- | --- |
| Uint64 | dataId |
| Uint32 | modifiesFlag |
| [String] | name |
| [DataStorePermission] | permission |
| [DataStorePermission] | delPermission |
| Uint16 | period |
| [qBuffer] | metaBinary |
| [List]&lt;[String]&gt; | tags |
| Uint64 | updatePassword |

## DataStoreChangeMetaParam ([Structure])
| Type | Name |
| --- | --- |
| Uint64 | dataId |
| Uint32 | modifiesFlag |
| [String] | name |
| [DataStorePermission] | permission |
| [DataStorePermission] | delPermission |
| Uint16 | period |
| [qBuffer] | metaBinary |
| [List]&lt;[String]&gt; | tags |
| Uint64 | updatePassword |
| Uint32 | referredCnt |
| Uint16 | dataType |
| Uint8 | status |
| [DataStoreChangeMetaCompareParam] | compareParam |
| [DataStorePersistenceTarget] | persistenceTarget |

## DataStoreGetMetaParam ([Structure])
| Type | Name |
| --- | --- |
| Uint64 | dataId |
| [DataStorePersistenceTarget] | persistenceTarget |
| Uint8 | resultOption |
| Uint64 | accessPassword |

Result option flags:

| Flag | Field |
| --- | --- |
| 0x4 | metaBinary |

## DataStoreRatingInfo ([Structure])
| Type | Name |
| --- | --- |
| Sint64 | totalValue |
| Uint32 | count |
| Sint64 | initialValue |

## DataStoreRatingInfoWithSlot ([Structure])
| Type | Name |
| --- | --- |
| Sint8 | slot |
| [DataStoreRatingInfo] | rating |

## DataStoreMetaInfo ([Structure])
| Type | Name |
| --- | --- |
| Uint64 | dataId |
| [PID] | ownerId |
| Uint32 | size |
| [String] | name |
| Uint16 | dataType |
| [qBuffer] | metaBinary |
| [DataStorePermission] | permission |
| [DataStorePermission] | delPermission |
| [DateTime] | createdTime |
| [DateTime] | updatedTime |
| Uint16 | period |
| Uint8 | status |
| Uint32 | referredCnt |
| Uint32 | referDataId |
| Uint32 | flag |
| [DateTime] | referredTime |
| [DateTime] | expireTime |
| [List]&lt;[String]&gt; | tags |
| [List]&lt;[DataStoreRatingInfoWithSlot]&gt; | ratings |

## DataStorePrepareUpdateParam ([Structure])
| Type | Name |
| --- | --- |
| Uint64 | dataId |
| Uint32 | size |
| Uint64 | updatePassword |
| [List]&lt;[String]&gt; | extraData |

## DataStoreReqUpdateInfo ([Structure])
| Type | Name |
| --- | --- |
| Uint32 | version |
| [String] | url |
| [List]&lt;[DataStoreKeyValue]&gt; | requestHeaders |
| [List]&lt;[DataStoreKeyValue]&gt; | formFields |
| [Buffer] | rootCaCert |

## DataStoreCompleteUpdateParam ([Structure])
| Type | Name |
| --- | --- |
| Uint64 | dataId |
| Uint32 | version |
| Bool | isSuccess |

## DataStoreSearchParam ([Structure])
| Type | Name |
| --- | --- |
| Uint8 | searchTarget |
| [List]&lt;[PID]&gt; | ownerIds |
| Uint8 | ownerType |
| [List]&lt;Uint64&gt; | destinationIds |
| Uint16 | dataType |
| [DateTime] | createdAfter |
| [DateTime] | createdBefore |
| [DateTime] | updatedAfter |
| [DateTime] | updatedBefore |
| Uint32 | referDataId |
| [List]&lt;[String]&gt; | tags |
| Uint8 | resultOrderColumn |
| Uint8 | resultOrder |
| [ResultRange] | resultRange |
| Uint8 | resultOption |
| Uint32 | minimalRatingFrequency |
| Bool | useCache |

Only present on Switch:

| Type | Name |
| --- | --- |
| Bool | totalCountEnabled |
| [List]&lt;Uint16&gt; | dataTypes |

## DataStoreSearchResult ([Structure])
| Type | Name |
| --- | --- |
| Uint32 | totalCount |
| [List]&lt;[DataStoreMetaInfo]&gt; | result |
| Uint8 | totalCountType |

## DataStoreGetNotificationUrlParam ([Structure])
| Type | Name |
| --- | --- |
| [String] | previousUrl |

## DataStoreReqGetNotificationUrlInfo ([Structure])
| Type | Name |
| --- | --- |
| [String] | url |
| [String] | key |
| [String] | query |
| [Buffer] | rootCaCert |

## DataStoreGetNewArrivedNotificationsParam ([Structure])
| Type | Name |
| --- | --- |
| Uint64 | lastNotificationId |
| Uint16 | limit |

## DataStoreNotificationV1 ([Structure])
| Type | Name |
| --- | --- |
| Uint64 | notificationId |
| Uint32 | dataId |

## DataStoreNotification ([Structure])
| Type | Name |
| --- | --- |
| Uint64 | notificationId |
| Uint64 | dataId |

## DataStoreRateObjectParam ([Structure])
| Type | Name |
| --- | --- |
| Sint32 | ratingValue |
| Uint64 | accessPassword |

## DataStoreRatingTarget ([Structure])
| Type | Name |
| --- | --- |
| Uint64 | dataId |
| Sint8 | slot |

## DataStoreGetSpecificMetaParamV1 ([Structure])
| Type | Name |
| --- | --- |
| [List]&lt;Uint32&gt; | dataIds |

## DataStoreGetSpecificMetaParam ([Structure])
| Type | Name |
| --- | --- |
| [List]&lt;Uint64&gt; | dataIds |

## DataStoreSpecificMetaInfoV1 ([Structure])
| Type | Name |
| --- | --- |
| Uint32 | dataId |
| [PID] | ownerId |
| Uint32 | size |
| Uint16 | dataType |
| Uint16 | version |

## DataStoreSpecificMetaInfo ([Structure])
| Type | Name |
| --- | --- |
| Uint64 | dataId |
| [PID] | ownerId |
| Uint32 | size |
| Uint16 | dataType |
| Uint32 | version |

## DataStoreTouchObjectParam ([Structure])
| Type | Name |
| --- | --- |
| Uint64 | dataId |
| Uint32 | lockId |
| Uint64 | accessPassword |

## DataStoreRatingLog ([Structure])
| Type | Name |
| --- | --- |
| Bool | isRated |
| [PID] | pid |
| Sint32 | ratingValue |
| [DateTime] | lockExpirationTime |

## DataStorePersistenceInfo ([Structure])
| Type | Name |
| --- | --- |
| [PID] | ownerId |
| Uint16 | persistenceSlotId |
| Uint64 | dataId |

## DataStorePasswordInfo ([Structure])
| Type | Name |
| --- | --- |
| Uint64 | dataId |
| Uint64 | accessPassword |
| Uint64 | updatePassword |

## DataStorePersistenceTarget ([Structure])
| Type | Name |
| --- | --- |
| [PID] | ownerId |
| Uint16 | persistenceSlotId |

## DataStoreKeyValue ([Structure])
| Type | Name |
| --- | --- |
| [String] | key |
| [String] | value |

## DataStorePermission ([Structure])
| Type | Name |
| --- | --- |
| Uint8 | permission |
| [List]&lt;[PID]&gt; | recipientIds |

## DataStoreRatingInitParamWithSlot ([Structure])
| Type | Name |
| --- | --- |
| Sint8 | slot |
| [DataStoreRatingInitParam] | param |

## DataStorePersistenceInitParam ([Structure])
| Type | Name |
| --- | --- |
| Uint16 | persistenceSlotId |
| Bool | deleteLastObject |

## DataStoreChangeMetaCompareParam ([Structure])
| Type | Name |
| --- | --- |
| Uint32 | comparisonFlag |
| [String] | name |
| [DataStorePermission] | permission |
| [DataStorePermission] | delPermission |
| Uint16 | period |
| [qBuffer] | metaBinary |
| [List]&lt;[String]&gt; | tags |
| Uint32 | referredCnt |
| Uint16 | dataType |
| Uint8 | status |

## DataStoreRatingInitParam ([Structure])
| Type | Name |
| --- | --- |
| Uint8 | flag |
| Uint8 | internalFlag |
| Uint8 | lockType |
| Sint64 | initialValue |
| Sint32 | rangeMin |
| Sint32 | rangeMax |
| Sint8 | periodHour |
| Sint16 | periodDuration |

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

[DataStorePrepareGetParamV1]: #datastorepreparegetparamv1-structure
[DataStoreReqGetInfoV1]: #datastorereqgetinfov1-structure
[DataStorePreparePostParamV1]: #datastorepreparepostparamv1-structure
[DataStoreReqPostInfoV1]: #datastorereqpostinfov1-structure
[DataStoreCompletePostParamV1]: #datastorecompletepostparamv1-structure
[DataStoreDeleteParam]: #datastoredeleteparam-structure
[DataStoreChangeMetaParamV1]: #datastorechangemetaparamv1-structure
[DataStoreGetMetaParam]: #datastoregetmetaparam-structure
[DataStoreMetaInfo]: #datastoremetainfo-structure
[DataStorePrepareUpdateParam]: #datastoreprepareupdateparam-structure
[DataStoreReqUpdateInfo]: #datastorerequpdateinfo-structure
[DataStoreCompleteUpdateParam]: #datastorecompleteupdateparam-structure
[DataStoreSearchParam]: #datastoresearchparam-structure
[DataStoreSearchResult]: #datastoresearchresult-structure
[DataStoreGetNotificationUrlParam]: #datastoregetnotificationurlparam-structure
[DataStoreReqGetNotificationUrlInfo]: #datastorereqgetnotificationurlinfo-structure
[DataStoreGetNewArrivedNotificationsParam]: #datastoregetnewarrivednotificationsparam-structure
[DataStoreNotificationV1]: #datastorenotificationv1-structure
[DataStoreRatingTarget]: #datastoreratingtarget-structure
[DataStoreRateObjectParam]: #datastorerateobjectparam-structure
[DataStoreRatingInfo]: #datastoreratinginfo-structure
[DataStoreRatingInfoWithSlot]: #datastoreratinginfowithslot-structure
[DataStoreGetSpecificMetaParamV1]: #datastoregetspecificmetaparamv1-structure
[DataStoreSpecificMetaInfoV1]: #datastorespecificmetainfov1-structure
[DataStorePreparePostParam]: #datastorepreparepostparam-structure
[DataStoreTouchObjectParam]: #datastoretouchobjectparam-structure
[DataStoreRatingLog]: #datastoreratinglog-structure
[DataStoreReqPostInfo]: #datastorereqpostinfo-structure
[DataStorePrepareGetParam]: #datastorepreparegetparam-structure
[DataStoreReqGetInfo]: #datastorereqgetinfo-structure
[DataStoreCompletePostParam]: #datastorecompletepostparam-structure
[DataStoreNotification]: #datastorenotification-structure
[DataStoreGetSpecificMetaParam]: #datastoregetspecificmetaparam-structure
[DataStoreSpecificMetaInfo]: #datastorespecificmetainfo-structure
[DataStorePersistenceInfo]: #datastorepersistenceinfo-structure
[DataStoreReqGetAdditionalMeta]: #datastorereqgetadditionalmeta-structure
[DataStorePasswordInfo]: #datastorepasswordinfo-structure
[DataStoreChangeMetaParam]: #datastorechangemetaparam-structure
[DataStorePersistenceTarget]: #datastorepersistencetarget-structure
[DataStoreKeyValue]: #datastorekeyvalue-structure
[DataStorePermission]: #datastorepermission-structure
[DataStoreRatingInitParamWithSlot]: #datastoreratinginitparamwithslot-structure
[DataStorePersistenceInitParam]: #datastorepersistenceinitparam-structure
[DataStoreChangeMetaCompareParam]: #datastorechangemetacompareparam-structure
[ResultRange]: NEX-Common-Types#resultrange-structure
[DataStoreRatingInitParam]: #datastoreratinginitparam-structure