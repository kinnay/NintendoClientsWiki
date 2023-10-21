[Switch Server](Server-List#switch) > System Update Check
---

The sun server only has one function: providing the latest system update version.

The sun server takes JSON-encoded requests and respond with JSON-encoding. The sun server only accepts requests with a valid device certificate.

* [Header](#headers)
* [Methods](#methods)
* [Errors](#errors)

## Headers
| Header | Description |
| --- | --- |
| Host | `sun.hac.lp1.d4c.nintendo.net` |
| User-Agent | [User agent](#user-agents) |
| Accept | `application/json` |

### User Agents
The user agent looks as follows: `NintendoSDK Firmware/<firmware version>-<revision> (platform:NX; did:<device id>; eid:lp1)`. The firmware version and revision number are obtained from the [system version title](https://switchbrew.org/wiki/System_Version_Title).

Here is an example: `NintendoSDK Firmware/15.0.0-4.0 (platform:NX; did:6265ca40780b1c0d; eid:lp1)`

## Methods

| Method | Path |
| --- | --- |
| GET | [`/v1/system_update_meta`](#get-v1system_update_meta) |

## GET /v1/system_update_meta
| Param | Description |
| --- | --- |
| device_id | Device id |

Response on success:

| Field | Description |
| --- | --- |
| timestamp | Current server time |
| system_update_metas | Array (see below) |

The system_update_metas array has exactly one entry, with the following fields:

| Field | Description |
| --- | --- |
| title_id | Latest system update title id |
| title_version | Latest system update title version |

Example:

```
GET /v1/system_update_meta?device_id=6265ca40780b1c0d HTTP/1.1
Host: sun.hac.lp1.d4c.nintendo.net
User-Agent: NintendoSDK Firmware/17.0.0-6.0 (platform:NX; did:6265ca40780b1c0d; eid:lp1)
Accept: application/json
```

```
HTTP/1.1 200 OK
Content-Type: application/json
Server: Apache
Content-Length: 107
Date: Sat, 21 Oct 2023 20:36:08 GMT
x-nintendo-akamai-reference-id: 0.902e0388.1697920568.236fe13
Connection: keep-alive

{"timestamp":1697920335,"system_update_metas":[{"title_id":"0100000000000816","title_version":1140851708}]}
```

## Errors
On error, the server sends the following response:

| Field | Description |
| --- | --- |
| error | Error info (see below) |

The error info has the following fields:

| Field | Description |
| --- | --- |
| code | Error code |
| message | Error message |

### Known Errors
| Status | Code | Message |
| --- | --- | --- |
| 404 | `000-5700` | Not Found |
