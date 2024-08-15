[Switch](Server-List#switch) > System Update Content
---

The atumn server provides title content. Unlike the [atum server](Atum-Server), it does not require an [edge token](DAuth-Server). The atumn server only provides content for system update titles.

* [Overview](#overview)
* [Request headers](#request-headers)
* [Examples](#examples)

## Overview

When the Switch performs a system update, it first downloads the content metadata of the system update title, whose title id was received from the [sun server](Sun-Server). It then downloads the content metadata of all titles that are listed in the content metadata of the system update title. Finally, it downloads the actual content archives of these titles.

The following files are provided by the server:

* `/t/s/<title id>/<title version>`: [NCA] containing [CNMT] (for the system update title)
* `/t/a/<title id>/<title version>`: [NCA] containing [CNMT] (for all other titles)
* `/c/s/<content id>`: [NCA] containing [CNMT] (for the system update title)
* `/c/a/<content id>`: [NCA] containing [CNMT] (for all other titles)
* `/c/c/<content id>`: [NCA] containing actual content

The `/t` and `/c` endpoints serve the same content. The only difference is that the `/t` endpoint returns content by title id and version, while the `/c` endpoint returns content by content id.

The following response headers are important:
* `X-Nintendo-Content-Hash` contains the SHA-256 hash of the whole [NCA].
* `X-Nintendo-Content-ID` contains the content id, which is the same as the first half of the content hash.

When the Switch downloads content metadata, it sends a `HEAD` request to the relevant `/t` endpoint. It then extracts the content id from the response headers, and downloads the actual metadata [NCA] by sending a `GET` request to the relevant `/c` endpoint.

When the Switch queries a `/t` endpoint (with `HEAD`) it includes a `device_id` parameter in the URL.

## Request Headers
| Header | Description |
| --- | --- |
| Host | `atumn.hac.lp1.d4c.nintendo.net` |
| Accept | `*/*` |
| User-Agent | [User agent](#user-agents) |

### User Agents
The user agent looks as follows: `NintendoSDK Firmware/<firmware version>-<revision> (platform:NX; did:<device id>; eid:lp1)`. The firmware version and revision number are obtained from the [system version title](https://switchbrew.org/wiki/System_Version_Title).

Here is an example: `NintendoSDK Firmware/15.0.0-4.0 (platform:NX; did:6265ca40780b1c0d; eid:lp1)`

## Examples
Let's say that the Switch has detected a system update. According to [sun](Sun-Server), the latest system update title id is `0100000000000816` and its title version is 1140851708.

The Switch first obtains its content id with the following request:

```
HEAD /t/s/0100000000000816/1140851708?device_id=6265ca40780b1c0d HTTP/1.1
Host: atumn.hac.lp1.d4c.nintendo.net
Accept: */*
User-Agent: NintendoSDK Firmware/16.0.3-1.0 (platform:NX; did:6265ca40780b1c0d; eid:lp1)
```

```
HTTP/1.1 200 OK
Accept-Ranges: bytes
Content-Length: 5632
Content-Type: application/octet-stream
ETag: "ca10dba3bcec4daf2ea41ca1c67827b9"
Last-Modified: Fri, 06 Oct 2023 02:50:22 GMT
Server: openresty/1.9.7.5
X-Nintendo-Content-Hash: 170ca33980ff8e9cdad31c6add0f38b6b11637c6cf2a4549f49cb2ab9607e8f8
X-Nintendo-Content-ID: 170ca33980ff8e9cdad31c6add0f38b6
Date: Sat, 21 Oct 2023 15:29:17 GMT
x-nintendo-akamai-reference-id: 0.84566168.1697894957.208979b5
Connection: keep-alive
```

It then downloads the metadata [NCA] with the following request:

```
GET /c/s/170ca33980ff8e9cdad31c6add0f38b6 HTTP/1.1
Host: atumn.hac.lp1.d4c.nintendo.net
Accept: */*
User-Agent: NintendoSDK Firmware/16.0.3-1.0 (platform:NX; did:6265ca40780b1c0d; eid:lp1)
```

```
HTTP/1.1 200 OK
Accept-Ranges: bytes
Content-Type: application/octet-stream
ETag: "ca10dba3bcec4daf2ea41ca1c67827b9"
Last-Modified: Fri, 06 Oct 2023 02:50:22 GMT
Server: openresty/1.9.7.5
X-Nintendo-Content-Hash: 170ca33980ff8e9cdad31c6add0f38b6b11637c6cf2a4549f49cb2ab9607e8f8
X-Nintendo-Content-ID: 170ca33980ff8e9cdad31c6add0f38b6
Content-Length: 5632
Date: Sat, 21 Oct 2023 15:29:17 GMT
x-nintendo-akamai-reference-id: 0.84566168.1697894957.20897b86
Connection: keep-alive

<encrypted NCA>
```

After parsing the [CNMT] from the [NCA] that it just obtained, it downloads the metadata [NCAs] of the titles that are listed in that [CNMT].

For example:

```
HEAD /t/a/0100000000000006/1140851648?device_id=6265ca40780b1c0d HTTP/1.1
Host: atumn.hac.lp1.d4c.nintendo.net
Accept: */*
User-Agent: NintendoSDK Firmware/16.0.3-1.0 (platform:NX; did:6265ca40780b1c0d; eid:lp1)
```

```
GET /c/a/aa4c1492ab0ab849fbc1002eb3ecc784 HTTP/1.1
Host: atumn.hac.lp1.d4c.nintendo.net
Accept: */*
User-Agent: NintendoSDK Firmware/16.0.3-1.0 (platform:NX; did:6265ca40780b1c0d; eid:lp1)
```

This is repeated for all other titles as well.

Finally, it downloads the actual content [NCAs] that are listed in the metadata [NCAs] that were downloaded in the previous step:

```
GET /c/c/e3a44d36db9756202bef1dcd3bfb65ef HTTP/1.1
Host: atumn.hac.lp1.d4c.nintendo.net
Accept: */*
User-Agent: NintendoSDK Firmware/16.0.3-1.0 (platform:NX; did:6265ca40780b1c0d; eid:lp1)
```

[CNMT]: https://switchbrew.org/wiki/CNMT
[NCA]: https://switchbrew.org/wiki/NCA
[NCAs]: https://switchbrew.org/wiki/NCA