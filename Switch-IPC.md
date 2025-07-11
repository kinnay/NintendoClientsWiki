These are my personal notes that aid me in understand the IPC interface of the Nintendo Switch, which is further documented on
[SwitchBrew](https://switchbrew.org/wiki/HIPC).

## Overview
All system services on the Nintendo Switch are implemented in userland processes. These processes communicate with each other through IPC.

The following syscalls can be used to manage ports:
* `svcManageNamedPort` register a named **port** on the kernel.
* `svcConnectToNamedPort` returns a **session** handle that can be used to communicate with a specific port.

On the Switch, there exists only one named port: `sm:`. The `sm:` port is used by userland processes to register other services, and to establish a session with them for communication.

The following syscalls can be used to send IPC requests to other services:

* `svcSendSyncRequest`
* `svcSendSyncRequestLight`
* `svcSendSyncRequestWithUserBuffer`
* `svcSendAsyncRequestWithUserBuffer`

By default, the message is stored in thread local storage, although a user buffer can be provided as well.

Furthermore, the following syscalls can be used to receive IPC requests, and to send a reply:

* `svcReplyAndReceive`
* `svcReplyAndReceiveLight`
* `svcReplyAndReceiveWithUserBuffer`
