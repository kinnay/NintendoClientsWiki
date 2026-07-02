ENL is Nintendo's private peer-to-peer framework that's used by many first-party games, such as Mario Kart 8, Splatoon 2 and Super Mario Maker 2. Check out the pages about [Pia](Pia-Overview) for details on how a peer-to-peer session is set up. Once the session is ready, ENL sends all packets through the [unreliable protocol](Unreliable-Protocol).

To transmit game-data, games can register content transporters to ENL. ENL also implements a few content transporters on its own.

A message consists of one or more records, terminated by a record with type 255. No byte swapping is done on the fields. The endianness depends on the system.

## Record Header
| Type | Description |
| --- | --- |
| Uint8 | Record type |
| Uint16 | Record size |
| Bytes | Record data |

| Record Type | Description |
| --- | --- |
| 0 - 31 | Game-specific |
| 253 | [System request info](#system-request-info) |
| 254 | [System information](#system-information) |
| 255 | End record |

## System request info
Clients can use this to request a specific record from another client. Every non-zero bit in the record mask indicates a record type that the client wants to receive. The least significant bit represents record type 0, and the most significant bit represents record type 31.

On the Switch, a new field was added that lets a client request a system-record. Here, bit 0 represents record type 253, and bit 1 represents record type 254.

*Wii U:*

| Type | Description |
| --- | --- |
| Uint32 | Record mask (games) |

*Switch:*

| Type | Description |
| --- | --- |
| Uint32 | Record mask (games) |
| Uint32 | Record mask (system) |

## System information
In the tables below, the values of P (maximum number of players) and Q (maximum number of CPUs) are configured by the game.

| Game | P | Q |
| --- | --- | --- |
| Mario Kart 8 | 14 | 10 |
| Splatoon 2 | 10 | 0 |
| Super Mario Maker 2 | 4 | 0 |

*Wii U:*

| Type | Description |
| --- | --- |
| Uint32 | Connected AID bitmap |
| Uint32 | Disconnected AID bitmap |
| Uint32 | CPU AID bitmap |
| Uint32 | Received AID bitmap |
| Uint64 | [Session time](Sync-Clock-Protocol) at join |
| Uint32 | Principal id |
| Uint32 | Unknown |
| Uint8 | Is player id table initialized |
| [UniqueId](#uniqueid) (P*2-1) | Player unique ids |
| [UniqueId](#uniqueid) (Q) | CPU unique ids |
| Uint8 | Player id sync unique |
| Uint8 (P) | Player id table |

*Switch:*

| Type | Description |
| --- | --- |
| Uint64 | Connected AID bitmap |
| Uint64 | Disconnected AID bitmap |
| Uint64 | CPU AID bitmap |
| Uint64 | Received AID bitmap |
| Uint64 | [Session time](Sync-Clock-Protocol) at join |
| Uint64 | Principal id |
| Uint8 | Is player id table initialized |
| [UniqueId](#uniqueid) (P*2-1) | Player unique ids |
| [UniqueId](#uniqueid) (Q) | CPU unique ids |
| Uint8 | Player id sync unique |
| Uint8 (P) | Player id table |

### UniqueId
*Wii U:*

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 4 | [Constant id] |
| 0x4 | 1 | Player id |
| 0x5 | 1 | Unknown |
| 0x6 | 2 | Padding (always 0) |

*Switch:*

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 8 | [Constant id] |
| 0x8 | 1 | Is local player |
| 0x9 | 1 | Is disconnected |
| 0xA | 6 | Padding (always 0) |

## Reverse Engineering Notes
A content transporter vtable has the following methods:

```c
init()
getSendBuffer()
getSendBufferSize()
isNeedSend()
getContentID()
getPacketNo()
setPacketNo(int)
send(bool)
startIdling()
endIdling()
isIdling()
sendCommit()
receiveCommit(const char &)
onCheckReceive(const char &, uint8_t *, uint32_t)
onReceived(const char &, uint8_t *, uint32_t)
onDisconnect(const char &, const char &)
onDisconnectGone(const char &, const char &)
readySendStream(enl::RamWriteStream &)
readyReceiveStream(enl::RamReadStream &, enl::Buffer *, uint32_t)
setLocalPlayerNum(uint8_t)
setSendInterval(uint8_t)
resetReceive()
getReceivedAIDBmp()
checkReceive(const char &)
checkAnybodyReceive()
onConnectInitialize()
isNeedCheckTwiceReceive()
updateSendTarget(const enl::UniqueID &, enl::UniqueID &)
getLastReceiveTime(const char &)
calcSendInterval(const sead::BitFlag<uint64_t> &)
checkDerivedRuntimeTypeInfo(const sead::RuntimeTypeInfo::Interface *)
getRuntimeTypeInfo()
getMySendData()
getMySendData()
getReceiveDataByAID(const char &)
getReceiveDataByPlayerID(const char &)
getReceiveDataByUniqueID(const enl::UniqueID &)
clearAllReceivedData()
checkAllReceive()
postInit_()
onReceivedCore_(const char &, enl::SystemInformation *, uint32_t)
onCheckReceiveCore_(const char &, enl::SystemInformation *, uint32_t)
getSendData()
getSendData()
```

Most of these have a standard implementation, but the following methods are interesting:
* `getSendBufferSize` returns the size of the payload.
* `getMySendData` is usually called to obtain a pointer to the payload. By looking for cross references to `getMySendData` it is possible to find functions that modify the payload.
* `send` sets a flag that indicates whether the record should be transmitted or not.

[Constant id]: Pia-Types#constant-id