[[Server List]] > Online Save Storage
---

The SCSI servers are for account migration. The SATA servers are for repairing save data.

### Storage servers
https://storage.lp1.scsi.srv.nintendo.net<br>
https://storage.lp1.sata.srv.nintendo.net

| URL |
| --- |
| `/api/nx/v1/component_files/<id>/finish_upload` |
| `/api/nx/v1/component_files/<id>/signed_uri` |
| `/api/nx/v1/component_files/<id>/update` |
| `/api/nx/v1/network_service_accounts/<id>/notification_tokens` |
| `/api/nx/v1/save_data_archives/` |
| `/api/nx/v1/save_data_archives/<id>` |
| `/api/nx/v1/save_data_archives/<id>/component_files/create` |
| `/api/nx/v1/save_data_archives/<id>/delete` |
| `/api/nx/v1/save_data_archives/<id>/extend_upload_timeout` |
| `/api/nx/v1/save_data_archives/<id>/finish_download` |
| `/api/nx/v1/save_data_archives/<id>/finish_upload` |
| `/api/nx/v1/save_data_archives/<id>/generate_key_seed_package` |
| `/api/nx/v1/save_data_archives/<id>/start_download` |
| `/api/nx/v1/save_data_archives/<id>/start_upload` |
| `/api/nx/v1/save_data_archives/start_upload` |

| URL |
| --- |
| `/api/nx/v2/component_files/<id>/finish_upload` |
| `/api/nx/v2/component_files/<id>/signed_uri` |
| `/api/nx/v2/component_files/<id>/update` |
| `/api/nx/v2/network_service_accounts/<id>/notification_tokens` |
| `/api/nx/v2/permissions` |
| `/api/nx/v2/save_data_archives/` |
| `/api/nx/v2/save_data_archives/<id>` |
| `/api/nx/v2/save_data_archives/<id>/component_files/create` |
| `/api/nx/v2/save_data_archives/<id>/delete` |
| `/api/nx/v2/save_data_archives/<id>/extend_upload_timeout` |
| `/api/nx/v2/save_data_archives/<id>/finish_download` |
| `/api/nx/v2/save_data_archives/<id>/finish_upload` |
| `/api/nx/v2/save_data_archives/<id>/generate_key_seed_package` |
| `/api/nx/v2/save_data_archives/<id>/start_download` |
| `/api/nx/v2/save_data_archives/<id>/start_upload` |
| `/api/nx/v2/save_data_archives/start_upload` |

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

| URL |
| --- |
| `/api/nx/v1/application_policy/<id>/<id>` |
| `/api/nx/v1/save_data_migration_policy/<id>/<id>` |

### SCSI migration server
https://migration.lp1.scsi.srv.nintendo.net

| URL |
| --- |
| `/api/nx/v1/save_data_migrations/gen_key` |
| `/api/nx/v1/save_data_migrations/get_key` |
| `/api/nx/v1/account_migrations/gen_key` |
| `/api/nx/v1/account_migrations/get_key` |