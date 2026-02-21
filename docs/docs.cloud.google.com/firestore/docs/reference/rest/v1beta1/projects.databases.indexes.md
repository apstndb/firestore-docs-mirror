## Resource: Index

An index definition.

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
  &quot;collectionId&quot;: string,
  &quot;fields&quot;: [
    {
      object (IndexField)
    }
  ],
  &quot;state&quot;: enum (State)
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  name  `

`  string  `

The resource name of the index. Output only.

`  collectionId  `

`  string  `

The collection ID to which this index applies. Required.

`  fields[]  `

`  object ( IndexField  ` )

The fields to index.

`  state  `

`  enum ( State  ` )

The state of the index. Output only.

## IndexField

A field of an index.

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
  &quot;fieldPath&quot;: string,
  &quot;mode&quot;: enum (Mode)
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  fieldPath  `

`  string  `

The path of the field. Must match the field path specification described by \[google.firestore.v1beta1.Document.fields\]\[fields\]. Special field path `  __name__  ` may be used by itself or at the end of a path. `  __type__  ` may be used only at the end of path.

`  mode  `

`  enum ( Mode  ` )

The field's mode.

## Mode

The mode determines how a field is indexed.

Enums

`  MODE_UNSPECIFIED  `

The mode is unspecified.

`  ASCENDING  `

The field's values are indexed so as to support sequencing in ascending order and also query by \<, \>, \<=, \>=, and =.

`  DESCENDING  `

The field's values are indexed so as to support sequencing in descending order and also query by \<, \>, \<=, \>=, and =.

`  ARRAY_CONTAINS  `

The field's array values are indexed so as to support membership using ARRAY\_CONTAINS queries.

## State

The state of an index. During index creation, an index will be in the `  CREATING  ` state. If the index is created successfully, it will transition to the `  READY  ` state. If the index is not able to be created, it will transition to the `  ERROR  ` state.

Enums

`  STATE_UNSPECIFIED  `

The state is unspecified.

`  CREATING  `

The index is being created. There is an active long-running operation for the index. The index is updated when writing a document. Some index data may exist.

`  READY  `

The index is ready to be used. The index is updated when writing a document. The index is fully populated from all stored documents it applies to.

`  ERROR  `

The index was being created, but something went wrong. There is no active long-running operation for the index, and the most recently finished long-running operation failed. The index is not updated when writing a document. Some index data may exist.

## Methods

### `             create           `

Creates the specified index.

### `             delete           `

Deletes an index.

### `             get           `

Gets an index.

### `             list           `

Lists the indexes that match the specified filters.
