---
name: documents/docs.cloud.google.com/datastore/docs/reference/data/rest/v1/Query
uri: https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/Query
title: Query
description: A highly-scalable NoSQL database for your web and mobile applications that automatically handles sharding and replication.
data_source: docs.cloud.google.com
---

- [JSON representation](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/Query#SCHEMA_REPRESENTATION)
- [Projection](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/Query#Projection)
  - [JSON representation](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/Query#Projection.SCHEMA_REPRESENTATION)
- [KindExpression](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/Query#KindExpression)
  - [JSON representation](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/Query#KindExpression.SCHEMA_REPRESENTATION)
- [Filter](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/Query#Filter)
  - [JSON representation](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/Query#Filter.SCHEMA_REPRESENTATION)
- [CompositeFilter](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/Query#CompositeFilter)
  - [JSON representation](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/Query#CompositeFilter.SCHEMA_REPRESENTATION)
- [Operator](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/Query#Operator)
- [PropertyFilter](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/Query#PropertyFilter)
  - [JSON representation](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/Query#PropertyFilter.SCHEMA_REPRESENTATION)
- [Operator](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/Query#Operator_1)
- [PropertyOrder](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/Query#PropertyOrder)
  - [JSON representation](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/Query#PropertyOrder.SCHEMA_REPRESENTATION)
- [Direction](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/Query#Direction)

A query for entities.

The query stages are executed in the following order: 1. kind 2. filter 3. projection 4. order + startCursor + endCursor 5. offset 6. limit 7. findNearest

**JSON representation**

```
{
  "projection": [
    {
      object (Projection)
    }
  ],
  "kind": [
    {
      object (KindExpression)
    }
  ],
  "filter": {
    object (Filter)
  },
  "order": [
    {
      object (PropertyOrder)
    }
  ],
  "distinctOn": [
    {
      object (PropertyReference)
    }
  ],
  "startCursor": string,
  "endCursor": string,
  "offset": integer,
  "limit": integer
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
<td><code>projection[]</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/Query#Projection"><code>Projection</code></a><code> )</code></p>
<p>The projection to return. Defaults to returning all properties.</p></td>
</tr>
<tr class="even">
<td><code>kind[]</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/Query#KindExpression"><code>KindExpression</code></a><code> )</code></p>
<p>The kinds to query (if empty, returns entities of all kinds). Currently at most 1 kind may be specified.</p></td>
</tr>
<tr class="odd">
<td><code>filter</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/Query#Filter"><code>Filter</code></a><code> )</code></p>
<p>The filter to apply.</p></td>
</tr>
<tr class="even">
<td><code>order[]</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/Query#PropertyOrder"><code>PropertyOrder</code></a><code> )</code></p>
<p>The order to apply to the query results (if empty, order is unspecified).</p></td>
</tr>
<tr class="odd">
<td><code>distinctOn[]</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/PropertyReference"><code>PropertyReference</code></a><code> )</code></p>
<p>The properties to make distinct. The query results will contain the first result for each distinct combination of values for the given properties (if empty, all results are returned).</p>
<p>Requires:</p>
<ul>
<li>If <code>order</code> is specified, the set of distinct on properties must appear before the non-distinct on properties in <code>order</code> .</li>
</ul></td>
</tr>
<tr class="even">
<td><code>startCursor</code></td>
<td><p><code>string ( </code><a href="https://developers.google.com/discovery/v1/type-format"><code>bytes</code></a><code> format)</code></p>
<p>A starting point for the query results. Query cursors are returned in query result batches and <a href="https://cloud.google.com/datastore/docs/concepts/queries#cursors_limits_and_offsets">can only be used to continue the same query</a> .</p>
<p>A base64-encoded string.</p></td>
</tr>
<tr class="odd">
<td><code>endCursor</code></td>
<td><p><code>string ( </code><a href="https://developers.google.com/discovery/v1/type-format"><code>bytes</code></a><code> format)</code></p>
<p>An ending point for the query results. Query cursors are returned in query result batches and <a href="https://cloud.google.com/datastore/docs/concepts/queries#cursors_limits_and_offsets">can only be used to limit the same query</a> .</p>
<p>A base64-encoded string.</p></td>
</tr>
<tr class="even">
<td><code>offset</code></td>
<td><p><code>integer</code></p>
<p>The number of results to skip. Applies before limit, but after all other constraints. Optional. Must be &gt;= 0 if specified.</p></td>
</tr>
<tr class="odd">
<td><code>limit</code></td>
<td><p><code>integer</code></p>
<p>The maximum number of results to return. Applies after all other constraints. Optional. Unspecified is interpreted as no limit. Must be &gt;= 0 if specified.</p></td>
</tr>
</tbody>
</table>

## Projection

A representation of a property in a projection.

**JSON representation**

```
{
  "property": {
    object (PropertyReference)
  }
}
```

| Fields     |                                                                                                                                                      |
|------------|------------------------------------------------------------------------------------------------------------------------------------------------------|
| `property` | `object ( `[`PropertyReference`](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/PropertyReference)` )` The property to project. |

## KindExpression

A representation of a kind.

**JSON representation**

```
{
  "name": string
}
```

| Fields |                                |
|--------|--------------------------------|
| `name` | `string` The name of the kind. |

## Filter

A holder for any type of filter.

**JSON representation**

```
{

  // Union field filter_type can be only one of the following:
  "compositeFilter": {
    object (CompositeFilter)
  },
  "propertyFilter": {
    object (PropertyFilter)
  }
  // End of list of possible types for union field filter_type.
}
```

| Fields                                                                                          |                                                                                                                                                     |
|-------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `filter_type` . The type of filter. `filter_type` can be only one of the following: |                                                                                                                                                     |
| `compositeFilter`                                                                               | `object ( `[`CompositeFilter`](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/Query#CompositeFilter)` )` A composite filter.   |
| `propertyFilter`                                                                                | `object ( `[`PropertyFilter`](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/Query#PropertyFilter)` )` A filter on a property. |

## CompositeFilter

A filter that merges multiple other filters using the given operator.

**JSON representation**

```
{
  "op": enum (Operator),
  "filters": [
    {
      object (Filter)
    }
  ]
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
<td><code>op</code></td>
<td><p><code>enum ( </code><a href="https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/Query#Operator"><code>Operator</code></a><code> )</code></p>
<p>The operator for combining multiple filters.</p></td>
</tr>
<tr class="even">
<td><code>filters[]</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/Query#Filter"><code>Filter</code></a><code> )</code></p>
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

## PropertyFilter

A filter on a specific property.

**JSON representation**

```
{
  "property": {
    object (PropertyReference)
  },
  "op": enum (Operator),
  "value": {
    object (Value)
  }
}
```

| Fields     |                                                                                                                                                        |
|------------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| `property` | `object ( `[`PropertyReference`](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/PropertyReference)` )` The property to filter by. |
| `op`       | `enum ( `[`Operator`](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/Query#Operator_1)` )` The operator to filter by.             |
| `value`    | `object ( `[`Value`](https://docs.cloud.google.com/datastore/docs/reference/data/rest/Shared.Types/Value)` )` The value to compare the property to.    |

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

## PropertyOrder

The desired order for a specific property.

**JSON representation**

```
{
  "property": {
    object (PropertyReference)
  },
  "direction": enum (Direction)
}
```

| Fields      |                                                                                                                                                                      |
|-------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `property`  | `object ( `[`PropertyReference`](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/PropertyReference)` )` The property to order by.                |
| `direction` | `enum ( `[`Direction`](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/Query#Direction)` )` The direction to order by. Defaults to `ASCENDING` . |

## Direction

The sort direction.

| Enums                   |                                           |
|-------------------------|-------------------------------------------|
| `DIRECTION_UNSPECIFIED` | Unspecified. This value must not be used. |
| `ASCENDING`             | Ascending.                                |
| `DESCENDING`            | Descending.                               |
