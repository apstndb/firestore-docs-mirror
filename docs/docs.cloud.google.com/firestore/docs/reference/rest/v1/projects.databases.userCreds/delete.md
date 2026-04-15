Deletes a user creds.

### HTTP request

Choose a location:

  
`DELETE https://firestore.googleapis.com/v1/{name=projects/*/databases/*/userCreds/*}`

The URLs use [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`name`

`string`

Required. A name of the form `projects/{projectId}/databases/{databaseId}/userCreds/{userCredsId}`

### Request body

The request body must be empty.

### Response body

If successful, the response body is an empty JSON object.

### Authorization scopes

Requires one of the following OAuth scopes:

  - `https://www.googleapis.com/auth/datastore`
  - `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .
