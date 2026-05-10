---
name: documents/docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.databases.userCreds/create
uri: https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.databases.userCreds/create
title: 'Method: projects.databases.userCreds.create'
description: A cloud-hosted NoSQL database that's simple enough for rapid prototyping yet scalable and flexible enough to grow to any size.
data_source: docs.cloud.google.com
update_time: "2026-03-20T21:17:05Z"
---

Create a user creds.

### HTTP request

Choose a location:

  
`POST https://firestore.googleapis.com/v1/{parent=projects/*/databases/*}/userCreds`

The URLs use [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`parent`

`string`

Required. A parent name of the form `projects/{projectId}/databases/{databaseId}`

### Query parameters

Parameters

`userCredsId`

`string`

Required. The ID to use for the user creds, which will become the final component of the user creds's resource name.

This value should be 4-63 characters. Valid characters are /\[a-z\]\[0-9\]-/ with first character a letter and the last a letter or a number. Must not be UUID-like /\[0-9a-f\]{8}(-\[0-9a-f\]{4}){3}-\[0-9a-f\]{12}/.

### Request body

The request body contains an instance of `  UserCreds  ` .

### Response body

If successful, the response body contains a newly created instance of `  UserCreds  ` .

### Authorization scopes

Requires one of the following OAuth scopes:

  - `https://www.googleapis.com/auth/datastore`
  - `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .
