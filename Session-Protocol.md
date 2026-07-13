[Pia](Pia-Overview) > [Protocols](Pia-Protocols) > Session Protocol
---

The following version numbers are advertised during the [connection request](Station-Protocol):

| Pia version | Version |
| --- | --- |
| 5.19 | 0 |
| 5.26 - 5.45 | 1 |

*Up to 5.45:*
| Type | Description |
| --- | --- |
| 3 | Next session id |
| 4 | Prepared for migrate session |
| 6 | Invitation as companion |
| 7 | Answer to invitation as companion |
| 8 | Destroy invitation |
| 9 | Answer to destroy invitation |
| 10 | Leave mesh invitation |
| 11 | Answer to leave mesh invitation |
| 12 | Start config participation |
| 13 | Answer to start config participation |
| 14 | Finish config participation |
| 16 | Answer to finish config participation |
| 17 | Request config participation |
| 18 | Answer to config participation |
| 19 | Completion for migrate session |
| 20 | Completion invitation |
| 21 | Answer to completion invitation |
| 22 | Completion failure response |