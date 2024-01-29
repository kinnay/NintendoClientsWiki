[[Server List]] > Eagle (relay servers)
---

Unlike most multiplayer games, a handful of games uses a relay server instead of [Pia](Pia-Overview), which is called eagle. Match making is still done with [NEX](NEX-Overview-(Game-Servers)), but when the session is ready, the server sends a [notification event](#notification-event) to the clients, which contains the url of the eagle server and a token.

* [Notification Event](#notification-event)
* [Server URL](#server-url)
* [Token Format](#token-format)
* [Packet Format](#packet-format)
* [Protocol Description](#protocol-description)

The following games use libeagle:
* [Tetris 99](Eagle-RPC-(Tetris-99))
* [Super Mario Bros. 35](Eagle-RPC-(SMB35))
* [PAC-MAN 99](Eagle-RPC-(PAC-MAN-99))
* F-Zero 99

## Notification Event
When a [matchmake session](Matchmake-Extension-Protocol) is created, the server spawns a container that runs the eagle server. When the eagle server is ready, the NEX server sends a [notification event](Notification-Protocol) to everyone in the matchmake session. The notification event has the following fields set:

| Field | Description |
| --- | --- |
| m_pidSource | 257049437023956657 (Quazal Rendez-Vous) |
| m_uiType | 200000 |
| m_uiParam1 | The gathering id |
| m_mapParam | See table below |

Map param:

| Field | Description |
| --- | --- |
| `url` | The url of the eagle server |
| `token` | Base64 encoded token |

## Server URL
The URL is written as follows: `<scheme>://<host>:<port>/<path>`.

The scheme must be either `kdp` (see https://github.com/skywind3000/kcp), `tcp`, `tcps`, `ws` or `wss`.

The port is optional and defaults to 443 if the connection is secured with TLS (`tcps` or `wss`) or 30000 if the connection is not secured with TLS. The path is only required on WebSocket connections (`ws` or `wss`). If TCP is used (`tcp` or `tcps`) packets are prefixed by a 16-bit big-endian integer that specifies the size of the packet.

The real server always uses the following URL: `wss://<server name>.g.<server env>.e.srv.nintendo.net:443/<game id>/ess-d7d-<server id>`. Sometimes, the suffix `-b` or `-g` is added to the server name.

| Game | Server Name | Game ID |
| --- | --- | --- |
| Tetris 99 | `d7d-arzn` | `EA3nJiq9BKyoxmBjJ2TkfzcRHwQe88FJ` |
| Super Mario Bros. 35 | `d7d-ayam` | `EGrCObHITxTtIa3O1A01uw2WHSEypGYb` |
| PAC-MAN 99 | `d7d-ayqv` | `EGrCObHITxTtIa3O1A01uw2WHSEypGYb` |

Example: `wss://d7d-arzn.g.lp1.e.srv.nintendo.net:443/EA3nJiq9BKyoxmBjJ2TkfzcRHwQe88FJ/ess-d7d-btb4mnggg9q5k2kdqb8g`

## Token Format
The token is a base64-encoded JSON object that contains the following fields:

| Field | Description |
| --- | --- |
| payload | Payload. See below. |
| signature | Base64-encoded signature (32 bytes) |
| version | Always 1 |

The payload has the following fields:

| Field | Description |
| --- | --- |
| expires_at | Timestamp in seconds (string) |
| server_env | Server environment (e.g. `lp1`) |
| server_id | A string of 20 lowercase alphanumeric characters. |
| user_id | Your pid (hex string) |

If the server name has the suffix `-b` or `-g`, the server id is given the suffix `-blue` or `-green` respectively.

## Packet Format
Packets are encoded as a stream of bits. Each packet starts with the following header:

| Bits | Description |
| --- | --- |
| 2 | Relay type |
| 8 | Payload id |
| [N](#library-versions) | Source node id |

The remainder of the packet depends on the relay type and payload id.

| Type | Description |
| --- | --- |
| 0 | No relay. |
| 1 | This packet is relayed to a single node. The header is followed by [N](#library-versions) bits that hold the destination node id. |
| 2 | This packet is relayed to multiple nodes. The header is followed by [M](#library-versions) bits that hold the destination nodes (one bit per node). |

Only RPC packets are relayed to other clients.

The payload comes after header and relay destination, but the bit stream is first aligned to 8 bits before the payload starts.

| Payload ID | Description |
| --- | --- |
| 0 | [Accepted](#accepted) |
| 1 | [Login request](#login-request) |
| 2 | [Login result](#login-result) |
| 3 | [Client ready](#client-ready) |
| 4 | [Ping](#ping) |
| 5 | [Pong](#pong) |
| 6 | [Prof request](#prof-request) |
| 7 | [Prof data](#prof-data) |
| 8 | [Node notice](#node-notice) |
| 9 | [Disconnected](#disconnected) |
| 16 - 255 | [RPC](#rpc) |

### Accepted
The server time is monotonic clock (no timestamp).

| Bits | Description |
| --- | --- |
| 16 | Node id |
| 64 | Server time (in milliseconds) |

### Login Request
If the token does not fit into a single packet, it is split into fragments. The last fragment is terminated with a null byte.

| Bits | Description |
| --- | --- |
| 7 | Login phase (0 or 1) |
| 1 | Last fragment |

Login phase 0:
| Bits | Description |
| --- | --- |
| 8 | Unknown |
| 32 | [Protocol version (P)](#library-versions) |
| 64 | App protocol version |
| 32 | DDL hash |
| 8 | Version string size (max 63 bytes) |
| | Version string |

Login phase 1:
| Bits | Description |
| --- | --- |
| 8 | Token string size |
| | Token string |

### Login Result
The payload contains the user id from the token and a null terminator.

| Bits | Description |
| --- | --- |
| 32 | Error code |
| 8 | Unknown |
| 16 | Payload size |
| | Payload |

### Client Ready
No payload.

### Ping
| Bits | Description |
| --- | --- |
| 64 | Client time (milliseconds) |

### Pong
| Bits | Description |
| --- | --- |
| 64 | Server time (milliseconds) |
| 64 | Client time (milliseconds) |

### Prof Request
No payload.

### Prof Data
| Bits | Description |
| --- | --- |
| 8 | Unknown |
| 32 | Unknown |
| 64 | Unknown |
| 64 | Unknown |
| 64 | Unknown |
| 64 | Unknown |
| 32 | Unknown |

### Node Notice
| Bits | Description |
| --- | --- |
| 8 | Type |
| ... | ... |

| Type | Description |
| --- | --- |
| 0 | Node added |
| 1 | Unknown (version 1.x) |
| 2 | Unknown (version 1.x) |
| 3 | Node removed |
| 4 | All nodes (version 2.x) |

Type 0 - 3:
| Bits | Description |
| --- | --- |
| 16 | Node id |
| 64 | Server time (milliseconds) |

Type 4:

| Bits | Description |
| --- | --- |
| [M](#library-versions) | Active nodes (one bit per node) |
| 64 | Server time (milliseconds) |

### Disconnected
No payload.

### RPC
| Bits | Description |
| --- | --- |
| 64 | Server time (milliseconds) |
| | Payload |

## Protocol Description
After the client has received the notification event from the NEX server, the following happens:
1. The client establishes a connection with the eagle server.
2. The server assigns a node id to the client and sends an [Accepted](#accepted) packet to the client.
3. The client sends a [Login Request](#login-request) packet to the server for login phase 0.
4. The client sends one or more [Login Request](#login-request) packets to the server for login phase 1.
5. The server sends a [Login Result](#login-result) packet to the client.
6. The client sends a [Client Ready](#client-ready) packet to the server.

Version 1.x:

7. The server sends [Node Notice](#node-notice) type 0 to all clients to tell them that a new node is ready.
8. Maybe something with node notice type 1?

Version 2.x:

7. The server sends [Node Notice](#node-notice) type 4 to inform it about the session state.
8. The server sends [Node Notice](#node-notice) type 0 to all other clients to tell them that a new node is ready.

Now, the client and server start exchanging RPC packets. If the client sends an RPC packet to the server, the server simply forwards it to the nodes that are specified in the packet header.

If node is 0 is specified in the packet header, the server also processes the RPC packet itself.

Eagle also provides two special node ids:
* [M]: The packet is relayed to all clients except for the source node.
* [M] + 1: The packet is relayed to all clients including the source node.

## Library Versions
The eagle library was rewritten almost completely between Tetris 99 and Super Mario Bros 35.

| Game | N | M |
| --- | --- | --- |
| Tetris 99 | 9 | 128 |
| Super Mario Bros 35 | 11 | 1024 |
| PAC-MAN 99 | 11 | 1024 |

| Game | Version string | P |
| --- | --- | --- |
| Tetris 99 | release/1.2.14 | 2 |
| Super Mario Bros 35 | 2.0.4 | 3 |
| PAC-MAN 99 | 2.0.4 | 3 |

[M]: #library-versions