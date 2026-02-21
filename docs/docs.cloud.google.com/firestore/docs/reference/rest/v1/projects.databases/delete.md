Deletes a database.

### HTTP request

`  DELETE https://firestore.googleapis.com/v1/{name=projects/*/databases/*}  `

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`  name  `

`  string  `

Required. A name of the form `  projects/{projectId}/databases/{databaseId}  `

### Query parameters

Parameters

`  etag  `

`  string  `

The current etag of the Database. If an etag is provided and does not match the current etag of the database, deletion will be blocked and a FAILED\_PRECONDITION error will be returned.

### Request body

The request body must be empty.

### Response body

If successful, the response body contains an instance of `  Operation  ` .

### Authorization scopes

Requires one of the following OAuth scopes:

  - `  https://www.googleapis.com/auth/datastore  `
  - `  https://www.googleapis.com/auth/cloud-platform  `

For more information, see the [Authentication Overview](/docs/authentication#authorization-gcp) .
