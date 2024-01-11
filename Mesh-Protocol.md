[[Pia Protocols]] > Mesh Protocol
---

| Protocol Port | Description |
| --- | --- |
| 0 | Unreliable |
| 1 | Reliable |

| Message Type | Description |
| --- | --- |
| 0x01 | [Join request](#join-request) |
| 0x02 | [Join response](#join-response-success) |
| 0x04 | [Leave request](#leave-request) |
| 0x08 | [Leave response](#leave-response) |
| 0x10 | [Destroy mesh](#destroy-request) |
| 0x11 | [Destroy response](#destroy-response) |
| 0x20 | [Update mesh](#update-mesh) |
| 0x21 | Kickout notice |
| 0x22 | Dummy message |
| 0x23 | Dummy ack |
| 0x24 | Connection failure notice |
| 0x40 | Greeting |
| 0x41 | Migration finish |
| 0x42 | Greeting response |
| 0x44 | Migration start |
| 0x48 | Migration response |
| 0x49 | Multi migration start |
| 0x4A | Multi migration rank decision |
| 0x80 | Connection report |
| 0x81 | Relay route directions |

The following version numbers are advertised during the [connection request](Station-Protocol):

| Pia version | Version |
| --- | --- |
| 5.19 - 5.20 | 0 |
| 5.21 - 5.27 | 1 |
| 5.28 - 5.29 | 2 |
| 5.30 - 5.43 | 3 |

# Join request
*Up to 5.10:*

| Type | Description |
| --- | --- |
| Uint8 | Message type (1) |
| Uint8 | Station index |
| Uint16 | Padding (always 0) |
| [StationAddress] | Station address |
| Uint32 | Ack id |

*5.11 - 5.18:*

| Type | Description |
| --- | --- |
| Uint8 | Message type (1) |
| Uint8 | Station index |
| Uint32 | Ack id |

# Join response (success)
If the join response is too big to be sent in a single packet it is split into fragments.

*Up to 3.10:*

| Type | Description |
| --- | --- |
| Uint8 | Message type (2) |
| Uint8 | Number of stations in mesh, including joining station |
| Uint8 | Index of host station |
| Uint8 | Index of joining station |
| Uint8 | Number of fragments |
| Uint8 | Fragment index |
| Uint8 | Number of station info entries in current fragment (N) |
| Uint8 | Base index of station info in current fragment |
| [StationInfo] (xN) | Station info list |
| Uint32 | Ack id |

*4.8 - 4.10:*

| Type | Description |
| --- | --- |
| Uint8 | Message type (2) |
| Uint8 | Number of stations in mesh, including joining station |
| Uint8 | Index of host station |
| Uint8 | Index of joining station |
| Uint8 | Number of fragments |
| Uint8 | Fragment index |
| Uint8 | Number of station info entries in current fragment (N) |
| Uint8 | Base index of station info in current fragment |
| Uint8 | Maximum number of stations in first mesh |
| Uint8 | Maximum number of stations in second mesh |
| Uint16 | Padding |
| [StationInfo] (xN) | Station info list |
| Uint32 | Ack id |

*5.18*

| Type | Description |
| --- | --- |
| Uint8 | Message type (2) |
| Uint8 | Number of stations in mesh, including joining station |
| Uint8 | Index of host station |
| Uint8 | Index of joining station |
| Uint8 | Number of fragments |
| Uint8 | Fragment index |
| Uint8 | Number of station info entries in current fragment (N) |
| Uint8 | Base index of station info entries in current fragment |
| Uint8 | Maximum number of stations in first mesh |
| Uint8 | Maximum number of stations in second mesh |
| Uint8 | Maximum number of stations (total) |
| Uint8 | Padding |
| Uint32 | Update counter (incremented on each mesh update) |
| [StationInfo] (xN) | Station info list |
| Uint32 | Ack id |

# Join response (denying)
| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 1 | Message type (2) |
| 0x1 | 1 | Always 0 |
| 0x2 | 1 | Always 0xFF |
| 0x3 | 1 | Always 0xFF |
| 0x4 | 1 | Reason |

# Leave request
| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 1 | Message type |
| 0x1 | 1 | Station index |
| 0x2 | 2 | Padding |
| 0x4 | 8 | [StationAddress] |

# Leave response
| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 1 | Message type |
| 0x1 | 1 | Station index |
| 0x2 | 2 | Padding |
| 0x4 | 8 | [StationAddress] |

# Destroy request
| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 1 | Message type |
| 0x1 | 1 | Station index |
| 0x2 | 2 | Padding |
| 0x4 | 8 | [StationAddress] |

# Destroy response
| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 1 | Message type |
| 0x1 | 1 | Station index |

# Update mesh
Because this message is sent through the reliable mesh protocol it does not need to be split into fragments like the join response.

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 1 | Message type |
| 0x1 | 1 | Number of stations |
| 0x2 | 1 | Host index |
| 0x3 | 1 | Always 0 |
| 0x4 | 4 | Update counter (incremented on each mesh update) |
| 0x8 | 1 | Number of fragments |
| 0x9 | 1 | Fragment index |
| 0xA | 1 | Number of station info entries in current fragment |
| 0xB | 1 | Base index of station info entries in current fragment |
| 0xC | | [StationInfo] entries |

# StationInfo
*Up to 5.9:*

| Type | Description |
| --- | --- |
| [StationConnectionInfo](Pia-Types#stationconnectioninfo) | Connection info |
| Uint8 | Station index |
| | Padding such that the size becomes a multiple of 4 bytes. |

*5.10 - 5.18:*

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 0x3E | [StationLocation](Pia-Types#stationlocation). If it takes up less than 0x3E bytes the remaining bytes are filled with 0's. |
| 0x3E | 1 | Station index |
| 0x3F | 1 | Padding |

[StationInfo]: #stationinfo

[StationAddress]: Pia-Types#stationaddress