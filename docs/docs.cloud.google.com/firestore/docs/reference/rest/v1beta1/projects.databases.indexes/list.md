---
name: documents/docs.cloud.google.com/firestore/docs/reference/rest/v1beta1/projects.databases.indexes/list
uri: https://docs.cloud.google.com/firestore/docs/reference/rest/v1beta1/projects.databases.indexes/list
title: 'Method: projects.databases.indexes.list'
description: A cloud-hosted NoSQL database that's simple enough for rapid prototyping yet scalable and flexible enough to grow to any size.
data_source: docs.cloud.google.com
---

Lists the indexes that match the specified filters.

### HTTP request

Choose a location:

  
`GET https://firestore.googleapis.com/v1beta1/{parent=projects/*/databases/*}/indexes`

The URLs use [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

| Parameters |                                                                                        |
|------------|----------------------------------------------------------------------------------------|
| `parent`   | `string` The database name. For example: `projects/{projectId}/databases/{databaseId}` |

### Query parameters

| Parameters  |                                        |
|-------------|----------------------------------------|
| `filter`    | `string`                               |
| `pageSize`  | `integer` The standard List page size. |
| `pageToken` | `string` The standard List page token. |

### Request body

The request body must be empty.

### Response body

The response for [`FirestoreAdmin.ListIndexes`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1beta1/projects.databases.indexes/list#google.firestore.admin.v1beta1.FirestoreAdmin.ListIndexes) .

If successful, the response body contains data with the following structure:

**JSON representation**

```
{
  "indexes": [
    {
      object (Index)
    }
  ],
  "nextPageToken": string
}
```

| Fields          |                                                                                                                                             |
|-----------------|---------------------------------------------------------------------------------------------------------------------------------------------|
| `indexes[]`     | `object ( `[`Index`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1beta1/projects.databases.indexes#Index)` )` The indexes. |
| `nextPageToken` | `string` The standard List next-page token.                                                                                                 |

### Authorization scopes

Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/datastore`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .
