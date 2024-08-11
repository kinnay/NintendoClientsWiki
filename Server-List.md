## Switch
| Environment | Description |
| --- | --- |
| lp1 | Live production |
| dd1, dp1, jd1, sd1, sp1, td1, xd1, yd1, zd1 | Development |

#### Connection Test ([docs](Connection-Test))
* http://ctest.cdn.nintendo.net
* http://ctest-ul-lp1.cdn.nintendo.net
* http://ctest-dl-lp1.cdn.nintendo.net

#### Device Authentication ([docs](DAuth-Server))
* https://dauth-lp1.ndas.srv.nintendo.net
* https://dcert-lp1.ndas.srv.nintendo.net
* https://dapi-lp1.ndas.srv.nintendo.net (internal)
* https://dadmin-lp1.ndas.mng.nintendo.net (internal)

#### Application Authentication ([docs](AAuth-Server))
* https://aauth-lp1.ndas.srv.nintendo.net
* https://acert-lp1.ndas.srv.nintendo.net
* https://aapi-lp1.ndas.srv.nintendo.net (internal)
* https://aadmin-lp1.ndas.mng.nintendo.net (internal)

#### Switch Accounts ([docs](BAAS-Server))
* https://e0d67c509fb203858ebcb2fe3f88c2aa.baas.nintendo.com (lp1)
* https://e97b8a9d672e4ce4845ec6947cd66ef6-sb.baas.nintendo.com (dd1)
* https://d9c8ea0e17f68bdeab8674c59f6fabda-sb.baas.nintendo.com (dp1)
* https://d78dbb1c550d43c6af49bf04c56bc094-sb.baas.nintendo.com (jd1)
* https://96130dc402837b377c07719e6c9514de-sb.baas.nintendo.com (sd1)
* https://dc219b6b3aa8e06873733fda1def0e03-sb.baas.nintendo.com (sp1)
* https://e03a97819c9711e59510d820a52f298a-sb.baas.nintendo.com (td1)

#### Nintendo Accounts ([docs](Account-Server-(Switch)))
* https://accounts.nintendo.com
* https://cdn.accounts.nintendo.com
* https://api.accounts.nintendo.com
* https://c-lp1.accounts.nintendo.com

#### eLicenses ([docs](Dragons-Servers))
* https://dragons.hac.lp1.dragons.nintendo.net
* https://dragonst.hac.lp1.dragons.nintendo.net
* https://tigers.hac.lp1.dragons.nintendo.net
* https://pubkey.lp1.dragons.nintendo.net

#### Game Servers (NPLN) ([docs](NPLN-Servers))
* `<tenant id>.lp1.t.npln.srv.nintendo.net` (game server)
* `s01.lp1.s.npln.srv.nintendo.net` (STUN)
* `s01.lp1.u.npln.srv.nintendo.net` (TURN)
* `npln-lp1-latency-<region>-agones.lp1.t.npln.srv.nintendo.net` (latency measurement)
* https://dashboard.d.npln.srv.nintendo.net (developer dashboard)

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
* https://Service-status-lp1.cdn.nintendo.net

#### Online Play Invitations ([docs](Online-Play-Invitation-Server))
* https://app.lp1.five.nintendo.net

#### Smartphone Services ([docs](ZNC-Server))
* https://api-lp1.znc.srv.nintendo.net
* https://web-lp1.znc.srv.nintendo.net

#### Online Save Storage ([docs](OLSC-Servers))
* https://storage.lp1.scsi.srv.nintendo.net
* https://migration.lp1.scsi.srv.nintendo.net
* https://storage.lp1.sata.srv.nintendo.net
* https://permission.lp1.sata.srv.nintendo.net
* https://pp.lp1.sata.srv.nintendo.net
* https://scsi-policy-lp1.cdn.nintendo.net

#### eShop Services ([docs](REST-Services))
* https://ecs-lp1.hac.shop.nintendo.net
* https://ias-lp1.hac.shop.nintendo.net

#### eShop Applet ([docs](eShop-Applet-(Switch)))
* https://bugyo.hac.lp1.eshop.nintendo.net
* https://tagaya.hac.lp1.eshop.nintendo.net

#### Title Installation ([docs](NIM-Servers))
* https://aqua.hac.lp1.d4c.nintendo.net
* https://atum.hac.lp1.d4c.nintendo.net
* https://atumn.hac.lp1.d4c.nintendo.net ([system update content](Atumn-Server))
* https://beach.hac.lp1.eshop.nintendo.net
* https://pearljam.hac.lp1.eshop.nintendo.net
* https://pushmo.hac.lp1.eshop.nintendo.net
* https://sun.hac.lp1.d4c.nintendo.net ([system update meta](Sun-Server))
* https://superfly.hac.lp1.d4c.nintendo.net
* https://veer.hac.lp1.d4c.nintendo.net

#### Push Notifications ([docs](NPNS-Servers))
Old:
* https://consumer.lp1.npns.srv.nintendo.net
* https://broker.lp1.npns.srv.nintendo.net
* https://provider-lp1.npns.srv.nintendo.net
* https://app-a03.lp1.npns.srv.nintendo.net
* https://app-b01.lp1.npns.srv.nintendo.net

New:
* https://god.hac.lp1.penne.srv.nintendo.net
* https://val.hac.lp1.penne.srv.nintendo.net

#### Telemetry ([docs](Telemetry-Servers))
* https://receive-lp1.dg.srv.nintendo.net (play reports)
* https://receive-lp1.er.srv.nintendo.net (error reports)
* https://sprofile-lp1.cdn.nintendo.net

#### News ([docs](BCAT-Servers))
* https://bcat-topics-lp1.cdn.nintendo.net
* https://bcat-list-lp1.cdn.nintendo.net
* https://bcat-data-lp1.cdn.nintendo.net

#### Parental Controls ([docs](Parental-Controls))
* https://api-lp1.pctl.srv.nintendo.net
* https://parentalcontrols-movie-lp1.cdn.nintendo.net

#### Other Services
* https://mii-secure-lp1.cdn.nintendo.net (mii images)
* https://idbe-hac.cdn.nintendo.net ([icon data](IDBE-Server))
* https://lp1.nso.nintendo.net (NSO applet)
* https://fw-api.lp1.nso.nintendo.net (NSO rewards)
* https://capi.lp1.op2.nintendo.net ([NSO membership verification](NSO-Verification-Server))
* https://api-lp1.frs.srv.nintendo.net ([friends](Friends-API))
* https://api.hac.lp1.acbaa.srv.nintendo.net ([Animal Crossing API](https://github.com/Kinnay/NintendoClients/wiki/AC:NH-Server))
* https://web-lp1.share.srv.nintendo.net
* https://bvc-hac-lp1.cdn.nintendo.net
* https://api.sect.srv.nintendo.net

## Wii U
| Server | Description |
| --- | --- |
| - account.nintendo.net<br>- game-dev.account.nintendo.net<br>- system-dev.account.nintendo.net<br>- library-dev.account.nintendo.net<br>- staging.account.nintendo.net | [[Account server]] |
| - mii-secure.account.nintendo.net<br>- mii-secure.cdn.nintendo.net<br>- mii-images.cdn.nintendo.net<br>- game-dev-mii-images.cdn.nintendo.net<br>- system-dev-mii-images.cdn.nintendo.net<br>- library-dev-mii-images.cdn.nintendo.net<br>- staging-mii-images.cdn.nintendo.net | Mii images |
| - nncs1.app.nintendowifi.net<br>- nncs2.app.nintendowifi.net | [NAT check server](NAT-Check-Server) |
| - hpp-&lt;game server id&gt;-&lt;environment&gt;.n.app.nintendo.net | [Hpp server](Hpp-Server) |
| - discovery.olv.nintendo.net | Miiverse |
| - tagaya.wup.shop.nintendo.net | [Title version list](Tagaya-Server) |
| - ninja.wup.shop.nintendo.net | [eShop api](Ninja-Server)
| - geisha-wup.cdn.nintendo.net | eShop website |
| - cas.wup.shop.nintendo.net<br>- ecs.wup.shop.nintendo.net<br>- ias.wup.shop.nintendo.net<br>- nus.wup.shop.nintendo.net | [eShop services](SOAP-Services) |
| - ccs.wup.shop.nintendo.net<br>- pls.wup.shop.nintendo.net<br>- pushmo.wup.shop.nintendo.net<br>- pushmore.wup.shop.nintendo.net<br>- samurai.wup.shop.nintendo.net<br>- samurai-wup.cdn.nintendo.net<br>- kanzashi-wup.cdn.nintendo.net<br>- kanzashi-movie-wup.cdn.nintendo.net<br>- samuraicdndev1-wup.cdn.nintendo.net<br>- geishacdndev1-wup.cdn.nintendo.net<br>- gw.sgks.shop.nintendo.net | eShop |
| - npvk.app.nintendo.net<br>- npvk-dev.app.nintendo.net<br>- npts.app.nintendo.net<br>- nppl.app.nintendo.net | BOSS |
| - idbe-wup.cdn.nintendo.net<br>- idbe-ctr.cdn.nintendo.net | [Icon data](IDBE-Server) |
| - m1.nintendo.net | [VC Manuals](VC-Manual-Server) |
| - nintendojp.d1.sc.omtrdc.net<br>- wiiu-ssl-static.ubi.com | |

## 3DS
| Server | Description |
| --- | --- |
| - conntest.nintendowifi.net | Connection test |
| - nasc.nintendowifi.net<br>- nasc.dev.nintendowifi.net<br>- nasc.test.nintendowifi.net | [Account server](NASC-Server) |
| - hpp-&lt;game server id&gt;-&lt;environment&gt;.n.app.nintendo.net | [Hpp server](Hpp-Server) |
| - ccs.c.shop.nintendowifi.net<br>- nus.c.shop.nintendowifi.net<br>- pls.c.shop.nintendowifi.net | eShop |
| - l-npns.app.nintendowifi.net<br>- npns-dev.c.app.nintendowifi.net<br>- nppl.c.app.nintendowifi.net<br>- npul.c.app.nintendowifi.net<br>- npvk.app.nintendowifi.net | SpotPass |
| - ctr-o2fgs.cdn.nintendo.net |

## Other
| Server | Description |
| --- | --- |
| - nexred.nintendo.co.jp | Redmine issue tracker for [NEX](NEX-Overview-(Game-Servers)) |
| - devbts30.nintendo.co.jp<br>- devhipchat.boy.nintendo.co.jp | Internal dev servers |