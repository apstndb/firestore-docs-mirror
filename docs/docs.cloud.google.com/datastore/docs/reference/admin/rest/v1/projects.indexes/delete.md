  - [HTTP request](https://docs.cloud.google.com/datastore/docs/reference/admin/rest/v1/projects.indexes/delete#body.HTTP_TEMPLATE)
  - [Path parameters](https://docs.cloud.google.com/datastore/docs/reference/admin/rest/v1/projects.indexes/delete#body.PATH_PARAMETERS)
  - [Request body](https://docs.cloud.google.com/datastore/docs/reference/admin/rest/v1/projects.indexes/delete#body.request_body)
  - [Response body](https://docs.cloud.google.com/datastore/docs/reference/admin/rest/v1/projects.indexes/delete#body.response_body)
  - [Authorization scopes](https://docs.cloud.google.com/datastore/docs/reference/admin/rest/v1/projects.indexes/delete#body.aspect)
  - [Try it\!](https://docs.cloud.google.com/datastore/docs/reference/admin/rest/v1/projects.indexes/delete#try-it)

Deletes an existing index. An index can only be deleted if it is in a `READY` or `ERROR` state. On successful execution of the request, the index will be in a `DELETING` `  state  ` . And on completion of the returned `  google.longrunning.Operation  ` , the index will be removed.

During index deletion, the process could result in an error, in which case the index will move to the `ERROR` state. The process can be recovered by fixing the data that caused the error, followed by calling `  delete  ` again.

### HTTP request

Choose a location:

  
`DELETE https://datastore.googleapis.com/v1/projects/{projectId}/indexes/{indexId}`

The URLs use [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`projectId`

`string`

Project ID against which to make the request.

`indexId`

`string`

The resource ID of the index to delete.

### Request body

The request body must be empty.

### Response body

If successful, the response body contains an instance of `  Operation  ` .

### Authorization scopes

Requires one of the following OAuth scopes:

  - `https://www.googleapis.com/auth/datastore`
  - `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .
