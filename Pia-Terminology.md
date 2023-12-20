[Pia](Pia-Overview) > Terminology
---

This page describes common terms that are used by the Pia library.

1. [Station](#station)
2. [Constant id](#constant-id)
3. [Variable id](#variable-id)
4. [Service variable id](#service-variable-id)

## Station
A station is just a console. Note that one station may carry multiple players.

## Constant ID
The constant id uniquely identifies a station, and never changes, even across sessions. The constant id depends on the network type.

**NEX** *(Up to 5.44):*

The constant id is the same as your principal id (pid).

**LAN** *(Up to 5.9):*

The constant id is generated from your local IP address and port: `ip << 32 | port`

**LDN** *(Up to 5.9):*

The constant id is generated from your MAC address: `mac[2] << 56 | mac[4] << 48 | mac[5] << 40 | mac[3] << 32 | mac[1] << 24 | mac[0] << 16`.

## Variable ID
The variable id uniquely identifies a station in the current session. Unlike the [constant id](#constant-id), it may change across sessions. The variable id depends on the network type:

**NEX** *(Up to 5.44):*

The variable id is the same as your connection id (CID).

**LAN** *(Up to 5.9):*

The variable is set to the current system tick (`nn::os::GetSystemTick()`) at the start of the session.

**LDN** *(Up to 5.9):*

The variable is set to the current system tick (`nn::os::GetSystemTick()`) at the start of the session.

## Service Variable ID
Like the [variable id](#variable-id), the service variable id uniquely identifies a station in the current session and may change across sessions. The service variable id depends on the network type:

**NEX** *(Up to 5.44):*

The services variable id is your Rendez-Vous connection id (RVCID). This is received from the server when the client registers itself with the [secure connection protocol](Secure-Protocol).

**LAN** *(Up to 5.9):*

The service variable id is generated from your local IP address and port: `(ip & 0xFFFF) << 16 | port`.

**LDN** *(Up to 5.9):*

The service variable id is the CRC32 hash of your MAC address.