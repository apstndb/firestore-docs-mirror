---
name: documents/docs.cloud.google.com/datastore/docs/reference/admin/rest/Shared.Types/Progress
uri: https://docs.cloud.google.com/datastore/docs/reference/admin/rest/Shared.Types/Progress
title: Progress
description: A highly-scalable NoSQL database for your web and mobile applications that automatically handles sharding and replication.
data_source: docs.cloud.google.com
---

- [JSON representation](https://docs.cloud.google.com/datastore/docs/reference/admin/rest/Shared.Types/Progress#SCHEMA_REPRESENTATION)

Measures the progress of a particular metric.

**JSON representation**

```
{
  "workCompleted": string,
  "workEstimated": string
}
```

| Fields          |                                                                                                                                                                                             |
|-----------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `workCompleted` | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` The amount of work that has been completed. Note that this may be greater than workEstimated.        |
| `workEstimated` | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` An estimate of how much work needs to be performed. May be zero if the work estimate is unavailable. |
