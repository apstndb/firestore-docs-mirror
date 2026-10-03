---
name: documents/docs.cloud.google.com/firestore/docs/reference/rest/v1beta2/projects.databases/importDocuments
uri: https://docs.cloud.google.com/firestore/docs/reference/rest/v1beta2/projects.databases/importDocuments
title: 'Method: projects.databases.importDocuments'
description: A cloud-hosted NoSQL database that's simple enough for rapid prototyping yet scalable and flexible enough to grow to any size.
data_source: docs.cloud.google.com
---

Imports documents into Google Cloud Firestore. Existing documents with the same name are overwritten. The import occurs in the background and its progress can be monitored and managed via the Operation resource that is created. If an databases.importDocuments operation is cancelled, it is possible that a subset of the data has already been imported to Cloud Firestore.

### HTTP request

Choose a location:

  
`POST https://firestore.googleapis.com/v1beta2/{name=projects/*/databases/*}:importDocuments`

The URLs use [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

| Parameters |                                                                                                          |
|------------|----------------------------------------------------------------------------------------------------------|
| `name`     | `string` Database to import into. Should be of the form: `projects/{projectId}/databases/{databaseId}` . |

### Request body

The request body contains data with the following structure:

**JSON representation**

```
{
  "collectionIds": [
    string
  ],
  "inputUriPrefix": string
}
```

| Fields            |                                                                                                                                                                                                                                              |
|-------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `collectionIds[]` | `string` Which collection ids to import. Unspecified means all collections included in the import.                                                                                                                                           |
| `inputUriPrefix`  | `string` Location of the exported files. This must match the outputUriPrefix of an ExportDocumentsResponse from an export that has completed successfully. See: `google.firestore.admin.v1beta2.ExportDocumentsResponse.output_uri_prefix` . |

### Response body

If successful, the response body contains an instance of [`Operation`](https://docs.cloud.google.com/firestore/docs/reference/rest/Shared.Types/Operation) .

### Authorization scopes

Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/datastore`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .
