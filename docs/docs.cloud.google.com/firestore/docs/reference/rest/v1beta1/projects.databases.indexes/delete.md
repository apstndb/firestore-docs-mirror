---
name: documents/docs.cloud.google.com/firestore/docs/reference/rest/v1beta1/projects.databases.indexes/delete
uri: https://docs.cloud.google.com/firestore/docs/reference/rest/v1beta1/projects.databases.indexes/delete
title: 'Method: projects.databases.indexes.delete'
description: A cloud-hosted NoSQL database that's simple enough for rapid prototyping yet scalable and flexible enough to grow to any size.
data_source: docs.cloud.google.com
update_time: "2026-03-20T21:17:05Z"
---

Deletes an index.

### HTTP request

Choose a location:

  
`DELETE https://firestore.googleapis.com/v1beta1/{name=projects/*/databases/*/indexes/*}`

The URLs use [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`name`

`string`

The index name. For example: `projects/{projectId}/databases/{databaseId}/indexes/{index_id}`

### Request body

The request body must be empty.

### Response body

If successful, the response body is an empty JSON object.

### Authorization scopes

Requires one of the following OAuth scopes:

  - `https://www.googleapis.com/auth/datastore`
  - `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .
