  - [HTTP request](#body.HTTP_TEMPLATE)
  - [Path parameters](#body.PATH_PARAMETERS)
  - [Request body](#body.request_body)
  - [Response body](#body.response_body)
  - [Authorization scopes](#body.aspect)
  - [Try it\!](#try-it)

Deletes an existing index. An index can only be deleted if it is in a `  READY  ` or `  ERROR  ` state. On successful execution of the request, the index will be in a `  DELETING  ` `  state  ` . And on completion of the returned `  google.longrunning.Operation  ` , the index will be removed.

During index deletion, the process could result in an error, in which case the index will move to the `  ERROR  ` state. The process can be recovered by fixing the data that caused the error, followed by calling `  delete  ` again.

### HTTP request

`  DELETE https://datastore.googleapis.com/v1/projects/{projectId}/indexes/{indexId}  `

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`  projectId  `

`  string  `

Project ID against which to make the request.

`  indexId  `

`  string  `

The resource ID of the index to delete.

### Request body

The request body must be empty.

### Response body

If successful, the response body contains an instance of `  Operation  ` .

### Authorization scopes

Requires one of the following OAuth scopes:

  - `  https://www.googleapis.com/auth/datastore  `
  - `  https://www.googleapis.com/auth/cloud-platform  `

For more information, see the [Authentication Overview](/docs/authentication#authorization-gcp) .
