Gets information about a location.

### HTTP request

`  GET https://firestore.googleapis.com/v1/{name=projects/*/locations/*}  `

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`  name  `

`  string  `

Resource name for the location.

### Request body

The request body must be empty.

### Response body

If successful, the response body contains an instance of `  Location  ` .

### Authorization scopes

Requires one of the following OAuth scopes:

  - `  https://www.googleapis.com/auth/datastore  `
  - `  https://www.googleapis.com/auth/cloud-platform  `

For more information, see the [Authentication Overview](/docs/authentication#authorization-gcp) .
