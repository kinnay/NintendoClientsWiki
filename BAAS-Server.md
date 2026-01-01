[Switch](Server-List#switch) > Account Server
---

The baas server manages user accounts and friendships on the Nintendo Switch.

Depending on the method, this server takes form or json encoded requests. The server always responds with json encoding.

The main URL is https://e0d67c509fb203858ebcb2fe3f88c2aa.baas.nintendo.com.

On 21.0.0 and later, the account sysmodule uses https://m-lp1.baas.nintendo.com instead. This server only accepts connections with a valid client certificate. The friends sysmodule still uses the previous URL.

* [Headers](#headers)
* [Methods](#methods)
* [Errors](#errors)
* [Environments](#environments)

## Headers
| Header | Description |
| --- | --- |
| Host | `e0d67c509fb203858ebcb2fe3f88c2aa.baas.nintendo.com` |
| User-Agent | [User agent](#user-agents) |
| Accept | `*/*` |
| Authorization | Access token received from <code><a href="#post-100applicationtoken">/1.0.0/application/token</a></code>, <code><a href="#post-100login">/1.0.0/login</a></code> or <code><a href="#post-100federation">/1.0.0/federation</a></code>, prefixed with `Bearer `. Depends on the method. |
| X-Nintendo-PowerState | `FA` (fully awake) or `HA` (half awake). This header is only sent in the <code><a href="#post-100applicationtoken">/1.0.0/application/token</a></code> and <code><a href="#post-100login">/1.0.0/login</a></code> requests. |

The following headers are only sent in POST, PUT, PATCH and DELETE requests.

| Header | Description |
| --- | --- |
| Content-Length | Content length |
| Content-Type | `application/x-www-form-urlencoded` |

If the content type is changed, and the request is performed by the account sysmodule, the headers are swapped.

| Header | Description |
| --- | --- |
| Content-Type | `application/json` or `application/json-patch+json` |
| Content-Length | Content length |

If the content type is changed, and the request is performed by the friends sysmodule, the `Content-Type` header appears between the `Accept` and `Authorization` headers instead.

### User Agents
The user agents below are taken from the account sysmodule. If the request is made by the friends sysmodule replace `nnAccount` by `nnFriends`.

| System Version | User agent |
| --- | --- |
| 9.0.0 - 9.2.0 | `libcurl (nnAccount; 789f928b-138e-4b2f-afeb-1acae821d897; SDK 9.3.0.0; Add-on 9.3.0.0)` |
| 10.0.0 - 10.2.0 | `libcurl (nnAccount; 789f928b-138e-4b2f-afeb-1acae821d897; SDK 10.4.0.0; Add-on 10.4.0.0)` |
| 11.0.0 - 11.0.1 | `libcurl (nnAccount; 789f928b-138e-4b2f-afeb-1acae821d897; SDK 11.4.0.0; Add-on 11.4.0.0)` |
| 12.0.0 - 12.1.0 | `libcurl (nnAccount; 789f928b-138e-4b2f-afeb-1acae821d897; SDK 12.3.0.0; Add-on 12.3.0.0)` |
| 13.0.0 | `libcurl (nnAccount; 789f928b-138e-4b2f-afeb-1acae821d897; SDK 13.3.0.0; Add-on 13.3.0.0)` |
| 13.1.0 - 13.2.1 | `libcurl (nnAccount; 789f928b-138e-4b2f-afeb-1acae821d897; SDK 13.4.0.0; Add-on 13.4.0.0)` |
| 14.0.0 - 14.1.2 | `libcurl (nnAccount; 789f928b-138e-4b2f-afeb-1acae821d897; SDK 14.3.0.0; Add-on 14.3.0.0)` |
| 15.0.0 - 15.0.1 | `libcurl (nnAccount; 789f928b-138e-4b2f-afeb-1acae821d897; SDK 15.3.0.0; Add-on 15.3.0.0)` |
| 16.0.0 - 16.1.0 | `libcurl (nnAccount; 789f928b-138e-4b2f-afeb-1acae821d897; SDK 16.2.0.0; Add-on 16.2.0.0)` |
| 17.0.0 - 17.0.1 | `libcurl (nnAccount; 789f928b-138e-4b2f-afeb-1acae821d897; SDK 17.5.0.0; Add-on 17.5.0.0)` |
| 18.0.0 - 18.1.0 | `libcurl (nnAccount; 789f928b-138e-4b2f-afeb-1acae821d897; SDK 18.3.0.0; Add-on 18.3.0.0)` |
| 19.0.0 - 19.0.1 | `libcurl (nnAccount; 789f928b-138e-4b2f-afeb-1acae821d897; SDK 19.3.0.0; Add-on 19.3.0.0)` |
| 20.0.0 - 20.5.0 | `libcurl (nnAccount; 789f928b-138e-4b2f-afeb-1acae821d897; SDK 20.5.4.0; Add-on 20.5.4.0)` |
| 21.0.0 - 21.1.0 | `libcurl (nnAccount; 789f928b-138e-4b2f-afeb-1acae821d897; SDK 21.4.0.0; Add-on 21.4.0.0)` |

## Methods
The following methods do not require an access token:

| Module | Method | URL |
| --- | --- | --- |
| Account | POST | [`/1.0.0/application/token`](#post-100applicationtoken) |
| None | GET | <code><a href="#get-100certificates">/1.0.0/certificates</a></code> |
| None | GET | <code><a href="#get-100internal_certificates">/1.0.0/internal_certificates</a></code> |

The following methods require an anonymous access token:

| Module | Method | URL |
| --- | --- | --- |
| Account | POST | <code><a href="#post-100login">/1.0.0/login</a></code> |
| Account | POST | <code><a href="#post-100federation">/1.0.0/federation</a></code> |
| Account | POST | <code><a href="#post-100users">/1.0.0/users</a></code> |

The following methods require a user access token:

| Module | Method | URL |
| --- | --- | --- |
| Account | POST | `/1.0.0/devices/me/delete` |
| Account | ? | `/1.0.0/devices/snapshot` |
| Account | POST | [`/1.0.0/image_upload`](#post-100image_upload) |
| Account | PUT | `/1.0.0/push_channels/<id>/<id>` |
| Friends | GET | `/1.0.0/users` |
| Both | GET | [`/1.0.0/users/<id>`](#get-100usersid) |
| Both | PATCH | [`/1.0.0/users/<id>`](#patch-100usersid) |
| Friends | GET | `/1.0.0/users/<id>/blocks` |
| Friends | POST | `/1.0.0/users/<id>/blocks` |
| Friends | DELETE | `/1.0.0/users/<id>/blocks/<id>` |
| Friends | PATCH | `/1.0.0/users/<id>/device_accounts/<id>` |
| Account | DELETE | [`/1.0.0/users/<id>/device_accounts/<id>`](#delete-100usersiddevice_accountsid) |
| Account | ? | `/1.0.0/users/<id>/device_histories` |
| Friends | POST | [`/1.0.0/users/<id>/generate_code`](#post-100usersidgenerate_code) |
| Account | POST | [`/1.0.0/users/<id>/link`](#post-100usersidlink) |
| Account | POST | `/1.0.0/users/<id>/unlink` |
| Friends | POST | `/2.0.0/friend_requests` |
| Friends | PATCH | `/2.0.0/friend_requests/<id>` |
| Friends | GET | `/2.0.0/users/<id>/friends` |
| Friends | PATCH | `/2.0.0/users/<id>/friends/<id>` |
| Friends | DELETE | `/2.0.0/users/<id>/friends/<id>` |
| Friends | GET | `/2.0.0/users/<id>/friend_requests/inbox` |
| Friends | GET | `/2.0.0/users/<id>/friend_requests/outbox` |
| Friends | GET | `/2.0.0/users/<id>/relationships/<id>` |

### POST /1.0.0/application/token
This method provides an anonymous access token.

| Param | Description |
| --- | --- |
| grantType | `public_client` |
| assertion | Device token obtained from [dauth server](DAuth-Server) |
| penneId | Penne id (optional, introduced in 19.0.0) |

Response on success:

| Field | Description |
| --- | --- |
| expiresIn | Expiration in seconds (10800) |
| accessToken | The anonymous access token |
| tokenType | `Bearer` |

Example:

```
POST /1.0.0/application/token HTTP/1.1
Host: e0d67c509fb203858ebcb2fe3f88c2aa.baas.nintendo.com
User-Agent: libcurl (nnAccount; 789f928b-138e-4b2f-afeb-1acae821d897; SDK 13.3.0.0; Add-on 13.3.0.0)
Accept: */*
X-Nintendo-PowerState: FA
Content-Length: 872
Content-Type: application/x-www-form-urlencoded

grantType=public_client&assertion=eyJqa3UiOiJodHRwczovL2RjZXJ0LWxwMS5uZGFzLnNydi5uaW50ZW5kby5uZXQva2V5cyIsImtpZCI6IjM2NzllMTg4LTI5ZWUtNDE4Zi04ZDkwLWI3MjRjYzg1MzQ0MSIsInR5cCI6IkpXVCIsImFsZyI6IlJTMjU2In0.eyJzdWIiOiI2ODMzN2FjYTI4ODE1Y2JiIiwiaXNzIjoiZGF1dGgtbHAxLm5kYXMuc3J2Lm5pbnRlbmRvLm5ldCIsImF1ZCI6IjhmODQ5YjVkMzQ3NzhkOGUiLCJleHAiOjE2MzI3NjMzMDEsImlhdCI6MTYzMjY3NjkwMSwianRpIjoiZTU5YTBiMGUtOTRlMS00NGFhLWI1ZGItMGZjMGNmNTAyYWRhIiwibmludGVuZG8iOnsic24iOiJYQVcxMDAxMjM0NTY3OCIsInBjIjoiSEFDIiwiZHQiOiJOWCBQcm9kIDEiLCJpc3QiOmZhbHNlfX0.Mdl42B_tWnQQZkpp0qkvEwpkAFGos1YQ8OBKDr_rJCQlNVZLrP6_sd53U8kvwI6TWbnuxFtNxcVJh21kbbY23WsjwQN9Ph2pbjEmneov5b5SfAjWSvfEqt_ViKFQVLv_MZZXQpBYZSQmJ3sA-BbOjeEO6JI5XI3_KR0uj9IxSH_LNSiEwMMNLkP0PcC3gO5cSKcmnb1NPW2BMMdlKOSIbxDSWE4sEuYt2Pl_u2F6hVMVeoC-4z43lIv2tv7aF9Pwv-D7MR-mOxQaxYVHw2Ux4FL0zPZOJMU6qPgfzACeItd6H_A4OBMKSQwBl4DEbSwdle5tph-ur01K91FhXhI6BA
```

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 1061
Connection: keep-alive
Cache-Control: no-store, no-cache
Pragma: no-cache
X-Cloud-Trace-Context: d6b433b5122481d45b61aa4379d547f2
Date: Sun, 26 Sep 2021 19:21:43 GMT
Server: Google Frontend
X-Cache: Miss from cloudfront
Via: 1.1 9608d1fa3f5912724e10840925944987.cloudfront.net (CloudFront)
X-Amz-Cf-Pop: AMS1-C1
X-Amz-Cf-Id: WGSd3qu043Y9Co4sredK7gclrF4BMYPKQXytykkQfwEez4HYJmIbDw==

{"accessToken": "eyJqa3UiOiJodHRwczovL2UwZDY3YzUwOWZiMjAzODU4ZWJjYjJmZTNmODhjMmFhLmJhYXMubmludGVuZG8uY29tLzEuMC4wL2ludGVybmFsX2NlcnRpZmljYXRlcyIsImFsZyI6IlJTMjU2Iiwia2lkIjoiMzA4M2MxYjItNWQ2OC00MzRiLWJlMzItMTFmOTE1NTcwNTAwIn0.eyJzdWIiOiJlZDllMmYwNWQyODZmN2I4IiwiYXVkIjoiZWQ5ZTJmMDVkMjg2ZjdiOCIsImJzOnN0cyI6WzM4NV0sIm5pbnRlbmRvIjp7ImR0IjoiTlggUHJvZCAxIiwicGMiOiJIQUMiLCJkaSI6IjY4MzM3YWNhMjg4MTVjYmIiLCJzbiI6IlhBVzEwMDEyMzQ1Njc4IiwiaXN0IjpmYWxzZX0sImlzcyI6Imh0dHBzOi8vZTBkNjdjNTA5ZmIyMDM4NThlYmNiMmZlM2Y4OGMyYWEuYmFhcy5uaW50ZW5kby5jb20iLCJ0eXAiOiJ0b2tlbiIsImJzOmdydCI6MSwiZXhwIjoxNjMyNjg3NzAxLCJpYXQiOjE2MzI2NzY5MDEsImp0aSI6Ijg3OGQwNzM1LTU3MWEtNGI5NC04MmE2LTJiZjE4MzExNGRiMSJ9.oVn3eE81TJwApnNzhoUJTWhvJJasP5OpURctjSw-evHZVGXSnNbEcNHAGMHQu5QHU7IMiDlBaIM4hb0BU_l7h4EIPtZzZxys0tb4IbyHUD8SQdqjrA7GPadmfuJkIQYMJUUVikTIbAfmVuZ0asM1HjBUEpUjn9JzJgF6355oOePqrcQtWTWtsmthwPpfLj7RfPeGuXlc_89Yj6wBplDkpS3NQGrVULxLXoRBgi_cnhZpgnauorOkynby2EZC2UNfaMxpPXa5yNXPM2HQIiAlnd78Zk4Knl2ZH5xhKbtI6Fzeo0CmCCgzQYfYoh2xhR7WowVPpDNfZiwZ7XX0a3hZLw", "tokenType": "Bearer", "expiresIn": 10800}
```

### POST /1.0.0/login
This method can be used to log in on a device account that was registered with <code><a href="#post-100users">/1.0.0/users</a></code>. If an application token is provided, the server checks if the device account is linked against a Nintendo account, and if the account has a Nintendo Switch Online membership.

| Param | Description |
| --- | --- |
| id | Device account id |
| password | Device account password |
| appAuthNToken | [AAuth token](AAuth-Server) (optional) |
| naCountry | Country code such as `NL` (introduced in 18.0.0) |
| isPersistent | `true` or `false` (introduced in 20.0.0) |
| skipOp2Verification | Skip NSO verification (optional) |

Response on success:

| Field | Description |
| --- | --- |
| expiresIn | Expiration in seconds (10800) |
| user | [User information](#user-information) |
| idToken | ID token (for game servers) |
| accessToken | Access token for user |
| tokenType | `Bearer` |
| summary | See below |

The summary field is only present if an app token is provided where the policy handler is set to `GAME_SERVER` and the user has an NSO membership. It looks as follows:

```json
"summary": {
    "nintendo": {
        "hasMembership": true
    }
}
```

### POST /1.0.0/federation
This method is the same as [`/1.0.0/login`](#post-100login) except that it also takes an ID token that represents a Nintendo account. This is required to link the Nintendo account to the device.

| Param | Description |
| --- | --- |
| id | Device account id |
| password | Device account password |
| idp | `nintendoAccount` |
| idToken | ID token obtained from [accounts.nintendo.com](Account-Server-(Switch)) |
| appAuthNToken | [AAuth token](AAuth-Server) (optional) |
| naCountry | Country code such as `NL` (introduced in 18.0.0) |
| skipOp2Verification | Skip NSO verification (optional) |

### POST /1.0.0/users
This method registers a new user on the server. This method does not take any parameters. On success, the response contains the new [user information](#user-information) and HTTP status code 201.

Example:

```
POST /1.0.0/users HTTP/1.1
Host: e0d67c509fb203858ebcb2fe3f88c2aa.baas.nintendo.com
User-Agent: libcurl (nnAccount; 789f928b-138e-4b2f-afeb-1acae821d897; SDK 13.3.0.0; Add-on 13.3.0.0)
Accept: */*
Authorization: Bearer eyJqa3UiOiJodHRwczovL2UwZDY3YzUwOWZiMjAzODU4ZWJjYjJmZTNmODhjMmFhLmJhYXMubmludGVuZG8uY29tLzEuMC4wL2ludGVybmFsX2NlcnRpZmljYXRlcyIsImFsZyI6IlJTMjU2Iiwia2lkIjoiMzA4M2MxYjItNWQ2OC00MzRiLWJlMzItMTFmOTE1NTcwNTAwIn0.eyJzdWIiOiJlZDllMmYwNWQyODZmN2I4IiwiYXVkIjoiZWQ5ZTJmMDVkMjg2ZjdiOCIsImJzOnN0cyI6WzM4NV0sIm5pbnRlbmRvIjp7ImR0IjoiTlggUHJvZCAxIiwicGMiOiJIQUMiLCJkaSI6IjY4MzM3YWNhMjg4MTVjYmIiLCJzbiI6IlhBVzEwMDEyMzQ1Njc4IiwiaXN0IjpmYWxzZX0sImlzcyI6Imh0dHBzOi8vZTBkNjdjNTA5ZmIyMDM4NThlYmNiMmZlM2Y4OGMyYWEuYmFhcy5uaW50ZW5kby5jb20iLCJ0eXAiOiJ0b2tlbiIsImJzOmdydCI6MSwiZXhwIjoxNjMyNjg3NzAxLCJpYXQiOjE2MzI2NzY5MDEsImp0aSI6Ijg3OGQwNzM1LTU3MWEtNGI5NC04MmE2LTJiZjE4MzExNGRiMSJ9.oVn3eE81TJwApnNzhoUJTWhvJJasP5OpURctjSw-evHZVGXSnNbEcNHAGMHQu5QHU7IMiDlBaIM4hb0BU_l7h4EIPtZzZxys0tb4IbyHUD8SQdqjrA7GPadmfuJkIQYMJUUVikTIbAfmVuZ0asM1HjBUEpUjn9JzJgF6355oOePqrcQtWTWtsmthwPpfLj7RfPeGuXlc_89Yj6wBplDkpS3NQGrVULxLXoRBgi_cnhZpgnauorOkynby2EZC2UNfaMxpPXa5yNXPM2HQIiAlnd78Zk4Knl2ZH5xhKbtI6Fzeo0CmCCgzQYfYoh2xhR7WowVPpDNfZiwZ7XX0a3hZLw
Content-Length: 0
Content-Type: application/x-www-form-urlencoded
```

```
HTTP/1.1 201 Created
Content-Type: application/json
Content-Length: 835
Last-Modified: Sun, 26 Sep 2021 19:21:43 GMT
Location: /1.0.0/users/f09c3d45cc3432c6
Cache-Control: no-store, no-cache
Pragma: no-cache
X-Cloud-Trace-Context: 7ce4b7892458ab7cb2b59ad859885437
Date: Sun, 26 Sep 2021 19:21:43 GMT
Server: Google Frontend
X-Cache: Miss from cloudfront
Via: 1.1 b2d8ce5eb7a72ad5dc65a8cc007a854d.cloudfront.net (CloudFront)
X-Amz-Cf-Pop: AMS1-C1
X-Amz-Cf-Id: 4uJpXHc1kKroh8tdpjO-x55dJLYyzudJ5VWnYdir2csFTjh5C7t3xA==
Connection: keep-alive

{"id":"f09c3d45cc3432c6","etag":"\"4d20053b9c0fcf9a\"","nickname":"","country":"","birthday":"0000-00-00","thumbnailUrl":"","deviceAccounts":[{"id":"7c23fd7c9b37b0cb","password":"0mr1prbsNFzRs0dRCHXRUNECGd1kJVg3Lq6zn0nR"}],"links":{},"permissions":{"personalAnalytics":true,"personalNotification":true,"friendRequestReception":true,"friends":"EVERYONE","presence":"FRIENDS","presenceUpdatedAt":1633432210,"personalAnalyticsUpdatedAt":1633432210,"personalNotificationUpdatedAt":1633432210},"extras":{"self":{},"favoriteFriends":{},"friends":{},"foaf":{},"everyone":{}},"presence":{"state":"OFFLINE","extras":{"self":{},"favoriteFriends":{},"friends":{},"foaf":{},"everyone":{}},"updatedAt":1632676901,"logoutAt":0},"deleted":false,"blocksUpdatedAt":1632676901,"friendsUpdatedAt":1632676901,"createdAt":1632676901,"updatedAt":1632676901}
```

### POST /1.0.0/image_upload
This method uploads a profile picture to the server. The request uses a JSON body.

| Field | Description |
| --- | --- |
| rawContent | Base64-encoded JPEG |
| ownerId | User id of owner |
| allowTransform | Boolean |

Response on success:

| Field | Description |
| --- | --- |
| id | Image id |
| ownerId | Owner id |
| owner | Owner |
| state | `STORED` |
| content | Content |
| createdAt | Created at (timestamp) |
| updatedAt | Updated at (timestamp) |

The owner has the following fields:

| Field | Description |
| --- | --- |
| id | Owner id |

The content has the following fields:

| Field | Description |
| --- | --- |
| id | Image id |
| width | Width |
| height | Height |
| format | `jpg` |
| url | URL of uploaded image |
| urlExpiresAt | Set to 2147483647 |

### GET /1.0.0/users/&lt;id&gt;
This method does not take any parameters and simply returns the [user information](#user-information) for the given user. If the access token does not belong to the given user, this method returns [`insufficient_scope`](#errors).

### PATCH /1.0.0/users/&lt;id&gt;
This method updates the given user. The following JSON patch paths are known to work:

* `/nickname`
* `/country`
* `/birthday`
* `/thumbnailUrl`
* `/extras/self/nxAccount`
* `/permissions/personalAnalytics`
* `/permissions/personalNotification`
* `/permissions/friendRequestReception`
* `/permissions/friends`
* `/permissions/presence`

### DELETE /1.0.0/users/&lt;id&gt;/device_accounts/&lt;id&gt;
Delete the given device account. This method does not take any parameters. Returns HTTP status 204 on success.

### POST /1.0.0/users/&lt;id&gt;/generate_code
Generates a new friend code. Returns the new [user information](#user-information) on success. After generating a friend code, one cannot generate a new friend code for 24 hours.

| Param | Description |
| --- | --- |
| type | `NX` |

### POST /1.0.0/users/&lt;id&gt;/link
Links a Nintendo account to the given device account.

| Param | Description |
| --- | --- |
| `idp` | `nintendoAccount` |
| `idToken` | ID token from Nintendo account |

Returns the new [user information](#user-information).

### GET /1.0.0/certificates
This method returns the JWK set for the id token that's issued by <code><a href="#post-100login">/1.0.0/login</a></code> and <code><a href="#post-100federation">/1.0.0/federation</a></code>.

### GET /1.0.0/internal_certificates
This method returns the JWK set for the access token that's issued by <code><a href="#post-100applicationtoken">/1.0.0/application/token</a></code>, <code><a href="#post-100login">/1.0.0/login</a></code> and <code><a href="#post-100federation">/1.0.0/federation</a></code>.

## User information
| Field | Description |
| --- | --- |
| id | User id (16 hex digits) |
| etag | ETag |
| nickname | Nickname |
| country | Country |
| birthday | YYYY-MM-DD |
| thumbnailUrl | Small thumbnail URL (256x256) |
| thumbnail2Url | Large thumbnail URL (512x512) |
| deviceAccounts | List of [device accounts](#device-account) |
| links | [Linked accounts](#linked-accounts) |
| permissions | [Privacy settings](#privacy-settings) |
| extras | [Extras](#extras) |
| presence | [Online status](#online-status) |
| deleted | Bool |
| blocksUpdatedAt | Timestamp |
| friendsUpdatedAt | Timestamp |
| thumbnailUploadedAt | Timestamp |
| createdAt | Timestamp |
| updatedAt | Timestamp |

#### Device account
The password is only present once, when the account is created.

| Field | Description |
| --- | --- |
| id | Device account id (16 hex digits) |
| password | Device account password (40 random alphanumeric characters) |

#### Linked accounts
| Field | Description |
| --- | --- |
| nintendoNetwork | [Nintendo network link](#linked-account) |
| nintendoAccount | [Nintendo account link](#linked-account) |
| twitter | [Twitter account link](#linked-account) |
| facebook | [Facebook account link](#linked-account) |
| google | [Google account link](#linked-account) |
| friendCode | [Friend code](#friend-code-link) |

#### Linked account
| Field | Description |
| --- | --- |
| id | Account id |
| createdAt | Timestamp |
| updatedAt | Timestamp |

#### Friend code link
| Field | Description |
| --- | --- |
| id | Friend code |
| createdAt | Timestamp |
| updatedAt | Timestamp |
| regenerableAt | Timestamp |
| regenerable | Bool |

#### Privacy settings
| Field | Description |
| --- | --- |
| personalAnalytics | Bool |
| personalNotification | Bool |
| friendRequestReception | Bool |
| friends | `EVERYONE`, `FRIENDS` or `SELF` |
| presence | `FRIENDS`, `FAVORITE_FRIENDS` or `SELF` |
| presenceUpdatedAt | Timestamp |
| personalAnalyticsUpdatedAt | Timestamp |
| personalNotificationUpdatedAt | Timestamp |

#### Online status
| Field | Description |
| --- | --- |
| state | `OFFLINE`, `INACTIVE`, `ONLINE` or `PLAYING` |
| extras | [Extras](#presence-extras) |
| updatedAt | Timestamp |
| logoutAt | Timestamp |

#### Extras
| Field | Description |
| --- | --- |
| self | [Extras](#user-extras) visible by no one |
| favoriteFriends | [Extras](#user-extras) visible by best friends |
| friends | [Extras](#user-extras) visible by all friends |
| foaf | [Extras](#user-extras) visible by friends of a friend |
| everyone | [Extras](#user-extras) visible by everyone |

#### User extras
The following fields are stored in each of the [extras](#extras).

| Field | Description |
| --- | --- |
| playLog | JSON-encoded string containing a list of [play log entries](#play-log-entry) |
| nxAccount | String that identifies the account (only present in 'self'-extras) |

#### Presence extras
The following fields are stored in each of the [extras](#extras).

| Field | Description |
| --- | --- |
| appInfo:appId | Title id |
| appInfo:presenceGroupId | Title id |
| appField | JSON-encoded string |

#### Play log entry
| Field | Description |
| --- | --- |
| appInfo:appId | Title id |
| appInfo:presenceGroupId | Title id |
| totalPlayCount | Total play count |
| totalPlayTime | Total play time in minutes |
| firstPlayedAt | Timestamp |
| lastPlayedAt | Timestamp |

## Errors
On error, the server sends the following response:

| Field | Description |
| --- | --- |
| status | HTTP status code |
| errorCode | Error name |
| title | Error title |
| detail | Error details |
| instance | Path of the request that failed |
| type | `https://baas.nintendo.com/errors/1.0.0/<status>/<errorCode>` |

### Known Errors
| Status | Code | Title | Detail |
| --- | --- | --- | --- |
| 404 | resource_is_not_found | Specified resource is not found | Resource is not found |
| 405 | method_not_allowed | Method Not Allowed | Method Not Allowed |
| 400 | invalid_params | Invalid Params | invalid params |
| 400 | invalid_request | Authorization header value is invalid | Auth scheme or auth params is invalid |
| 400 | invalid_device_account | Invalid Device Account | Device Account's id or password is invalid |
| 400 | invalid_ndas_app_authn_token | Invalid NDAS App AuthN Token | |
| 400 | invalid_idp | ? | ? |
| 400 | invalid_idp_account | Invalid IdP Account | IdP account is invalid |
| 400 | linked_user_not_found | Linked User Not Found | linked user not found |
| 400 | invalid_friend_code_format | ? | ? |
| 400 | user_link_not_exist | ? | ? |
| 400 | invalid_raw_content | Invalid Raw Content | invalid raw content |
| 401 | invalid_token | Token is invalid | The access token was invalid |
| 403 | insufficient_scope | Token is insufficient | The access token does not have sufficient scope |
| 403 | forbidden | ? | ? |
| 403 | membership_required | Membership Required | |
| 403 | unavailable_device_account | Unavailable Device Account | Device Account is unavailable |
| 403 | banned_user | ? | ? |
| 403 | banned_user_by_application | ? | ? |
| 404 | deleted_user | ? | ? |
| 406 | not_acceptable_language | ? | ? |
| 409 | resource_already_exists | ? | ? |
| 409 | user_link_already_exists | ? | ? |
| 412 | precondition_failed | ? | ? |
| 415 | unsupported_media_type | Unsupported Media Type | unsupported media type |
| 422 | friend_code_unregenerable_state | Friend Code Unregenerable State | |
| 500 | internal_server_error | Internal Server Error | Internal Server Error |
| 502 | could_not_confirm_membership | ? | ? |
| 503 | under_maintenance | ? | ? |

## Environments
| Environment | Prefix |
| --- | --- |
| `dd1` | [`e97b8a9d672e4ce4845ec6947cd66ef6-sb`](https://e97b8a9d672e4ce4845ec6947cd66ef6-sb.baas.nintendo.com) |
| `dp1` | [`d9c8ea0e17f68bdeab8674c59f6fabda-sb`](https://d9c8ea0e17f68bdeab8674c59f6fabda-sb.baas.nintendo.com) |
| `jd1` | [`d78dbb1c550d43c6af49bf04c56bc094-sb`](https://d78dbb1c550d43c6af49bf04c56bc094-sb.baas.nintendo.com) |
| `lp1` | [`e0d67c509fb203858ebcb2fe3f88c2aa`](https://e0d67c509fb203858ebcb2fe3f88c2aa.baas.nintendo.com) |
| `sd1` | [`96130dc402837b377c07719e6c9514de-sb`](https://96130dc402837b377c07719e6c9514de-sb.baas.nintendo.com) |
| `sp1` | [`dc219b6b3aa8e06873733fda1def0e03-sb`](https://dc219b6b3aa8e06873733fda1def0e03-sb.baas.nintendo.com) |
| `td1` | [`e03a97819c9711e59510d820a52f298a-sb`](https://e03a97819c9711e59510d820a52f298a-sb.baas.nintendo.com) |
