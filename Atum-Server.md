[Switch](Server-List#switch) > Game Content
---

The atum server provides title content. It always requires an [edge token](DAuth-Server).

* [Overview](#overview)
* [Request headers](#request-headers)

## Overview
The following files are provided by the server:

* `/c1/a/d/<id>`
* `/c1/a/d/<id>/<id>`
* `/c1/r/t/<id>`
* `/c1/t/a/<id>/<id>`
* `/c1/<id>/c/a/<id>`
* `/c1/<id>/c/c/<id>`
* `/c2/<id>/c/a/<id>`
* `/c2/<id>/c/c/<id>`

## Request Headers
| Header | Description |
| --- | --- |
| Host | `atumn.hac.lp1.d4c.nintendo.net` |
| Accept | `*/*` |
| User-Agent | [User agent](#user-agents) |
| X-Nintendo-DenebEdgeToken | [Edge token](DAuth-Server) |

### User Agents
The user agent looks as follows: `NintendoSDK Firmware/<firmware version>-<revision> (platform:NX; did:<device id>; eid:lp1)`. The firmware version and revision number are obtained from the [system version title](https://switchbrew.org/wiki/System_Version_Title).

Here is an example: `NintendoSDK Firmware/15.0.0-4.0 (platform:NX; did:6265ca40780b1c0d; eid:lp1)`

[CNMT]: https://switchbrew.org/wiki/CNMT
[NCA]: https://switchbrew.org/wiki/NCA
[NCAs]: https://switchbrew.org/wiki/NCA