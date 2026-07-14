In LDN and LAN mode, [Pia](Pia-Overview) derives encryption keys using a game-specific key. This page lists the game-specific key for some games.

The game-specific key is used to encrypt and/or authenticate browse request and replies in [LAN mode](LAN-Protocol), and to derive the [Pia session key](Pia-Protocol#session-key).

| Game | Key |
| --- | --- |
| Game Boy - Nintendo Switch Online | `54ddaeaedb3ce1a39f793c962bf4a36c` |
| Mario Kart 8 Deluxe | `ABCDEFGHIJKLMNOP` |
| Nintendo Switch Sports | `48545a26643c254c39107cd1f8004453` |
| [Pokemon Brilliant Diamond](Pokemon-Brilliant-Diamon) (1.3.0) | `9900bd0cdcfa65639918bd0fc7fa6577` |
| Pokemon Fire Red | `83ca7fab734c34633b10183526c1e85b` |
| Pokemon Sword/Shield | `p1frXqxmeCZWFv0X` |
| Splatoon 2 | `ee182a63e216cdb1f51ad4bed8cf6508` |
| Splatoon 3 | `78deee82d86875782c40b15278f37815` |
| [Super Mario Maker 2](Super-Mario-Maker-2) | `667c18475889faab61f93ef1da180971` |
| Super Mario Party | `ndcube_buffet_ss` |

Most first-party games use [ENL](ENL-Key-Generation) to derive the game-specific key.