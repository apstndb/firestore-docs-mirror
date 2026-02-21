Disables a user creds. No-op if the user creds are already disabled.

### HTTP request

`  POST https://firestore.googleapis.com/v1/{name=projects/*/databases/*/userCreds/*}:disable  `

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`  name  `

`  string  `

Required. A name of the form `  projects/{projectId}/databases/{databaseId}/userCreds/{userCredsId}  `

### Request body

The request body must be empty.

### Response body

If successful, the response body contains an instance of `  UserCreds  ` .

### Authorization scopes

Requires one of the following OAuth scopes:

  - `  https://www.googleapis.com/auth/datastore  `
  - `  https://www.googleapis.com/auth/cloud-platform  `

For more information, see the [Authentication Overview](/docs/authentication#authorization-gcp) .
