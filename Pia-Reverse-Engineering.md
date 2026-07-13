This page contains some reverse engineering notes for the Pia library.

A list of games with Pia and function names can be found [here](https://kinnay.github.io/view.html?page=switch&pia=1&syms=1).

## LDN Passphrase
A list of passphrases can be found [here](LDN-Passphrases).

The LDN passphrase is passed to the Pia library through `nn::pia::local::LdnCreateSessionSetting::SetWirelessCryptoKey` or `nn::pia::local::LdnJoinSessionSetting::SetWirelessCryptoKey`.

When [ENL](ENL-Protocol) is used, the passphrase is configured through `enl::PiaMatchmakeCondition::setPassPhrase`.

## Pia Game Key
A list of game keys can be found [here](Pia-Game-Keys).

The game key is passed to the Pia library through `nn::pia::session::Session::Startup`. A good strategy to find the game key is to look for references to `nn::pia::common::CryptoSetting`.

When [ENL](ENL-Protocol) is used, the game key is created with `enl::PiaMatchmakeCondition::makeRandomCryptoKey`. Note that this function is inlined in recent games, which makes it a bit more difficult to find.