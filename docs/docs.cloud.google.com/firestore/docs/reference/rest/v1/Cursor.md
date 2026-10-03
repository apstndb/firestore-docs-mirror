---
name: documents/docs.cloud.google.com/firestore/docs/reference/rest/v1/Cursor
uri: https://docs.cloud.google.com/firestore/docs/reference/rest/v1/Cursor
title: Cursor
description: A cloud-hosted NoSQL database that's simple enough for rapid prototyping yet scalable and flexible enough to grow to any size.
data_source: docs.cloud.google.com
---

A position in a query result set.

**JSON representation**

```
{
  "values": [
    {
      object (Value)
    }
  ],
  "before": boolean
}
```

| Fields     |                                                                                                                                                                                                                                                                                       |
|------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `values[]` | `object ( `[`Value`](https://docs.cloud.google.com/firestore/docs/reference/rest/Shared.Types/ArrayValue#Value)` )` The values that represent a position, in the order they appear in the order by clause of a query. Can contain fewer values than specified in the order by clause. |
| `before`   | `boolean` If the position is just before or just after the given values, relative to the sort order defined by the query.                                                                                                                                                             |
