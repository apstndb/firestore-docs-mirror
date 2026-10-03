---
name: documents/docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.databases.collectionGroups.fields/list
uri: https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.databases.collectionGroups.fields/list
title: 'Method: projects.databases.collectionGroups.fields.list'
description: A cloud-hosted NoSQL database that's simple enough for rapid prototyping yet scalable and flexible enough to grow to any size.
data_source: docs.cloud.google.com
---

Lists the field configuration and metadata for this database.

Currently, [`FirestoreAdmin.ListFields`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.databases.collectionGroups.fields/list#google.firestore.admin.v1.FirestoreAdmin.ListFields) only supports listing fields that have been explicitly overridden. To issue this query, call [`FirestoreAdmin.ListFields`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.databases.collectionGroups.fields/list#google.firestore.admin.v1.FirestoreAdmin.ListFields) with the filter set to `indexConfig.usesAncestorConfig:false` or `ttlConfig:*` .

### HTTP request

Choose a location:

  
`GET https://firestore.googleapis.com/v1/{parent=projects/*/databases/*/collectionGroups/*}/fields`

The URLs use [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

| Parameters |                                                                                                                            |
|------------|----------------------------------------------------------------------------------------------------------------------------|
| `parent`   | `string` Required. A parent name of the form `projects/{projectId}/databases/{databaseId}/collectionGroups/{collectionId}` |

### Query parameters

| Parameters  |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
|-------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `filter`    | `string` The filter to apply to list results. Currently, [`FirestoreAdmin.ListFields`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.databases.collectionGroups.fields/list#google.firestore.admin.v1.FirestoreAdmin.ListFields) only supports listing fields that have been explicitly overridden. To issue this query, call [`FirestoreAdmin.ListFields`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.databases.collectionGroups.fields/list#google.firestore.admin.v1.FirestoreAdmin.ListFields) with a filter that includes `indexConfig.usesAncestorConfig:false` or `ttlConfig:*` . |
| `pageSize`  | `integer` The number of results to return.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| `pageToken` | `string` A page token, returned from a previous call to [`FirestoreAdmin.ListFields`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.databases.collectionGroups.fields/list#google.firestore.admin.v1.FirestoreAdmin.ListFields) , that may be used to get the next page of results.                                                                                                                                                                                                                                                                                                                                   |

### Request body

The request body must be empty.

### Response body

The response for [`FirestoreAdmin.ListFields`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.databases.collectionGroups.fields/list#google.firestore.admin.v1.FirestoreAdmin.ListFields) .

If successful, the response body contains data with the following structure:

**JSON representation**

```
{
  "fields": [
    {
      object (Field)
    }
  ],
  "nextPageToken": string
}
```

| Fields          |                                                                                                                                                                 |
|-----------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `fields[]`      | `object ( `[`Field`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.databases.collectionGroups.fields#Field)` )` The requested fields. |
| `nextPageToken` | `string` A page token that may be used to request another page of results. If blank, this is the last page.                                                     |

### Authorization scopes

Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/datastore`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .
