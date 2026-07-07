[Pia](Pia-Overview) > LAN Protocol
---

This page describes the protocol that's used to find nearby consoles in LAN mode. In this mode, UDP broadcast packets are used to discover other consoles. LAN mode is not the default mode for local multiplayer and not all games support it. It can usually be enabled by pressing L + R + Left Stick in one of the menus.

Every packet starts with a single byte that indicates its type.

The maximum size of browse request and reply packets is 1364 bytes, although in practice they are always smaller.

## Packet types
| Value | Description |
| --- | --- |
| 0 | [Browse request](#0-browse-request) |
| 1 | [Browse reply](#1-browse-reply) |
| 3 | [Host request](#3-host-request) |
| 4 | [Host message](#4-host-message) |
| 5 | [Session request](#5-session-request) |
| 6 | [Session message](#6-session-message) |
| 7 | [Keep alive message](#7-keep-alive-message) |

## (0) Browse Request
### Transport Method
The browse request is not encapsulated in a [Pia packet](Pia-Protocol).

*Up to 5.45:*

The packet is broadcasted through UDP port 30000.

*6.16 - 7.2:*

The packet is broadcasted through UDP port 35000.

### Packet Format
*Up to 5.6:*

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 1 | Packet type (0) |
| 0x1 | 4 | Size of search criteria (0x23A) |
| 0x5 | 0x23A | [LanSessionSearchCriteria](#lansessionsearchcriteria) |

*5.7 - 5.45:*

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 1 | Packet type (0) |
| 0x1 | 4 | Size of search criteria (0x23A) |
| 0x5 | 0x23A | [LanSessionSearchCriteria](#lansessionsearchcriteria) |
| 0x23F | 0x12A | [Crypto challenge](#crypto-challenge) |

*6.16 - 6.30:*

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 1 | Packet type (0) |
| 0x1 | 4 | Size of search network setting |
| 0x2 | | [LanSearchNetworkSetting](#lansearchnetworksetting) |
| | 0x12A | [Crypto challenge](#crypto-challenge) |

*7.2:*

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 1 | Packet type (0) |
| 0x1 | 4 | Size of search network setting (0x20) |
| 0x2 | 0x20 | [LanSearchNetworkSetting](#lansearchnetworksetting) (encrypted) |
| 0x32 | 0x13B | [Crypto challenge](#crypto-challenge) |

### LanSessionSearchCriteria
*Up to 5.45:*

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 4 | Minimum number of participants ([range](#range)) |
| 0x4 | 4 | Maximum number of participants ([range](#range)) |
| 0x8 | 1 | Opened only |
| 0x9 | 1 | Vacant only |
| 0xA | 4 | Result range offset |
| 0xE | 4 | Result range size |
| 0x12 | 4 | Game mode |
| 0x16 | 4 | Session type |
| 0x1A | 0x50 * 6 | [Attribute lists](#attribute-list) |
| 0x1FA | 1 * 6 | Number of attributes |
| 0x200 | 4 * 6 | Attribute range min |
| 0x218 | 4 * 6 | Attribute range max |
| 0x230 | 1 * 6 | Is attribute range used |
| 0x236 | 4 | [Search flags](#search-flags) |

#### Search flags
These flags indicate which fields are compared against the active session to determine if there is a match.

| Mask | Description |
| --- | --- |
| 0x1 | Minimum number of participants |
| 0x2 | Maximum number of participants |
| 0x4 | Opened only |
| 0x8 | Vacant only |
| 0x10 | Game mode |
| 0x20 | Session type |
| 0x40 | First attribute list |
| ... | ... |
| 0x800 | Last attribute list |

#### Range
| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 2 | Maximum |
| 0x2 | 2 | Minimum |

#### Attribute list
Each attribute list may contain up to 20 attributes. Every attribute is stored as a 4-byte integer.

### LanSearchNetworkSetting
*6.16 - 6.20:*

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 8 | Matchmake key |
| 0x8 | 2 | Maximum number of stations (upper bound) |
| 0xA | 2 | Maximum number of stations (lower bound) |
| 0xC | 2 | [Search flags](#search-flags-1) |

*6.23 - 6.30:*

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 8 | Matchmake key |
| 0x8 | 2 | Maximum number of stations (upper bound) |
| 0xA | 2 | Maximum number of stations (lower bound) |
| 0xC | 2 | [Search flags](#search-flags-1) |
| 0xE | 8 | Title id |

#### Search Flags
These flags indicate which fields are compared against the active session to determine if there is a match.

*6.16 - 6.26:*

| Mask | Description |
| --- | --- |
| 0x1 | Matchmake key |
| 0x2 | Maximum number of stations |
| 0x4 | Opened only |
| 0x8 | Vacant only |

*6.29 - 6.30:*

| Mask | Description |
| --- | --- |
| 0x1 | Ignored |
| 0x2 | Matchmake key |
| 0x4 | Maximum number of stations |
| 0x8 | Opened only |
| 0x10 | Vacant only |

## (1) Browse reply
This packet is sent to the source of the [browse request](#browse-request). It is not encapsulated in a [Pia packet](Pia-Protocol). The browse reply is transmitted three times, presumably to increase the chance that it arrives at the destination console.

*Up to 5.6:*

| Type | Description |
| --- | --- |
| Uint8 | Packet type (1) |
| Uint32 | Size of session info |
| [LanSessionInfo](#lansessioninfo) | Session info |

*5.7 - 5.45:*

| Type | Description |
| --- | --- |
| Uint8 | Packet type (1) |
| Uint32 | Size of session info |
| [LanSessionInfo](#lansessioninfo) | Session info |
| Bytes | [Crypto challenge reply](#crypto-challenge) |

*6.29 - 6.30:*

| Type | Description |
| --- | --- |
| Uint8 | Packet type (1) |
| Uint32 | Size of network property |
| [LanNetworkProperty](#lannetworkproperty) | Network property |
| Bytes | [Crypto challenge reply](#crypto-challenge) |

### LanSessionInfo
*Up to 5.2:*

| Type | Description |
| --- | --- |
| Uint32 | Game mode |
| Uint32 | [Network id] |
| Uint32 (x6) | Attributes |
| Uint16 | Current number of participants |
| Uint16 | Minimum number of participants |
| Uint16 | Maximum number of participants |
| Uint32 | Session type |
| Bytes (0x180) | Application data |
| Uint32 | Application data size |
| Bool | Is opened |
| [StationLocation] | Host address |
| [LanStationInfo](#lanstationinfo) (x16) | Station info of every player in the room |

*5.3 - 5.6:*

The [system communication version](#system-communication-version) and application communication version fields were added. The session type field now occupies 2 bytes instead of 4.

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 4 | Game mode |
| 0x4 | 4 | [Network id] |
| 0x8 | 4 * 6 | Attributes |
| 0x20 | 2 | Current number of participants |
| 0x22 | 2 | Minimum number of participants |
| 0x24 | 2 | Maximum number of participants |
| 0x26 | 1 | [System communication version](#system-communication-version) |
| 0x27 | 1 | Application communication version |
| 0x28 | 2 | Session type |
| 0x2A | 384 | Application data |
| 0x1AA | 4 | Application data size |
| 0x1AE | 1 | Is opened |
| 0x1AF | 35 | Host address ([StationLocation]) |
| 0x1D2 | 50 * 16 | [LanStationInfo](#lanstationinfo) for up to 16 players |

*5.7 - 5.9:*

The [session key param](#session-key-param) field was added, due to encryption being introduced to PiaLan.

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 4 | Game mode |
| 0x4 | 4 | [Network id] |
| 0x8 | 4 * 6 | Attributes |
| 0x20 | 2 | Current number of participants |
| 0x22 | 2 | Minimum number of participants |
| 0x24 | 2 | Maximum number of participants |
| 0x26 | 1 | [System communication version](#system-communication-version) |
| 0x27 | 1 | Application communication version |
| 0x28 | 2 | Session type |
| 0x2A | 384 | Application data |
| 0x1AA | 4 | Application data size |
| 0x1AE | 1 | Is opened |
| 0x1AF | 35 | Host address ([StationLocation]) |
| 0x1D2 | 50 * 16 | [LanStationInfo](#lanstationinfo) for up to 16 players |
| 0x4F2 | 32 | [Session key param](#session-key-param) |

*5.10 - 5.45:*

The [StationLocation] type was removed. The host address now consists of a [StationAddress] and separate fields for its [constant id], [variable id] and [service variable id].

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 4 | Game mode |
| 0x4 | 4 | [Network id] |
| 0x8 | 4 * 6 | Attributes |
| 0x20 | 2 | Current number of participants |
| 0x22 | 2 | Minimum number of participants |
| 0x24 | 2 | Maximum number of participants |
| 0x26 | 1 | [System communication version](#system-communication-version) |
| 0x27 | 1 | Application communication version |
| 0x28 | 2 | Session type |
| 0x2A | 384 | Application data |
| 0x1AA | 4 | Application data size |
| 0x1AE | 1 | Is opened |
| 0x1AF | 18 | Host address ([StationAddress](Pia-Types#stationaddress)) |
| 0x1C1 | 8 | Host [constant id] |
| 0x1C9 | 4 | Host [variable id] |
| 0x1CD | 4 | Host [service variable id] |
| 0x1D1 | 50 * 16 | [LanStationInfo](#lanstationinfo) for up to 16 players |
| 0x4F1 | 32 | [Session key param](#session-key-param) |

#### LanStationInfo
If there are less than 16 stations in the room, the remaining entries of this structure are filled with null bytes.

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 1 | Role (1=host, 2=player) |
| 0x1 | 1 | Username encoding type (1=UTF-8, 2=UTF-16) |
| 0x2 | 40 | Username |
| 0x2A | 8 | [Constant id] |

### LanNetworkProperty
*6.29 - 6.30:*

The structure was redesigned from scratch.

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 8 | [Network id] |
| 0x8 | 0x200 | [Property data](#property-data) and padding |
| 0x208 | 4 | Property data size |
| 0x20C | 8 | Matchmake key |
| 0x214 | 2 | Current number of stations |
| 0x216 | 2 | Maximum number of stations |
| 0x218 | 1 | Is opened |
| 0x219 | 1 | Has player number limit |
| 0x21A | 1 | Current number of players |
| 0x21B | 0x12 | Host address ([StationAddress]) |

#### Property Data
If the application data consumes less than 0x184 bytes, this is reflected in the property data size field in the [LanNetworkProperty](#lannetworkproperty) structure.

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 0x7C | [System property data](#system-property-data) |
| 0x7C | Up to 0x184 | Application data |

#### System Property Data
| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 2 | System property data size (0x7C) |
| 0x2 | 1 | [System communication version](#system-communication-version) |
| 0x3 | 2 | Application communication version |
| 0x5 | 16 | User password |
| 0x15 | 1 | Has player number limit |
| 0x16 | 1 | Current number of players |
| 0x17 | 4 | Host player name size |
| 0x1B | 1 | Host player name encoding (1=utf8, 2=utf16) |
| 0x1C | 64 | Host player name and padding |
| 0x5C | 32 | [Session key param](#session-key-param) |

### System Communication Version
| Version | Pia Version |
| --- | --- |
| 0 | 5.3 |
| 2 | 5.6 |
| 3 | 5.7 |
| 4 | 5.8 |
| 5 | 5.9 |
| 6 | 5.10 |
| 7 | 5.11 - 5.18 |
| 8 | 5.19 - 5.45 |
| 10 | 6.16 - 6.30 |
| 22 | 6.41 |

## (3) Host Request
This packet is sent through UDP broadcast ports 49152 - 49155 and is encapsulated in a [Pia message](Pia-Protocol). The message payload contains the following data and is encrypted with the session key:

*Up to 5.45:*

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 1 | Message type (3) |
| 0x1 | 11 | Padding (always 0) |
| 0xC | 4 | [Network id] |

## (4) Host Message
This message is encapsulated in a [Pia message](Pia-Protocol) and is encrypted with the session key.

*Up to 5.9:*

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 1 | Message type (4) |
| 0x1 | 11 | Padding (always 0) |
| 0xC | 4 | [Network id] |
| 0x10 | | [StationConnectionInfo](Pia-Types#stationconnectioninfo) for host |

*5.10 - 5.45:*

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 1 | Message type (4) |
| 0x1 | 11 | Padding (always 0) |
| 0xC | 4 | [Network id] |
| 0x10 | | [StationLocation](Pia-Types#stationlocation) for host |

## (5) Session Request
This packet is sent through UDP broadcast ports 49152 - 49155 and is encapsulated in a [Pia message](Pia-Protocol). The message payload contains the following data and is encrypted with the session key:

*Up to 5.45:*

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 1 | Message type (5) |
| 0x1 | 11 | Padding (always 0) |
| 0xC | 4 | [Network id] |

## (6) Session Message
This message is encapsulated in a [Pia message](Pia-Protocol) and is encrypted with the session key. The goal of this message is to transmit a [LanSessionInfo](#lansessioninfo) structure. Depending on the size of the [LanSessionInfo](#lansessioninfo), this message may be split into multiple fragments. Each fragment contains up to 800 bytes of data.

Whenever the session is updated, a session message is sent through UDP broadcast port 49152 - 49155. A session message is also sent to a specific station when the station requests an update with a [session request](#5-session-request).

*Up to 5.45:*

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 1 | Message type (6) |
| 0x1 | 11 | Padding (always 0) |
| 0xC | 4 | This is a random value that must be the same in all fragments that belong to the same session message. This is used to distinguish different session replies. |
| 0x10 | 2 | Session message id. This is an incrementing number that should be the same in all fragments that belong to the same session message. |
| 0x12 | 1 | Fragment index |
| 0x13 | 1 | Number of fragments |
| 0x14 | 4 | Fragment size |
| 0x18 | | Fragment data |

## (7) Keep Alive Message
This packet is sent through UDP port 49152 and is encapsulated in a [Pia message](Pia-Protocol). This message is sent once every two seconds, even if the console is not participating in a session. If the console is participating in a session, the message payload is encrypted with the session key. Otherwise, the payload is not encrypted. It is unclear what purpose of the keep alive message is, as it is ignored by the receiver. In Pia version 5.28 and later, the keep alive message is sent to localhost (`127.0.0.1`). In earlier versions, it is sent to the broadcast IP address.

The message payload contains the following data:

*Up to 5.45:*

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 1 | Message type (7) |
| 0x1 | 11 | Padding (always 0) |

## Crypto Challenge
In Pia version 5.7 and later, the [browse request](#0-browse-request) contains a cryptographic challenge that must be correctly answered in the [browse reply](#1-browse-reply). Both the challenge and the response have the following format.

The challenge key and challenge data are randomized for every packet that is transmitted.

*5.7 - 6.33:*

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 1 | [Version](#version) |
| 0x1 | 1 | Crypto enabled (0 or 1) |
| 0x2 | 8 | Incrementing counter used for nonce |
| 0xA | 16 | Challenge key (random bytes) |
| 0x1A | 16 | Authentication tag for AES-GCM |
| 0x2A | 256 or 16 | Challenge or response, encrypted with AES-GCM |

*6.40 - 6.41:*

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 1 | [Version](#version) |
| 0x1 | 1 | Crypto enabled (0 or 1) |
| 0x2 | 1 | Sequence id |
| 0x3 | 8 | Incrementing counter used for nonce |
| 0xB | 16 | Challenge key (random bytes) |
| 0x1B | 16 | Authentication tag for AES-GCM |
| 0x2B | 256 or 16 | Challenge or response, encrypted with AES-GCM |

*7.2:*

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 1 | [Version](#version) |
| 0x1 | 1 | Crypto enabled (0 or 1) |
| 0x2 | 1 | Sequence id |
| 0x3 | 8 | Incrementing counter used for nonce |
| 0xB | 304 | Unknown |

The sequence id in a browse request is incremented on every transmitted request. The sequence id in a browse reply must be equal to the sequence id in the browse request.

### Encryption
The content of the challenge/response when crypto is enabled is described below. If crypto is disabled the authentication tag and challenge/response data are filled with random bytes.

The nonce for the AES-GCM algorithm is generated as follows:

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 4 | Broadcast address (<code>local_address &vert; ~subnet_mask</code>) |
| 0x4 | 8 | Nonce counter |

### Version
| Version | Pia version |
| --- | --- |
| 1 | 5.7 - 5.10 |
| 2 | 5.11 - 5.45 |
| 3 | 6.16 - 6.33 |
| 4 | 6.40 - 6.41 |
| 5 | 7.2 |

### Challenge
The challenge consists of 256 random bytes. The key for encrypting the challenge is generated by AES-encrypting the challenge key with a [game-specific key](Pia-Game-Keys).

### Response
The response contains the first 16 bytes of the HMAC-SHA256 of the decrypted challenge with a [game-specific key](Pia-Game-Keys). The key for encrypting the response is the first 16 bytes of the HMAC-SHA256 of the [session key param](#session-key-param) with the [game-specific key](Pia-Game-Keys):

### Session Key Param
The session key param are used to derive the [challenge response key](#response).

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 16 | [Challenge key](#crypto-challenge) in browse response |
| 0x10 | 16 | [Challenge key received](#crypto-challenge) in browse request |

When the host receives a valid browse request for the first time, it saves the session key param in the [LanSessionInfo](#lansessioninfo) or [LanNetworkProperty](#lannetworkproperty) structure. This is used to derive the [session key](Pia-Protocol#session-key).

[StationLocation]: Pia-Types#stationlocation
[StationAddress]: Pia-Types#stationaddress

[constant id]: Pia-Types#constant-id
[variable id]: Pia-Types#variable-id
[service variable id]: Pia-Types#service-variable-id
[network id]: Pia-Types#network-id