An error code contains a module id and a module-specific code, separated by a dash. For example: `2306-0502`.

The following module ids are currently known:

| Code | Name | Description |
| --- | --- | --- |
| 2001 | `svc` | Supervisor calls (syscalls) |
| 2002 | `fs` | Filesystem |
| 2003 | `os` | Operating system |
| 2004 | `htcs` | Host target connection services |
| 2005 | `ncm` | Nintendo content manager |
| 2006 | `dd` | Device address space |
| 2007 | `osdbg` | OS debugging |
| 2008 | `lr` | Location resolver |
| 2009 | `ldr` | Loader services |
| 2010 | `sf` | Service framework |
| 2011 | `sf::hipc` | Service framework (IPC) |
| 2012 | `tma` | Target manager agent |
| 2013 | `dmnt` | Debug monitor |
| 2014 | `gds` | ? |
| 2015 | `pm` | Process manager |
| 2016 | `ns` | Nintendo shell services |
| 2017 | `bsdsocket` | Berkeley sockets |
| 2018 | `htc` | Host target connections |
| 2019 | `tsc` | ? |
| 2020 | `kvdb` | Key-value database |
| 2021 | `sm` | Service manager |
| 2022 | `ro` | Loader symbol registration |
| 2023 | `gc` | ? |
| 2024 | `sdmmc` | MMC storage |
| 2025 | `ovln` | Overlay notifications |
| 2026 | `spl` | Secure platform services |
| 2027 | `socket` | Socket API |
| 2028 | `dt` | Device tree |
| 2029 | `htclow` | Host target connections (low level) |
| 2030 | `ddsf` | Device driver service framework |
| 2031 | `htcfs` | Host target connections (filesystem) |
| 2032 | `async` | Asynchronous tasks |
| 2033 | `util` | Utilities |
| 2035 | `tipc` | Tiny IPC |
| 2037 | `anif` | ? |
| 2100 | `eth` | Ethernet |
| 2101 | `i2c` | I2C (hardware communication) |
| 2102 | `gpio` | GPIO (hardware communication) |
| 2103 | `uart` | UART (hardware communication) |
| 2104 | `cpad` | Classic controller |
| 2105 | `settings` | System settings |
| 2106 | `ftm` | Touchscreen |
| 2107 | `wlan` | WLAN |
| 2108 | `xcd` | NX controller driver |
| 2109 | `tmp451` | Temperature sensor |
| 2110 | `nifm` | Network interface manager (internet connection) |
| 2111 | `codec` | Audio decoding |
| 2112 | `lsm6ds3` | Accelerometer / gyroscope |
| 2113 | `bluetooth` | Bluetooth |
| 2114 | `vi` | Video display |
| 2115 | `nfp` | Amiibo |
| 2116 | `time` | Time services |
| 2117 | `fgm` | Frequency governer module |
| 2118 | `oe` | Operating environment (battery, performance, etc.) |
| 2119 | `bh1730fvc` | Light sensor |
| 2120 | `pcie` | PCIe (hardware communication) |
| 2121 | `friends` | Friends |
| 2122 | `bcat` | Background content delivery (used for news and game data) |
| 2123 | `ssl` | [SSL / TLS](#ssl-error-codes) |
| 2124 | `account` | [Account services](#account-error-codes) |
| 2125 | `news` | News |
| 2126 | `mii` | Miis |
| 2127 | `nfc` | Near-field communication |
| 2128 | `am` | Applet manager |
| 2129 | `prepo` | Play reports (telemetry) |
| 2130 | `ahid` | ? |
| 2131 | `applet` | Applets |
| 2132 | `ae` | Applet environment |
| 2133 | `pcv` | Power control / voltage services |
| 2134 | `usb::pd` | USB power delivery |
| 2135 | `bpc` | Board power control |
| 2136 | `psm` | Power management |
| 2137 | `nim` | [Network installation manager](#nim-error-codes) |
| 2138 | `psc` | Power state control |
| 2139 | `tc` | Thermal coordinator |
| 2140 | `usb` | USB |
| 2141 | `nsd` | Network service discovery |
| 2142 | `pctl` | Parental controls |
| 2143 | `btm` | Bluetooth manager |
| 2144 | `la` | Library applets |
| 2145 | `es` | E-ticket services |
| 2146 | `ngc` | Profanity checks |
| 2147 | `erpt` | Error report generation |
| 2148 | `apm` | Applet profile manager |
| 2149 | `cec` | CEC (HDMI) |
| 2150 | `profiler` | CPU profiler |
| 2151 | `eupld` | Error report uploads |
| 2152 | `libde` | Icon downloads |
| 2153 | `audio` | Audio |
| 2154 | `npns` | Nintendo push notification service |
| 2155 | `http` | [HTTP requests (curl)](#http-error-codes) |
| 2156 | `idle` | Auto-sleep |
| 2157 | `arp` | Application registry |
| 2158 | `updater` | Updater |
| 2159 | `swkbd` | Software keyboard |
| 2160 | `netdiag` | Network diagnostics |
| 2161 | `nfc::mifare` | Mifare |
| 2162 | `err` | Errors |
| 2163 | `fatal` | Fatal errors |
| 2164 | `ec` | E-commerce services |
| 2165 | `spsm` | Power state |
| 2166 | `aoc` | Add-on content |
| 2167 | `bgtc` | Background tasks |
| 2168 | `creport` | Crash reports |
| 2169 | `sasbus` | SAS bus |
| 2170 | `pl` | Platform services |
| 2171 | `cdmsc` | USB mass storage |
| 2172 | `audioctrl` | Audio control |
| 2173 | `lbl` | Backlight control |
| 2175 | `jit` | JIT compilation |
| 2176 | `hdcp` | HDCP |
| 2177 | `omm` | Operation mode manager |
| 2178 | `pdm` | Play statistics database |
| 2179 | `olsc` | Online save storage |
| 2180 | `srepo` | System reports |
| 2181 | `dauth` | [Device authentication](#dauth-error-codes)|
| 2182 | `stdfu` | ? |
| 2183 | `dbg` | Debugging |
| 2184 | `cdacm` | USB ACM |
| 2185 | `tcap` | Thermal coordinator advanced policy |
| 2186 | `dhcps` | DHCP services |
| 2187 | `spi` | SPI |
| 2188 | `avm` | Application version manager |
| 2189 | `pwm` | PWM bus |
| 2190 | `dnsserver` | DNS server |
| 2191 | `rtc` | Real time clock |
| 2192 | `regulator` | Regulator |
| 2193 | `led` | LED |
| 2194 | `htctool` | Host target connection tool |
| 2195 | `sio` | Lite controller |
| 2196 | `pcm` | Power / voltage reader |
| 2197 | `clkrst` | Clock resets |
| 2198 | `powctl` | Power controller |
| 2199 | `hiddriver` | HID driver |
| 2200 | `dma` | Direct memory access |
| 2202 | `hid` | Humand interface device |
| 2203 | `ldn` | Local device network |
| 2204 | `cs` | ? |
| 2205 | `irsensor` | IR sensor |
| 2206 | `capsrv` | Screenshots |
| 2207 | `mm` | ? |
| 2208 | `manu` | Manufacturing services |
| 2209 | `atk` | Audio toolkit (NintendoWare) |
| 2210 | `web` | Web browser |
| 2211 | `lcs` | Local content share |
| 2212 | `grc` | Game recording |
| 2213 | `repair` | Repair |
| 2214 | `album` | Album |
| 2215 | `rid` | Demo |
| 2216 | `migration` | User migration |
| 2217 | `migration::idc` | User migration (IDC) |
| 2218 | `hidbus` | HID bus |
| 2219 | `ens` | Extended network services (game-specific HTTP services) |
| 2220 | `nd` | Neighbour detection |
| 2221 | `ndd` | Neighbour device protocol |
| 2222 | `toycon` | Toycon |
| 2223 | `websocket` | Websockets |
| 2224 | `socketio` | Socket I/O |
| 2306 | `nex` | [Game servers (old)](#nex-error-codes)<br>[Error descriptions](#nex-error-descriptions) |
| 2307 | | Voice chat |
| 2308 | | Item catalog |
| 2309 | | Consumable service management |
| 2318 | `pia` | [Peer to peer (new)](#pia-error-codes-new) |
| 2321 | `npln` | Game servers (new) |
| 2522 | | Crash reporting tool |
| 2618 | `pia` | [Peer to peer (old)](#pia-error-codes-old) |
| 2621 | | Mandom (subscription management) |
| 2622 | | Sugar (consumable service management) |
| 2623 | `eagle` | [Relay servers](#eagle-error-codes) |
| 2800 | | Web applet (application) |
| 2801 | | Post album |
| 2802 | | View album |
| 2807 | | Web applet (news) |
| 2808 | | Web applet (offline) |
| 2811 | | EC applet |
| 2813 | | Nintendo eShop |
| 2814 | | Internet settings |
| 2815 | `coral` | [Voice chat](#coral-error-codes) |
| 2818 | | Voice chat |
| 2819 | | Application rights |
| 2820 | | Nintendo eShop (local) |
| 2821 | | NSO applet |

# SSL Error Codes
| Error Codes | Description |
| --- | --- |
| 0000 - 0199 | [General errors](#ssl-errors-general) |
| 0200 - 0299 | [PR errors](#ssl-errors-pr) |
| 0300 - 0399 | [SSL errors](#ssl-errors-ssl) |
| 1500 - 1599 | [SSL alert errors](#ssl-errors-ssl-alert) |

## SSL Errors (General)
| Error Code | Description |
| --- | --- |
| 2123-0011 | An I/O error has occurred |
| 2123-0013 | An unexpected error has occurred |
| 2123-0102 | Some kind of resource was exhausted (e.g. out of memory) |
| 2123-0116 | Invalid file descriptor |

## SSL Errors (PR)
| Error Code | Description |
| --- | --- |
| 2123-0204 | `PR_WOULD_BLOCK_ERROR` |
| 2123-0205 | `PR_IO_TIMEOUT_ERROR` |
| 2123-0206 | `PR_OPERATION_ABORTED_ERROR` |
| 2123-0208 | `PR_NOT_CONNECTED_ERROR` |
| 2123-0209 | `PR_CONNECT_RESET_ERROR` |
| 2123-0210 | `PR_CONNECT_ABORTED_ERROR` |
| 2123-0211 | `PR_SOCKET_SHUTDOWN_ERROR` |
| 2123-0212 | `PR_NETWORK_DOWN_ERROR` |

## SSL Errors (SSL)
| Error Code | Description |
| --- | --- |
| 2123-0301 | `SSL_ERROR_BAD_CERT_DOMAIN` |
| 2123-0302 | `SSL_ERROR_NO_CERTIFICATE` |
| 2123-0310 | Received record/message with unknown discriminant. |
| 2123-0311 | Received a malformed (too long or short) SSL handshake. |
| 2123-0312 | Received an SSL handshake that was inappropriate for the state we're in. |
| 2123-0313 | Received an SSL record that was inappropriate for the state we're in. |
| 2123-0314 | `SSL_ERROR_RX_RECORD_TOO_LONG` |
| 2123-0315 | `SSL_ERROR_RX_UNEXPECTED_HELLO_VERIFY_REQUEST` |
| 2123-0316 | `SSL_ERROR_RX_UNEXPECTED_CERT_STATUS` |
| 2123-0317 | `SSL_ERROR_INCORRECT_SIGNATURE_ALGORITHM` |
| 2123-0318 | `SSL_ERROR_WEAK_SERVER_*_KEY` |
| 2123-0319 | `SSL_ERROR_EXPIRED_CERT_ALERT` |
| 2123-0321 | `SSL_ERROR_*_DIGEST_FAILURE` |
| 2123-0322 | `SSL_ERROR_MAC_COMPUTATION_FAILURE` |
| 2123-0330 | `SSL_ERROR_DECOMPRESSION_FAILURE` |

## SSL Errors (SSL Alert)
| Error Code | Description |
| --- | --- |
| 2123-1501 | `SSL_ERROR_CLOSE_NOTIFY_ALERT` |
| 2123-1502 | `SSL_ERROR_HANDSHAKE_UNEXPECTED_ALERT` |
| 2123-1503 | `SSL_ERROR_BAD_MAC_ALERT` |
| 2123-1504 | `SSL_ERROR_DECRYPTION_FAILED_ALERT` |
| 2123-1505 | `SSL_ERROR_RECORD_OVERFLOW_ALERT` |
| 2123-1506 | `SSL_ERROR_DECOMPRESSION_FAILURE_ALERT` |
| 2123-1507 | `SSL_ERROR_HANDSHAKE_FAILURE_ALERT` |
| 2123-1509 | `SSL_ERROR_BAD_CERT_ALERT` |
| 2123-1510 | `SSL_ERROR_UNSUPPORTED_CERT_ALERT` |
| 2123-1511 | `SSL_ERROR_REVOKED_CERT_ALERT` |
| 2123-1512 | `SSL_ERROR_EXPIRED_CERT_ALERT` |
| 2123-1513 | `SSL_ERROR_CERTIFICATE_UNKNOWN_ALERT` |
| 2123-1514 | `SSL_ERROR_ILLEGAL_PARAMETER_ALERT` |
| 2123-1515 | `SSL_ERROR_UNKNOWN_CA_ALERT` |
| 2123-1516 | `SSL_ERROR_ACCESS_DENIED_ALERT` |
| 2123-1517 | `SSL_ERROR_DECODE_ERROR_ALERT` |
| 2123-1518 | `SSL_ERROR_DECRYPT_ERROR_ALERT` |
| 2123-1519 | `SSL_ERROR_EXPORT_RESTRICTION_ALERT` |
| 2123-1520 | `SSL_ERROR_PROTOCOL_VERSION_ALERT` |
| 2123-1521 | `SSL_ERROR_INSUFFICIENT_SECURITY_ALERT` |
| 2123-1522 | `SSL_ERROR_INTERNAL_ERROR_ALERT` |
| 2123-1523 | `SSL_ERROR_INAPPROPRIATE_FALLBACK_ALERT` |
| 2123-1524 | `SSL_ERROR_USER_CANCELED_ALERT` |
| 2123-1525 | `SSL_ERROR_NO_RENEGOTIATION_ALERT` |
| 2123-1526 | `SSL_ERROR_UNSUPPORTED_EXTENSION_ALERT` |
| 2123-1527 | `SSL_ERROR_CERTIFICATE_UNOBTAINABLE_ALERT` |
| 2123-1528 | `SSL_ERROR_UNRECOGNIZED_NAME_ALERT` |
| 2123-1529 | `SSL_ERROR_BAD_CERT_STATUS_RESPONSE_ALERT` |
| 2123-1530 | `SSL_ERROR_BAD_CERT_HASH_VALUE_ALERT` |

# Account Error Codes
These errors are related to account services.

| Error Codes | Description |
| --- | --- |
| 4500 - 4599 | [DAuth (device authentication)](#account-errors-dauth) |
| 4600 - 4799 | [AAuth (application authentication)](#account-errors-aauth) |
| 5000 - 5249 | [BAAS (backend as a service)](#account-errors-baas) |
| 6000 - 6249 | [Account server errors](#account-errors-nas) |
| 7000 - 7499 | [HTTP status errors](#account-errors-http) |
| Other | [Other account errors](#account-errors-general) |

## Account Errors (General)
| Error Code | Description |
| --- | --- |
| 2124-0010 | BaaS or account server returned invalid error code |
| 2124-3001 | AAuth server returned error 0111 ("Application update is required.") |
| 2124-3120 | AAuth server returned invalid response but http status indicates success |
| 2124-3121 | BaaS server returned invalid response but http status indicates success |

## Account Errors (DAuth)
The following errors are shown when the [DAuth server](DAuth-Server) returns an error code:

| Dialog | Code | Description |
| --- | --- | --- |
| 2124-4504 | 0004 | Unauthorized device. |
| 2124-4507 | 0007 | System update is required. |
| 2124-4508 | 0008 | Device has been banned. |
| 2124-4509 | 0009 | Internal Server Error. |
| 2124-4510 | 0010 | Under maintenance. |
| 2124-4511 | 0011 | Invalid client. |
| 2124-4512 | 0012 | API not found. |
| 2124-4513 | 0013 | Invalid certificate. |
| 2124-4514 | 0014 | Invalid parameter in request. |
| 2124-4515 | 0015 | Invalid parameter in request. |
| 2124-4516 | 0016 | Invalid parameter in request. |
| 2124-4517 | 0017 | This device might be broken. |
| 2124-4518 | 0018 | |
| 2124-4519 | 0019 | |
| 2124-4520 | 0020 | |
| 2124-4521 | 0021 | |
| 2124-4522 | 0022 | |
| 2124-4523 | 0023 | |
| 2124-4524 | 0024 | |
| 2124-4525 | 0025 | |
| 2124-4526 | 0026 | |
| 2124-4527 | 0027 | |
| 2124-4528 | 0028 | |
| 2124-4529 | 0029 | |
| 2124-4530 | 0030 | |
| 2124-4531 | 0031 | |

## Account Errors (AAuth)
These errors are shown when the [AAuth server](AAuth-Server) returns an error code.

| Dialog | Code | Description |
| --- | --- | --- |
| 2124-4603 | 0103 | Device token expired. |
| 2124-4605 | 0105 | ROM ID has been banned. |
| 2124-4606 | 0106 | Unauthorized application. |
| 2124-4607 | 0107 | |
| 2124-4608 | 0108 | |
| 2124-4609 | 0109 | Service closed. |
| 2124-4610 | 0110 | |
| 2124-4611 | 0111 | Application update is required. |
| 2124-4612 | 0112 | Internal Server Error. |
| 2124-4613 | 0113 | |
| 2124-4618 | 0118 | Invalid parameter in request. |
| 2124-4620 | 0120 | |
| 2124-4621 | 0121 | Region mismatch. |
| 2124-4799 | Other | AAuth server returned invalid error code |

## Account Errors (BAAS)
These errors are related to the [Switch account server](BAAS-Server).

| Error Code | Description |
| --- | --- |
| 2124-5000 | `invalid_params` |
| 2124-5001 | `invalid_request` |
| 2124-5002 | `invalid_device_account` |
| 2124-5003 | `invalid_ndas_app_authn_token` |
| 2124-5004 | `invalid_idp` |
| 2124-5005 | `invalid_idp_account` |
| 2124-5006 | `linked_user_not_found` |
| 2124-5007 | `invalid_friend_code_format` |
| 2124-5008 | `user_link_not_exist` |
| 2124-5009 | `invalid_raw_content` |
| 2124-5100 | `invalid_token` |
| 2124-5101 | `insufficient_scope` |
| 2124-5102 | `forbidden` |
| 2124-5103 | `unavailable_device_account` |
| 2124-5104 | `resource_is_not_found` |
| 2124-5105 | `method_not_allowed` |
| 2124-5106 | `not_acceptable_language` |
| 2124-5107 | `resource_already_exists` |
| 2124-5108 | `user_link_already_exists` |
| 2124-5109 | `precondition_failed` |
| 2124-5110 | `friend_code_unregenerable_state` |
| 2124-5111 | `banned_user` |
| 2124-5112 | `deleted_user` |
| 2124-5113 | `membership_required` |
| 2124-5114 | `banned_user_by_application` |
| 2124-5200 | `internal_server_error` |
| 2124-5210 | `could_not_confirm_membership` |
| 2124-5249 | `under_maintenance` |

## Account Errors (NAS)
| Error Codes | Request path |
| --- | --- |
| 6000-6099 | [`/connect/1.0.0/authorize`](#account-errors-(nas-authorization-request)) |
| 6100-6199 | [`/connect/1.0.0/api/token`](#account-errors-(nas-token-request)) |
| 6200-6249 | - [`/api/1.0.0/users/<id>/qrcode_param`](#account-errors-(nas-user-request))<br>- [`/2.0.0/users/me`](#account-errors-(nas-user-request)) |

### Account Errors (NAS Authorization Request)
| Error Codes | Name | Detail |
| --- | --- | --- |
| 2124-6000 | `unauthorized_client` | |
| 2124-6001 | `access_denied` | |
| 2124-6003 | `access_denied` | `id_token_hint_invalid` |
| 2124-6004 | `access_denied` | `user_deleted` |
| 2124-6010 | `invalid_scope` | |
| 2124-6011 | `invalid_scope` | `scope_token_unknown` |
| 2124-6012 | `invalid_scope` | `scope_token_prohibited` |
| 2124-6020 | `server_error` | |
| 2124-6021 | `login_required` | |
| 2124-6022 | `login_required` | `user_not_logged_in` |
| 2124-6023 | `login_required` | `user_different_from_id_token_hint` |
| 2124-6030 | `consent_required` | |
| 2124-6031 | `interaction_required` | |
| 2124-6032 | `interaction_required` | `user_banned` |
| 2124-6033 | `interaction_required` | `user_suspended` |
| 2124-6034 | `interaction_required` | `user_terms_agreement_required` |
| 2124-6099 | `under_maintenance` | |

### Account Errors (NAS Token Request)
| Error Codes | Name | Detail |
| --- | --- | --- |
| 2124-6100 | `invalid_request` | |
| 2124-6101 | `invalid_client` | |
| 2124-6102 | `invalid_grant` | |
| 2124-6103 | `invalid_grant` | `user_deleted` |
| 2124-6104 | `invalid_grant` | `user_banned` |
| 2124-6105 | `invalid_grant` | `user_suspended` |
| 2124-6106 | `invalid_grant` | `user_withdrawn` |
| 2124-6107 | `invalid_grant` | `user_terms_agreement_required` |
| 2124-6120 | `invalid_scope` | |
| 2124-6121 | `invalid_scope` | `scope_token_unknown` |
| 2124-6122 | `invalid_scope` | `scope_token_prohibited` |
| 2124-6123 | `invalid_scope` | `scope_token_not_authorized` |
| 2124-6130 | `unauthorized_client` | |
| 2124-6131 | `unsupported_grant_type` | |
| 2124-6132 | `server_error` | |
| 2124-6199 | `under_maintenance` | |

### Account Errors (NAS User Request)
| Error Codes | Name |
| --- | --- |
| 2124-6200 | `invalid_token` |
| 2124-6201 | `insufficient_scope` |
| 2124-6249 | `under_maintenance` |

## Account Errors (HTTP)
| Error Code | HTTP status |
| --- | --- |
| 2124-7000 | Invalid |
| 2124-7001 | Invalid (4xx) |
| 2124-7002 | Invalid (5xx) |
| 2124-7400 | 400 (Bad Request) |
| 2124-7401 | 401 (Unauthorized) |
| 2124-7403 | 403 (Forbidden) |
| 2124-7404 | 404 (Not Found) |
| 2124-7405 | 405 (Method Not Allowed) |
| 2124-7406 | 406 (Not Acceptable) |
| 2124-7407 | 407 (Proxy Authentication Required) |
| 2124-7408 | 408 (Request Timeout) |
| 2124-7409 | 409 (Conflict) |
| 2124-7410 | 410 (Gone) |
| 2124-7411 | 411 (Length Required) |
| 2124-7412 | 412 (Precondition Failed) |
| 2124-7413 | 413 (Payload Too Large) |
| 2124-7414 | 414 (URI Too Long) |
| 2124-7415 | 415 (Unsupported Media Type) |
| 2124-7416 | 416 (Requested Range Not Satisfiable) |
| 2124-7417 | 417 (Expectation Failed) |
| 2124-7500 | 500 (Internal Server Error) |
| 2124-7501 | 501 (Not Implemented) |
| 2124-7502 | 502 (Bad Gateway) |
| 2124-7503 | 503 (Service Unavailable) |
| 2124-7504 | 504 (Gateway Timeout) |
| 2124-7505 | 505 (HTTP Version Not Supported) |

# NIM Error Codes
| Error Code | Description |
| --- | --- |
| 2137-4501 | unexpected-error |
| 2137-4502 | api-not-found |
| 2137-4503 | communication-failed |
| 2137-4504 | invalid-params |
| 2137-4505 | invalid-auth-token |
| 2137-4506 | resource-not-found |
| 2137-4508 | device-registration-limit-reached |
| 2137-4509 | invalid-nearness-check-result |
| 2137-4510 | operation-not-allowed |
| 2137-4511 | invalid-certificate |
| 2137-4512 | direct-message-failed |
| 2137-4513 | direct-message-receiver-is-offline |
| 2137-4514 | invalid-account-config-payload |
| 2137-4515 | device-unregistration-limit-reached |
| 2137-4516 | invalid-migration-state |
| 2137-4517 | vermillion-app-call-failed |
| 2137-4518 | atums-call-failed |
| 2137-4519 | dragons-call-failed |
| 2137-4520 | pegasus-call-failed |
| 2137-4521 | baas-call-failed |
| 2137-4522 | penne-call-failed |
| 2137-4523 | nas-call-failed |

# HTTP Error Codes
| Error Codes | Description |
| --- | --- |
| 0100 - 0599 | [HTTP errors](#http-errors-status) |
| 8000 - 8199 | [Curl errors](#http-errors-curl) |

## HTTP Errors (Status)
| Error Code | HTTP status |
| --- | --- |
| 2155-0100 | 100 (Continue) |
| 2155-0101 | 101 (Switchting Protocols) |
| 2155-0102 | 102 (Processing) |
| 2155-0300 | 300 (Multiple Choices) |
| 2155-0301 | 301 (Moved Permanently) |
| 2155-0302 | 302 (Found) |
| 2155-0303 | 303 (See Other) |
| 2155-0304 | 304 (Not Modified) |
| 2155-0305 | 305 (Use Proxy) |
| 2155-0306 | 306 (Switch Proxy) |
| 2155-0307 | 307 (Temporary Redirect) |
| 2155-0308 | 308 (Permanent Redirect) |
| 2155-0400 | 400 (Bad Request) |
| 2155-0401 | 401 (Unauthorized) |
| 2155-0402 | 402 (Payment Required) |
| 2155-0403 | 403 (Forbidden) |
| 2155-0404 | 404 (Not Found) |
| 2155-0405 | 405 (Method Not Allowed) |
| 2155-0406 | 406 (Not Acceptable) |
| 2155-0407 | 407 (Proxy Authentication Required) |
| 2155-0408 | 408 (Request Timeout) |
| 2155-0409 | 409 (Conflict) |
| 2155-0410 | 410 (Gone) |
| 2155-0411 | 411 (Length Required) |
| 2155-0412 | 412 (Precondition Failed) |
| 2155-0413 | 413 (Payload Too Large) |
| 2155-0414 | 414 (URI Too Long) |
| 2155-0415 | 415 (Unsupported Media Type) |
| 2155-0416 | 416 (Requested Range Not Satisfiable) |
| 2155-0417 | 417 (Expectation Failed) |
| 2155-0418 | 418 (I'm a Teapot) |
| 2155-0422 | 422 (Unprocessable Entity) |
| 2155-0423 | 423 (Locked) |
| 2155-0424 | 424 (Failed Dependency) |
| 2155-0426 | 426 (Upgrade Required) |
| 2155-0429 | 429 (Too Many Requests) |
| 2155-0451 | 451 (Unavailable For Legal Reasons) |
| 2155-0498 | Invalid (4xx) |
| 2155-0500 | 500 (Internal Server Error) |
| 2155-0501 | 501 (Not Implemented) |
| 2155-0502 | 502 (Bad Gateway) |
| 2155-0503 | 503 (Service Unavailable) |
| 2155-0504 | 504 (Gateway Timeout) |
| 2155-0505 | 505 (HTTP Version Not Supported) |
| 2155-0506 | 506 (Variant Also Negotiates) |
| 2155-0507 | 507 (Insufficient Storage) |
| 2155-0508 | 508 (Loop Detected) |
| 2155-0509 | 509 (Bandwidth Limit Exceeded) |
| 2155-0510 | 510 (Not Extended) |
| 2155-0511 | 511 (Network Authentication Required) |
| 2155-0598 | Invalid (5xx) |
| 2155-0599 | Invalid |

## HTTP Errors (Curl)
| Error Code | Description |
| --- | --- |
| 2155-8001 | CURLE_UNSUPPORTED_PROTOCOL |
| 2155-8002 | CURLE_FAILED_INIT |
| 2155-8003 | CURLE_URL_MALFORMAT |
| 2155-8004 | CURLE_NOT_BUILT_IN |
| 2155-8005 | CURLE_COULDNT_RESOLVE_PROXY |
| 2155-8006 | CURLE_COULDNT_RESOLVE_HOST |
| 2155-8007 | CURLE_COULDNT_CONNECT |
| 2155-8009 | CURLE_REMOTE_ACCESS_DENIED |
| 2155-8016 | CURLE_HTTP2 |
| 2155-8018 | CURLE_PARTIAL_FILE |
| 2155-8021 | CURLE_QUOTE_ERROR |
| 2155-8022 | CURLE_HTTP_RETURNED_ERROR |
| 2155-8023 | CURLE_WRITE_ERROR |
| 2155-8025 | CURLE_UPLOAD_FAILED |
| 2155-8026 | CURLE_READ_ERROR |
| 2155-8027 | CURLE_OUT_OF_MEMORY |
| 2155-8028 | CURLE_OPERATION_TIMEDOUT |
| 2155-8033 | CURLE_RANGE_ERROR |
| 2155-8034 | CURLE_HTTP_POST_ERROR |
| 2155-8035 | CURLE_SSL_CONNECT_ERROR |
| 2155-8036 | CURLE_BAD_DOWNLOAD_RESUME |
| 2155-8041 | CURLE_FUNCTION_NOT_FOUND |
| 2155-8042 | CURLE_ABORTED_BY_CALLBACK |
| 2155-8043 | CURLE_BAD_FUNCTION_ARGUMENT |
| 2155-8045 | CURLE_INTERFACE_FAILED |
| 2155-8047 | CURLE_TOO_MANY_REDIRECTS |
| 2155-8048 | CURLE_UNKNOWN_OPTION |
| 2155-8051 | CURLE_PEER_FAILED_VERIFICATION |
| 2155-8052 | CURLE_GOT_NOTHING |
| 2155-8053 | CURLE_SSL_ENGINE_NOTFOUND |
| 2155-8054 | CURLE_SSL_ENGINE_SETFAILED |
| 2155-8055 | CURLE_SEND_ERROR |
| 2155-8056 | CURLE_RECV_ERROR |
| 2155-8058 | CURLE_SSL_CERTPROBLEM |
| 2155-8059 | CURLE_SSL_CIPHER |
| 2155-8061 | CURLE_BAD_CONTENT_ENCODING |
| 2155-8063 | CURLE_FILESIZE_EXCEEDED |
| 2155-8064 | CURLE_USE_SSL_FAILED |
| 2155-8065 | CURLE_SEND_FAIL_REWIND |
| 2155-8066 | CURLE_SSL_ENGINE_INITFAILED |
| 2155-8067 | CURLE_LOGIN_DENIED |
| 2155-8075 | CURLE_CONV_FAILED |
| 2155-8076 | CURLE_CONV_REQD |
| 2155-8077 | CURLE_SSL_CACERT_BADFILE |
| 2155-8080 | CURLE_SSL_SHUTDOWN_FAILED |
| 2155-8081 | CURLE_AGAIN |
| 2155-8082 | CURLE_SSL_CRL_BADFILE |
| 2155-8083 | CURLE_SSL_ISSUER_ERROR |
| 2155-8088 | CURLE_CHUNK_FAILED |
| 2155-8089 | CURLE_NO_CONNECTION_AVAILABLE |
| 2155-8090 | CURLE_SSL_PINNEDPUBKEYNOTMATCH |
| 2155-8091 | CURLE_SSL_INVALIDCERTSTATUS |
| 2155-8092 | Curl returned error 94 (nintendo-specific) |
| 2155-8093 | Curl returned error 95 (nintendo-specific) |
| 2155-8094 | Curl returned error 96 (nintendo-specific) |
| 2155-8095 | Curl returned error 97 (nintendo-specific) |
| 2155-8096 | Curl returned error 98 (nintendo-specific) |
| 2155-8148 | Curl returned an invalid error code |
| 2155-8151 | CURLM_BAD_HANDLE |
| 2155-8152 | CURLM_BAD_EASY_HANDLE |
| 2155-8153 | CURLM_OUT_OF_MEMORY |
| 2155-8154 | CURLM_INTERNAL_ERROR |
| 2155-8155 | CURLM_BAD_SOCKET |
| 2155-8156 | CURLM_UNKNOWN_OPTION |
| 2155-8157 | CURLM_ADDED_ALREADY |
| 2155-8191 | Curl multi returned an invalid error code |

# DAuth Error Codes
These errors are related to [device](DAuth-Server) and [application](AAuth-Server) authentication.

| Error code | Description |
| --- | --- |
| 4000 - 4099 | [DAuth (device authentication)](#dauth-errors-dauth) |
| 4100 - 4199 | [AAuth (application authentication)](#dauth-errors-aauth) |
| 4500 - 4599 | [Dragons (e-license management)](#dauth-errors-dragons) |
| Other | [General errors](#dauth-errors-general) |

## DAuth Errors (General)
| Error code | Description |
| --- | --- |
| 2181-0200 | DAuth service is busy (too many async requests at the same time) |
| 2181-3100 | DAuth or AAuth server returned invalid response |
| 2181-3101 | Dragons server returned invalid response |
| 2181-3200 | Failed to load device token from cache |

## DAuth Errors (DAuth)

The following errors are shown when the [DAuth server](DAuth-Server) returns an error code:

| Dialog | Code | Description |
| --- | --- | --- |
| 2181-4004 | 0004 | Unauthorized device. |
| 2181-4007 | 0007 | System update is required. |
| 2181-4008 | 0008 | Device has been banned. |
| 2181-4009 | 0009 | Internal Server Error. |
| 2181-4010 | 0010 | Under maintenance. |
| 2181-4011 | 0011 | Invalid client. |
| 2181-4012 | 0012 | API not found. |
| 2181-4013 | 0013 | Invalid certificate. |
| 2181-4014 | 0014 | Invalid parameter in request. |
| 2181-4015 | 0015 | Invalid parameter in request. |
| 2181-4016 | 0016 | Invalid parameter in request. |
| 2181-4017 | 0017 | This device might be broken. |
| 2181-4018 | 0018 | |
| 2181-4019 | 0019 | |
| 2181-4020 | 0020 | |
| 2181-4021 | 0021 | |
| 2181-4022 | 0022 | |
| 2181-4023 | 0023 | |
| 2181-4024 | 0024 | |
| 2181-4025 | 0025 | |
| 2181-4026 | 0026 | |
| 2181-4027 | 0027 | |
| 2181-4028 | 0028 | |
| 2181-4029 | 0029 | |
| 2181-4030 | 0030 | |
| 2181-4031 | 0031 | |

## DAuth Errors (AAuth)

The following errors are shown when the [AAuth server](AAuth-Server) returns an error code:

| Dialog | Code | Description |
| --- | --- | --- |
| 2181-4103 | 0103 | Device token expired. |
| 2181-4105 | 0105 | ROM ID has been banned. |
| 2181-4106 | 0106 | Unauthorized application. |
| 2181-4107 | 0107 | |
| 2181-4108 | 0108 | |
| 2181-4109 | 0109 | Service closed. |
| 2181-4110 | 0110 | |
| 2181-4111 | 0111 | Application update is required. |
| 2181-4112 | 0112 | Internal Server Error. |
| 2181-4113 | 0113 | |
| 2181-4118 | 0118 | Invalid parameter in request. |
| 2181-4120 | 0120 | |
| 2181-4121 | 0121 | Region mismatch. |

## DAuth Errors (Dragons)

The following errors are shown when the [dragons server](Dragons-Servers) returns an error code:

| Error Code | Description |
| --- | --- |
| 2181-4501 | `400/invalid_parameter` |
| 2181-4502 | `401/authentication_required` |
| 2181-4503 | `403/invalid_token` |
| 2181-4506 | `404/license_not_found` |
| 2181-4507 | `403/license_inactive` |
| 2181-4508 | `503/abort_retry` |
| 2181-4511 | `400/invalid_device_certificate` |
| 2181-4512 | `401/account_id_required` |
| 2181-4513 | `403/license_archive_not_allowed` |
| 2181-4514 | `403/license_not_grantable` |
| 2181-4515 | `403/rights_policy_not_allowed` |
| 2181-4516 | `403/system_update_required` |
| 2181-4517 | `404/license_archive_not_found` |
| 2181-4518 | `404/page_not_found` |
| 2181-4519 | `405/method_not_allowed` |
| 2181-4520 | `406/not_acceptable` |
| 2181-4521 | `415/unsupported_media_type` |
| 2181-4522 | `500/delete_record_failed` |
| 2181-4523 | `500/insert_record_failed` |
| 2181-4524 | `500/shogun_error` |
| 2181-4525 | `500/unexpected_error` |
| 2181-4526 | `503/service_unavailable` |
| 2181-4528 | `500/op2_error` |
| 2181-4529 | `503/op2_maintenance` |
| 2181-4532 | `400/duplicate_rights_id` |
| 2181-4533 | `400/invalid_eticket_template` |
| 2181-4534 | `403/edge_token_not_grantable` |
| 2181-4535 | `404/promotion_policy_not_found` |
| 2181-4536 | `404/title_not_found` |
| 2181-4537 | `500/update_record_failed` |
| 2181-4538 | `500/unknown_issuer` |

# NEX Error Codes
| Error code | Name |
| --- | --- |
| 2306-0102 | Core::Unknown |
| 2306-0103 | Core::NotImplemented |
| 2306-0104 | Core::InvalidPointer |
| 2306-0105 | Core::OperationAborted |
| 2306-0106 | Core::Exception |
| 2306-0107 | Core::AccessDenied |
| 2306-0108 | Core::InvalidHandle |
| 2306-0109 | Core::InvalidIndex |
| 2306-0110 | Core::OutOfMemory |
| 2306-0111 | Core::InvalidArgument |
| 2306-0112 | Core::Timeout |
| 2306-0113 | Core::InitializationFailure |
| 2306-0114 | Core::CallInitiationFailure |
| 2306-0115 | Core::RegistrationError |
| 2306-0116 | Core::BufferOverflow |
| 2306-0117 | Core::InvalidLockState |
| 2306-0118 | Core::InvalidSequence |
| 2306-0119 | Core::SystemError |
| 2306-0120 | Core::Cancelled |
| 2306-0201 | DDL::InvalidSignature |
| 2306-0202 | DDL::IncorrectVersion |
| 2306-0301 | RendezVous::ConnectionFailure |
| 2306-0302 | RendezVous::NotAuthenticated |
| 2306-0303 | RendezVous::InvalidUsername |
| 2306-0304 | RendezVous::InvalidPassword |
| 2306-0305 | RendezVous::UsernameAlreadyExists |
| 2306-0306 | RendezVous::AccountDisabled |
| 2306-0307 | RendezVous::AccountExpired |
| 2306-0308 | RendezVous::ConcurrentLoginDenied |
| 2306-0309 | RendezVous::EncryptionFailure |
| 2306-0310 | RendezVous::InvalidPID |
| 2306-0311 | RendezVous::MaxConnectionsReached |
| 2306-0312 | RendezVous::InvalidGID |
| 2306-0313 | RendezVous::InvalidControlScriptID |
| 2306-0314 | RendezVous::InvalidOperationInLiveEnvironment |
| 2306-0315 | RendezVous::DuplicateEntry |
| 2306-0316 | RendezVous::ControlScriptFailure |
| 2306-0317 | RendezVous::ClassNotFound |
| 2306-0318 | RendezVous::SessionVoid |
| 2306-0320 | RendezVous::DDLMismatch |
| 2306-0321 | RendezVous::InvalidConfiguration |
| 2306-0322 | RendezVous::SessionFull |
| 2306-0323 | RendezVous::InvalidGatheringPassword |
| 2306-0324 | RendezVous::WithoutParticipationPeriod |
| 2306-0325 | RendezVous::PersistentGatheringCreationMax |
| 2306-0326 | RendezVous::PersistentGatheringParticipationMax |
| 2306-0327 | RendezVous::DeniedByParticipants |
| 2306-0328 | RendezVous::ParticipantInBlackList |
| 2306-0329 | RendezVous::GameServerMaintenance |
| 2306-0330 | RendezVous::OperationPostpone |
| 2306-0331 | RendezVous::OutOfRatingRange |
| 2306-0332 | RendezVous::ConnectionDisconnected |
| 2306-0333 | RendezVous::InvalidOperation |
| 2306-0334 | RendezVous::NotParticipatedGathering |
| 2306-0335 | RendezVous::MatchmakeSessionUserPasswordUnmatch |
| 2306-0336 | RendezVous::MatchmakeSessionSystemPasswordUnmatch |
| 2306-0337 | RendezVous::UserIsOffline |
| 2306-0338 | RendezVous::AlreadyParticipatedGathering |
| 2306-0339 | RendezVous::PermissionDenied |
| 2306-0340 | RendezVous::NotFriend |
| 2306-0341 | RendezVous::SessionClosed |
| 2306-0342 | RendezVous::DatabaseTemporarilyUnavailable |
| 2306-0343 | RendezVous::InvalidUniqueId |
| 2306-0344 | RendezVous::MatchmakingWithdrawn |
| 2306-0345 | RendezVous::LimitExceeded |
| 2306-0346 | RendezVous::AccountTemporarilyDisabled |
| 2306-0347 | RendezVous::PartiallyServiceClosed |
| 2306-0348 | RendezVous::ConnectionDisconnectedForConcurrentLogin |
| 2306-0401 | PythonCore::Exception |
| 2306-0402 | PythonCore::TypeError |
| 2306-0403 | PythonCore::IndexError |
| 2306-0404 | PythonCore::InvalidReference |
| 2306-0405 | PythonCore::CallFailure |
| 2306-0406 | PythonCore::MemoryError |
| 2306-0407 | PythonCore::KeyError |
| 2306-0408 | PythonCore::OperationError |
| 2306-0409 | PythonCore::ConversionError |
| 2306-0410 | PythonCore::ValidationError |
| 2306-0501 | Transport::Unknown |
| 2306-0502 | Transport::ConnectionFailure |
| 2306-0503 | Transport::InvalidUrl |
| 2306-0504 | Transport::InvalidKey |
| 2306-0505 | Transport::InvalidURLType |
| 2306-0506 | Transport::DuplicateEndpoint |
| 2306-0507 | Transport::IOError |
| 2306-0508 | Transport::Timeout |
| 2306-0509 | Transport::ConnectionReset |
| 2306-0510 | Transport::IncorrectRemoteAuthentication |
| 2306-0511 | Transport::ServerRequestError |
| 2306-0512 | Transport::DecompressionFailure |
| 2306-0513 | Transport::ReliableSendBufferFullFatal |
| 2306-0514 | Transport::UPnPCannotInit |
| 2306-0515 | Transport::UPnPCannotAddMapping |
| 2306-0516 | Transport::NatPMPCannotInit |
| 2306-0517 | Transport::NatPMPCannotAddMapping |
| 2306-0519 | Transport::UnsupportedNAT |
| 2306-0520 | Transport::DnsError |
| 2306-0521 | Transport::ProxyError |
| 2306-0522 | Transport::DataRemaining |
| 2306-0523 | Transport::NoBuffer |
| 2306-0524 | Transport::NotFound |
| 2306-0525 | Transport::TemporaryServerError |
| 2306-0526 | Transport::PermanentServerError |
| 2306-0527 | Transport::ServiceUnavailable |
| 2306-0528 | Transport::ReliableSendBufferFull |
| 2306-0529 | Transport::InvalidStation |
| 2306-0530 | Transport::InvalidSubStreamID |
| 2306-0531 | Transport::PacketBufferFull |
| 2306-0532 | Transport::NatTraversalError |
| 2306-0533 | Transport::NatCheckError |
| 2306-0602 | DOCore::StationNotReached |
| 2306-0603 | DOCore::TargetStationDisconnect |
| 2306-0604 | DOCore::LocalStationLeaving |
| 2306-0605 | DOCore::ObjectNotFound |
| 2306-0606 | DOCore::InvalidRole |
| 2306-0607 | DOCore::CallTimeout |
| 2306-0608 | DOCore::RMCDispatchFailed |
| 2306-0609 | DOCore::MigrationInProgress |
| 2306-0610 | DOCore::NoAuthority |
| 2306-0611 | DOCore::NoTargetStationSpecified |
| 2306-0612 | DOCore::JoinFailed |
| 2306-0613 | DOCore::JoinDenied |
| 2306-0614 | DOCore::ConnectivityTestFailed |
| 2306-0615 | DOCore::Unknown |
| 2306-0616 | DOCore::UnfreedReferences |
| 2306-0617 | DOCore::JobTerminationFailed |
| 2306-0618 | DOCore::InvalidState |
| 2306-0619 | DOCore::FaultRecoveryFatal |
| 2306-0620 | DOCore::FaultRecoveryJobProcessFailed |
| 2306-0621 | DOCore::StationInconsitency |
| 2306-0622 | DOCore::AbnormalMasterState |
| 2306-0623 | DOCore::VersionMismatch |
| 2306-0701 | FPD::NotInitialized |
| 2306-0702 | FPD::AlreadyInitialized |
| 2306-0703 | FPD::NotConnected |
| 2306-0704 | FPD::Connected |
| 2306-0705 | FPD::InitializationFailure |
| 2306-0706 | FPD::OutOfMemory |
| 2306-0707 | FPD::RmcFailed |
| 2306-0708 | FPD::InvalidArgument |
| 2306-0709 | FPD::InvalidLocalAccountID |
| 2306-0710 | FPD::InvalidPrincipalID |
| 2306-0711 | FPD::InvalidLocalFriendCode |
| 2306-0712 | FPD::LocalAccountNotExists |
| 2306-0713 | FPD::LocalAccountNotLoaded |
| 2306-0714 | FPD::LocalAccountAlreadyLoaded |
| 2306-0715 | FPD::FriendAlreadyExists |
| 2306-0716 | FPD::FriendNotExists |
| 2306-0717 | FPD::FriendNumMax |
| 2306-0718 | FPD::NotFriend |
| 2306-0719 | FPD::FileIO |
| 2306-0720 | FPD::P2PInternetProhibited |
| 2306-0721 | FPD::Unknown |
| 2306-0722 | FPD::InvalidState |
| 2306-0724 | FPD::AddFriendProhibited |
| 2306-0726 | FPD::InvalidAccount |
| 2306-0727 | FPD::BlacklistedByMe |
| 2306-0729 | FPD::FriendAlreadyAdded |
| 2306-0730 | FPD::MyFriendListLimitExceed |
| 2306-0731 | FPD::RequestLimitExceed |
| 2306-0732 | FPD::InvalidMessageID |
| 2306-0733 | FPD::MessageIsNotMine |
| 2306-0734 | FPD::MessageIsNotForMe |
| 2306-0735 | FPD::FriendRequestBlocked |
| 2306-0736 | FPD::NotInMyFriendList |
| 2306-0737 | FPD::FriendListedByMe |
| 2306-0738 | FPD::NotInMyBlacklist |
| 2306-0739 | FPD::IncompatibleAccount |
| 2306-0740 | FPD::BlockSettingChangeNotAllowed |
| 2306-0741 | FPD::SizeLimitExceeded |
| 2306-0742 | FPD::OperationNotAllowed |
| 2306-0743 | FPD::NotNetworkAccount |
| 2306-0744 | FPD::NotificationNotFound |
| 2306-0745 | FPD::PreferenceNotInitialized |
| 2306-0746 | FPD::FriendRequestNotAllowed |
| 2306-0801 | Authentication::NASAuthenticateError |
| 2306-0802 | Authentication::TokenParseError |
| 2306-0803 | Authentication::HttpConnectionError |
| 2306-0804 | Authentication::HttpDNSError |
| 2306-0805 | Authentication::HttpGetProxySetting |
| 2306-0806 | Authentication::TokenExpired |
| 2306-0807 | Authentication::ValidationFailed |
| 2306-0808 | Authentication::InvalidParam |
| 2306-0809 | Authentication::PrincipalIdUnmatched |
| 2306-0810 | Authentication::MoveCountUnmatch |
| 2306-0811 | Authentication::UnderMaintenance |
| 2306-0812 | Authentication::UnsupportedVersion |
| 2306-0813 | Authentication::ServerVersionIsOld |
| 2306-0814 | Authentication::Unknown |
| 2306-0815 | Authentication::ClientVersionIsOld |
| 2306-0816 | Authentication::AccountLibraryError |
| 2306-0817 | Authentication::ServiceNoLongerAvailable |
| 2306-0818 | Authentication::UnknownApplication |
| 2306-0819 | Authentication::ApplicationVersionIsOld |
| 2306-0820 | Authentication::OutOfService |
| 2306-0821 | Authentication::NetworkServiceLicenseRequired |
| 2306-0822 | Authentication::NetworkServiceLicenseSystemError |
| 2306-0823 | Authentication::NetworkServiceLicenseError3 |
| 2306-0824 | Authentication::NetworkServiceLicenseError4 |
| 2306-1101 | Ranking::NotInitialized |
| 2306-1102 | Ranking::InvalidArgument |
| 2306-1103 | Ranking::RegistrationError |
| 2306-1105 | Ranking::NotFound |
| 2306-1106 | Ranking::InvalidScore |
| 2306-1107 | Ranking::InvalidDataSize |
| 2306-1109 | Ranking::PermissionDenied |
| 2306-1110 | Ranking::Unknown |
| 2306-1111 | Ranking::NotImplemented |
| 2306-1201 | DataStore::Unknown |
| 2306-1202 | DataStore::InvalidArgument |
| 2306-1203 | DataStore::PermissionDenied |
| 2306-1204 | DataStore::NotFound |
| 2306-1205 | DataStore::AlreadyLocked |
| 2306-1206 | DataStore::UnderReviewing |
| 2306-1207 | DataStore::Expired |
| 2306-1208 | DataStore::InvalidCheckToken |
| 2306-1209 | DataStore::SystemFileError |
| 2306-1210 | DataStore::OverCapacity |
| 2306-1211 | DataStore::OperationNotAllowed |
| 2306-1212 | DataStore::InvalidPassword |
| 2306-1213 | DataStore::ValueNotEqual |
| 2306-1500 | ServiceItem::Unknown |
| 2306-1501 | ServiceItem::InvalidArgument |
| 2306-1502 | ServiceItem::EShopUnknownHttpError |
| 2306-1503 | ServiceItem::EShopResponseParseError |
| 2306-1504 | ServiceItem::NotOwned |
| 2306-1505 | ServiceItem::InvalidLimitationType |
| 2306-1506 | ServiceItem::ConsumptionRightShortage |
| 2306-1801 | MatchmakeReferee::Unknown |
| 2306-1802 | MatchmakeReferee::InvalidArgument |
| 2306-1803 | MatchmakeReferee::AlreadyExists |
| 2306-1804 | MatchmakeReferee::NotParticipatedGathering |
| 2306-1805 | MatchmakeReferee::NotParticipatedRound |
| 2306-1806 | MatchmakeReferee::StatsNotFound |
| 2306-1807 | MatchmakeReferee::RoundNotFound |
| 2306-1808 | MatchmakeReferee::RoundArbitrated |
| 2306-1809 | MatchmakeReferee::RoundNotArbitrated |
| 2306-1901 | Subscriber::Unknown |
| 2306-1902 | Subscriber::InvalidArgument |
| 2306-1903 | Subscriber::OverLimit |
| 2306-1904 | Subscriber::PermissionDenied |
| 2306-2001 | Ranking2::Unknown |
| 2306-2002 | Ranking2::InvalidArgument |
| 2306-2003 | Ranking2::InvalidScore |
| 2306-2201 | Screening::Unknown |
| 2306-2202 | Screening::InvalidArgument |
| 2306-2203 | Screening::NotFound |

# NEX Error Descriptions
| Error&nbsp;code | Description |
| --- | --- |
| 2306-0102 | The reason for the error is unknown. |
| 2306-0103 | The operation is currently not implemented. |
| 2306-0104 | The operation specifies or accesses an invalid pointer. |
| 2306-0105 | The operation was aborted. |
| 2306-0106 | The operation raised an exception. |
| 2306-0107 | An attempt was made to access data in an incorrect manner. This may be due to inadequate permission or the data, file, etc. not existing. |
| 2306-0108 | The operation specifies or accesses an invalid DOHandle. |
| 2306-0109 | The operation specifies or accesses an invalid index. |
| 2306-0110 | The system could not allocate or access enough memory or disk space to perform the specified operation. |
| 2306-0111 | Invalid argument were passed with the operation. The argument(s) may be out of range or invalid. |
| 2306-0112 | The operation did not complete within the specified timeout for that operation. |
| 2306-0113 | Initialization of the component failed. |
| 2306-0114 | The call failed to initialize. |
| 2306-0115 | An error occurred during registration. |
| 2306-0116 | The buffer is too large to be sent. |
| 2306-0301 | Connection was unable to be established, either with the Rendez-Vous back end or a Peer. |
| 2306-0302 | The Principal could not be authenticated by the Authentication Service. |
| 2306-0303 | The Principal tried to log in with an invalid user name, i.e. the user name does not exist in the database. |
| 2306-0304 | The Principal either tried to log in with an invalid password for the provided user name or tried to join a Gathering with an invalid password. |
| 2306-0305 | The provided user name already exists in the database. All usernames must be unique. |
| 2306-0306 | The Principal's account still exists in the database but the account has been disabled. |
| 2306-0307 | The Principal's account still exists in the database but the account has expired. |
| 2306-0308 | The Principal does not have the Capabilities to perform concurrent log ins, i.e. at any given time only one log-in may be maintained. |
| 2306-0309 | Data encryption failed. |
| 2306-0310 | The operation specifies or accesses an invalid PrincipalID. |
| 2306-0311 | Maximum connnection number is reached |
| 2306-0501 | The reason for the error is unknown. |
| 2306-0502 | Network connection was unable to be established. |
| 2306-0503 | The URL contained in the StationURL is invalid. The syntax may be incorrect. |
| 2306-0504 | The key used to authenticate a given station is invalid. The secure transport layer uses secret-key based cryptography to ensure the integrity and confidentiality of data sent across the network. |
| 2306-0505 | The specified transport type is invalid. |
| 2306-0506 | The Station is already connected via another EndPoint. |
| 2306-0507 | The data coudl not be sent across the network. This could be due to an invalid message, packet, or buffer. |
| 2306-0508 | The operation did not complete within the specified timeout for that operation. |
| 2306-0509 | The network connection was reset. |
| 2306-0510 | The destination Station did not authenticate itself properly. |
| 2306-0511 | 3rd-party server or device answered with an error code according to protocol used e.g. HTTP error code |

# Pia Error Codes (New)
| Error Code | Name |
| --- | --- |
| 2318-0001 | AllocationFailed |
| 2318-0002 | AlreadyInitialized |
| 2318-0003 | BufferShortage |
| 2318-0004 | BrokenData |
| 2318-0005 | Cancelled |
| 2318-0006 | NetworkConnectionIsLost |
| 2318-0007 | InvalidArgument |
| 2318-0008 | InvalidState |
| 2318-0009 | NoData |
| 2318-0010 | NotFound |
| 2318-0011 | NotImplemented |
| 2318-0012 | NotInitialized |
| 2318-0013 | BufferIsFull |
| 2318-0014 | TimeOut |
| 2318-0015 | AlreadyExists |
| 2318-0016 | ContainerIsFull |
| 2318-0017 | TemporaryUnavailable |
| 2318-0019 | NotSet |
| 2318-0030 | SocketAddressFamilyIncompatible |
| 2318-0031 | NetworkConnectionIsLostDuringNatTraversalProcess |
| 2318-0101 | MemoryLeak |
| 2318-0102 | NetworkInterfaceIsNotFound |
| 2318-0103 | UnexpectedNetworkInterfaceAddress |
| 2318-0201 | NatCheckCommunicationFailed |
| 2318-0202 | InUsed |
| 2318-0203 | NatCheckDnsFailed |
| 2318-0204 | MonitoringDnsFailed |
| 2318-0302 | InvalidNode |
| 2318-0304 | NegligibleFault |
| 2318-0305 | InvalidConnection |
| 2318-0308 | LocalCommunicationInvalidState |
| 2318-0309 | NetworkIsNotFound |
| 2318-0310 | NetworkIsFull |
| 2318-0311 | LocalCommunicationLowerVersion |
| 2318-0312 | LocalCommunicationHigherVersion |
| 2318-0313 | WifiOff |
| 2318-0314 | Sleep |
| 2318-0315 | WirelessControllerCountLimitation |
| 2318-0317 | NetworkConnectionRejected |
| 2318-0401 | ConnectionFailed |
| 2318-0402 | CreateStationFailed |
| 2318-0403 | VersionMismatched |
| 2318-0404 | IsNotInCommunication |
| 2318-0405 | TableIsFull |
| 2318-0406 | IncreaseDataSize |
| 2318-0501 | RequestDenied |
| 2318-0502 | StationConnectionFailed |
| 2318-0506 | MeshIsFull |
| 2318-0507 | InvalidMessage |
| 2318-0510 | NatTraversalFailedUnknown |
| 2318-0513 | NatTraversalFailedLocalEim |
| 2318-0514 | NatTraversalFailedLocalEdm |
| 2318-0515 | NatTraversalFailedLocalEimSamePublicAddress |
| 2318-0516 | NatTraversalFailedLocalEdmSamePublicAddress |
| 2318-0521 | NatTraversalRequestTimeout |
| 2318-0522 | NatTraversalFailedByDuplicateGlobalAddress |
| 2318-0533 | JoinSessionFailedByNetworkConnectionTimeout |
| 2318-0534 | JoinSessionFailedByHostMigration |
| 2318-0535 | JoinSessionFailedByNetworkHostMigration |
| 2318-0536 | JoinSessionFailedBySystemDeniedResponse |
| 2318-0537 | JoinSessionFailedByLocalStationNotFound |
| 2318-0539 | JoinSessionFailedByCreateStation |
| 2318-0540 | JoinSessionFailedByDuplicateConstantId |
| 2318-0541 | SessionIsNotFound |
| 2318-0542 | RoomIsFull |
| 2318-0543 | DeniedByParticipant |
| 2318-0544 | ParticipantInBlocklist |
| 2318-0545 | SessionUserPasswordUnmatch |
| 2318-0546 | SessionSystemPasswordUnmatch |
| 2318-0547 | MeshConnectionIsLost |
| 2318-0548 | SessionIsClosed |
| 2318-0549 | CompanionStationIsOffline |
| 2318-0550 | HostIsNotFriend |
| 2318-0551 | SessionConnectionIsLost |
| 2318-0552 | CompanionStationIsLeft |
| 2318-0554 | SessionMigrationFailed |
| 2318-0555 | SessionWrongState |
| 2318-0557 | JoinSessionFailedByNetworkConnectionIsLostOnJoinRequest |
| 2318-0561 | MatchmakeServerMaintenance |
| 2318-0562 | MatchmakeServerProcessAborted |
| 2318-0563 | SessionConnectionIsLostByHost |
| 2318-0564 | SessionConnectionIsLostByHostMigrationFailure |
| 2318-0565 | SessionConnectionIsLostByInconsistentInfo |
| 2318-0566 | KickedOutFromSessionByInconsistentInfo |
| 2318-0567 | KickedOutFromSessionByUser |
| 2318-0571 | CreateCommunityFailedUpperLimit |
| 2318-0572 | JoinCommunityFailedUpperLimit |
| 2318-0573 | CommunityIsFull |
| 2318-0574 | CommunityIsNotFound |
| 2318-0575 | CommunityIsClosed |
| 2318-0576 | CommunityUserPasswordUnmatch |
| 2318-0577 | AlreadyJoinedCommunity |
| 2318-0578 | UserAccountNotExisted |
| 2318-0579 | DuplicateConstantId |
| 2318-0590 | LicenseForNetworkServiceNotAvailable |
| 2318-0591 | LicenseForNetworkServiceError |
| 2318-0592 | LicenseForNetworkServiceSubscriptionError |
| 2318-0593 | LicenseForNetworkServiceSubscriptionError2 |
| 2318-0602 | SyncDataIsNotArrivedYet |
| 2318-0606 | SyncDataIsNotSet |
| 2318-0701 | SystemLowerVersion |
| 2318-0702 | SystemHigherVersion |
| 2318-0802 | InvalidClock |
| 2318-1001 | SdkError |
| 2318-1003 | CancelledByUser |
| 2318-1101 | OutOfMemory |
| 2318-1102 | LoginTimeout |
| 2318-1103 | AlreadyLoggedIn |
| 2318-1104 | MatchmakeServerAuthenticationFailed |
| 2318-1105 | MatchmakeServerAuthenticationFailedByCommunicationVersion |
| 2318-1106 | MatchmakeServerInvalidClientCommunicationVersion |
| 2318-1107 | MatchmakeServerInvalidServerCommunicationVersion |
| 2318-1200 | TurnDnsFailed |
| 2318-1201 | SignalingServerProcessTimeout |
| 2318-1202 | TurnServerProcessTimeout |
| 2318-1203 | TurnFailedByDuplicateMappedAddress |
| 2318-1500 | MatchmakeServerConnectionFailed |
| 2318-1501 | MatchmakeServerProcessTimeout |
| 2318-1502 | MatchmakeServerServiceClientError |
| 2318-1800 | InvalidSocketError |

# Pia Error Codes (Old)
| Error Code | Name |
| --- | --- |
| 2618-0000 | ResultSdkViewerResultError |
| 2618-0001 | ResultAllocationFailed |
| 2618-0002 | ResultAlreadyInitialized |
| 2618-0003 | ResultBufferShortage |
| 2618-0004 | ResultBrokenData |
| 2618-0005 | ResultCancelled |
| 2618-0006 | ResultNetworkConnectionIsLost |
| 2618-0007 | ResultInvalidArgument |
| 2618-0008 | ResultInvalidState |
| 2618-0009 | ResultNoData |
| 2618-0010 | ResultNotFound |
| 2618-0011 | ResultNotImplemented |
| 2618-0012 | ResultNotInitialized |
| 2618-0013 | ResultBufferIsFull |
| 2618-0014 | ResultTimeOut |
| 2618-0015 | ResultAlreadyExists |
| 2618-0016 | ResultContainerIsFull |
| 2618-0017 | ResultTemporaryUnavailable |
| 2618-0019 | ResultNotSet |
| 2618-0101 | ResultMemoryLeak |
| 2618-0201 | ResultNatCheckFailed |
| 2618-0202 | ResultInUse |
| 2618-0203 | ResultDnsFailed |
| 2618-0302 | ResultInvalidNode |
| 2618-0304 | ResultNegligibleFault |
| 2618-0305 | ResultInvalidConnection |
| 2618-0308 | ResultErrorOccurred |
| 2618-0309 | ResultNetworkIsNotFound |
| 2618-0310 | ResultNetworkIsFull |
| 2618-0311 | ResultLocalLowerVersion |
| 2618-0312 | ResultLocalHigherVersion |
| 2618-0313 | ResultWifiOff |
| 2618-0314 | ResultSleep |
| 2618-0315 | ResultWirelessControllerCountLimitation |
| 2618-0401 | ResultConnectionFailed |
| 2618-0402 | ResultCreateStationFailed |
| 2618-0403 | ResultIncompatibleFormat |
| 2618-0404 | ResultNotInCommunication |
| 2618-0405 | ResultTableIsFull |
| 2618-0501 | ResultJoinRequestDenied |
| 2618-0502 | ResultStationConnectionFailed |
| 2618-0506 | ResultMeshIsFull |
| 2618-0507 | ResultInvalidSystemMessage |
| 2618-0510 | ResultStationConnectionNatTraversalFailedUnknown |
| 2618-0513 | ResultNatTraversalFailedBothEim |
| 2618-0514 | ResultNatTraversalFailedBothEdm |
| 2618-0515 | ResultNatTraversalFailedLocalEimRemoteEdm |
| 2618-0516 | ResultNatTraversalFailedLocalEdmRemoteEim |
| 2618-0517 | ResultRelayFailedNoCandidate |
| 2618-0518 | ResultRelayFailedRttLimit |
| 2618-0519 | ResultRelayFailedRelayNumLimit |
| 2618-0520 | ResultRelayFailedUnknown |
| 2618-0521 | ResultNatTraversalRequestTimeout |
| 2618-0541 | ResultSessionIsNotFound |
| 2618-0542 | ResultMatchmakeSessionIsFull |
| 2618-0543 | ResultDeniedByParticipants |
| 2618-0544 | ResultParticipantInBlockList |
| 2618-0545 | ResultSessionUserPasswordUnmatch |
| 2618-0546 | ResultSessionSystemPasswordUnmatch |
| 2618-0547 | ResultMeshConnectionIsLost |
| 2618-0548 | ResultSessionIsClosed |
| 2618-0549 | ResultCompanionStationIsOffline |
| 2618-0550 | ResultHostIsNotFriend |
| 2618-0551 | ResultSessionConnectionIsLost |
| 2618-0552 | ResultCompanionStationIsLeft |
| 2618-0554 | ResultSessionMigrationFailed |
| 2618-0555 | ResultSessionWrongState |
| 2618-0561 | ResultGameServerMaintenance |
| 2618-0562 | ResultGameServerProcessAborted |
| 2618-0571 | ResultCreateCommunityFailedUpperLimit |
| 2618-0572 | ResultJoinCommunityFailedUpperLimit |
| 2618-0573 | ResultCommunityIsFull |
| 2618-0574 | ResultCommunityIsNotFound |
| 2618-0575 | ResultCommunityIsClosed |
| 2618-0576 | ResultCommunityUserPasswordUnmatch |
| 2618-0577 | ResultAlreadyJoinedCommunity |
| 2618-0578 | ResultUserAccountNotExisted |
| 2618-0579 | ResultNetworkConnectionIsLostByDuplicateLogin |
| 2618-0583 | ResultNatTraversalFailedBothEimSamePublicAddress |
| 2618-0584 | ResultNatTraversalFailedBothEdmSamePublicAddress |
| 2618-0585 | ResultNatTraversalFailedLocalEimRemoteEdmSamePublicAddress |
| 2618-0586 | ResultNatTraversalFailedLocalEdmRemoteEimSamePublicAddress |
| 2618-0590 | ResultLicenseForNetworkServiceNotAvailable |
| 2618-0591 | ResultLicenseForNetworkServiceError |
| 2618-0592 | ResultLicenseForNetworkServiceSubscriptionError |
| 2618-0593 | ResultLicenseForNetworkServiceSubscriptionError2 |
| 2618-0602 | ResultDataIsNotArrivedYet |
| 2618-0606 | ResultDataIsNotSet |
| 2618-0701 | ResultLanLowerVersion |
| 2618-0702 | ResultLanHigherVersion |
| 2618-1001 | ResultSdkError |
| 2618-1003 | ResultCancelledByUser |

# Eagle Error Codes
| Error code | Name |
| --- | --- |
| 2623-0000 | FAILURE |
| 2623-0001 | INTERNAL_ERROR |
| 2623-0002 | INVALID_STATE |
| 2623-0003 | INVALID_ARGUMENT |
| 2623-0004 | NO_PERMISSIONS |
| 2623-0005 | NO_SUCH_FILE |
| 2623-0006 | FILE_ALREADY_EXISTS |
| 2623-0007 | NOT_ENOUGH_BUFFER |
| 2623-0008 | ARGUMENTS_SIZE_TOO_LARGE |
| 2623-0009 | NO_MEMORY_USER |
| 2623-0010 | NO_MEMORY_TRANSPORT |
| 2623-0011 | UNEXPECTED_ALIGNMENT |
| 2623-1000 | ALREADY_LISTENING |
| 2623-1001 | ALREADY_CONNECTING |
| 2623-1002 | ALREADY_CONNECTED |
| 2623-1003 | TARNSPORT_ALREADY_STOPPED |
| 2623-1004 | IN_PROGRESS |
| 2623-1005 | UNRESOLVED_HOSTNAME |
| 2623-1006 | SOCKET_CREATION_FAILURE |
| 2623-1007 | SOCKET_CONNECTION_FAILURE |
| 2623-1008 | SOCKET_CONNECTION_TIMEOUT |
| 2623-1009 | HTTP_REQUEST_FAILURE |
| 2623-1010 | HTTP_REQUEST_TIMEOUT |
| 2623-1011 | WEBSOCK_HANDSHAKE_FAILURE |
| 2623-1012 | SSL_CREATION_FAILURE |
| 2623-1013 | SSL_OPERATION_FAILURE |
| 2623-1014 | SSL_HANDSHAKE_FAILURE |
| 2623-1015 | SSL_CONTEXT_CREATION_FAILURE |
| 2623-1016 | EXCEEDED_MAXIMUM_SIZE_BY_ENCRYPTION |
| 2623-1017 | HTTPS_PROXY_REQUEST_FAILURE |
| 2623-1018 | HTTPS_PROXY_REQUEST_TIMEOUT |
| 2623-1019 | DISCONNECTED_ACTIVE |
| 2623-1020 | DISCONNECTED_PASSIVE |
| 2623-1021 | KEEPALIVE_TIMEOUT |
| 2623-1022 | PROTOCOL_VER_MISMATCH |
| 2623-1023 | DDL_HASH_MISMATCH |
| 2623-1024 | APP_PROTOCOL_VER_MISMATCH |
| 2623-1025 | GET_PROXY_SETTING_FAILURE |
| 2623-1026 | LOGIN_TIMEOUT |
| 2623-1027 | INVALID_URL |
| 2623-1028 | UNKNOWN_PROTOCOL_TYPE |
| 2623-1029 | PROTOCOL_INITIALIZE_FAILURE |
| 2623-1030 | PROTOCOL_LISTENING_FAILURE |
| 2623-1031 | ALREADY_CONNECTION_CLOSED |
| 2623-1032 | NOT_ENOUGH_DATA |
| 2623-1033 | KCP_CREATE_FAILURE |
| 2623-1034 | NOT_ENOUGH_KDP_SOCKET_POOL |
| 2623-1035 | KCP_ILLEGAL_PARAM |
| 2623-1036 | KCP_FAILURE |
| 2623-1037 | NOT_ENOUGH_KDP_RECEIVE_BUFFER |
| 2623-1038 | TOO_MANY_OPEN_SOCKETS |
| 2623-1039 | SSL_HANDSHAKE_TIMEOUT |
| 2623-1040 | WEBSOCK_HANDSHAKE_TIMEOUT |
| 2623-1041 | PROTOCOL_CONNECTING_FAILURE |
| 2623-2000 | UNAUTHORIZED |
| 2623-2001 | PROXY_AUTH_FAILURE |
| 2623-2002 | PROXY_BASIC_AUTH_FAILURE |
| 2623-2003 | PROXY_DIGEST_AUTH_FAILURE |
| 2623-3000 | DDL_HASH_NOT_SET |
| 2623-3001 | MODE_IS_CLIENT |
| 2623-3002 | MODE_IS_SERVER |
| 2623-3003 | INVALID_NSO_KEY |
| 2623-3004 | INVALID_NODE_ID |
| 2623-3005 | NSO_CLONE_UNRECEIVED |
| 2623-3006 | APP_PROTOCOL_VER_NOT_SET |
| 2623-3007 | ILLEGAL_NODE |
| 2623-3008 | RPC_CALLING_ALREADY_FAILED |
| 2623-3009 | RPC_CALLBACK_FAILURE |
| 2623-3010 | ILLEGAL_RPC_CALLED |
| 2623-3011 | RTT_STAT_UNMEASURED |
| 2623-8000 | NN_SSL_CONNECTION_CLOSED |
| 2623-8001 | NN_SSL_ERROR_LOWER |
| 2623-8002 | NN_SSL_INSUFFICIENT_MEMORY |
| 2623-8003 | NN_SSL_INTERNAL_LOGIC_ERROR |
| 2623-8004 | NN_SSL_INVALID_REFERENCE |
| 2623-8005 | NN_SSL_IO_TIMEOUT |
| 2623-8006 | NN_SSL_IO_WOULD_BLOCK |
| 2623-8007 | NN_SSL_RESOURCE_BUSY |
| 2623-8008 | NN_SSL_RESOURCE_MAX |
| 2623-8009 | NN_SSL_VERIFY_CERT_FAILED |
| 2623-8010 | NN_SSL_RESULT_CONNECTION_RESET |
| 2623-8011 | NN_SSL_RESULT_CONNECTION_ABORTED |
| 2623-8012 | NN_SSL_RESULT_SOCKET_SHUTDOWN |
| 2623-8013 | NN_SSL_RESULT_NETWORK_DOWN |
| 2623-9000 | SERVER_MAINTENANCE |
| 2623-9999 | Invalid error code |

# Coral Error Codes
| Error code | Name |
| --- | --- |
| 2815-2101 | SmartDeviceVoiceChat::Unknown |
| 2815-2102 | SmartDeviceVoiceChat::InvalidArgument |
| 2815-2103 | SmartDeviceVoiceChat::InvalidResponse |
| 2815-2104 | SmartDeviceVoiceChat::InvalidAccessToken |
| 2815-2105 | SmartDeviceVoiceChat::Unauthorized |
| 2815-2106 | SmartDeviceVoiceChat::AccessError |
| 2815-2107 | SmartDeviceVoiceChat::UserNotFound |
| 2815-2108 | SmartDeviceVoiceChat::RoomNotFound |
| 2815-2109 | SmartDeviceVoiceChat::RoomNotActivated |
| 2815-2110 | SmartDeviceVoiceChat::ApplicationNotSupported |
| 2815-2111 | SmartDeviceVoiceChat::InternalServerError |
| 2815-2112 | SmartDeviceVoiceChat::ServiceUnavailable |
| 2815-2113 | SmartDeviceVoiceChat::UnexpectedError |
| 2815-2114 | SmartDeviceVoiceChat::UnderMaintenance |
| 2815-2115 | SmartDeviceVoiceChat::ServiceNoLongerAvailable |
| 2815-2116 | SmartDeviceVoiceChat::AccountTemporarilyDisabled |
| 2815-2117 | SmartDeviceVoiceChat::PermissionDenied |
| 2815-2118 | SmartDeviceVoiceChat::NetworkServiceLicenseRequired |
| 2815-2119 | SmartDeviceVoiceChat::AccountLibraryError |
| 2815-2120 | SmartDeviceVoiceChat::GameModeNotFound |