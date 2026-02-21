  - [Resource: Index](#Index)
      - [JSON representation](#Index.SCHEMA_REPRESENTATION)
  - [AncestorMode](#AncestorMode)
  - [IndexedProperty](#IndexedProperty)
      - [JSON representation](#IndexedProperty.SCHEMA_REPRESENTATION)
  - [Direction](#Direction)
  - [State](#State)
  - [Methods](#METHODS_SUMMARY)

## Resource: Index

Datastore composite index definition.

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
  &quot;projectId&quot;: string,
  &quot;indexId&quot;: string,
  &quot;kind&quot;: string,
  &quot;ancestor&quot;: enum (AncestorMode),
  &quot;properties&quot;: [
    {
      object (IndexedProperty)
    }
  ],
  &quot;state&quot;: enum (State)
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  projectId  `

`  string  `

Output only. Project ID.

`  indexId  `

`  string  `

Output only. The resource ID of the index.

`  kind  `

`  string  `

Required. The entity kind to which this index applies.

`  ancestor  `

`  enum ( AncestorMode  ` )

Required. The index's ancestor mode. Must not be ANCESTOR\_MODE\_UNSPECIFIED.

`  properties[]  `

`  object ( IndexedProperty  ` )

Required. An ordered sequence of property names and their index attributes.

Requires:

  - A maximum of 100 properties.

`  state  `

`  enum ( State  ` )

Output only. The state of the index.

## AncestorMode

For an ordered index, specifies whether each of the entity's ancestors will be included.

Enums

`  ANCESTOR_MODE_UNSPECIFIED  `

The ancestor mode is unspecified.

`  NONE  `

Do not include the entity's ancestors in the index.

`  ALL_ANCESTORS  `

Include all the entity's ancestors in the index.

## IndexedProperty

A property of an index.

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
  &quot;name&quot;: string,
  &quot;direction&quot;: enum (Direction)
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  name  `

`  string  `

Required. The property name to index.

`  direction  `

`  enum ( Direction  ` )

Required. The indexed property's direction. Must not be DIRECTION\_UNSPECIFIED.

## Direction

The direction determines how a property is indexed.

Enums

`  DIRECTION_UNSPECIFIED  `

The direction is unspecified.

`  ASCENDING  `

The property's values are indexed so as to support sequencing in ascending order and also query by \<, \>, \<=, \>=, and =.

`  DESCENDING  `

The property's values are indexed so as to support sequencing in descending order and also query by \<, \>, \<=, \>=, and =.

## State

The possible set of states of an index.

Enums

`  STATE_UNSPECIFIED  `

The state is unspecified.

`  CREATING  `

The index is being created, and cannot be used by queries. There is an active long-running operation for the index. The index is updated when writing an entity. Some index data may exist.

`  READY  `

The index is ready to be used. The index is updated when writing an entity. The index is fully populated from all stored entities it applies to.

`  DELETING  `

The index is being deleted, and cannot be used by queries. There is an active long-running operation for the index. The index is not updated when writing an entity. Some index data may exist.

`  ERROR  `

The index was being created or deleted, but something went wrong. The index cannot by used by queries. There is no active long-running operation for the index, and the most recently finished long-running operation failed. The index is not updated when writing an entity. Some index data may exist.

## Methods

### `             create           `

Creates the specified index.

### `             delete           `

Deletes an existing index.

### `             get           `

Gets an index.

### `             list           `

Lists the indexes that match the specified filters.
