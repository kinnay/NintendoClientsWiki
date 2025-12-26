[Pia](Pia-Overview) > [Protocols](Pia-Protocols) > Monitoring Data Protocol
---

This protocol is used for the P2P monitoring server on the Switch. The messages are wrapped in unencrypted [Pia packets](Pia-Protocol) and are sent to `g<game server id>-%.p.srv.nintendo.net` through UDP port 34343.

If no game server id is specified (e.g. when the game uses [NPLN](NPLN-Servers)), then `g2122d301` is used as a default.

Wii U games send the monitoring data to the NEX server instead, through the [SendReport](Secure-Protocol#8-sendreport) method of the [secure connection protocol](Secure-Protocol).

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
| 6.40 | 43 |

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

*Version 43:*

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 16 | [Header](#monitoring-data-header) |
| 0x10 | 4 | Pia version |
| 0x14 | 4 | Pia SDK version |
| 0x18 | 4 | Game SDK version |
| 0x1C | 4 | NPLN version |
| 0x20 | 4 | Unknown |
| 0x24 | 1 x 120 | Unknown |
| 0x9C | 4 | Unknown |
| 0xA0 | 4 | Unknown |
| 0xA4 | 4 | Unknown |
| 0xA8 | 1 | Unknown |
| 0xA9 | 4 | Unknown |
| 0xAD | 4 | Unknown |
| 0xB1 | 4 | Unknown |
| 0xB5 | 2 | Unknown |
| 0xB7 | 1 x 188 | Unknown |
| 0x173 | 8 | Unknown |
| 0x17B | 1 x 7 | Unknown |
| 0x182 | 2 | Unknown |
| 0x184 | 1 | Unknown |
| 0x185 | 4 | Unknown |
| 0x189 | 4 | Unknown |
| 0x18D | 2 | Unknown |
| 0x18F | 2 | Unknown |
| 0x191 | 2 | Unknown |
| 0x193 | 2 | Unknown |
| 0x195 | 2 | Unknown |
| 0x197 | 1 | Unknown |
| 0x198 | 1 | Unknown |
| 0x199 | 2 | Unknown |
| 0x19B | 4 | Unknown |
| 0x19F | 4 | Unknown |
| 0x1A3 | 4 | Unknown |
| 0x1A7 | 4 | Unknown |
| 0x1AB | 4 | Unknown |
| 0x1AF | 4 | Unknown |
| 0x1B3 | 8 | Unknown |
| 0x1BB | 1 x 15 | Unknown |
| 0x1CA | 2 x 12 | Unknown |
| 0x1E2 | 1 | Unknown |
| 0x1E3 | 4 | Unknown |
| 0x1E7 | 4 | Unknown |
| 0x1EB | 2 | Unknown |
| 0x1ED | 1 | Unknown |
| 0x1EE | 4 | Unknown |
| 0x1F2 | 1 | Unknown |
| 0x1F3 | 96 | Unknown |
| 0x253 | 4 x 10 | Unknown |
| 0x27B | 2 | Unknown |
| 0x27D | 2 | Unknown |
| 0x27F | 4 | Unknown |
| 0x283 | 2 | Unknown |
| 0x285 | 4 | Unknown |
| 0x289 | 2 x 10 | Unknown |
| 0x29D | 4 x 18 | Unknown |
| 0x2E5 | 1 | Unknown |
| 0x2E6 | 1 | Unknown |
| 0x2E7 | 1 | Unknown |
| 0x2E8 | 1 | Unknown |
| 0x2E9 | 1 | Unknown |
| 0x2EA | 4 x 8 | Unknown |
| 0x30A | 8 | Unknown |
| 0x312 | 1 | Unknown |
| 0x313 | 2 | Unknown |
| 0x315 | 1 | Unknown |
| 0x316 | 1 | Unknown |
| 0x317 | 1 | Unknown |
| 0x318 | 4 | Unknown |
| 0x31C | 1 | Unknown |
| 0x31D | 1 | Unknown |
| 0x31E | 1 | Unknown |
| 0x31F | 2 x 15 | Unknown |
| 0x33D | 1 | Unknown |
| 0x33E | 2 | Unknown |
| 0x340 | 1 | Unknown |
| 0x341 | 2 | Unknown |
| 0x343 | 4 | Unknown |
| 0x347 | 4 | Unknown |
| 0x34B | 4 | Unknown |
| 0x34F | 1 x 6 | Unknown |
| 0x355 | 2 | Unknown |
| 0x357 | 2 | Unknown |
| 0x359 | 1 | Unknown |
| 0x35A | 2 | Unknown |
| 0x35C | 1 | Unknown |
| 0x35D | 2 | Unknown |
| 0x35F | 4 | Unknown |
| 0x363 | 2 | Unknown |
| 0x365 | 1 | Unknown |
| 0x366 | 2 | Unknown |
| 0x368 | 1 | Unknown |
| 0x369 | 2 | Unknown |
| 0x36B | 1 | Unknown |
| 0x36C | 2 | Unknown |
| 0x36E | 1 | Unknown |
| 0x36F | 1 | Unknown |
| 0x370 | 2 | Unknown |
| 0x372 | 1 | Unknown |
| 0x373 | 2 | Unknown |
| 0x375 | 1 | Unknown |
| 0x376 | 2 | Unknown |
| 0x378 | 1 | Unknown |
| 0x379 | 2 | Unknown |
| 0x37B | 1 | Unknown |
| 0x37C | 2 | Unknown |
| 0x37E | 1 | Unknown |
| 0x37F | 2 | Unknown |
| 0x381 | 1 | Unknown |
| 0x382 | 2 | Unknown |
| 0x384 | 1 | Unknown |
| 0x385 | 2 | Unknown |
| 0x387 | 1 | Unknown |
| 0x388 | 1 | Unknown |
| 0x389 | 1 | Unknown |
| 0x38A | 4 | Unknown |
| 0x38E | 2 | Unknown |
| 0x390 | 2 | Unknown |
| 0x392 | 4 | Unknown |
| 0x396 | 2 | Unknown |
| 0x398 | 1 | Unknown |
| 0x399 | 2 | Unknown |
| 0x39B | 1 | Unknown }
| 0x39C | --- | End |

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

## Session End Monitoring Data
| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 16 | [Monitoring data header](#monitoring-data-header) |
| ... | ... | ... |