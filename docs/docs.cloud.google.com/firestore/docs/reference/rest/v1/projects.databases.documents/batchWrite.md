---
name: documents/docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.databases.documents/batchWrite
uri: https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.databases.documents/batchWrite
title: 'Method: projects.databases.documents.batchWrite'
description: A cloud-hosted NoSQL database that's simple enough for rapid prototyping yet scalable and flexible enough to grow to any size.
data_source: docs.cloud.google.com
---

Applies a batch of write operations.

The documents.batchWrite method does not apply the write operations atomically and can apply them out of order. Method does not allow more than one write per document. Each write succeeds or fails independently. See the [`BatchWriteResponse`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.databases.documents/batchWrite#body.BatchWriteResponse) for the success status of each write.

If you require an atomically applied set of writes, use [`documents.commit`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.databases.documents/commit#google.firestore.v1.Firestore.Commit) instead.

### HTTP request

Choose a location:

  
`POST https://firestore.googleapis.com/v1/{database=projects/*/databases/*}/documents:batchWrite`

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
  "writes": [
    {
      object (Write)
    }
  ],
  "labels": {
    string: string,
    ...
  }
}
```

| Fields     |                                                                                                                                                                                                                                                                                                            |
|------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `writes[]` | `object ( `[`Write`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1/Write)` )` The writes to apply. Method does not apply writes atomically and does not guarantee ordering. Each write succeeds or fails independently. You cannot write to the same document more than once per request. |
| `labels`   | `map (key: string, value: string)` Labels associated with this batch write. An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` .                                                                                                          |

### Response body

The response from [`Firestore.BatchWrite`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.databases.documents/batchWrite#google.firestore.v1.Firestore.BatchWrite) .

If successful, the response body contains data with the following structure:

**JSON representation**

```
{
  "writeResults": [
    {
      object (WriteResult)
    }
  ],
  "status": [
    {
      object (Status)
    }
  ]
}
```

| Fields           |                                                                                                                                                                                                                              |
|------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `writeResults[]` | `object ( `[`WriteResult`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1/WriteResult)` )` The result of applying the writes. This i-th write result corresponds to the i-th write in the request.           |
| `status[]`       | `object ( `[`Status`](https://docs.cloud.google.com/firestore/docs/reference/rest/Shared.Types/Operation#Status)` )` The status of applying the writes. This i-th write status corresponds to the i-th write in the request. |

### Authorization scopes

Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/datastore`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .
