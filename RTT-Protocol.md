[[Pia Protocols]] > RTT Protocol
---

All messages are sent through port 1 and contain the following payload:

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 4 | 0 = request, 1 = response |
| 0x4 | 4 | Padding (always 0) |
| 0x8 | 8 | System time (OSGetSystemTime on Wii U, nn::os::GetSystemTick on Switch) |

The following version numbers are advertised during the [connection request](Station-Protocol):

| Pia version | Version |
| --- | --- |
| 5.29 - 5.44 | 3 |
| 5.45 | 4 |
