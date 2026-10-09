This page describes the local content share protocol of the Nintendo Switch. This protocol can be used to share update data with a nearby device without internet connection. The protocol is implemented by the `qlaunch` program and can be activated by using the "Match Version With Local Users" feature of the home menu. This page describes the protocol as seen in firmware version 22.5.0.

Unless specified otherwise, all fields are encoded in big endian byte order.

* [Network details](#network-details)
* [Server protocol](#server-protocol)

## Network Details
The protocol is implemented on top of [LDN](LDN-Protocol). After creating the LDN network, the host starts a TCP server on port 55555. The server protocol is described [below](Server-Protocol).

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

## Server Protocol
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
| 10 | ? |
| 11 | ? |
| 12 | ? |
| 13 | ? |
| 14 | ? |
| 15 | ? |
| 16 | ? |
| 17 | ? |
| 18 | ? |
| 19 | ? |
| 20 | ? |
| 21 | ? |
| 22 | ? |
| 23 | ? |
| 24 | ? |
| 25 | ? |
| 26 | ? |
| 27 | ? |

### Application Control Data Size Request
| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 8 | [Packet header](#server-protocol) |
| 0x8 | 8 | Title id |

### Application Control Data Size Response
| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 8 | [Packet header](#server-protocol) |
| 0x8 | 8 | Title id |
| 0x10 | 4 | Application control data size |

### Application Control Data Request
| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 8 | [Packet header](#server-protocol) |
| 0x8 | 8 | Title id |

### Application Control Data Response
The application control data contains the [NACP file](https://switchbrew.org/wiki/NACP) of the game, followed by a JPEG thumbnail.

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 8 | [Packet header](#server-protocol) |
| 0x8 | 8 | Title id |
| 0x10 | 4 | Application control data size |
| 0x14 | | Application control data |

### Join Request
| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 8 | [Packet header](#server-protocol) |
| 0x8 | 1 | [Protocol version](#protocol-version) |
| 0x9 | 1 | Number of applications |
| 0xA | 1 | Padding |
| 0xB | 129 | Device nickname |
| 0x8C | 4 | Padding |
| 0x90 | 256 | [System delivery info](https://switchbrew.org/wiki/NS_services#SystemDeliveryInfo) (little endian) |
| 0x190 | | [Application detail](#application-details) array |

### Join Response
The node is is assigned by the host. It starts at a random value and is increment for every new participant.

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 8 | [Packet header](#server-protocol) |
| 0x8 | 4 | Node id |

### Error Packet
| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 8 | [Packet header](#server-protocol) |
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
| 0x0 | 8 | [Packet header](#server-protocol) |
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