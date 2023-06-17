As explained on the [Game Server Overview](NEX-Overview-(Game-Servers)) page, NEX is based on Quazal Rendez-Vous. Many protocols come from the original Quazal Rendez-Vous library, but Nintendo also implemented some new protocols.

The servers also seem to use some [internal protocols](NEX-Internal-Protocols).

See also: [[RMC Protocol]]

## Common Protocols
| ID | Protocol |
| --- | --- |
| 1 | [Remote log device](Remote-Log-Device-Protocol) |
| 3 | [NAT traversal](NAT-Traversal-Protocol) |
| 10 | [Ticket granting](Authentication-Protocol) |
| 11 | [Secure connection](Secure-Protocol) |
| 14 | [Notification events](Notification-Protocol) |
| 18 | [Health](Health-Protocol) |
| 19 | [Monitoring](Monitoring-Protocol) |
| 20 | [Friends](Friends-Protocol) |
| 21 | [Match making](Match-Making-Protocol) |
| 23 | [Messaging](Messaging-Protocol) |
| 24 | [Persistent store](Persistent-Store-Protocol) |
| 25 | [Account management](Account-Management-Protocol) |
| 27 | [Message delivery](Message-Delivery-Protocol) |
| 50 | [Match making (extension)](Match-Making-Protocol-Ext) |

## Nintendo Only
| ID | Protocol |
| --- | --- |
| 100 | [Nintendo notification events](Nintendo-Notification-Event-Protocol) |
| 101 | [Friends (3DS)](Friends-Protocol-(3DS)) |
| 102 | [Friends (Wii U)](Friends-Protocol-(Wii-U)) |
| 109 | [Matchmake extension](Matchmake-Extension-Protocol) |
| 110 | [Utility](Utility-Protocol) |
| 112 | [Ranking](Ranking-Protocol) |
| 115 | [Data store](Data-Store-Protocol) |
| 116 | [Debug](Debug-Protocol) |
| 119 | [Service item](Service-Item-Protocol) |
| 120 | [Matchmake referee](Matchmake-Referee-Protocol) |
| 121 | [Subscriber](Subscriber-Protocol) |
| 122 | [Ranking 2](Ranking-Protocol-2) |
| 123 | [AA user](AA-User-Protocol) |
| 124 | [Screening](Screening-Protocol) |

## Game-Specific
| ID | Game | Protocol |
| --- | --- | --- |
| 200 | Pokemon Bank | [Shop](Shop-Protocol-(Pokemon-Bank)) |
| 201 | Super Smash Bros. Ultimate | [Tournament](Tournament-Protocol-(SSBU)) |

## Not provided by NEX
Ubisoft games always use the original Quazal Rendez-Vous library instead of NEX. The following protocols are not implemented by NEX, but may seen in Ubisoft games:

| ID | Protocol |
| --- | --- |
| 12 | Back end management |
| 16 | [Simple authentication](Simple-Authentication-Protocol) |
| 17 | Siege |
| 26 | Competition |
| 28 | Client settings |
| 29 | [Ubi account management](Ubi-Account-Management-Protocol) |
| 30 | Geo localization |
| 31 | [News](News-Protocol) |
| 35 | [Privileges](Privileges-Protocol) |
| 36 | [Tracking 3](Tracking-Protocol-3) |
| 39 | [Localization](Localization-Protocol) |
| 42 | [Game session](Game-Session-Protocol) |
| 44 | Sub account management |
| 45 | IP to location |
| 46 | IP to location admin |
| 47 | Ubi friends |
| 48 | Skill rating |
| 49 | [Uplay win](Uplay-Win-Protocol) |
| 51 | [Title storage](Title-Storage-Protocol) |
| 53 | [User storage](User-Storage-Protocol) |
| 55 | [Player stats](Player-Stats-Protocol) |
| 60 | Spark |
| 71 | [Offline game notifications](Offline-Game-Notification-Protocol) |
| 72 | [User account management](User-Account-Management-Protocol) |
| 84 | Siege admin |
| ? | [Web notifications storage](Web-Notification-Storage-Protocol)
| ? | [User storage admin](User-Storage-Admin-Protocol)
| ? | [OLS storage](OLS-Storage-Protocol) |