---
name: documents/docs.cloud.google.com/datastore/docs/reference/admin/rest/Shared.Types/ExportEntitiesMetadata
uri: https://docs.cloud.google.com/datastore/docs/reference/admin/rest/Shared.Types/ExportEntitiesMetadata
title: ExportEntitiesMetadata
description: A highly-scalable NoSQL database for your web and mobile applications that automatically handles sharding and replication.
data_source: docs.cloud.google.com
---

- [JSON representation](https://docs.cloud.google.com/datastore/docs/reference/admin/rest/Shared.Types/ExportEntitiesMetadata#SCHEMA_REPRESENTATION)

Metadata for ExportEntities operations.

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
  "outputUrlPrefix": string
}
```

| Fields             |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
|--------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `common`           | `object ( `[`CommonMetadata`](https://docs.cloud.google.com/datastore/docs/reference/admin/rest/Shared.Types/CommonMetadata)` )` Metadata common to all Datastore Admin operations.                                                                                                                                                                                                                                                                                                                                                            |
| `progressEntities` | `object ( `[`Progress`](https://docs.cloud.google.com/datastore/docs/reference/admin/rest/Shared.Types/Progress)` )` An estimate of the number of entities processed.                                                                                                                                                                                                                                                                                                                                                                          |
| `progressBytes`    | `object ( `[`Progress`](https://docs.cloud.google.com/datastore/docs/reference/admin/rest/Shared.Types/Progress)` )` An estimate of the number of bytes processed.                                                                                                                                                                                                                                                                                                                                                                             |
| `entityFilter`     | `object ( `[`EntityFilter`](https://docs.cloud.google.com/datastore/docs/reference/admin/rest/Shared.Types/EntityFilter)` )` Description of which entities are being exported.                                                                                                                                                                                                                                                                                                                                                                 |
| `outputUrlPrefix`  | `string` Location for the export metadata and data files. This will be the same value as the [`google.datastore.admin.v1.ExportEntitiesRequest.output_url_prefix`](https://docs.cloud.google.com/datastore/docs/reference/admin/rest/v1/projects/export#body.request_body.FIELDS.output_url_prefix) field. The final output location is provided in [`google.datastore.admin.v1.ExportEntitiesResponse.output_url`](https://docs.cloud.google.com/datastore/docs/reference/admin/rest/Shared.Types/ExportEntitiesResponse#FIELDS.output_url) . |
