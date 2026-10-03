---
name: documents/docs.cloud.google.com/datastore/docs/reference/admin/rest/v1beta1/projects/import
uri: https://docs.cloud.google.com/datastore/docs/reference/admin/rest/v1beta1/projects/import
title: 'Method: projects.import'
description: A highly-scalable NoSQL database for your web and mobile applications that automatically handles sharding and replication.
data_source: docs.cloud.google.com
---

- [HTTP request](https://docs.cloud.google.com/datastore/docs/reference/admin/rest/v1beta1/projects/import#body.HTTP_TEMPLATE)
- [Path parameters](https://docs.cloud.google.com/datastore/docs/reference/admin/rest/v1beta1/projects/import#body.PATH_PARAMETERS)
- [Request body](https://docs.cloud.google.com/datastore/docs/reference/admin/rest/v1beta1/projects/import#body.request_body)
  - [JSON representation](https://docs.cloud.google.com/datastore/docs/reference/admin/rest/v1beta1/projects/import#body.request_body.SCHEMA_REPRESENTATION)
- [Response body](https://docs.cloud.google.com/datastore/docs/reference/admin/rest/v1beta1/projects/import#body.response_body)
- [Authorization scopes](https://docs.cloud.google.com/datastore/docs/reference/admin/rest/v1beta1/projects/import#body.aspect)
- [Try it!](https://docs.cloud.google.com/datastore/docs/reference/admin/rest/v1beta1/projects/import#try-it)

Imports entities into Google Cloud Datastore. Existing entities with the same key are overwritten. The import occurs in the background and its progress can be monitored and managed via the Operation resource that is created. If an projects.import operation is cancelled, it is possible that a subset of the data has already been imported to Cloud Datastore.

### HTTP request

Choose a location:

  
`POST https://datastore.googleapis.com/v1beta1/projects/{projectId}:import`

The URLs use [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

| Parameters  |                                                        |
|-------------|--------------------------------------------------------|
| `projectId` | `string` Project ID against which to make the request. |

### Request body

The request body contains data with the following structure:

**JSON representation**

```
{
  "labels": {
    string: string,
    ...
  },
  "inputUrl": string,
  "entityFilter": {
    object (EntityFilter)
  }
}
```

| Fields         |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
|----------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `labels`       | `map (key: string, value: string)` Client-assigned labels. An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` .                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| `inputUrl`     | `string` The full resource URL of the external storage location. Currently, only Google Cloud Storage is supported. So inputUrl should be of the form: `gs://BUCKET_NAME[/NAMESPACE_PATH]/OVERALL_EXPORT_METADATA_FILE` , where `BUCKET_NAME` is the name of the Cloud Storage bucket, `NAMESPACE_PATH` is an optional Cloud Storage namespace path (this is not a Cloud Datastore namespace), and `OVERALL_EXPORT_METADATA_FILE` is the metadata file written by the projects.export operation. For more information about Cloud Storage namespace paths, see [Object name considerations](https://cloud.google.com/storage/docs/naming#object-considerations) . For more information, see `google.datastore.admin.v1beta1.ExportEntitiesResponse.output_url` . |
| `entityFilter` | `object ( ``EntityFilter`` )` Optionally specify which kinds/namespaces are to be imported. If provided, the list must be a subset of the EntityFilter used in creating the export, otherwise a FAILED_PRECONDITION error will be returned. If no filter is specified then all entities from the export are imported.                                                                                                                                                                                                                                                                                                                                                                                                                                            |

### Response body

If successful, the response body contains an instance of [`Operation`](https://docs.cloud.google.com/datastore/docs/reference/admin/rest/Shared.Types/Operation) .

### Authorization scopes

Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/datastore`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .
