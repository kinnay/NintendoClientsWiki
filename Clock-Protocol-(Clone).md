[Pia](Pia-Overview) > [Protocols](Pia-Protocols) > Clock Protocol (clones)
---

The clock protocol provides a game-specific clock that is synchronized across all stations in the mesh. The speed at which the clock advances is controlled by the game. When a station wants to synchronize its clock, it sends a request to the station with the lowest index in the mesh. This is not necessarily the host.

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 1 | 0 = request, 1 = response |
| 0x1 | 1 | Sequence id |
| 0x2 | 8 | Request clock value |
| 0xA | 8 | Response clock value |

The following version number is advertised during the [connection request](Station-Protocol):

| Pia version | Version |
| --- | --- |
| 5.19 - 5.44 | 0 |
| 5.45 | 1 |


