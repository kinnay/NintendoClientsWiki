[NEX](NEX-Overview-(Game-Servers)) > Kerberos Authentication
---

This page describes how user authentication works on game servers.

Before reading this page, make sure you have a basic understanding of how the game servers work in general.

* [Overview](#overview)
* [Credentials](#credentials)
* [Special accounts](#special-accounts)
* [Kerberos tickets](#kerberos-tickets)
* [Password authentication](#password-authentication)
* [Token authentication](#token-authentication)
* [Key derivation](#key-derivation)
* [Ticket format](#ticket-format)
* [Terminology](#terminology)
* [Exercise](#exercise)

## Overview
NEX uses a simplified form of Kerberos authentication. To log in on a game server, one must first connect to the authentication server. This server only provides a single service: the [ticket granting service](Authentication-Protocol). The ticket granting service provides the location of the secure server, and a ticket that is required to establish a connection with the secure server. This is explained in more detail below.

![](https://www.dropbox.com/s/0wjj7trxgek7z8u/kerberos_basic.png?raw=1)

On 3DS and Wii U servers, authentication is password-based (see [password authentication](#password-authentication)). On Switch servers, users must provide an id token to log in (see [authentication with token](#token-authentication)).

## Credentials
Game server accounts are separate from other Nintendo accounts. Username and password are generated automatically and can not be changed by normal users. Credentials are obtained in a platform specific way:

<table>
  <tr>
    <td><b>3DS</b></td><td>A game server account is created with <a href="https://github.com/kinnay/NintendoClients/wiki/Account-Management-Protocol#27-nintendocreateaccount">NintendoCreateAccount</a> the first time you go online.</td>
  </tr>
  <tr>
    <td><b>Wii U</b></td><td>Username and password are requested from the [[account server]] (/provider/nex_token/@me)</td>
  </tr>
  <tr>
    <td><b>Switch</b></td><td>Normal user accounts don't have a password anymore. Instead, they must provide an id token to log in. This token (and your username) can be retrieved by logging in on the <a href="BAAS-Server">BAAS server</a> after acquiring a <a href="DAuth-Server">device token</a> and an <a href="AAuth-Server">application token</a>.</td>
  </tr>
</table>

There's also a bunch of [special accounts](#special-accounts) on all game servers.

## Special Accounts
The password of the guest account is `MMQea3n!fsik`, but Nintendo has changed this password on all Wii U and 3DS servers except for the friend server. On Switch servers, all accounts except for Quazal Rendez-Vous and SandboxProbe are deleted.

The Quazal Authentication account represents the authentication server, and the Quazal Rendez-Vous account represents the secure server. This is relevant for [Kerberos authentication](#kerberos-tickets).

#### 3DS / Wii U:
| PID | Name |
| --- | --- |
| 1 | Quazal Authentication |
| 2 | Quazal Rendez-Vous |
| 100 | guest |
| 101 | Administrator |
| 102 | eval |
| 103 | SandboxProbe |
| 104 | LobbyAdministrator |
| 110 | BackgroundPlayer0 |

#### Switch:
| PID | Name |
| --- | --- |
| 243564795342340018 | Quazal Authentication |
| 257049437023956657 | Quazal Rendez-Vous |
| 564330319085596911 | guest |
| 584465510887342041 | Administrator |
| 621476855497894457 | eval |
| 693188807183308752 | SandboxProbe |
| 1279596992968541952 | LobbyAdministrator |
| 1405107338776927048 | BackgroundPlayer0 |

## Kerberos Tickets
Kerberos authentication allows a **source user** to establish a secure connection with a **target user**. In practice, the **target user** is always Quazal Rendez-Vous (which represents the secure server).

A Kerberos ticket, which the **source user** receives from the authentication server, contains the following information, encrypted with the **source key**:

1. A random session key. This will be used in communication with the **target user**.
2. The principal id of the **target user**.
3. The internal ticket.

After decrypting the Kerberos ticket, the **source user** sends the internal ticket to the **target user** during connection establishment. The internal ticket contains the following information, encrypted with the **target key**:

1. The time at which the ticket was issued. If the ticket is older than 2 minutes, the **target user** aborts the connection.
2. The principal id of the **source user**. This way, the **target user** knows who is connecting.
3. The session key.

The **source key** is a key that is only known by the source user. The **target key** is a key that is only known by the target user.

## Password Authentication
Your password is never sent to the authentication server. Instead, it is used to derive the **source key**. This is a simple but effective authentication scheme: if you don't know the password you can't decrypt the [ticket](#kerberos-tickets), and therefore you cannot establish a connection with the **target user**.

The ticket can be retrieved with one of the following methods:
1. **[Login / ValidateAndRequestTicket](Authentication-Protocol#1-login)**. This method takes a single parameter: the username. The response contains your principal id, the location of the secure server, and a ticket that is encrypted with the key that is derived from your password.
2. **[LoginEx / ValidateAndRequestTicketWithCustomData](Authentication-Protocol#2-loginex)**. This method takes extra data in addition to the username, such as the server version that the client is expecting and a token that the client received along with its username and password. The game server does not seem to verify the token.
3. **[RequestTicket](Authentication-Protocol#3-requestticket)**. This method is a bit different. It requires that you know your principal id in advance (for example, from the **[Login](Authentication-Protocol#1-login)** method). The **[RequestTicket](Authentication-Protocol#3-requestticket)** method explicitly takes a **source** and **target user** id and returns an appropriate ticket. It's possible that the **target user** of the ticket that is returned by the **[Login](Authentication-Protocol#1-login)** or **[LoginEx](Authentication-Protocol#2-loginex)** method does not belong to the secure server. In that case the **[RequestTicket](Authentication-Protocol#3-requestticket)** method can be used to get the correct ticket.

To figure out if it needs to request a new ticket with the **[RequestTicket](Authentication-Protocol#3-requestticket)** method, NEX compares the **target user** id in the decrypted ticket against the user id in connection info for the secure server.

## Token Authentication
On Switch servers, authentication works slightly differently. Special accounts, such as **guest**, still use [password-based authentication](#password-authentication), but normal users must provide an id token to log in. If an id token is not provided, or if it is invalid, the server refuses to hand out a ticket and returns an error code instead.

Because there is no way to give a token to **[ValidateAndRequestTicket](Authentication-Protocol#1-login)** and **[RequestTicket](AuthenticationProtocol#3-requestticket)**, these methods cannot be used for a normal user account on Switch servers. Instead, one of the following methods must be used, depending on the NEX version:

1. **[ValidateAndRequestTicketWithCustomData](Authentication-Protocol#2-loginex)** (before NEX 4.4.0). The id token is sent to the server in the AuthenticationInfo parameter. If the id token is valid, the **source key** is sent to the client in the response, along with ticket.
2. **[ValidateAndRequestTicketWithParam](Authentication-Protocol#6-validateandrequestticketwithparam)** (NEX 4.4.0 and later). This method is the same as above, but with slightly different request and response parameters.

## Key Derivation
If password-based authentication is used, the **source** and **target key** are generated as follows:

**3DS / Wii U**: The password is MD5-hashed `65000 + pid % 1024` times.

**Switch**: The key is `MD5(MD5(password) + PACK("<Q", pid))`

Here, `pid` and `password` are the principal id and password of the **source** or **target user**.

## Ticket Format
The following encryption algorithm is used: first, the ticket is encrypted with RC4. Then a HMAC-MD5 of the encrypted data is appended. The decryption process is the reverse: first check the HMAC, then decrypt.

The [Kerberos ticket](#kerberos-tickets) contains the following data, encrypted with the **source key**:

| Type | Description |
| --- | --- |
| Bytes | A random session key |
| [PID] | The principal id of the **target user** |
| [Buffer] | [Internal ticket data](#internal-ticket-format) |
| [Buffer] | Optional null-terminated string (contains [JSON attributes](#json-attributes) on new game servers) |

The length of the session key is always 32 bytes, except in communication with the 3DS / Wii U friends server, in which case it's 16 bytes.

The optional string is not always present. The client checks whether the ticket has more data to determine whether there is an optional string. The optional string is supported in NEX version 4.3.x and later.

### Internal Ticket Format
The format of the internal ticket was updated at some point. In the old format, the internal ticket data was encrypted directly with the **target key**. In the new format, a random key is sent along with the internal ticket in plain text, which is combined with the **target key** to derive the final encryption key.

#### Old version
| Type | Description |
| --- | --- |
| [Ticket Info](#ticket-info) | Encrypted ticket info |

#### New version
| Type | Description |
| --- | --- |
| [Buffer] | Random key |
| [Buffer] | Encrypted ticket info |

The final encryption key is calculated as follows: `MD5(target_user_key + random_key)`

#### Ticket Info
The date time is used to check ticket expiration. A ticket is valid for exactly 2 minutes.

**Note:** the structure below is outdated. Recent game servers return a larger structure with an unknown format.

| Type | Description |
| --- | --- |
| [DateTime] | The time at which the ticket was issued |
| [PID] | The principal id of the **source user** |
| Bytes | The session key |

### JSON Attributes
If present, the JSON attributes contain the following null-terminated string:

```json
{"v": 1, "att": 2, "pid": 11607394848327368017, "mi": {"ms": -1, "mp": 1, "cpa": true}}
```

These fields have the following meaning.

| Field | Description |
| --- | --- |
| `v` | Version (always 1) |
| `att` | Token type (0=3DS, 1=Wii U, 2=Switch) |
| `pid` | User id |
| `mi` | Unknown |

In some cases, the attributes have an `exp` field that contains the expiration timestamp in seconds.

## Terminology
* **Authentication server:** the server that generates the tickets. This server only provides a single service: the ticket granting service.
* **Principal id:** this is simply a user id.
* **Secure server:** the actual game server. To establish a connection with the secure server, one must first request a ticket from the authentication server.
* **Source key:** a key that is only known by the source user (usually derived from its password).
* **Source user:** the user that requests the ticket, i.e. the user that wants to establish a connection with a target user.
* **Target key:** a key that is only known by the target user (always derived from its password).
* **Target user:** the user that the source user wants to establish a connection with. In practice, the target user is always Quazal Rendez-Vous (which represents the secure server).
* **Ticket granting service:** the service that generates the tickets. This service is provided by the authentication server.

## Exercise
Suppose we want to log in on a Switch server as guest. We received the following ticket from the authentication server:

```
86e5b91add71b984c713dab188cdcabc1b4298f922021fe4be049be91b279489
0de22074734bfd9e75ac3f4ecbb31155933845c601dc8b45d5c7f8e055d80a3c
cef3ee876cbc64c4a7802f20c126be6c73398d367c934902b7cfe7a187d1d38e
6bfe18c564217c53a01f11002b19cf7c5361ffb65ba10fe87e0cc8005a1a674a
fd7461c5154b193a62ccaad8e1a9a28d92645e69
```

1. Try to decode the ticket. Everything you need to know is explained on this wiki page. Extract the session key and check the principal id of the **target user**.
2. Decode the internal ticket, assuming that the password of the Quazal Rendez-Vous account is `5MYiXWwtBuI6JzhU`. Check if the session key is the same. Check if the principal id of the user is what you expect. Decode the timestamp. When was the ticket issued?

Don't forget to check the HMAC before decryption.

[Buffer]: NEX-Common-Types#buffer
[PID]: NEX-Common-Types#pid
[DateTime]: NEX-Common-Types#datetime