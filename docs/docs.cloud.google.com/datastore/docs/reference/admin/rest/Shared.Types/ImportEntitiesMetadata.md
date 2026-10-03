---
name: documents/docs.cloud.google.com/datastore/docs/reference/admin/rest/Shared.Types/ImportEntitiesMetadata
uri: https://docs.cloud.google.com/datastore/docs/reference/admin/rest/Shared.Types/ImportEntitiesMetadata
title: ImportEntitiesMetadata
description: A highly-scalable NoSQL database for your web and mobile applications that automatically handles sharding and replication.
data_source: docs.cloud.google.com
---

- [JSON representation](https://docs.cloud.google.com/datastore/docs/reference/admin/rest/Shared.Types/ImportEntitiesMetadata#SCHEMA_REPRESENTATION)

Metadata for ImportEntities operations.

**JSON representation**

```
{
  "common": {
    object (CommonMetadata)
  },
  "progressEntities": {
    object (Progress)
  },
  "progressBytes": {
    object (Progress)
  },
  "entityFilter": {
    object (EntityFilter)
  },
  "inputUrl": string
}
```

| Fields             |                                                                                                                                                                                                                                                                                       |
|--------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `common`           | `object ( `[`CommonMetadata`](https://docs.cloud.google.com/datastore/docs/reference/admin/rest/Shared.Types/CommonMetadata)` )` Metadata common to all Datastore Admin operations.                                                                                                   |
| `progressEntities` | `object ( `[`Progress`](https://docs.cloud.google.com/datastore/docs/reference/admin/rest/Shared.Types/Progress)` )` An estimate of the number of entities processed.                                                                                                                 |
| `progressBytes`    | `object ( `[`Progress`](https://docs.cloud.google.com/datastore/docs/reference/admin/rest/Shared.Types/Progress)` )` An estimate of the number of bytes processed.                                                                                                                    |
| `entityFilter`     | `object ( `[`EntityFilter`](https://docs.cloud.google.com/datastore/docs/reference/admin/rest/Shared.Types/EntityFilter)` )` Description of which entities are being imported.                                                                                                        |
| `inputUrl`         | `string` The location of the import metadata file. This will be the same value as the [`google.datastore.admin.v1.ExportEntitiesResponse.output_url`](https://docs.cloud.google.com/datastore/docs/reference/admin/rest/Shared.Types/ExportEntitiesResponse#FIELDS.output_url) field. |
