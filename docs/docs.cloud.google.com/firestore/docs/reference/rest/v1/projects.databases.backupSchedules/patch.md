---
name: documents/docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.databases.backupSchedules/patch
uri: https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.databases.backupSchedules/patch
title: 'Method: projects.databases.backupSchedules.patch'
description: A cloud-hosted NoSQL database that's simple enough for rapid prototyping yet scalable and flexible enough to grow to any size.
data_source: docs.cloud.google.com
---

Updates a backup schedule.

### HTTP request

Choose a location:

  
`PATCH https://firestore.googleapis.com/v1/{backupSchedule.name=projects/*/databases/*/backupSchedules/*}`

The URLs use [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`backupSchedule.name`

`string`

Output only. The unique backup schedule identifier across all locations and databases for the given project.

This will be auto-assigned.

Format is `projects/{project}/databases/{database}/backupSchedules/{backupSchedule}`

### Query parameters

Parameters

`updateMask`

` string ( FieldMask  ` format)

The list of fields to be updated.

This is a comma-separated list of fully qualified names of fields. Example: `"user.displayName,photo"` .

### Request body

The request body contains an instance of `  BackupSchedule  ` .

### Response body

If successful, the response body contains an instance of `  BackupSchedule  ` .

### Authorization scopes

Requires one of the following OAuth scopes:

  - `https://www.googleapis.com/auth/datastore`
  - `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .
