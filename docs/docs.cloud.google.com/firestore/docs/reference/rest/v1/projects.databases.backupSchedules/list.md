List backup schedules.

### HTTP request

`  GET https://firestore.googleapis.com/v1/{parent=projects/*/databases/*}/backupSchedules  `

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`  parent  `

`  string  `

Required. The parent database.

Format is `  projects/{project}/databases/{database}  ` .

### Request body

The request body must be empty.

### Response body

The response for `  FirestoreAdmin.ListBackupSchedules  ` .

If successful, the response body contains data with the following structure:

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;backupSchedules&quot;: [
    {
      object (BackupSchedule)
    }
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  backupSchedules[]  `

`  object ( BackupSchedule  ` )

List of all backup schedules.

### Authorization scopes

Requires one of the following OAuth scopes:

  - `  https://www.googleapis.com/auth/datastore  `
  - `  https://www.googleapis.com/auth/cloud-platform  `

For more information, see the [Authentication Overview](/docs/authentication#authorization-gcp) .
