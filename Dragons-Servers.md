[Switch](Server-List#switch) > eLicenses
---

The dragons servers are responsible for managing e-licenses on the Nintendo Switch. An e-license carries the right to play a game, and is obtained by purchasing the game on the Nintendo eShop.

The dragons servers take JSON-encoded requests and respond with JSON-encoding. The dragons servers only accept connections with a valid device certificate.

* [Header](#headers)
* [Methods](#methods)
* [Errors](#errors)

## Headers
The following headers are always present:

| Header | Description |
| --- | --- |
| Host | One of the dragons servers |
| Accept | `*/*` |
| User-Agent | [User agent](#user-agents) |
| DeviceAuthorization | `Bearer ` + [device token](DAuth-Server) |

The following headers are optional and depend on the method and device type:

| Header | Description |
| --- | --- |
| AccountAuthorization | `Bearer ` + [account token](Account-Server-(Switch)) |
| Nintendo-Account-Id | Nintendo account id (`%016llx`) |
| Nintendo-Application-Id | Title id (`%016llx`) |
| Nintendo-Nsa-Id-Token | `Bearer ` + id token |
| Nintendo-ReferToVirtualDeviceLink | Only present on kiosk and development hardware. If present, always `true`. |

If the request body is empty, a `Content-Length: 0` header is sent, and up to 16.1.0 also a `Content-Type: application/x-www-form-urlencoded` header.

Otherwise, the following headers are sent:

| Header | Description |
| --- | --- |
| Content-Type | `application/json` |
| Content-Length | Content length |

There is one exception. In [`/v1/contents_authorization_token_for_aauth/issue`](#post-v1contents_authorization_token_for_aauthissue),  the headers are ordered as follows: `Host`, `User-Agent`, `Accept`, `Content-Type`, `DeviceAuthorization`, `Nintendo-Application-Id` and `Content-Length`. The reason is that this request is performed by the account sysmodule instead of nim.

### User Agents
The user agent looks as follows: `NintendoSDK Firmware/<firmware version>-<revision> (platform:NX; did:<device id>; eid:lp1)`. The firmware version and revision number are obtained from the [system version title](https://switchbrew.org/wiki/System_Version_Title).

Here is an example: `NintendoSDK Firmware/15.0.0-4.0 (platform:NX; did:6265ca40780b1c0d; eid:lp1)`

There is one exception: for [`/<version>/contents_authorization_token_for_aauth/issue`](#post-versioncontents_authorization_token_for_aauthissue), the [dauth user agent](DAuth-Server) is used instead.

## Methods
The API version is `v1` up to system version 19.0.1 and `v2` in system version 20.0.0 and later. Only the tigers server uses `v1` on all system versions.

https://dragons.hac.lp1.dragons.nintendo.net:

| Method | Path |
| --- | --- |
| POST | [`/<version>/contents_authorization_token/issue`](#post-versioncontents_authorizationissue) |
| POST | [`/<version>/contents_authorization_token_for_aauth/issue`](#post-versioncontents_authorization_token_for_aauthissue) |
| PUT | [`/<version>/debug/migration/state`](#put-versiondebugmigrationstate) |
| POST | [`/<version>/debug/rights/lending/extend`](#post-versiondebugrightslendingextend) |
| POST | [`/<version>/elicense_archives/publish`](#post-versionelicense_archivespublish) |
| PUT | [`/<version>/elicense_archives/<id>/report`](#put-versionelicense_archivesidreport) |
| POST | [`/<version>/elicense_archives/publish`](#post-versionelicense_archivespublish) |
| POST | [`/<version>/elicenses/exercise`](#post-versionelicensesexercise) |
| PUT | [`/<version>/elicenses/extend`](#put-versionelicensesextend) |
| GET | [`/<version>/elicenses/inactivated_reason`](#get-versionelicensesinactivated_reason) |
| GET | [`/<version>/elicenses/migration_state`](#get-versionelicensesmigration_state) |
| POST | [`/<version>/elicenses/prune`](#post-versionelicensesprune) |
| POST | [`/<version>/elicenses/report`](#post-versionelicensesreport) |
| POST | [`/<version>/elicenses/revoke`](#post-versionelicensesrevoke) |
| POST | [`/<version>/elicenses/revoke_all`](#post-versionelicensesrevoke_all) |
| POST | [`/<version>/migration/migrate_device_linked_elicenses`](#post-versionmigrationmigrate_device_linked_elicenses) |
| PUT | [`/<version>/migration/migrate_to_terminated`](#put-versionmigrationmigrate_to_terminated) |
| POST | [`/<version>/migration/revoke_device_linked_elicenses`](#post-versionmigrationrevoke_device_linked_elicenses) |
| PUT | [`/<version>/notification_token`](#post-versionnotification_token) |
| PUT | [`/<version>/penne_id`](#post-versionpenne_id) |
| POST | [`/<version>/rights/available_elicenses`](#post-versionrightsavailable_elicenses) |
| POST | [`/<version>/rights/lending/confirm`](#post-versionrightslendingconfirm) |
| POST | [`/<version>/rights/lending/reserve`](#post-versionrightslendingreserve) |
| POST | [`/<version>/rights/lending/retrieve`](#post-versionrightslendingretrieve) |
| POST | [`/<version>/rights/lending/return`](#post-versionrightslendingreturn) |
| POST | [`/<version>/rights/lending/revoke`](#post-versionrightslendingrevoke) |
| POST | [`/<version>/rights/lending/revoke_reservations`](#post-versionrightslendingrevoke_reservations) |
| POST | [`/<version>/rights/publish_device_linked_elicenses`](#post-versionrightspublish_device_linked_elicenses) |
| POST | [`/<version>/rights/publish_elicenses`](#post-versionrightspublish_elicenses) |
| POST | [`/<version>/signing_key_for_pruning_elicenses/issue`](#post-versionsigning_key_for_pruning_elicenses) |

https://dragonst.hac.lp1.dragons.nintendo.net:

| Method | URL |
| --- | --- |
| POST | [`/<version>/debug/edge_token/issue`](#post-versiondebugedge_tokenissue) |
| PUT | [`/<version>/debug/migration/state`](#put-versiondebugmigrationstate) |
| POST | [`/<version>/debug/rights/lending/extend`](#post-versiondebugrightslendingextend) |
| POST | [`/<version>/edge_token/issuable_titles`](#post-versionedge_tokenissuable_titles) |
| POST | [`/<version>/edge_token/issue`](#post-versionedge_tokenissue) |

https://tigers.hac.lp1.dragons.nintendo.net:

| Method | URL |
| --- | --- |
| POST | [`/v1/etickets/publish`](#post-v1eticketspublish) |

## POST /&lt;version>/contents_authorization/issue
| Field | Description |
| --- | --- |
| nonce | Nonce |
| elicenses | List of elicenses |

## POST /&lt;version>/contents_authorization_token_for_aauth/issue
**This method was added in system version 15.0.0.**

Starting with system version 15.0.0, a contents authorization token is required for digital [application authentication](AAuth-Server). This method returns such a token.

Note that the Switch sends the [headers](#headers) for this method in a different order and uses a different [user agent](#user-agents).

| Field | Description |
| --- | --- |
| elicense_id | E-license id (32 hex digits) |
| na_id | Nintendo account id (16 hex digits) |

Response on success:

| Field | Description |
| --- | --- |
| contents_authorization_token | The token |

Example:

```
POST /v1/contents_authorization_token_for_aauth/issue HTTP/1.1
Host: dragons.hac.lp1.dragons.nintendo.net
User-Agent: libcurl (nnDauth; 16f4553f-9eee-4e39-9b61-59bc7c99b7c8; SDK 15.3.0.0)
Accept: */*
Content-Type: application/json
DeviceAuthorization: Bearer eyJqa3UiOiJodHRwczovL2RjZXJ0LWxwMS5uZGFzLnNydi5uaW50ZW5kby5uZXQva2V5cyIsImtpZCI6ImNhOTdhNTIwLTA2NWItNGEwZC1iOGU4LTlhYzQ5OWFlNjkzZCIsInR5cCI6IkpXVCIsImFsZyI6IlJTMjU2In0.eyJzdWIiOiI2MjY1OTY2MWUzZmRmZTExIiwiaXNzIjoiZGF1dGgtbHAxLm5kYXMuc3J2Lm5pbnRlbmRvLm5ldCIsImF1ZCI6ImQ1YjZjYWMyYzE1MTRjNTYiLCJleHAiOjE2NjczMzQ4NjMsImlhdCI6MTY2NzI0ODQ2MywianRpIjoiYjMyYmIzYzYtMjQwNy00NGUzLWIwZjUtYjkzODljMGJmODNmIiwibmludGVuZG8iOnsic24iOiJYQUo3MDEyMzQ1Njc4OSIsInBjIjoiSEFDIiwiZHQiOiJOWCBQcm9kIDEiLCJpc3QiOmZhbHNlfX0.j7Iah1gCA1N5jnAOQnUFgowK3VlrjJi3wxzvM_F6KJLK23nYYNqg0Nn-pATZZ-yV7KJWkuyD07anxWErcYI47nsV4L_sYHvsnw_gXTwD7hlc02_VO1MEnG_CDUsVgrLhDFasQJgcya4vLDgPZpuf-VnpX_H9ZM8JYDusT0uCrv9x_5Ad_o6mpHZK9R56BJ6AoSV0JrRP7cJv2X-cYlDQCnat6CKZxxmNrd5_IrfP8dUBWI4w3wFsJWA2euOQr8pwn2hwG666VU_u4r-PUti8mzbLGFjI9dkvaSKkVwECL_27Xpqw5KxP70z3NhIFmguFo8AwzFLDR0Zvpt3y_tajiQ
Nintendo-Application-Id: 010040600c5ce000
Content-Length: 77

{"elicense_id":"337c8aaef372df9c2c239ebaaf49f723","na_id":"72b0f0bdb31753d5"}
```

```
HTTP/1.1 200 OK
Content-Type: application/json;charset=UTF-8
Content-Length: 951
Server: nginx
X-Content-Type-Options: nosniff
Expires: Mon, 31 Oct 2022 19:34:39 GMT
Cache-Control: max-age=0, no-cache, no-store
Pragma: no-cache
Date: Mon, 17 Oct 2022 08:31:43 GMT
x-nintendo-akamai-reference-id: 0.38ac1666.1667248479.7ecea70
Connection: keep-alive

{"contents_authorization_token":"eyJqa3UiOiJodHRwczpcL1wvcHVia2V5LmxwMS5kcmFnb25zLm5pbnRlbmRvLm5ldFwvY2F0YVwvdjFcL2p3a3MiLCJraWQiOiI2YzI2MjRkOC0zMGQ0LTRlYjgtYWJjOC0wNmZiODMzYzhjNGIiLCJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiJ9.eyJhdWQiOiIwMTAwNDA2MDBjNWNlMDAwIiwiZGV2aWNlX2lkIjoiNjI2NTk2NjFlM2ZkZmUxMSIsImlzcyI6ImxwMS5kcmFnb25zLm5pbnRlbmRvLm5ldCIsImV4cCI6MTY2NzMzNDg3OSwiaWF0IjoxNjY3MjQ4NDc5LCJqdGkiOiI0ZGYyZTY1Ni04ZTk2LTQwOWEtOGE3ZS1iZDFkZDFiYmM1NzIiLCJjb250ZW50Ijp7InRpdGxlX2lkIjoiMDEwMDQwNjAwYzVjZTAwMCIsIm5hX2lkIjoiNzJiMGYwYmRiMzE3NTNkNSIsInRpY2tldF9pZCI6NzIyMTI4OTQzNDk2MDQ5MzksImlzX293bmVkX3JpZ2h0cyI6dHJ1ZX19.MqMnkyEWuVp9TOtbpPhRJGcHRd-fCK_8rGa7rO0HeiC6pkIn7qafBzpc-TD1Xf_DYN_C0m9OXjlX0rVs0vosIzXsoqVDQodB6XAteRWfDNUc6odpW-rgqOiNpbIBymcpbRYOsdJh41zQjl_hpdM44UOR6ZgvL1hKoQVaw7XVz5NANig-WlKyNDVCcSsWhycyBuRkZOPb9OblTbvRkIzluRTFG9lxHCDnwczxGiaLoZjEgUrqIcWQJBUyOxB2UiL5sitK53GsHhFHxVZqTwjM7wl7nzrQaVDsp_Zc26hkIrUeuvDTBZHWXNPrte-nja5CZ-lN-UNIwe2j9N61baD9YQ"}
```

## POST /&lt;version>/debug/edge_token/issue
| Field | Description |
| --- | --- |
| title_ids | List of title ids |
| na_id_tokens | List of Nintendo account id tokens |
| vendor | Vendor | `akamai`, `lumen`, `llnw`, `fastly` or `cloudflare` |

Response on success:

| Field | Description |
| --- | --- |
| expires_in | Expiration in seconds (21600) |
| dragons_edge_token | Edge token |
| title_ids | List of title ids |

## PUT /&lt;version>/debug/migration/state
| Field | Description |
| --- | --- |
| state | State |

## POST /&lt;version>/debug/rights/lending/extend
| Field | Description |
| --- | --- |
| owner_na_id | Owner Nintendo account id (16 hex digits) |
| rights_ids | List of rights ids (16 hex digits each) |
| expire_date | Expiration date (optional) |

The server sends an empty response on success.

## POST /&lt;version>/edge_token/issuable_titles
| Field | Description |
| --- | --- |
| title_ids | List of rights ids |
| application_ids | List of title ids |
| na_id_tokens | List of Nintendo account id tokens |

## POST /&lt;version>/edge_token/issue
| Field | Description |
| --- | --- |
| title_ids | List of title ids |
| na_id_tokens | List of Nintendo account id tokens |
| vendor | Vendor | `akamai`, `lumen`, `llnw`, `fastly` or `cloudflare` |

## PUT /&lt;version>/elicense_archives/&lt;id>/report
The id must contain 32 hex digits.

## POST /&lt;version>/elicense_archives/publish
| Field | Description |
| --- | --- |
| challenge | Challenge (16 hex digits) |
| certificate | Device certificate (base64) |

Response on success:

| Field | Description |
| --- | --- |
| elicense_archive | E-license archive (base64) |

## POST /&lt;version>/elicenses/exercise
| Field | Description |
| --- | --- |
| elicense_ids | E-license ids |
| account_ids | Account ids |

The server sends an empty response on success.

## PUT /&lt;version>/elicenses/extend
| Field | Description |
| --- | --- |
| elicense_ids | E-license ids |

## GET /&lt;version>/elicenses/inactivated_reason
| Param | Description |
| --- | --- |
| elicense_ids | E-license ids |

Response on success:

| Field | Description |
| --- | --- |
| inactivated_reasons | Inactivated reasons |

## GET /&lt;version>/elicenses/migration_state
This method takes no parameters.

## POST &lt;version>/elicenses/prune
| Field | Description |
| --- | --- |
| exclude_account_ids | List of account ids to exclude |
| signature | Signature |

## POST /&lt;version>/elicenses/report
| Field | Description |
| --- | --- |
| elicense_ids | E-license ids |
| account_ids | Account ids |

## POST /&lt;version>/elicenses/revoke
| Field | Description |
| --- | --- |
| elicense_ids | E-license ids |

The server sends an empty response on success.

## POST /&lt;version>/elicenses/revoke_all
This method takes no arguments.

The server sends an empty response on success.

## POST /&lt;version>migration/migrate_device_linked_elicenses
This method takes no arguments.

## PUT /&lt;version>migration/migrate_to_terminated
This method takes no arguments.

## POST /&lt;version>migration/revoke_device_linked_elicenses
This method takes no arguments.

## POST /&lt;version>/notification_token
| Field | Description |
| --- | --- |
| notification_token | 36 characters |

The server sends an empty response on success.

## POST /&lt;version>/penne_id
| Field | Description |
| --- | --- |
| penne_id | A 'p' followed by 32 characters |

The server sends an empty response on success.

## POST /&lt;version>/rights/available_elicenses
| Field | Description |
| --- | --- |
| rights_ids | List of rights ids (16 hex digits each) |

Response on success:

| Field | Description |
| --- | --- |
| available_elicenses | List of elicenses |

Each entry contains the following fields:

| Field | Description |
| --- | --- |
| rights_id | The rights id |
| is_available | Boolean |
| reason | `no_rights`, `not_device_linked`, `not_released`, `expired`, `used_by_another`, `requested_by_client`, `device_link_unknown`, `requires_online_subscription`, `requires_online_subscription_ex`, `online_subscription_unknown`, `not_device_registered`, `device_registration_unknown`, `offline_initialization_recovery`, `requested_by_offdevice`, `revoked_by_cs`, `lending_rights`, `borrowing_requirements_not_met`, `retrieved_by_owner`, `limit_exceeded` or `revoked_by_leaving_family` |
| elicense_type | `temporary`, `permanent`, `device_linked_permanent`, `promotion`, `sapico`, `v_permanent` or `v_sharable_temporary` |

## POST /&lt;version>/rights/lending/confirm
| Field | Description |
| --- | --- |
| owner_na_id | Owner Nintendo account id |
| rights_ids | List of rights ids |

## POST /&lt;version>/rights/lending/reserve
| Field | Description |
| --- | --- |
| borrower_na_id | Borrower Nintendo account id |
| rights_ids | List of rights ids |

## POST /&lt;version>/rights/lending/retrieve
| Field | Description |
| --- | --- |
| rights_ids | List of rights ids |

## POST /&lt;version>/rights/lending/return
| Field | Description |
| --- | --- |
| owner_na_id | Onwer Nintendo account id |
| rights_ids | List of rights ids |

## POST /&lt;version>/rights/lending/revoke
| Field | Description |
| --- | --- |
| owner_na_id | Onwer Nintendo account id |
| rights_ids | List of rights ids |

The server sends an empty response on success.

## POST /&lt;version>/rights/lending/revoke_reservations
| Field | Description |
| --- | --- |
| rights_ids | List of rights ids |

The server sends an empty response on success.

## POST /&lt;version>/rights/publish_device_linked_elicenses
This method takes no arguments.

Response on success:

| Field | Description |
| --- | --- |
| elicenses | List of e-licenses |

Each entry has the following fields:

| Field | Description |
| --- | --- |
| account_id | Nintendo account id |
| rights_id | Rights id |
| device_id | Device id |
| status | Status (e.g. `active`) |
| elicense_id | E-license id (32 hex digits) |
| elicense_type | `temporary`, `permanent`, `device_linked_permanent`, `promotion`, `sapico`, `v_permanent` or `v_sharable_temporary` |

## POST /&lt;version>/rights/publish_elicenses
| Field | Description |
| --- | --- |
| rights_ids | List of rights ids |
| elicense_type | E-license type |

## POST /&lt;version>/signing_key_for_pruning_elicenses
| Field | Description |
| --- | --- |
| certificate | Device certificate (base64 encoded) |

## POST /v1/etickets/publish
| Field | Description |
| --- | --- |
| certificate | Device certificate (base64 encoded) |
| titles | List of titles |

## Errors
On error, the server sends the following response:

| Field | Description |
| --- | --- |
| type | `https://problems.dragons.nintendo.net/errors/v1/<status>/<code>` |
| title | Error title |
| detail | Error details. This field is an empty string in all errors that have been observed so far. |
| number | HTTP status code |

If the error code is `invalid_parameter`, the response may contain more details under the `invalid-params` key, for example:

* `'invalid-params': [{'name': 'naId', 'reason': 'must not be null'}]`
* `'invalid-params': [{'name': 'naId.accountId', 'reason': 'must match "\\p{XDigit}{16}"'}]`

### Known Errors
| Status | Code | Title |
| --- | --- | --- |
| 400 | `duplicate_rights_id` | |
| 400 | `exceed_upper_lending_limit` | |
| 400 | `invalid_account_for_borrowing` | |
| 400 | `invalid_device_certificate` | Device certificate is invalid |
| 400 | `invalid_device_for_lending` | |
| 400 | `invalid_eticket_template` | |
| 400 | `invalid_lending_state` | Lending state is invalid |
| 400 | `invalid_parameter` | Parameter is invalid |
| 400 | `license_active_on_lender_device` | |
| 400 | `rights_has_already_lent` | |
| 401 | `account_id_required` | Account ID is required |
| 401 | `authentication_required` | Authentication is required |
| 403 | `edge_token_not_grantable` | |
| 403 | `invalid_rights_for_lending` | |
| 403 | `invalid_migration_state` | |
| 403 | `invalid_token` | Token is invalid |
| 403 | `license_archive_not_allowed` | |
| 403 | `license_inactive` | ELicense is inactive |
| 403 | `license_not_grantable` | |
| 403 | `rights_policy_not_allowed` | |
| 403 | `system_update_required` | |
| 404 | `license_archive_not_found` | ELicense archive is not found |
| 404 | `license_not_found` | ELicense is not found |
| 404 | `page_not_found` | Page not found |
| 404 | `promotion_policy_not_found` | |
| 404 | `title_not_found` | |
| 405 | `method_not_allowed` | Method not allowed |
| 406 | `not_acceptable` | |
| 415 | `unsupported_media_type` | |
| 500 | `delete_record_failed` | |
| 500 | `insert_record_failed` | |
| 500 | `op2_error` | |
| 500 | `shogun_error` | |
| 500 | `unexpected_error` | |
| 500 | `unknown_issuer` | |
| 500 | `update_record_failed` | |
| 503 | `abort_retry` | |
| 503 | `op2_maintenance` | |
| 503 | `service_unavailable` | |