  - [HTTP request](https://docs.cloud.google.com/datastore/docs/reference/admin/rest/v1/projects.operations/get#body.HTTP_TEMPLATE)
  - [Path parameters](https://docs.cloud.google.com/datastore/docs/reference/admin/rest/v1/projects.operations/get#body.PATH_PARAMETERS)
  - [Request body](https://docs.cloud.google.com/datastore/docs/reference/admin/rest/v1/projects.operations/get#body.request_body)
  - [Response body](https://docs.cloud.google.com/datastore/docs/reference/admin/rest/v1/projects.operations/get#body.response_body)
  - [Authorization scopes](https://docs.cloud.google.com/datastore/docs/reference/admin/rest/v1/projects.operations/get#body.aspect)
  - [Try it\!](https://docs.cloud.google.com/datastore/docs/reference/admin/rest/v1/projects.operations/get#try-it)

Gets the latest state of a long-running operation. Clients can use this method to poll the operation result at intervals as recommended by the API service.

### HTTP request

Choose a location:

  
`GET https://datastore.googleapis.com/v1/{name=projects/*/operations/*}`

The URLs use [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`name`

`string`

The name of the operation resource.

### Request body

The request body must be empty.

### Response body

If successful, the response body contains an instance of `  Operation  ` .

### Authorization scopes

Requires one of the following OAuth scopes:

  - `https://www.googleapis.com/auth/datastore`
  - `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .
