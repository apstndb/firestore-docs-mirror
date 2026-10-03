---
name: documents/docs.cloud.google.com/datastore/docs/reference/data/rest/v1beta3/projects/runAggregationQuery
uri: https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1beta3/projects/runAggregationQuery
title: 'Method: projects.runAggregationQuery'
description: A highly-scalable NoSQL database for your web and mobile applications that automatically handles sharding and replication.
data_source: docs.cloud.google.com
---

- [HTTP request](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1beta3/projects/runAggregationQuery#body.HTTP_TEMPLATE)
- [Path parameters](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1beta3/projects/runAggregationQuery#body.PATH_PARAMETERS)
- [Request body](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1beta3/projects/runAggregationQuery#body.request_body)
  - [JSON representation](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1beta3/projects/runAggregationQuery#body.request_body.SCHEMA_REPRESENTATION)
- [Response body](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1beta3/projects/runAggregationQuery#body.response_body)
  - [JSON representation](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1beta3/projects/runAggregationQuery#body.RunAggregationQueryResponse.SCHEMA_REPRESENTATION)
- [Authorization scopes](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1beta3/projects/runAggregationQuery#body.aspect)
- [AggregationQuery](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1beta3/projects/runAggregationQuery#AggregationQuery)
  - [JSON representation](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1beta3/projects/runAggregationQuery#AggregationQuery.SCHEMA_REPRESENTATION)
- [Aggregation](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1beta3/projects/runAggregationQuery#Aggregation)
  - [JSON representation](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1beta3/projects/runAggregationQuery#Aggregation.SCHEMA_REPRESENTATION)
- [Count](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1beta3/projects/runAggregationQuery#Count)
  - [JSON representation](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1beta3/projects/runAggregationQuery#Count.SCHEMA_REPRESENTATION)
- [Sum](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1beta3/projects/runAggregationQuery#Sum)
  - [JSON representation](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1beta3/projects/runAggregationQuery#Sum.SCHEMA_REPRESENTATION)
- [Avg](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1beta3/projects/runAggregationQuery#Avg)
  - [JSON representation](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1beta3/projects/runAggregationQuery#Avg.SCHEMA_REPRESENTATION)
- [AggregationResultBatch](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1beta3/projects/runAggregationQuery#AggregationResultBatch)
  - [JSON representation](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1beta3/projects/runAggregationQuery#AggregationResultBatch.SCHEMA_REPRESENTATION)
- [AggregationResult](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1beta3/projects/runAggregationQuery#AggregationResult)
  - [JSON representation](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1beta3/projects/runAggregationQuery#AggregationResult.SCHEMA_REPRESENTATION)
- [Try it!](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1beta3/projects/runAggregationQuery#try-it)

Runs an aggregation query.

### HTTP request

Choose a location:

  
`POST https://datastore.googleapis.com/v1beta3/projects/{projectId}:runAggregationQuery`

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
  "partitionId": {
    object (PartitionId)
  },
  "readOptions": {
    object (ReadOptions)
  },
  "explainOptions": {
    object (ExplainOptions)
  },

  // Union field query_type can be only one of the following:
  "aggregationQuery": {
    object (AggregationQuery)
  },
  "gqlQuery": {
    object (GqlQuery)
  }
  // End of list of possible types for union field query_type.
}
```

| Fields                                                                                       |                                                                                                                                                                                                                                                                        |
|----------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `partitionId`                                                                                | `object ( ``PartitionId`` )` Entities are partitioned into subsets, identified by a partition ID. Queries are scoped to a single partition. This partition ID is normalized with the standard default context partition ID.                                            |
| `readOptions`                                                                                | `object ( `[`ReadOptions`](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1beta3/ReadOptions)` )` The options for this query.                                                                                                                       |
| `explainOptions`                                                                             | `object ( `[`ExplainOptions`](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1beta3/ExplainOptions)` )` Optional. Explain options for the query. If set, additional query statistics will be returned. If not, only query results will be returned. |
| Union field `query_type` . The type of query. `query_type` can be only one of the following: |                                                                                                                                                                                                                                                                        |
| `aggregationQuery`                                                                           | `object ( `[`AggregationQuery`](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1beta3/projects/runAggregationQuery#AggregationQuery)` )` The query to run.                                                                                          |
| `gqlQuery`                                                                                   | `object ( `[`GqlQuery`](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1beta3/GqlQuery)` )` The GQL query to run. This query must be an aggregation query.                                                                                          |

### Response body

The response for [`Datastore.RunAggregationQuery`](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1beta3/projects/runAggregationQuery#google.datastore.v1beta3.Datastore.RunAggregationQuery) .

If successful, the response body contains data with the following structure:

**JSON representation**

```
{
  "batch": {
    object (AggregationResultBatch)
  },
  "query": {
    object (AggregationQuery)
  },
  "explainMetrics": {
    object (ExplainMetrics)
  }
}
```

| Fields           |                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
|------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `batch`          | `object ( `[`AggregationResultBatch`](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1beta3/projects/runAggregationQuery#AggregationResultBatch)` )` A batch of aggregation results. Always present.                                                                                                                                                                                                                                    |
| `query`          | `object ( `[`AggregationQuery`](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1beta3/projects/runAggregationQuery#AggregationQuery)` )` The parsed form of the `GqlQuery` from the request, if it was set.                                                                                                                                                                                                                             |
| `explainMetrics` | `object ( `[`ExplainMetrics`](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1beta3/ExplainMetrics)` )` Query explain metrics. This is only present when the [`RunAggregationQueryRequest.explain_options`](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1beta3/projects/runAggregationQuery#body.request_body.FIELDS.explain_options) is provided, and it is sent only once with the last response in the stream. |

### Authorization scopes

Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/datastore`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

## AggregationQuery

Datastore query for running an aggregation over a [`Query`](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1beta3/Query) .

**JSON representation**

```
{
  "aggregations": [
    {
      object (Aggregation)
    }
  ],

  // Union field query_type can be only one of the following:
  "nestedQuery": {
    object (Query)
  }
  // End of list of possible types for union field query_type.
}
```

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>aggregations[]</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1beta3/projects/runAggregationQuery#Aggregation"><code>Aggregation</code></a><code> )</code></p>
<p>Optional. Series of aggregations to apply over the results of the <code>nestedQuery</code> .</p>
<p>Requires:</p>
<ul>
<li>A minimum of one and maximum of five aggregations per query.</li>
</ul></td>
</tr>
<tr class="even">
<td>Union field <code>query_type</code> . The base query to aggregate over. <code>query_type</code> can be only one of the following:</td>
<td></td>
</tr>
<tr class="odd">
<td><code>nestedQuery</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1beta3/Query"><code>Query</code></a><code> )</code></p>
<p>Nested query for aggregation</p></td>
</tr>
</tbody>
</table>

## Aggregation

Defines an aggregation that produces a single result.

**JSON representation**

```
{
  "alias": string,

  // Union field operator can be only one of the following:
  "count": {
    object (Count)
  },
  "sum": {
    object (Sum)
  },
  "avg": {
    object (Avg)
  }
  // End of list of possible types for union field operator.
}
```

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>alias</code></td>
<td><p><code>string</code></p>
<p>Optional. Optional name of the property to store the result of the aggregation.</p>
<p>If not provided, Datastore will pick a default name following the format <code>property_&lt;incremental_id++&gt;</code> . For example:</p>
<pre data-fenced=""><code>AGGREGATE
  COUNT_UP_TO(1) AS count_up_to_1,
  COUNT_UP_TO(2),
  COUNT_UP_TO(3) AS count_up_to_3,
  COUNT(*)
OVER (
  ...
);</code></pre>
<p>becomes:</p>
<pre data-fenced=""><code>AGGREGATE
  COUNT_UP_TO(1) AS count_up_to_1,
  COUNT_UP_TO(2) AS property_1,
  COUNT_UP_TO(3) AS count_up_to_3,
  COUNT(*) AS property_2
OVER (
  ...
);</code></pre>
<p>Requires:</p>
<ul>
<li>Must be unique across all aggregation aliases.</li>
<li>Conform to <code>entity property name</code> limitations.</li>
</ul></td>
</tr>
<tr class="even">
<td>Union field <code>operator</code> . The type of aggregation to perform, required. <code>operator</code> can be only one of the following:</td>
<td></td>
</tr>
<tr class="odd">
<td><code>count</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1beta3/projects/runAggregationQuery#Count"><code>Count</code></a><code> )</code></p>
<p>Count aggregator.</p></td>
</tr>
<tr class="even">
<td><code>sum</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1beta3/projects/runAggregationQuery#Sum"><code>Sum</code></a><code> )</code></p>
<p>Sum aggregator.</p></td>
</tr>
<tr class="odd">
<td><code>avg</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1beta3/projects/runAggregationQuery#Avg"><code>Avg</code></a><code> )</code></p>
<p>Average aggregator.</p></td>
</tr>
</tbody>
</table>

## Count

Count of entities that match the query.

The `COUNT(*)` aggregation function operates on the entire entity so it does not require a field reference.

**JSON representation**

```
{
  "upTo": string
}
```

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>upTo</code></td>
<td><p><code>string ( </code><a href="https://developers.google.com/discovery/v1/type-format"><code>Int64Value</code></a><code> format)</code></p>
<p>Optional. Optional constraint on the maximum number of entities to count.</p>
<p>This provides a way to set an upper bound on the number of entities to scan, limiting latency, and cost.</p>
<p>Unspecified is interpreted as no bound.</p>
<p>If a zero value is provided, a count result of zero should always be expected.</p>
<p>High-Level Example:</p>
<pre data-fenced=""><code>AGGREGATE COUNT_UP_TO(1000) OVER ( SELECT * FROM k );</code></pre>
<p>Requires:</p>
<ul>
<li>Must be non-negative when present.</li>
</ul></td>
</tr>
</tbody>
</table>

## Sum

Sum of the values of the requested property.

- Only numeric values will be aggregated. All non-numeric values including `NULL` are skipped.

- If the aggregated values contain `NaN` , returns `NaN` . Infinity math follows IEEE-754 standards.

- If the aggregated value set is empty, returns 0.

- Returns a 64-bit integer if all aggregated numbers are integers and the sum result does not overflow. Otherwise, the result is returned as a double. Note that even if all the aggregated values are integers, the result is returned as a double if it cannot fit within a 64-bit signed integer. When this occurs, the returned value will lose precision.

- When underflow occurs, floating-point aggregation is non-deterministic. This means that running the same query repeatedly without any changes to the underlying values could produce slightly different results each time. In those cases, values should be stored as integers over floating-point numbers.

**JSON representation**

```
{
  "property": {
    object (PropertyReference)
  }
}
```

| Fields     |                                                                                                                                                                |
|------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `property` | `object ( `[`PropertyReference`](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1beta3/PropertyReference)` )` The property to aggregate on. |

## Avg

Average of the values of the requested property.

- Only numeric values will be aggregated. All non-numeric values including `NULL` are skipped.

- If the aggregated values contain `NaN` , returns `NaN` . Infinity math follows IEEE-754 standards.

- If the aggregated value set is empty, returns `NULL` .

- Always returns the result as a double.

**JSON representation**

```
{
  "property": {
    object (PropertyReference)
  }
}
```

| Fields     |                                                                                                                                                                |
|------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `property` | `object ( `[`PropertyReference`](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1beta3/PropertyReference)` )` The property to aggregate on. |

## AggregationResultBatch

A batch of aggregation results produced by an aggregation query.

**JSON representation**

```
{
  "aggregationResults": [
    {
      object (AggregationResult)
    }
  ],
  "moreResults": enum (MoreResultsType),
  "readTime": string
}
```

| Fields                 |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
|------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `aggregationResults[]` | `object ( `[`AggregationResult`](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1beta3/projects/runAggregationQuery#AggregationResult)` )` The aggregation results for this batch.                                                                                                                                                                                                                                                                                                                                                                                        |
| `moreResults`          | `enum ( `[`MoreResultsType`](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1beta3/MoreResultsType)` )` The state of the query after the current batch. Only COUNT(\*) aggregations are supported in the initial launch. Therefore, expected result type is limited to `NO_MORE_RESULTS` .                                                                                                                                                                                                                                                                                |
| `readTime`             | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Read timestamp this batch was returned from. In a single transaction, subsequent query result batches for the same query can have a greater timestamp. Each batch's read timestamp is valid for all preceding batches. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` . |

## AggregationResult

The result of a single bucket from a Datastore aggregation query.

The keys of `aggregateProperties` are the same for all results in an aggregation query, unlike entity queries which can have different fields present for each result.

**JSON representation**

```
{
  "aggregateProperties": {
    string: {
      object (Value)
    },
    ...
  }
}
```

| Fields                |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
|-----------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `aggregateProperties` | `map (key: string, value: object ( ``Value`` ))` The result of the aggregation functions, ex: `COUNT(*) AS total_entities` . The key is the [`alias`](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1beta3/projects/runAggregationQuery#Aggregation.FIELDS.alias) assigned to the aggregation function on input and the size of this map equals the number of aggregation functions in the query. An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` . |
