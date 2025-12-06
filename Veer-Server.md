[Switch](Server-List#switch) > Vendor Weights
---

Title content is provided by three different vendors: akamai, llnw and lumen. The veer server provides a policy that assigns a weight to each vendor. The higher the weight for a vendor, the higher the probability that the Switch downloads the content from that vendor.

The veer server was introduced in system version 14.0.0 and only accepts requests with a valid device certificate.

* [Header](#headers)
* [Methods](#methods)

## Headers
| Header | Description |
| --- | --- |
| Host | `veer.hac.lp1.d4c.nintendo.net` |
| User-Agent | [User agent](#user-agents) |
| Accept | `application/json` |

### User Agents
The user agent looks as follows: `NintendoSDK Firmware/<firmware version>-<revision> (platform:NX; did:<device id>; eid:lp1)`. The firmware version and revision number are obtained from the [system version title](https://switchbrew.org/wiki/System_Version_Title).

Here is an example: `NintendoSDK Firmware/15.0.0-4.0 (platform:NX; did:6265ca40780b1c0d; eid:lp1)`

## Methods
| Method | Path |
| --- | --- |
| GET | `/v1/policy.json` |
| GET | `/v2/policy.json` |
| GET | `/v3/policy.json` |

| System version | API version |
| --- | --- |
| 14.0.0 - 14.1.2 | v2 |
| 15.0.0 - 18.1.0 | v3 |

| Param | Description |
| --- | --- |
| context | `selection`, `reselection_by_system_due_to_error`, `reselection_by_system_due_to_timeout` or `reselection_by_user` |

Note that `v1` was never used by the Switch.

Response for `v1`:

```json
{
  "weights": [{"vendor": "akamai", "weight":100}],
  "uuid": "3c37a3ea-4f26-42b3-bddf-1988f8f322cb"
}
```

Response for `v2`:

```json
{
  "weights": [
    {"vendor": "akamai", "weight":100},
    {"vendor": "llnw", "weight":0}
  ],
  "uuid":"9b2d588a-7f85-46e8-8347-2b4f32288b41"
}
```

Response for `v3`:

```json
{
  "weights": [
    {"vendor": "akamai", "weight": 81},
    {"vendor": "llnw", "weight": 19}
  ],
  "uuid": "2cd1b8b6-c1e7-4238-96c3-0e18ec9c2945",
  "ttl": 86400
}
```


Response for `v4`:

```json
{
  "weights": [
    {"vendor": "akamai", "weight":50},
    {"vendor": "fastly", "weight":50},
    {"vendor": "cloudflare", "weight":0}
  ],
  "uuid": "0a3a7f5b-399b-401b-a71c-02aa0b4ffe4c",
  "ttl": 300
}
```

Response for `v5`:

```json
{
  "weights": [
    {"vendor": "akamai", "weight":50},
    {"vendor": "fastly", "weight":50},
    {"vendor": "cloudflare", "weight":0}
  ],
  "uuid": "e324921d-d8de-4ed5-9f81-fb5ca8789cf7",
  "ttl": 60
}
```