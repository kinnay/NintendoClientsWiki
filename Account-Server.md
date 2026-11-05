[[Server List]] > Account Server (Wii U)
---

The account server always responds with an XML body. GET requests are form-encoded. POST and PUT requests have an XML body.

The XML-encoding is not consistent between URLs. Usually, the response contains no XML declaration and no whitespace. However, sometimes the response starts with `<?xml version="1.0" encoding="UTF-8" standalone="yes"?>`, and sometimes the response is prettified using 4 spaces as indentation.

The common client certificate is needed to connect to these servers.

Main server: https://account.nintendo.net

Other servers:
* https://game-dev.account.nintendo.net
* https://system-dev.account.nintendo.net
* https://library-dev.account.nintendo.net
* https://staging.account.nintendo.net

## Methods
The following methods can be used without authorization:

| Method | URL |
| --- | --- |
| GET | <code><a href="#get-v1apiadmintime">/v1/api/admin/time</a></code> |
| GET | <code><a href="#get-v1apiadminmapped_ids">/v1/api/admin/mapped_ids</a></code> |
| GET | `/v1/api/content/agreements/Nintendo-Network-EULA/<country>/@latest` |
| GET | `/v1/api/content/time_zones/<country>/<language>` |
| DELETE | `/v1/api/devices/@current` |
| PUT | `/v1/api/devices/@current/inactivate` |
| POST | `/v1/api/devices/@current/migrations` |
| DELETE | `/v1/api/devices/@current/migrations` |
| POST | `/v1/api/devices/@current/migrations/commit` |
| GET | `/v1/api/devices/@current/status` |
| GET | `/v1/api/miis` |
| POST | <code><a href="#post-v1apioauth20access_tokengenerate">/v1/api/oauth20/access_token/generate</a></code> |
| POST | <code><a href="#post-v1apipeople">/v1/api/people</a></code> |
| GET | [`/v1/api/people/<nnid>`](#get-v1apipeoplennid)  |
| POST | `/v1/api/support/coppa/authorization` |
| PUT | `/v1/api/support/email_confirmation/<%lu>/<%06u>` |
| GET | `/v1/api/support/forgotten_password/<%lu>` |
| POST | `/v1/api/support/parental_approval` |
| GET | `/v1/api/support/parental_approval/send_email/coppa_code` |
| GET | `/v1/api/support/resend_confirmation` |
| GET | `/v1/api/support/send_confirmation/pin` |
| GET | `/v1/api/support/send_forgotten/pin` |
| POST | `/v1/support/validate/email` |

The following methods access your account data and require a `Bearer` authorization token. This token can be retrieved with <code><a href="#post-v1apioauth20access_tokengenerate">/v1/api/oauth20/access_token/generate</a></code>.

| Method | URL |
| --- | --- |
| PUT | `/v1/api/people/@me` |
| DELETE | `/v1/api/people/@me` |
| POST | `/v1/api/people/@me/deletion` |
| GET | `/v1/api/people/@me/devices` |
| DELETE | `/v1/api/people/@me/devices/@current` |
| POST | `/v1/api/people/@me/devices/@current/attributes` |
| PUT | `/v1/api/people/@me/devices/@current/inactive` |
| GET | `/v1/api/people/@me/emails` |
| PUT | `/v1/api/people/@me/miis/@primary` |
| GET | `/v1/api/people/@me/profile` |
| GET | <code><a href="#get-v1apiprovidernex_tokenme">/v1/api/provider/nex_token/@me</a></code> |
| GET | `/v1/api/provider/service_token/@me` |

The following methods require a `HashedBasic` authorization token.

| Method | URL |
| --- | --- |
| POST | `/v1/api/people/@me/agreements` |
| POST | `/v1/api/people/@me/devices` |
| GET | `/v1/api/people/@me/devices/owner` |

## Headers
The following headers are included in requests by the Wii U:

| Field | Description |
| --- | --- |
| X-Nintendo-Platform-ID | Always 1 |
| X-Nintendo-Device-Type | 1=Debug, 2=Retail |
| X-Nintendo-Device-ID | Unsigned integer (MCP_GetDeviceId) |
| X-Nintendo-Serial-Number | String |
| X-Nintendo-System-Version | Version of `version.bin` title (`%04X`) |
| X-Nintendo-Region | 1=JPN, 2=USA, 4=EUR, 8=AUS, 16=CHN, 32=KOR, 64=TWN |
| X-Nintendo-Country | JP for Japan, DE for Germany, etc. |
| X-Nintendo-Client-ID | a2efa818a34fa16b8afbc8a74eba3eda |
| X-Nintendo-Client-Secret | c91cdb5658bd4954ade78533a339cf9a |
| X-Nintendo-FPD-Version | Always "0000"? |
| X-Nintendo-Environment | Lx/Dx/Sx/Tx/Jx (default: L1) |
| X-Nintendo-Title-ID | Example: 0005000010138300 |
| X-Nintendo-Unique-ID | Part of title id, example: 01383 |
| X-Nintendo-Application-Version | Title version |
| X-Nintendo-Device-Cert | [Device certificate](#device-certificate) |

The server replies with the following headers, in addition to `Content-Type` (if applicable), `Content-Length` and `Date`:

| Header | Description |
| --- | --- |
| X-Nintendo-Date | Server timestamp (in milliseconds) |
| Server | `Nintendo 3DS (http)` |

### GET /v1/api/admin/time
This request does not take an parameters. The response body is empty, and no `Content-Type` header is returned by the server. The server time can be retrieved from the `X-Nintendo-Date` header.

### GET /v1/api/admin/mapped_ids
Converts between PID and NNID. PIDs starts at 1799999999 and decrement on every new account.

| Param | Description |
| --- | --- |
| input_type | "pid" or "user_id" |
| output_type | "pid" or "user_id" |
| input | comma-separated list |

Example response:
```
<mapped_ids>
  <mapped_id>
    <in_id>Kinnay-WiiU</in_id>
    <out_id>1798037410</out_id>
  </mapped_id>
</mapped_ids>
```

### POST /v1/api/oauth20/access_token/generate
This method generates an access token. The access token can be included in the "Authorization" header, and is needed for all requests that require access to your account data.

There are two ways to request an access token: using NNID and password or password hash, or using a refresh token from an earlier access token request.

The password hash can be calculated using the following method:
```
data = struct.pack("<I", pid) + b"\x02\x65\x43\x46" + password.encode("ascii")
hash = hashlib.sha256(data).digest()
```

| Field | Description |
| --- | --- |
| grant_type | "password" |
| user_id | NNID |
| password | Password or password hash |
| password_type (optional) | "hash" |

| Field | Description |
| --- | --- |
| grant_type | "refresh_token" |
| refresh_token | Refresh token |

Example response:
```
<OAuth20>
  <access_token>
    <token>...</token>
    <refresh_token>...</refresh_token>
    <expires_in>3600</expires_in>
  </access_token>
</OAuth20>
```

### GET /v1/api/provider/nex_token/@me
Provides login information and location of game server.

| Param | Description |
| --- | --- |
| game_server_id | Game server id |

Example response:
```
<nex_token>
  <host>34.208.166.202</host>
  <nex_password>...</nex_password>
  <pid>1798037410</pid>
  <port>43220</port>
  <token>...</token>
</nex_token>
```
### GET /v1/api/people/&lt;nnid&gt;
Checks if the given NNID is in use.

It will give this error if it is in use:
```
<errors> 
	<error> 
		<code>0100</code> 
		<message>Account ID already exists</message> 
	</error> 
</errors>
```
Otherwise it will return nothing, still with the content type of `text/xml`.

### POST /v1/api/people
Creates a new NNID

The console sends an xml request containing the user data:
```
<person>
  <birth_date>BIRTHDAY IN YYYY-MM-DD FORMAT</birth_date>
  <user_id>USERNAME</user_id>
  <password>PASSWORD</password>
  <country>COUNTRY</country>
  <language>LANGUAGE</language>
  <tz_name>TIMEZONE NAME</tz_name>
  <agreement>
    <agreement_date>TIME OF AGREEMENT</agreement_date>
    <country>COUNTRY</country>
    <type>NINTENDO-NETWORK-EULA</type>
    <version>VERSION OF AGREEMENT</version>
  </agreement>
  <email>
    <address>EMAIL</address>
    <owned>N</owned>
    <parent>N</parent>
    <primary>Y</primary>
    <validated>N</validated>
    <type>DEFAULT</type>
  </email>
  <gender>M or F</gender>
  <region>REGION CODE</region>
  <marketing_flag>N</marketing_flag>
  <off_device_flag>N</off_device_flag>
  <mii>
    <name>MII NAME</name>
    <primary>Y</primary>
    <data>MII DATA IN BASE64</data>
  </mii>
</person>
```
On success it sends back the user's PID:
```
<person> 
	<pid>1234567890</pid> 
</person>
```

## Errors
Here's an example error response:
```
<errors>
  <error>
    <cause>client_id</cause>
    <code>0004</code>
    <message>API application invalid or incorrect application credentials</message>
  </error>
</errors>
```

Sometimes, the cause tag is closed immediately (`<cause/>`). Sometimes, it is omitted entirely.

In some cases it can give multiple errors in the same response like this:
```
<errors>
	<error>
		<cause>data</cause>
		<code>0002</code>
		<message>data format is invalid</message>
	</error>
	<error>
		<cause>X-Nintendo-Region</cause>
		<code>0002</code>
		<message>X-Nintendo-Region format is invalid</message>
	</error>
</errors>

```

### Known Errors
| Code | Cause | Message |
| --- | --- | --- |
| 0002 | | deviceId format is invalid |
| 0002 | | serialNumber format is invalid |
| 0002 | data | data format is invalid |
| 0002 | | platformId format is invalid |
| 0002 | | version format is invalid |
| 0002 | user_id | user_id format is invalid |
| 0002 | password | password format is invalid |
| 0002 | X-Nintendo-Region | X-Nintendo-Region format is invalid |
| 0004 | grant_type | Invalid Grant Type |
| 0004 | client_id | API application invalid or incorrect application credentials |
| 0005 | access_token | Invalid access token |
| 0007 | Forbidden request |
| 0008 | | Not Found |
| 0100 | | Account ID already exists |
| 0101 | userId | Account ID is not acceptable  |
| 0103 | email | Email format is invalid |
| 0106 | | Invalid account ID or password |
| 0107 | | Account country and device country do not match |
| 0110 | | Unlinked device |
| 0113 | | Unauthorized device |
| 0113 | device_id | Unauthorized device |
| 0118 | | Unique ID and Game Server ID are not linked |
| 0123 | | Service has expired |
| 0124 | | Application version is older than usable version registered |
| 1017 | | The requested game environment wasn't found for the given game server. |
| 1022 | client_id | The requested client was not found. |
| 1033 | | Excessive forgot password e-mail attempt |
| 1126 | | The domain "..." is not accessible. |
| 1500 | The request sent by the client was syntactically incorrect. | Bad Request Error | 
| 1600 | Bad Request | Unable to process request |
| 1600 | Unsupported Media Type | Unable to process request |
| 2001 | | Internal server error |

| Code | Description |
| --- | --- |
| 1 | BAD_FORMAT_PARAMETER |
| 2 | BAD_FORMAT_REQUEST |
| 3 | REQUEST_PARAMETER_MISSING |
| 4 | UNAUTHORIZED_CLIENT |
| 5 | INVALID_ACCOUNT_TOKEN |
| 6 | ACCOUNT_TOKEN_EXPIRED |
| 7 | REQUEST_FORBIDDEN |
| 8 | REQUEST_NOT_FOUND |
| 9 | WRONG_HTTP_METHOD |
| 10 | INVALID_PLATFORM_ID |
| 11 | SYSTEM_UPDATE_REQUIRED |
| 12 | BANNED_DEVICE_ALL |
| 100 | ACCOUNT_ID_ALREADY_EXISTS |
| 101 | ACCOUNT_ID_NOT_ACCEPTABLE |
| 103 | MAIL_ADDRESS_NOT_ACCEPTABLE |
| 104 | UNAUTHORIZED_DEVICE |
| 105 | REACHED_REGISTRATION_LIMIT |
| 106 | WRONG_ACCOUNT_PASSWORD |
| 107 | COUNTRY_MISMATCH |
| 108 | BANNED_ACCOUNT_ALL |
| 110 | DEVICE_MISMATCH |
| 111 | ACCOUNT_ID_CHANGED |
| 112 | ACCOUNT_ALREADY_DELETED |
| 114 | COPPA_NOT_ACCEPTED |
| 115 | REACHED_ASSOCIATION_LIMIT |
| 116 | WRONG_CONFIRMATION_CODE |
| 117 | CONFIRMATION_CODE_EXPIRED |
| 118 | GAME_SERVER_ID_UNIQUE_ID_NOT_LINKED |
| 119 | BANNED_ACCOUNT_IN_APPLICATION |
| 120 | BANNED_DEVICE_IN_APPLICATION |
| 121 | BANNED_ACCOUNT_IN_NEX_SERVICE |
| 122 | BANNED_DEVICE_IN_NEX_SERVICE |
| 123 | SERVICE_CLOSED |
| 124 | APPLICATION_UPDATE_REQUIRED |
| 125 | CLIENT_ID_UNIQUE_ID_NOT_LINKED |
| 126 | BANNED_ACCOUNT_IN_INDEPENDENT_SERVICE |
| 127 | BANNED_DEVICE_IN_INDEPENDENT_SERVICE |
| 128 | MAIL_ADDRESS_NOT_VALIDATED |
| 129 | WRONG_BIRTH_DATE_OR_MAIL_ADDRESS |
| 130 | PID_NOT_FOUND |
| 131 | WRONG_ACCOUNT_MAIL |
| 132 | BANNED_ACCOUNT_ALL_TEMPORARILY |
| 134 | BANNED_ACCOUNT_IN_APPLICATION_TEMPORARILY |
| 136 | BANNED_ACCOUNT_IN_NEX_SERVICE_TEMPORARILY |
| 137 | BANNED_DEVICE_IN_NEX_SERVICE_TEMPORARILY |
| 138 | BANNED_ACCOUNT_IN_INDEPENDENT_SERVICE_TEMPORARILY |
| 139 | BANNED_DEVICE_IN_INDEPENDENT_SERVICE_TEMPORARILY |
| 142 | COPPA_AGREEMENT_CANCELED |
| 143 | DEVICE_INACTIVE |
| 1004 | EULA_NOT_ACCEPTED |
| 1006 | INVALID_UNIQUE_ID |
| 1016 | NEX_ACCOUNT_NOT_FOUND |
| 1017 | GAME_SERVER_ID_ENVIRONMENT_NOT_FOUND |
| 1018 | GENERATE_TOKEN_FAILURE |
| 1019 | INVALID_NEX_CLIENT_ID |
| 1020 | INVALID_CLIENT_KEY |
| 1021 | INVALID_GAME_SERVER_ID |
| 1022 | INVALID_CLIENT_ID |
| 1023 | WRONG_MAIL_ADDRESS |
| 1024 | MASTER_PIN_NOT_FOUND |
| 1025 | MAIL_TEXT_NOT_FOUND |
| 1031 | SEND_MAIL_FAILURE |
| 1032 | DOMAIN_ACCOUNT_ALREADY_EXISTS |
| 1033 | EXCESSIVE_MAIL_SEND_REQUEST |
| 1035 | CREDIT_CARD_GENERAL_FAILURE |
| 1036 | CREDIT_CARD_DATE_EXPIRED |
| 1037 | CREDIT_CARD_DECLINED |
| 1038 | INVALID_CREDIT_CARD_NUMBER |
| 1039 | CREDIT_CARD_NUMBER_WRONG |
| 1040 | INVALID_CREDIT_CARD_DATE |
| 1041 | CREDIT_CARD_BLACKLISTED |
| 1042 | INVALID_CREDIT_CARD_PIN |
| 1043 | CREDIT_CARD_PIN_WRONG |
| 1044 | INVALID_LOCATION |
| 1045 | INVALID_POSTAL_CODE |
| 1046 | DEVICE_EULA_COUNTRY_MISMATCH |
| 1100 | INVALID_EULA_COUNTRY |
| 1101 | INVALID_EULA_COUNTRY_AND_VERSION |
| 1103 | PARENTAL_CONTROLS_REQUIRED |
| 1104 | ACCOUNT_ID_FORMAT_INVALID |
| 1105 | WRONG_ACCOUNT_PASSWORD_OR_MAIL_ADDRESS |
| 1106 | AUTHENTICATION_LOCKED |
| 1107 | ACCOUNT_ID_PASSWORD_SAME |
| 1111 | APPROVAL_ID_NOT_FOUND |
| 1115 | PENDING_MIGRATION |
| 1125 | MAIL_ADDRESS_DOMAIN_NAME_NOT_ACCEPTABLE |
| 1126 | MAIL_ADDRESS_DOMAIN_NAME_NOT_RESOLVED |
| 1200 | NOT_PROVIDED_COUNTRY |
| 2001 | INTERNAL_SERVER_ERROR |
| 2002 | UNDER_MAINTENANCE |
| 2999 | NINTENDO_NETWORK_CLOSED |

## Device Certificate
This header is only sent in the requests for:
* `/v1/api/oauth20/access_token/generate`
* `/v1/api/people`
* `/v1/api/people/@me/agreements`
* `/v1/api/people/@me/devices`
* `/v1/api/people/@me/devices/owner`

The device certificate consists of 384 base64-encoded bytes:

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 0x4 | Signature type:<br>`0x00010002`: SHA-1 (debug)<br>`0x00010005`: SHA-256 (retail) |
| 0x4 | 0x3C | Signature |
| 0x40 | 0x40 | Padding |
| 0x80 | 0x40 | `Root-CA<%08X>-MS<%08X>` |
| 0xC0 | 0x4 | Key type (always 2) |
| 0xC4 | 0x40 | Device id (`NG<%08X>`) |
| 0x104 | 0x4 | NG key id |
| 0x108 | 0x78 | Public key |
