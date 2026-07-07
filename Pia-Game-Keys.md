In LDN and LAN mode, [Pia](Pia-Overview) derives encryption keys using a game-specific key. This page lists the game-specific key for some games.

The game-specific key is used to encrypt and/or authenticate browse request and replies in [LAN mode](LAN-Protocol), and to derive the [Pia session key](Pia-Protocol#session-key).

| Game | Key |
| --- | --- |
| Game Boy - Nintendo Switch Online | `54ddaeaedb3ce1a39f793c962bf4a36c` |
| Mario Kart 8 Deluxe | `ABCDEFGHIJKLMNOP` |
| Nintendo Switch Sports | `48545a26643c254c39107cd1f8004453` |
| Pokemon Fire Red | `83ca7fab734c34633b10183526c1e85b` |
| Pokemon Sword/Shield | `p1frXqxmeCZWFv0X` |
| Splatoon 2 | `ee182a63e216cdb1f51ad4bed8cf6508` |
| Super Mario Maker 2 | `667c18475889faab61f93ef1da180971` |

Most first-party games use [ENL](ENL-Key-Generation) to derive the game-specific key.