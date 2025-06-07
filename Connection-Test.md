[Switch](Server-List#switch) > Connection Test
---

Nintendo provides the following connection test servers for the Nintendo Switch:
* http://ctest.cdn.nintendo.net
* http://ctest-dl-lp1.cdn.nintendo.net
* http://ctest-ul-lp1.cdn.nintendo.net
* https://api.hac.lp1.ctest.srv.nintendo.net

On the Switch 2, the following servers are used instead:
* https://ctest.p01.ctest.srv.nintendo.net
* https://ctest-dl.p01.lp1.ctest.srv.nintendo.net
* https://ctest-ul.p01.lp1.ctest.srv.nintendo.net
* https://api.p01.lp1.ctest.srv.nintendo.net

The first server is used to check if the internet connection is working when you connect to a wifi network. The next two are used to measure your download and upload speed.

The last server was introduced in system version 18.0.0 and is a replacement for `/v1/time` of the [[AAuth server]].

## Connection Test
### Switch 1
Request:

```
GET / HTTP/1.1
Host: ctest.cdn.nintendo.net
User-Agent: NX NIFM/00
Accept: */*
Connection: keep-alive
```

Response:

```
HTTP/1.1 200 OK
Content-Length: 2
Expires: Mon, 05 Apr 2021 14:52:05 GMT
Cache-Control: max-age=0, no-cache, no-store
Pragma: no-cache
Date: Mon, 05 Apr 2021 14:52:05 GMT
Connection: keep-alive
X-Organization: Nintendo
Content-Type: text/plain

ok
```

### Switch 2
Request:
```
GET / HTTP/1.1
Host: ctest.p01.ctest.srv.nintendo.net
User-Agent: libcurl (nnNifm; bf4812d9-d89b-4804-b53a-d08e0bed634f; SDK 20.5.4.0; Add-on 20.5.4.0)
Accept: */*
```

Response:

```
HTTP/1.1 200 OK
Content-Length: 2
Expires: Sat, 07 Jun 2025 09:18:57 GMT
Cache-Control: max-age=0, no-cache, no-store
Pragma: no-cache
Date: Sat, 07 Jun 2025 09:18:57 GMT
Connection: keep-alive
X-Organization: Nintendo
Content-Type: text/plain

ok
```

## Download Speed
Request:

```
GET /30m HTTP/1.0
Host: ctest-dl-lp1.cdn.nintendo.net
User-Agent: Nintendo NX
Accept: */*
Connection: keep-alive
```

Response:

```
HTTP/1.1 200 OK
Accept-Ranges: bytes
Content-Type: text/plain
ETag: "30a54a61adf95decd3bda4761c65c5c8:1492755189"
Last-Modified: Fri, 21 Apr 2017 06:13:09 GMT
Server: AkamaiNetStorage
Content-Length: 31457280
Expires: Wed, 23 Nov 2022 11:42:53 GMT
Cache-Control: max-age=0, no-cache, no-store
Pragma: no-cache
Date: Wed, 23 Nov 2022 11:42:53 GMT
Connection: keep-alive

<random bytes>
```

## Upload Speed
Request:

```
POST /1m HTTP/1.0
Host: ctest-ul-lp1.cdn.nintendo.net
User-Agent: Nintendo NX
Accept: */*
Content-Length: 1048576
Content-Type: application/x-www-form-urlencoded
Connection: keep-alive
```

Response:

```
HTTP/1.0 200 OK
Accept-Ranges: bytes
Content-Length: 0
Server: AkamaiNetStorage
Pragma: no-cache
Cache-Control: no-cache, no-store
Expires: Wed, 23 Nov 2022 11:43:01 GMT
Date: Wed, 23 Nov 2022 11:43:01 GMT
Connection: keep-alive
```

## API
The server provides two endpoints:
* `/v1/ip`
* `/v1/time`

## Errors
If the user agent does not start with `NX NIFM/` (during connection test) or `Nintendo` (for the other servers) the server sends the following response instead:

```
HTTP/1.1 403 Forbidden
Server: AkamaiGHost
Mime-Version: 1.0
Content-Type: text/html
Content-Length: 275
Expires: Mon, 05 Apr 2021 14:53:52 GMT
Date: Mon, 05 Apr 2021 14:53:52 GMT
Connection: keep-alive

<HTML><HEAD>
<TITLE>Access Denied</TITLE>
</HEAD><BODY>
<H1>Access Denied</H1>
 
You don't have permission to access "http&#58;&#47;&#47;ctest&#46;cdn&#46;nintendo&#46;net&#47;" on this server.<P>
Reference&#32;&#35;18&#46;3faf3554&#46;1617634432&#46;da3d018
</BODY>
</HTML>
```