[Switch](Server-List#switch) > Application Authentication
---

Up to 19.0.1: https://aauth-lp1.ndas.srv.nintendo.net<br>
In 20.0.0 and later: https://aauth.hac.lp1.ndas.srv.nintendo.net

The aauth server provides application tokens. These are required to access game-specific servers, such as [NEX](NEX-Overview-(Game-Servers)) and [NPLN](NPLN-Servers). To obtain an application token, one must first obtain a [device token](DAuth-Server).

![](https://www.dropbox.com/s/jtyzp3pj0xdrzvb/aauth.png?raw=1)

Because the certificates are signed by Nintendo there is only one way to obtain a valid certificate: buy a game and dump it.

The aauth server takes form-encoded requests and responds with json-encoding. It uses base64url, and the client does not add any padding characters.

* [Headers](#headers)
* [Methods](#methods)
* [Errors](#errors)
* [Examples](#examples)

In 20.0.0, the aauth server was moved to a different server, and now requires a device certificate during the handshake.

## Headers
Up to 17.0.1:

| Header | Description |
| --- | --- |
| Host | `aauth-lp1.ndas.srv.nintendo.net` |
| User-Agent | [User agent](#user-agents) |
| Accept | `*/*` |
| X-Nintendo-PowerState | `FA` (fully awake) or `HA` (half awake). This header is only sent in the [application token request](#application-token-request). |
| Content-Length | Content length |
| Content-Type | `application/x-www-form-urlencoded` |

Between 18.0.0 and 19.0.1, the user agent is no longer present and the headers are reordered:

| Header | Description |
| --- | --- |
| Host | `aauth-lp1.ndas.srv.nintendo.net` |
| Accept | `*/*` |
| Content-Type | `application/x-www-form-urlencoded` |
| X-Nintendo-PowerState | `FA` (fully awake) or `HA` (half awake). This header is only sent in the [application token request](#application-token-request). |
| Content-Length | Content length |

In 20.0.0 and later, the user agent is back:

| Header | Description |
| --- | --- |
| Host | `aauth-lp1.ndas.srv.nintendo.net` |
| Accept | `*/*` |
| User-Agent | [User agent](#user-agents) |
| Content-Type | `application/x-www-form-urlencoded` |
| X-Nintendo-PowerState | `FA` (fully awake) or `HA` (half awake). This header is only sent in the [application token request](#application-token-request). |
| Content-Length | Content length |

#### User Agents
| System Version | User agent |
| --- | --- |
| 9.0.0 - 9.2.0 | `libcurl (nnAccount; 789f928b-138e-4b2f-afeb-1acae821d897; SDK 9.3.0.0; Add-on 9.3.0.0)` |
| 10.0.0 - 10.2.0 | `libcurl (nnAccount; 789f928b-138e-4b2f-afeb-1acae821d897; SDK 10.4.0.0; Add-on 10.4.0.0)` |
| 11.0.0 - 11.0.1 | `libcurl (nnHttp; 789f928b-138e-4b2f-afeb-1acae821d897; SDK 11.4.0.0; Add-on 11.4.0.0)` |
| 12.0.0 - 12.1.0 | `libcurl (nnHttp; 789f928b-138e-4b2f-afeb-1acae821d897; SDK 12.3.0.0; Add-on 12.3.0.0)` |
| 13.0.0 | `libcurl (nnHttp; 789f928b-138e-4b2f-afeb-1acae821d897; SDK 13.3.0.0; Add-on 13.3.0.0)` |
| 13.1.0 - 13.2.1 | `libcurl (nnHttp; 789f928b-138e-4b2f-afeb-1acae821d897; SDK 13.4.0.0; Add-on 13.4.0.0)` |
| 14.0.0 - 14.1.2 | `libcurl (nnHttp; 789f928b-138e-4b2f-afeb-1acae821d897; SDK 14.3.0.0; Add-on 14.3.0.0)` |
| 15.0.0 - 15.0.1 | `libcurl (nnHttp; 789f928b-138e-4b2f-afeb-1acae821d897; SDK 15.3.0.0; Add-on 15.3.0.0)` |
| 16.0.0 - 16.1.0 | `libcurl (nnHttp; 789f928b-138e-4b2f-afeb-1acae821d897; SDK 16.2.0.0; Add-on 16.2.0.0)` |
| 17.0.0 - 17.0.1 | `libcurl (nnHttp; 789f928b-138e-4b2f-afeb-1acae821d897; SDK 17.5.0.0; Add-on 17.5.0.0)` |
| 20.0.0 - 20.5.0 | `libcurl (nnDauth; 16f4553f-9eee-4e39-9b61-59bc7c99b7c8; SDK 20.5.4.0)` |
| 21.0.0 - 21.1.0 | `libcurl (nnDauth; 16f4553f-9eee-4e39-9b61-59bc7c99b7c8; SDK 21.4.0.0)` |

## Methods
The following method returns a timestamp and your ip address:

| Method | Path |
| --- | --- |
| GET | [`/v1/time`](#time-request) |

In API version 3 and later, one must solve a cryptographic challenge to prove that the gamecard is inserted. This is not required for digital titles.

| Method | Path |
| --- | --- |
| POST | [`/v3/challenge`](#challenge-request) |
| POST | [`/v4/challenge`](#challenge-request) |
| POST | [`/v5/challenge`](#challenge-request) |

The following methods return an application token as JWT:

| Method | Path |
| --- | --- |
| POST | [`/v1/application_auth_token`](#application-token-request) |
| POST | [`/v2-44cd4221f90742b5f37a4948b37dacf024d0bb14dde86db0af20ec300a36a0fe/application_auth_token`](#application-token-request) |
| POST | [`/v3/application_auth_token`](#application-token-request) |
| POST | [`/v4/application_auth_token`](#application-token-request) |
| POST | [`/v5/application_auth_token`](#application-token-request) |

#### System Versions
| System | API |
| --- | --- |
| 1.0.0 - 4.1.0 | v1 |
| 5.0.0 - 8.1.1 | v2 |
| 9.0.0 - 14.1.2 | v3 |
| 15.0.0 - 18.1.0 | v4 |
| 19.0.0 - 21.1.0 | v5 |

#### API Changes
| API | Changelog |
| --- | --- |
| v1 | Initial version. |
| v2 | The API path is obfuscated with a random hex string. The `environment` parameter was removed. The online play policy was added. For digital titles, the certificate is encrypted with a random key. The `NO_CERT` media type was added. |
| v3 | The API path is no longer obfuscated. The challenge was added for gamecards. |
| v4 | The `cert_key` parameter was removed for digital titles. A token from dragons is now required. |
| v5 | The `media_type` parameter was renamed to `auth_type` and the gamecard challenge was redesigned. |

## Time Request
This method is unrelated to aauth. It returns a `text/plain` document that contains two lines:
1. The current server time in milliseconds
2. The external IP address of the client

It also returns this information in the `X-NINTENDO-UNIXTIME` and `X-NINTENDO-GLOBAL-IP` headers.

This method is no longer used since system version 18.0.0. It is replaced by a [ctest server](https://github.com/kinnay/NintendoClients/wiki/Connection-Test).

## Challenge Request
This request is only required if the media type is `GAMECARD`.

| Param | Description |
| --- | --- |
| device_auth_token | Device token from [dauth server](DAuth-Server) |

Note: up to system version 17.0.1, the device_auth_token was preceded by an ampersand, even though it is the first and only parameter in the request.

Response on success, up to version 4:

| Field | Description |
| --- | --- |
| value | Base64-encoded (16 bytes) |
| seed | Base64-encoded (15 bytes) |

Version 5:

| Field | Description |
| --- | --- |
| challenge | Base64-encoded (32 bytes) |
| challenge_src | Base64-encoded (9 bytes) |
| seed | Base64-encoded (15 bytes) |

The seed value never changes. It is even consistent across environments.

## Application Token Request
This method returns an application token as JWT. Certificates can be dumped with [nxdumptool](https://github.com/DarkMatterCore/nxdumptool). For digital titles, always dump the base ticket and do not remove console specific data.

### Version 1

| Param | Description |
| --- | --- |
| application_id | Title id (`%016x`) |
| application_version | Title version (`%08x`) |
| environment | `lp1` |
| device_auth_token | Device token from [dauth server](DAuth-Server) |
| media_type | `GAMECARD`, `DIGITAL` or `SYSTEM` |

If the media type is `GAMECARD` or `DIGITAL`:

| Param | Description |
| --- | --- |
| cert | Base64-encoded application certificate |

Response on success:

| Field | Description |
| --- | --- |
| expires_in | Expiration in seconds (86400) |
| application_auth_token | Application token |
| settings | Settings (see below) |

The settings field contains a list of objects with the following fields:

| Field | Description |
| --- | --- |
| nas:client_id | 16 hex digits |
| nas:redirect_uri | `nintendo://<title id>.app` |

For most titles, the settings list is empty.

### Version 2
The environment parameter was removed, the cert_key parameter was added, and the online play policy was added to the response.

The `NO_CERT` media type is used if the Switch does not have a valid ticket for a digital title. On production systems, this can only happen if the title was installed through unofficial means, which is usually a piracy attempt. Using `NO_CERT` will ban your device.

| Param | Description |
| --- | --- |
| application_id | Title id (`%016x`) |
| application_version | Title version (`%08x`) |
| device_auth_token | Device token from [dauth server](DAuth-Server) |
| media_type | `GAMECARD`, `DIGITAL`, `SYSTEM` or `NO_CERT` |

If the media type is `GAMECARD`:

| Param | Description |
| --- | --- |
| cert | Base64-encoded gamecard certificate (512 bytes) |

If the media type is `DIGITAL`:

| Param | Description |
| --- | --- |
| cert | Encrypted ticket (base64) |
| cert_key | Encrypted key (base64) |

For digital titles, the ticket is no longer sent to the server in plain text. Instead, it is encrypted with AES-CBC with a random key (the IV is filled with zeroes). The key itself is then encrypted with RSA-OAEP with SHA256.

Public exponent: `65537`

Modulus:
```
2903599220185509629948246004681271806662185201109683699434876284
9306378942456577312580648895443616535088601867223713942187399041
4854872772034425863387471719375473684104853507768450203982749294
8967945831738920699512732919046223059402955082098739033920491649
6879108565068863591362496844602988110766097564477545097467537357
3183749964356608012071405755940871989007021731074728723470759285
8155278592486462922448753256166071381157786436864032235809243318
2591089355065715995209202752330511548478896205428626608544326862
4782505679727111312756904637828438785474471375120478991907979820
98870089661523253199182993983393803812441
```

Response on success:

| Field | Description |
| --- | --- |
| expires_in | Expiration in seconds (86400) |
| application_auth_token | Application token |
| settings | Settings |
| online_play_policy | `MEMBERSHIP_REQUIRED` or `FREE` |
| policy_handler | `SYSTEM` or `GAME_SERVER` (only present if membership is required) |

### Version 3
A challenge is now required if the media type is `GAMECARD`:

| Param | Description |
| --- | --- |
| application_id | Title id (`%016x`) |
| application_version | Title version (`%08x`) |
| device_auth_token | Device token from [dauth server](DAuth-Server) |
| media_type | `GAMECARD` |
| gvt | Base64-encoded challenge reply, based on the seed and value from the [challenge](#challenge-request) (88 bytes) |
| cert | Base64-encoded gamecard certificate (512 bytes) |

The `gvt` parameter is calculated with <code><a href="https://switchbrew.org/wiki/Lotus3#ChallengeCardExistence">ChallengeCardExistence</a></code>. I have no idea how this works.

### Version 4
For digitial titles, the Switch no longer sends the application certificate to the server. Instead, it requests a contents authorization token from the [dragons server](Dragons-Servers).

| Param | Description |
| --- | --- |
| application_id | Title id (`%016x`) |
| application_version | Title version (`%08x`) |
| device_auth_token | Device token from [dauth server](DAuth-Server) |
| media_type | `DIGITAL` |
| cert | Contents authorization token from [dragons server](Dragons-Servers) |

### Version 5
The media_type parameter was renamed to auth_type. The challenge and challenge_src parameters were added for gamecard authentication.

| Param | Description |
| --- | --- |
| application_id | Title id (`%016x`) |
| application_version | Title version (`%08x`) |
| device_auth_token | Device token from [dauth server](DAuth-Server) |
| media_type | `GAMECARD` |
| gvt | Base64-encoded challenge reply, based on the seed and value from the [challenge](#challenge-request) (88 bytes) |
| cert | Base64-encoded gamecard certificate (512 bytes) |
| challenge | Challenge |
| challenge_src | Challenge src |

## System Titles
The following titles can be used with the `SYSTEM` media type:

* `010000000000002f` (NPNS)
* `010000000000003a` (Migration)
* `010000000000003e` (OLSC)
* `0100000000000040` (ND)
* `0100000000000044` (?)

## Errors
On error, the server sends the following response:

| Field | Description |
| --- | --- |
| errors | List of errors |

Every error is encoded like this:

| Field | Description |
| --- | --- |
| code | Error code (string with 4 digits) |
| message | Error message |

### Known Errors
| Code | Message |
| --- | --- |
| 0103 | Device token expired. |
| 0105 | ROM ID has been banned. |
| 0106 | Unauthorized application. |
| 0107 | ? |
| 0108 | ? |
| 0109 | Service closed. |
| 0110 | ? |
| 0111 | Application update is required. |
| 0112 | Internal Server Error. |
| 0113 | ? |
| 0118 | Invalid parameter in request. |
| 0120 | ? |
| 0121 | Region mismatch. |

## Examples
The `/v1/time` request is very simple:

```
GET /v1/time HTTP/1.1
Host: aauth-lp1.ndas.srv.nintendo.net
Accept: */*
```

Example of `/v1/time` response:

```
HTTP/1.1 200 OK
Server: nginx
Date: Thu, 30 Sep 2021 14:02:21 GMT
Content-Type: text/plain; charset=utf-8
Transfer-Encoding: chunked
Connection: keep-alive
X-Frame-Options: SAMEORIGIN
X-XSS-Protection: 1; mode=block
X-Content-Type-Options: nosniff
X-Download-Options: noopen
X-Permitted-Cross-Domain-Policies: none
Referrer-Policy: strict-origin-when-cross-origin
X-NINTENDO-UNIXTIME: 1633003341066
X-NINTENDO-GLOBAL-IP: 93.184.216.34
Vary: Accept
ETag: W/"7c7283f8b06feb54a9d29b679a4ca0af"
Cache-Control: max-age=0, private, must-revalidate
X-RequestId: 297b792a-f6f2-456b-a3ca-66c6e73620b7
X-Runtime: 0.000683
X-Nintendo-Used-Directive: global auth
X-Nintendo-Request-Host-Header: aauth-lp1.ndas.srv.nintendo.net
X-Nintendo-Request-SNI: aauth-lp1.ndas.srv.nintendo.net

1633003341066
93.184.216.34
```

To authenticate gamecards one must first obtain a challenge:

```
POST /v3/challenge HTTP/1.1
Host: aauth-lp1.ndas.srv.nintendo.net
User-Agent: libcurl (nnHttp; 789f928b-138e-4b2f-afeb-1acae821d897; SDK 13.3.0.0; Add-on 13.3.0.0)
Accept: */*
Content-Length: 857
Content-Type: application/x-www-form-urlencoded

&device_auth_token=eyJqa3UiOiJodHRwczovL2RjZXJ0LWxwMS5uZGFzLnNydi5uaW50ZW5kby5uZXQva2V5cyIsImtpZCI6IjM2NzllMTg4LTI5ZWUtNDE4Zi04ZDkwLWI3MjRjYzg1MzQ0MSIsInR5cCI6IkpXVCIsImFsZyI6IlJTMjU2In0.eyJzdWIiOiI2ODMzN2FjYTI4ODE1Y2JiIiwiaXNzIjoiZGF1dGgtbHAxLm5kYXMuc3J2Lm5pbnRlbmRvLm5ldCIsImF1ZCI6IjhmODQ5YjVkMzQ3NzhkOGUiLCJleHAiOjE2MzI3NjMzMDEsImlhdCI6MTYzMjY3NjkwMSwianRpIjoiZTU5YTBiMGUtOTRlMS00NGFhLWI1ZGItMGZjMGNmNTAyYWRhIiwibmludGVuZG8iOnsic24iOiJYQVcxMDAxMjM0NTY3OCIsInBjIjoiSEFDIiwiZHQiOiJOWCBQcm9kIDEiLCJpc3QiOmZhbHNlfX0.Mdl42B_tWnQQZkpp0qkvEwpkAFGos1YQ8OBKDr_rJCQlNVZLrP6_sd53U8kvwI6TWbnuxFtNxcVJh21kbbY23WsjwQN9Ph2pbjEmneov5b5SfAjWSvfEqt_ViKFQVLv_MZZXQpBYZSQmJ3sA-BbOjeEO6JI5XI3_KR0uj9IxSH_LNSiEwMMNLkP0PcC3gO5cSKcmnb1NPW2BMMdlKOSIbxDSWE4sEuYt2Pl_u2F6hVMVeoC-4z43lIv2tv7aF9Pwv-D7MR-mOxQaxYVHw2Ux4FL0zPZOJMU6qPgfzACeItd6H_A4OBMKSQwBl4DEbSwdle5tph-ur01K91FhXhI6BA
```

```
HTTP/1.1 200 OK
Server: nginx
Date: Sun, 26 Sep 2021 19:21:43 GMT
Content-Type: application/json; charset=utf-8
Transfer-Encoding: chunked
X-Frame-Options: SAMEORIGIN
X-XSS-Protection: 1; mode=block
X-Content-Type-Options: nosniff
X-Download-Options: noopen
X-Permitted-Cross-Domain-Policies: none
Referrer-Policy: strict-origin-when-cross-origin
Vary: Accept
ETag: W/"eff6fe99a35dd733bdb7e43956f9db16"
Cache-Control: max-age=0, private, must-revalidate
X-Request-Id: b782a5a4-739a-47d6-b061-aa2cbfa4bea2
X-Runtime: 0.005265
X-Nintendo-Used-Directive: global auth
X-Nintendo-Request-Host-Header: aauth-lp1.ndas.srv.nintendo.net
X-Nintendo-Request-SNI: aauth-lp1.ndas.srv.nintendo.net
Connection: keep-alive

{"value":"XLYSEWCMMwSUlU4wJC3VBA==","seed":"wLJ0JZCC3cu5KSU8bLbe"}
```

Then one can obtain an application token for a gamecard:

```
POST /v3/application_auth_token HTTP/1.1
Host: aauth-lp1.ndas.srv.nintendo.net
User-Agent: libcurl (nnHttp; 789f928b-138e-4b2f-afeb-1acae821d897; SDK 13.3.0.0; Add-on 13.3.0.0)
Accept: */*
X-Nintendo-PowerState: FA
Content-Length: 1749
Content-Type: application/x-www-form-urlencoded
Expect: 100-continue

application_id=0100abf008968000&application_version=00070000&device_auth_token=eyJqa3UiOiJodHRwczovL2RjZXJ0LWxwMS5uZGFzLnNydi5uaW50ZW5kby5uZXQva2V5cyIsImtpZCI6IjM2NzllMTg4LTI5ZWUtNDE4Zi04ZDkwLWI3MjRjYzg1MzQ0MSIsInR5cCI6IkpXVCIsImFsZyI6IlJTMjU2In0.eyJzdWIiOiI2ODMzN2FjYTI4ODE1Y2JiIiwiaXNzIjoiZGF1dGgtbHAxLm5kYXMuc3J2Lm5pbnRlbmRvLm5ldCIsImF1ZCI6IjhmODQ5YjVkMzQ3NzhkOGUiLCJleHAiOjE2MzI3NjMzMDEsImlhdCI6MTYzMjY3NjkwMSwianRpIjoiZTU5YTBiMGUtOTRlMS00NGFhLWI1ZGItMGZjMGNmNTAyYWRhIiwibmludGVuZG8iOnsic24iOiJYQVcxMDAxMjM0NTY3OCIsInBjIjoiSEFDIiwiZHQiOiJOWCBQcm9kIDEiLCJpc3QiOmZhbHNlfX0.Mdl42B_tWnQQZkpp0qkvEwpkAFGos1YQ8OBKDr_rJCQlNVZLrP6_sd53U8kvwI6TWbnuxFtNxcVJh21kbbY23WsjwQN9Ph2pbjEmneov5b5SfAjWSvfEqt_ViKFQVLv_MZZXQpBYZSQmJ3sA-BbOjeEO6JI5XI3_KR0uj9IxSH_LNSiEwMMNLkP0PcC3gO5cSKcmnb1NPW2BMMdlKOSIbxDSWE4sEuYt2Pl_u2F6hVMVeoC-4z43lIv2tv7aF9Pwv-D7MR-mOxQaxYVHw2Ux4FL0zPZOJMU6qPgfzACeItd6H_A4OBMKSQwBl4DEbSwdle5tph-ur01K91FhXhI6BA&media_type=GAMECARD&gvt=xvzGsqK2NF5qWDKzGb71HYGqqIMVe4B78jBDy8zRXg9X3eMNDhtBHS6QVn_07O2eAdaCAKDgrd2CJ6vOgkfisWG4MIGViKO98YiaTEu6xT9SkmKDOTgJog&cert=_W2lx8BZrU3zHi3eeV6VBzEpxWYeyzAdy_Q49_Sq7u7my6ZY_QxzTggxvMIfhkFGiLPhEmtH5McHbAA3Ecb5wnr7Q0C2UD8Kijkt7QgwBGe6gY__nyhe34o-8Y-PFPzaos5b9UmWTAPPHMhIav1Br7XuK0wHKbdYToc_UZ45YFVUWcKWZbSkPRI4zVP_hKNtWvFMmzhRGIEvcA3tA1ormTWDUSSBaxasgo3FSEKQHJaJpq-K3XwWRX4h8DRXierAYwpLCPRpI92C8QJjWhwumAVDa4Dlc1YtE08iEjQ0ZuFAGV2UPXoz57OznzeqP077uodFnKZmMv07576XEbobyENFUlQAAAAAAAAAAAAAAABy4lviwORBYWj1Lz_TAxxdABAAAAAAAAAAAAlTU7O6Za21K9jZis87UO27ERAIoxTcyvpqMWZb7_qhzPystmkcIvWH0ENCfilg6fb2d5m5nY-RQhToEMU2qa_GCZrsPFUENAaN4jVfjYWk5GXX4tk3e-XJTcfyv2Q0oysuwqFGuyww_Ok7XjyTmvVu_7KhPM8oP4ixzoNTHe1cxAmsGi7qATnUN9ke5dIzlhqd7RNqIxz2kibJXV8iKX_BXvRgeepYfVQoIpVxQNFyitqOKy_RZ6LDvA82-C5E1d6hMTj6YQ0oxBhMTRg9N0tNwoQJQ4Y
```

For a digital title:

```
POST /v3/application_auth_token HTTP/1.1
Host: aauth-lp1.ndas.srv.nintendo.net
User-Agent: libcurl (nnHttp; 789f928b-138e-4b2f-afeb-1acae821d897; SDK 13.3.0.0; Add-on 13.3.0.0)
Accept: */*
X-Nintendo-PowerState: FA
Content-Length: 2254
Content-Type: application/x-www-form-urlencoded
Expect: 100-continue

application_id=0100abf008968000&application_version=00070000&device_auth_token=eyJqa3UiOiJodHRwczovL2RjZXJ0LWxwMS5uZGFzLnNydi5uaW50ZW5kby5uZXQva2V5cyIsImtpZCI6IjM2NzllMTg4LTI5ZWUtNDE4Zi04ZDkwLWI3MjRjYzg1MzQ0MSIsInR5cCI6IkpXVCIsImFsZyI6IlJTMjU2In0.eyJzdWIiOiI2ODMzN2FjYTI4ODE1Y2JiIiwiaXNzIjoiZGF1dGgtbHAxLm5kYXMuc3J2Lm5pbnRlbmRvLm5ldCIsImF1ZCI6IjhmODQ5YjVkMzQ3NzhkOGUiLCJleHAiOjE2MzI3NjMzMDEsImlhdCI6MTYzMjY3NjkwMSwianRpIjoiZTU5YTBiMGUtOTRlMS00NGFhLWI1ZGItMGZjMGNmNTAyYWRhIiwibmludGVuZG8iOnsic24iOiJYQVcxMDAxMjM0NTY3OCIsInBjIjoiSEFDIiwiZHQiOiJOWCBQcm9kIDEiLCJpc3QiOmZhbHNlfX0.Mdl42B_tWnQQZkpp0qkvEwpkAFGos1YQ8OBKDr_rJCQlNVZLrP6_sd53U8kvwI6TWbnuxFtNxcVJh21kbbY23WsjwQN9Ph2pbjEmneov5b5SfAjWSvfEqt_ViKFQVLv_MZZXQpBYZSQmJ3sA-BbOjeEO6JI5XI3_KR0uj9IxSH_LNSiEwMMNLkP0PcC3gO5cSKcmnb1NPW2BMMdlKOSIbxDSWE4sEuYt2Pl_u2F6hVMVeoC-4z43lIv2tv7aF9Pwv-D7MR-mOxQaxYVHw2Ux4FL0zPZOJMU6qPgfzACeItd6H_A4OBMKSQwBl4DEbSwdle5tph-ur01K91FhXhI6BA&media_type=DIGITAL&cert=Ea_BETtJ5tBzI730PfZO2md_qU705gnovFqRjsgw4NbPqQDw_b8H_ecpqm2NbBYs4i3ls95PjSUNHAcV5Yqv36v_wO2eSKyz09YCMo5-eN5DYmyjXaSgy8Fb-Qu0H0VGciRIrx5PNpUJIs7JqV6faPacffFoL4Ac74x6oLtWlRGdgTW7J-cq5ij0O3YNAX_3PoucRi0-xapIVHwRiFUzsj8KM3ug4QttmqVMPW8OAFUWFkGqmsyW_riWRsfDu0srLna4UEc9RxQMbecR-Qw3wyMl5JjCkfA05QLo0MECrhiQE10-yfmlu-ti1pg3wu9y_yiWEJdvgN58H4vlW_n4KL-xDFIdlkQsc4pd3RuL8NwxTSKP_Z2HTyDULs_XpbBejThr59xMGMUdrLOGnxwKiCsjM6SS0P6EpSQSjn4ASns6S1ImTbIvgj8LH4M8wck51XxjOBUz3T_03JQIn9PxObe_OOVfCobKeQXCtKjrvIq40AXg2v2ljj_K7vu8ZmtLMpliexg3dHhr6RgP1TA_tWDLaG_osxnk3XnPDz9FYLLhfugWL2ujsaoNezBOZuKw4CXQ5-IRFk0tWj9lIQvXs8_UFkJXSLIvsS_rs5X3ZaZ0Oc1F8Crt-0Iqgo6g3l259EtwMy6o89yWvU7hSMJ2DfiCEf298eVPMYs95SiTb3bW-wZYfGxVaMJ1XErqlojCi_rSmn9UlHCLgV9PEBK2iF-uAPt1CVxIaejB_7XHtg0bLdMq2OkiyAKHmEFHNPfOvKeJSNh5VQVp18EWbXrio2BXdn0-2UygI8AiTuqq3ummNd6yrNOfU-NNrt5Hccaa6QxsDXCeUlRDmds-lJJJAARL04_E4nZZTnxQE5_sImSkFLBQv8UMjTt0QIFBL_TeR3BkeAi7PSa1YQ0c0_2Bmix7OUuCO1G2mCBGkePVedGPEenm6A9iFNJkyiAhtKBc&cert_key=Tkyp0lOXSP-SEDZ5ShslGnoM1JweZj5kavHTdTnzZaAazXZdTkhaosxZYv2YVL1oqOD7Vmf4orO0Ns85HFGJ8s7cd6dQzvrpyu1uaN4Wum_w5OCf5ld_ga4M8F9TTEUYlAQz0Ft3f9zED0IWOGXqMU0t536XejUQxIUZlNWKBsWT_PZn1nOEcNSeTVHJ5He7QBF6Om99JUvl_qy3v_OppBsBoLdZf_F2miwjCFs0AO7wyf_boK7uU4v-6MtGA8fyyJQgXlAn8SAQTEL3lYVFJyED-Xkel99V8W_3egdnIMvvbJLSRIpLdqjfHqlK32KAcRpzT8J6koc3BkvBhYzNEQ
```

Or for a system title:

```
POST /v3/application_auth_token HTTP/1.1
Host: aauth-lp1.ndas.srv.nintendo.net
User-Agent: libcurl (nnHttp; 789f928b-138e-4b2f-afeb-1acae821d897; SDK 13.3.0.0; Add-on 13.3.0.0)
Accept: */*
X-Nintendo-PowerState: FA
Content-Length: 935
Content-Type: application/x-www-form-urlencoded

application_id=010000000000003e&application_version=00000000&device_auth_token=eyJqa3UiOiJodHRwczovL2RjZXJ0LWxwMS5uZGFzLnNydi5uaW50ZW5kby5uZXQva2V5cyIsImtpZCI6IjM2NzllMTg4LTI5ZWUtNDE4Zi04ZDkwLWI3MjRjYzg1MzQ0MSIsInR5cCI6IkpXVCIsImFsZyI6IlJTMjU2In0.eyJzdWIiOiI2ODMzN2FjYTI4ODE1Y2JiIiwiaXNzIjoiZGF1dGgtbHAxLm5kYXMuc3J2Lm5pbnRlbmRvLm5ldCIsImF1ZCI6IjhmODQ5YjVkMzQ3NzhkOGUiLCJleHAiOjE2MzI3NjMzMDEsImlhdCI6MTYzMjY3NjkwMSwianRpIjoiZTU5YTBiMGUtOTRlMS00NGFhLWI1ZGItMGZjMGNmNTAyYWRhIiwibmludGVuZG8iOnsic24iOiJYQVcxMDAxMjM0NTY3OCIsInBjIjoiSEFDIiwiZHQiOiJOWCBQcm9kIDEiLCJpc3QiOmZhbHNlfX0.Mdl42B_tWnQQZkpp0qkvEwpkAFGos1YQ8OBKDr_rJCQlNVZLrP6_sd53U8kvwI6TWbnuxFtNxcVJh21kbbY23WsjwQN9Ph2pbjEmneov5b5SfAjWSvfEqt_ViKFQVLv_MZZXQpBYZSQmJ3sA-BbOjeEO6JI5XI3_KR0uj9IxSH_LNSiEwMMNLkP0PcC3gO5cSKcmnb1NPW2BMMdlKOSIbxDSWE4sEuYt2Pl_u2F6hVMVeoC-4z43lIv2tv7aF9Pwv-D7MR-mOxQaxYVHw2Ux4FL0zPZOJMU6qPgfzACeItd6H_A4OBMKSQwBl4DEbSwdle5tph-ur01K91FhXhI6BA&media_type=SYSTEM
```

Response example:

```
HTTP/1.1 200 OK
Server: nginx
Date: Sun, 26 Sep 2021 19:21:43 GMT
Content-Type: application/json; charset=utf-8
Transfer-Encoding: chunked
Connection: keep-alive
...
X-Nintendo-Used-Directive: global auth
X-Nintendo-Request-Host-Header: aauth-lp1.ndas.srv.nintendo.net
X-Nintendo-Request-SNI: aauth-lp1.ndas.srv.nintendo.net

{"expires_in":86400,"application_auth_token":"eyJqa3UiOiJodHRwczovL2FjZXJ0LWxwMS5uZGFzLnNydi5uaW50ZW5kby5uZXQva2V5cyIsImtpZCI6IjZiMjVhNGU4LTRiOWItNDJhMy1hZDJiLWVhYzRiZGJjOWQ0NiIsInR5cCI6IkpXVCIsImFsZyI6IlJTMjU2In0.eyJzdWIiOiIwMTAwYWJmMDA4OTY4MDAwIiwiZXhwIjoxNjMyNzYzMzAxLCJpYXQiOjE2MzI2NzY5MDEsImlzcyI6ImFhdXRoLWxwMS5uZGFzLnNydi5uaW50ZW5kby5uZXQiLCJqdGkiOiI4MmRmNjY3Yi0wZGExLTQzODEtODdlNC0xYWU0MDNjOGI1NjgiLCJuaW50ZW5kbyI6eyJhaSI6IjAxMDBhYmYwMDg5NjgwMDAiLCJhdiI6IjAwMDciLCJhdCI6MTYzMjY3NjkwMSwiZWRpIjoiYjQ2YmRhNGUxZGQ1ZTdjZTAwMjQzMGE2OGIyYzZkNGUiLCJvcHAiOiJNRU1CRVJTSElQX1JFUVVJUkVEIiwicGgiOiJHQU1FX1NFUlZFUiJ9fQ.bVRnffmMbfN3Q-XAEHAt8qa-QPQf-jOBQMwhhMu0hWOUK3UGviDiG4fti_ws6-0vaYxsAisiong051wUhDi0MyzN9BSsJ1nTA0mB6rRfCeqdsdbgRz6hWP4lRgeuzeyVSX6NTIQvdIJTYsqd800i1tkpR2ynTBVwUHwcle9vqNWuIkzZgl-osk439AP70vV2okLSFoSP49EGH6UW7ocgstto9xwy39DiY93y8Di0uX-GvYQK_inAxaIgMUCLBcKJzZ8iwUKV8E1MeD-yWNWGJ9nW9F5kPa6mvDFBOdzcvIYYTjnKh2JSJLS2-nlNyTZoN8t3OfTVLwd3KlDj0HhzZA","settings":[],"online_play_policy":"MEMBERSHIP_REQUIRED","policy_handler":"GAME_SERVER"}
```

Or if an error has occurred:

```
HTTP/1.1 400 Bad Request
Server: nginx
Date: Sun, 26 Sep 2021 19:21:43 GMT
Content-Type: application/json; charset=utf-8
Transfer-Encoding: chunked
Connection: keep-alive
X-Frame-Options: SAMEORIGIN
X-XSS-Protection: 1; mode=block
X-Content-Type-Options: nosniff
X-Download-Options: noopen
X-Permitted-Cross-Domain-Policies: none
Referrer-Policy: strict-origin-when-cross-origin
Vary: Accept
Cache-Control: no-cache
X-Request-Id: ae8b948d-a0ca-4073-a41a-2393a69f12c6
X-Runtime: 0.006897

{"errors": [{"code": "0118", "message": "Invalid parameter in request."}]}
```