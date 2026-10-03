---
name: documents/docs.cloud.google.com/datastore/docs/reference/data/rest/v1beta3/projects/beginTransaction
uri: https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1beta3/projects/beginTransaction
title: 'Method: projects.beginTransaction'
description: A highly-scalable NoSQL database for your web and mobile applications that automatically handles sharding and replication.
data_source: docs.cloud.google.com
---

- [HTTP request](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1beta3/projects/beginTransaction#body.HTTP_TEMPLATE)
- [Path parameters](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1beta3/projects/beginTransaction#body.PATH_PARAMETERS)
- [Request body](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1beta3/projects/beginTransaction#body.request_body)
  - [JSON representation](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1beta3/projects/beginTransaction#body.request_body.SCHEMA_REPRESENTATION)
- [Response body](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1beta3/projects/beginTransaction#body.response_body)
  - [JSON representation](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1beta3/projects/beginTransaction#body.BeginTransactionResponse.SCHEMA_REPRESENTATION)
- [Authorization scopes](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1beta3/projects/beginTransaction#body.aspect)
- [TransactionOptions](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1beta3/projects/beginTransaction#TransactionOptions)
  - [JSON representation](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1beta3/projects/beginTransaction#TransactionOptions.SCHEMA_REPRESENTATION)
- [ReadWrite](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1beta3/projects/beginTransaction#ReadWrite)
  - [JSON representation](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1beta3/projects/beginTransaction#ReadWrite.SCHEMA_REPRESENTATION)
- [ReadOnly](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1beta3/projects/beginTransaction#ReadOnly)
  - [JSON representation](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1beta3/projects/beginTransaction#ReadOnly.SCHEMA_REPRESENTATION)
- [Try it!](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1beta3/projects/beginTransaction#try-it)

Begins a new transaction.

### HTTP request

Choose a location:

  
`POST https://datastore.googleapis.com/v1beta3/projects/{projectId}:beginTransaction`

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
  "transactionOptions": {
    object (TransactionOptions)
  }
}
```

| Fields               |                                                                                                                                                                                             |
|----------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `transactionOptions` | `object ( `[`TransactionOptions`](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1beta3/projects/beginTransaction#TransactionOptions)` )` Options for a new transaction. |

### Response body

The response for [`Datastore.BeginTransaction`](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1beta3/projects/beginTransaction#google.datastore.v1beta3.Datastore.BeginTransaction) .

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

## TransactionOptions

Options for beginning a new transaction.

Transactions can be created explicitly with calls to [`Datastore.BeginTransaction`](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1beta3/projects/beginTransaction#google.datastore.v1beta3.Datastore.BeginTransaction) or implicitly by setting `ReadOptions.new_transaction` in read requests.

**JSON representation**

```
{

  // Union field mode can be only one of the following:
  "readWrite": {
    object (ReadWrite)
  },
  "readOnly": {
    object (ReadOnly)
  }
  // End of list of possible types for union field mode.
}
```

| Fields                                                                                                                                          |                                                                                                                                                                                                |
|-------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `mode` . The `mode` of the transaction, indicating whether write operations are supported. `mode` can be only one of the following: |                                                                                                                                                                                                |
| `readWrite`                                                                                                                                     | `object ( `[`ReadWrite`](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1beta3/projects/beginTransaction#ReadWrite)` )` The transaction should allow both reads and writes. |
| `readOnly`                                                                                                                                      | `object ( `[`ReadOnly`](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1beta3/projects/beginTransaction#ReadOnly)` )` The transaction should only allow reads.              |

## ReadWrite

Options specific to read / write transactions.

**JSON representation**

```
{
  "previousTransaction": string
}
```

| Fields                |                                                                                                                                                                              |
|-----------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `previousTransaction` | `string ( `[`bytes`](https://developers.google.com/discovery/v1/type-format)` format)` The transaction identifier of the transaction being retried. A base64-encoded string. |

## ReadOnly

Options specific to read-only transactions.

**JSON representation**

```
{
  "readTime": string
}
```

| Fields     |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
|------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `readTime` | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Reads entities at the given time. This must be a microsecond precision timestamp within the past one hour, or if Point-in-Time Recovery is enabled, can additionally be a whole minute timestamp within the past 7 days. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` . |
