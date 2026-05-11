---
name: documents/docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.locations.backups/get
uri: https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.locations.backups/get
title: 'Method: projects.locations.backups.get'
description: A cloud-hosted NoSQL database that's simple enough for rapid prototyping yet scalable and flexible enough to grow to any size.
data_source: docs.cloud.google.com
---

Gets information about a backup.

### HTTP request

Choose a location:

  
`GET https://firestore.googleapis.com/v1/{name=projects/*/locations/*/backups/*}`

The URLs use [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`name`

`string`

Required. Name of the backup to fetch.

Format is `projects/{project}/locations/{location}/backups/{backup}` .

### Request body

The request body must be empty.

### Response body

If successful, the response body contains an instance of `  Backup  ` .

### Authorization scopes

Requires one of the following OAuth scopes:

  - `https://www.googleapis.com/auth/datastore`
  - `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .
