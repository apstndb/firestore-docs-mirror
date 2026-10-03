---
name: documents/docs.cloud.google.com/datastore/docs/reference/data/rest/v1/EntityResult
uri: https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/EntityResult
title: EntityResult
description: A highly-scalable NoSQL database for your web and mobile applications that automatically handles sharding and replication.
data_source: docs.cloud.google.com
---

- [JSON representation](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/EntityResult#SCHEMA_REPRESENTATION)

The result of fetching an entity from Datastore.

**JSON representation**

```
{
  "entity": {
    object (Entity)
  },
  "version": string,
  "createTime": string,
  "updateTime": string,
  "cursor": string
}
```

| Fields       |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
|--------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `entity`     | `object ( `[`Entity`](https://docs.cloud.google.com/datastore/docs/reference/data/rest/Shared.Types/Value#Entity)` )` The resulting entity.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| `version`    | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` The version of the entity, a strictly positive number that monotonically increases with changes to the entity. This field is set for [`FULL`](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/projects/runQuery#ResultType.ENUM_VALUES.FULL) entity results. For [`missing`](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/projects/lookup#body.LookupResponse.FIELDS.missing) entities in `LookupResponse` , this is the version of the snapshot that was used to look up the entity, and it is always set except for eventually consistent reads. |
| `createTime` | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` The time at which the entity was created. This field is set for [`FULL`](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/projects/runQuery#ResultType.ENUM_VALUES.FULL) entity results. If this entity is missing, this field will not be set. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .                                             |
| `updateTime` | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` The time at which the entity was last changed. This field is set for [`FULL`](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/projects/runQuery#ResultType.ENUM_VALUES.FULL) entity results. If this entity is missing, this field will not be set. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .                                        |
| `cursor`     | `string ( `[`bytes`](https://developers.google.com/discovery/v1/type-format)` format)` A cursor that points to the position after the result entity. Set only when the `EntityResult` is part of a `QueryResultBatch` message. A base64-encoded string.                                                                                                                                                                                                                                                                                                                                                                                                                              |
