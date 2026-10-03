---
name: documents/docs.cloud.google.com/datastore/docs/reference/admin/rest/v1/projects.indexes/list
uri: https://docs.cloud.google.com/datastore/docs/reference/admin/rest/v1/projects.indexes/list
title: 'Method: projects.indexes.list'
description: A highly-scalable NoSQL database for your web and mobile applications that automatically handles sharding and replication.
data_source: docs.cloud.google.com
---

- [HTTP request](https://docs.cloud.google.com/datastore/docs/reference/admin/rest/v1/projects.indexes/list#body.HTTP_TEMPLATE)
- [Path parameters](https://docs.cloud.google.com/datastore/docs/reference/admin/rest/v1/projects.indexes/list#body.PATH_PARAMETERS)
- [Query parameters](https://docs.cloud.google.com/datastore/docs/reference/admin/rest/v1/projects.indexes/list#body.QUERY_PARAMETERS)
- [Request body](https://docs.cloud.google.com/datastore/docs/reference/admin/rest/v1/projects.indexes/list#body.request_body)
- [Response body](https://docs.cloud.google.com/datastore/docs/reference/admin/rest/v1/projects.indexes/list#body.response_body)
  - [JSON representation](https://docs.cloud.google.com/datastore/docs/reference/admin/rest/v1/projects.indexes/list#body.ListIndexesResponse.SCHEMA_REPRESENTATION)
- [Authorization scopes](https://docs.cloud.google.com/datastore/docs/reference/admin/rest/v1/projects.indexes/list#body.aspect)
- [Try it!](https://docs.cloud.google.com/datastore/docs/reference/admin/rest/v1/projects.indexes/list#try-it)

Lists the indexes that match the specified filters. Datastore uses an eventually consistent query to fetch the list of indexes and may occasionally return stale results.

### HTTP request

Choose a location:

  
`GET https://datastore.googleapis.com/v1/projects/{projectId}/indexes`

The URLs use [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

| Parameters  |                                                        |
|-------------|--------------------------------------------------------|
| `projectId` | `string` Project ID against which to make the request. |

### Query parameters

| Parameters  |                                                                                              |
|-------------|----------------------------------------------------------------------------------------------|
| `filter`    | `string`                                                                                     |
| `pageSize`  | `integer` The maximum number of items to return. If zero, then all results will be returned. |
| `pageToken` | `string` The nextPageToken value returned from a previous List request, if any.              |

### Request body

The request body must be empty.

### Response body

The response for [`google.datastore.admin.v1.DatastoreAdmin.ListIndexes`](https://docs.cloud.google.com/datastore/docs/reference/admin/rest/v1/projects.indexes/list#google.datastore.admin.v1.DatastoreAdmin.ListIndexes) .

If successful, the response body contains data with the following structure:

**JSON representation**

```
{
  "indexes": [
    {
      object (Index)
    }
  ],
  "nextPageToken": string
}
```

| Fields          |                                                                                                                                    |
|-----------------|------------------------------------------------------------------------------------------------------------------------------------|
| `indexes[]`     | `object ( `[`Index`](https://docs.cloud.google.com/datastore/docs/reference/admin/rest/v1/projects.indexes#Index)` )` The indexes. |
| `nextPageToken` | `string` The standard List next-page token.                                                                                        |

### Authorization scopes

Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/datastore`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .
