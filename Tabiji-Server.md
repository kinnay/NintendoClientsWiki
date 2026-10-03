[Switch](Server-List#switch) > Play Statistics
---

The tabiji server is used to upload and retrieve play statistics for a given user. In official firmware, the server is contacted by the `eupld` process. The server was introduced in firmware version 23.0.0.

The server is hosted at the following URL: `https://api.hac.lp1.tabiji.srv.nintendo.net`.

A device certificate is required to access this server.

* [Header](#headers)
* [Methods](#methods)
* [Errors](#errors)

## Headers
| Header | Description |
| --- | --- |
| Host | `api.hac.lp1.tabiji.srv.nintendo.net` |
| Accept | `*/*` |
| User-Agent | [User agent](#user-agents) |
| Authorization | [ID token](BAAS-Server) |

On POST requests, the following headers are also present:

| Header | Description |
| --- | --- |
| Content-Type | `application/json` |
| Content-Length | Content length |

### User Agents
| System version | User agent |
| --- | --- |
| 23.0.0 - 23.0.1 | `libcurl (nnPdm; 789f928b-138e-4b2f-afeb-1acae821d897; SDK 23.3.0.0; Add-on 23.3.0.0)` |

## Methods
| Method | Path |
| --- | --- |
| POST | [`/console/v1/play_histories`](#post-consolev1play_histories) |
| GET | [`/console/v1/play_statistics/<title id>`](#get-consolev1play_statisticstitle-id) |

## POST /console/v1/play_histories
| Field | Description |
| --- | --- |
| play_histories | Play history array |

Elements of the play history array has the following fields:

| Field | Description |
| --- | --- |
| title | Title information (see below) |
| session_id | Unknown, looks like a random hex number, e.g. `0x5c037756e4b13cd9` |
| operation_mode | `HANDHELD` or `CONSOLE` |
| is_stream_play | Boolean |
| os_version | Firmware version string or null |
| is_japan | Boolean or null |
| play_log_policy | `NONE`, `OPEN`, `CLOSED` or `LOG_ONLY` |
| duration_sec | Integer |
| timezone_offset_sec | Integer or null |
| started_at | Clock value (see below) |
| ended_at | Clock value (see below) |

The title information has the following fields:

| Field | Description |
| --- | --- |
| application_id | Title id string |
| acd_index | Unknown |
| version | Title version as integer |
| storage_id | `NONE`, `CARD`, `HOST`, `ANY`, `SD_CARD`, `BUILT_IN_USER` or `BUILT_IN_SYSTEM` |
| application_copy_id_hash | Unknown |

A clock value has the following fields:

| Field | Description |
| --- | --- |
| network_clock_sec | Unknown (integer) |
| steady_clock_source_id | Unknown |
| steady_clock_sec | Unknown |
| user_clock_sec | Unknown (integer) |

Response on success:

| Field | Description |
| --- | --- |
| accepted_item_count | Integer |
| backpressure | See below |
| rejected_items | Unknown array |

The backpressure field contains the following fields:

| Field | Description |
| --- | --- |
| catchup | See below |
| standard | See below |

The catchup and standard fields contain the following fields:

| Field | Description |
| --- | --- |
| max_play_histories_count | Integer |
| min_interval_sec | Integer |

## GET /console/v1/play_statistics/&lt;title id&gt;
Response on success:

| Field | Description |
| --- | --- |
| backpressure | See below |
| play_statistic | Play statistic (see below) |

The "backpressure" field contains an object with a "standard" field, which contains an object with a "min_interval_sec" field, which contains an integer.

The play statistics contain the following fields:

| Field | Description |
| --- | --- |
| application_id | Title id string |
| device_latest_play_time | Timestamp |
| first_play_time | Timestamp |
| is_open | Boolean |
| latest_acd_index | Unknown |
| latest_play_time | Timestamp |
| total_play_count | Integer |
| total_play_time | Integer |

## Errors
On error, the server sends the following response:

| Field | Description |
| --- | --- |
| code | Error code |
| detail | Error description |
| status | HTTP status code |
| title | Error title |

### Known Errors
| Code | Status | Title | Detail |
| --- | --- | --- | --- |
| 3000 | 401 | Unauthorized | authentication required |
| 4040 | 404 | Not Found | play statistic not found |