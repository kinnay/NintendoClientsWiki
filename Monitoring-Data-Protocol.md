[Pia](Pia-Overview) > [Protocols](Pia-Protocols) > Monitoring Data Protocol
---

This protocol is used for the P2P monitoring server on the Switch. The messages are wrapped in unencrypted [Pia packets](Pia-Protocol) and are sent to `g<game server id>-%.p.srv.nintendo.net` through UDP port 34343.

If no game server id is specified (e.g. when the game uses [NPLN](NPLN-Servers)), then `g2122d301` is used as a default.

Wii U games send the monitoring data to the NEX server instead, through the [SendReport](Secure-Protocol#8-sendreport) method of the [secure connection protocol](Secure-Protocol).

Up to Pia version 5.23, the monitoring data protocol was called the "feedback protocol".

The following version number is advertised during the [connection request](Station-Protocol):

| Pia version | Version |
| --- | --- |
| 5.19 - 5.45 | 0 |

## Packet Format
Every packet consists of:
* An unencrypted [header](#monitoring-data-header)
* A [compressed and encrypted](#payload-encoding) payload

## Monitoring Data Header
This structure appears at the start of the packet, but also at the start of the decrypted and decompressed payload.

*Up to 5.6:*

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 1 | [Version number](#version-numbers) |
| 0x1 | 1 | [Data type](#data-types) |
| 0x2 | 1 | Flags |
| 0x3 | 1 | Always 0xFF |
| 0x4 | 2 | Payload size |
| 0x6 | 10 | Padding (filled with 0xFF) |

*5.7 and later:*

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 1 | [Version number](#version-numbers) |
| 0x1 | 1 | [Data type](#data-types) |
| 0x2 | 1 | Flags |
| 0x3 | 1 | Unknown |
| 0x4 | 2 | Payload size |
| 0x6 | 8 | AES-GCM nonce (random number) |
| 0xE | 1 | Encryption key id (random number) |
| 0xF | 1 | Always 0xFF |

### Version Numbers
Monitoring was added to Pia in version 3.4.

| Pia version | Monitoring version |
| --- | --- |
| 3.4 | 1 |
| 3.5 | 2 |
| 3.6 | 3 |
| 3.7 | 4 |
| 3.8 | 5 |
| 3.9 | 6 |
| 3.10 | 7 |
| 4.5 | 9 |
| 4.6 | 10 |
| 4.9 | 11 |
| 4.10 | 12 |
| 5.2 - 5.4 | 15 |
| 5.5 | 16 |
| 5.6 | 17 |
| 5.7 - 5.9 | 18 |
| 5.10 - 5.12 | 19 |
| 5.14 | 20 |
| 5.17 - 5.19 | 22 |
| 5.20 | 23 |
| 5.21 - 5.31 | 24 |
| 5.32 - 5.40 | 25 |
| 5.41 | 26 |
| 5.42 - 5.45 | 27 |
| 6.16 | 30 |
| 6.20 - 6.23 | 32 |
| 6.25 | 33 |
| 6.26 | 34 |
| 6.29 | 35 |
| 6.30 | 36 |
| 6.31 | 37 |
| 6.32 - 6.33 | 38 |
| 6.34 | 39 |
| 6.40 - 6.41 | 43 |
| 7.2 | 45 |

### Data Types
The content of the payload depends on the version number and data type in the monitoring data header.

| Data Type | Payload content |
| --- | --- |
| 0 | [Session begin monitoring content](#session-begin-monitoring-content) |
| 1 | [Session end monitoring data](#session-end-monitoring-data) |
| 2 | [Session end monitoring data](#session-end-monitoring-data) |

## Payload Encoding
The payload is first zlib compressed and then encrypted.

*Up to 5.6:*

The payload is encrypted with AES-ECB with the key `901edf193dc5ef3c5290647bff20c385`.

*5.7 and later:*

The payload is encrypted with AES-GCM. The AES-GCM tag is appended to the encrypted payload.

The key is chosen by the lower nybble of the encryption key id in the monitoring data header:

```
 0: c1d494af4a0a956c545d2e41fc1ceb24
 1: caf247fb40aa9655e58c2b02bff89e14
 2: bc6da24db8c7e22d2e3fdd97a2b5e3d2
 3: 3ef3a41d8a2e78518974679562afe5fa
 4: c0a02f90a2642ea6a64b199e01f46a57
 5: 9eb9c98fc889495c7056f2cd8015aac0
 6: 632acbe8c6c77246475b577b6b2d8c76
 7: 8dafd0578b2d3ff285e0292ce08d25a2
 8: cc082ad011d3c38c7b5ed28637f37c1c
 9: 6cd46046c71362116e36cb96c0098912
10: 54598618dc2a24474a9d5e80f783a145
11: f35eaa5cc8ebc1dc42ada6c3f4130556
12: 127d237973e98688548b5dac5eb6cc7b
13: f677ccf32241122aeeece3df23aaa736
14: d7cb0683d251030fc7613b4b2461224b
15: c587a79cbac8a2ddcee27409242a8702
```

The nonce is constructed as follows:

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 8 | Nonce from monitoring data header |
| 0x8 | 4 | Always `5bd085fa` |

## Session Begin Monitoring Content
All fields are initialized to 0xFF.

*Version 18:*

| Type | Description |
| --- | --- |
| [MonitoringDataHeader](#monitoring-data-header) | Monitoring data header |
| Uint32 | Pia version |
| Uint32 | SDK version |
| Uint32 | NEX version |
| Uint8 | Unknown |
| Uint8 | Unknown |
| Uint8 | Platform id (3=Wii U, 4=Switch) |
| Uint8 | Language |
| Uint8 | Unknown |
| Uint32 | Pia heap size |
| Uint32 | Bitmask that describes which [protocols](Pia-Protocols) are created. |
| Uint64 | Unknown |
| Uint8 | Unknown |
| Uint32 | Unknown |
| Uint32 | Unknown |
| Uint8 | Unknown |
| Uint8 | Unknown |
| Uint32 | External client address |
| Uint32 | Local client address |
| Uint8 | NAT mapping |
| Uint8 | NAT filtering |
| Uint8 | NAT port increment |
| Uint8 | NAT mode flags |
| Uint16 | Unknown |
| Uint16 | Time required to resolve address of NAT check server (milliseconds) |
| Uint16 | Unknown |
| Uint32 | Unknown |
| Uint32 | MD5 hash of pid |
| Uint32 | Unknown |
| Uint32 | Game server id |
| Uint8 | [Thread mode](#thread-mode) |
| Uint16 | Unknown |
| Uint32 | Unknown |
| Uint32 | Unknown |
| Uint32 | Unknown |
| Uint32 | Unknown |
| Uint16 | Unknown |
| Uint32 | Unknown |
| Uint16 | Unknown |
| Uint32 | Unknown |
| Uint16 | Relay route rtt max |
| Uint16 | Relay route num max |
| Uint16 | Unknown |
| Uint32 | Unknown |
| Uint8 | Unknown |
| Uint8 | Unknown |
| Uint8 | Unknown |
| Uint32 | Unknown |
| Uint32 | Unknown |
| Uint8 | Unknown |
| Uint32 | Unknown |
| Uint32 | Unknown |
| Uint32 | Unknown |
| Uint32 | Unknown |
| Uint32 | Unknown |
| Uint32 | Unknown |
| Uint32 | Unknown |
| Uint32 | Unknown |
| Uint32 | Unknown |
| Uint32 | Unknown |
| Uint32 | Unknown |
| Uint32 | Unknown |
| Uint32 | Unknown |
| Uint32 | Unknown |
| Uint32 | Unknown |
| Uint8 | Unknown |
| Uint32 | Unknown |
| Uint32 | Unknown |
| Uint32 | Unknown |
| Uint32 | Unknown |
| Uint32 | Unknown |
| Uint32 | Unknown |
| Uint32 | Unknown |
| Uint32 | Unknown |
| Uint16 | Unknown |
| Uint8 | Unknown |
| Uint8 | Unknown |
| Uint32 | Unknown |
| Uint16 | Unknown |
| Uint16 | Unknown |
| Uint16 | Unknown |
| Uint16 | Unknown |
| Uint16 | Unknown |
| Uint16 | Unknown |
| Uint16 | Unknown |
| Uint16 | Unknown |
| Uint8 | Unknown |
| Uint16 | Unknown |
| Uint16 | External client port |
| Uint16 | Local client port |
| Uint8 | Unknown |
| Uint32 | MD5 hash of pid of session host |
| Uint8 | Unknown |
| Uint8 | Unknown |
| Uint8 | Unknown |
| Uint32 | Joint session gathering id |
| Uint32 | Unknown |
| Uint32 | Unknown |
| Uint8 | Unknown |
| Uint8 | Unknown |
| Uint32 | Time required to create or join matchmake session (milliseconds) |
| Uint32 | Unknown |
| Uint32 | Unknown |
| Uint32 | Unknown |
| Uint32 | Unknown |
| Uint32 | Unknown |
| Uint32 | Unknown |
| Uint32 | Unknown |
| Uint16 | Unknown |
| [NexSessionSearchCriteria](#nexsessionsearchcriteria) | Search criteria 1 |
| [NexSessionSearchCriteria](#nexsessionsearchcriteria) | Search criteria 2 |
| Uint8 | Number of session join attempts |
| Uint8 | Unknown |
| Uint8 | Unknown |
| [NexSessionSearchCriteriaExtra](#nexsessionsearchcriteriaextra) | Extra search criteria 1 |
| [NexSessionSearchCriteriaExtra](#nexsessionsearchcriteriaextra) | Extra search criteria 2 |
| Uint8 | Number of NAT traversal failures |
| Uint8 | Number of session join failures because the connection with the host could not be established |
| Uint8 | Number of session join failures because of an error receiving the join response |
| Uint8 | Number of session join failures because the session started host migration before a connection was established with all clients |
| Uint8 | Number of session join failures because the session started host migration before the join was completed |
| Uint8 | Number of session join failures because the join request was denied |
| Uint32 | Unknown |
| Uint32 | Unknown |
| Uint8 | Unknown |
| Uint8 | Unknown |
| Uint8 | Unknown |
| Uint8 | Unknown |
| Uint8 | Unknown |
| Uint8 | Unknown |
| Uint16 | Unknown |
| Uint16 | Unknown |
| Uint32 | Unknown |
| Uint32 | Unknown |
| Uint16 | Unknown |
| Uint16 | Unknown |
| Uint32[75] | Unknown |
| Uint8[60] | Unknown |
| Uint8 | Last [result](#nat-traversal-result) of starting NAT traversal |
| Uint8 | Last [result](#nat-traversal-result) of completing NAT traversal |
| Uint16 | Unknown |
| Uint16 | Unknown |
| Uint16 | Unknown |
| Uint16 | Time required to resolve address of monitoring server (milliseconds) |
| Uint16 | Unknown |
| Uint8[15] | Unknown |
| Uint32 | NAT relay server address |
| Uint16 | NAT relay server port |
| Uint8[67] | Unknown |
| Uint8[150] | Unknown |
| Uint8[150] | Unknown |
| Uint8[32] | Unknown |
| Uint8[150] | Unknown |
| Uint8[176] | Unknown |
| Uint8[300] | Unknown |
| Uint8 | Unknown |
| Uint8 | Unknown |
| Uint8 | Unknown |
| Uint8 | Unknown |
| Uint8 | Unknown |
| Uint8 | Unknown |
| Uint8 | Unknown |
| Uint8 | Unknown |
| Uint32 | Always `PiaM` |

*Version 34:*

| Offset | Size | Module | Description |
| --- | --- | --- | --- |
| 0x0 | 16 | Common | [Header](#monitoring-data-header) |
| 0x10 | 4 | Common | Pia version |
| 0x14 | 4 | Common | Pia SDK version |
| 0x18 | 4 | Common | Game SDK version |
| 0x1C | 4 | Common | NPLN version |
| 0x20 | 4 | Common | Application matchmake version |
| 0x24 | 1 | Common | Build bit |
| 0x25 | 1 | Common | Build type |
| 0x26 | 1 | Common | Platform type |
| 0x27 | 20 | Common | Engine version |
| 0x3B | 32 | Common | Android board |
| 0x5B | 32 | Common | Android model |
| 0x7B | 32 | Common | Android brand |
| 0x9B | 1 | Common | [Country code](#country-code) |
| 0x9C | 4 | Common | [Device location name hash](#device-location-name-hash) |
| 0xA0 | 4 | Common | Pia revision |
| 0xA4 | 4 | Common | Heap size |
| 0xA8 | 1 | Common | Network type |
| 0xA9 | 4 | Common | Average dispatch time |
| 0xAD | 4 | Common | Maximum dispatch time |
| 0xB1 | 4 | Common | Dispatch count |
| 0xB5 | 2 | Common | Monitoring server dns resolution time |
| 0xB7 | 3 | Common | Smart device system version |
| 0xBA | 1 | Common | Reachability |
| 0xBB | 16 | Common | Carrier name |
| 0xCB | 8 | Common | Carrier type |
| 0xD3 | 16 | Common | Local address IPv4 (1) |
| 0xE3 | 16 | Common | Local address IPv4 (2) |
| 0xF3 | 16 | Common | Local address IPv4 (3) |
| 0x103 | 16 | Common | Local address IPv4 (4) |
| 0x113 | 16 | Common | Local address IPv4 (used) |
| 0x123 | 16 | Common | Local address IPv6 (1) |
| 0x133 | 16 | Common | Local address IPv6 (2) |
| 0x143 | 16 | Common | Local address IPv6 (3) |
| 0x153 | 16 | Common | Local address IPv6 (4) |
| 0x163 | 16 | Common | Local address IPv6 (used) |
| 0x173 | 8 | Local | Local communication id |
| 0x17B | 1 | Local | Maximum number of stations |
| 0x17C | 1 | Local | Application communication version |
| 0x17D | 1 | Local | Function enable flags |
| 0x17E | 1 | Local | System communication version |
| 0x17F | 1 | NAT | Is NAT 64 |
| 0x180 | 1 | NAT | NAT mapping |
| 0x181 | 1 | NAT | NAT filtering |
| 0x182 | 2 | NAT | NAT port increment |
| 0x184 | ... | ? | ? |
| 0x384 | 2 | Clone | Number of buffers per station for event clone protocol |
| 0x386 | 4 | Clone | Maximum id for atomic clone protocol |
| 0x38A | ... | ? | ? |
| 0x434 | --- | --- | End |

*Version 43:*

| Offset | Size | Module | Description |
| --- | --- | --- | --- |
| 0x0 | 16 | Common | [Header](#monitoring-data-header) |
| 0x10 | 4 | Common | Pia version |
| 0x14 | 4 | Common | Pia SDK version |
| 0x18 | 4 | Common | Game SDK version |
| 0x1C | 4 | Common | NPLN version |
| 0x20 | 4 | Common | Application matchmake version |
| 0x24 | 1 | Common | Build bit |
| 0x25 | 1 | Common | Build type |
| 0x26 | 1 | Common | Platform type |
| 0x27 | 20 | Common | Engine version |
| 0x3B | 32 | Common | Android board |
| 0x5B | 32 | Common | Android model |
| 0x7B | 32 | Common | Android brand |
| 0x9B | 1 | Common | [Country code](#country-code) |
| 0x9C | 4 | Common | [Device location name hash](#device-location-name-hash) |
| 0xA0 | 4 | Common | Pia revision |
| 0xA4 | 4 | Common | Heap size |
| 0xA8 | 1 | Common | Network type |
| 0xA9 | 4 | Common | Average dispatch time |
| 0xAD | 4 | Common | Maximum dispatch time |
| 0xB1 | 4 | Common | Dispatch count |
| 0xB5 | 2 | Common | Monitoring server dns resolution time |
| 0xB7 | 3 | Common | Smart device system version |
| 0xBA | 1 | Common | Reachability |
| 0xBB | 16 | Common | Carrier name |
| 0xCB | 8 | Common | Carrier type |
| 0xD3 | 16 | Common | Local address IPv4 (1) |
| 0xE3 | 16 | Common | Local address IPv4 (2) |
| 0xF3 | 16 | Common | Local address IPv4 (3) |
| 0x103 | 16 | Common | Local address IPv4 (4) |
| 0x113 | 16 | Common | Local address IPv4 (used) |
| 0x123 | 16 | Common | Local address IPv6 (1) |
| 0x133 | 16 | Common | Local address IPv6 (2) |
| 0x143 | 16 | Common | Local address IPv6 (3) |
| 0x153 | 16 | Common | Local address IPv6 (4) |
| 0x163 | 16 | Common | Local address IPv6 (used) |
| 0x173 | 8 | Local | Local communication id |
| 0x17B | 1 | Local | Maximum number of stations |
| 0x17C | 1 | Local | Application communication version |
| 0x17D | 1 | Local | Function enable flags |
| 0x17E | 1 | Local | System communication version |
| 0x17F | 1 | NAT | Is NAT 64 |
| 0x180 | 1 | NAT | NAT mapping |
| 0x181 | 1 | NAT | NAT filtering |
| 0x182 | 2 | NAT | NAT port increment |
| 0x184 | 1 | NAT | NAT attribute |
| 0x185 | 4 | NAT | Public IP address |
| 0x189 | 4 | NAT | Private IP address |
| 0x18D | 2 | NAT | Public port |
| 0x18F | 2 | NAT | Interface port |
| 0x191 | 2 | NAT | NAT check server DNS resolution time |
| 0x193 | 2 | NAT | NAT property detection time |
| 0x195 | 2 | NAT | NAT port detection time |
| 0x197 | 1 | NAT | NAT property detection count |
| 0x198 | 1 | NAT | NAT TTL |
| 0x199 | 2 | NET | Maximum number of stations |
| 0x19B | 4 | NET | Create network processing time |
| 0x19F | 4 | NET | Connect network processing time |
| 0x1A3 | 4 | NET | Search network processing time |
| 0x1A7 | 4 | NET | Auto connect network processing time |
| 0x1AB | 4 | NET | Destroy network processing time |
| 0x1AF | 4 | NET | Disconnect network processing time |
| 0x1B3 | 8 | NET | Matchmake key |
| 0x1BB | 40 | WAN | NAT traversal results (?) |
| 0x1E3 | 4 | WAN | NAT traversal success time (milliseconds) |
| 0x1E7 | 4 | WAN | Relay server address |
| 0x1EB | 2 | WAN | Relay server port |
| 0x1ED | 1 | WAN | Signaling failure count |
| 0x1EE | 4 | WAN | Game unique id |
| 0x1F2 | 1 | WAN | Unknown |
| 0x1F3 | 96 | WAN | Attribute filtering query |
| 0x253 | 4 | WAN | Join random room server response time |
| 0x257 | 4 | WAN | Join room server response time |
| 0x25B | 4 | WAN | Leave room server response time |
| 0x25F | 4 | WAN | Find room server response time |
| 0x263 | 4 | WAN | Find user server response time |
| 0x267 | 4 | WAN | Search member list size |
| 0x26B | 4 | Izumo | Create search index attribute id |
| 0x26F | 4 | Izumo | Search index attribute id |
| 0x273 | 4 | Transport | Protocol usage flag |
| 0x277 | 4 | Transport | Keep alive interval |
| 0x27B | 2 | Transport | Best RTT in all stations |
| 0x27D | 2 | Transport | Best RTT variable id |
| 0x27F | 4 | Transport | Worst RTT in all stations |
| 0x283 | 2 | Transport | Worst RTT variable id |
| 0x285 | 4 | Transport | Median RTT in all stations |
| 0x289 | 2 | Transport | Maximum number of stations |
| 0x28B | 2 | Transport | Number of send thread buffers per station |
| 0x28D | 2 | Transport | Number of receive thread buffers per station |
| 0x28F | 2 | Transport | Number of unreliable receive buffers per station |
| 0x291 | 2 | Transport | Number of reliable send buffers per station |
| 0x293 | 2 | Transport | Number of reliable receive buffers per station |
| 0x295 | 2 | Transport | Number of broadcast reliable send buffers per station |
| 0x297 | 2 | Transport | Number of broadcast reliable receive buffers per station |
| 0x299 | 2 | Transport | Number of stream broadcast reliable send buffers per station |
| 0x29B | 2 | Transport | Number of stream broadcast reliable receive buffers per station |
| 0x29D | 4 x 18 | ? | ? |
| 0x2E5 | 1 | ? | ? |
| 0x2E6 | 1 | ? | ? |
| 0x2E7 | 1 | ? | ? |
| 0x2E8 | 1 | ? | ? |
| 0x2E9 | 1 | ? | ? |
| 0x2EA | 4 | Session | Join result |
| 0x2EE | 4 | Session | Join error code |
| 0x2F2 | 4 | Session | Join result filename hash |
| 0x2F6 | 4 | Session | Join result line number |
| 0x2FA | 4 | Session | Join processing time |
| 0x2FE | 4 | Session | Join processing dispatch count |
| 0x302 | 4 | Session | Join mesh processing time |
| 0x306 | 4 | Session | Join mesh processing dispatch count |
| 0x30A | 8 | Session | Join session id |
| 0x312 | 1 | Session | Join order |
| 0x313 | 2 | Session | Join variable id |
| 0x315 | 1 | ? | ? |
| 0x316 | 1 | ? | ? |
| 0x317 | 1 | ? | ? |
| 0x318 | 4 | ? | ? |
| 0x31C | 1 | ? | ? |
| 0x31D | 1 | ? | ? |
| 0x31E | 1 | ? | ? |
| 0x31F | 2 x 15 | ? | ? |
| 0x33D | 1 | ? | ? |
| 0x33E | 2 | ? | ? |
| 0x340 | 1 | ? | ? |
| 0x341 | 2 | ? | ? |
| 0x343 | 4 | ? | ? |
| 0x347 | 4 | ? | ? |
| 0x34B | 4 | ? | ? |
| 0x34F | 1 x 6 | ? | ? |
| 0x355 | 2 | Evolution | Evolution version |
| 0x357 | 2 | Evolution | WAN waiting probe response via server timeout |
| 0x359 | 1 | Evolution | WAN waiting probe response via server timeout result |
| 0x35A | 2 | Evolution | WAN waiting probe 1 timeout |
| 0x35C | 1 | Evolution | WAN waiting probe 1 timeout result |
| 0x35D | 2 | Evolution | WAN resolve IPv4 to IPv6 timeout |
| 0x35F | 4 | Evolution | WAN resolve IPv4 to IPv6 time |
| 0x363 | 2 | Evolution | ? |
| 0x365 | 1 | Evolution | ? |
| 0x366 | 2 | Evolution | ? |
| 0x368 | 1 | Evolution | ? |
| 0x369 | 2 | Evolution | ? |
| 0x36B | 1 | Evolution | ? |
| 0x36C | 2 | Evolution | ? |
| 0x36E | 1 | Evolution | ? |
| 0x36F | 1 | Evolution | ? |
| 0x370 | 2 | Evolution | Photon wait event timeout search room |
| 0x372 | 1 | Evolution | Photon wait event timeout search room result |
| 0x373 | 2 | Evolution | Photon wait event timeout create room |
| 0x375 | 1 | Evolution | Photon wait event timeout create room result |
| 0x376 | 2 | Evolution | Photon wait event timeout join room |
| 0x378 | 1 | Evolution | Photon wait event timeout join room result |
| 0x379 | 2 | Evolution | Photon wait event timeout join random room |
| 0x37B | 1 | Evolution | Photon wait event timeout join random room result |
| 0x37C | 2 | Evolution | Photon wait event timeout leave room |
| 0x37E | 1 | Evolution | Photon wait event timeout leave room result |
| 0x37F | 2 | Evolution | Photon wait event timeout leave room action |
| 0x381 | 1 | Evolution | NET wait disconnected timeout result |
| 0x382 | 2 | Evolution | Photon wait event timeout local info |
| 0x384 | 1 | Evolution | Photon wait event timeout local info result |
| 0x385 | 2 | Evolution | Session join request send timeout |
| 0x387 | 1 | Evolution | Session join request send timeout result |
| 0x388 | 1 | Evolution | Session join mesh retry count max |
| 0x389 | 1 | Evolution | Session join mesh retry count max result |
| 0x38A | 4 | Evolution | Session Izumo host migration timeout |
| 0x38E | 2 | Evolution | Session LAN host migration timeout |
| 0x390 | 2 | Evolution | Session local host migration timeout |
| 0x392 | 4 | Evolution | Session NPLN host migration timeout |
| 0x396 | 2 | Evolution | Session Photon host migration timeout |
| 0x398 | 1 | Evolution | Session host migration timeout result |
| 0x399 | 2 | ? | ? |
| 0x39B | 1 | ? | ? |
| 0x39C | --- | --- | End |

### NexSessionSearchCriteria
| Type | Description |
| --- | --- |
| Uint32 | Game mode |
| Uint8 | Min participants num range (min) |
| Uint8 | Min participants num range (max) |
| Uint8 | Max participants num range (min) |
| Uint8 | Max participants num range (max) |
| Uint8 (x6) | Attribute array size |
| Uint32 (x6) | Attribute range min |
| Uint32 (x6) | Attribute range max |
| Uint8 | Session type |
| Uint8 | Flags:<br>1: exclude user password set<br>2: exclude non host pid<br>4: opened only<br>8: vacant only |
| Uint8 | Random session selection method |

### NexSessionSearchCriteriaExtra
| Type | Description |
| --- | --- |
| Uint32 | Rating value |
| Uint32 | Violation rate |
| Uint32 | Disconnection rate |
| Uint8 | Unknown |
| Uint8 | Use geo ip |

### Thread Mode
| Mode | Description |
| --- | --- |
| 0 | ThreadModeUndefined |
| 1 | ThreadModeSafeTransportBuffer |
| 2 | ThreadModeUnsafeTransportBuffer |
| 3 | ThreadModeUnsafeUser |
| 4 | ThreadModeSafeUser |
| 5 | ThreadModeInternal |
| 6 | ThreadModeInternalTransportBuffer |

### NAT Traversal Result
| Value | Description |
| --- | --- |
| 0 | Reliable |
| 1 | Unreliable |
| 2 | Failure or very unreliable |

### Country Code
| ID | Country |
| --- | --- |
| 0 | Japan |
| 1 | US |
| 2 | France |
| 3 | Germany |
| 4 | Italy |
| 5 | Spain |
| 6 | China |
| 7 | Korea |
| 8 | Netherlands |
| 9 | Portugal |
| 10 | Russia |
| 11 | Taiwan |
| 12 | UK |
| 13 | Canada |
| 14 | Latin America |
| 15 | China (simplified) |
| 16 | China (traditional) |
| 17 | Brazil |

### Device Location Name Hash
This is calculated over the time zone name, from `nn::time::GetDeviceLocationName`.

```python
import hashlib
import struct

def hash(timezone):
    hash = hashlib.md5(timezone.encode()).digest()
    parts = struct.unpack(">4I", hash)
    value = parts[0] ^ parts[1] ^ parts[2] ^ parts[3]
    return struct.pack(">I", value)
```

## Session End Monitoring Data
| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 16 | [Monitoring data header](#monitoring-data-header) |
| ... | ... | ... |