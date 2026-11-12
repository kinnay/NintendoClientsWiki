[Switch](Server-List#switch) > Title Information
---

The Pegasus server provides title information, such as the latest version list and platform list. The Pegasus server only accepts requests with a valid device certificate and requires an [edge token](DAuth-Server).

* [User agents](#user-agents)
* [Methods](#methods)

The Pegasus server was initially introduced in system version 20.0.0. In system version 23.0.0, the Pegasus server became a replacement for the [Tagaya](Tagaya-Server-(Switch)) server.

### User Agents
The user agent looks as follows: `NintendoSDK Firmware/<firmware version>-<revision> (platform:NX; did:<device id>; eid:lp1)`. The firmware version and revision number are obtained from the [system version title](https://switchbrew.org/wiki/System_Version_Title).

Here is an example: `NintendoSDK Firmware/23.0.1-1.0 (platform:NX; did:6265ca40780b1c0d; eid:lp1)`

## Methods
| Method | Path |
| --- | --- |
| GET | [`/v1/versionlist`](#get-v1versionlist) |
| GET | [`/v1/ratinglist`](#get-v1ratinglist) |
| GET | [`/v1/apps/<title id>/recommend-versions`](#get-v1appstitle-idrecommend-versions) |
| POST | [`/v1/apps/search`](#post-v1appssearch) |
| ? | `/v1/apps/<title id>/latest/platforms` |

## GET /v1/versionlist
This method was first used in system version 23.0.0. It replaces the [Tagaya server](Tagaya-Server-(Switch)).

This method returns the latest version list:

| Field | Description |
| --- | --- |
| lastModified | Timestamp at which the list was last modified |
| cnmts | Title list |
| formatVersion | Always 2 |

Every entry in the title list contains the following fields:

| Field | Description |
| --- | --- |
| id | Title id |
| version | Latest title version |
| requiredVersion | Required title version to play online |

Example:

```
GET /v1/versionlist HTTP/1.1
Host: pegasus.hac.lp1.pegasus.srv.nintendo.net
User-Agent: NintendoSDK Firmware/23.0.1-1.0 (platform:NX; did:6265ca40780b1c0d; eid:lp1)
Accept: application/json
X-Nintendo-DenebEdgeToken: exp=1791077276~acl=%2F%2A~data=sub=6265ca40780b1c0d.sn=XAW10012345678.id=b99373ae-1c33-4502-96fa-f6b0f5f05a11~hmac=402b48874f35fd56177927f78967c4e024087d1cfbe9715efbf5d9db6b4837ab
```

```
HTTP/1.1 200 OK
Content-Type: application/json
Server: nginx
Cache-Control: public, max-age=24
Date: Sat, 03 Oct 2026 02:10:44 GMT
Content-Length: 900812
x-nintendo-akamai-reference-id: 0.d5519e97.1723470112.646ab36
Connection: keep-alive

{"lastModified":1790959426,"cnmts":[{"id":"0100000000010800","version":393216,"requiredVersion":393216},{"id":"010000000eef0800","version":65536,"requiredVersion":65536}],"formatVersion":2}
```

(In reality the response is much bigger and contains more than 10,000 titles).

## GET /v1/ratinglist
This method was first used in system version 23.0.0.

This method returns the following:

| Field | Description |
| --- | --- |
| fv | Format version (always 1) |
| lm | Last modified (timestamp) |
| apps | List of apps |

The apps list seems to be empty as of August 2026.

## GET /v1/apps/&lt;title id&gt;/recommend-versions
This method returns at least the following fields:

| Field | Description |
| --- | --- |
| `recommendVersions` | List of version entries |

Every version entry contains the following fields:

| Field | Description |
| --- | --- |
| `cnmtId` | Cnmt id |
| `cnmtType` | `Application`, `Patch`, `DataPatch` or `AddOnContent` |
| `recommendVersion` | Recommended version |

## POST /v1/apps/search
This method was first used in system version 20.0.0.

This method returns the playable platform list for a specific title version.

The request contains a `keys` field, which contains a list of objects with the following fields:

| Field | Description |
| --- | --- |
| `applicationId` | Title id |
| `releaseVersion` | Title version |

The response contains the following fields:

| Field | Description |
| --- | --- |
| `unfounds` | Missing titles |
| `founds` | Found titles |

The `founds` field contains a list of objects with the following fields:

| Field | Description |
| --- | --- |
| `applicationId` | Title id |
| `releaseVersion` | Title version |
| `platforms` | List of platforms (e.g. `Ounce`) |

Example:

```json
{
    "unfounds": [],
    "founds": [{
        "applicationId": "0400c3f00006e000",
        "releaseVersion": 0,
        "platforms": ["Ounce"]
    }]
}
```