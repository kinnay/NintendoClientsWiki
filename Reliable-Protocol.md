[[Pia Protocols]] > Reliable Protocol
---

This protocol may be used by games to send data packets to other consoles. The reliable protocol ensures that all packets arrive in the correct order by using a [[reliable sliding window]]. The payload of each reliable message contains game-specific data.

The following version numbers are advertised during the [connection request](Station-Protocol):

| Pia version | Version |
| --- | --- |
| 5.29 | 2 |
| 5.44 | 4 |
