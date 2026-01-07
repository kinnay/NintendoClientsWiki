Table of contents:

* [Switch 2](#switch-2)
* [Switch](#switch)
* [Wii U](#wii-u)
* [3DS](#3ds)
* [Mobile apps](#mobile-apps)
* [Developers](#developers)
* [Internal](#internal)

# Switch 2
#### Connection Test ([docs](Connection-Test))
* `https://api.p01.lp1.ctest.srv.nintendo.net`
* `https://ctest-dl.p01.lp1.ctest.srv.nintendo.net`
* `https://ctest-ul.p01.lp1.ctest.srv.nintendo.net`
* `https://ctest.p01.ctest.srv.nintendo.net`
* `https://ctest.cdn.nintendo.net`

#### Device Authentication
* `https://dauth.p01.lp1.ndas.srv.nintendo.net`

#### Application Authentication
* `https://aauth.p01.lp1.ndas.srv.nintendo.net`

#### Switch Users ([docs](BAAS-Server))
* `https://e0d67c509fb203858ebcb2fe3f88c2aa.baas.nintendo.com`
* `https://cdn-image-e0d67c509fb203858ebcb2fe3f88c2aa.baas.nintendo.com`

#### Nintendo Accounts ([docs](Account-Server-(Switch)))
* `https://accounts.nintendo.com`
* `https://cdn.accounts.nintendo.com`
* `https://api.accounts.nintendo.com`
* `https://c-lp1.accounts.nintendo.com`

#### Game Servers (NPLN) ([docs](NPLN-Servers))
* `<tenant id>.lp1.t.npln.srv.nintendo.net` (game server)
  * **Example:** `t-e96531c6-lp1.lp1.t.npln.srv.nintendo.net`
* `npln-lp1-latency-<region>-<id>-green-agones.lp1.t.npln.srv.nintendo.net` (latency measurement)
  * **Example:** `npln-lp1-latency-eu-01-green-agones.lp1.t.npln.srv.nintendo.net`
* `s01.lp1.s.npln.srv.nintendo.net` (STUN)
* `s01.lp1.u.npln.srv.nintendo.net` (TURN)

#### eLicenses
* `https://dragons.p01.lp1.dragons.nintendo.net`
* `https://dragonst.p01.lp1.dragons.nintendo.net`
* `https://tigers.p01.lp1.dragons.nintendo.net`

#### Push Notifications
* `https://god.p01.lp1.penne.srv.nintendo.net`
* `https://val.p01.lp1.penne.srv.nintendo.net`
* `https://fro-1.p01.lp1.penne.srv.nintendo.net`
* `https://fro-2.p01.lp1.penne.srv.nintendo.net`

#### System Updates
* `https://sun.p01.lp1.d4c.srv.nintendo.net`
* `https://atumn.p01.lp1.d4c.srv.nintendo.net`
* `https://aqua.p01.lp1.d4c.srv.nintendo.net`

#### Content Servers
* `https://tagaya.p01.lp1.eshop.nintendo.net`
* `https://beach.p01.lp1.eshop.nintendo.net`
* `https://pearljam.p01.lp1.eshop.nintendo.net`
* `https://pushmo.p01.lp1.eshop.nintendo.net`
* `https://superfly.p01.lp1.d4c.srv.nintendo.net`
* `https://veer.p01.lp1.d4c.srv.nintendo.net`
* `https://atum.p01.lp1.d4c.srv.nintendo.net`
* `https://atum-img-lp1.cdn.nintendo.net`

#### Online Save Storage
* `https://storage.p01.lp1.scsi.srv.nintendo.net`
* `https://policy.p01.lp1.scsi.srv.nintendo.net`
* `scsi-upload-lp1.s3.us-west-2.amazonaws.com`

#### Telemetry ([docs](Telemetry-Servers))
* `https://receive.p01.lp1.dg.srv.nintendo.net`
* `https://receive.p01.lp1.er.srv.nintendo.net`

#### NAT Check ([docs](NAT-Check-Server))
* `nncs1.p01.lp1.n.n.srv.nintendo.net`
* `nncs2.p01.lp1.n.n.srv.nintendo.net`
* `nncs1-lp1.n.n.srv.nintendo.net`
* `nncs2-lp1.n.n.srv.nintendo.net`

#### System Transfer
* `https://transfer.p01.lp1.banco.srv.nintendo.net`
* `https://download.p01.lp1.banco.srv.nintendo.net`

#### Online Play Invitations ([docs](Online-Play-Invitation-Server))
* `https://app.lp1.five.nintendo.net`

#### News
* `https://list.p01.lp1.bcat.srv.nintendo.net`
* `https://topics.p01.lp1.bcat.srv.nintendo.net`
* `https://data.p01.lp1.bcat.srv.nintendo.net`
* `https://web.p01.lp1.bcat.srv.nintendo.net`

#### Game Chat
* `https://enishi.p01.lp1.idobata.srv.nintendo.net`
* `https://sebumi.p01.lp1.idobata.srv.nintendo.net`

#### Album Upload
* `api.p01.lp1.nega.srv.nintendo.net`
* `nega-lp1-upload.s3.us-east-1.amazonaws.com`

#### Other Servers
* `https://bvc.p01.lp1.bvc.srv.nintendo.net` (browser version check)
* `https://idbe-p01.cdn.nintendo.net` ([icon data](IDBE-Server))
* `https://nemof.p01.lp1.nemo.srv.nintendo.net` (eShop videos)
* `https://gw.p01.lp1.vermillion.srv.nintendo.net` (virtual game cards)
* `https://p01.lp1.znma.srv.nintendo.net` (parental controls)
* `https://capi.lp1.op2.nintendo.net` ([NSO membership verification](NSO-Verification-Server))
* `https://p01.lp1.savanna.srv.nintendo.net` (eShop)
* `https://lp1.nso.nintendo.net` (NSO applet)
* `https://fw-api.lp1.nso.nintendo.net` ([NSO rewards](NSO-Reward-Server))
* `https://service-status.p01.lp1.smn.srv.nintendo.net` (service status)
* `https://m-lp1.baas.nintendo.com`

Unknown:

* `*.p01.lp1.pegasus.srv.nintendo.net`
* `*.p01.lp1.sprofile.srv.nintendo.net`
* `*.p01.lp1.p01-aaab.srv.nintendo.net`
* `*.p01.lp1.civil.nintendo.net`
* `*.p01.lp1.ss.nintendo.net`
* `*.p01.lp1.kanawa.srv.nintendo.net`

# Switch
| Environment | Description |
| --- | --- |
| lp1 | Production |
| sd1, sp1 | Staging |
| dd1, dp1 | Game development |
| jd1 | Testing |
| td1 | System development |
| xd1, yd1, zd1 | Other |

#### Connection Test ([docs](Connection-Test))
* `http://ctest.cdn.nintendo.net`
* `http://ctest-ul-lp1.cdn.nintendo.net`
* `http://ctest-dl-lp1.cdn.nintendo.net`
* `https://api.hac.lp1.ctest.srv.nintendo.net`

#### Device Authentication ([docs](DAuth-Server))
* `https://dauth-lp1.ndas.srv.nintendo.net`
* `https://dcert-lp1.ndas.srv.nintendo.net`
* `https://dapi-lp1.ndas.srv.nintendo.net` (internal)
* `https://dadmin-lp1.ndas.mng.nintendo.net` (internal)

#### Application Authentication ([docs](AAuth-Server))
* `https://aauth.hac.lp1.ndas.srv.nintendo.net` (new)
* `https://aauth-lp1.ndas.srv.nintendo.net` (old)
* `https://acert-lp1.ndas.srv.nintendo.net`
* `https://aapi-lp1.ndas.srv.nintendo.net` (internal)
* `https://aadmin-lp1.ndas.mng.nintendo.net` (internal)

#### Switch Users ([docs](BAAS-Server))
* `https://e0d67c509fb203858ebcb2fe3f88c2aa.baas.nintendo.com` (lp1)
* `https://e97b8a9d672e4ce4845ec6947cd66ef6-sb.baas.nintendo.com` (dd1)
* `https://d9c8ea0e17f68bdeab8674c59f6fabda-sb.baas.nintendo.com` (dp1)
* `https://d78dbb1c550d43c6af49bf04c56bc094-sb.baas.nintendo.com` (jd1)
* `https://96130dc402837b377c07719e6c9514de-sb.baas.nintendo.com` (sd1)
* `https://dc219b6b3aa8e06873733fda1def0e03-sb.baas.nintendo.com` (sp1)
* `https://e03a97819c9711e59510d820a52f298a-sb.baas.nintendo.com` (td1)

#### Nintendo Accounts ([docs](Account-Server-(Switch)))
* `https://accounts.nintendo.com`
* `https://cdn.accounts.nintendo.com`
* `https://api.accounts.nintendo.com`
* `https://c-lp1.accounts.nintendo.com`

#### eLicenses ([docs](Dragons-Servers))
* `https://dragons.hac.lp1.dragons.nintendo.net`
* `https://dragonst.hac.lp1.dragons.nintendo.net`
* `https://tigers.hac.lp1.dragons.nintendo.net`
* `https://pubkey.lp1.dragons.nintendo.net`

#### Game Servers (NPLN) ([docs](NPLN-Servers))
* `<tenant id>.lp1.t.npln.srv.nintendo.net` (game server)
* `s01.lp1.s.npln.srv.nintendo.net` (STUN)
* `s01.lp1.u.npln.srv.nintendo.net` (TURN)
* `npln-lp1-latency-<region>-agones.lp1.t.npln.srv.nintendo.net` (latency measurement)

#### Game Servers (NEX)
* `g<game server id>-lp1.s.n.srv.nintendo.net` ([game server](NEX-Overview-(Game-Servers)))
* `g<game server id>-lp1.r.n.srv.nintendo.net` (P2P relay)
* `g<game server id>-lp1.p.srv.nintendo.net` ([P2P monitoring](Monitoring-Data-Protocol))

#### NAT Check ([docs](NAT-Check-Server))
* `nncs1-lp1.n.n.srv.nintendo.net`
* `nncs2-lp1.n.n.srv.nintendo.net`

#### Eagle Relay ([docs](Eagle-Protocol))
* `d7d-<server name>.g.lp1.e.srv.nintendo.net`

#### Game Server Availability ([docs](Service-Status-Server))
* `https://Service-status-lp1.cdn.nintendo.net`

#### Online Play Invitations ([docs](Online-Play-Invitation-Server))
* `https://app.lp1.five.nintendo.net`

#### Smartphone Services ([docs](ZNC-Server))
* `https://api-lp1.znc.srv.nintendo.net`
* `https://web-lp1.znc.srv.nintendo.net`

#### Online Save Storage ([docs](OLSC-Servers))
* `https://storage.lp1.scsi.srv.nintendo.net`
* `https://migration.lp1.scsi.srv.nintendo.net`
* `https://storage.lp1.sata.srv.nintendo.net`
* `https://permission.lp1.sata.srv.nintendo.net`
* `https://pp.lp1.sata.srv.nintendo.net`
* `https://scsi-policy-lp1.cdn.nintendo.net`
* `https://lp1.sprofile.srv.nintendo.net`

#### eShop Services ([docs](REST-Services))
* `https://ecs-lp1.hac.shop.nintendo.net`
* `https://ias-lp1.hac.shop.nintendo.net`

#### eShop Applet ([docs](eShop-Applet-(Switch)))
* `https://bugyo.hac.lp1.eshop.nintendo.net`

#### System Updates
* `https://sun.hac.lp1.d4c.nintendo.net` ([system update meta](Sun-Server))
* `https://atumn.hac.lp1.d4c.nintendo.net` ([system update content](Atumn-Server))
* `https://aqua.hac.lp1.d4c.nintendo.net` ([system update requirements](Aqua-Server))

#### Game Content (Metadata)
* `https://tagaya.hac.lp1.eshop.nintendo.net` ([title version list](Tagaya-Server-(Switch)))
* `https://beach.hac.lp1.eshop.nintendo.net`
* `https://pearljam.hac.lp1.eshop.nintendo.net`
* `https://pushmo.hac.lp1.eshop.nintendo.net`
* `https://superfly.hac.lp1.d4c.nintendo.net`
* `https://veer.hac.lp1.d4c.nintendo.net` ([vendor weights](Veer-Server))

#### Game Content (Data) ([docs](Atum-Server))
* `https://atum.hac.lp1.d4c.nintendo.net` (Akamai)
* `https://atum-4ff.hac.lp1.d4c.nintendo.net` (Lumen)
* `https://atum-eda.hac.lp1.d4c.nintendo.net` (LLNW)
* `https://atum-5a8.hac.lp1.d4c.nintendo.net` (Fastly)
* `https://atum-f03.hac.lp1.d4c.nintendo.net` (Cloudflare)

#### Push Notifications
Old ([docs](NPNS-Servers)):
* `https://consumer.lp1.npns.srv.nintendo.net`
* `https://broker.lp1.npns.srv.nintendo.net`
* `https://provider-lp1.npns.srv.nintendo.net`
* `https://app-a03.lp1.npns.srv.nintendo.net`
* `https://app-b01.lp1.npns.srv.nintendo.net`

New ([docs](Penne-Servers)):
* `https://god.hac.lp1.penne.srv.nintendo.net`
* `https://val.hac.lp1.penne.srv.nintendo.net`
* `https://fro-8.hac.lp1.penne.srv.nintendo.net`

#### Telemetry ([docs](Telemetry-Servers))
* `https://receive-lp1.dg.srv.nintendo.net` (play reports)
* `https://realtime-receive-lp1.dg.srv.nintendo.net`
* `https://receive-lp1.er.srv.nintendo.net` (error reports)
* `https://sprofile-lp1.cdn.nintendo.net`

#### News ([docs](BCAT-Servers))
* `https://bcat-topics-lp1.cdn.nintendo.net`
* `https://bcat-list-lp1.cdn.nintendo.net`
* `https://bcat-data-lp1.cdn.nintendo.net`

#### Parental Controls ([docs](Parental-Controls))
* `https://api-lp1.pctl.srv.nintendo.net`
* `https://parentalcontrols-movie-lp1.cdn.nintendo.net`

#### System Transfer
* `https://transfer.hac.lp1.banco.srv.nintendo.net`
* `https://download.hac.lp1.banco.srv.nintendo.net`

#### Other Servers
* `https://mii-secure-lp1.cdn.nintendo.net` (mii images)
* `https://idbe-hac.cdn.nintendo.net` ([icon data](IDBE-Server))
* `https://nemof.hac.lp1.nemo.srv.nintendo.net` (eShop videos)
* `https://lp1.nso.nintendo.net` (NSO applet)
* `https://fw-api.lp1.nso.nintendo.net` ([NSO rewards](NSO-Reward-Server))
* `https://capi.lp1.op2.nintendo.net` ([NSO membership verification](NSO-Verification-Server))
* `https://api-lp1.frs.srv.nintendo.net` ([friends](Friends-API))
* `https://api.hac.lp1.acbaa.srv.nintendo.net` ([Animal Crossing API](https://github.com/Kinnay/NintendoClients/wiki/AC:NH-Server))
* `https://web-lp1.share.srv.nintendo.net`
* `https://bvc-hac-lp1.cdn.nintendo.net` (browser version check)
* `https://api.sect.srv.nintendo.net`
* `https://gw.hac.lp1.vermillion.srv.nintendo.net` ([virtual game cards](Vermillion-Server))

# Wii U
#### Account Server ([docs](Account-Server))
* `https://account.nintendo.net`
* `https://game-dev.account.nintendo.net`
* `https://system-dev.account.nintendo.net`
* `https://library-dev.account.nintendo.net`
* `https://staging.account.nintendo.net`

#### Mii Images
* `https://mii-secure.account.nintendo.net`
* `https://mii-secure.cdn.nintendo.net`
* `https://mii-images.cdn.nintendo.net`
* `https://game-dev-mii-images.cdn.nintendo.net`
* `https://system-dev-mii-images.cdn.nintendo.net`
* `https://library-dev-mii-images.cdn.nintendo.net`
* `https://staging-mii-images.cdn.nintendo.net`

#### NAT Check Server ([docs](NAT-Check-Server))
* `nncs1.app.nintendowifi.net`
* `nncs2.app.nintendowifi.net`

#### Hpp Server ([docs](Hpp-Server))
* `https://hpp-<game server id>-<environment>.n.app.nintendo.net`

#### Miiverse
* `https://discovery.olv.nintendo.net`

#### Title Version List ([docs](Tagaya-Server))
* `https://tagaya.wup.shop.nintendo.net`

#### eShop API ([docs](Ninja-Server))
* `https://ninja.wup.shop.nintendo.net`

#### eShop Website
* `https://geisha-wup.cdn.nintendo.net`

#### eShop Services ([docs](SOAP-Services))
* `https://cas.wup.shop.nintendo.net`
* `https://ecs.wup.shop.nintendo.net`
* `https://ias.wup.shop.nintendo.net`
* `https://nus.wup.shop.nintendo.net`

#### Other eShop Servers
* `https://ccs.wup.shop.nintendo.net`
* `https://pls.wup.shop.nintendo.net`
* `https://pushmo.wup.shop.nintendo.net`
* `https://pushmore.wup.shop.nintendo.net`
* `https://samurai.wup.shop.nintendo.net`
* `https://samurai-wup.cdn.nintendo.net`
* `https://kanzashi-wup.cdn.nintendo.net`
* `https://kanzashi-movie-wup.cdn.nintendo.net`
* `https://samuraicdndev1-wup.cdn.nintendo.net`
* `https://geishacdndev1-wup.cdn.nintendo.net`
* `https://gw.sgks.shop.nintendo.net`

#### BOSS
* `https://npvk.app.nintendo.net`
* `https://npvk-dev.app.nintendo.net`
* `https://npts.app.nintendo.net`
* `https://nppl.app.nintendo.net`

#### Icon Data ([docs](IDBE-Server))
* `https://idbe-wup.cdn.nintendo.net`
* `https://idbe-ctr.cdn.nintendo.net`

#### VC Manuals ([docs](VC-Manual-Server))
* `https://m1.nintendo.net`

#### Other Servers
* `https://nintendojp.d1.sc.omtrdc.net`
* `https://wiiu-ssl-static.ubi.com`

# 3DS
#### Connection Test
* `http://conntest.nintendowifi.net`

#### Account Server ([docs](NASC-Server))
* `https://nasc.nintendowifi.net`
* `https://nasc.dev.nintendowifi.net`
* `https://nasc.test.nintendowifi.net`

#### Hpp Server ([docs](Hpp-Server))
* `https://hpp-<game server id>-<environment>.n.app.nintendo.net`

#### eShop
* `https://ccs.c.shop.nintendowifi.net`
* `https://nus.c.shop.nintendowifi.net`
* `https://pls.c.shop.nintendowifi.net`

#### SpotPass
* `https://l-npns.app.nintendowifi.net`
* `https://npns-dev.c.app.nintendowifi.net`
* `https://nppl.c.app.nintendowifi.net`
* `https://npul.c.app.nintendowifi.net`
* `https://npvk.app.nintendowifi.net`

#### Other Servers
* `https://ctr-o2fgs.cdn.nintendo.net`

# Mobile Apps
#### General
* `https://accounts.nintendo.com`
* `https://api.accounts.nintendo.com`
* `https://cdn-image-e0d67c509fb203858ebcb2fe3f88c2aa.baas.nintendo.com` (user profile images)
* `https://cdn-mii.accounts.nintendo.com` (mii images)
* `https://atum-img-lp1.cdn.nintendo.net` (game icons)

#### Nintendo Switch App
General:
* `https://api-lp1.znc.srv.nintendo.net`
* `https://cdn.znc.srv.nintendo.net`
* `https://media-dl.wc.lp1.nega.srv.nintendo.net` (album downloads)

Apps:
* `https://web.sd.lp1.acbaa.srv.nintendo.net` (NookLink)
* `https://app.smashbros.nintendo.net` (Smash World)
* `https://www-aaaba-lp1-hac.cdn.nintendo.net` (Smash World)
* `https://app.splatoon2.nintendo.net` (SplatNet 2)
* `https://api.lp1.av5ja.srv.nintendo.net` (SplatNet 3)
* `https://api.lp1.usagi.srv.nintendo.net` (SplatNet 3)
* `https://api.lp1.87abc152.srv.nintendo.net` (Zelda Notes)

#### Nintendo Music
* `251737943c34c5e6ae451f19ff36c2bb.baas.nintendo.com`
* `https://api.m.nintendo.com`
* `https://image-assets.m.nintendo.com`
* `https://media-assets.m.nintendo.com`

#### Nintendo Store
* `https://cms-front.znej.nintendo.com`
* `https://app-api.znej.nintendo.com`

#### Nintendo Today
* `https://55f574e737db5d869cac906761c0c37e.baas.nintendo.com`
* `https://prod-server.de4taiqu.srv.nintendo.net`
* `https://prod-znsa.de4taiqu.srv.nintendo.net`
* `https://prod-webview-znsa.de4taiqu.srv.nintendo.net`

#### Parental Controls
* `https://app.lp1.znma.srv.nintendo.net` (parental controls)

#### Super Mario Run
* `https://1d73367a8bc4b849f5286dc68416acfd.baas.nintendo.com`
* `https://api.supermariorun.com`
* `https://download-cdn-supermariorun.akamaized.net`

#### Mario Kart Tour
* `https://a6913b7b80402974409b47079c29d775.baas.nintendo.com`
* `https://api.mariokarttour.com`
* `https://download-cdn-mariokarttour.akamaized.net`

# Developers
* https://developer.nintendo.com (developer portal)
* https://ndid.mng.nintendo.net (SSO login)
* https://omas.mng.nintendo.net (online title management for 3DS/Wii U)
* https://omas2.mng.nintendo.net (online title management for Switch)
* https://slim.mng.nintendo.net (software legal information management)
* https://dashboard.d.npln.srv.nintendo.net (NPLN dashboard)
* https://nmas.mng.nintendo.net (NEX server management old)
* https://nmas.tool.n.mng.nintendo.net (NEX server management new)
* https://ncms3.mng.nintendo.net (Nintendo content management)
* https://sd-report.mng.nintendo.net (save data tool)
* https://crash-report.wc.lp1.er.srv.nintendo.net (crash report tool)
* https://webapp.bmas2.srv.nintendo.net (ban management)
* https://smas.mng.nintendo.net (service stats)
* https://sst.mng.nintendo.net (shop sales tool)
* https://dg.mng.nintendo.net (play report tool)
* https://door-d4c.mng.nintendo.net (ROM management)

# Internal
* `nexred.nintendo.co.jp` (Redmine issue tracker for [NEX](NEX-Overview-(Game-Servers)))
* `devbts30.nintendo.co.jp`
* `devproxy.nintendo.co.jp`
* `spdlybra.nintendo.co.jp`
* `devhipchat.boy.nintendo.co.jp`
* `ndo-gitlab.boy.nintendo.co.jp`