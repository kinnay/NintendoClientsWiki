[Switch](Server-List#switch) > Virtual Game Cards
---

The vermillion server implements virtual game cards.

URL: https://gw.hac.lp1.vermillion.srv.nintendo.net

## Methods
| Method | Path |
| --- | --- |
| GET | `/v1/accounts/config` |
| GET | `/v1/accounts/devices` |
| ? | `/v1/accounts/devices/<id>` |
| ? | `/v1/accounts/devices/<id>/replace` |
| ? | `/v1/accounts/in-same-family` |
| POST | `/v1/accounts/notify` |
| POST | `/v1/accounts/notify-to-family` |
| GET | `/v1/accounts/vphym-borrowers/candidates` |
| GET | `/v1/accounts/vphyms` |
| GET | `/v1/devices` |
| GET | `/v1/nearness-checks` |

## Errors
On error, the server sends the following response:

| Field | Description |
| --- | --- |
| type | `https://problem-details.ennovate.srv.nintendo.net/vemillion-gw/<name>`
| status | HTTP status code |
| title | Error title |
| errorCode | Error code |
| module | `VERMILLION_GW` |
| traceId | Trace id (32 hex digits) |

### Known Errors
| Name | Status | Code | Title |
| --- | --- | --- | --- |
| `unexpected-error` | | |
| `api-not-found` | 404 | `5011` | `API_NOT_FOUND` |
| `communication-failed` | | |
| `invalid-params` | | |
| `invalid-auth-token` | 401 | `5014` | `INVALID_AUTH_TOKEN` |
| `resource-not-found` | | |
| `device-registration-limit-reached` | | |
| `invalid-nearness-check-result` | | |
| `operation-not-allowed` | | |
| `invalid-certificate` | | |
| `direct-message-failed` | | |
| `direct-message-receiver-is-offline` | | |
| `invalid-account-config-payload` | | |
| `device-unregistration-limit-reached` | | |
| `invalid-migration-state` | | |
| `vermillion-app-call-failed` | | |
| `atums-call-failed` | | |
| `dragons-call-failed` | | |
| `pegasus-call-failed` | | |
| `baas-call-failed` | | |
| `penne-call-failed` | | |
| `nas-call-failed` | | |