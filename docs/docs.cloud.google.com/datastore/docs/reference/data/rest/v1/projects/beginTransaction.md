---
name: documents/docs.cloud.google.com/datastore/docs/reference/data/rest/v1/projects/beginTransaction
uri: https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/projects/beginTransaction
title: 'Method: projects.beginTransaction'
description: A highly-scalable NoSQL database for your web and mobile applications that automatically handles sharding and replication.
data_source: docs.cloud.google.com
---

- [HTTP request](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/projects/beginTransaction#body.HTTP_TEMPLATE)
- [Path parameters](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/projects/beginTransaction#body.PATH_PARAMETERS)
- [Request body](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/projects/beginTransaction#body.request_body)
  - [JSON representation](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/projects/beginTransaction#body.request_body.SCHEMA_REPRESENTATION)
- [Response body](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/projects/beginTransaction#body.response_body)
  - [JSON representation](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/projects/beginTransaction#body.BeginTransactionResponse.SCHEMA_REPRESENTATION)
- [Authorization scopes](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/projects/beginTransaction#body.aspect)
- [Try it!](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/projects/beginTransaction#try-it)

Begins a new transaction.

### HTTP request

Choose a location:

  
`POST https://datastore.googleapis.com/v1/projects/{projectId}:beginTransaction`

The URLs use [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

| Parameters  |                                                                             |
|-------------|-----------------------------------------------------------------------------|
| `projectId` | `string` Required. The ID of the project against which to make the request. |

### Request body

The request body contains data with the following structure:

**JSON representation**

```
{
  "databaseId": string,
  "transactionOptions": {
    object (TransactionOptions)
  }
}
```

| Fields               |                                                                                                                                                              |
|----------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `databaseId`         | `string` The ID of the database against which to make the request. '(default)' is not allowed; please use empty string '' to refer the default database.     |
| `transactionOptions` | `object ( `[`TransactionOptions`](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/TransactionOptions)` )` Options for a new transaction. |

### Response body

The response for [`Datastore.BeginTransaction`](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/projects/beginTransaction#google.datastore.v1.Datastore.BeginTransaction) .

If successful, the response body contains data with the following structure:

**JSON representation**

```
{
  "transaction": string
}
```

| Fields        |                                                                                                                                                              |
|---------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `transaction` | `string ( `[`bytes`](https://developers.google.com/discovery/v1/type-format)` format)` The transaction identifier (always present). A base64-encoded string. |

### Authorization scopes

Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/datastore`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .
