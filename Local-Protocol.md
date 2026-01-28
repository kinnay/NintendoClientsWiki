[[Pia Protocols]] > Local Protocol
---

This protocol is used in LDN mode.

| Message Type | Description |
| --- | --- |
| 0x11 | [Update session](#update-session-message) |
| 0x12 | [Destroy network](#destroy-network-message) |
| 0x13 | [Start host migration](#start-host-migration-message) |
| 0x21 | [Update session ack](#ack-message) |

The following version numbers are advertised during the [connection request](Station-Protocol):

| Pia version | Version |
| --- | --- |
| 5.19 - 5.44 | 0 |

## Local message header
*5.2 - 5.44:*

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 1 | Version number (1) |
| 0x1 | 1 | Message type |
| 0x2 | 2 | Payload size |
| 0x4 | 6 | Always 0 |
| 0xA | 2 | Padding |

## Update session message
The host broadcasts this message on the network every 100 milliseconds.

*5.2:*
| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 12 | [Local message header](#local-message-header) |
| 0xC | 4 | Sequence id |
| 0x10 | 4 | Network id |
| 0x14 | 4 | Host variable id |
| 0x18 | 1 | Allow participating state |
| 0x19 | 7 | Padding |
| 0x20 | | [Payload](#update-session-payload) |

*5.7 - 5.44:*

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 12 | [Local message header](#local-message-header) |
| 0xC | 4 | Sequence id |
| 0x10 | 4 | Network id |
| 0x14 | 4 | Host variable id |
| 0x18 | 4 | Host service variable id |
| 0x1C | 4 | Padding |
| 0x20 | 8 | Host constant id |
| 0x28 | 1 | Allow participating state |
| 0x29 | 7 | Padding |
| 0x30 | | [Payload](#update-session-payload) |

### Update session payload
*5.2 - 5.44:*

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 8 x 9 | [Local nodes](#local-node) |
| 0x48 | 1 | Host migration state |

## Destroy network message
*5.9:*

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 12 | [Local message header](#local-message-header) |
| 0xC | 4 | Always 0 |

## Start host migration message
*5.9:*

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 12 | [Local message header](#local-message-header) |
| 0xC | 4 | Always 0 |

## Ack message
*5.9 - 5.44:*

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 12 | [Local message header](#local-message-header) |
| 0xC | 4 | Sequence id |
| 0x10 | 4 | Always 0 |

## Local node
*5.2 - 5.44:*

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 8 | [Local address](#local-address) |
| 0x8 | 1 | Host migration ranking |

## Local address
*5.2 - 5.44:*

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 6 | [Inet address](Pia-Types#inetaddress) |
| 0x6 | 2 | Extension address (always 0) |