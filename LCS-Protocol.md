This page describes the local content share protocol of the Nintendo Switch. This protocol can be used to share update data with a nearby device without internet connection. The protocol can be activated by using the "Match Version With Local Users" feature of the home menu. This page describes the protocol as seen in firmware version 22.5.0.

Unless specified otherwise, all fields are encoded in big endian byte order.

* [Network details](#network-details)
* [Management protocol](#management-protocol)
* [Transfer protocol](#transfer-protocol)
* [Communication flow](#communication-flow)

## Network Details
The protocol is implemented on top of [LDN](LDN-Protocol). After creating the LDN network, the host starts a TCP server on port 55555. The server protocol is described [below](Management-Protocol).

When a Nintendo Switch game is selected on the home menu, the LDN network is created with the following parameters:
* Local communication id: `0100000000001000`
* Scene id: 1
* Maximum number of participants: 8
* Participant name: `LcsHost` or `LcsClient`, depending on the role of the device
* Application communication version: 1
* Passphrase: `2d30885a658ab4e4d85092ed525a994c`

> **Note:** when a Nintendo Switch 2 game is selected on the home menu, the network is created with Nintendo Switch 2-specific encryption keys. The details of exchanging Nintendo Switch 2 software via LCS are currently unknown.

The application data that is broadcasted by the access point has the following format:

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 1 | [Protocol version](#protocol-version) |
| 0x1 | 1 | Unknown |
| 0x2 | 1 | Current number of participants |
| 0x3 | 1 | Maximum number of participants |
| 0x4 | 1 | Number of applications (N) |
| 0x5 | 1 | Unknown |
| 0x6 | 1 | Unknown |
| 0x7 | 1 | Padding |
| 0x8 | 4 | Unknown |
| 0xC | 4 | Unknown |
| 0x10 | 7 | Padding |
| 0x17 | 129 | Device nickname |
| 0x98 | 8 * 8 | Unknown |
| 0xD8 | 40 * N | Application info |

Currently, the implementation only supports one application to be shared per network. Therefore, the size of the application data is always 256 bytes in practice.

The application info has the following format:

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 4 | Always 4? |
| 0x4 | 4 | Unknown |
| 0x8 | 8 | Title id |
| 0x10 | 8 | Content size? |
| 0x18 | 16 | Display version string |

## Protocol Version
The protocol version is `(major << 4) | minor`. The application communication version of the LDN network is set to the major version.

| System version | Protocol version |
| --- | --- |
| 22.5.0 | `0x13` |

## Management Protocol
This protocol is provided by the owner of the local content share group on TCP port 55555. It is implemented by the `qlaunch` process.

Every packet has the following format:

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 1 | Always 16? |
| 0x1 | 1 | Packet type |
| 0x2 | 2 | Padding |
| 0x4 | 4 | Payload size (N) |
| 0x8 | N | Payload |

The following packet types are currently known:

| Type | Description |
| --- | --- |
| 1 | [Application control data size request](#application-control-data-size-request) |
| 2 | [Application control data size response](#application-control-data-size-response) |
| 3 | [Application control data request](#application-control-data-request) |
| 4 | [Application control data response](#application-control-data-response) |
| 5 | [Join request](#join-request) |
| 6 | Leave network |
| 7 | [Join response](#join-response) |
| 8 | [Error](#error-packet) |
| 9 | [Network info](#network-info) |
| 10 | [Start communication](#start-communication) |
| 11 | ? |
| 12 | [Prepare system update request](#prepare-system-update-request) |
| 13 | [Prepare system update response](#prepare-system-update-response) |
| 14 | [Send system update request](#send-system-update-request) |
| 15 | [Send system update response](#send-system-update-response) |
| 16 | [Receive system update request](#receive-system-update-request) |
| 17 | [Receive system update response](#receive-system-update-response) |
| 18 | [Prepare game update request](#prepare-game-update-request) |
| 19 | [Prepare game update response](#prepare-game-update-response) |
| 20 | [Send game update request](#send-game-update-request) |
| 21 | [Send game update response](#send-game-update-response) |
| 22 | [Receive game update request](#receive-game-update-request) |
| 23 | [Receive game update response](#receive-game-update-response) |
| 24 | ? |
| 25 | ? |
| 26 | ? |
| 27 | ? |

### Application Control Data Size Request
| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 8 | [Packet header](#management-protocol) |
| 0x8 | 8 | Title id |

### Application Control Data Size Response
| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 8 | [Packet header](#management-protocol) |
| 0x8 | 8 | Title id |
| 0x10 | 4 | Application control data size |

### Application Control Data Request
| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 8 | [Packet header](#management-protocol) |
| 0x8 | 8 | Title id |

### Application Control Data Response
The application control data contains the [NACP file](https://switchbrew.org/wiki/NACP) of the game, followed by a JPEG thumbnail.

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 8 | [Packet header](#management-protocol) |
| 0x8 | 8 | Title id |
| 0x10 | 4 | Application control data size |
| 0x14 | | Application control data |

### Join Request
| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 8 | [Packet header](#management-protocol) |
| 0x8 | 1 | [Protocol version](#protocol-version) |
| 0x9 | 1 | Number of applications |
| 0xA | 1 | Padding |
| 0xB | 129 | Device nickname |
| 0x8C | 4 | Padding |
| 0x90 | 256 | [System delivery info] (little endian) |
| 0x190 | | [Application detail](#application-details) array |

### Join Response
The node is is assigned by the host. It starts at a random value and is increment for every new participant.

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 8 | [Packet header](#management-protocol) |
| 0x8 | 4 | Node id |

### Error Packet
| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 8 | [Packet header](#management-protocol) |
| 0x8 | 1 | Error code (see below) |
| 0x9 | 3 | Padding |

The following error codes are currently known:

| Code | Description |
| --- | --- |
| 1 | `2211-0232` |
| 2 | Join denied (network is full) |
| 3 | `2211-0256` - `2211-0287` except `2211-0260` |
| 4 | ? |
| 5 | ? |
| 6 | ? |
| 7 | ? |
| 8 | ? |
| 9 | Join denied (version too low) |
| 10 | Join denied (version too high) |

### Network Info
| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 8 | [Packet header](#management-protocol) |
| 0x8 | 1 | Number of applications |
| 0x9 | 1 | Number of nodes |
| 0xA | 6 | Padding |
| 0x10 | | [Application detail](#application-details) array |
| | | Node info array |

Every node info entry has the following structure:

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 4 | Node id |
| 0x4 | 7 | Padding |
| 0xB | 129 | Device nickname |

### Start Communication
This packet is transmitted when the host of the group presses the "Start communication" button. It has no payload.

### Prepare System Update Request
| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 8 | [Packet header](#management-protocol) |
| 0x8 | 4 | Unknown |

### Prepare System Update Response
| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 8 | [Packet header](#management-protocol) |
| 0x8 | 4 | Unknown |
| 0xC | 256 | Always 0 |

### Send System Update Request
| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 8 | [Packet header](#management-protocol) |
| 0x8 | 1 | Always 1 |
| 0x9 | 1 | Always 20 |
| 0xA | 1 | Always 1 |
| 0xB | 1 | Always 0 |delivery
| 0xC | 4 | IPv4 address of receiver |
| 0x10 | 4 | Node id of receiver |
| 0x14 | 4 | Always 0 |
| 0x18 | 256 | Always 0 |

### Send System Update Response
| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 8 | [Packet header](#management-protocol) |
| 0x8 | 1 | [Status value](#status-value) |
| 0x9 | 3 | Padding |
| 0xC | 256 | [System delivery info] (little endian) |

### Receive System Update Request
| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 8 | [Packet header](#management-protocol) |
| 0x8 | 1 | Always 2 |
| 0x9 | 1 | Always 20 |
| 0xA | 1 | Unknown (0 or 1) |
| 0xB | 1 | Always 0 |
| 0xC | 4 | IPv4 address of sender |
| 0x10 | 4 | Node id of sender |
| 0x14 | 4 | Always 0 |
| 0x18 | 256 | [System delivery info] (little endian) |

### Receive System Update Response
| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 8 | [Packet header](#management-protocol) |
| 0x8 | 1 | [Status value](#status-value) |
| 0x9 | 3 | Padding |
| 0xC | 256 | Always 0 |

### Prepare Game Update Request
| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 8 | [Packet header](#management-protocol) |
| 0x8 | 4 | Always 4 |
| 0xC | 8 | Title id |

### Prepare Game Update Response
| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 8 | [Packet header](#management-protocol) |
| 0x8 | 1 | [Status value](#status-value) |
| 0x9 | 1 | Always 0 |
| 0xA | 6 | Padding |

### Send Game Update Request
| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 8 | [Packet header](#management-protocol) |
| 0x8 | 1 | Always 1 |
| 0x9 | 1 | Always 4 |
| 0xA | 1 | Always 20 |
| 0xB | 1 | Unknown (0 or 1) |
| 0xC | 1 | Always 0 |
| 0xD | 3 | Padding |
| 0x10 | 4 | IPv4 address of receiver |
| 0x14 | 4 | Node id of receiver |
| 0x18 | 8 | Title id |

### Send Game Update Response
| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 8 | [Packet header](#management-protocol) |
| 0x8 | 1 | [Status value](#status-value) |
| 0x9 | 1 | Number of [content meta keys] (N) |
| 0xA | 6 | Padding |
| 0x10 | 16 * N | [Content meta keys] |

### Receive Game Update Request
| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 8 | [Packet header](#management-protocol) |
| 0x8 | 1 | Always 2 |
| 0x9 | 1 | Always 4 |
| 0xA | 1 | Always 20 |
| 0xB | 1 | Unknown (0 or 1) |
| 0xC | 1 | Number of [content meta keys] (N) |
| 0xD | 3 | Padding |
| 0x10 | 4 | IPv4 address of sender |
| 0x14 | 4 | Node id of sender |
| 0x18 | 8 | Title id |
| 0x20 | 16 * N | [Content meta keys] |

### Receive Game Update Response
| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 8 | [Packet header](#management-protocol) |
| 0x8 | 1 | [Status value](#status-value) |
| 0x9 | 1 | Always 0 |
| 0xA | 6 | Padding |

### Application Details
This structure is encoded in little endian byte order.

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 4 | Number of application delivery infos (N) |
| 0x4 | 4 | Padding |
| 0x8 | 8 | Title id |
| 0x10 | 4 | Unknown |
| 0x14 | 4 | Unknown |
| 0x18 | 8 | Estimated required size |
| 0x20 | 16 | Display version string |
| 0x30 | 88 | Padding? |
| 0x88 | 256 * N | [Application delivery info](https://switchbrew.org/wiki/NS_services#ApplicationDeliveryInfo) array |

### Status Value
Some packets include a status value that indicates whether an error has occurred. An error may occur, for example, when not enough free space is available on the device. The following values are currently known:

| Value | Description |
| --- | --- |
| 0 | Error |
| 2 | No error |

It is unclear whether the value 1 is ever used.

## Transfer Protocol
This protocol allows a node to share update data with another. The host of the network decides which nodes should share update data with each other. This is coordinated through the [management protocol](#management-protocol). The transfer protocol is implemented by the `nim` process.

When a node is requested to share update data with another, it starts a TCP server on port 55556. The node that shall receive the update data may then establish a connection with that server.

All packets are structured as follows:

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 4 | Magic number (`LDRq` for request, or `LDRs` for response) |
| 0x4 | 1 | Message type |
| 0x5 | 1 | Padding |
| 0x6 | 2 | Unknown |
| 0x8 | 8 | Payload size |
| 0x10 | | Payload |

The following message types are currently known:

| Type | Description |
| --- | --- |
| 1 | [Get content info](#get-content-info) |
| 2 | [Download content](#download-content) |
| 3 | Get ticket info |

### Get Content Info
Request:

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 16 | [Content meta key] |

Response:

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 32 | SHA-256 of content |
| 0x20 | 16 | Content id |
| 0x30 | 5 | Content size |
| 0x35 | 1 | Content attributes |
| 0x36 | 1 | Content type |
| 0x37 | 1 | Content id offset |

### Download Content
Request:

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 16 | Content id |
| 0x10 | 1 | Disable progress update |
| 0x11 | 7 | Padding |

Response:

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | | Encrypted NCA |

## Communication Flow
When a local content share room is created on a device, it creates a [network](#network-details) that advertises the game that is currently selected on the home menu. Other devices can scan for nearby networks and join them. After joining the underlying LDN network, the client must send a [join request](#join-request) to the host. The host responds by sending a [join response](#join-response) or an [error packet](#error-packet) back to the client. Whenever the network information is changed, such as when a new device is accepted into the group, the host broadcasts a [network info](#network-info) packet to all clients to inform them of the change.

When the user that created the group presses the "Start Communication" button, after at least one other device has joined the group, the host transmits a [start communication](#start-communication) packet. After that, it is no longer possible to join the group.

The host then decides which nodes can share update data with each other. If a system update is required, the system update is always exchanged before the game update. The host selects one node as the sender, and one node as the receiver. The host sends a [send system update request](#send-system-update-request) or [send game update request](#send-game-update-request) to the sender. After the host receives a response, the host sends a [receive system update request](#receive-system-update-request) or [receive game update-request](#receive-game-update-request) to the receiver.

The sender then opens a TCP server on port 55556. The receiver establishes a connection with this port. The update data is exchanged through the connection.

[system delivery info]: https://switchbrew.org/wiki/NS_services#SystemDeliveryInfo
[content meta key]: https://switchbrew.org/wiki/NCM_services#ContentMetaKey
[content meta keys]: https://switchbrew.org/wiki/NCM_services#ContentMetaKey