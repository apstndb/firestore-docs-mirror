---
name: documents/docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.databases.documents/beginTransaction
uri: https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.databases.documents/beginTransaction
title: 'Method: projects.databases.documents.beginTransaction'
description: A cloud-hosted NoSQL database that's simple enough for rapid prototyping yet scalable and flexible enough to grow to any size.
data_source: docs.cloud.google.com
---

Starts a new transaction.

### HTTP request

Choose a location:

  
`POST https://firestore.googleapis.com/v1/{database=projects/*/databases/*}/documents:beginTransaction`

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
  "options": {
    object (TransactionOptions)
  }
}
```

| Fields    |                                                                                                                                                                                                 |
|-----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `options` | `object ( `[`TransactionOptions`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1/TransactionOptions)` )` The options for the transaction. Defaults to a read-write transaction. |

### Response body

The response for [`Firestore.BeginTransaction`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.databases.documents/beginTransaction#google.firestore.v1.Firestore.BeginTransaction) .

If successful, the response body contains data with the following structure:

**JSON representation**

```
{
  "transaction": string
}
```

| Fields        |                                                                                                                                                   |
|---------------|---------------------------------------------------------------------------------------------------------------------------------------------------|
| `transaction` | `string ( `[`bytes`](https://developers.google.com/discovery/v1/type-format)` format)` The transaction that was started. A base64-encoded string. |

### Authorization scopes

Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/datastore`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .
