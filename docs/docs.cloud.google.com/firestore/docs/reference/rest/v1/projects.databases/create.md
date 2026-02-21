Create a database.

### HTTP request

`  POST https://firestore.googleapis.com/v1/{parent=projects/*}/databases  `

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`  parent  `

`  string  `

Required. A parent name of the form `  projects/{projectId}  `

### Query parameters

Parameters

`  databaseId  `

`  string  `

Required. The ID to use for the database, which will become the final component of the database's resource name.

This value should be 4-63 characters. Valid characters are /\[a-z\]\[0-9\]-/ with first character a letter and the last a letter or a number. Must not be UUID-like /\[0-9a-f\]{8}(-\[0-9a-f\]{4}){3}-\[0-9a-f\]{12}/.

"(default)" database ID is also valid if the database is Standard edition.

### Request body

The request body contains an instance of `  Database  ` .

### Response body

If successful, the response body contains a newly created instance of `  Operation  ` .

### Authorization scopes

Requires one of the following OAuth scopes:

  - `  https://www.googleapis.com/auth/datastore  `
  - `  https://www.googleapis.com/auth/cloud-platform  `

For more information, see the [Authentication Overview](/docs/authentication#authorization-gcp) .
