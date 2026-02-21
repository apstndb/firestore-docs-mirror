List all user creds in the database. Note that the returned resource does not contain the secret value itself.

### HTTP request

`  GET https://firestore.googleapis.com/v1/{parent=projects/*/databases/*}/userCreds  `

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`  parent  `

`  string  `

Required. A parent database name of the form `  projects/{projectId}/databases/{databaseId}  `

### Request body

The request body must be empty.

### Response body

The response for `  FirestoreAdmin.ListUserCreds  ` .

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
  &quot;userCreds&quot;: [
    {
      object (UserCreds)
    }
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  userCreds[]  `

`  object ( UserCreds  ` )

The user creds for the database.

### Authorization scopes

Requires one of the following OAuth scopes:

  - `  https://www.googleapis.com/auth/datastore  `
  - `  https://www.googleapis.com/auth/cloud-platform  `

For more information, see the [Authentication Overview](/docs/authentication#authorization-gcp) .
