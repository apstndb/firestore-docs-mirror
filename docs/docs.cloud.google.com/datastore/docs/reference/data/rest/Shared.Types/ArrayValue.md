---
name: documents/docs.cloud.google.com/datastore/docs/reference/data/rest/Shared.Types/ArrayValue
uri: https://docs.cloud.google.com/datastore/docs/reference/data/rest/Shared.Types/ArrayValue
title: ArrayValue
description: A highly-scalable NoSQL database for your web and mobile applications that automatically handles sharding and replication.
data_source: docs.cloud.google.com
---

- [JSON representation](https://docs.cloud.google.com/datastore/docs/reference/data/rest/Shared.Types/ArrayValue#SCHEMA_REPRESENTATION)

An array value.

**JSON representation**

```
{
  "values": [
    {
      object (Value)
    }
  ]
}
```

| Fields     |                                                                                                                                                                                                                                                         |
|------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `values[]` | `object ( `[`Value`](https://docs.cloud.google.com/datastore/docs/reference/data/rest/Shared.Types/Value)` )` Values in the array. The order of values in an array is preserved as long as all values have identical settings for 'excludeFromIndexes'. |
