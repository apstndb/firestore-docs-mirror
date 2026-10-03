---
name: documents/docs.cloud.google.com/datastore/docs/reference/admin/rest/Shared.Types/CommonMetadata
uri: https://docs.cloud.google.com/datastore/docs/reference/admin/rest/Shared.Types/CommonMetadata
title: CommonMetadata
description: A highly-scalable NoSQL database for your web and mobile applications that automatically handles sharding and replication.
data_source: docs.cloud.google.com
---

- [JSON representation](https://docs.cloud.google.com/datastore/docs/reference/admin/rest/Shared.Types/CommonMetadata#SCHEMA_REPRESENTATION)

Metadata common to all Datastore Admin operations.

**JSON representation**

```
{
  "startTime": string,
  "endTime": string,
  "operationType": enum (OperationType),
  "labels": {
    string: string,
    ...
  },
  "state": enum (State)
}
```

| Fields          |                                                                                                                                                                                                                                                                                                                                                                                                                                       |
|-----------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `startTime`     | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` The time that work began on the operation. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .                      |
| `endTime`       | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` The time the operation ended, either successfully or otherwise. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` . |
| `operationType` | `enum ( `[`OperationType`](https://docs.cloud.google.com/datastore/docs/reference/admin/rest/Shared.Types/OperationType)` )` The type of the operation. Can be used as a filter in ListOperationsRequest.                                                                                                                                                                                                                             |
| `labels`        | `map (key: string, value: string)` The client-assigned labels which were provided when the operation was created. May also include additional labels. An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` .                                                                                                                                                           |
| `state`         | `enum ( `[`State`](https://docs.cloud.google.com/datastore/docs/reference/admin/rest/Shared.Types/State)` )` The current state of the Operation.                                                                                                                                                                                                                                                                                      |
