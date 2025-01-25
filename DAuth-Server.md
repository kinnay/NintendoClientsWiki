[Switch](Server-List#switch) > Device Authentication
---

URL: https://dauth-lp1.ndas.srv.nintendo.net

Many Switch servers can only be accessed after obtaining a token from the dauth server. The dauth server only accepts requests with a valid client certificate. Every Switch has its own client certificate, which stored in [PRODINFO](https://switchbrew.org/wiki/Calibration).

![](https://www.dropbox.com/s/cwubnhmd5neum9k/dauth.png?raw=1)

Because the certificate is signed by Nintendo there is only one way to get a valid certificate: buy a Switch and dump it.

The dauth server takes form-encoded requests and responds with json-encoding. It uses base64url, and the client does not add any padding characters.

* [Headers](#headers)
* [Methods](#methods)
* [Errors](#errors)
* [Examples](#examples)

## Headers
Up to 17.0.1:

| Header | Description |
| --- | --- |
| Host | `dauth-lp1.ndas.srv.nintendo.net` |
| User-Agent | [User agent](#user-agents) |
| Accept | `*/*` |
| X-Nintendo-PowerState | `FA` (fully awake) or `HA` (half awake) (7.0.0 and later, see note below)|
| Content-Length | Content length |
| Content-Type | `application/x-www-form-urlencoded` |

The X-Nintendo-PowerState header is only present on system version 7.0.0 and later. In 7.0.0, there is a space between `X-Nintendo-PowerState` and the colon. This was fixed in 7.0.1.

In 18.0.0 and later, the user agent is no longer present and the headers are reordered:

| Header | Description |
| --- | --- |
| Host | `dauth-lp1.ndas.srv.nintendo.net` |
| Accept | `*/*` |
| Content-Type | `application/x-www-form-urlencoded` |
| X-Nintendo-PowerState | `FA` (fully awake) or `HA` (half awake) |
| Content-Length | Content length |

#### User Agents
| System Version | User agent |
| --- | --- |
| 1.0.0 | `libcurl (nnAccount; 789f928b-138e-4b2f-afeb-1acae821d897; SDK 0.16.29.0; Add-on 0.11.29.0)` |
| 2.0.0 - 2.3.0 | `libcurl (nnAccount; 789f928b-138e-4b2f-afeb-1acae821d897; SDK 1.3.0.0; Add-on 1.3.0.0)` |
| 3.0.0 - 3.0.2 | `libcurl (nnAccount; 789f928b-138e-4b2f-afeb-1acae821d897; SDK 3.4.0.0; Add-on 3.4.0.0)` |
| 4.0.0 - 4.1.0 | `libcurl (nnAccount; 789f928b-138e-4b2f-afeb-1acae821d897; SDK 4.4.0.0; Add-on 4.4.0.0)` |
| 5.0.0 - 5.1.0 | `libcurl (nnDauth; 789f928b-138e-4b2f-afeb-1acae821d897; SDK 5.3.0.0; Add-on 5.3.0.0)` |
| 6.0.0 - 6.1.0 | `libcurl (nnHttp; 789f928b-138e-4b2f-afeb-1acae821d897; SDK 6.4.0.0; Add-on 6.4.0.0)` |
| 6.2.0 | `libcurl (nnDauth; 16f4553f-9eee-4e39-9b61-59bc7c99b7c8; SDK 6.4.0.0)` |
| 7.0.0 - 7.0.1 | `libcurl (nnDauth; 16f4553f-9eee-4e39-9b61-59bc7c99b7c8; SDK 7.3.0.0)` |
| 8.0.0 | `libcurl (nnDauth; 16f4553f-9eee-4e39-9b61-59bc7c99b7c8; SDK 8.2.99.0)` |
| 8.0.1 - 8.1.1 | `libcurl (nnDauth; 16f4553f-9eee-4e39-9b61-59bc7c99b7c8; SDK 8.2.0.0)` |
| 9.0.0 - 9.2.0 | `libcurl (nnDauth; 16f4553f-9eee-4e39-9b61-59bc7c99b7c8; SDK 9.3.0.0)` |
| 10.0.0 - 10.2.0 | `libcurl (nnDauth; 16f4553f-9eee-4e39-9b61-59bc7c99b7c8; SDK 10.4.0.0)` |
| 11.0.0 - 11.0.1 | `libcurl (nnDauth; 16f4553f-9eee-4e39-9b61-59bc7c99b7c8; SDK 11.4.0.0)` |
| 12.0.0 - 12.1.0 | `libcurl (nnDauth; 16f4553f-9eee-4e39-9b61-59bc7c99b7c8; SDK 12.3.0.0)` |
| 13.0.0 | `libcurl (nnDauth; 16f4553f-9eee-4e39-9b61-59bc7c99b7c8; SDK 13.3.0.0)` |
| 13.1.0 - 13.2.1 | `libcurl (nnDauth; 16f4553f-9eee-4e39-9b61-59bc7c99b7c8; SDK 13.4.0.0)` |
| 14.0.0 - 14.1.2 | `libcurl (nnDauth; 16f4553f-9eee-4e39-9b61-59bc7c99b7c8; SDK 14.3.0.0)` |
| 15.0.0 - 15.0.1 | `libcurl (nnDauth; 16f4553f-9eee-4e39-9b61-59bc7c99b7c8; SDK 15.3.0.0)` |
| 16.0.0 - 16.1.0 | `libcurl (nnDauth; 16f4553f-9eee-4e39-9b61-59bc7c99b7c8; SDK 16.2.0.0)` |
| 17.0.0 - 17.0.1 | `libcurl (nnDauth; 16f4553f-9eee-4e39-9b61-59bc7c99b7c8; SDK 17.5.0.0)` |

No user agent is present in system version 18.0.0 and later.

## Methods
In API version 3 and later, one must perform a cryptographic challenge to obtain a device token or edge token:

| Method | Path |
| --- | --- |
| POST | [`/v3-59ed5fa1c25bb2aea8c4d73d74b919a94d89ed48d6865b728f63547943b17404/challenge`](#challenge-request) |
| POST | [`/v4-fb411cdeda62ff6da97e57c29d6300bc12b6b709869e56906aec88cb42a299cd/challenge`](#challenge-request) |
| POST | [`/v5/challenge`](#challenge-request) |
| POST | [`/v6/challenge`](#challenge-request) |
| POST | [`/v7/challenge`](#challenge-request) |

The following methods return a device token as JWT:

| Method | Path |
| --- | --- |
| POST | [`/v1/device_auth_token`](#device-token-request) |
| POST | [`/439528b578b74475d24ec19264097f17d2cc578c8584816b644e7b7fa93044d7/device_auth_token`](#device-token-request) |
| POST | [`/v3-59ed5fa1c25bb2aea8c4d73d74b919a94d89ed48d6865b728f63547943b17404/device_auth_token`](#device-token-request) |
| POST | [`/v4-fb411cdeda62ff6da97e57c29d6300bc12b6b709869e56906aec88cb42a299cd/device_auth_token`](#device-token-request) |
| POST | [`/v5/device_auth_token`](#device-token-request) |
| POST | [`/v6/device_auth_token`](#device-token-request) |
| POST | [`/v7/device_auth_token`](#device-token-request) |

The following methods return a different kind of device token:

| Method | Path |
| --- | --- |
| POST | [`/v3-59ed5fa1c25bb2aea8c4d73d74b919a94d89ed48d6865b728f63547943b17404/edge_token`](#edge-token-request) |
| POST | [`/v4-fb411cdeda62ff6da97e57c29d6300bc12b6b709869e56906aec88cb42a299cd/edge_token`](#edge-token-request) |
| POST | [`/v5/edge_token`](#edge-token-request) |
| POST | [`/v6/edge_token`](#edge-token-request) |
| POST | [`/v7/edge_token`](#edge-token-request) |

#### System Versions
| System | API |
| --- | --- |
| 1.0.0 - 3.0.0 | v1 |
| 3.0.1 - 4.1.0 | v2 |
| 5.0.0 - 6.1.0 | v3 |
| 6.2.0 | v4 |
| 7.0.0 - 8.1.1 | v5 |
| 9.0.0 - 12.1.0 | v6 |
| 13.0.0 - 19.0.1 | v7 |

#### API Changes
| API | Changelog |
| --- | --- |
| v1 | Initial version. |
| v2 | The API path is obfuscated with random hex string. |
| v3 | The challenge was added and the format of the system version parameter was changed. Device authentication now requires knowledge of the master key, and the client can no longer fake an unreleased system version. Also, the `edge_token` route was added. |
| v4 | The prefix of the system version digest was changed. |
| v5 | The `X-Nintendo-PowerState` header was added. The API path is no longer obfuscated. |
| v6 | The `ist` parameter was added. |
| v7 | The `vendor_id` parameter was added to the edge token request. |

## Challenge Request
| Param | Description |
| --- | --- |
| key_generation | [Master key revision](#master-key-revisions) |

Response:

| Field | Description |
| --- | --- |
| challenge | Base64-encoded challenge (35 bytes) |
| data | Base64-encoded AES key required for MAC calculation (16 bytes) |

The data value never changes, but it depends on the given key generation. It is even consistent across environments. The challenge value is valid for one minute.

The challenge field used to contain 32 unknown bytes. However, at the end of 2024, the challenge was updated and contains the following 35 bytes instead:

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 1 | Always 2 |
| 0x1 | 4 | Timestamp |
| 0x5 | 1 | Always 0 or 2 |
| 0x6 | 29 | Unknown |

Since the challenge is treated as an opaque piece of data, no changes were needed on the client side.

At the same time, the server stopped adding base64 padding to the challenge and data fields.

## Device Token Request
This method returns a device token as JWT.

### Version 1 - 2

| Param | Description |
| --- | --- |
| client_id | Application-specific [client id](#known-client-ids) |
| system_version | System version (`%08x`) |

Response on success:

| Field | Description |
| --- | --- |
| expires_in | Expiration in seconds (86400) |
| device_auth_token | Device token |

### Version 3 - 5
A challenge was added and the format of the system version parameter was changed:

| Param | Description |
| --- | --- |
| challenge | Base64-encoded [challenge](#challenge-request) |
| client_id | Application-specific [client id](#known-client-ids) |
| key_generation | [Master key revision](#master-key-revisions) |
| system_version | [System version digest](https://switchbrew.org/wiki/System_Version_Title) |
| mac | Base64-encoded AES-CMAC of all previous fields in form-encoding |

The key for the AES-CMAC is calculated as follows, using AES-ECB:
1. The `aes_kek_generation_source` is decrypted with the master key.
2. The dauth key source is decrypted with the key from step 1.
3. The key from the `data` field of the challenge is decrypted with the key from step 2.

The dauth key source is: `8be45abcf987021523ca4f5e2300dbf0`

### Version 6 - 7
An `ist` parameter was added:

| Param | Description |
| --- | --- |
| challenge | Base64-encoded [challenge](#challenge-request) |
| client_id | Application-specific [client id](#known-client-ids) |
| ist | `true` or `false` (depends on [platform region](https://switchbrew.org/wiki/Settings_services#GetT)) |
| key_generation | [Master key revision](#master-key-revisions) |
| system_version | [System version digest](https://switchbrew.org/wiki/System_Version_Title) |
| mac | Base64-encoded AES-CMAC of all previous fields in form-encoding |

## Edge Token Request
This method returns a different kind of device token. Up to v6, it takes the same parameters as [`/device_auth_token`](#device-token-request).

Response on success:

| Field | Description |
| --- | --- |
| expires_in | Expiration in seconds (86400) |
| dtoken | Device token |

### Version 7
A `vendor_id` parameter was added:

| Param | Description |
| --- | --- |
| challenge | Base64-encoded [challenge](#challenge-request) |
| client_id | Application-specific [client id](#known-client-ids) |
| ist | `true` or `false` (depends on [platform region](https://switchbrew.org/wiki/Settings_services#GetT)) |
| key_generation | [Master key revision](#master-key-revisions) |
| system_version | [System version digest](https://switchbrew.org/wiki/System_Version_Title) |
| vendor_id | `akamai`, `llnw` or `lumen` |
| mac | Base64-encoded AES-CMAC of all previous fields in form-encoding |

## Master Key Revisions
| System version | Key generation |
| --- | --- |
| 5.0.0 - 5.1.0 | 5 |
| 6.0.0 - 6.1.0 | 6 |
| 6.2.0 | 7 |
| 7.0.0 - 8.0.1 | 8 |
| 8.1.0 - 8.1.1 | 9 |
| 9.0.0 - 9.0.1 | 10 |
| 9.1.0 - 12.1.0 | 11 |
| 13.0.0 - 13.2.1 | 13 |
| 14.0.0 - 14.1.2 | 14 |
| 15.0.0 - 15.0.1 | 15 |
| 16.0.0 - 16.1.0 | 16 |
| 17.0.0 - 18.1.0 | 17 |
| 19.0.0 - 19.0.1 | 19 |

## Known Client IDs
| Client ID | Description | Edge |
| --- | --- | --- |
| `146c8ac7b8a0db52` | SCSI storage | Yes |
| `3117b250cab38f45` | Atum and IDBE | Yes |
| `41f4a6491028e3c4` | Pushmo and Tagaya | Yes |
| `67bf9945b45248c6` | BCAT | Yes |
| `6ac5a6873fe5f68c` | SATA storage | No |
| `75fe236362ff5f8b` | [Account server](Account-Server-(Switch)) | No |
| `81333c548b2e876d` | [Account server](Account-Server-(Switch)) | No |
| `83b72b05dc3278d7` | NPNS | No |
| `8f849b5d34778d8e` | [AAuth](AAuth-Server) and [BaaS](BAAS-Server) | No |
| `93af0acb26258de9` | Beach and Bugyo | Yes |
| `bad8156f44ac935a` | SProfile | No |
| `d5b6cac2c1514c56` | Dragons | No |
| `dc656ea03b63cf68` | Parental controls | No |
| `df51c436bc01c437` | Prepo | No |
| `e58171fe439390ce` | Penne | No |

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
For more detailed descriptions, see below.

Most errors use HTTP status code 400. The only known exception is error 0009, which uses status code 500.

| Code | Message |
| --- | --- |
| 0004 | Unauthorized device. |
| 0007 | System update is required. |
| 0008 | Device has been banned. |
| 0009 | Internal Server Error. |
| 0010 | ? |
| 0011 | ? |
| 0013 | ? |
| 0014 | Invalid parameter in request. |
| 0015 | Invalid parameter in request. |
| 0016 | Invalid parameter in request. |
| 0017 | This device might be broken. |
| 0018 | ? |
| 0019 | ? |
| 0020 | ? |
| 0021 | ? |
| 0022 | ? |
| 0023 | ? |
| 0024 | ? |
| 0025 | ? |
| 0026 | ? |
| 0027 | ? |
| 0028 | ? |
| 0029 | ? |
| 0030 | ? |
| 0031 | ? |

| Code | Description |
| --- | --- |
| 0004 | The device certificate belongs to a different environment. |
| 0007 | A system update is required. |
| 0008 | The device is banned permanently. |
| 0009 | An internal server error has occurred. |
| 0014 | Generic error. |
| 0015 | The challenge has expired. |
| 0016 | The MAC is wrong. |
| 0017 | The device is banned. |

## Examples
Note that the client must always use a valid device certificate as the client certificate. If the client does not provide a certificate, the nginx server used to reject the request:

```
HTTP/1.1 400 Bad Request
Server: nginx
Date: Sun, 26 Sep 2021 19:21:43 GMT
Content-Type: text/html
Content-Length: 246
Connection: close

<html>
<head><title>400 No required SSL certificate was sent</title></head>
<body bgcolor="white">
<center><h1>400 Bad Request</h1></center>
<center>No required SSL certificate was sent</center>
<hr><center>nginx</center>
</body>
</html>
```

Nowadays, the server terminates the connection immediately after the TLS handshake instead.

Before anything else, one must obtain a challenge:

```
POST /v7/challenge HTTP/1.1
Host: dauth-lp1.ndas.srv.nintendo.net
User-Agent: libcurl (nnDauth; 16f4553f-9eee-4e39-9b61-59bc7c99b7c8; SDK 13.3.0.0)
Accept: */*
X-Nintendo-PowerState: FA
Content-Length: 17
Content-Type: application/x-www-form-urlencoded

key_generation=13
```

```
HTTP/1.1 200 OK
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
ETag: W/"eb797bb39b7f70a033c7bbd5020bf9f0"
Cache-Control: max-age=0, private, must-revalidate
X-Request-Id: b1afb7d0-b6d9-4eff-8561-0159c97cdf58
X-Runtime: 0.009675
X-Nintendo-Used-Directive: global auth
X-Nintendo-Request-Host-Header: dauth-lp1.ndas.srv.nintendo.net
X-Nintendo-Request-SNI: dauth-lp1.ndas.srv.nintendo.net

{"challenge":"mtAvqNqzYSoCEixxL_rjWoHfdDjAH51h5XcKZ6ksq2s=","data":"1OikFLkHptkhDpqy7VHb3g=="}
```

Then, one can obtain a device token:

```
POST /v7/device_auth_token HTTP/1.1
Host: dauth-lp1.ndas.srv.nintendo.net
User-Agent: libcurl (nnDauth; 16f4553f-9eee-4e39-9b61-59bc7c99b7c8; SDK 13.3.0.0)
Accept: */*
X-Nintendo-PowerState: FA
Content-Length: 211
Content-Type: application/x-www-form-urlencoded

challenge=mtAvqNqzYSoCEixxL_rjWoHfdDjAH51h5XcKZ6ksq2s=&client_id=8f849b5d34778d8e&ist=false&key_generation=13&system_version=CusHY#000d0000#r1xneESd4PiTRYIhVIl0bK1ST5L5BUmv_uGPLqc4PPo=&mac=AW9LE1TSN0xrzY1FfHHXwg
```

```
HTTP/1.1 200 OK
Server: nginx
Date: Sun, 26 Sep 2021 19:21:43 GMT
Content-Type: application/json; charset=utf-8
Transfer-Encoding: chunked
Connection: keep-alive
...
X-Nintendo-Used-Directive: global auth
X-Nintendo-Request-Host-Header: dauth-lp1.ndas.srv.nintendo.net
X-Nintendo-Request-SNI: dauth-lp1.ndas.srv.nintendo.net

{"expires_in":86400,"device_auth_token":"eyJqa3UiOiJodHRwczovL2RjZXJ0LWxwMS5uZGFzLnNydi5uaW50ZW5kby5uZXQva2V5cyIsImtpZCI6IjM2NzllMTg4LTI5ZWUtNDE4Zi04ZDkwLWI3MjRjYzg1MzQ0MSIsInR5cCI6IkpXVCIsImFsZyI6IlJTMjU2In0.eyJzdWIiOiI2ODMzN2FjYTI4ODE1Y2JiIiwiaXNzIjoiZGF1dGgtbHAxLm5kYXMuc3J2Lm5pbnRlbmRvLm5ldCIsImF1ZCI6IjhmODQ5YjVkMzQ3NzhkOGUiLCJleHAiOjE2MzI3NjMzMDEsImlhdCI6MTYzMjY3NjkwMSwianRpIjoiZTU5YTBiMGUtOTRlMS00NGFhLWI1ZGItMGZjMGNmNTAyYWRhIiwibmludGVuZG8iOnsic24iOiJYQVcxMDAxMjM0NTY3OCIsInBjIjoiSEFDIiwiZHQiOiJOWCBQcm9kIDEiLCJpc3QiOmZhbHNlfX0.Mdl42B_tWnQQZkpp0qkvEwpkAFGos1YQ8OBKDr_rJCQlNVZLrP6_sd53U8kvwI6TWbnuxFtNxcVJh21kbbY23WsjwQN9Ph2pbjEmneov5b5SfAjWSvfEqt_ViKFQVLv_MZZXQpBYZSQmJ3sA-BbOjeEO6JI5XI3_KR0uj9IxSH_LNSiEwMMNLkP0PcC3gO5cSKcmnb1NPW2BMMdlKOSIbxDSWE4sEuYt2Pl_u2F6hVMVeoC-4z43lIv2tv7aF9Pwv-D7MR-mOxQaxYVHw2Ux4FL0zPZOJMU6qPgfzACeItd6H_A4OBMKSQwBl4DEbSwdle5tph-ur01K91FhXhI6BA"}
```

Or an edge token:

```
POST /v7/edge_token HTTP/1.1
Host: dauth-dd1.ndas.srv.nintendo.net
User-Agent: libcurl (nnDauth; 16f4553f-9eee-4e39-9b61-59bc7c99b7c8; SDK 13.3.0.0)
Accept: */*
X-Nintendo-PowerState: FA
Content-Length: 228
Content-Type: application/x-www-form-urlencoded

challenge=mtAvqNqzYSoCEixxL_rjWoHfdDjAH51h5XcKZ6ksq2s=&client_id=67bf9945b45248c6&ist=false&key_generation=13&system_version=CusHY#000d0000#r1xneESd4PiTRYIhVIl0bK1ST5L5BUmv_uGPLqc4PPo=&vendor_id=akamai&mac=8HKiiCC5Zqp3zxut8sSWZw
```

```
HTTP/1.1 200 OK
Server: nginx
Date: Sun, 26 Sep 2021 19:21:43 GMT
Content-Type: application/json; charset=utf-8
Transfer-Encoding: chunked
Connection: keep-alive
...
X-Nintendo-Used-Directive: global auth
X-Nintendo-Request-Host-Header: dauth-dd1.ndas.srv.nintendo.net
X-Nintendo-Request-SNI: dauth-dd1.ndas.srv.nintendo.net

{"expires_in":86400,"dtoken":"exp=1632763301~acl=%2F%2A~data=sub=68337aca28815cbb.sn=XAW10012345678.id=a73ff2b9-e772-4dc6-a01e-0861227bd202~hmac=bb7c0f27edddeb50777ec6a2fba6deacd8b8fc04faeaaaa864027c54767dea6c"}
```

Example of an error response:

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
X-Request-Id: 84a8a661-a312-480a-b389-35cf83106b51
X-Runtime: 0.007699

{"errors":[{"code":"0014","message":"Invalid parameter in request."}]}
```