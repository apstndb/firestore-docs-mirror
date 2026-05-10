---
name: documents/docs.cloud.google.com/datastore/docs/reference/admin/rest/Shared.Types/State
uri: https://docs.cloud.google.com/datastore/docs/reference/admin/rest/Shared.Types/State
title: State
description: A highly-scalable NoSQL database for your web and mobile applications that automatically handles sharding and replication.
data_source: docs.cloud.google.com
update_time: "2025-10-17T22:06:14Z"
---

The various possible states for an ongoing Operation.

Enums

`STATE_UNSPECIFIED`

Unspecified.

`INITIALIZING`

Request is being prepared for processing.

`PROCESSING`

Request is actively being processed.

`CANCELLING`

Request is in the process of being cancelled after user called google.longrunning.Operations.CancelOperation on the operation.

`FINALIZING`

Request has been processed and is in its finalization stage.

`SUCCESSFUL`

Request has completed successfully.

`FAILED`

Request has finished being processed, but encountered an error.

`CANCELLED`

Request has finished being cancelled after user called google.longrunning.Operations.CancelOperation.
