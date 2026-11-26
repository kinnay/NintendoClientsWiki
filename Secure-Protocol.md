## [[NEX Protocols]] > Secure Connection (11)

The following games have additional methods in the Secure Connection protocol:
* [Nintendo Badge Arcade](Secure-Protocol-(NBA))
* [Monster Hunter Generations Ultimate/XX](Secure-Protocol-(MHXX))

The remainder of this page describes the methods that are not specific to any game.

| Method ID | Method Name |
| --- | --- |
| 1 | [Register](#1-register) |
| 2 | [RequestConnectionData](#2-requestconnectiondata) |
| 3 | [RequestUrls](#3-requesturls) |
| 4 | [RegisterEx](#4-registerex) |
| 5 | [TestConnectivity](#5-testconnectivity) |
| 6 | [UpdateURLs](#6-updateurls) |
| 7 | [ReplaceURL](#7-replaceurl) |
| 8 | [SendReport](#8-sendreport) |

# (1) Register
The secure server keeps a list of client urls that can be registered (added) and replaced by the client.

## Request
| Type | Name | Description |
| --- | --- | --- |
| [List]&lt;[StationURL]&gt; | vecMyURLs | Local client urls |

## Response
| Type | Name | Description |
| --- | --- | --- |
| [Result] | %retval% | Result code |
| Uint32 | pidConnectionID | Rendez-Vous connection id |
| [StationURL] | urlPublic | Public client url, as perceived by the server |

The client should place the connection id into the RVCID field of its client station urls.

# (2) RequestConnectionData
## Request
| Type | Name | Description |
| --- | --- | --- |
| Uint32 | cidTarget | CID of station url |
| Uint32 | pidTarget | PID of station url |

## Response
| Type | Name | Description |
| --- | --- | --- |
| Bool | %retval% | Result |
| [List]&lt;[ConnectionData](#connectiondata-structure)&gt; | pvecConnectionsData | Connection data |

### ConnectionData ([Structure])
| Type | Name | Description |
| --- | --- | --- |
| [StationURL] | m_StationUrl | Station url |
| Uint32 | m_ConnectionID | Connection id |

# (3) RequestUrls
## Request
| Type | Name | Description |
| --- | --- | --- |
| Uint32 | cidTarget | CID |
| Uint32 | pidTarget | PID |

## Response
| Type | Name | Description |
| --- | --- | --- |
| Bool | %retval% | Result |
| [List]&lt;[StationURL]&gt; | plstURLs | Station urls |

# (4) RegisterEx
## Request
| Type | Name | Description |
| --- | --- | --- |
| [List]&lt;[StationURL]&gt; | vecMyURLs | Local client urls |
| [Data] | hCustomData | Login data, see below |

### NintendoLoginData / AccountExtraInfo
| Type | Description |
| --- | --- |
| [String] | Token (received from the account server) |

## Response
Same as response for the [Register](#1-register) method.

# (5) TestConnectivity
This method takes no parameters and doesn't return anything.

# (6) UpdateURLs
## Request
| Type | Name | Description |
| --- | --- | --- |
| [List]&lt;[StationURL]&gt; | vecMyURLs | Station urls |

## Response
This method doesn't return anything.

# (7) ReplaceURL
## Request
| Type | Name | Description |
| --- | --- | --- |
| [StationURL] | target | Old station url |
| [StationURL] | url | New station url |

## Response
This method does not return anything.

# (8) SendReport
## Request
| Type | Name | Description |
| --- | --- | --- |
| Uint32 | reportId | Report id |
| [qBuffer] | reportData | Data |

## Response
This method does not return anything.

[Result]: NEX-Common-Types#result
[qBuffer]: NEX-Common-Types#qbuffer
[List]: NEX-Common-Types#list
[String]: NEX-Common-Types#string
[StationURL]: NEX-Common-Types#stationurl
[Data]: NEX-Common-Types#anydataholder
[Structure]: NEX-Common-Types#structure
