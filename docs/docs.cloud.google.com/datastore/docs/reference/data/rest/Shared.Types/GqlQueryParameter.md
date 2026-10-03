---
name: documents/docs.cloud.google.com/datastore/docs/reference/data/rest/Shared.Types/GqlQueryParameter
uri: https://docs.cloud.google.com/datastore/docs/reference/data/rest/Shared.Types/GqlQueryParameter
title: GqlQueryParameter
description: A highly-scalable NoSQL database for your web and mobile applications that automatically handles sharding and replication.
data_source: docs.cloud.google.com
---

- [JSON representation](https://docs.cloud.google.com/datastore/docs/reference/data/rest/Shared.Types/GqlQueryParameter#SCHEMA_REPRESENTATION)

A binding parameter for a GQL query.

**JSON representation**

```
{

  // Union field parameter_type can be only one of the following:
  "value": {
    object (Value)
  },
  "cursor": string
  // End of list of possible types for union field parameter_type.
}
```

| Fields                                                                                                   |                                                                                                                                                                                     |
|----------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `parameter_type` . The type of parameter. `parameter_type` can be only one of the following: |                                                                                                                                                                                     |
| `value`                                                                                                  | `object ( `[`Value`](https://docs.cloud.google.com/datastore/docs/reference/data/rest/Shared.Types/Value)` )` A value parameter.                                                    |
| `cursor`                                                                                                 | `string ( `[`bytes`](https://developers.google.com/discovery/v1/type-format)` format)` A query cursor. Query cursors are returned in query result batches. A base64-encoded string. |
