Metadata for `  google.longrunning.Operation  ` results from `  FirestoreAdmin.UpdateField  ` .

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
  &quot;startTime&quot;: string,
  &quot;endTime&quot;: string,
  &quot;field&quot;: string,
  &quot;indexConfigDeltas&quot;: [
    {
      object (IndexConfigDelta)
    }
  ],
  &quot;state&quot;: enum (OperationState),
  &quot;progressDocuments&quot;: {
    object (Progress)
  },
  &quot;progressBytes&quot;: {
    object (Progress)
  },
  &quot;ttlConfigDelta&quot;: {
    object (TtlConfigDelta)
  }
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  startTime  `

`  string ( Timestamp  ` format)

The time this operation started.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `  "2014-10-02T15:01:23Z"  ` , `  "2014-10-02T15:01:23.045123456Z"  ` or `  "2014-10-02T15:01:23+05:30"  ` .

`  endTime  `

`  string ( Timestamp  ` format)

The time this operation completed. Will be unset if operation still in progress.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `  "2014-10-02T15:01:23Z"  ` , `  "2014-10-02T15:01:23.045123456Z"  ` or `  "2014-10-02T15:01:23+05:30"  ` .

`  field  `

`  string  `

The field resource that this operation is acting on. For example: `  projects/{projectId}/databases/{databaseId}/collectionGroups/{collectionId}/fields/{fieldPath}  `

`  indexConfigDeltas[]  `

`  object ( IndexConfigDelta  ` )

A list of `  IndexConfigDelta  ` , which describe the intent of this operation.

`  state  `

`  enum ( OperationState  ` )

The state of the operation.

`  progressDocuments  `

`  object ( Progress  ` )

The progress, in documents, of this operation.

`  progressBytes  `

`  object ( Progress  ` )

The progress, in bytes, of this operation.

`  ttlConfigDelta  `

`  object ( TtlConfigDelta  ` )

Describes the deltas of TTL configuration.

## IndexConfigDelta

Information about an index configuration change.

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
  &quot;changeType&quot;: enum (ChangeType),
  &quot;index&quot;: {
    object (Index)
  }
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  changeType  `

`  enum ( ChangeType  ` )

Specifies how the index is changing.

`  index  `

`  object ( Index  ` )

The index being changed.

## Index

Cloud Firestore indexes enable simple and complex queries against documents in a database.

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
  &quot;queryScope&quot;: enum (QueryScope),
  &quot;apiScope&quot;: enum (ApiScope),
  &quot;fields&quot;: [
    {
      object (IndexField)
    }
  ],
  &quot;state&quot;: enum (State),
  &quot;density&quot;: enum (Density),
  &quot;multikey&quot;: boolean,
  &quot;shardCount&quot;: integer,
  &quot;unique&quot;: boolean
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  name  `

`  string  `

Output only. A server defined name for this index. The form of this name for composite indexes will be: `  projects/{projectId}/databases/{databaseId}/collectionGroups/{collectionId}/indexes/{composite_index_id}  ` For single field indexes, this field will be empty.

`  queryScope  `

`  enum ( QueryScope  ` )

Indexes with a collection query scope specified allow queries against a collection that is the child of a specific document, specified at query time, and that has the same collection ID.

Indexes with a collection group query scope specified allow queries against all collections descended from a specific document, specified at query time, and that have the same collection ID as this index.

`  apiScope  `

`  enum ( ApiScope  ` )

The API scope supported by this index.

`  fields[]  `

`  object ( IndexField  ` )

The fields supported by this index.

For composite indexes, this requires a minimum of 2 and a maximum of 100 fields. The last field entry is always for the field path `  __name__  ` . If, on creation, `  __name__  ` was not specified as the last field, it will be added automatically with the same direction as that of the last field defined. If the final field in a composite index is not directional, the `  __name__  ` will be ordered ASCENDING (unless explicitly specified).

For single field indexes, this will always be exactly one entry with a field path equal to the field path of the associated field.

`  state  `

`  enum ( State  ` )

Output only. The serving state of the index.

`  density  `

`  enum ( Density  ` )

Immutable. The density configuration of the index.

`  multikey  `

`  boolean  `

Optional. Whether the index is multikey. By default, the index is not multikey. For non-multikey indexes, none of the paths in the index definition reach or traverse an array, except via an explicit array index. For multikey indexes, at most one of the paths in the index definition reach or traverse an array, except via an explicit array index. Violations will result in errors.

Note this field only applies to index with MONGODB\_COMPATIBLE\_API ApiScope.

`  shardCount  `

`  integer  `

Optional. The number of shards for the index.

`  unique  `

`  boolean  `

Optional. Whether it is an unique index. Unique index ensures all values for the indexed field(s) are unique across documents.

## IndexField

A field in an index. The fieldPath describes which field is indexed, the value\_mode describes how the field value is indexed.

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

  // Union field value_mode can be only one of the following:
  &quot;order&quot;: enum (Order),
  &quot;arrayConfig&quot;: enum (ArrayConfig),
  &quot;vectorConfig&quot;: {
    object (VectorConfig)
  }
  // End of list of possible types for union field value_mode.
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  fieldPath  `

`  string  `

Can be **name** . For single field indexes, this must match the name of the field or may be omitted.

Union field `  value_mode  ` . How the field value is indexed. `  value_mode  ` can be only one of the following:

`  order  `

`  enum ( Order  ` )

Indicates that this field supports ordering by the specified order or comparing using =, \!=, \<, \<=, \>, \>=.

`  arrayConfig  `

`  enum ( ArrayConfig  ` )

Indicates that this field supports operations on `  arrayValue  ` s.

`  vectorConfig  `

`  object ( VectorConfig  ` )

Indicates that this field supports nearest neighbor and distance operations on vector.

## VectorConfig

The index configuration to support vector search operations

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
  &quot;dimension&quot;: integer,

  // Union field type can be only one of the following:
  &quot;flat&quot;: {
    object (FlatIndex)
  }
  // End of list of possible types for union field type.
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  dimension  `

`  integer  `

Required. The vector dimension this configuration applies to.

The resulting index will only include vectors of this dimension, and can be used for vector search with the same dimension.

Union field `  type  ` . The type of index used. `  type  ` can be only one of the following:

`  flat  `

`  object ( FlatIndex  ` )

Indicates the vector index is a flat index.

## FlatIndex

This type has no fields.

An index that stores vectors in a flat data structure, and supports exhaustive search.

## TtlConfigDelta

Information about a TTL configuration change.

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
  &quot;changeType&quot;: enum (ChangeType)
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  changeType  `

`  enum ( ChangeType  ` )

Specifies how the TTL configuration is changing.
