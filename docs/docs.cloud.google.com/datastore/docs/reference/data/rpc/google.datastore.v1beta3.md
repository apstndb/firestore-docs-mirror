---
name: documents/docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3
uri: https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3
title: Package google.datastore.v1beta3
description: A highly-scalable NoSQL database for your web and mobile applications that automatically handles sharding and replication.
data_source: docs.cloud.google.com
---

## Index

- [`Datastore`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.Datastore) (interface)
- [`AggregationQuery`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.AggregationQuery) (message)
- [`AggregationQuery.Aggregation`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.AggregationQuery.Aggregation) (message)
- [`AggregationQuery.Aggregation.Avg`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.AggregationQuery.Aggregation.Avg) (message)
- [`AggregationQuery.Aggregation.Count`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.AggregationQuery.Aggregation.Count) (message)
- [`AggregationQuery.Aggregation.Sum`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.AggregationQuery.Aggregation.Sum) (message)
- [`AggregationResult`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.AggregationResult) (message)
- [`AggregationResultBatch`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.AggregationResultBatch) (message)
- [`AllocateIdsRequest`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.AllocateIdsRequest) (message)
- [`AllocateIdsResponse`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.AllocateIdsResponse) (message)
- [`ArrayValue`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.ArrayValue) (message)
- [`BeginTransactionRequest`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.BeginTransactionRequest) (message)
- [`BeginTransactionResponse`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.BeginTransactionResponse) (message)
- [`CommitRequest`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.CommitRequest) (message)
- [`CommitRequest.Mode`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.CommitRequest.Mode) (enum)
- [`CommitResponse`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.CommitResponse) (message)
- [`CompositeFilter`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.CompositeFilter) (message)
- [`CompositeFilter.Operator`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.CompositeFilter.Operator) (enum)
- [`Entity`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.Entity) (message)
- [`EntityResult`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.EntityResult) (message)
- [`EntityResult.ResultType`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.EntityResult.ResultType) (enum)
- [`ExecutionStats`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.ExecutionStats) (message)
- [`ExplainMetrics`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.ExplainMetrics) (message)
- [`ExplainOptions`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.ExplainOptions) (message)
- [`Filter`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.Filter) (message)
- [`GqlQuery`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.GqlQuery) (message)
- [`GqlQueryParameter`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.GqlQueryParameter) (message)
- [`Key`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.Key) (message)
- [`Key.PathElement`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.Key.PathElement) (message)
- [`KindExpression`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.KindExpression) (message)
- [`LookupRequest`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.LookupRequest) (message)
- [`LookupResponse`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.LookupResponse) (message)
- [`Mutation`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.Mutation) (message)
- [`Mutation.ConflictResolutionStrategy`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.Mutation.ConflictResolutionStrategy) (enum)
- [`MutationResult`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.MutationResult) (message)
- [`PartitionId`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.PartitionId) (message)
- [`PlanSummary`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.PlanSummary) (message)
- [`Projection`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.Projection) (message)
- [`PropertyFilter`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.PropertyFilter) (message)
- [`PropertyFilter.Operator`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.PropertyFilter.Operator) (enum)
- [`PropertyMask`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.PropertyMask) (message)
- [`PropertyOrder`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.PropertyOrder) (message)
- [`PropertyOrder.Direction`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.PropertyOrder.Direction) (enum)
- [`PropertyReference`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.PropertyReference) (message)
- [`PropertyTransform`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.PropertyTransform) (message)
- [`PropertyTransform.ServerValue`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.PropertyTransform.ServerValue) (enum)
- [`Query`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.Query) (message)
- [`QueryResultBatch`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.QueryResultBatch) (message)
- [`QueryResultBatch.MoreResultsType`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.QueryResultBatch.MoreResultsType) (enum)
- [`ReadOptions`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.ReadOptions) (message)
- [`ReadOptions.ReadConsistency`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.ReadOptions.ReadConsistency) (enum)
- [`ReserveIdsRequest`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.ReserveIdsRequest) (message)
- [`ReserveIdsResponse`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.ReserveIdsResponse) (message)
- [`RollbackRequest`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.RollbackRequest) (message)
- [`RollbackResponse`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.RollbackResponse) (message)
- [`RunAggregationQueryRequest`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.RunAggregationQueryRequest) (message)
- [`RunAggregationQueryResponse`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.RunAggregationQueryResponse) (message)
- [`RunQueryRequest`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.RunQueryRequest) (message)
- [`RunQueryResponse`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.RunQueryResponse) (message)
- [`TransactionOptions`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.TransactionOptions) (message)
- [`TransactionOptions.ReadOnly`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.TransactionOptions.ReadOnly) (message)
- [`TransactionOptions.ReadWrite`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.TransactionOptions.ReadWrite) (message)
- [`Value`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.Value) (message)

## Datastore

Each RPC normalizes the partition IDs of the keys in its input entities, and always returns entities with keys with normalized partition IDs. This applies to all keys and entities, including those in values, except keys with both an empty path and an empty or unset partition ID. Normalization of input keys sets the project ID (if not already set) to the project ID from the request.

**AllocateIds**

`rpc AllocateIds( `[`AllocateIdsRequest`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.AllocateIdsRequest)` ) returns ( `[`AllocateIdsResponse`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.AllocateIdsResponse)` )`

Allocates IDs for the given keys, which is useful for referencing an entity before it is inserted.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/datastore`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**BeginTransaction**

`rpc BeginTransaction( `[`BeginTransactionRequest`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.BeginTransactionRequest)` ) returns ( `[`BeginTransactionResponse`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.BeginTransactionResponse)` )`

Begins a new transaction.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/datastore`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**Commit**

`rpc Commit( `[`CommitRequest`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.CommitRequest)` ) returns ( `[`CommitResponse`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.CommitResponse)` )`

Commits a transaction, optionally creating, deleting or modifying some entities.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/datastore`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**Lookup**

`rpc Lookup( `[`LookupRequest`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.LookupRequest)` ) returns ( `[`LookupResponse`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.LookupResponse)` )`

Looks up entities by key.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/datastore`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**ReserveIds**

`rpc ReserveIds( `[`ReserveIdsRequest`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.ReserveIdsRequest)` ) returns ( `[`ReserveIdsResponse`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.ReserveIdsResponse)` )`

Prevents the supplied keys' IDs from being auto-allocated by Cloud Datastore.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/datastore`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**Rollback**

`rpc Rollback( `[`RollbackRequest`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.RollbackRequest)` ) returns ( `[`RollbackResponse`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.RollbackResponse)` )`

Rolls back a transaction.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/datastore`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**RunAggregationQuery**

`rpc RunAggregationQuery( `[`RunAggregationQueryRequest`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.RunAggregationQueryRequest)` ) returns ( `[`RunAggregationQueryResponse`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.RunAggregationQueryResponse)` )`

Runs an aggregation query.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/datastore`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**RunQuery**

`rpc RunQuery( `[`RunQueryRequest`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.RunQueryRequest)` ) returns ( `[`RunQueryResponse`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.RunQueryResponse)` )`

Queries for entities.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/datastore`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

## AggregationQuery

Datastore query for running an aggregation over a [`Query`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.Query) .

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
<td><p><a href="https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.AggregationQuery.Aggregation"><code>Aggregation</code></a></p>
<p>Optional. Series of aggregations to apply over the results of the <code>nested_query</code> .</p>
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
<td><code>nested_query</code></td>
<td><p><a href="https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.Query"><code>Query</code></a></p>
<p>Nested query for aggregation</p></td>
</tr>
</tbody>
</table>

## Aggregation

Defines an aggregation that produces a single result.

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
<li>Conform to <a href="https://docs.cloud.google.com/static/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.Entity.FIELDS.repeated.google.datastore.v1beta3.Entity.PropertiesEntry.google.datastore.v1beta3.Entity.properties"><code>entity property name</code></a> limitations.</li>
</ul></td>
</tr>
<tr class="even">
<td>Union field <code>operator</code> . The type of aggregation to perform, required. <code>operator</code> can be only one of the following:</td>
<td></td>
</tr>
<tr class="odd">
<td><code>count</code></td>
<td><p><a href="https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.AggregationQuery.Aggregation.Count"><code>Count</code></a></p>
<p>Count aggregator.</p></td>
</tr>
<tr class="even">
<td><code>sum</code></td>
<td><p><a href="https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.AggregationQuery.Aggregation.Sum"><code>Sum</code></a></p>
<p>Sum aggregator.</p></td>
</tr>
<tr class="odd">
<td><code>avg</code></td>
<td><p><a href="https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.AggregationQuery.Aggregation.Avg"><code>Avg</code></a></p>
<p>Average aggregator.</p></td>
</tr>
</tbody>
</table>

## Avg

Average of the values of the requested property.

- Only numeric values will be aggregated. All non-numeric values including `NULL` are skipped.

- If the aggregated values contain `NaN` , returns `NaN` . Infinity math follows IEEE-754 standards.

- If the aggregated value set is empty, returns `NULL` .

- Always returns the result as a double.

| Fields     |                                                                                                                                                                                          |
|------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `property` | [`PropertyReference`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.PropertyReference) The property to aggregate on. |

## Count

Count of entities that match the query.

The `COUNT(*)` aggregation function operates on the entire entity so it does not require a field reference.

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
<td><code>up_to</code></td>
<td><p><a href="https://protobuf.dev/reference/protobuf/google.protobuf/#int64-value"><code>Int64Value</code></a></p>
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

| Fields     |                                                                                                                                                                                          |
|------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `property` | [`PropertyReference`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.PropertyReference) The property to aggregate on. |

## AggregationResult

The result of a single bucket from a Datastore aggregation query.

The keys of `aggregate_properties` are the same for all results in an aggregation query, unlike entity queries which can have different fields present for each result.

| Fields                 |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
|------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `aggregate_properties` | `map<string, `[`Value`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.Value)` >` The result of the aggregation functions, ex: `COUNT(*) AS total_entities` . The key is the [`alias`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.AggregationQuery.Aggregation.FIELDS.string.google.datastore.v1beta3.AggregationQuery.Aggregation.alias) assigned to the aggregation function on input and the size of this map equals the number of aggregation functions in the query. |

## AggregationResultBatch

A batch of aggregation results produced by an aggregation query.

| Fields                  |                                                                                                                                                                                                                                                                                                                                                            |
|-------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `aggregation_results[]` | [`AggregationResult`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.AggregationResult) The aggregation results for this batch.                                                                                                                                                         |
| `more_results`          | [`MoreResultsType`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.QueryResultBatch.MoreResultsType) The state of the query after the current batch. Only COUNT(\*) aggregations are supported in the initial launch. Therefore, expected result type is limited to `NO_MORE_RESULTS` . |
| `read_time`             | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) Read timestamp this batch was returned from. In a single transaction, subsequent query result batches for the same query can have a greater timestamp. Each batch's read timestamp is valid for all preceding batches.                                                   |

## AllocateIdsRequest

The request for [`Datastore.AllocateIds`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.Datastore.AllocateIds) .

| Fields       |                                                                                                                                                                                                                                                |
|--------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `project_id` | `string` Required. The ID of the project against which to make the request.                                                                                                                                                                    |
| `keys[]`     | [`Key`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.Key) Required. A list of keys with incomplete key paths for which to allocate IDs. No key may be reserved/read-only. |

## AllocateIdsResponse

The response for [`Datastore.AllocateIds`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.Datastore.AllocateIds) .

| Fields   |                                                                                                                                                                                                                                                   |
|----------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `keys[]` | [`Key`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.Key) The keys specified in the request (in the same order), each with its key path completed with a newly allocated ID. |

## ArrayValue

An array value.

| Fields     |                                                                                                                                                                                                                                                                                |
|------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `values[]` | [`Value`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.Value) Values in the array. The order of values in an array is preserved as long as all values have identical settings for 'exclude_from_indexes'. |

## BeginTransactionRequest

The request for [`Datastore.BeginTransaction`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.Datastore.BeginTransaction) .

| Fields                |                                                                                                                                                                                             |
|-----------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `project_id`          | `string` Required. The ID of the project against which to make the request.                                                                                                                 |
| `transaction_options` | [`TransactionOptions`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.TransactionOptions) Options for a new transaction. |

## BeginTransactionResponse

The response for [`Datastore.BeginTransaction`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.Datastore.BeginTransaction) .

| Fields        |                                                      |
|---------------|------------------------------------------------------|
| `transaction` | `bytes` The transaction identifier (always present). |

## CommitRequest

The request for [`Datastore.Commit`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.Datastore.Commit) .

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
<td><code>project_id</code></td>
<td><p><code>string</code></p>
<p>Required. The ID of the project against which to make the request.</p></td>
</tr>
<tr class="even">
<td><code>mode</code></td>
<td><p><a href="https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.CommitRequest.Mode"><code>Mode</code></a></p>
<p>The type of commit to perform. Defaults to <code>TRANSACTIONAL</code> .</p></td>
</tr>
<tr class="odd">
<td><code>mutations[]</code></td>
<td><p><a href="https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.Mutation"><code>Mutation</code></a></p>
<p>The mutations to perform.</p>
<p>When mode is <code>TRANSACTIONAL</code> , mutations affecting a single entity are applied in order. The following sequences of mutations affecting a single entity are not permitted in a single <code>Commit</code> request:</p>
<ul>
<li><code>insert</code> followed by <code>insert</code></li>
<li><code>update</code> followed by <code>insert</code></li>
<li><code>upsert</code> followed by <code>insert</code></li>
<li><code>delete</code> followed by <code>update</code></li>
</ul>
<p>When mode is <code>NON_TRANSACTIONAL</code> , no two mutations may affect a single entity.</p></td>
</tr>
<tr class="even">
<td>Union field <code>transaction_selector</code> . Must be set when mode is <code>TRANSACTIONAL</code> . <code>transaction_selector</code> can be only one of the following:</td>
<td></td>
</tr>
<tr class="odd">
<td><code>transaction</code></td>
<td><p><code>bytes</code></p>
<p>The identifier of the transaction associated with the commit. A transaction identifier is returned by a call to <a href="https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.Datastore.BeginTransaction"><code>Datastore.BeginTransaction</code></a> .</p></td>
</tr>
</tbody>
</table>

## Mode

The modes available for commits.

| Enums               |                                                                                                                                                                            |
|---------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `MODE_UNSPECIFIED`  | Unspecified. This value must not be used.                                                                                                                                  |
| `TRANSACTIONAL`     | Transactional: The mutations are either all applied, or none are applied. Learn about transactions [here](https://cloud.google.com/datastore/docs/concepts/transactions) . |
| `NON_TRANSACTIONAL` | Non-transactional: The mutations may not apply as all or none.                                                                                                             |

## CommitResponse

The response for [`Datastore.Commit`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.Datastore.Commit) .

| Fields               |                                                                                                                                                                                                                                                                        |
|----------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `mutation_results[]` | [`MutationResult`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.MutationResult) The result of performing the mutations. The i-th mutation result corresponds to the i-th mutation in the request. |
| `index_updates`      | `int32` The number of index entries updated during the commit, or zero if none were updated.                                                                                                                                                                           |
| `commit_time`        | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) The transaction commit timestamp. Not set for non-transactional commits.                                                                                                             |

## CompositeFilter

A filter that merges multiple other filters using the given operator.

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
<td><code>op</code></td>
<td><p><a href="https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.CompositeFilter.Operator"><code>Operator</code></a></p>
<p>The operator for combining multiple filters.</p></td>
</tr>
<tr class="even">
<td><code>filters[]</code></td>
<td><p><a href="https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.Filter"><code>Filter</code></a></p>
<p>The list of filters to combine.</p>
<p>Requires:</p>
<ul>
<li>At least one filter is present.</li>
</ul></td>
</tr>
</tbody>
</table>

## Operator

A composite filter operator.

| Enums                  |                                                                         |
|------------------------|-------------------------------------------------------------------------|
| `OPERATOR_UNSPECIFIED` | Unspecified. This value must not be used.                               |
| `AND`                  | The results are required to satisfy each of the combined filters.       |
| `OR`                   | Documents are required to satisfy at least one of the combined filters. |

## Entity

A Datastore data object.

Must not exceed 1 MiB - 4 bytes.

| Fields       |                                                                                                                                                                                                                                                                                                                                                                                                                                  |
|--------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `key`        | [`Key`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.Key) The entity's key. An entity must have a key, unless otherwise documented (for example, an entity in `Value.entity_value` may have no key). An entity's kind is its key path's last element's kind, or null if it has no key.                                                                      |
| `properties` | `map<string, `[`Value`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.Value)` >` The entity's properties. The map's keys are property names. A property name matching regex `__.*__` is reserved. A reserved property name is forbidden in certain documented contexts. The map keys, represented as UTF-8, must not exceed 1,500 bytes and cannot be empty. |

## EntityResult

The result of fetching an entity from Datastore.

| Fields        |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
|---------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `entity`      | [`Entity`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.Entity) The resulting entity.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| `version`     | `int64` The version of the entity, a strictly positive number that monotonically increases with changes to the entity. This field is set for [`FULL`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.EntityResult.ResultType.ENUM_VALUES.google.datastore.v1beta3.EntityResult.ResultType.FULL) entity results. For [`missing`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.LookupResponse.FIELDS.repeated.google.datastore.v1beta3.EntityResult.google.datastore.v1beta3.LookupResponse.missing) entities in `LookupResponse` , this is the version of the snapshot that was used to look up the entity, and it is always set except for eventually consistent reads. |
| `create_time` | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) The time at which the entity was created. This field is set for [`FULL`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.EntityResult.ResultType.ENUM_VALUES.google.datastore.v1beta3.EntityResult.ResultType.FULL) entity results. If this entity is missing, this field will not be set.                                                                                                                                                                                                                                                                                                                                                                  |
| `update_time` | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) The time at which the entity was last changed. This field is set for [`FULL`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.EntityResult.ResultType.ENUM_VALUES.google.datastore.v1beta3.EntityResult.ResultType.FULL) entity results. If this entity is missing, this field will not be set.                                                                                                                                                                                                                                                                                                                                                             |
| `cursor`      | `bytes` A cursor that points to the position after the result entity. Set only when the `EntityResult` is part of a `QueryResultBatch` message.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |

## ResultType

Specifies what data the 'entity' field contains. A `ResultType` is either implied (for example, in `LookupResponse.missing` from `datastore.proto` , it is always `KEY_ONLY` ) or specified by context (for example, in message `QueryResultBatch` , field `entity_result_type` specifies a `ResultType` for all the values in field `entity_results` ).

| Enums                     |                                                               |
|---------------------------|---------------------------------------------------------------|
| `RESULT_TYPE_UNSPECIFIED` | Unspecified. This value is never used.                        |
| `FULL`                    | The key and properties.                                       |
| `PROJECTION`              | A projected subset of properties. The entity may have no key. |
| `KEY_ONLY`                | Only the key.                                                 |

## ExecutionStats

Execution statistics for the query.

| Fields               |                                                                                                                                                                                                                                                                                                                                                                                                             |
|----------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `results_returned`   | `int64` Total number of results returned, including documents, projections, aggregation results, keys.                                                                                                                                                                                                                                                                                                      |
| `execution_duration` | [`Duration`](https://protobuf.dev/reference/protobuf/google.protobuf/#duration) Total time to execute the query in the backend.                                                                                                                                                                                                                                                                             |
| `read_operations`    | `int64` Total billable read operations.                                                                                                                                                                                                                                                                                                                                                                     |
| `debug_stats`        | [`Struct`](https://protobuf.dev/reference/protobuf/google.protobuf/#struct) Debugging statistics from the execution of the query. Note that the debugging stats are subject to change as Firestore evolves. It could include: { "indexes_entries_scanned": "1000", "documents_scanned": "20", "billing_details" : { "documents_billable": "20", "index_entries_billable": "1000", "min_query_cost": "0" } } |

## ExplainMetrics

Explain metrics for the query.

| Fields            |                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
|-------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `plan_summary`    | [`PlanSummary`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.PlanSummary) Planning phase information for the query.                                                                                                                                                                                                                                                                          |
| `execution_stats` | [`ExecutionStats`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.ExecutionStats) Aggregated stats from the execution of the query. Only present when [`ExplainOptions.analyze`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.ExplainOptions.FIELDS.bool.google.datastore.v1beta3.ExplainOptions.analyze) is set to true. |

## ExplainOptions

Explain options for the query.

| Fields    |                                                                                                                                                                                                                                                                                                 |
|-----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `analyze` | `bool` Optional. Whether to execute this query. When false (the default), the query will be planned, returning only metrics from the planning stages. When true, the query will be planned and executed, returning the full query results along with both planning and execution stage metrics. |

## Filter

A holder for any type of filter.

| Fields                                                                                          |                                                                                                                                                                              |
|-------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `filter_type` . The type of filter. `filter_type` can be only one of the following: |                                                                                                                                                                              |
| `composite_filter`                                                                              | [`CompositeFilter`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.CompositeFilter) A composite filter.   |
| `property_filter`                                                                               | [`PropertyFilter`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.PropertyFilter) A filter on a property. |

## GqlQuery

A [GQL query](https://cloud.google.com/datastore/docs/apis/gql/gql_reference) .

| Fields                  |                                                                                                                                                                                                                                                                                                                                                                                                                                      |
|-------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `query_string`          | `string` A string of the format described [here](https://cloud.google.com/datastore/docs/apis/gql/gql_reference) .                                                                                                                                                                                                                                                                                                                   |
| `allow_literals`        | `bool` When false, the query string must not contain any literals and instead must bind all values. For example, `SELECT * FROM Kind WHERE a = 'string literal'` is not allowed, while `SELECT * FROM Kind WHERE a = @value` is.                                                                                                                                                                                                     |
| `named_bindings`        | `map<string, `[`GqlQueryParameter`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.GqlQueryParameter)` >` For each non-reserved named binding site in the query string, there must be a named parameter with that name, but not necessarily the inverse. Key must match regex `[A-Za-z_$][A-Za-z_$0-9]*` , must not match regex `__.*__` , and must not be `""` . |
| `positional_bindings[]` | [`GqlQueryParameter`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.GqlQueryParameter) Numbered binding site @1 references the first numbered parameter, effectively using 1-based indexing, rather than the usual 0. For each binding site numbered i in `query_string` , there must be an i-th numbered parameter. The inverse must also be true.              |

## GqlQueryParameter

A binding parameter for a GQL query.

| Fields                                                                                                   |                                                                                                                                                       |
|----------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `parameter_type` . The type of parameter. `parameter_type` can be only one of the following: |                                                                                                                                                       |
| `value`                                                                                                  | [`Value`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.Value) A value parameter. |
| `cursor`                                                                                                 | `bytes` A query cursor. Query cursors are returned in query result batches.                                                                           |

## Key

A unique identifier for an entity. If a key's partition ID or any of its path kinds or names are reserved/read-only, the key is reserved/read-only. A reserved/read-only key is forbidden in certain documented contexts.

| Fields         |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
|----------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `partition_id` | [`PartitionId`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.PartitionId) Entities are partitioned into subsets, currently identified by a project ID and namespace ID. Queries are scoped to a single partition.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| `path[]`       | [`PathElement`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.Key.PathElement) The entity path. An entity path consists of one or more elements composed of a kind and a string or numerical identifier, which identify entities. The first element identifies a *root entity* , the second element identifies a *child* of the root entity, the third element identifies a child of the second entity, and so forth. The entities identified by all prefixes of the path are called the element's *ancestors* . An entity path is always fully complete: *all* of the entity's ancestors are required to be in the path along with the entity identifier itself. The only exception is that in some documented cases, the identifier in the last path element (for the entity) itself may be omitted. For example, the last path element of the key of `Mutation.insert` may have no identifier. A path can never be empty, and a path can have at most 100 elements. |

## PathElement

A (kind, ID/name) pair used to construct a key path.

If either name or ID is set, the element is complete. If neither is set, the element is incomplete.

| Fields                                                                              |                                                                                                                                                                                                                                                                                                                            |
|-------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `kind`                                                                              | `string` The kind of the entity. A kind matching regex `__.*__` is reserved/read-only. A kind must not contain more than 1500 bytes when UTF-8 encoded. Cannot be `""` . Must be valid UTF-8 bytes. Legacy values that are not valid UTF-8 are encoded as `__bytes<X>__` where `<X>` is the base-64 encoding of the bytes. |
| Union field `id_type` . The type of ID. `id_type` can be only one of the following: |                                                                                                                                                                                                                                                                                                                            |
| `id`                                                                                | `int64` The auto-allocated ID of the entity. Never equal to zero. Values less than zero are discouraged and may not be supported in the future.                                                                                                                                                                            |
| `name`                                                                              | `string` The name of the entity. A name matching regex `__.*__` is reserved/read-only. A name must not be more than 1500 bytes when UTF-8 encoded. Cannot be `""` . Must be valid UTF-8 bytes. Legacy values that are not valid UTF-8 are encoded as `__bytes<X>__` where `<X>` is the base-64 encoding of the bytes.      |

## KindExpression

A representation of a kind.

| Fields |                                |
|--------|--------------------------------|
| `name` | `string` The name of the kind. |

## LookupRequest

The request for [`Datastore.Lookup`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.Datastore.Lookup) .

| Fields          |                                                                                                                                                                                                                                                                                                                                                                                                            |
|-----------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `project_id`    | `string` Required. The ID of the project against which to make the request.                                                                                                                                                                                                                                                                                                                                |
| `read_options`  | [`ReadOptions`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.ReadOptions) The options for this lookup request.                                                                                                                                                                                                                        |
| `keys[]`        | [`Key`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.Key) Required. Keys of entities to look up.                                                                                                                                                                                                                                      |
| `property_mask` | [`PropertyMask`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.PropertyMask) The properties to return. Defaults to returning all properties. If this field is set and an entity has a property not referenced in the mask, it will be absent from \[LookupResponse.found.entity.properties\]\[\]. The entity's key is always returned. |

## LookupResponse

The response for [`Datastore.Lookup`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.Datastore.Lookup) .

| Fields       |                                                                                                                                                                                                                                                                                                                   |
|--------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `found[]`    | [`EntityResult`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.EntityResult) Entities found as `ResultType.FULL` entities. The order of results in this field is undefined and has no relation to the order of the keys in the input.         |
| `missing[]`  | [`EntityResult`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.EntityResult) Entities not found as `ResultType.KEY_ONLY` entities. The order of results in this field is undefined and has no relation to the order of the keys in the input. |
| `deferred[]` | [`Key`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.Key) A list of keys that were not looked up due to resource constraints. The order of results in this field is undefined and has no relation to the order of the keys in the input.     |
| `read_time`  | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) The time at which these entities were read or found missing.                                                                                                                                                                    |

## Mutation

A mutation to apply to an entity.

| Fields                                                                                                                                                                                                                                                                                                                                                                                       |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `conflict_resolution_strategy`                                                                                                                                                                                                                                                                                                                                                               | [`ConflictResolutionStrategy`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.Mutation.ConflictResolutionStrategy) The strategy to use when a conflict is detected. Defaults to `SERVER_VALUE` . If this is set, then `conflict_detection_strategy` must also be set.                                                                                                                                                              |
| `property_mask`                                                                                                                                                                                                                                                                                                                                                                              | [`PropertyMask`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.PropertyMask) The properties to write in this mutation. None of the properties in the mask may have a reserved name, except for `__key__` . This field is ignored for `delete` . If the entity already exists, only properties referenced in the mask are updated, others are left untouched. Properties referenced in the mask but not in the entity are deleted. |
| `property_transforms[]`                                                                                                                                                                                                                                                                                                                                                                      | [`PropertyTransform`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.PropertyTransform) Optional. The transforms to perform on the entity. This field can be set only when the operation is `insert` , `update` , or `upsert` . If present, the transforms are be applied to the entity regardless of the property mask, in order, after the operation.                                                                            |
| Union field `operation` . The mutation operation. For `insert` , `update` , and `upsert` : - The entity's key must not be reserved/read-only. - No property in the entity may have a reserved name, not even a property in an entity in a value. - No value in the entity may have meaning 18, not even a value in an entity in another value. `operation` can be only one of the following: |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| `insert`                                                                                                                                                                                                                                                                                                                                                                                     | [`Entity`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.Entity) The entity to insert. The entity must not already exist. The entity key's final path element may be incomplete.                                                                                                                                                                                                                                                  |
| `update`                                                                                                                                                                                                                                                                                                                                                                                     | [`Entity`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.Entity) The entity to update. The entity must already exist. Must have a complete key path.                                                                                                                                                                                                                                                                              |
| `upsert`                                                                                                                                                                                                                                                                                                                                                                                     | [`Entity`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.Entity) The entity to upsert. The entity may or may not already exist. The entity key's final path element may be incomplete.                                                                                                                                                                                                                                            |
| `delete`                                                                                                                                                                                                                                                                                                                                                                                     | [`Key`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.Key) The key of the entity to delete. The entity may or may not already exist. Must have a complete key path and must not be reserved/read-only.                                                                                                                                                                                                                            |
| Union field `conflict_detection_strategy` . When set, the server will detect whether or not this mutation conflicts with the current version of the entity on the server. Conflicting mutations are not applied, and are marked as such in MutationResult. `conflict_detection_strategy` can be only one of the following:                                                                   |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| `base_version`                                                                                                                                                                                                                                                                                                                                                                               | `int64` The version of the entity that this mutation is being applied to. If this does not match the current version on the server, the mutation conflicts.                                                                                                                                                                                                                                                                                                                                           |
| `update_time`                                                                                                                                                                                                                                                                                                                                                                                | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) The update time of the entity that this mutation is being applied to. If this does not match the current update time on the server, the mutation conflicts.                                                                                                                                                                                                                                                         |

## ConflictResolutionStrategy

The possible ways to resolve a conflict detected in a mutation.

| Enums                  |                                           |
|------------------------|-------------------------------------------|
| `STRATEGY_UNSPECIFIED` | Unspecified. Defaults to `SERVER_VALUE` . |
| `SERVER_VALUE`         | The server entity is kept.                |
| `FAIL`                 | The whole commit request fails.           |

## MutationResult

The result of applying a mutation.

| Fields                |                                                                                                                                                                                                                                                                                                                                                                   |
|-----------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `key`                 | [`Key`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.Key) The automatically allocated key. Set only when the mutation allocated a key.                                                                                                                                                       |
| `version`             | `int64` The version of the entity on the server after processing the mutation. If the mutation doesn't change anything on the server, then the version will be the version of the current entity or, if no entity is present, a version that is strictly greater than the version of any previous entity and less than the version of any possible future entity. |
| `create_time`         | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) The create time of the entity. This field will not be set after a 'delete'.                                                                                                                                                                                                     |
| `update_time`         | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) The update time of the entity on the server after processing the mutation. If the mutation doesn't change anything on the server, then the timestamp will be the update timestamp of the current entity. This field will not be set after a 'delete'.                           |
| `conflict_detected`   | `bool` Whether a conflict was detected for this mutation. Always false when a conflict detection strategy field is not set in the mutation.                                                                                                                                                                                                                       |
| `transform_results[]` | [`Value`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.Value) The results of applying each [`PropertyTransform`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.PropertyTransform) , in the same order of the request.    |

## PartitionId

A partition ID identifies a grouping of entities. The grouping is always by project and namespace, however the namespace ID may be empty.

A partition ID contains several dimensions: project ID and namespace ID.

Partition dimensions:

- May be `""` .
- Must be valid UTF-8 bytes.
- Must have values that match regex `[A-Za-z\d\.\-_]{1,100}` If the value of any dimension matches regex `__.*__` , the partition is reserved/read-only. A reserved/read-only partition ID is forbidden in certain documented contexts.

Foreign partition IDs (in which the project ID does not match the context project ID ) are discouraged. Reads and writes of foreign partition IDs may fail if the project is not in an active state.

| Fields         |                                                                              |
|----------------|------------------------------------------------------------------------------|
| `project_id`   | `string` The ID of the project to which the entities belong.                 |
| `namespace_id` | `string` If not empty, the ID of the namespace to which the entities belong. |

## PlanSummary

Planning phase information for the query.

| Fields           |                                                                                                                                                                                                                                                                                   |
|------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `indexes_used[]` | [`Struct`](https://protobuf.dev/reference/protobuf/google.protobuf/#struct) The indexes selected for the query. For example: \[ {"query_scope": "Collection", "properties": "(foo ASC, **name** ASC)"}, {"query_scope": "Collection", "properties": "(bar ASC, **name** ASC)"} \] |

## Projection

A representation of a property in a projection.

| Fields     |                                                                                                                                                                                     |
|------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `property` | [`PropertyReference`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.PropertyReference) The property to project. |

## PropertyFilter

A filter on a specific property.

| Fields     |                                                                                                                                                                                       |
|------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `property` | [`PropertyReference`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.PropertyReference) The property to filter by. |
| `op`       | [`Operator`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.PropertyFilter.Operator) The operator to filter by.    |
| `value`    | [`Value`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.Value) The value to compare the property to.              |

## Operator

A property filter operator.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Enums</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>OPERATOR_UNSPECIFIED</code></td>
<td>Unspecified. This value must not be used.</td>
</tr>
<tr class="even">
<td><code>LESS_THAN</code></td>
<td><p>The given <code>property</code> is less than the given <code>value</code> .</p>
<p>Requires:</p>
<ul>
<li>That <code>property</code> comes first in <code>order_by</code> .</li>
</ul></td>
</tr>
<tr class="odd">
<td><code>LESS_THAN_OR_EQUAL</code></td>
<td><p>The given <code>property</code> is less than or equal to the given <code>value</code> .</p>
<p>Requires:</p>
<ul>
<li>That <code>property</code> comes first in <code>order_by</code> .</li>
</ul></td>
</tr>
<tr class="even">
<td><code>GREATER_THAN</code></td>
<td><p>The given <code>property</code> is greater than the given <code>value</code> .</p>
<p>Requires:</p>
<ul>
<li>That <code>property</code> comes first in <code>order_by</code> .</li>
</ul></td>
</tr>
<tr class="odd">
<td><code>GREATER_THAN_OR_EQUAL</code></td>
<td><p>The given <code>property</code> is greater than or equal to the given <code>value</code> .</p>
<p>Requires:</p>
<ul>
<li>That <code>property</code> comes first in <code>order_by</code> .</li>
</ul></td>
</tr>
<tr class="even">
<td><code>EQUAL</code></td>
<td>The given <code>property</code> is equal to the given <code>value</code> .</td>
</tr>
<tr class="odd">
<td><code>IN</code></td>
<td><p>The given <code>property</code> is equal to at least one value in the given array.</p>
<p>Requires:</p>
<ul>
<li>That <code>value</code> is a non-empty <code>ArrayValue</code> , subject to disjunction limits.</li>
<li>No <code>NOT_IN</code> is in the same query.</li>
</ul></td>
</tr>
<tr class="even">
<td><code>NOT_EQUAL</code></td>
<td><p>The given <code>property</code> is not equal to the given <code>value</code> .</p>
<p>Requires:</p>
<ul>
<li>No other <code>NOT_EQUAL</code> or <code>NOT_IN</code> is in the same query.</li>
<li>That <code>property</code> comes first in the <code>order_by</code> .</li>
</ul></td>
</tr>
<tr class="odd">
<td><code>HAS_ANCESTOR</code></td>
<td><p>Limit the result set to the given entity and its descendants.</p>
<p>Requires:</p>
<ul>
<li>That <code>value</code> is an entity key.</li>
<li>All evaluated disjunctions must have the same <code>HAS_ANCESTOR</code> filter.</li>
</ul></td>
</tr>
<tr class="even">
<td><code>NOT_IN</code></td>
<td><p>The value of the <code>property</code> is not in the given array.</p>
<p>Requires:</p>
<ul>
<li>That <code>value</code> is a non-empty <code>ArrayValue</code> with at most 10 values.</li>
<li>No other <code>OR</code> , <code>IN</code> , <code>NOT_IN</code> , <code>NOT_EQUAL</code> is in the same query.</li>
<li>That <code>field</code> comes first in the <code>order_by</code> .</li>
</ul></td>
</tr>
</tbody>
</table>

## PropertyMask

The set of arbitrarily nested property paths used to restrict an operation to only a subset of properties in an entity.

| Fields    |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
|-----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `paths[]` | `string` The paths to the properties covered by this mask. A path is a list of property names separated by dots ( `.` ), for example `foo.bar` means the property `bar` inside the entity property `foo` inside the entity associated with this path. If a property name contains a dot `.` or a backslash `\` , then that name must be escaped. A path must not be empty, and may not reference a value inside an [`array value`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.Value.FIELDS.google.datastore.v1beta3.ArrayValue.google.datastore.v1beta3.Value.array_value) . |

## PropertyOrder

The desired order for a specific property.

| Fields      |                                                                                                                                                                                                               |
|-------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `property`  | [`PropertyReference`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.PropertyReference) The property to order by.                          |
| `direction` | [`Direction`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.PropertyOrder.Direction) The direction to order by. Defaults to `ASCENDING` . |

## Direction

The sort direction.

| Enums                   |                                           |
|-------------------------|-------------------------------------------|
| `DIRECTION_UNSPECIFIED` | Unspecified. This value must not be used. |
| `ASCENDING`             | Ascending.                                |
| `DESCENDING`            | Descending.                               |

## PropertyReference

A reference to a property relative to the kind expressions.

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
<td><code>name</code></td>
<td><p><code>string</code></p>
<p>A reference to a property.</p>
<p>Requires:</p>
<ul>
<li>MUST be a dot-delimited ( <code>.</code> ) string of segments, where each segment conforms to <a href="https://docs.cloud.google.com/static/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.Entity.FIELDS.repeated.google.datastore.v1beta3.Entity.PropertiesEntry.google.datastore.v1beta3.Entity.properties"><code>entity property name</code></a> limitations.</li>
</ul></td>
</tr>
</tbody>
</table>

## PropertyTransform

A transformation of an entity property.

| Fields                                                                                                                         |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
|--------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `property`                                                                                                                     | `string` Optional. The name of the property. Property paths (a list of property names separated by dots ( `.` )) may be used to refer to properties inside entity values. For example `foo.bar` means the property `bar` inside the entity property `foo` . If a property name contains a dot `.` or a backlslash `\` , then that name must be escaped.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| Union field `transform_type` . The transformation to apply to the property. `transform_type` can be only one of the following: |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| `set_to_server_value`                                                                                                          | [`ServerValue`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.PropertyTransform.ServerValue) Sets the property to the given server value.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| `increment`                                                                                                                    | [`Value`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.Value) Adds the given value to the property's current value. This must be an integer or a double value. If the property is not an integer or double, or if the property does not yet exist, the transformation will set the property to the given value. If either of the given value or the current property value are doubles, both values will be interpreted as doubles. Double arithmetic and representation of double values follows IEEE 754 semantics. If there is positive/negative integer overflow, the property is resolved to the largest magnitude positive/negative integer.                                                                                                                                             |
| `maximum`                                                                                                                      | [`Value`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.Value) Sets the property to the maximum of its current value and the given value. This must be an integer or a double value. If the property is not an integer or double, or if the property does not yet exist, the transformation will set the property to the given value. If a maximum operation is applied where the property and the input value are of mixed types (that is - one is an integer and one is a double) the property takes on the type of the larger operand. If the operands are equivalent (e.g. 3 and 3.0), the property does not change. 0, 0.0, and -0.0 are all zero. The maximum of a zero stored value and zero input value is always the stored value. The maximum of any numeric value x and NaN is NaN.  |
| `minimum`                                                                                                                      | [`Value`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.Value) Sets the property to the minimum of its current value and the given value. This must be an integer or a double value. If the property is not an integer or double, or if the property does not yet exist, the transformation will set the property to the input value. If a minimum operation is applied where the property and the input value are of mixed types (that is - one is an integer and one is a double) the property takes on the type of the smaller operand. If the operands are equivalent (e.g. 3 and 3.0), the property does not change. 0, 0.0, and -0.0 are all zero. The minimum of a zero stored value and zero input value is always the stored value. The minimum of any numeric value x and NaN is NaN. |
| `append_missing_elements`                                                                                                      | [`ArrayValue`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.ArrayValue) Appends the given elements in order if they are not already present in the current property value. If the property is not an array, or if the property does not yet exist, it is first set to the empty array. Equivalent numbers of different types (e.g. 3L and 3.0) are considered equal when checking if a value is missing. NaN is equal to NaN, and the null value is equal to the null value. If the input contains multiple equivalent values, only the first will be considered. The corresponding transform result will be the null value.                                                                                                                                                                   |
| `remove_all_from_array`                                                                                                        | [`ArrayValue`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.ArrayValue) Removes all of the given elements from the array in the property. If the property is not an array, or if the property does not yet exist, it is set to the empty array. Equivalent numbers of different types (e.g. 3L and 3.0) are considered equal when deciding whether an element should be removed. NaN is equal to NaN, and the null value is equal to the null value. This will remove all equivalent values if there are duplicates. The corresponding transform result will be the null value.                                                                                                                                                                                                                |

## ServerValue

A value that is calculated by the server.

| Enums                      |                                                                                                                                                                                                                      |
|----------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `SERVER_VALUE_UNSPECIFIED` | Unspecified. This value must not be used.                                                                                                                                                                            |
| `REQUEST_TIME`             | The time at which the server processed the request, with millisecond precision. If used on multiple properties (same or different entities) in a transaction, all the properties will get the same server timestamp. |

## Query

A query for entities.

The query stages are executed in the following order: 1. kind 2. filter 3. projection 4. order + start_cursor + end_cursor 5. offset 6. limit 7. find_nearest

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
<td><code>projection[]</code></td>
<td><p><a href="https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.Projection"><code>Projection</code></a></p>
<p>The projection to return. Defaults to returning all properties.</p></td>
</tr>
<tr class="even">
<td><code>kind[]</code></td>
<td><p><a href="https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.KindExpression"><code>KindExpression</code></a></p>
<p>The kinds to query (if empty, returns entities of all kinds). Currently at most 1 kind may be specified.</p></td>
</tr>
<tr class="odd">
<td><code>filter</code></td>
<td><p><a href="https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.Filter"><code>Filter</code></a></p>
<p>The filter to apply.</p></td>
</tr>
<tr class="even">
<td><code>order[]</code></td>
<td><p><a href="https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.PropertyOrder"><code>PropertyOrder</code></a></p>
<p>The order to apply to the query results (if empty, order is unspecified).</p></td>
</tr>
<tr class="odd">
<td><code>distinct_on[]</code></td>
<td><p><a href="https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.PropertyReference"><code>PropertyReference</code></a></p>
<p>The properties to make distinct. The query results will contain the first result for each distinct combination of values for the given properties (if empty, all results are returned).</p>
<p>Requires:</p>
<ul>
<li>If <code>order</code> is specified, the set of distinct on properties must appear before the non-distinct on properties in <code>order</code> .</li>
</ul></td>
</tr>
<tr class="even">
<td><code>start_cursor</code></td>
<td><p><code>bytes</code></p>
<p>A starting point for the query results. Query cursors are returned in query result batches and <a href="https://cloud.google.com/datastore/docs/concepts/queries#cursors_limits_and_offsets">can only be used to continue the same query</a> .</p></td>
</tr>
<tr class="odd">
<td><code>end_cursor</code></td>
<td><p><code>bytes</code></p>
<p>An ending point for the query results. Query cursors are returned in query result batches and <a href="https://cloud.google.com/datastore/docs/concepts/queries#cursors_limits_and_offsets">can only be used to limit the same query</a> .</p></td>
</tr>
<tr class="even">
<td><code>offset</code></td>
<td><p><code>int32</code></p>
<p>The number of results to skip. Applies before limit, but after all other constraints. Optional. Must be &gt;= 0 if specified.</p></td>
</tr>
<tr class="odd">
<td><code>limit</code></td>
<td><p><a href="https://protobuf.dev/reference/protobuf/google.protobuf/#int32-value"><code>Int32Value</code></a></p>
<p>The maximum number of results to return. Applies after all other constraints. Optional. Unspecified is interpreted as no limit. Must be &gt;= 0 if specified.</p></td>
</tr>
</tbody>
</table>

## QueryResultBatch

A batch of results produced by a query.

| Fields               |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
|----------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `skipped_results`    | `int32` The number of results skipped, typically because of an offset.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| `skipped_cursor`     | `bytes` A cursor that points to the position after the last skipped result. Will be set when `skipped_results` != 0.                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| `entity_result_type` | [`ResultType`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.EntityResult.ResultType) The result type for every entity in `entity_results` .                                                                                                                                                                                                                                                                                                                                                                    |
| `entity_results[]`   | [`EntityResult`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.EntityResult) The results for this batch.                                                                                                                                                                                                                                                                                                                                                                                                        |
| `end_cursor`         | `bytes` A cursor that points to the position after the last result in the batch.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| `more_results`       | [`MoreResultsType`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.QueryResultBatch.MoreResultsType) The state of the query after the current batch.                                                                                                                                                                                                                                                                                                                                                             |
| `snapshot_version`   | `int64` The version number of the snapshot this batch was returned from. This applies to the range of results from the query's `start_cursor` (or the beginning of the query if no cursor was given) to this batch's `end_cursor` (not the query's `end_cursor` ). In a single transaction, subsequent query result batches for the same query can have a greater snapshot version number. Each batch's snapshot version is valid for all preceding batches. The value will be zero for eventually consistent queries.                                                              |
| `read_time`          | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) Read timestamp this batch was returned from. This applies to the range of results from the query's `start_cursor` (or the beginning of the query if no cursor was given) to this batch's `end_cursor` (not the query's `end_cursor` ). In a single transaction, subsequent query result batches for the same query can have a greater timestamp. Each batch's read timestamp is valid for all preceding batches. This value will not be set for eventually consistent queries in Cloud Datastore. |

## MoreResultsType

The possible values for the `more_results` field.

| Enums                           |                                                                            |
|---------------------------------|----------------------------------------------------------------------------|
| `MORE_RESULTS_TYPE_UNSPECIFIED` | Unspecified. This value is never used.                                     |
| `NOT_FINISHED`                  | There may be additional batches to fetch from this query.                  |
| `MORE_RESULTS_AFTER_LIMIT`      | The query is finished, but there may be more results after the limit.      |
| `MORE_RESULTS_AFTER_CURSOR`     | The query is finished, but there may be more results after the end cursor. |
| `NO_MORE_RESULTS`               | The query is finished, and there are no more results.                      |

## ReadOptions

The options shared by read requests.

| Fields                                                                                                                                                                                                                                                                                                                                                                                                                                               |                                                                                                                                                                                                                                                                                                                                                                                             |
|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `consistency_type` . For Cloud Firestore in Datastore mode, if you don't specify read_consistency then all lookups and queries default to `read_consistency` = `STRONG` . Note that, in Cloud Datastore, global queries defaulted to `read_consistency` = `EVENTUAL` . Explicitly setting `read_consistency` = `EVENTUAL` will result in eventually consistent lookups and queries. `consistency_type` can be only one of the following: |                                                                                                                                                                                                                                                                                                                                                                                             |
| `read_consistency`                                                                                                                                                                                                                                                                                                                                                                                                                                   | [`ReadConsistency`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.ReadOptions.ReadConsistency) The non-transactional read consistency to use.                                                                                                                                                                           |
| `transaction`                                                                                                                                                                                                                                                                                                                                                                                                                                        | `bytes` The identifier of the transaction in which to read. A transaction identifier is returned by a call to [`Datastore.BeginTransaction`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.Datastore.BeginTransaction) .                                                                                                |
| `read_time`                                                                                                                                                                                                                                                                                                                                                                                                                                          | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) Reads entities as they were at the given time. This value is only supported for Cloud Firestore in Datastore mode. This must be a microsecond precision timestamp within the past one hour, or if Point-in-Time Recovery is enabled, can additionally be a whole minute timestamp within the past 7 days. |

## ReadConsistency

The possible values for read consistencies.

| Enums                          |                                           |
|--------------------------------|-------------------------------------------|
| `READ_CONSISTENCY_UNSPECIFIED` | Unspecified. This value must not be used. |
| `STRONG`                       | Strong consistency.                       |
| `EVENTUAL`                     | Eventual consistency.                     |

## ReserveIdsRequest

The request for [`Datastore.ReserveIds`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.Datastore.ReserveIds) .

| Fields        |                                                                                                                                                                                                                                 |
|---------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `project_id`  | `string` Required. The ID of the project against which to make the request.                                                                                                                                                     |
| `database_id` | `string` The ID of the database against which to make the request. '(default)' is not allowed; please use empty string '' to refer the default database.                                                                        |
| `keys[]`      | [`Key`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.Key) Required. A list of keys with complete key paths whose numeric IDs should not be auto-allocated. |

## ReserveIdsResponse

This type has no fields.

The response for [`Datastore.ReserveIds`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.Datastore.ReserveIds) .

## RollbackRequest

The request for [`Datastore.Rollback`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.Datastore.Rollback) .

| Fields        |                                                                                                                                                                                                                                                    |
|---------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `project_id`  | `string` Required. The ID of the project against which to make the request.                                                                                                                                                                        |
| `transaction` | `bytes` Required. The transaction identifier, returned by a call to [`Datastore.BeginTransaction`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.Datastore.BeginTransaction) . |

## RollbackResponse

This type has no fields.

The response for [`Datastore.Rollback`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.Datastore.Rollback) . (an empty message).

## RunAggregationQueryRequest

The request for [`Datastore.RunAggregationQuery`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.Datastore.RunAggregationQuery) .

| Fields                                                                                       |                                                                                                                                                                                                                                                                                                                                               |
|----------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `project_id`                                                                                 | `string` Required. The ID of the project against which to make the request.                                                                                                                                                                                                                                                                   |
| `partition_id`                                                                               | [`PartitionId`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.PartitionId) Entities are partitioned into subsets, identified by a partition ID. Queries are scoped to a single partition. This partition ID is normalized with the standard default context partition ID. |
| `read_options`                                                                               | [`ReadOptions`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.ReadOptions) The options for this query.                                                                                                                                                                    |
| `explain_options`                                                                            | [`ExplainOptions`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.ExplainOptions) Optional. Explain options for the query. If set, additional query statistics will be returned. If not, only query results will be returned.                                              |
| Union field `query_type` . The type of query. `query_type` can be only one of the following: |                                                                                                                                                                                                                                                                                                                                               |
| `aggregation_query`                                                                          | [`AggregationQuery`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.AggregationQuery) The query to run.                                                                                                                                                                    |
| `gql_query`                                                                                  | [`GqlQuery`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.GqlQuery) The GQL query to run. This query must be an aggregation query.                                                                                                                                       |

## RunAggregationQueryResponse

The response for [`Datastore.RunAggregationQuery`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.Datastore.RunAggregationQuery) .

| Fields            |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
|-------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `batch`           | [`AggregationResultBatch`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.AggregationResultBatch) A batch of aggregation results. Always present.                                                                                                                                                                                                                                                                                                                                                                                  |
| `query`           | [`AggregationQuery`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.AggregationQuery) The parsed form of the `GqlQuery` from the request, if it was set.                                                                                                                                                                                                                                                                                                                                                                           |
| `explain_metrics` | [`ExplainMetrics`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.ExplainMetrics) Query explain metrics. This is only present when the [`RunAggregationQueryRequest.explain_options`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.RunAggregationQueryRequest.FIELDS.google.datastore.v1beta3.ExplainOptions.google.datastore.v1beta3.RunAggregationQueryRequest.explain_options) is provided, and it is sent only once with the last response in the stream. |

## RunQueryRequest

The request for [`Datastore.RunQuery`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.Datastore.RunQuery) .

| Fields                                                                                       |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
|----------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `project_id`                                                                                 | `string` Required. The ID of the project against which to make the request.                                                                                                                                                                                                                                                                                                                                                                                                                            |
| `partition_id`                                                                               | [`PartitionId`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.PartitionId) Entities are partitioned into subsets, identified by a partition ID. Queries are scoped to a single partition. This partition ID is normalized with the standard default context partition ID.                                                                                                                                                          |
| `read_options`                                                                               | [`ReadOptions`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.ReadOptions) The options for this query.                                                                                                                                                                                                                                                                                                                             |
| `property_mask`                                                                              | [`PropertyMask`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.PropertyMask) The properties to return. This field must not be set for a projection query. See [`LookupRequest.property_mask`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.LookupRequest.FIELDS.google.datastore.v1beta3.PropertyMask.google.datastore.v1beta3.LookupRequest.property_mask) . |
| `explain_options`                                                                            | [`ExplainOptions`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.ExplainOptions) Optional. Explain options for the query. If set, additional query statistics will be returned. If not, only query results will be returned.                                                                                                                                                                                                       |
| Union field `query_type` . The type of query. `query_type` can be only one of the following: |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `query`                                                                                      | [`Query`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.Query) The query to run.                                                                                                                                                                                                                                                                                                                                                   |
| `gql_query`                                                                                  | [`GqlQuery`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.GqlQuery) The GQL query to run. This query must be a non-aggregation query.                                                                                                                                                                                                                                                                                             |

## RunQueryResponse

The response for [`Datastore.RunQuery`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.Datastore.RunQuery) .

| Fields            |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
|-------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `batch`           | [`QueryResultBatch`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.QueryResultBatch) A batch of query results. This is always present unless running a query under explain-only mode: [`RunQueryRequest.explain_options`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.RunQueryRequest.FIELDS.google.datastore.v1beta3.ExplainOptions.google.datastore.v1beta3.RunQueryRequest.explain_options) was provided and [`ExplainOptions.analyze`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.ExplainOptions.FIELDS.bool.google.datastore.v1beta3.ExplainOptions.analyze) was set to false. |
| `query`           | [`Query`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.Query) The parsed form of the `GqlQuery` from the request, if it was set.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| `explain_metrics` | [`ExplainMetrics`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.ExplainMetrics) Query explain metrics. This is only present when the [`RunQueryRequest.explain_options`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.RunQueryRequest.FIELDS.google.datastore.v1beta3.ExplainOptions.google.datastore.v1beta3.RunQueryRequest.explain_options) is provided, and it is sent only once with the last response in the stream.                                                                                                                                                                                                                                 |

## TransactionOptions

Options for beginning a new transaction.

Transactions can be created explicitly with calls to [`Datastore.BeginTransaction`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.Datastore.BeginTransaction) or implicitly by setting `ReadOptions.new_transaction` in read requests.

| Fields                                                                                                                                          |                                                                                                                                                                                                                   |
|-------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `mode` . The `mode` of the transaction, indicating whether write operations are supported. `mode` can be only one of the following: |                                                                                                                                                                                                                   |
| `read_write`                                                                                                                                    | [`ReadWrite`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.TransactionOptions.ReadWrite) The transaction should allow both reads and writes. |
| `read_only`                                                                                                                                     | [`ReadOnly`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.TransactionOptions.ReadOnly) The transaction should only allow reads.              |

## ReadOnly

Options specific to read-only transactions.

| Fields      |                                                                                                                                                                                                                                                                                                            |
|-------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `read_time` | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) Reads entities at the given time. This must be a microsecond precision timestamp within the past one hour, or if Point-in-Time Recovery is enabled, can additionally be a whole minute timestamp within the past 7 days. |

## ReadWrite

Options specific to read / write transactions.

| Fields                 |                                                                      |
|------------------------|----------------------------------------------------------------------|
| `previous_transaction` | `bytes` The transaction identifier of the transaction being retried. |

## Value

A message that can hold any of the supported value types and associated metadata.

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
<td><code>meaning</code></td>
<td><p><code>int32</code></p>
<p>The <code>meaning</code> field should only be populated for backwards compatibility.</p></td>
</tr>
<tr class="even">
<td><code>exclude_from_indexes</code></td>
<td><p><code>bool</code></p>
<p>If the value should be excluded from all indexes including those defined explicitly.</p></td>
</tr>
<tr class="odd">
<td>Union field <code>value_type</code> . Must have a value set. <code>value_type</code> can be only one of the following:</td>
<td></td>
</tr>
<tr class="even">
<td><code>null_value</code></td>
<td><p><a href="https://protobuf.dev/reference/protobuf/google.protobuf/#null-value"><code>NullValue</code></a></p>
<p>A null value.</p></td>
</tr>
<tr class="odd">
<td><code>boolean_value</code></td>
<td><p><code>bool</code></p>
<p>A boolean value.</p></td>
</tr>
<tr class="even">
<td><code>integer_value</code></td>
<td><p><code>int64</code></p>
<p>An integer value.</p></td>
</tr>
<tr class="odd">
<td><code>double_value</code></td>
<td><p><code>double</code></p>
<p>A double value.</p></td>
</tr>
<tr class="even">
<td><code>timestamp_value</code></td>
<td><p><a href="https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp"><code>Timestamp</code></a></p>
<p>A timestamp value. When stored in the Datastore, precise only to microseconds; any additional precision is rounded down.</p></td>
</tr>
<tr class="odd">
<td><code>key_value</code></td>
<td><p><a href="https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.Key"><code>Key</code></a></p>
<p>A key value.</p></td>
</tr>
<tr class="even">
<td><code>string_value</code></td>
<td><p><code>string</code></p>
<p>A UTF-8 encoded string value. When <code>exclude_from_indexes</code> is false (it is indexed) , may have at most 1500 bytes. Otherwise, may be set to at most 1,000,000 bytes.</p></td>
</tr>
<tr class="odd">
<td><code>blob_value</code></td>
<td><p><code>bytes</code></p>
<p>A blob value. May have at most 1,000,000 bytes. When <code>exclude_from_indexes</code> is false, may have at most 1500 bytes. In JSON requests, must be base64-encoded.</p></td>
</tr>
<tr class="even">
<td><code>geo_point_value</code></td>
<td><p><a href="https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.type#google.type.LatLng"><code>LatLng</code></a></p>
<p>A geo point value representing a point on the surface of Earth.</p></td>
</tr>
<tr class="odd">
<td><code>entity_value</code></td>
<td><p><a href="https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.Entity"><code>Entity</code></a></p>
<p>An entity value.</p>
<ul>
<li>May have no key.</li>
<li>May have a key with an incomplete key path.</li>
<li>May have a reserved/read-only key.</li>
</ul></td>
</tr>
<tr class="even">
<td><code>array_value</code></td>
<td><p><a href="https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.ArrayValue"><code>ArrayValue</code></a></p>
<p>An array value. Cannot contain another array value. A <code>Value</code> instance that sets field <code>array_value</code> must not set fields <code>meaning</code> or <code>exclude_from_indexes</code> .</p></td>
</tr>
</tbody>
</table>
