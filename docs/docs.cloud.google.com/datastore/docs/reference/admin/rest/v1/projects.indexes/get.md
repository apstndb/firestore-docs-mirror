  - [HTTP request](https://docs.cloud.google.com/datastore/docs/reference/admin/rest/v1/projects.indexes/get#body.HTTP_TEMPLATE)
  - [Path parameters](https://docs.cloud.google.com/datastore/docs/reference/admin/rest/v1/projects.indexes/get#body.PATH_PARAMETERS)
  - [Request body](https://docs.cloud.google.com/datastore/docs/reference/admin/rest/v1/projects.indexes/get#body.request_body)
  - [Response body](https://docs.cloud.google.com/datastore/docs/reference/admin/rest/v1/projects.indexes/get#body.response_body)
  - [Authorization scopes](https://docs.cloud.google.com/datastore/docs/reference/admin/rest/v1/projects.indexes/get#body.aspect)
  - [Try it\!](https://docs.cloud.google.com/datastore/docs/reference/admin/rest/v1/projects.indexes/get#try-it)

Gets an index.

### HTTP request

Choose a location:

  
`GET https://datastore.googleapis.com/v1/projects/{projectId}/indexes/{indexId}`

The URLs use [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`projectId`

`string`

Project ID against which to make the request.

`indexId`

`string`

The resource ID of the index to get.

### Request body

The request body must be empty.

### Response body

If successful, the response body contains an instance of `  Index  ` .

### Authorization scopes

Requires one of the following OAuth scopes:

  - `https://www.googleapis.com/auth/datastore`
  - `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .
