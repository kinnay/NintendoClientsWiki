[Pia](Pia-Overview) > Packet Format
---

These packets are usually sent directly from one console to another through UDP, with no server in between. Everything is encoded in big-endian byte order.

All packets consist of an unencrypted [header](#header), which is followed by one or more [messages](#messages), and sometimes an unencrypted [footer](#footer).

## Header
*Up to 5.6:*

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 4 | Magic number: `32 AB 98 64` |
| 0x4 | 1 | Encrypted (1=No 2=Yes) |
| 0x5 | 1 | [Connection id](#connection-id) |
| 0x6 | 2 | [Packet id](#packet-id) |
| 0x8 | 2 | [Source timer](#rtt-calculation) |
| 0xA | 2 | [Destination timer](#rtt-calculation) |

*5.7 - 5.10:*

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 4 | Magic number: `32 AB 98 64` |
| 0x4 | 1 | Encrypted (1=No 2=Yes) |
| 0x5 | 1 | [Connection id](#connection-id) |
| 0x6 | 2 | [Packet id](#packet-id) |
| 0x8 | 2 | [Source timer](#rtt-calculation) |
| 0xA | 2 | [Destination timer](#rtt-calculation) |
| 0xC | 8 | [AES-GCM nonce](#encryption) |
| 0x14 | 16 | [AES-GCM authentication tag](#encryption) |

*5.11 - 5.21:*

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 4 | Magic number: `32 AB 98 64` |
| 0x4 | 1 | This byte consists of two parts:<br>`0x80`: Encryption enabled<br>`0x7F`: [Version number](#version) (3 or 4) |
| 0x5 | 1 | [Connection id](#connection-id) |
| 0x6 | 2 | [Packet id](#packet-id) |
| 0x8 | 8 | [AES-GCM nonce](#encryption) |
| 0x10 | 16 | [AES-GCM authentication tag](#encryption) |

*5.23 - 5.26:*

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 4 | Magic number: `32 AB 98 64` |
| 0x4 | 1 | This byte consists of two parts:<br>`0x80`: Encryption enabled<br>`0x7F`: [Version number](#version) (5) |
| 0x5 | 1 | [Connection id](#connection-id) |
| 0x6 | 2 | [Packet id](#packet-id) |
| 0x8 | 8 | [AES-GCM nonce](#encryption) |
| 0x10 | 8 | [AES-GCM authentication tag](#encryption) (first 8 bytes) |

*5.27 - 5.45:*

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 4 | Magic number: `32 AB 98 64` |
| 0x4 | 1 | This byte consists of two parts:<br>`0x80`: Encryption enabled<br>`0x7F`: [Version number](#version) (9) |
| 0x5 | 4 | Destination [variable id](Pia-Types#variable-id) |
| 0x9 | 4 | Source [variable id](Pia-Types#variable-id) |
| 0xD | 2 | [Packet id](#packet-id) |
| 0xF | 1 | [Footer size](#footer) |
| 0x10 | 8 | [AES-GCM nonce](#encryption) |
| 0x18 | 8 | [AES-GCM authentication tag](#encryption) (first 8 bytes) |

*6.16 - 6.30:*

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 4 | Magic number: `32 AB 98 64` |
| 0x4 | 1 | This byte consists of two parts:<br>`0x80`: Encryption enabled<br>`0x7F`: [Version number](#version) (11, 12 or 13) |
| 0x5 | 2 | Destination [variable id](Pia-Types#variable-id) |
| 0x7 | 2 | Source [variable id](Pia-Types#variable-id) |
| 0x9 | 2 | [Packet id](#packet-id) |
| 0xB | 1 | [Footer size](#footer) |
| 0xC | 8 | [AES-GCM nonce](#encryption) |
| 0x14 | 8 | [AES-GCM authentication tag](#encryption) (first 8 bytes) |

*6.32 - 6.41:*

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 4 | Magic number: `32 AB 98 64` |
| 0x4 | 1 | This byte consists of two parts:<br>`0x80`: Encryption enabled<br>`0x7F`: [Version number](#version) (11, 12 or 13) |
| 0x5 | 1 | Padding size |
| 0x6 | 2 | Destination [variable id](Pia-Types#variable-id) |
| 0x8 | 2 | Source [variable id](Pia-Types#variable-id) |
| 0xA | 2 | [Packet id](#packet-id) |
| 0xC | 1 | [Footer size](#footer) |
| 0xD | 8 | [AES-GCM nonce](#encryption) |
| 0x15 | 8 | [AES-GCM authentication tag](#encryption) (first 8 bytes) |

### Version
| Pia Version | Header version |
| --- | --- |
| 5.11 - 5.17 | 3 |
| 5.18 - 5.21 | 4 |
| 5.23 - 5.26 | 5 |
| 5.27 - 5.45 | 9 |
| 6.16 - 6.23 | 11 |
| 6.25 - 6.26 | 12 |
| 6.29 - 6.30 | 13 |
| 6.32 - 6.34 | 15 |
| 6.40 - 6.41 | 16 |

### Maximum Packet Size
| Pia Version | Maximum Size |
| --- | --- |
| Up to 6.33 | 1472 |
| 6.34 - 6.40 | 1452 |

### Connection ID
During connection establishment, both consoles generate a random number between 2 and 255. This is the connection id. If packets are sent to a specific address, rather than station index, the connection id is set to 0.

### Packet ID
If the connection id is 0, the packet id is also 0. If the connection id is not 0, the packet id is an incrementing number starting at 1.

When the packet id rolls over, the value 0 is skipped. This means that the next id after packet id 65535 is 1.

### RTT Calculation
The RTT timers contain the number of milliseconds since the start of the session. Every client has its own session timer (they are independent from each other). Aside from its own timer, every client also keeps track of the timers of all other clients. When A sends a packet to B the destination timer is what A believes the session timer of B to be. Hopefully, an example will make this clear:

Let's say the timer of A is at 234 when A sends a packet to B. It takes 2 milliseconds until the packet arrives at B. B receives 234 from A even though the timer of A is now at 236. 10 milliseconds later, B sends a packet to A with 244 (234 + 10) in the destination timer field. Again, it takes 2 milliseconds until the packet arrives at A. At this point, the timer of A is at 248, but it receives 244 in the destination timer field, so it knows that it takes 4 milliseconds for a packet to travel back and forth between A and B.

![](https://www.dropbox.com/s/4fbobmcugbbokr3/rtt.png?raw=1)

If no packet has been received from the target yet, the destination timer is set to 0. To avoid collisions, the destination timer is set to `0xFFFF` if it would otherwise be 0.

### Footer
The footer is only used in LDN mode when a packet is sent to more than one console. It contains the [variable id](Pia-Types#variable-id) of all receiving consoles as 16-bit integers.

## Messages
This part of the packet may be [encrypted](#encryption). A packet may contain more than one message  (the number of messages is determined from the size of packet).

All messages are padded such that their size is a multiple of 4 bytes.

*Up to 5.4:*

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 1 | [Message flags](#message-flags) |
| 0x1 | 1 | [Source station index](#station-index) |
| 0x2 | 2 | Payload size |
| 0x4 | 4 | [Destination](#destination) |
| 0x8 | 4 | [Source constant id](Pia-Types#constant-id) |
| 0xC | 2 | [Protocol type](Pia-Protocols) |
| 0xE | 2 | Protocol port (protocol-specific) |
| 0x10 | 4 | Reserved (always 0) |
| 0x14 | | Payload (protocol-specific) |
| | | Padding |

*5.6 - 5.10:*

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 1 | [Message flags](#message-flags) |
| 0x1 | 2 | Payload size |
| 0x3 | 8 | [Destination](#destination) |
| 0xB | 8 | [Source constant id](Pia-Types#constant-id) |
| 0x13 | 1 | [Protocol type](Pia-Protocols) |
| 0x14 | 1 | Protocol port (protocol-specific) |
| 0x15 | 3 | Padding (always 0) |
| 0x18 | | Payload (protocol-specific) |
| | | Padding |

*5.11 - 5.12:*

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 1 | [Message flags](#message-flags) |
| 0x1 | 1 | Version (always 1) |
| 0x2 | 2 | Payload size |
| 0x4 | 1 | [Protocol type](Pia-Protocols) |
| 0x5 | 1 | Protocol port (protocol-specific) |
| 0x6 | 8 | [Destination](#destination) |
| 0xE | 8 | [Source constant id](Pia-Types#constant-id) |
| 0x16 | | Payload (protocol-specific) |
| | | Padding |

*5.14 - 5.17:*

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 1 | [Message flags](#message-flags) |
| 0x1 | 1 | Version (always 2) |
| 0x2 | 2 | Payload size |
| 0x4 | 1 | [Protocol type](Pia-Protocols) |
| 0x5 | 3 | Protocol port (protocol-specific) |
| 0x8 | 8 | [Destination](#destination) |
| 0x10 | 8 | [Source constant id](Pia-Types#constant-id) |
| 0x18 | | Payload (protocol-specific) |
| | | Padding |

*5.18 - 5.26:*

Fields that are not present are copied from the previous message.

| Type | Description |
| --- | --- |
| Uint8 | Flags indicating which of the following fields are present. |
| Uint8 | [Message flags](#message-flags). *Only present if `flags & 1`.* |
| Uint16 | Payload size. *Only present if `flags & 2`.* |
| Uint8 | [Protocol type](Pia-Protocols). *Only present if `flags & 4`.* |
| Uint24 | Protocol port (protocol-specific). *Only present if `flags & 4`.* |
| Uint64 | [Destination](#destination). *Only present if `flags & 8`.* |
| Uint64 | [Source constant id](Pia-Types#constant-id). *Only present if `flags & 16`.* |
| Bytes | Payload (protocol-specific) |
| | Padding |

*5.27 - 6.30:*

Fields that are not present are copied from the previous message.

| Type | Description |
| --- | --- |
| Uint8 | Flags indicating which of the following fields are present. |
| Uint8 | [Message flags](#message-flags). *Only present if `flags & 1`.* |
| Uint16 | Payload size. *Only present if `flags & 2`.* |
| Uint8 | [Protocol type](Pia-Protocols). *Only present if `flags & 4`.* |
| Uint24 | Protocol port (protocol-specific). *Only present if `flags & 4`.* |
| Uint64 | [Destination](#destination). *Only present if `flags & 8`.* |
| Bytes | Payload (protocol-specific) |
| | Padding |

*6.32 - 6.40:*

Fields that are not present are copied from the previous message.

| Type | Description |
| --- | --- |
| Uint8 | Flags indicating which of the following fields are present. |
| Uint8 | [Message flags](#message-flags). *Only present if `flags & 1`.* |
| Uint16 | Payload size. *Only present if `flags & 2`.* |
| Uint8 | [Protocol type](Pia-Protocols). *Only present if `flags & 4`.* |
| Uint8 | Protocol port (protocol-specific). *Only present if `flags & 8`.* |
| Uint8 | Protocol-specific. *Only present if `flags & 16`.* |
| Bytes | Payload (protocol-specific) |
| | Padding |

### Message flags
*Up to 5.4:*

| Mask | Description |
| --- | --- |
| 0x1 | Destination is [constant id](Pia-Types#constant-id) |
| 0x2 | The message needs be relayed to another console |
| 0x4 | The message was relayed through another console |
| 0x8 | The message may not be bundled with other messages in a single packet |

*5.6 - 5.12:*

The meaning of the destination bit was flipped.

| Mask | Description |
| --- | --- |
| 0x1 | Destination is bitmap |
| 0x2 | The message needs be relayed to another console |
| 0x4 | The message was relayed through another console |
| 0x8 | The message may not be bundled with other messages in a single packet |

*5.14 - 5.26:*

A number of protocols now support compression.

| Mask | Description |
| --- | --- |
| 0x1 | Destination is bitmap |
| 0x2 | The message needs be relayed to another console |
| 0x4 | The message was relayed through another console |
| 0x8 | The message may not be bundled with other messages in a single packet |
| 0x10 | The message payload is zlib compressed (not all protocols support this) |

*5.27 - 5.45:*

| Mask | Description |
| --- | --- |
| 0x1 | Destination is bitmap |
| 0x2 | The message needs to be relayed to a single console |
| 0x4 | The message needs to be relayed to multiple consoles |
| 0x8 | The message was relayed through another console |
| 0x10 | The message may not be bundled with other messages in a single packet |
| 0x20 | The message payload is zlib compressed (not all protocols support this) |

*6.16 - 6.30:*

| Mask | Description |
| --- | --- |
| 0x1 | Skip source [variable id](Pia-Types#variable-id) check |
| 0x2 | The message needs to be relayed to a single console |
| 0x4 | The message needs to be relayed to multiple consoles |
| 0x8 | The message was relayed through another console |
| 0x10 | The message may not be bundled with other messages in a single packet |
| 0x20 | The message payload is zlib compressed (not all protocols support this) |
| 0x40 | Unknown |
| 0x80 | Unknown |

### Station index
Every console in a mesh gets its own station index. The following station index values are special:

* **253:** Invalid. Used for consoles that haven't joined a mesh yet.
* **254:** Represents the host of the mesh.
* **255:** Used for broadcast messages.

### Destination
The content of this field depends on the [message flags](#message-flags). It is either a [constant id](Pia-Types#constant-id) or a bitmap. In the latter case, each bit represents one destination console (the bit number of a console is its station index: `1 << station_index`). For messages that are broadcast to all consoles, the destination field is set to 0.

If a message needs to be relayed, the destination id must always be a bitmap.

## Encryption
Packets are encrypted and signed with the [session key](#session-key). The messages are padded with 0xFF before encryption such that their combined size is a multiple of 16 bytes.

*Up to 5.6:*

If encryption is enabled, the messages are encrypted with AES-ECB. The HMAC-MD5 of the whole packet (both header and encrypted payload) is appended to the packet.

*5.7 - 6.30:*

If encryption is enabled, the messages are encrypted with AES-GCM. The authentication tag is stored in the [header](#header). No other signature is appended to the packet.

### Nonce

The AES-GCM nonce depends on the network type and is generated as follows:

**NEX** *(up to 5.26):*

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 1 | [Connection id](#header) |
| 0x1 | 3 | `gathering_id & 0xFFFFFF` |
| 0x4 | 8 | Nonce from [header](#header) |

**NEX** *(5.27 - 5.45):*

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 1 | [Source variable id](#header) `& 0xFF` |
| 0x1 | 3 | `gathering_id & 0xFFFFFF` |
| 0x4 | 8 | Nonce from [header](#header) |

**LDN** *(up to 5.26):*

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 3 | First 3 bytes of CRC32 hash |
| 0x3 | 1 | [Connection id](#header) |
| 0x4 | 8 | Nonce from [header](#header) |

**LDN** *(5.27 - 5.45):*

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 3 | First 3 bytes of CRC32 hash |
| 0x3 | 1 | [Source variable id](#header) `& 0xFF` |
| 0x4 | 8 | Nonce from [header](#header) |

The CRC32 hash is calculated over the following data:

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 4 | Session id (see [application data](LDN-Application-Data-(Pia))) |
| 0x4 | 6 | MAC address of source |

The session id is stored in little-endian byte order.

**LDN** *(6.16 - 6.30):*

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 4 | XOR of network id and IP address of source |
| 0x4 | 8 | Nonce from [header](#header) |

**LAN** *(up to 5.26):*

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 4 | IP address of source |
| 0x4 | 1 | [Connection id](#header) |
| 0x5 | 7 | Last 7 bytes of nonce from [header](#header) |

**LAN** *(5.27 - 5.45):*

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 4 | IP address of source |
| 0x4 | 1 | [Source variable id](#header) `& 0xFF` |
| 0x5 | 7 | Last 7 bytes of nonce from [header](#header) |

**LAN** *(6.16 - 6.30):*

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 4 | IP address of source (CRC-32 hash if IPv6 is used) |
| 0x4 | 8 | Nonce from [header](#header) |

**NPLN** *(6.16 - 6.30):*

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 4 | Network id |
| 0x4 | 8 | Nonce from [header](#header) |

### Session Key
The session key is used for packet encryption and signature calculation.

**NEX** *(Up to 5.45):*

The session key is obtained from the game server during [matchmaking](Match-Making-Types#matchmakesession-structure).

**LDN** *(Up to 5.6):*

Encryption is not supported in LDN mode.

**LDN** *(5.7):*

The session key is [specified by the game](Pia-Game-Keys).

**LDN** *(5.9 - 5.45):*

A [random number generator](SEAD-RNG) is constructed using the [session param](LDN-Application-Data-(Pia)) as seed. Four random 32-bit integers are generated and appended to each other in little-endian byte order. The session key is generated by encrypting this buffer with AES, using a [game-specific key](Pia-Game-Keys).

**LDN** *(6.16 - 6.30):*

The session key is generated by encrypting the network [SSID](LDN-Protocol) with AES, using a [game-specific-key](Pia-Game-Keys).

**LAN** *(Up to 6.30):*

First, the last byte of the [session key param](LAN-Protocol#session-key-param) is incremented by 1. The session key is generated by taking the first 16 bytes of the HMAC-SHA256 of the incremented session key param, using a [game-specific key](Pia-Game-Keys).
