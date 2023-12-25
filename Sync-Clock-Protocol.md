[Pia](Pia-Overview) > [Protocols](Pia-Protocols) > Sync Clock Protocol
---

The sync clock protocol provides a monotonic clock that is synchronized across all stations in the mesh. The clock is controlled by the host.

Every two seconds, the station sends the following message to the host:

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 8 | Current system tick |
| 0x8 | 8 | Always 0 |

The host sends the following reply:

| Offset | Size | Description |
| --- | --- | --- |
| 0x0 | 8 | System tick copied from request |
| 0x8 | 8 | Synchronized clock in milliseconds |