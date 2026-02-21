  - [HTTP request](#body.HTTP_TEMPLATE)
  - [Path parameters](#body.PATH_PARAMETERS)
  - [Request body](#body.request_body)
      - [JSON representation](#body.request_body.SCHEMA_REPRESENTATION)
  - [Response body](#body.response_body)
      - [JSON representation](#body.RunQueryResponse.SCHEMA_REPRESENTATION)
  - [Authorization scopes](#body.aspect)
  - [QueryResultBatch](#QueryResultBatch)
      - [JSON representation](#QueryResultBatch.SCHEMA_REPRESENTATION)
  - [ResultType](#ResultType)
  - [Try it\!](#try-it)

Queries for entities.

### HTTP request

`  POST https://datastore.googleapis.com/v1/projects/{projectId}:runQuery  `

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`  projectId  `

`  string  `

Required. The ID of the project against which to make the request.

### Request body

The request body contains data with the following structure:

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;databaseId&quot;: string,
  &quot;partitionId&quot;: {
    object (PartitionId)
  },
  &quot;readOptions&quot;: {
    object (ReadOptions)
  },
  &quot;propertyMask&quot;: {
    object (PropertyMask)
  },
  &quot;explainOptions&quot;: {
    object (ExplainOptions)
  },

  // Union field query_type can be only one of the following:
  &quot;query&quot;: {
    object (Query)
  },
  &quot;gqlQuery&quot;: {
    object (GqlQuery)
  }
  // End of list of possible types for union field query_type.
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  databaseId  `

`  string  `

The ID of the database against which to make the request.

'(default)' is not allowed; please use empty string '' to refer the default database.

`  partitionId  `

`  object ( PartitionId  ` )

Entities are partitioned into subsets, identified by a partition ID. Queries are scoped to a single partition. This partition ID is normalized with the standard default context partition ID.

`  readOptions  `

`  object ( ReadOptions  ` )

The options for this query.

`  propertyMask  `

`  object ( PropertyMask  ` )

The properties to return. This field must not be set for a projection query.

See `  LookupRequest.property_mask  ` .

`  explainOptions  `

`  object ( ExplainOptions  ` )

Optional. Explain options for the query. If set, additional query statistics will be returned. If not, only query results will be returned.

Union field `  query_type  ` . The type of query. `  query_type  ` can be only one of the following:

`  query  `

`  object ( Query  ` )

The query to run.

`  gqlQuery  `

`  object ( GqlQuery  ` )

The GQL query to run. This query must be a non-aggregation query.

### Response body

The response for `  Datastore.RunQuery  ` .

If successful, the response body contains data with the following structure:

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;batch&quot;: {
    object (QueryResultBatch)
  },
  &quot;query&quot;: {
    object (Query)
  },
  &quot;transaction&quot;: string,
  &quot;explainMetrics&quot;: {
    object (ExplainMetrics)
  }
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  batch  `

`  object ( QueryResultBatch  ` )

A batch of query results. This is always present unless running a query under explain-only mode: `  RunQueryRequest.explain_options  ` was provided and `  ExplainOptions.analyze  ` was set to false.

`  query  `

`  object ( Query  ` )

The parsed form of the `  GqlQuery  ` from the request, if it was set.

`  transaction  `

`  string ( bytes format)  `

The identifier of the transaction that was started as part of this projects.runQuery request.

Set only when `  ReadOptions.new_transaction  ` was set in `  RunQueryRequest.read_options  ` .

A base64-encoded string.

`  explainMetrics  `

`  object ( ExplainMetrics  ` )

Query explain metrics. This is only present when the `  RunQueryRequest.explain_options  ` is provided, and it is sent only once with the last response in the stream.

### Authorization scopes

Requires one of the following OAuth scopes:

  - `  https://www.googleapis.com/auth/datastore  `
  - `  https://www.googleapis.com/auth/cloud-platform  `

For more information, see the [Authentication Overview](/docs/authentication#authorization-gcp) .

## QueryResultBatch

A batch of results produced by a query.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;skippedResults&quot;: integer,
  &quot;skippedCursor&quot;: string,
  &quot;entityResultType&quot;: enum (ResultType),
  &quot;entityResults&quot;: [
    {
      object (EntityResult)
    }
  ],
  &quot;endCursor&quot;: string,
  &quot;moreResults&quot;: enum (MoreResultsType),
  &quot;snapshotVersion&quot;: string,
  &quot;readTime&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  skippedResults  `

`  integer  `

The number of results skipped, typically because of an offset.

`  skippedCursor  `

`  string ( bytes format)  `

A cursor that points to the position after the last skipped result. Will be set when `  skippedResults  ` \!= 0.

A base64-encoded string.

`  entityResultType  `

`  enum ( ResultType  ` )

The result type for every entity in `  entityResults  ` .

`  entityResults[]  `

`  object ( EntityResult  ` )

The results for this batch.

`  endCursor  `

`  string ( bytes format)  `

A cursor that points to the position after the last result in the batch.

A base64-encoded string.

`  moreResults  `

`  enum ( MoreResultsType  ` )

The state of the query after the current batch.

`  snapshotVersion  `

`  string ( int64 format)  `

The version number of the snapshot this batch was returned from. This applies to the range of results from the query's `  startCursor  ` (or the beginning of the query if no cursor was given) to this batch's `  endCursor  ` (not the query's `  endCursor  ` ).

In a single transaction, subsequent query result batches for the same query can have a greater snapshot version number. Each batch's snapshot version is valid for all preceding batches. The value will be zero for eventually consistent queries.

`  readTime  `

`  string ( Timestamp  ` format)

Read timestamp this batch was returned from. This applies to the range of results from the query's `  startCursor  ` (or the beginning of the query if no cursor was given) to this batch's `  endCursor  ` (not the query's `  endCursor  ` ).

In a single transaction, subsequent query result batches for the same query can have a greater timestamp. Each batch's read timestamp is valid for all preceding batches. This value will not be set for eventually consistent queries in Cloud Datastore.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `  "2014-10-02T15:01:23Z"  ` , `  "2014-10-02T15:01:23.045123456Z"  ` or `  "2014-10-02T15:01:23+05:30"  ` .

## ResultType

Specifies what data the 'entity' field contains. A `  ResultType  ` is either implied (for example, in `  LookupResponse.missing  ` from `  datastore.proto  ` , it is always `  KEY_ONLY  ` ) or specified by context (for example, in message `  QueryResultBatch  ` , field `  entityResultType  ` specifies a `  ResultType  ` for all the values in field `  entityResults  ` ).

Enums

`  RESULT_TYPE_UNSPECIFIED  `

Unspecified. This value is never used.

`  FULL  `

The key and properties.

`  PROJECTION  `

A projected subset of properties. The entity may have no key.

`  KEY_ONLY  `

Only the key.
