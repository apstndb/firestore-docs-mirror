---
name: documents/docs.cloud.google.com/firestore/docs/reference/rest/v1beta1/projects.databases.documents/rollback
uri: https://docs.cloud.google.com/firestore/docs/reference/rest/v1beta1/projects.databases.documents/rollback
title: 'Method: projects.databases.documents.rollback'
description: A cloud-hosted NoSQL database that's simple enough for rapid prototyping yet scalable and flexible enough to grow to any size.
data_source: docs.cloud.google.com
---

Rolls back a transaction.

### HTTP request

Choose a location:

  
`POST https://firestore.googleapis.com/v1beta1/{database=projects/*/databases/*}/documents:rollback`

The URLs use [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

| Parameters |                                                                                                      |
|------------|------------------------------------------------------------------------------------------------------|
| `database` | `string` Required. The database name. In the format: `projects/{projectId}/databases/{databaseId}` . |

### Request body

The request body contains data with the following structure:

**JSON representation**

```
{
  "transaction": string
}
```

| Fields        |                                                                                                                                                         |
|---------------|---------------------------------------------------------------------------------------------------------------------------------------------------------|
| `transaction` | `string ( `[`bytes`](https://developers.google.com/discovery/v1/type-format)` format)` Required. The transaction to roll back. A base64-encoded string. |

### Response body

If successful, the response body is an empty JSON object.

### Authorization scopes

Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/datastore`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .
