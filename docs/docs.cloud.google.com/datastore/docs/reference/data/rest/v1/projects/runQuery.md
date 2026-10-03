---
name: documents/docs.cloud.google.com/datastore/docs/reference/data/rest/v1/projects/runQuery
uri: https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/projects/runQuery
title: 'Method: projects.runQuery'
description: A highly-scalable NoSQL database for your web and mobile applications that automatically handles sharding and replication.
data_source: docs.cloud.google.com
---

- [HTTP request](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/projects/runQuery#body.HTTP_TEMPLATE)
- [Path parameters](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/projects/runQuery#body.PATH_PARAMETERS)
- [Request body](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/projects/runQuery#body.request_body)
  - [JSON representation](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/projects/runQuery#body.request_body.SCHEMA_REPRESENTATION)
- [Response body](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/projects/runQuery#body.response_body)
  - [JSON representation](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/projects/runQuery#body.RunQueryResponse.SCHEMA_REPRESENTATION)
- [Authorization scopes](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/projects/runQuery#body.aspect)
- [QueryResultBatch](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/projects/runQuery#QueryResultBatch)
  - [JSON representation](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/projects/runQuery#QueryResultBatch.SCHEMA_REPRESENTATION)
- [ResultType](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/projects/runQuery#ResultType)
- [Try it!](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/projects/runQuery#try-it)

Queries for entities.

### HTTP request

Choose a location:

  
`POST https://datastore.googleapis.com/v1/projects/{projectId}:runQuery`

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
  "partitionId": {
    object (PartitionId)
  },
  "readOptions": {
    object (ReadOptions)
  },
  "propertyMask": {
    object (PropertyMask)
  },
  "explainOptions": {
    object (ExplainOptions)
  },

  // Union field query_type can be only one of the following:
  "query": {
    object (Query)
  },
  "gqlQuery": {
    object (GqlQuery)
  }
  // End of list of possible types for union field query_type.
}
```

| Fields                                                                                       |                                                                                                                                                                                                                                                                                                                                                                  |
|----------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `databaseId`                                                                                 | `string` The ID of the database against which to make the request. '(default)' is not allowed; please use empty string '' to refer the default database.                                                                                                                                                                                                         |
| `partitionId`                                                                                | `object ( `[`PartitionId`](https://docs.cloud.google.com/datastore/docs/reference/data/rest/Shared.Types/Value#PartitionId)` )` Entities are partitioned into subsets, identified by a partition ID. Queries are scoped to a single partition. This partition ID is normalized with the standard default context partition ID.                                   |
| `readOptions`                                                                                | `object ( `[`ReadOptions`](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/ReadOptions)` )` The options for this query.                                                                                                                                                                                                                      |
| `propertyMask`                                                                               | `object ( `[`PropertyMask`](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/PropertyMask)` )` The properties to return. This field must not be set for a projection query. See [`LookupRequest.property_mask`](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/projects/lookup#body.request_body.FIELDS.property_mask) . |
| `explainOptions`                                                                             | `object ( `[`ExplainOptions`](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/ExplainOptions)` )` Optional. Explain options for the query. If set, additional query statistics will be returned. If not, only query results will be returned.                                                                                                |
| Union field `query_type` . The type of query. `query_type` can be only one of the following: |                                                                                                                                                                                                                                                                                                                                                                  |
| `query`                                                                                      | `object ( `[`Query`](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/Query)` )` The query to run.                                                                                                                                                                                                                                            |
| `gqlQuery`                                                                                   | `object ( `[`GqlQuery`](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/GqlQuery)` )` The GQL query to run. This query must be a non-aggregation query.                                                                                                                                                                                      |

### Response body

The response for [`Datastore.RunQuery`](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/projects/runQuery#google.datastore.v1.Datastore.RunQuery) .

If successful, the response body contains data with the following structure:

**JSON representation**

```
{
  "batch": {
    object (QueryResultBatch)
  },
  "query": {
    object (Query)
  },
  "transaction": string,
  "explainMetrics": {
    object (ExplainMetrics)
  }
}
```

| Fields           |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
|------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `batch`          | `object ( `[`QueryResultBatch`](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/projects/runQuery#QueryResultBatch)` )` A batch of query results. This is always present unless running a query under explain-only mode: [`RunQueryRequest.explain_options`](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/projects/runQuery#body.request_body.FIELDS.explain_options) was provided and [`ExplainOptions.analyze`](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/ExplainOptions#FIELDS.analyze) was set to false. |
| `query`          | `object ( `[`Query`](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/Query)` )` The parsed form of the `GqlQuery` from the request, if it was set.                                                                                                                                                                                                                                                                                                                                                                                                            |
| `transaction`    | `string ( `[`bytes`](https://developers.google.com/discovery/v1/type-format)` format)` The identifier of the transaction that was started as part of this projects.runQuery request. Set only when [`ReadOptions.new_transaction`](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/ReadOptions#FIELDS.new_transaction) was set in [`RunQueryRequest.read_options`](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/projects/runQuery#body.request_body.FIELDS.read_options) . A base64-encoded string.                                    |
| `explainMetrics` | `object ( `[`ExplainMetrics`](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/ExplainMetrics)` )` Query explain metrics. This is only present when the [`RunQueryRequest.explain_options`](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/projects/runQuery#body.request_body.FIELDS.explain_options) is provided, and it is sent only once with the last response in the stream.                                                                                                                                                        |

### Authorization scopes

Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/datastore`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

## QueryResultBatch

A batch of results produced by a query.

**JSON representation**

```
{
  "skippedResults": integer,
  "skippedCursor": string,
  "entityResultType": enum (ResultType),
  "entityResults": [
    {
      object (EntityResult)
    }
  ],
  "endCursor": string,
  "moreResults": enum (MoreResultsType),
  "snapshotVersion": string,
  "readTime": string
}
```

| Fields             |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
|--------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `skippedResults`   | `integer` The number of results skipped, typically because of an offset.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| `skippedCursor`    | `string ( `[`bytes`](https://developers.google.com/discovery/v1/type-format)` format)` A cursor that points to the position after the last skipped result. Will be set when `skippedResults` != 0. A base64-encoded string.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| `entityResultType` | `enum ( `[`ResultType`](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/projects/runQuery#ResultType)` )` The result type for every entity in `entityResults` .                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| `entityResults[]`  | `object ( `[`EntityResult`](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/EntityResult)` )` The results for this batch.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `endCursor`        | `string ( `[`bytes`](https://developers.google.com/discovery/v1/type-format)` format)` A cursor that points to the position after the last result in the batch. A base64-encoded string.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| `moreResults`      | `enum ( `[`MoreResultsType`](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/MoreResultsType)` )` The state of the query after the current batch.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| `snapshotVersion`  | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` The version number of the snapshot this batch was returned from. This applies to the range of results from the query's `startCursor` (or the beginning of the query if no cursor was given) to this batch's `endCursor` (not the query's `endCursor` ). In a single transaction, subsequent query result batches for the same query can have a greater snapshot version number. Each batch's snapshot version is valid for all preceding batches. The value will be zero for eventually consistent queries.                                                                                                                                                                                                                                                                   |
| `readTime`         | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Read timestamp this batch was returned from. This applies to the range of results from the query's `startCursor` (or the beginning of the query if no cursor was given) to this batch's `endCursor` (not the query's `endCursor` ). In a single transaction, subsequent query result batches for the same query can have a greater timestamp. Each batch's read timestamp is valid for all preceding batches. This value will not be set for eventually consistent queries in Cloud Datastore. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` . |

## ResultType

Specifies what data the 'entity' field contains. A `ResultType` is either implied (for example, in `LookupResponse.missing` from `datastore.proto` , it is always `KEY_ONLY` ) or specified by context (for example, in message `QueryResultBatch` , field `entityResultType` specifies a `ResultType` for all the values in field `entityResults` ).

| Enums                     |                                                               |
|---------------------------|---------------------------------------------------------------|
| `RESULT_TYPE_UNSPECIFIED` | Unspecified. This value is never used.                        |
| `FULL`                    | The key and properties.                                       |
| `PROJECTION`              | A projected subset of properties. The entity may have no key. |
| `KEY_ONLY`                | Only the key.                                                 |
