---
name: documents/docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.databases.backupSchedules/create
uri: https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.databases.backupSchedules/create
title: 'Method: projects.databases.backupSchedules.create'
description: A cloud-hosted NoSQL database that's simple enough for rapid prototyping yet scalable and flexible enough to grow to any size.
data_source: docs.cloud.google.com
update_time: "2026-03-20T21:17:05Z"
---

Creates a backup schedule on a database. At most two backup schedules can be configured on a database, one daily backup schedule and one weekly backup schedule.

### HTTP request

Choose a location:

  
`POST https://firestore.googleapis.com/v1/{parent=projects/*/databases/*}/backupSchedules`

The URLs use [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`parent`

`string`

Required. The parent database.

Format `projects/{project}/databases/{database}`

### Request body

The request body contains an instance of `  BackupSchedule  ` .

### Response body

If successful, the response body contains a newly created instance of `  BackupSchedule  ` .

### Authorization scopes

Requires one of the following OAuth scopes:

  - `https://www.googleapis.com/auth/datastore`
  - `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .
