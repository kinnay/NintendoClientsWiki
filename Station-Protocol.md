[Pia](Pia-Overview) > [Protocols](Pia-Protocols) > Station Protocol
---

The difference between the reliable and unreliable protocol is that the reliable protocol wraps messages in a [reliable sliding window](Pia-Types#reliableslidingwindow). The reliable protocol is not used by Pia however, and support for it was removed in version *5.6*.

In Pia 6.x, the station protocol and [[mesh protocol]] were merged into the [session protocol](Session-Protocol-(new)).

| Port | Description |
| --- | --- |
| 0 | Unreliable |
| 1 | Reliable |

The first byte of each packet indicates the message type.

| Type | Description |
| --- | --- |
| 1 | [Connection request](#connection-request) |
| 2 | [Connection response](#connection-response) |
| 3 | [Disconnection request](#disconnection-request) |
| 4 | [Disconnection response](#disconnection-response) |
| 5 | [Ack](#ack) |
| 6 | Relay connection request |
| 7 | Relay connection response |

Messages that need to be acknowledged are retransmitted every 500 milliseconds until they are acknowledged.

### Version numbers

| Pia Version | Version |
| --- | --- |
| 3.3 - 3.6 | 2 |
| 3.7 - 3.10 | 3 |
| 4.5 - 4.10 | 5 |
| 5.2 - 5.6 | 7 |
| 5.7 - 5.9 | 8 |
| 5.10 - 5.18 | 9 |

In version 5.19, the `StationProtocol` was renamed to `MeshStationProtocol` and version numbers start at 0 again:

| Pia Version | Version |
| --- | --- |
| 5.19 - 5.23 | 0 |
| 5.24 - 5.26 | 1 |
| 5.27 - 5.45 | 2 |

## Connection Request
In versions where applicable, the inverse connection id must be the connection id that was previously received from the other station.

*3.3 - 4.10:*

| Type | Description |
| --- | --- |
| Uint8 | Message type  (1) |
| Uint8 | Connection id |
| Uint8 | [Version number](#version-numbers) |
| Uint8 | Is inverse connection request |
| [StationConnectionInfo] | Station connection info |
| Uint32 | Ack id |

*5.2 - 5.6:*

| Type | Description |
| --- | --- |
| Uint8 | Message type  (1) |
| Uint8 | Connection id |
| Uint8 | [Version number](#version-numbers) |
| Uint8 | Is inverse connection request |
| Uint64 | Target [constant id] |
| [StationConnectionInfo] | Station connection info |
| Uint32 | Ack id |

*5.7 - 5.9:*

| Type | Description |
| --- | --- |
| Uint8 | Message type  (1) |
| Uint8 | Connection id |
| Uint8 | [Version number](#version-numbers) |
| Uint8 | Is inverse connection request |
| Uint64 | Target [constant id] |
| Uint32 | Target [variable id]
| Uint8 | Inverse connection id |
| [StationConnectionInfo] | Station connection info |
| Uint32 | Ack id |

*5.10 - 5.18:*

| Type | Description |
| --- | --- |
| Uint8 | Message type  (1) |
| Uint8 | Connection id |
| Uint8 | [Version number](#version-numbers) |
| Uint8 | Is inverse connection request |
| Uint64 | Target [constant id] |
| Uint32 | Target [variable id]
| Uint8 | Inverse connection id |
| [StationLocation] | Station location |
| Uint32 | Ack id |

*5.19 - 5.26:*

| Type | Description |
| --- | --- |
| Uint8 | Message type  (1) |
| Uint8 | Number of available protocols (N) |
| Uint8 (N*2) | [Protocol list](#protocol-list) |
| Uint8 | Connection id |
| Uint8 | Is inverse connection request |
| Uint64 | Target [constant id] |
| Uint32 | Target [variable id]
| Uint8 | Inverse connection id |
| [StationLocation] | Station location |
| Uint32 | Ack id |

*5.27 - 5.45:*

| Type | Description |
| --- | --- |
| Uint8 | Message type (1) |
| Uint8 | [Connection result](#connection-result) (always 0) |
| Uint8 | [Platform id](#platform-id) |
| Uint64 | Target [constant id] |
| Uint32 | Target [variable id] |
| Uint8 | Number of available protocols (N) |
| Uint8 (N*2) | [Protocol list](#protocol-list) |
| Uint16 | Size of station location |
| [StationLocation] | Station location |
| Uint8 (32) | Identification token (ascii) |
| Uint32 | [Network id] |
| Uint8 | Number of players |
| Uint8 | Number of participants. This is either 1 or equal to the number of players, depending on whether each player should count as a participant in the session. |
| Uint8 | Number of player infos (P) |
| [PlayerInfo](#player-info) (P) | Player info |
| Uint32 | Ack id |

## Connection Response
A connection response can either [accept](#accepted) or [deny](#denying) the connection request. This is indicated by the [connection result](#connection-result).

### Accepted

*3.3 - 4.10:*

| Type | Description |
| --- | --- |
| Uint8 | Message type (2) |
| Uint8 | [Connection result](#connection-result) (accepted) |
| Uint8 | [Version number](#version-numbers) |
| Uint8 | [Platform id](#platform-id) |
| Uint8 (32) | Identification token (ascii) |
| [PlayerInfo](#player-info) | Player info |
| Uint32 | Ack id |

*5.2 - 5.6:*

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 1 | Message type (2) |
| 0x1 | 1 | [Connection result](#connection-result) (accepted) |
| 0x2 | 1 | [Version number](#version-numbers) |
| 0x3 | 1 | [Platform id](#platform-id) |
| 0x4 | 1 | [Fragment id](#fragment-id) |
| 0x5 | 32 | Identification token (ascii) |
| 0x25 | 4 | [Network id] |
| 0x29 | 1 | Number of players |
| 0x2A | 1 | Number of participants. This is either 1 or equal to the number of players, depending on whether each player should count as a participant in the session. |
| 0x2B | 1 | Number of player infos |
| 0x2C | | [Player info](#player-info), contains 2 or 4 entries, depending on [fragmentation](#fragment-id). |
| | 4 | Ack id |

*5.7 - 5.18:*

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 1 | Message type (2) |
| 0x1 | 1 | [Connection result](#connection-result) (accepted) |
| 0x2 | 1 | [Version number](#version-numbers) |
| 0x3 | 1 | [Platform id](#platform-id) |
| 0x4 | 1 | [Fragment id](#fragment-id) |
| 0x5 | 8 | Target [constant id] |
| 0xD | 4 | Target [variable id] |
| 0x11 | 32 | Identification token (ascii) |
| 0x31 | 4 | [Network id] |
| 0x35 | 1 | Number of players |
| 0x36 | 1 | Number of participants. This is either 1 or equal to the number of players, depending on whether each player should count as a participant in the session. |
| 0x37 | 1 | Number of player infos |
| 0x38 | | [Player info](#player-info), contains 2 or 4 entries, depending on [fragmentation](#fragment-id). |
| | 4 | Ack id |

*5.19:*

**Note:** due to a bug in Nintendo's code, the last byte of the last player info entry is dropped. The packet therefore contains one less byte than expected.

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 1 | Message type (2) |
| 0x1 | 1 | [Connection result](#connection-result) (accepted) |
| 0x2 | 1 | Station protocol id (always `0x14`) |
| 0x3 | 1 | Station protocol [version number](#version-numbers) |
| 0x4 | 1 | [Platform id](#platform-id) |
| 0x5 | 1 | [Fragment id](#fragment-id) |
| 0x6 | 8 | Target [constant id] |
| 0xE | 4 | Target [variable id] |
| 0x12 | 32 | Identification token (ascii) |
| 0x32 | 4 | [Network id] |
| 0x36 | 1 | Number of players |
| 0x37 | 1 | Number of participants. This is either 1 or equal to the number of players, depending on whether each player should count as a participant in the session. |
| 0x38 | 1 | Number of player infos |
| 0x39 | | [Player info](#player-info), contains 2 or 4 entries, depending on [fragmentation](#fragment-id). The last byte is discarded. |
| | 4 | Ack id |

*5.27 - 5.45:*

| Type | Description |
| --- | --- |
| Uint8 | Message type (2) |
| Uint8 | [Connection result](#connection-result) (accepted) |
| Uint8 | [Platform id](#platform-id) |
| Uint64 | Target [constant id] |
| Uint32 | Target [variable id] |
| Uint8 | Number of available protocols (N) |
| Uint8 (N*2) | [Protocol list](#protocol-list) |
| Uint16 | Size of station location |
| [StationLocation] | Station location |
| Uint8 (32) | Identification token (ascii) |
| Uint32 | [Network id] |
| Uint8 | Number of players |
| Uint8 | Number of participants. This is either 1 or equal to the number of players, depending on whether each player should count as a participant in the session. |
| Uint8 | Number of player infos |
| [PlayerInfo](#player-info) (2 or 4) | Player info |
| Uint32 | Ack id |

### Denying
*3.3 - 5.6:*

| Type | Description |
| --- | --- |
| Uint8 | Message type (2) |
| Uint8 | [Connection result](#connection-result) |
| Uint8 | [Version number](#version-numbers) |
| Uint8 | Always 0 |

*5.7 - 5.18:*

| Type | Description |
| --- | --- |
| Uint8 | Message type (2) |
| Uint8 | [Connection result](#connection-result) |
| Uint8 | [Version number](#version-numbers) |
| Uint8 | Always 0 |
| Uint8 | Always 0 |
| Uint64 | [Constant id] |
| Uint32 | [Variable id] |

*5.19 - 5.23:*

| Type | Description |
| --- | --- |
| Uint8 | Message type (2) |
| Uint8 | [Connection result](#connection-result) |
| Uint8 | Protocol id that has unexpected protocol version |
| Uint8 | Expected protocol version |
| Uint16 | Always 0 |
| Uint64 | [Constant id] |
| Uint32 | [Variable id] |

*5.24 - 5.26:*

| Type | Description |
| --- | --- |
| Uint8 | Message type (2) |
| Uint8 | [Connection result](#connection-result) |
| Uint8 | Protocol id that has unexpected protocol version |
| Uint8 | Expected protocol version |
| Uint16 | Always 0 |
| Uint64 | [Constant id] |
| Uint32 | [Variable id] |
| Uint8 | Connection id |

*5.27 - 5.45:*

| Type | Description |
| --- | --- |
| Uint8 | Message type (2) |
| Uint8 | [Connection result](#connection-result) |
| Uint8 | Always 0 |
| Uint64 | [Constant id] |
| Uint32 | [Variable id] |

## Disconnection request
| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 1 | Message type |

## Disconnection response
| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 1 | Message type |

## Ack
| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 1 | Message type |
| 0x1 | 3 | Padding |
| 0x4 | 4 | Ack id |

## Platform ID
| ID | Platform |
| --- | --- |
| 3 | Wii U |
| 4 | Switch |

## Connection Result
| Value | Description |
| --- | --- |
| 0 | Accepted |
| 1 | Connection denied |
| 2 | Version is too low |
| 3 | Version is too high |

## Fragment ID
In some Pia versions, the connection response may be fragmented, depending on the maximum payload size.

| ID | Description |
| --- | --- |
| 0 | The player info array contains all players. |
| 1 | The player info array contains the first two players. |
| 2 | The player info array contains the last two players. |

## Protocol List
The protocol list contains the following for every available protocol.

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 1 | Protocol id |
| 0x1 | 1 | Protocol version |

## Player Info
*3.3 - 3.10:*
| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 32 | Player name (UTF-16) |
| 0x20 | 1 | Player name length (number of characters) |
| 0x21 | 1 | Language |
| 0x22 | 2 | Padding |

*4.5 - 4.10:*
| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 32 | Player name (UTF-16) |
| 0x20 | 1 | Player name length (number of characters) |
| 0x21 | 1 | Language |
| 0x22 | 4 | Gathering id |
| 0x26 | 2 | Padding |

*5.2 - 5.6:*
| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 80 | Player name |
| 0x50 | 1 | Player name encoding (1=UTF-8, 2=UTF-16) |
| 0x51 | 40 | Account name |
| 0x79 | 1 | Account name encoding (1=UTF-8, 2=UTF-16) |
| 0x7A | 1 | Language |
| 0x7B | 64 | Play history registration key |

*5.7 - 5.26:*

The principal id was added to the struct.

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 80 | Player name |
| 0x50 | 1 | Player name encoding (1=UTF-8, 2=UTF-16) |
| 0x51 | 40 | Account name |
| 0x79 | 1 | Account name encoding (1=UTF-8, 2=UTF-16) |
| 0x7A | 1 | Language |
| 0x7B | 64 | Play history registration key |
| 0xBB | 8 | Principal id |

*5.27 - 5.45:*

The order of string and encoding was swapped.

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 1 | Player name encoding (1=UTF-8, 2=UTF-16) |
| 0x1 | 80 | Player name |
| 0x51 | 1 | Account name encoding (1=UTF-8, 2=UTF-16) |
| 0x52 | 40 | Account name |
| 0x7A | 1 | Language |
| 0x7B | 64 | Play history registration key |
| 0xBB | 8 | Principal id |

[Constant id]: Pia-Types#constant-id
[Variable id]: Pia-Types#variable-id
[Network id]: Pia-Types#network-id

[StationConnectionInfo]: Pia-Types#stationconnectioninfo
[StationLocation]: Pia-Types#stationlocation
[IdentificationInfo]: Pia-Types#identificationinfo