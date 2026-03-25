[[Server List]] > Online Save Storage
---

The SCSI servers are for account migration. The SATA servers are for repairing save data.

### Storage servers
https://storage.lp1.scsi.srv.nintendo.net

| Method | URL |
| --- | --- |
| ? | `/api/nx/v2/component_files/<id>/finish_upload` |
| ? | `/api/nx/v2/component_files/<id>/signed_uri` |
| ? | `/api/nx/v2/component_files/<id>/update` |
| POST | [`/api/nx/v2/network_service_accounts/<id>/notification_tokens`](#post-apinxv2network_service_accountsidnotification_tokens) |
| ? | `/api/nx/v2/permissions` |
| GET | [`/api/nx/v2/save_data_archives`](#get-apinxv2save_data_archives) |
| GET | [`/api/nx/v2/save_data_archives/<id>`](#get-apinxv2save_data_archivesid) |
| ? | `/api/nx/v2/save_data_archives/<id>/component_files/create` |
| ? | `/api/nx/v2/save_data_archives/<id>/delete` |
| POST | [`/api/nx/v2/save_data_archives/<id>/extend_upload_timeout`](#post-apinxv2save_data_archivesidextend_upload_timeout) |
| ? | `/api/nx/v2/save_data_archives/<id>/finish_download` |
| POST | [`/api/nx/v2/save_data_archives/<id>/finish_upload`](#post-apinxv2save_data_archivesidfinish_upload) |
| POST | [`/api/nx/v2/save_data_archives/<id>/generate_key_seed_package`](#post-apinxv2save_data_archivesidgenerate_key_seed_package) |
| ? | `/api/nx/v2/save_data_archives/<id>/start_download` |
| POST | [`/api/nx/v2/save_data_archives/<id>/start_upload`](#post-apinxv2save_data_archivesidstart_upload) |
| ? | `/api/nx/v2/save_data_archives/start_upload` |

### SATA permission server
https://permission.lp1.sata.srv.nintendo.net

| URL |
| --- |
| `/api/nx/v1/customer_operations` |
| `/api/nx/v1/customer_operations/update_action_completed` |
| `/api/nx/v1/save_data_sets` |
| `/api/nx/v1/save_data_sets/generate_key_package` |

### SATA privacy policy
https://pp.lp1.sata.srv.nintendo.net

This server redirects to Nintendo's privacy policy page in various languages.

| URL |
| --- |
| `/noa/en_US.html` |
| `/noa/es_LA.html` |
| `/noa/fr_CA.html` |
| `/noa/pt_BR.html` |
| `/noe/de_DE.html` |
| `/noe/en_GB.html` |
| `/noe/es_ES.html` |
| `/noe/fr_FR.html` |
| `/noe/it_IT.html` |
| `/noe/nl_NL.html` |
| `/noe/pt_PT.html` |
| `/noe/ru_RU.html` |

### SCSI policy server
https://scsi-policy-lp1.cdn.nintendo.net

| Method | URL |
| --- | --- |
| GET | [`/api/nx/v1/application_policy/<id>/<version>`](#get-apinxv1application_policyidversion) |
| GET | `/api/nx/v2/application_policy/<id>/<version>` |
| ? | `/api/nx/v1/save_data_migration_policy/<id>/<id>` |

### SCSI migration server
https://migration.lp1.scsi.srv.nintendo.net

| URL |
| --- |
| `/api/nx/v1/save_data_migrations/gen_key` |
| `/api/nx/v1/save_data_migrations/get_key` |
| `/api/nx/v1/account_migrations/gen_key` |
| `/api/nx/v1/account_migrations/get_key` |

## POST /api/nx/v2/network_service_accounts/&lt;id&gt;notification_tokens
| Field | Description |
| --- | --- |
| notification_token | 36 hex digits |

Response on success:

| Field | Description |
| --- | --- |
| notification_token | 36 hex digits |

## GET /api/nx/v2/save_data_archives
| Param | Description |
| --- | --- |
| datatype | Unknown |
| device_id | Device id filter (optional, may be set to `me`) |
| application_id | Application id filter |

Response on success:

| Field | Description |
| --- | --- |
| save_data_archives | List of save data archives |

## GET /api/nx/v2/save_data_archives
| Param | Description |
| --- | --- |
| datatype | Unknown |
| device_id | Device id filter (optional, may be set to `me`) |
| application_id | Application id filter |

Response on success:

| Field | Description |
| --- | --- |
| save_data_archive | List of [save data archives](#save-data-archive) |

## GET /api/nx/v2/save_data_archives/&lt;id>
Response on success:

| Field | Description |
| --- | --- |
| save_data_archive | The [save data archive](#save-data-archive) |

## POST /api/nx/v2/save_data_archives/&lt;id>/extend_upload_timeout
Response on success:

| Field | Description |
| --- | --- |
| code | `2000` |

## POST /api/nx/v2/save_data_archives/&lt;id>/finish_upload
| Field | Description |
| --- | --- |
| encoded_mac | 16 base64url encoded bytes without padding |

Response on success:

| Field | Description |
| --- | --- |
| save_data_archive | The [save data archive](#save-data-archive) |

## POST /api/nx/v2/save_data_archives/&lt;id>/generate_key_seed_package
| Field | Description |
| --- | --- |
| encoded_challenge | 16 base64url encoded bytes without padding |

Response on success:

| Field | Description |
| --- | --- |
| encoded_key_seed_package | 512 base64url encoded bytes |

## POST /api/nx/v2/save_data_archives/&lt;id>/start_upload
| Field | Description |
| --- | --- |
| datatype | Data type (integer) |
| data_size | Size in bytes |
| saved_at_as_unixtime | Timestamp |
| launch_required_version | Integer |
| series_id | Integer |
| encoded_digest | Unknown base64url encoded 32 bytes |
| has_thumbnail | Boolean |
| desc | Description (may be null) |
| auto_backup | Boolean |

Response on success:

| Field | Description |
| --- | --- |
| save_data_archive | The [save data archive](#save-data-archive) |

## GET /api/nx/v1/application_policy/&lt;id&gt;/&lt;version&gt;
Returns the policy type for a given title id and version.

| Param | Description |
| --- | --- |
| dtoken | [Edge token](DAuth-Server) |

Response on success:

| Field | Description |
| --- | --- |
| policy_type | `ALL_OK` or `ALL_NG` |

## Save Data Archive
A save data archive contains the following fields. The component_files field is only included when a specific save data archive is requested, and not when save data archives are listed.

| Field | Description |
| --- | --- |
| id | Save data archive id |
| nsa_id | [BaaS](BAAS-Server) user id |
| application_id | Title id (16 hex digits) |
| device_id | Device id |
| device_serial | Device serial number |
| data_size | Size in bytes |
| desc | Description (may be null) |
| series_id | Unknown (integer) |
| datatype | Unknown (integer) |
| status | `fixed` or `uploading` |
| auto_backup | Boolean |
| num_of_partitions | Number of partitions (integer) |
| launch_required_version | Required title version |
| previous_save_data_archive_id | Previous save data archive id (may be null) |
| encoded_digest | Unknown base64url encoded 32 bytes |
| saved_at_as_unixtime | Timestamp |
| finished_at_as_unixtime | Timestamp |
| component_files | List of component files |

A component file object has the following fields:

| Field | Description |
| --- | --- |
| id | Component file id |
| index | Index |
| datatype | `meta` or `save` |
| status | `fixed` or `uploading` |
| archive_size | Archive size in bytes |
| encoded_archive_digest | 16 base64url encoded bytes |