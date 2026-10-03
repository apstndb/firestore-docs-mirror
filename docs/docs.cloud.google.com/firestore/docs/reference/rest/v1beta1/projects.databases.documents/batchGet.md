---
name: documents/docs.cloud.google.com/firestore/docs/reference/rest/v1beta1/projects.databases.documents/batchGet
uri: https://docs.cloud.google.com/firestore/docs/reference/rest/v1beta1/projects.databases.documents/batchGet
title: 'Method: projects.databases.documents.batchGet'
description: A cloud-hosted NoSQL database that's simple enough for rapid prototyping yet scalable and flexible enough to grow to any size.
data_source: docs.cloud.google.com
---

Gets multiple documents.

Documents returned by this method are not guaranteed to be returned in the same order that they were requested.

### HTTP request

Choose a location:

  
`POST https://firestore.googleapis.com/v1beta1/{database=projects/*/databases/*}/documents:batchGet`

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
  "documents": [
    string
  ],
  "mask": {
    object (DocumentMask)
  },

  // Union field consistency_selector can be only one of the following:
  "transaction": string,
  "newTransaction": {
    object (TransactionOptions)
  },
  "readTime": string
  // End of list of possible types for union field consistency_selector.
}
```

| Fields                                                                                                                                                                               |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `documents[]`                                                                                                                                                                        | `string` The names of the documents to retrieve. In the format: `projects/{projectId}/databases/{databaseId}/documents/{document_path}` . The request will fail if any of the document is not a child resource of the given `database` . Duplicate names will be elided.                                                                                                                                                                                                                                                                                                                                     |
| `mask`                                                                                                                                                                               | `object ( `[`DocumentMask`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1beta1/DocumentMask)` )` The fields to return. If not set, returns all fields. If a document has a field that is not present in this mask, that field will not be returned in the response.                                                                                                                                                                                                                                                                                                                         |
| Union field `consistency_selector` . The consistency mode for this transaction. If not set, defaults to strong consistency. `consistency_selector` can be only one of the following: |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| `transaction`                                                                                                                                                                        | `string ( `[`bytes`](https://developers.google.com/discovery/v1/type-format)` format)` Reads documents in a transaction. A base64-encoded string.                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| `newTransaction`                                                                                                                                                                     | `object ( `[`TransactionOptions`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1beta1/TransactionOptions)` )` Starts a new transaction and reads the documents. Defaults to a read-only transaction. The new transaction ID will be returned as the first response in the stream.                                                                                                                                                                                                                                                                                                            |
| `readTime`                                                                                                                                                                           | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Reads documents as they were at the given time. This must be a microsecond precision timestamp within the past one hour, or if Point-in-Time Recovery is enabled, can additionally be a whole minute timestamp within the past 7 days. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` . |

### Response body

The streamed response for [`Firestore.BatchGetDocuments`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1beta1/projects.databases.documents/batchGet#google.firestore.v1beta1.Firestore.BatchGetDocuments) .

If successful, the response body contains data with the following structure:

**JSON representation**

```
{
  "transaction": string,
  "readTime": string,

  // Union field result can be only one of the following:
  "found": {
    object (Document)
  },
  "missing": string
  // End of list of possible types for union field result.
}
```

| Fields                                                                                                                                              |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
|-----------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `transaction`                                                                                                                                       | `string ( `[`bytes`](https://developers.google.com/discovery/v1/type-format)` format)` The transaction that was started as part of this request. Will only be set in the first response, and only if [`BatchGetDocumentsRequest.new_transaction`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1beta1/projects.databases.documents/batchGet#body.request_body.FIELDS.new_transaction) was set in the request. A base64-encoded string.                                                                                                                              |
| `readTime`                                                                                                                                          | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` The time at which the document was read. This may be monotically increasing, in this case the previous documents in the result stream are guaranteed not to have changed between their readTime and this one. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` . |
| Union field `result` . A single result. This can be empty if the server is just returning a transaction. `result` can be only one of the following: |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| `found`                                                                                                                                             | `object ( `[`Document`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1beta1/projects.databases.documents#Document)` )` A document that was requested.                                                                                                                                                                                                                                                                                                                                                                                                               |
| `missing`                                                                                                                                           | `string` A document name that was requested but does not exist. In the format: `projects/{projectId}/databases/{databaseId}/documents/{document_path}` .                                                                                                                                                                                                                                                                                                                                                                                                                            |

### Authorization scopes

Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/datastore`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .
