## [[NEX Protocols]] > Notifications (14)

| Method ID | Method Name |
| --- | --- |
| 1 | [ProcessNotificationEvent](#1-processnotificationevent) |

# (1) ProcessNotificationEvent
## Request
| Type | Name | Description |
| --- | --- | --- |
| [NotificationEvent](#notificationevent-structure) | oEvent | Event object |

## Response
No RMC response is sent.

# NotificationEvent ([Structure])
Most notification types are predefined. However, some games also implement their own notification types (see [libeagle](Eagle-Protocol) for example).

**Wii U:**

| Type | Name |
| --- | --- |
| [PID] | m_pidSource |
| Uint32 | m_uiType |
| Uint32 | m_uiParam1 |
| Uint32 | m_uiParam2 |
| [String] | m_strParam |

The following field is only present in NEX version 3.5.x and later:

| Type | Name |
| --- | --- |
| Uint32 | m_uiParam3 |

**Switch:**

The following fields are always present (revision 0 and 1):

| Type | Name |
| --- | --- |
| [PID] | m_pidSource |
| Uint32 | m_uiType |
| Uint64 | m_uiParam1 |
| Uint64 | m_uiParam2 |
| [String] | m_strParam |
| Uint64 | m_uiParam3 |

The following field is only present in revision 1:

| Type | Name |
| --- | --- |
| [Map]&lt;[String], [Variant]&gt; | m_mapParam |

## Notification Types
* Type 3001 - 3008 are sent to the owner of the gathering.
* Type 4000 and 109000 are sent to all participants of the gathering.
* Type 116000 is sent to all participants of the round.

| Type | Description |
| --- | --- |
| 3001 | New participant |
| 3002 | Participation cancelled |
| 3007 | Participant disconnected |
| 3008 | Participation ended |
| 4000 | Ownership changed |
| 109000 | Gathering unregistered |
| 110000 | Host changed |
| 116000 | Matchmake referee round started |
| 120000 | System password changed |
| 121000 | System password cleared |
| 122000 | Switch gathering |

Notification type 3001:

| Field | Description |
| --- | --- |
| m_pidSource | Principal id |
| m_uiParam1 | Gathering id |
| m_uiParam2 | Principal id |
| m_strParam | Message |
| m_uiParam3 | Number of participants |

Notification type 3002, 3007 and 3008:

| Field | Description |
| --- | --- |
| m_pidSource | Principal id |
| m_uiParam1 | Gathering id |
| m_uiParam2 | Principal id |
| m_strParam | Message |

Notification type 4000:

| Field | Description |
| --- | --- |
| m_pidSource | Previous owner |
| m_uiParam1 | Gathering id |
| m_uiParam2 | New owner |
| m_strParam | Timestamp in microseconds |

Notification type 109000:

| Field | Description |
| --- | --- |
| m_pidSource | Principal id |
| m_uiParam1 | Gathering id |

Notification type 116000:

| Field | Description |
| --- | --- |
| m_pidSource | Principal that started the round |
| m_uiParam1 | Round id |

Notifiation type 122000:

| Field | Description |
| --- | --- |
| m_pidSource | Host pid |
| m_uiParam1 | New gathering id |
| m_uiParam2 | Client pid |

[PID]: NEX-Common-Types#pid
[String]: NEX-Common-Types#string
[Structure]: NEX-Common-Types#structure
[Map]: NEX-Common-Types#map
[Variant]: NEX-Common-Types#variant