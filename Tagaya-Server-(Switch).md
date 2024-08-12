[Switch](Server-List#switch) > Title Version List
---

The tagaya server provides the latest version number for each title. The tagaya server only accepts requests with a valid device certificate and requires an [edge token](DAuth-Server).

* [Header](#headers)
* [Methods](#methods)

## Headers
| Header | Description |
| --- | --- |
| Host | `tagaya.hac.lp1.eshop.nintendo.net` |
| User-Agent | [User agent](#user-agents) |
| Accept | `application/json` |
| If-None-Match | Last known ETag (optional) |
| X-Nintendo-DenebEdgeToken | [Edge token](DAuth-Server) |

The If-None-Match header is only present if the Switch has already requested a version list after the last reboot.

In earlier system versions, the User-Agent header appeared after all other headers.

### User Agents
The user agent looks as follows: `NintendoSDK Firmware/<firmware version>-<revision> (platform:NX; did:<device id>; eid:lp1)`. The firmware version and revision number are obtained from the [system version title](https://switchbrew.org/wiki/System_Version_Title).

Here is an example: `NintendoSDK Firmware/15.0.0-4.0 (platform:NX; did:6265ca40780b1c0d; eid:lp1)`

## Methods
| Method | Path |
| --- | --- |
| GET | [`/tagaya/hac_versionlist`](#get-tagayahac_versionlist) |

## GET /tagaya/hac_versionlist
This method returns the latest version list:

| Field | Description |
| --- | --- |
| titles | List of titles and version numbers |
| format_version | Always 1 |
| last_modified | Timestamp at which the list was last modified |

Every entry in the title list contains the following fields:

| Field | Description |
| --- | --- |
| id | Title id |
| version | Latest title version |
| required_version | Required title version to play online |

Example:

```
GET /tagaya/hac_versionlist HTTP/1.1
Host: tagaya.hac.lp1.eshop.nintendo.net
User-Agent: NintendoSDK Firmware/18.1.0-1.0 (platform:NX; did:6265ca40780b1c0d; eid:lp1)
Accept: application/json
X-Nintendo-DenebEdgeToken: exp=1723559081~acl=%2F%2A~data=sub=6265ca40780b1c0d.sn=XAW10012345678.id=034b569d-54be-4072-8f4d-31108b5ea054~hmac=8b3d5d6b7e60d774af3a1b11dddcc98769e46713b984344c4fc70a14dab1ab83
```

```
HTTP/1.1 200 OK
Content-Type: application/octet-stream
ETag: "5b73da0cf0e2ff2251cd5f55052000aa"
Last-Modified: Mon, 12 Aug 2024 13:15:03 GMT
Server: AmazonS3
x-amz-id-2: rzLg9iqqL/NCak+AeyH9jXJx76qExql0giDJSLublZYnUWi3sbhxos1/HHF8pj2vVnOR2KzEbjM=
x-amz-request-id: 6R2D9T51Y52ZQARD
x-amz-server-side-encryption: AES256
Date: Mon, 12 Aug 2024 13:41:52 GMT
Transfer-Encoding: chunked
x-nintendo-akamai-reference-id: 0.d5519e97.1723470112.646ab36
Connection: keep-alive

{"titles":[{"id":"01007ef00011e800","version":786432,"required_version":786432},{"id":"0100bce000598800","version":65536,"required_version":65536},{"id":"010053d0001be800","version":262144,"required_version":262144},{"id":"0100cd3000bdc800","version":196608,"required_version":196608}],"format_version":1,"last_modified":1723468500}
```

(In reality the response is much bigger, close to 10,000 titles).