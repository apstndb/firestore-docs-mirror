---
name: documents/docs.cloud.google.com/firestore/docs/reference/rest/v1beta1/StructuredQuery
uri: https://docs.cloud.google.com/firestore/docs/reference/rest/v1beta1/StructuredQuery
title: StructuredQuery
description: A cloud-hosted NoSQL database that's simple enough for rapid prototyping yet scalable and flexible enough to grow to any size.
data_source: docs.cloud.google.com
---

A Firestore query.

The query stages are executed in the following order: 1. from 2. where 3. select 4. orderBy + startAt + endAt 5. offset 6. limit 7. findNearest

**JSON representation**

```
{
  "select": {
    object (Projection)
  },
  "from": [
    {
      object (CollectionSelector)
    }
  ],
  "where": {
    object (Filter)
  },
  "orderBy": [
    {
      object (Order)
    }
  ],
  "startAt": {
    object (Cursor)
  },
  "endAt": {
    object (Cursor)
  },
  "offset": integer,
  "limit": integer,
  "findNearest": {
    object (FindNearest)
  }
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
<td><code>select</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/firestore/docs/reference/rest/v1beta1/StructuredQuery#Projection"><code>Projection</code></a><code> )</code></p>
<p>Optional sub-set of the fields to return.</p>
<p>This acts as a <a href="https://docs.cloud.google.com/firestore/docs/reference/rest/v1beta1/DocumentMask"><code>DocumentMask</code></a> over the documents returned from a query. When not set, assumes that the caller wants all fields returned.</p></td>
</tr>
<tr class="even">
<td><code>from[]</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/firestore/docs/reference/rest/v1beta1/StructuredQuery#CollectionSelector"><code>CollectionSelector</code></a><code> )</code></p>
<p>The collections to query.</p></td>
</tr>
<tr class="odd">
<td><code>where</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/firestore/docs/reference/rest/v1beta1/StructuredQuery#Filter"><code>Filter</code></a><code> )</code></p>
<p>The filter to apply.</p></td>
</tr>
<tr class="even">
<td><code>orderBy[]</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/firestore/docs/reference/rest/v1beta1/StructuredQuery#Order"><code>Order</code></a><code> )</code></p>
<p>The order to apply to the query results.</p>
<p>Callers can provide a full ordering, a partial ordering, or no ordering at all. While Firestore will always respect the provided order, the behavior for queries without a full ordering is different per database edition:</p>
<p>In Standard edition, Firestore guarantees a stable ordering through the following rules:</p>
<ul>
<li>The <code>orderBy</code> is required to reference all fields used with an inequality filter.</li>
<li>All fields that are required to be in the <code>orderBy</code> but are not already present are appended in lexicographical ordering of the field name.</li>
<li>If an order on <code>__name__</code> is not specified, it is appended by default.</li>
</ul>
<p>Fields are appended with the same sort direction as the last order specified, or 'ASCENDING' if no order was specified. For example:</p>
<ul>
<li><code>ORDER BY a</code> becomes <code>ORDER BY a ASC, __name__ ASC</code></li>
<li><code>ORDER BY a DESC</code> becomes <code>ORDER BY a DESC, __name__ DESC</code></li>
<li><code>WHERE a &gt; 1</code> becomes <code>WHERE a &gt; 1 ORDER BY a ASC, __name__ ASC</code></li>
<li><code>WHERE __name__ &gt; ... AND a &gt; 1</code> becomes <code>WHERE __name__ &gt; ... AND a &gt; 1 ORDER BY a ASC, __name__ ASC</code></li>
</ul>
<p>In Enterprise edition, Firestore does not guarantee a stable ordering. Instead it will pick the most efficient ordering based on the indexes available at the time of query execution. This will result in a different ordering for queries that are otherwise identical. To ensure a stable ordering, always include a unique field in the <code>orderBy</code> clause, such as <code>__name__</code> .</p></td>
</tr>
<tr class="odd">
<td><code>startAt</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/firestore/docs/reference/rest/v1beta1/Cursor"><code>Cursor</code></a><code> )</code></p>
<p>A potential prefix of a position in the result set to start the query at.</p>
<p>The ordering of the result set is based on the <code>ORDER BY</code> clause of the original query.</p>
<pre data-fenced=""><code>SELECT * FROM k WHERE a = 1 AND b &gt; 2 ORDER BY b ASC, __name__ ASC;</code></pre>
<p>This query's results are ordered by <code>(b ASC, __name__ ASC)</code> .</p>
<p>Cursors can reference either the full ordering or a prefix of the location, though it cannot reference more fields than what are in the provided <code>ORDER BY</code> .</p>
<p>Continuing off the example above, attaching the following start cursors will have varying impact:</p>
<ul>
<li><code>START BEFORE (2, /k/123)</code> : start the query right before <code>a = 1 AND b &gt; 2 AND __name__ &gt; /k/123</code> .</li>
<li><code>START AFTER (10)</code> : start the query right after <code>a = 1 AND b &gt; 10</code> .</li>
</ul>
<p>Unlike <code>OFFSET</code> which requires scanning over the first N results to skip, a start cursor allows the query to begin at a logical position. This position is not required to match an actual result, it will scan forward from this position to find the next document.</p>
<p>Requires:</p>
<ul>
<li>The number of values cannot be greater than the number of fields specified in the <code>ORDER BY</code> clause.</li>
</ul></td>
</tr>
<tr class="even">
<td><code>endAt</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/firestore/docs/reference/rest/v1beta1/Cursor"><code>Cursor</code></a><code> )</code></p>
<p>A potential prefix of a position in the result set to end the query at.</p>
<p>This is similar to <code>START_AT</code> but with it controlling the end position rather than the start position.</p>
<p>Requires:</p>
<ul>
<li>The number of values cannot be greater than the number of fields specified in the <code>ORDER BY</code> clause.</li>
</ul></td>
</tr>
<tr class="odd">
<td><code>offset</code></td>
<td><p><code>integer</code></p>
<p>The number of documents to skip before returning the first result.</p>
<p>This applies after the constraints specified by the <code>WHERE</code> , <code>START AT</code> , &amp; <code>END AT</code> but before the <code>LIMIT</code> clause.</p>
<p>Requires:</p>
<ul>
<li>The value must be greater than or equal to zero if specified.</li>
</ul></td>
</tr>
<tr class="even">
<td><code>limit</code></td>
<td><p><code>integer</code></p>
<p>The maximum number of results to return.</p>
<p>Applies after all other constraints.</p>
<p>Requires:</p>
<ul>
<li>The value must be greater than or equal to zero if specified.</li>
</ul></td>
</tr>
<tr class="odd">
<td><code>findNearest</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/firestore/docs/reference/rest/v1beta1/StructuredQuery#FindNearest"><code>FindNearest</code></a><code> )</code></p>
<p>Optional. A potential nearest neighbors search.</p>
<p>Applies after all other filters and ordering.</p>
<p>Finds the closest vector embeddings to the given query vector.</p></td>
</tr>
</tbody>
</table>

## Projection

The projection of document's fields to return.

**JSON representation**

```
{
  "fields": [
    {
      object (FieldReference)
    }
  ]
}
```

| Fields     |                                                                                                                                                                                                                                              |
|------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `fields[]` | `object ( `[`FieldReference`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1beta1/FieldReference)` )` The fields to return. If empty, all fields are returned. To only return the name of the document, use `['__name__']` . |

## CollectionSelector

A selection of a collection, such as `messages as m1` .

**JSON representation**

```
{
  "collectionId": string,
  "allDescendants": boolean
}
```

| Fields           |                                                                                                                                                                                           |
|------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `collectionId`   | `string` The collection ID. When set, selects only collections with this ID.                                                                                                              |
| `allDescendants` | `boolean` When false, selects only collections that are immediate children of the `parent` specified in the containing `RunQueryRequest` . When true, selects all descendant collections. |

## Filter

A filter.

**JSON representation**

```
{

  // Union field filter_type can be only one of the following:
  "compositeFilter": {
    object (CompositeFilter)
  },
  "fieldFilter": {
    object (FieldFilter)
  },
  "unaryFilter": {
    object (UnaryFilter)
  }
  // End of list of possible types for union field filter_type.
}
```

| Fields                                                                                          |                                                                                                                                                                           |
|-------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `filter_type` . The type of filter. `filter_type` can be only one of the following: |                                                                                                                                                                           |
| `compositeFilter`                                                                               | `object ( `[`CompositeFilter`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1beta1/StructuredQuery#CompositeFilter)` )` A composite filter.               |
| `fieldFilter`                                                                                   | `object ( `[`FieldFilter`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1beta1/StructuredQuery#FieldFilter)` )` A filter on a document field.             |
| `unaryFilter`                                                                                   | `object ( `[`UnaryFilter`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1beta1/StructuredQuery#UnaryFilter)` )` A filter that takes exactly one argument. |

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
<td><p><code>enum ( </code><a href="https://docs.cloud.google.com/firestore/docs/reference/rest/v1beta1/StructuredQuery#Operator"><code>Operator</code></a><code> )</code></p>
<p>The operator for combining multiple filters.</p></td>
</tr>
<tr class="even">
<td><code>filters[]</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/firestore/docs/reference/rest/v1beta1/StructuredQuery#Filter"><code>Filter</code></a><code> )</code></p>
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
| `AND`                  | Documents are required to satisfy all of the combined filters.          |
| `OR`                   | Documents are required to satisfy at least one of the combined filters. |

## FieldFilter

A filter on a specific field.

**JSON representation**

```
{
  "field": {
    object (FieldReference)
  },
  "op": enum (Operator),
  "value": {
    object (Value)
  }
}
```

| Fields  |                                                                                                                                                      |
|---------|------------------------------------------------------------------------------------------------------------------------------------------------------|
| `field` | `object ( `[`FieldReference`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1beta1/FieldReference)` )` The field to filter by.        |
| `op`    | `enum ( `[`Operator`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1beta1/StructuredQuery#Operator_1)` )` The operator to filter by. |
| `value` | `object ( ``Value`` )` The value to compare to.                                                                                                      |

## Operator

A field filter operator.

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
<td><p>The given <code>field</code> is less than the given <code>value</code> .</p>
<p>Requires:</p>
<ul>
<li>That <code>field</code> come first in <code>orderBy</code> .</li>
</ul></td>
</tr>
<tr class="odd">
<td><code>LESS_THAN_OR_EQUAL</code></td>
<td><p>The given <code>field</code> is less than or equal to the given <code>value</code> .</p>
<p>Requires:</p>
<ul>
<li>That <code>field</code> come first in <code>orderBy</code> .</li>
</ul></td>
</tr>
<tr class="even">
<td><code>GREATER_THAN</code></td>
<td><p>The given <code>field</code> is greater than the given <code>value</code> .</p>
<p>Requires:</p>
<ul>
<li>That <code>field</code> come first in <code>orderBy</code> .</li>
</ul></td>
</tr>
<tr class="odd">
<td><code>GREATER_THAN_OR_EQUAL</code></td>
<td><p>The given <code>field</code> is greater than or equal to the given <code>value</code> .</p>
<p>Requires:</p>
<ul>
<li>That <code>field</code> come first in <code>orderBy</code> .</li>
</ul></td>
</tr>
<tr class="even">
<td><code>EQUAL</code></td>
<td>The given <code>field</code> is equal to the given <code>value</code> .</td>
</tr>
<tr class="odd">
<td><code>NOT_EQUAL</code></td>
<td><p>The given <code>field</code> is not equal to the given <code>value</code> .</p>
<p>Requires:</p>
<ul>
<li>No other <code>NOT_EQUAL</code> , <code>NOT_IN</code> , <code>IS_NOT_NULL</code> , or <code>IS_NOT_NAN</code> .</li>
<li>That <code>field</code> comes first in the <code>orderBy</code> .</li>
</ul></td>
</tr>
<tr class="even">
<td><code>ARRAY_CONTAINS</code></td>
<td>The given <code>field</code> is an array that contains the given <code>value</code> .</td>
</tr>
<tr class="odd">
<td><code>IN</code></td>
<td><p>The given <code>field</code> is equal to at least one value in the given array.</p>
<p>Requires:</p>
<ul>
<li>That <code>value</code> is a non-empty <code>ArrayValue</code> , subject to disjunction limits.</li>
<li>No <code>NOT_IN</code> filters in the same query.</li>
</ul></td>
</tr>
<tr class="even">
<td><code>ARRAY_CONTAINS_ANY</code></td>
<td><p>The given <code>field</code> is an array that contains any of the values in the given array.</p>
<p>Requires:</p>
<ul>
<li>That <code>value</code> is a non-empty <code>ArrayValue</code> , subject to disjunction limits.</li>
<li>No other <code>ARRAY_CONTAINS_ANY</code> filters within the same disjunction.</li>
<li>No <code>NOT_IN</code> filters in the same query.</li>
</ul></td>
</tr>
<tr class="odd">
<td><code>NOT_IN</code></td>
<td><p>The value of the <code>field</code> is not in the given array.</p>
<p>Requires:</p>
<ul>
<li>That <code>value</code> is a non-empty <code>ArrayValue</code> with at most 10 values.</li>
<li>No other <code>OR</code> , <code>IN</code> , <code>ARRAY_CONTAINS_ANY</code> , <code>NOT_IN</code> , <code>NOT_EQUAL</code> , <code>IS_NOT_NULL</code> , or <code>IS_NOT_NAN</code> .</li>
<li>That <code>field</code> comes first in the <code>orderBy</code> .</li>
</ul></td>
</tr>
</tbody>
</table>

## UnaryFilter

A filter with a single operand.

**JSON representation**

```
{
  "op": enum (Operator),

  // Union field operand_type can be only one of the following:
  "field": {
    object (FieldReference)
  }
  // End of list of possible types for union field operand_type.
}
```

| Fields                                                                                                    |                                                                                                                                                                 |
|-----------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `op`                                                                                                      | `enum ( `[`Operator`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1beta1/StructuredQuery#Operator_2)` )` The unary operator to apply.          |
| Union field `operand_type` . The argument to the filter. `operand_type` can be only one of the following: |                                                                                                                                                                 |
| `field`                                                                                                   | `object ( `[`FieldReference`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1beta1/FieldReference)` )` The field to which to apply the operator. |

## Operator

A unary operator.

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
<td><code>IS_NAN</code></td>
<td>The given <code>field</code> is equal to <code>NaN</code> .</td>
</tr>
<tr class="odd">
<td><code>IS_NULL</code></td>
<td>The given <code>field</code> is equal to <code>NULL</code> .</td>
</tr>
<tr class="even">
<td><code>IS_NOT_NAN</code></td>
<td><p>The given <code>field</code> is not equal to <code>NaN</code> .</p>
<p>Requires:</p>
<ul>
<li>No other <code>NOT_EQUAL</code> , <code>NOT_IN</code> , <code>IS_NOT_NULL</code> , or <code>IS_NOT_NAN</code> .</li>
<li>That <code>field</code> comes first in the <code>orderBy</code> .</li>
</ul></td>
</tr>
<tr class="odd">
<td><code>IS_NOT_NULL</code></td>
<td><p>The given <code>field</code> is not equal to <code>NULL</code> .</p>
<p>Requires:</p>
<ul>
<li>A single <code>NOT_EQUAL</code> , <code>NOT_IN</code> , <code>IS_NOT_NULL</code> , or <code>IS_NOT_NAN</code> .</li>
<li>That <code>field</code> comes first in the <code>orderBy</code> .</li>
</ul></td>
</tr>
</tbody>
</table>

## Order

An order on a field.

**JSON representation**

```
{
  "field": {
    object (FieldReference)
  },
  "direction": enum (Direction)
}
```

| Fields      |                                                                                                                                                                                |
|-------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `field`     | `object ( `[`FieldReference`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1beta1/FieldReference)` )` The field to order by.                                   |
| `direction` | `enum ( `[`Direction`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1beta1/StructuredQuery#Direction)` )` The direction to order by. Defaults to `ASCENDING` . |

## Direction

A sort direction.

| Enums                   |              |
|-------------------------|--------------|
| `DIRECTION_UNSPECIFIED` | Unspecified. |
| `ASCENDING`             | Ascending.   |
| `DESCENDING`            | Descending.  |

## FindNearest

Nearest Neighbors search config. The ordering provided by FindNearest supersedes the orderBy stage. If multiple documents have the same vector distance, the returned document order is not guaranteed to be stable between queries.

**JSON representation**

```
{
  "vectorField": {
    object (FieldReference)
  },
  "queryVector": {
    object (Value)
  },
  "distanceMeasure": enum (DistanceMeasure),
  "limit": integer,
  "distanceResultField": string,
  "distanceThreshold": number
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
<td><code>vectorField</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/firestore/docs/reference/rest/v1beta1/FieldReference"><code>FieldReference</code></a><code> )</code></p>
<p>Required. An indexed vector field to search upon. Only documents which contain vectors whose dimensionality match the queryVector can be returned.</p></td>
</tr>
<tr class="even">
<td><code>queryVector</code></td>
<td><p><code>object ( </code><code>Value</code><code> )</code></p>
<p>Required. The query vector that we are searching on. Must be a vector of no more than 2048 dimensions.</p></td>
</tr>
<tr class="odd">
<td><code>distanceMeasure</code></td>
<td><p><code>enum ( </code><a href="https://docs.cloud.google.com/firestore/docs/reference/rest/v1beta1/StructuredQuery#DistanceMeasure"><code>DistanceMeasure</code></a><code> )</code></p>
<p>Required. The distance measure to use, required.</p></td>
</tr>
<tr class="even">
<td><code>limit</code></td>
<td><p><code>integer</code></p>
<p>Required. The number of nearest neighbors to return. Must be a positive integer of no more than 1000.</p></td>
</tr>
<tr class="odd">
<td><code>distanceResultField</code></td>
<td><p><code>string</code></p>
<p>Optional. Optional name of the field to output the result of the vector distance calculation. Must conform to <a href="https://docs.cloud.google.com/firestore/docs/reference/rest/v1beta1/projects.databases.documents#Document.FIELDS.fields"><code>document field name</code></a> limitations.</p></td>
</tr>
<tr class="even">
<td><code>distanceThreshold</code></td>
<td><p><code>number</code></p>
<p>Optional. Option to specify a threshold for which no less similar documents will be returned. The behavior of the specified <code>distanceMeasure</code> will affect the meaning of the distance threshold. Since DOT_PRODUCT distances increase when the vectors are more similar, the comparison is inverted.</p>
<ul>
<li>For EUCLIDEAN, COSINE: <code>WHERE distance &lt;= distanceThreshold</code></li>
<li>For DOT_PRODUCT: <code>WHERE distance &gt;= distanceThreshold</code></li>
</ul></td>
</tr>
</tbody>
</table>

## DistanceMeasure

The distance measure to use when comparing vectors.

| Enums                          |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
|--------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `DISTANCE_MEASURE_UNSPECIFIED` | Should not be set.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| `EUCLIDEAN`                    | Measures the EUCLIDEAN distance between the vectors. See [Euclidean](https://en.wikipedia.org/wiki/Euclidean_distance) to learn more. The resulting distance decreases the more similar two vectors are.                                                                                                                                                                                                                                                                                                              |
| `COSINE`                       | COSINE distance compares vectors based on the angle between them, which allows you to measure similarity that isn't based on the vectors magnitude. We recommend using DOT_PRODUCT with unit normalized vectors instead of COSINE distance, which is mathematically equivalent with better performance. See [Cosine Similarity](https://en.wikipedia.org/wiki/Cosine_similarity) to learn more about COSINE similarity and COSINE distance. The resulting COSINE distance decreases the more similar two vectors are. |
| `DOT_PRODUCT`                  | Similar to cosine but is affected by the magnitude of the vectors. See [Dot Product](https://en.wikipedia.org/wiki/Dot_product) to learn more. The resulting distance increases the more similar two vectors are.                                                                                                                                                                                                                                                                                                     |
