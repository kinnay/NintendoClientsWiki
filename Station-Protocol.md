[Pia](Pia-Overview) > [Protocols](Pia-Protocols) > Station Protocol
---

The difference between the reliable and unreliable protocol is that the reliable protocol wraps messages in a [reliable sliding window](Pia-Types#reliableslidingwindow). The reliable protocol is not used by Pia however, and support for it was removed in version *5.6*.

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
| 5.27 - 5.43 | 2 |

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

*5.27 - 5.43:*

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
| Uint32 | Session id |
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

| Type | Description |
| --- | --- |
| Uint8 | Message type (2) |
| Uint8 | [Connection result](#connection-result) (accepted) |
| Uint8 | [Version number](#version-numbers) |
| Uint8 | [Platform id](#platform-id) |
| Uint8 | [Fragment id](#fragment-id) |
| Uint8 (32) | Identification token (ascii) |
| Uint32 | Session id |
| Uint8 | Number of players |
| Uint8 | Number of participants. This is either 1 or equal to the number of players, depending on whether each player should count as a participant in the session. |
| Uint8 | Number of player infos |
| [PlayerInfo](#player-info) (2 or 4) | Player info, may be [fragmented](#fragment-id). |
| Uint32 | Ack id |

*5.7 - 5.18:*

| Type | Description |
| --- | --- |
| Uint8 | Message type (2) |
| Uint8 | [Connection result](#connection-result) (accepted) |
| Uint8 | [Version number](#version-numbers) |
| Uint8 | [Platform id](#platform-id) |
| Uint8 | [Fragment id](#fragment-id) |
| Uint64 | Target [constant id] |
| Uint32 | Target [variable id] |
| Uint8 (32) | Identification token (ascii) |
| Uint32 | Session id |
| Uint8 | Number of players |
| Uint8 | Number of participants. This is either 1 or equal to the number of players, depending on whether each player should count as a participant in the session. |
| Uint8 | Number of player infos |
| [PlayerInfo](#player-info) (2 or 4) | Player info, may be [fragmented](#fragment-id). |
| Uint32 | Ack id |

*5.27 - 5.43:*

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
| Uint32 | Session id |
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

*5.27 - 5.43:*

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
| 2 | Incompatible version |

## Fragment ID
In some Pia versions, the connection response may be fragmented, depending on the maximum payload size.

| ID | Description |
| --- | --- |
| 0 | The player info array contains all players. |
| 1 | The player info array contains the first two players. |
| 2 | The player info array contains the last two players. |

## Protocol List
The protocol list contains the following for every available protocol.

| Type | Description |
| --- | --- |
| Uint8 | Protocol id |
| Uint8 | Protocol version |

## Player Info
*3.3 - 3.10:*
| Type | Description |
| --- | --- |
| Uint16 (16) | Player name (UTF-16) |
| Uint8 | Player name length (number of characters) |
| Uint8 | Language |
| Uint16 | Padding |

*4.5 - 4.10:*
| Type | Description |
| --- | --- |
| Uint16 (16) | Player name (UTF-16) |
| Uint8 | Player name length (number of characters) |
| Uint8 | Language |
| Uint32 | Unknown |
| Uint16 | Padding |

*5.2 - 5.6:*
| Type | Description |
| --- | --- |
| Bytes (80) | Player name |
| Uint8 | Player name encoding (1=UTF-8, 2=UTF-16) |
| Bytes (40) | Account name |
| Uint8 | Account name encoding (1=UTF-8, 2=UTF-16) |
| Uint8 | Language |
| Bytes (64) | Play history registration key |

*5.7 - 5.19:*
| Type | Description |
| --- | --- |
| Bytes (80) | Player name |
| Uint8 | Player name encoding (1=UTF-8, 2=UTF-16) |
| Bytes (40) | Account name |
| Uint8 | Account name encoding (1=UTF-8, 2=UTF-16) |
| Uint8 | Language |
| Bytes (64) | Play history registration key |
| Uint64 | Principal id |

*5.27 - 5.43:*

| Type | Description |
| --- | --- |
| Uint8 | Player name encoding (1=UTF-8, 2=UTF-16) |
| Bytes (80) | Player name |
| Uint8 | Account name encoding (1=UTF-8, 2=UTF-16) |
| Bytes (40) | Account name |
| Uint8 | Language |
| Bytes (64) | Play history registration key |
| Uint64 | Principal id |

[Constant id]: Pia-Types#constant-id
[Variable id]: Pia-Types#variable-id

[StationConnectionInfo]: Pia-Types#stationconnectioninfo
[StationLocation]: Pia-Types#stationlocation
[IdentificationInfo]: Pia-Types#identificationinfo