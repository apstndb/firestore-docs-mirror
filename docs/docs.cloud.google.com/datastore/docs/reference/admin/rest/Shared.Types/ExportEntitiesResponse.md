---
name: documents/docs.cloud.google.com/datastore/docs/reference/admin/rest/Shared.Types/ExportEntitiesResponse
uri: https://docs.cloud.google.com/datastore/docs/reference/admin/rest/Shared.Types/ExportEntitiesResponse
title: ExportEntitiesResponse
description: A highly-scalable NoSQL database for your web and mobile applications that automatically handles sharding and replication.
data_source: docs.cloud.google.com
---

- [JSON representation](https://docs.cloud.google.com/datastore/docs/reference/admin/rest/Shared.Types/ExportEntitiesResponse#SCHEMA_REPRESENTATION)

The response for [`google.datastore.admin.v1.DatastoreAdmin.ExportEntities`](https://docs.cloud.google.com/datastore/docs/reference/admin/rest/v1/projects/export#google.datastore.admin.v1.DatastoreAdmin.ExportEntities) .

**JSON representation**

```
{
  "outputUrl": string
}
```

| Fields      |                                                                                                                                                                                                                                                                                                                                                                                               |
|-------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `outputUrl` | `string` Location of the output metadata file. This can be used to begin an import into Cloud Datastore (this project or another project). See [`google.datastore.admin.v1.ImportEntitiesRequest.input_url`](https://docs.cloud.google.com/datastore/docs/reference/admin/rest/v1/projects/import#body.request_body.FIELDS.input_url) . Only present if the operation completed successfully. |
