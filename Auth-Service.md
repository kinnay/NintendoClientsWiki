[NPLN](NPLN-Servers) > Auth Service
---

Full name: `nn.npln.auth.v1.Auth`

* [Overview](#overview)
* [Methods](#methods)
* [Source code](https://github.com/kinnay/NPLN-Protocols/blob/master/latest/proto/auth/v1/auth.proto)

## Overview
The auth service manages user accounts on an NPLN tenant. Before using another service, one must first obtain an access token from the auth service.

#### External Ids
Most methods of the auth service require you to provide an **external id token**. The id token can be obtained by logging in on the [BaaS server](BAAS-Server) and identifies a specific user on your Switch. It also proves that you own a specific title.

![](https://www.dropbox.com/s/wrzz0wkawmoo09b/baas_id_token.png?raw=1&x=3)

#### Accounts

The first time you provide an id token to NPLN, the server automatically creates an **account** that is tied to your **external id**. The account is shared across all tenants.

#### Users
NPLN allows you to create an arbitrary number of **users** on a tenant. Every user that is created belongs to a specific account and only exists under the given tenant. There are two ways to create a user on a tenant:
* A new user can be created manually with [CreateUser](#createuser). After creating a user manually, an access token can be obtained with [IssueToken](#issuetoken).
* Every tenant provides 16 prearranged users per account. An access token for a prearranged user can be obtained with [IssuePrearrangedUserToken](#issueprearrangedusertoken).

Every tenant also provides an anonymous user. This user is special because it does not belong to a specific account. Most services deny requests that are made by an anonymous user.

## Methods
The following methods do not require an access token:

* [CreateUser](#createuser)
* [IssueToken](#issuetoken)
* [RefreshToken](#refreshtoken)
* [IssuePrearrangedUserToken](#issueprearrangedusertoken)
* [IssueAnonymousUserToken](#issueanonymoususertoken)
* [RefreshAnonymousUserToken](#refreshanonymoususertoken)
* ValidateToken

The following methods require an access token:
* [ListUsers](#listusers)
* [DeleteUser](#deleteuser)

### CreateUser
This method creates a user on the given tenant.

```json
{
    "parent": "tenants/t-50e39f8f-lp1",
    "external_id_token": {
        "nsa_id_token": "eyJqa3UiOiJodHRwczovL2UwZDY3YzUwOWZiMjAzODU4ZWJjYjJmZTNmODhjMmFhLmJhYXMubmludGVuZG8uY29tLzEuMC4wL2NlcnRpZmljYXRlcyIsImFsZyI6IlJTMjU2Iiwia2lkIjoiNTc0Zjc0MjctN2M1NC00ODUwLTg2ZjAtNzk0Yjg5NjU1ZTJiIn0.eyJhdWQiOiJlZDllMmYwNWQyODZmN2I4Iiwic3ViIjoiOGNhOGQ3ODQyZjg2NWIyZiIsIm5pbnRlbmRvIjp7ImF0IjoxNjcwMjc2MjU2LCJhdiI6IjAwMDEiLCJobSI6dHJ1ZSwicGgiOiJHQU1FX1NFUlZFUiIsImFpIjoiMDEwMDhmNjAwOGM1ZTAwMCIsImVkaSI6ImYxZjlkNzMyMGQ5YmEwZGVkMWFkZmQ2OTgxZWNmMWY0Iiwib3BwIjoiTUVNQkVSU0hJUF9SRVFVSVJFRCJ9LCJpc3MiOiJodHRwczovL2UwZDY3YzUwOWZiMjAzODU4ZWJjYjJmZTNmODhjMmFhLmJhYXMubmludGVuZG8uY29tIiwidHlwIjoiaWRfdG9rZW4iLCJleHAiOjE2NzAyODcwNTYsImlhdCI6MTY3MDI3NjI1NiwiYnM6ZGlkIjoiNTgxZWE3ODZhOTFmMTY4OSIsImp0aSI6IjY3NDNmMDllLWQ4OTEtNGY3YS05MDgzLTMwNzlkOTgxZTk0YiJ9.6DfNTQbTmkuA3bUPwMi3oQa06Tic2D8WB5vv-45zNFxa2l_0YbhpMarbNoxsTH2v7493GaUA520mh2f_HISN1yrjCA3C3YIGGr7NWoDd_Ew97JU1uV2b26klUom4XHADUnzHOoPCu5QwoB_8Dwa3ls25oSwy5hkcNiRnsfB_d2U14bCVwdnKjzbUAXgL7k2oTP2lV2j4aD8Pu5PhKeFuZdUo8gj-5_0sP2O3w1HyywdysIGDON7GYJ1mrc36sF7kB_MfHmYr65rSoFtqN_mHVYuxSGv1C3SwtZA2K_YFjahy2mjXubu68N7eatoFoP8xe2xbevf7Q5wfujHk5yJOqw"
    }
}
```

```json
{
    "name": "tenants/t-50e39f8f-lp1/users/u-qtb6z4jkvrndteijghom",
    "account": "accounts/a-qartk5uwkh3noiajj6nm"
}
```

### IssueToken
This method issues an access token for a user that was registered with [CreateUser](#createuser).

```json
{
    "user": "tenants/t-50e39f8f-lp1/users/u-qtb6z4jkvrndteijghom",
    "external_id_token": {
        "nsa_id_token": "eyJqa3UiOiJodHRwczovL2UwZDY3YzUwOWZiMjAzODU4ZWJjYjJmZTNmODhjMmFhLmJhYXMubmludGVuZG8uY29tLzEuMC4wL2NlcnRpZmljYXRlcyIsImFsZyI6IlJTMjU2Iiwia2lkIjoiNTc0Zjc0MjctN2M1NC00ODUwLTg2ZjAtNzk0Yjg5NjU1ZTJiIn0.eyJhdWQiOiJlZDllMmYwNWQyODZmN2I4Iiwic3ViIjoiOGNhOGQ3ODQyZjg2NWIyZiIsIm5pbnRlbmRvIjp7ImF0IjoxNjcwMjc2MjU2LCJhdiI6IjAwMDEiLCJobSI6dHJ1ZSwicGgiOiJHQU1FX1NFUlZFUiIsImFpIjoiMDEwMDhmNjAwOGM1ZTAwMCIsImVkaSI6ImYxZjlkNzMyMGQ5YmEwZGVkMWFkZmQ2OTgxZWNmMWY0Iiwib3BwIjoiTUVNQkVSU0hJUF9SRVFVSVJFRCJ9LCJpc3MiOiJodHRwczovL2UwZDY3YzUwOWZiMjAzODU4ZWJjYjJmZTNmODhjMmFhLmJhYXMubmludGVuZG8uY29tIiwidHlwIjoiaWRfdG9rZW4iLCJleHAiOjE2NzAyODcwNTYsImlhdCI6MTY3MDI3NjI1NiwiYnM6ZGlkIjoiNTgxZWE3ODZhOTFmMTY4OSIsImp0aSI6IjY3NDNmMDllLWQ4OTEtNGY3YS05MDgzLTMwNzlkOTgxZTk0YiJ9.6DfNTQbTmkuA3bUPwMi3oQa06Tic2D8WB5vv-45zNFxa2l_0YbhpMarbNoxsTH2v7493GaUA520mh2f_HISN1yrjCA3C3YIGGr7NWoDd_Ew97JU1uV2b26klUom4XHADUnzHOoPCu5QwoB_8Dwa3ls25oSwy5hkcNiRnsfB_d2U14bCVwdnKjzbUAXgL7k2oTP2lV2j4aD8Pu5PhKeFuZdUo8gj-5_0sP2O3w1HyywdysIGDON7GYJ1mrc36sF7kB_MfHmYr65rSoFtqN_mHVYuxSGv1C3SwtZA2K_YFjahy2mjXubu68N7eatoFoP8xe2xbevf7Q5wfujHk5yJOqw"
    }
}
```

```json
{
    "token": {
        "user": "tenants/t-50e39f8f-lp1/users/u-qtb6z4jkvrndteijghom",
        "access_token": "eyJhbGciOiJFUzI1NiIsImprdSI6Imp3a1NldHMvbnBsbkFjY2Vzc1Rva2VuIiwia2lkIjoiMGRmOTAyZmEtMDU2Ny00ZmFmLThiZmYtNmQyNmY3YjY2Y2FmIn0.eyJleHAiOjE2NzAzMDcwNTIsImlhdCI6MTY3MDI3ODI1MiwiaXNzIjoiZGVmYXVsdCBpc3MiLCJucGxuIjp7ImFpZCI6ImEtcWFydGs1dXdraDNub2lhamo2bm0iLCJhcHBfaWQiOiIwMTAwOGY2MDA4YzVlMDAwIiwiYXV0aG9yaXphdGlvbiI6eyJhbGxvdyI6WyJubi5ucGxuLmF1dGguKioiLCIqKiJdLCJkZW55IjpbXSwibnNvX3Jlc3RyaWN0ZWQiOmZhbHNlfSwiZXh0X2lkIjoiOGNhOGQ3ODQyZjg2NWIyZiIsImV4dF9pZF90eXBlIjoxLCJ0aWQiOiJ0LTUwZTM5ZjhmLWxwMSJ9LCJzdWIiOiJ1LXF0YjZ6NGprdnJuZHRlaWpnaG9tIn0.63CrNQWCLKKK8haWYf9DRLY8S3eUPtyhpecuoDLZVYui4Pz6RgpTRG3tlWperORYo_F1lNfJMWRIlhl2W2Xq2w",
        "refresh_token": "07da3ac7-1e0c-42e6-a6ba-f4cae9ed4bd3",
        "ttl": {
            "seconds": 28800
        }
    }
}
```

### RefreshToken
This method issues an access token using a refresh token. Each refresh token can only be used once.

```json
{
    "user": "tenants/t-50e39f8f-lp1/users/u-qtb6z4jkvrndteijghom",
    "refresh_token": "07da3ac7-1e0c-42e6-a6ba-f4cae9ed4bd3"
}
```

```json
{
    "token": {
        "user": "tenants/t-50e39f8f-lp1/users/u-qtb6z4jkvrndteijghom",
        "access_token": "eyJhbGciOiJFUzI1NiIsImprdSI6Imp3a1NldHMvbnBsbkFjY2Vzc1Rva2VuIiwia2lkIjoiMGRmOTAyZmEtMDU2Ny00ZmFmLThiZmYtNmQyNmY3YjY2Y2FmIn0.eyJleHAiOjE2NzAzMDcwNTIsImlhdCI6MTY3MDI3ODI1MiwiaXNzIjoiZGVmYXVsdCBpc3MiLCJucGxuIjp7ImFpZCI6ImEtcWFydGs1dXdraDNub2lhamo2bm0iLCJhcHBfaWQiOiIwMTAwOGY2MDA4YzVlMDAwIiwiYXV0aG9yaXphdGlvbiI6eyJhbGxvdyI6WyJubi5ucGxuLmF1dGguKioiLCIqKiJdLCJkZW55IjpbXSwibnNvX3Jlc3RyaWN0ZWQiOmZhbHNlfSwiZXh0X2lkIjoiOGNhOGQ3ODQyZjg2NWIyZiIsImV4dF9pZF90eXBlIjoxLCJ0aWQiOiJ0LTUwZTM5ZjhmLWxwMSJ9LCJzdWIiOiJ1LXF0YjZ6NGprdnJuZHRlaWpnaG9tIn0.63CrNQWCLKKK8haWYf9DRLY8S3eUPtyhpecuoDLZVYui4Pz6RgpTRG3tlWperORYo_F1lNfJMWRIlhl2W2Xq2w",
        "refresh_token": "5e3da902-4041-4300-9636-4f06e72e5523",
        "ttl": {
            "seconds": 28800
        }
    }
}
```

### IssuePrearrangedUserToken
This method issues an access token for a prearranged user. Every tenant provides 16 prearranged users per account.

```json
{
    "tenant": "tenants/t-50e39f8f-lp1",
    "user_index": 0,
    "external_id_token": {
        "nsa_id_token": "eyJqa3UiOiJodHRwczovL2UwZDY3YzUwOWZiMjAzODU4ZWJjYjJmZTNmODhjMmFhLmJhYXMubmludGVuZG8uY29tLzEuMC4wL2NlcnRpZmljYXRlcyIsImFsZyI6IlJTMjU2Iiwia2lkIjoiNTc0Zjc0MjctN2M1NC00ODUwLTg2ZjAtNzk0Yjg5NjU1ZTJiIn0.eyJhdWQiOiJlZDllMmYwNWQyODZmN2I4Iiwic3ViIjoiOGNhOGQ3ODQyZjg2NWIyZiIsIm5pbnRlbmRvIjp7ImF0IjoxNjcwMjc2MjU2LCJhdiI6IjAwMDEiLCJobSI6dHJ1ZSwicGgiOiJHQU1FX1NFUlZFUiIsImFpIjoiMDEwMDhmNjAwOGM1ZTAwMCIsImVkaSI6ImYxZjlkNzMyMGQ5YmEwZGVkMWFkZmQ2OTgxZWNmMWY0Iiwib3BwIjoiTUVNQkVSU0hJUF9SRVFVSVJFRCJ9LCJpc3MiOiJodHRwczovL2UwZDY3YzUwOWZiMjAzODU4ZWJjYjJmZTNmODhjMmFhLmJhYXMubmludGVuZG8uY29tIiwidHlwIjoiaWRfdG9rZW4iLCJleHAiOjE2NzAyODcwNTYsImlhdCI6MTY3MDI3NjI1NiwiYnM6ZGlkIjoiNTgxZWE3ODZhOTFmMTY4OSIsImp0aSI6IjY3NDNmMDllLWQ4OTEtNGY3YS05MDgzLTMwNzlkOTgxZTk0YiJ9.6DfNTQbTmkuA3bUPwMi3oQa06Tic2D8WB5vv-45zNFxa2l_0YbhpMarbNoxsTH2v7493GaUA520mh2f_HISN1yrjCA3C3YIGGr7NWoDd_Ew97JU1uV2b26klUom4XHADUnzHOoPCu5QwoB_8Dwa3ls25oSwy5hkcNiRnsfB_d2U14bCVwdnKjzbUAXgL7k2oTP2lV2j4aD8Pu5PhKeFuZdUo8gj-5_0sP2O3w1HyywdysIGDON7GYJ1mrc36sF7kB_MfHmYr65rSoFtqN_mHVYuxSGv1C3SwtZA2K_YFjahy2mjXubu68N7eatoFoP8xe2xbevf7Q5wfujHk5yJOqw"
    }
}
```

```json
{
    "token": {
        "user": "tenants/t-50e39f8f-lp1/users/u-axutxgrmymlr2cijghom",
        "access_token": "eyJhbGciOiJFUzI1NiIsImprdSI6Imp3a1NldHMvbnBsbkFjY2Vzc1Rva2VuIiwia2lkIjoiMGRmOTAyZmEtMDU2Ny00ZmFmLThiZmYtNmQyNmY3YjY2Y2FmIn0.eyJleHAiOjE2NzAzMDcwNTIsImlhdCI6MTY3MDI3ODI1MiwiaXNzIjoiZGVmYXVsdCBpc3MiLCJucGxuIjp7ImFpZCI6ImEtcWFydGs1dXdraDNub2lhamo2bm0iLCJhcHBfaWQiOiIwMTAwOGY2MDA4YzVlMDAwIiwiYXV0aG9yaXphdGlvbiI6eyJhbGxvdyI6WyJubi5ucGxuLmF1dGguKioiLCIqKiJdLCJkZW55IjpbXSwibnNvX3Jlc3RyaWN0ZWQiOmZhbHNlfSwiZXh0X2lkIjoiOGNhOGQ3ODQyZjg2NWIyZiIsImV4dF9pZF90eXBlIjoxLCJ0aWQiOiJ0LTUwZTM5ZjhmLWxwMSJ9LCJzdWIiOiJ1LWF4dXR4Z3JteW1scjJjaWpnaG9tIn0.ZK2OTM_-7DR2ejz5A_4MOyGk3lUtlDm0jpVCH3ycPR5Mi6DYNiTnfYzeiZ6Yi4BL5rjQ5YNabbA5qyNz13OSew",
        "refresh_token": "5d78c46e-2ad5-4975-b109-7962b7c7988a",
        "ttl": {
            "seconds": 28800
        }
    }
}
```

### IssueAnonymousUserToken
This method issues an anonymous access token. Most services deny requests that are made by an anonymous user.

```json
{
    "tenant": "tenants/t-50e39f8f-lp1",
    "external_id_token": {
        "nsa_id_token": "eyJqa3UiOiJodHRwczovL2UwZDY3YzUwOWZiMjAzODU4ZWJjYjJmZTNmODhjMmFhLmJhYXMubmludGVuZG8uY29tLzEuMC4wL2NlcnRpZmljYXRlcyIsImFsZyI6IlJTMjU2Iiwia2lkIjoiNTc0Zjc0MjctN2M1NC00ODUwLTg2ZjAtNzk0Yjg5NjU1ZTJiIn0.eyJhdWQiOiJlZDllMmYwNWQyODZmN2I4Iiwic3ViIjoiOGNhOGQ3ODQyZjg2NWIyZiIsIm5pbnRlbmRvIjp7ImF0IjoxNjcwMjc2MjU2LCJhdiI6IjAwMDEiLCJobSI6dHJ1ZSwicGgiOiJHQU1FX1NFUlZFUiIsImFpIjoiMDEwMDhmNjAwOGM1ZTAwMCIsImVkaSI6ImYxZjlkNzMyMGQ5YmEwZGVkMWFkZmQ2OTgxZWNmMWY0Iiwib3BwIjoiTUVNQkVSU0hJUF9SRVFVSVJFRCJ9LCJpc3MiOiJodHRwczovL2UwZDY3YzUwOWZiMjAzODU4ZWJjYjJmZTNmODhjMmFhLmJhYXMubmludGVuZG8uY29tIiwidHlwIjoiaWRfdG9rZW4iLCJleHAiOjE2NzAyODcwNTYsImlhdCI6MTY3MDI3NjI1NiwiYnM6ZGlkIjoiNTgxZWE3ODZhOTFmMTY4OSIsImp0aSI6IjY3NDNmMDllLWQ4OTEtNGY3YS05MDgzLTMwNzlkOTgxZTk0YiJ9.6DfNTQbTmkuA3bUPwMi3oQa06Tic2D8WB5vv-45zNFxa2l_0YbhpMarbNoxsTH2v7493GaUA520mh2f_HISN1yrjCA3C3YIGGr7NWoDd_Ew97JU1uV2b26klUom4XHADUnzHOoPCu5QwoB_8Dwa3ls25oSwy5hkcNiRnsfB_d2U14bCVwdnKjzbUAXgL7k2oTP2lV2j4aD8Pu5PhKeFuZdUo8gj-5_0sP2O3w1HyywdysIGDON7GYJ1mrc36sF7kB_MfHmYr65rSoFtqN_mHVYuxSGv1C3SwtZA2K_YFjahy2mjXubu68N7eatoFoP8xe2xbevf7Q5wfujHk5yJOqw"
    }
}
```

```json
{
    "token": {
        "user": "tenants/t-50e39f8f-lp1/users/u-anonymous",
        "access_token": "eyJhbGciOiJFUzI1NiIsImprdSI6Imp3a1NldHMvbnBsbkFjY2Vzc1Rva2VuIiwia2lkIjoiMGRmOTAyZmEtMDU2Ny00ZmFmLThiZmYtNmQyNmY3YjY2Y2FmIn0.eyJleHAiOjE2NzAzMDcwNTIsImlhdCI6MTY3MDI3ODI1MiwiaXNzIjoiZGVmYXVsdCBpc3MiLCJucGxuIjp7ImFpZCI6ImEtcWFydGs1dXdraDNub2lhamo2bm0iLCJhcHBfaWQiOiIwMTAwOGY2MDA4YzVlMDAwIiwiYXV0aG9yaXphdGlvbiI6eyJhbGxvdyI6WyJubi5ucGxuLmF1dGguKioiLCIqKiJdLCJkZW55IjpbXSwibnNvX3Jlc3RyaWN0ZWQiOmZhbHNlfSwiZXh0X2lkIjoiOGNhOGQ3ODQyZjg2NWIyZiIsImV4dF9pZF90eXBlIjoxLCJ0aWQiOiJ0LTUwZTM5ZjhmLWxwMSJ9LCJzdWIiOiJ1LWFub255bW91cyJ9.ihimHHAyWHOwH2QQZEuK7hTryku95SpN6dlL52zPT69zNuWVriRIE08Px5-Lev-DB9cAZCknyuPcYO7JyiWE7w",
        "refresh_token": "f20b5f44-5257-40e7-8f68-2956b094f668",
        "ttl": {
            "seconds": 28800
        }
    }
}
```

### RefreshAnonymousUserToken
This method issues an anonymous access token using a refresh token. Each refresh token can only be used once.

```json
{
    "tenant": "tenants/t-50e39f8f-lp1",
    "refresh_token": "f20b5f44-5257-40e7-8f68-2956b094f668"
}
```

```json
{
    "token": {
        "user": "tenants/t-50e39f8f-lp1/users/u-anonymous",
        "access_token": "eyJhbGciOiJFUzI1NiIsImprdSI6Imp3a1NldHMvbnBsbkFjY2Vzc1Rva2VuIiwia2lkIjoiMGRmOTAyZmEtMDU2Ny00ZmFmLThiZmYtNmQyNmY3YjY2Y2FmIn0.eyJleHAiOjE2NzAzMDcwNTIsImlhdCI6MTY3MDI3ODI1MiwiaXNzIjoiZGVmYXVsdCBpc3MiLCJucGxuIjp7ImFpZCI6ImEtcWFydGs1dXdraDNub2lhamo2bm0iLCJhcHBfaWQiOiIwMTAwOGY2MDA4YzVlMDAwIiwiYXV0aG9yaXphdGlvbiI6eyJhbGxvdyI6WyJubi5ucGxuLmF1dGguKioiLCIqKiJdLCJkZW55IjpbXSwibnNvX3Jlc3RyaWN0ZWQiOmZhbHNlfSwiZXh0X2lkIjoiOGNhOGQ3ODQyZjg2NWIyZiIsImV4dF9pZF90eXBlIjoxLCJ0aWQiOiJ0LTUwZTM5ZjhmLWxwMSJ9LCJzdWIiOiJ1LWFub255bW91cyJ9.ihimHHAyWHOwH2QQZEuK7hTryku95SpN6dlL52zPT69zNuWVriRIE08Px5-Lev-DB9cAZCknyuPcYO7JyiWE7w",
        "refresh_token": "5bb91b45-2f83-4f49-87f9-ca659b97bd53",
        "ttl": {
            "seconds": 28800
        }
    }
}
```

### ListUsers
This method lists all users that were created with [CreateUser](#createuser) under the current account. Prearranged users are not included in the list. This method requires an access token.

```json
{
    "parent": "tenants/current"
}
```

```json
{
    "users": [
        {
            "name": "tenants/t-50e39f8f-lp1/users/u-qtb6z4jkvrndteijghom",
            "account": "accounts/a-qartk5uwkh3noiajj6nm"
        }
    ]
}
```

### DeleteUser
This method deletes a user that was created with [CreateUser](#createuser). Prearranged users cannot be deleted. This method requires an access token.

```json
{
    "name": "tenants/current/users/u-qtb6z4jkvrndteijghom"
}
```