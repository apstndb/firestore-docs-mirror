---
name: documents/docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.databases.backupSchedules/list
uri: https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.databases.backupSchedules/list
title: 'Method: projects.databases.backupSchedules.list'
description: A cloud-hosted NoSQL database that's simple enough for rapid prototyping yet scalable and flexible enough to grow to any size.
data_source: docs.cloud.google.com
---

List backup schedules.

### HTTP request

Choose a location:

  
`GET https://firestore.googleapis.com/v1/{parent=projects/*/databases/*}/backupSchedules`

The URLs use [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

| Parameters |                                                                                               |
|------------|-----------------------------------------------------------------------------------------------|
| `parent`   | `string` Required. The parent database. Format is `projects/{project}/databases/{database}` . |

### Request body

The request body must be empty.

### Response body

The response for [`FirestoreAdmin.ListBackupSchedules`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.databases.backupSchedules/list#google.firestore.admin.v1.FirestoreAdmin.ListBackupSchedules) .

If successful, the response body contains data with the following structure:

**JSON representation**

```
{
  "backupSchedules": [
    {
      object (BackupSchedule)
    }
  ]
}
```

| Fields              |                                                                                                                                                                                   |
|---------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `backupSchedules[]` | `object ( `[`BackupSchedule`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.databases.backupSchedules#BackupSchedule)` )` List of all backup schedules. |

### Authorization scopes

Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/datastore`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .
