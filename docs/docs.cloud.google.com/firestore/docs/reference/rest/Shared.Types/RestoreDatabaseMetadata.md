---
name: documents/docs.cloud.google.com/firestore/docs/reference/rest/Shared.Types/RestoreDatabaseMetadata
uri: https://docs.cloud.google.com/firestore/docs/reference/rest/Shared.Types/RestoreDatabaseMetadata
title: RestoreDatabaseMetadata
description: A cloud-hosted NoSQL database that's simple enough for rapid prototyping yet scalable and flexible enough to grow to any size.
data_source: docs.cloud.google.com
---

Metadata for the [`long-running operation`](https://docs.cloud.google.com/firestore/docs/reference/rest/Shared.Types/Operation) from the \[databases.restore\]\[google.firestore.admin.v1.RestoreDatabase\] request.

**JSON representation**

```
{
  "startTime": string,
  "endTime": string,
  "operationState": enum (OperationState),
  "database": string,
  "backup": string,
  "progressPercentage": {
    object (Progress)
  }
}
```

| Fields               |                                                                                                                                                                                                                                                                                                                                                                                                                                  |
|----------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `startTime`          | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` The time the restore was started. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .                          |
| `endTime`            | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` The time the restore finished, unset for ongoing restores. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` . |
| `operationState`     | `enum ( `[`OperationState`](https://docs.cloud.google.com/firestore/docs/reference/rest/Shared.Types/OperationState)` )` The operation state of the restore.                                                                                                                                                                                                                                                                     |
| `database`           | `string` The name of the database being restored to.                                                                                                                                                                                                                                                                                                                                                                             |
| `backup`             | `string` The name of the backup restoring from.                                                                                                                                                                                                                                                                                                                                                                                  |
| `progressPercentage` | `object ( `[`Progress`](https://docs.cloud.google.com/firestore/docs/reference/rest/Shared.Types/Progress)` )` How far along the restore is as an estimated percentage of remaining time.                                                                                                                                                                                                                                        |
