[NPLN](NPLN-Servers) > Messaging Service
---

Full name: `nn.npln.messaging.v1.Messaging`

* [Overview](#overview)
* [Methods](#methods)
* [Source code](https://github.com/kinnay/NPLN-Protocols/blob/master/latest/proto/messaging/v1/messaging.proto)

## Overview
The messaging service allows games to send messages to other players.

To listen for messages, the client must call the `RecvMessage` method.

There are three kinds of messages:
* **Regular messages:** these carry game-specific information in the `fields` and `message_type` properties.
* **Ack messages:** if a regular message has the `need_ack` flag set, its receiver should send an ack message in return.
* **Keep alive messages:** if a client is listening for messages and no messages have been delivered for 45 seconds, the server delivers a keep alive message. The server also delivers a keep alive message immediately after the client starts listening for messages. The first keep alive message also includes an `idle_timeout` field, which is set to 95 seconds.

## Methods
* [RecvMessage](#recvmessage)
* [SendMessage](#sendmessage)
* SendAck

### RecvMessage
This method can be used to receive messages from the server. Because it is a server-streaming RPC, this method only needs to be called once.

Request:

```json
{
    "user": "tenants/current/users/current"
}
```

The server immediately sends a keep alive message with an idle timeout:

```json
{
    "keep_alive": {
        "idle_timeout": {
            "seconds": 95
        }
    }
}
```

When no messages are delivered for 45 seconds, the server also sends a keep alive message:

```json
{
    "keep_alive": {
        "idle_timeout": {}
    }
}
```

If a player sends a message to you, it will be delivered by the server:

```json
{
    "message": {
        "message_body": {
            "message_request_id": "5211fb2ef2818a0c",
            "fields": {
                "fields": {
                    "key": "device_id",
                    "value": {
                        "string_value": "1604bba5-5b84-567a-aeb5-07a8037131be"
                    }
                },
                {
                    "key": "app_version",
                    "value": {
                        "integer_value": 0
                    }
                }
            },
            "message_type": "NplnLogin"
        }
        "sender_user": "tenants/t-156eef4e-lp1/users/u-azbb3i4ze5j46mfu7zum",
        "message_resume_token": "v2_1697905329915-0",
        "send_time": {
            "seconds": 1697905329,
            "nanos": 913690646
        }
    }
}
```

### SendMessage
This method can be used to send a message to one or more players.

```json
{
    "user": "tenants/current/users/current",
    "receiver_users": [
        "tenants/t-156eef4e-lp1/users/u-azbb3i4ze5j46mfu7zum"
    ],
    "message_body": {
        "message_request_id": "5211fb2ef2818a0c",
        "fields": {
            "fields": {
                "key": "device_id",
                "value": {
                    "string_value": "1604bba5-5b84-567a-aeb5-07a8037131be"
                }
            },
            {
                "key": "app_version",
                "value": {
                    "integer_value": 0
                }
            }
        },
        "message_type": "NplnLogin"
    }
}
```