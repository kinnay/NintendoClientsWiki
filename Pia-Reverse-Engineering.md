This page contains some reverse engineering notes for the Pia library.

A list of games with Pia and function names can be found [here](https://kinnay.github.io/view.html?page=switch&pia=1&syms=1).

## LDN Passphrase
A list of passphrases can be found [here](LDN-Passphrases).

The LDN passphrase is passed to the Pia library through `nn::pia::local::LdnCreateSessionSetting::SetWirelessCryptoKey` or `nn::pia::local::LdnJoinSessionSetting::SetWirelessCryptoKey`.

When [ENL](ENL-Protocol) is used, the passphrase is configured through `enl::PiaMatchmakeCondition::setPassPhrase`.