  - [JSON representation](#SCHEMA_REPRESENTATION)
  - [Projection](#Projection)
      - [JSON representation](#Projection.SCHEMA_REPRESENTATION)
  - [KindExpression](#KindExpression)
      - [JSON representation](#KindExpression.SCHEMA_REPRESENTATION)
  - [Filter](#Filter)
      - [JSON representation](#Filter.SCHEMA_REPRESENTATION)
  - [CompositeFilter](#CompositeFilter)
      - [JSON representation](#CompositeFilter.SCHEMA_REPRESENTATION)
  - [Operator](#Operator)
  - [PropertyFilter](#PropertyFilter)
      - [JSON representation](#PropertyFilter.SCHEMA_REPRESENTATION)
  - [Operator](#Operator_1)
  - [PropertyOrder](#PropertyOrder)
      - [JSON representation](#PropertyOrder.SCHEMA_REPRESENTATION)
  - [Direction](#Direction)

A query for entities.

The query stages are executed in the following order: 1. kind 2. filter 3. projection 4. order + startCursor + endCursor 5. offset 6. limit 7. findNearest

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
  &quot;projection&quot;: [
    {
      object (Projection)
    }
  ],
  &quot;kind&quot;: [
    {
      object (KindExpression)
    }
  ],
  &quot;filter&quot;: {
    object (Filter)
  },
  &quot;order&quot;: [
    {
      object (PropertyOrder)
    }
  ],
  &quot;distinctOn&quot;: [
    {
      object (PropertyReference)
    }
  ],
  &quot;startCursor&quot;: string,
  &quot;endCursor&quot;: string,
  &quot;offset&quot;: integer,
  &quot;limit&quot;: integer
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  projection[]  `

`  object ( Projection  ` )

The projection to return. Defaults to returning all properties.

`  kind[]  `

`  object ( KindExpression  ` )

The kinds to query (if empty, returns entities of all kinds). Currently at most 1 kind may be specified.

`  filter  `

`  object ( Filter  ` )

The filter to apply.

`  order[]  `

`  object ( PropertyOrder  ` )

The order to apply to the query results (if empty, order is unspecified).

`  distinctOn[]  `

`  object ( PropertyReference  ` )

The properties to make distinct. The query results will contain the first result for each distinct combination of values for the given properties (if empty, all results are returned).

Requires:

  - If `  order  ` is specified, the set of distinct on properties must appear before the non-distinct on properties in `  order  ` .

`  startCursor  `

`  string ( bytes format)  `

A starting point for the query results. Query cursors are returned in query result batches and [can only be used to continue the same query](https://cloud.google.com/datastore/docs/concepts/queries#cursors_limits_and_offsets) .

A base64-encoded string.

`  endCursor  `

`  string ( bytes format)  `

An ending point for the query results. Query cursors are returned in query result batches and [can only be used to limit the same query](https://cloud.google.com/datastore/docs/concepts/queries#cursors_limits_and_offsets) .

A base64-encoded string.

`  offset  `

`  integer  `

The number of results to skip. Applies before limit, but after all other constraints. Optional. Must be \>= 0 if specified.

`  limit  `

`  integer  `

The maximum number of results to return. Applies after all other constraints. Optional. Unspecified is interpreted as no limit. Must be \>= 0 if specified.

## Projection

A representation of a property in a projection.

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

The property to project.

## KindExpression

A representation of a kind.

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
  &quot;name&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  name  `

`  string  `

The name of the kind.

## Filter

A holder for any type of filter.

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

  // Union field filter_type can be only one of the following:
  &quot;compositeFilter&quot;: {
    object (CompositeFilter)
  },
  &quot;propertyFilter&quot;: {
    object (PropertyFilter)
  }
  // End of list of possible types for union field filter_type.
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `  filter_type  ` . The type of filter. `  filter_type  ` can be only one of the following:

`  compositeFilter  `

`  object ( CompositeFilter  ` )

A composite filter.

`  propertyFilter  `

`  object ( PropertyFilter  ` )

A filter on a property.

## CompositeFilter

A filter that merges multiple other filters using the given operator.

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
  &quot;op&quot;: enum (Operator),
  &quot;filters&quot;: [
    {
      object (Filter)
    }
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  op  `

`  enum ( Operator  ` )

The operator for combining multiple filters.

`  filters[]  `

`  object ( Filter  ` )

The list of filters to combine.

Requires:

  - At least one filter is present.

## Operator

A composite filter operator.

Enums

`  OPERATOR_UNSPECIFIED  `

Unspecified. This value must not be used.

`  AND  `

The results are required to satisfy each of the combined filters.

`  OR  `

Documents are required to satisfy at least one of the combined filters.

## PropertyFilter

A filter on a specific property.

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
  },
  &quot;op&quot;: enum (Operator),
  &quot;value&quot;: {
    object (Value)
  }
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  property  `

`  object ( PropertyReference  ` )

The property to filter by.

`  op  `

`  enum ( Operator  ` )

The operator to filter by.

`  value  `

`  object ( Value  ` )

The value to compare the property to.

## Operator

A property filter operator.

Enums

`  OPERATOR_UNSPECIFIED  `

Unspecified. This value must not be used.

`  LESS_THAN  `

The given `  property  ` is less than the given `  value  ` .

Requires:

  - That `  property  ` comes first in `  order_by  ` .

`  LESS_THAN_OR_EQUAL  `

The given `  property  ` is less than or equal to the given `  value  ` .

Requires:

  - That `  property  ` comes first in `  order_by  ` .

`  GREATER_THAN  `

The given `  property  ` is greater than the given `  value  ` .

Requires:

  - That `  property  ` comes first in `  order_by  ` .

`  GREATER_THAN_OR_EQUAL  `

The given `  property  ` is greater than or equal to the given `  value  ` .

Requires:

  - That `  property  ` comes first in `  order_by  ` .

`  EQUAL  `

The given `  property  ` is equal to the given `  value  ` .

`  IN  `

The given `  property  ` is equal to at least one value in the given array.

Requires:

  - That `  value  ` is a non-empty `  ArrayValue  ` , subject to disjunction limits.
  - No `  NOT_IN  ` is in the same query.

`  NOT_EQUAL  `

The given `  property  ` is not equal to the given `  value  ` .

Requires:

  - No other `  NOT_EQUAL  ` or `  NOT_IN  ` is in the same query.
  - That `  property  ` comes first in the `  order_by  ` .

`  HAS_ANCESTOR  `

Limit the result set to the given entity and its descendants.

Requires:

  - That `  value  ` is an entity key.
  - All evaluated disjunctions must have the same `  HAS_ANCESTOR  ` filter.

`  NOT_IN  `

The value of the `  property  ` is not in the given array.

Requires:

  - That `  value  ` is a non-empty `  ArrayValue  ` with at most 10 values.
  - No other `  OR  ` , `  IN  ` , `  NOT_IN  ` , `  NOT_EQUAL  ` is in the same query.
  - That `  field  ` comes first in the `  order_by  ` .

## PropertyOrder

The desired order for a specific property.

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
  },
  &quot;direction&quot;: enum (Direction)
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  property  `

`  object ( PropertyReference  ` )

The property to order by.

`  direction  `

`  enum ( Direction  ` )

The direction to order by. Defaults to `  ASCENDING  ` .

## Direction

The sort direction.

Enums

`  DIRECTION_UNSPECIFIED  `

Unspecified. This value must not be used.

`  ASCENDING  `

Ascending.

`  DESCENDING  `

Descending.
