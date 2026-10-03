---
name: documents/docs.cloud.google.com/datastore/docs/reference/admin/rest/Shared.Types/IndexOperationMetadata
uri: https://docs.cloud.google.com/datastore/docs/reference/admin/rest/Shared.Types/IndexOperationMetadata
title: IndexOperationMetadata
description: A highly-scalable NoSQL database for your web and mobile applications that automatically handles sharding and replication.
data_source: docs.cloud.google.com
---

- [JSON representation](https://docs.cloud.google.com/datastore/docs/reference/admin/rest/Shared.Types/IndexOperationMetadata#SCHEMA_REPRESENTATION)

Metadata for Index operations.

**JSON representation**

```
{
  "common": {
    object (CommonMetadata)
  },
  "progressEntities": {
    object (Progress)
  },
  "indexId": string
}
```

| Fields             |                                                                                                                                                                                     |
|--------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `common`           | `object ( `[`CommonMetadata`](https://docs.cloud.google.com/datastore/docs/reference/admin/rest/Shared.Types/CommonMetadata)` )` Metadata common to all Datastore Admin operations. |
| `progressEntities` | `object ( `[`Progress`](https://docs.cloud.google.com/datastore/docs/reference/admin/rest/Shared.Types/Progress)` )` An estimate of the number of entities processed.               |
| `indexId`          | `string` The index resource ID that this operation is acting on.                                                                                                                    |
