---
name: documents/docs.cloud.google.com/firestore/docs/reference/rest/v1beta1/projects.databases.indexes/get
uri: https://docs.cloud.google.com/firestore/docs/reference/rest/v1beta1/projects.databases.indexes/get
title: 'Method: projects.databases.indexes.get'
description: A cloud-hosted NoSQL database that's simple enough for rapid prototyping yet scalable and flexible enough to grow to any size.
data_source: docs.cloud.google.com
---

Gets an index.

### HTTP request

Choose a location:

  
`GET https://firestore.googleapis.com/v1beta1/{name=projects/*/databases/*/indexes/*}`

The URLs use [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`name`

`string`

The name of the index. For example: `projects/{projectId}/databases/{databaseId}/indexes/{index_id}`

### Request body

The request body must be empty.

### Response body

If successful, the response body contains an instance of `  Index  ` .

### Authorization scopes

Requires one of the following OAuth scopes:

  - `https://www.googleapis.com/auth/datastore`
  - `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .
