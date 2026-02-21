Creates a backup schedule on a database. At most two backup schedules can be configured on a database, one daily backup schedule and one weekly backup schedule.

### HTTP request

`  POST https://firestore.googleapis.com/v1/{parent=projects/*/databases/*}/backupSchedules  `

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`  parent  `

`  string  `

Required. The parent database.

Format `  projects/{project}/databases/{database}  `

### Request body

The request body contains an instance of `  BackupSchedule  ` .

### Response body

If successful, the response body contains a newly created instance of `  BackupSchedule  ` .

### Authorization scopes

Requires one of the following OAuth scopes:

  - `  https://www.googleapis.com/auth/datastore  `
  - `  https://www.googleapis.com/auth/cloud-platform  `

For more information, see the [Authentication Overview](/docs/authentication#authorization-gcp) .
