---
name: documents/docs.cloud.google.com/firestore/docs/reference/rest/v1beta2/projects.databases.collectionGroups.indexes/create
uri: https://docs.cloud.google.com/firestore/docs/reference/rest/v1beta2/projects.databases.collectionGroups.indexes/create
title: 'Method: projects.databases.collectionGroups.indexes.create'
description: A cloud-hosted NoSQL database that's simple enough for rapid prototyping yet scalable and flexible enough to grow to any size.
data_source: docs.cloud.google.com
---

Creates a composite index. This returns a `  google.longrunning.Operation  ` which may be used to track the status of the creation. The metadata for the operation will be the type `IndexOperationMetadata` .

### HTTP request

Choose a location:

  
`POST https://firestore.googleapis.com/v1beta2/{parent=projects/*/databases/*/collectionGroups/*}/indexes`

The URLs use [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`parent`

`string`

A parent name of the form `projects/{projectId}/databases/{databaseId}/collectionGroups/{collectionId}`

### Request body

The request body contains an instance of `Index` .

### Response body

If successful, the response body contains a newly created instance of `  Operation  ` .

### Authorization scopes

Requires one of the following OAuth scopes:

  - `https://www.googleapis.com/auth/datastore`
  - `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .
