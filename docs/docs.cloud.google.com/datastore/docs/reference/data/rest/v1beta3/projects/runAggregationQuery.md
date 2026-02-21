  - [HTTP request](#body.HTTP_TEMPLATE)
  - [Path parameters](#body.PATH_PARAMETERS)
  - [Request body](#body.request_body)
      - [JSON representation](#body.request_body.SCHEMA_REPRESENTATION)
  - [Response body](#body.response_body)
      - [JSON representation](#body.RunAggregationQueryResponse.SCHEMA_REPRESENTATION)
  - [Authorization scopes](#body.aspect)
  - [AggregationQuery](#AggregationQuery)
      - [JSON representation](#AggregationQuery.SCHEMA_REPRESENTATION)
  - [Aggregation](#Aggregation)
      - [JSON representation](#Aggregation.SCHEMA_REPRESENTATION)
  - [Count](#Count)
      - [JSON representation](#Count.SCHEMA_REPRESENTATION)
  - [Sum](#Sum)
      - [JSON representation](#Sum.SCHEMA_REPRESENTATION)
  - [Avg](#Avg)
      - [JSON representation](#Avg.SCHEMA_REPRESENTATION)
  - [AggregationResultBatch](#AggregationResultBatch)
      - [JSON representation](#AggregationResultBatch.SCHEMA_REPRESENTATION)
  - [AggregationResult](#AggregationResult)
      - [JSON representation](#AggregationResult.SCHEMA_REPRESENTATION)
  - [Try it\!](#try-it)

Runs an aggregation query.

### HTTP request

`  POST https://datastore.googleapis.com/v1beta3/projects/{projectId}:runAggregationQuery  `

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
  &quot;partitionId&quot;: {
    object (PartitionId)
  },
  &quot;readOptions&quot;: {
    object (ReadOptions)
  },
  &quot;explainOptions&quot;: {
    object (ExplainOptions)
  },

  // Union field query_type can be only one of the following:
  &quot;aggregationQuery&quot;: {
    object (AggregationQuery)
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

`  partitionId  `

`  object ( PartitionId  ` )

Entities are partitioned into subsets, identified by a partition ID. Queries are scoped to a single partition. This partition ID is normalized with the standard default context partition ID.

`  readOptions  `

`  object ( ReadOptions  ` )

The options for this query.

`  explainOptions  `

`  object ( ExplainOptions  ` )

Optional. Explain options for the query. If set, additional query statistics will be returned. If not, only query results will be returned.

Union field `  query_type  ` . The type of query. `  query_type  ` can be only one of the following:

`  aggregationQuery  `

`  object ( AggregationQuery  ` )

The query to run.

`  gqlQuery  `

`  object ( GqlQuery  ` )

The GQL query to run. This query must be an aggregation query.

### Response body

The response for `  Datastore.RunAggregationQuery  ` .

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
    object (AggregationResultBatch)
  },
  &quot;query&quot;: {
    object (AggregationQuery)
  },
  &quot;explainMetrics&quot;: {
    object (ExplainMetrics)
  }
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  batch  `

`  object ( AggregationResultBatch  ` )

A batch of aggregation results. Always present.

`  query  `

`  object ( AggregationQuery  ` )

The parsed form of the `  GqlQuery  ` from the request, if it was set.

`  explainMetrics  `

`  object ( ExplainMetrics  ` )

Query explain metrics. This is only present when the `  RunAggregationQueryRequest.explain_options  ` is provided, and it is sent only once with the last response in the stream.

### Authorization scopes

Requires one of the following OAuth scopes:

  - `  https://www.googleapis.com/auth/datastore  `
  - `  https://www.googleapis.com/auth/cloud-platform  `

For more information, see the [Authentication Overview](/docs/authentication#authorization-gcp) .

## AggregationQuery

Datastore query for running an aggregation over a `  Query  ` .

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
  &quot;aggregations&quot;: [
    {
      object (Aggregation)
    }
  ],

  // Union field query_type can be only one of the following:
  &quot;nestedQuery&quot;: {
    object (Query)
  }
  // End of list of possible types for union field query_type.
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  aggregations[]  `

`  object ( Aggregation  ` )

Optional. Series of aggregations to apply over the results of the `  nestedQuery  ` .

Requires:

  - A minimum of one and maximum of five aggregations per query.

Union field `  query_type  ` . The base query to aggregate over. `  query_type  ` can be only one of the following:

`  nestedQuery  `

`  object ( Query  ` )

Nested query for aggregation

## Aggregation

Defines an aggregation that produces a single result.

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
  &quot;alias&quot;: string,

  // Union field operator can be only one of the following:
  &quot;count&quot;: {
    object (Count)
  },
  &quot;sum&quot;: {
    object (Sum)
  },
  &quot;avg&quot;: {
    object (Avg)
  }
  // End of list of possible types for union field operator.
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  alias  `

`  string  `

Optional. Optional name of the property to store the result of the aggregation.

If not provided, Datastore will pick a default name following the format `  property_<incremental_id++>  ` . For example:

``` text
AGGREGATE
  COUNT_UP_TO(1) AS count_up_to_1,
  COUNT_UP_TO(2),
  COUNT_UP_TO(3) AS count_up_to_3,
  COUNT(*)
OVER (
  ...
);
```

becomes:

``` text
AGGREGATE
  COUNT_UP_TO(1) AS count_up_to_1,
  COUNT_UP_TO(2) AS property_1,
  COUNT_UP_TO(3) AS count_up_to_3,
  COUNT(*) AS property_2
OVER (
  ...
);
```

Requires:

  - Must be unique across all aggregation aliases.
  - Conform to `  entity property name  ` limitations.

Union field `  operator  ` . The type of aggregation to perform, required. `  operator  ` can be only one of the following:

`  count  `

`  object ( Count  ` )

Count aggregator.

`  sum  `

`  object ( Sum  ` )

Sum aggregator.

`  avg  `

`  object ( Avg  ` )

Average aggregator.

## Count

Count of entities that match the query.

The `  COUNT(*)  ` aggregation function operates on the entire entity so it does not require a field reference.

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
  &quot;upTo&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  upTo  `

`  string ( Int64Value format)  `

Optional. Optional constraint on the maximum number of entities to count.

This provides a way to set an upper bound on the number of entities to scan, limiting latency, and cost.

Unspecified is interpreted as no bound.

If a zero value is provided, a count result of zero should always be expected.

High-Level Example:

``` text
AGGREGATE COUNT_UP_TO(1000) OVER ( SELECT * FROM k );
```

Requires:

  - Must be non-negative when present.

## Sum

Sum of the values of the requested property.

  - Only numeric values will be aggregated. All non-numeric values including `  NULL  ` are skipped.

  - If the aggregated values contain `  NaN  ` , returns `  NaN  ` . Infinity math follows IEEE-754 standards.

  - If the aggregated value set is empty, returns 0.

  - Returns a 64-bit integer if all aggregated numbers are integers and the sum result does not overflow. Otherwise, the result is returned as a double. Note that even if all the aggregated values are integers, the result is returned as a double if it cannot fit within a 64-bit signed integer. When this occurs, the returned value will lose precision.

  - When underflow occurs, floating-point aggregation is non-deterministic. This means that running the same query repeatedly without any changes to the underlying values could produce slightly different results each time. In those cases, values should be stored as integers over floating-point numbers.

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
  &quot;property&quot;: {
    object (PropertyReference)
  }
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  property  `

`  object ( PropertyReference  ` )

The property to aggregate on.

## Avg

Average of the values of the requested property.

  - Only numeric values will be aggregated. All non-numeric values including `  NULL  ` are skipped.

  - If the aggregated values contain `  NaN  ` , returns `  NaN  ` . Infinity math follows IEEE-754 standards.

  - If the aggregated value set is empty, returns `  NULL  ` .

  - Always returns the result as a double.

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
  &quot;property&quot;: {
    object (PropertyReference)
  }
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  property  `

`  object ( PropertyReference  ` )

The property to aggregate on.

## AggregationResultBatch

A batch of aggregation results produced by an aggregation query.

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
  &quot;aggregationResults&quot;: [
    {
      object (AggregationResult)
    }
  ],
  &quot;moreResults&quot;: enum (MoreResultsType),
  &quot;readTime&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  aggregationResults[]  `

`  object ( AggregationResult  ` )

The aggregation results for this batch.

`  moreResults  `

`  enum ( MoreResultsType  ` )

The state of the query after the current batch. Only COUNT(\*) aggregations are supported in the initial launch. Therefore, expected result type is limited to `  NO_MORE_RESULTS  ` .

`  readTime  `

`  string ( Timestamp  ` format)

Read timestamp this batch was returned from.

In a single transaction, subsequent query result batches for the same query can have a greater timestamp. Each batch's read timestamp is valid for all preceding batches.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `  "2014-10-02T15:01:23Z"  ` , `  "2014-10-02T15:01:23.045123456Z"  ` or `  "2014-10-02T15:01:23+05:30"  ` .

## AggregationResult

The result of a single bucket from a Datastore aggregation query.

The keys of `  aggregateProperties  ` are the same for all results in an aggregation query, unlike entity queries which can have different fields present for each result.

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
  &quot;aggregateProperties&quot;: {
    string: {
      object (Value)
    },
    ...
  }
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  aggregateProperties  `

`  map (key: string, value: object ( Value  ` ))

The result of the aggregation functions, ex: `  COUNT(*) AS total_entities  ` .

The key is the `  alias  ` assigned to the aggregation function on input and the size of this map equals the number of aggregation functions in the query.

An object containing a list of `  "key": value  ` pairs. Example: `  { "name": "wrench", "mass": "1.3kg", "count": "3" }  ` .
