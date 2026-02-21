Updates a database.

### HTTP request

`  PATCH https://firestore.googleapis.com/v1/{database.name=projects/*/databases/*}  `

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`  database.name  `

`  string  `

The resource name of the Database. Format: `  projects/{project}/databases/{database}  `

### Query parameters

Parameters

`  updateMask  `

`  string ( FieldMask  ` format)

The list of fields to be updated.

This is a comma-separated list of fully qualified names of fields. Example: `  "user.displayName,photo"  ` .

### Request body

The request body contains an instance of `  Database  ` .

### Response body

If successful, the response body contains an instance of `  Operation  ` .

### Authorization scopes

Requires one of the following OAuth scopes:

  - `  https://www.googleapis.com/auth/datastore  `
  - `  https://www.googleapis.com/auth/cloud-platform  `

For more information, see the [Authentication Overview](/docs/authentication#authorization-gcp) .
