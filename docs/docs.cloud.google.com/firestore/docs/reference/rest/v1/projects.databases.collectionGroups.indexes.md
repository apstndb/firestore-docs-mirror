## Resource: Index

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

## Methods

### `             create           `

Creates a composite index.

### `             delete           `

Deletes a composite index.

### `             get           `

Gets a composite index.

### `             list           `

Lists composite indexes.
