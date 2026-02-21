  - [JSON representation](#SCHEMA_REPRESENTATION)
  - [Key](#Key)
      - [JSON representation](#Key.SCHEMA_REPRESENTATION)
  - [PartitionId](#PartitionId)
      - [JSON representation](#PartitionId.SCHEMA_REPRESENTATION)
  - [PathElement](#PathElement)
      - [JSON representation](#PathElement.SCHEMA_REPRESENTATION)
  - [Entity](#Entity)
      - [JSON representation](#Entity.SCHEMA_REPRESENTATION)

A message that can hold any of the supported value types and associated metadata.

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
  &quot;meaning&quot;: integer,
  &quot;excludeFromIndexes&quot;: boolean,

  // Union field value_type can be only one of the following:
  &quot;nullValue&quot;: null,
  &quot;booleanValue&quot;: boolean,
  &quot;integerValue&quot;: string,
  &quot;doubleValue&quot;: number,
  &quot;timestampValue&quot;: string,
  &quot;keyValue&quot;: {
    object (Key)
  },
  &quot;stringValue&quot;: string,
  &quot;blobValue&quot;: string,
  &quot;geoPointValue&quot;: {
    object (LatLng)
  },
  &quot;entityValue&quot;: {
    object (Entity)
  },
  &quot;arrayValue&quot;: {
    object (ArrayValue)
  }
  // End of list of possible types for union field value_type.
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  meaning  `

`  integer  `

The `  meaning  ` field should only be populated for backwards compatibility.

`  excludeFromIndexes  `

`  boolean  `

If the value should be excluded from all indexes including those defined explicitly.

Union field `  value_type  ` . Must have a value set. `  value_type  ` can be only one of the following:

`  nullValue  `

`  null  `

A null value.

`  booleanValue  `

`  boolean  `

A boolean value.

`  integerValue  `

`  string ( int64 format)  `

An integer value.

`  doubleValue  `

`  number  `

A double value.

`  timestampValue  `

`  string ( Timestamp  ` format)

A timestamp value. When stored in the Datastore, precise only to microseconds; any additional precision is rounded down.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `  "2014-10-02T15:01:23Z"  ` , `  "2014-10-02T15:01:23.045123456Z"  ` or `  "2014-10-02T15:01:23+05:30"  ` .

`  keyValue  `

`  object ( Key  ` )

A key value.

`  stringValue  `

`  string  `

A UTF-8 encoded string value. When `  excludeFromIndexes  ` is false (it is indexed) , may have at most 1500 bytes. Otherwise, may be set to at most 1,000,000 bytes.

`  blobValue  `

`  string ( bytes format)  `

A blob value. May have at most 1,000,000 bytes. When `  excludeFromIndexes  ` is false, may have at most 1500 bytes. In JSON requests, must be base64-encoded.

A base64-encoded string.

`  geoPointValue  `

`  object ( LatLng  ` )

A geo point value representing a point on the surface of Earth.

`  entityValue  `

`  object ( Entity  ` )

An entity value.

  - May have no key.
  - May have a key with an incomplete key path.
  - May have a reserved/read-only key.

`  arrayValue  `

`  object ( ArrayValue  ` )

An array value. Cannot contain another array value. A `  Value  ` instance that sets field `  arrayValue  ` must not set fields `  meaning  ` or `  excludeFromIndexes  ` .

## Key

A unique identifier for an entity. If a key's partition ID or any of its path kinds or names are reserved/read-only, the key is reserved/read-only. A reserved/read-only key is forbidden in certain documented contexts.

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
  &quot;path&quot;: [
    {
      object (PathElement)
    }
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  partitionId  `

`  object ( PartitionId  ` )

Entities are partitioned into subsets, currently identified by a project ID and namespace ID. Queries are scoped to a single partition.

`  path[]  `

`  object ( PathElement  ` )

The entity path. An entity path consists of one or more elements composed of a kind and a string or numerical identifier, which identify entities. The first element identifies a *root entity* , the second element identifies a *child* of the root entity, the third element identifies a child of the second entity, and so forth. The entities identified by all prefixes of the path are called the element's *ancestors* .

An entity path is always fully complete: *all* of the entity's ancestors are required to be in the path along with the entity identifier itself. The only exception is that in some documented cases, the identifier in the last path element (for the entity) itself may be omitted. For example, the last path element of the key of `  Mutation.insert  ` may have no identifier.

A path can never be empty, and a path can have at most 100 elements.

## PartitionId

A partition ID identifies a grouping of entities. The grouping is always by project and namespace, however the namespace ID may be empty.

A partition ID contains several dimensions: project ID and namespace ID.

Partition dimensions:

  - May be `  ""  ` .
  - Must be valid UTF-8 bytes.
  - Must have values that match regex `  [A-Za-z\d\.\-_]{1,100}  ` If the value of any dimension matches regex `  __.*__  ` , the partition is reserved/read-only. A reserved/read-only partition ID is forbidden in certain documented contexts.

Foreign partition IDs (in which the project ID does not match the context project ID ) are discouraged. Reads and writes of foreign partition IDs may fail if the project is not in an active state.

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
  &quot;databaseId&quot;: string,
  &quot;namespaceId&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  projectId  `

`  string  `

The ID of the project to which the entities belong.

`  databaseId  `

`  string  `

If not empty, the ID of the database to which the entities belong.

`  namespaceId  `

`  string  `

If not empty, the ID of the namespace to which the entities belong.

## PathElement

A (kind, ID/name) pair used to construct a key path.

If either name or ID is set, the element is complete. If neither is set, the element is incomplete.

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
  &quot;kind&quot;: string,

  // Union field id_type can be only one of the following:
  &quot;id&quot;: string,
  &quot;name&quot;: string
  // End of list of possible types for union field id_type.
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  kind  `

`  string  `

The kind of the entity.

A kind matching regex `  __.*__  ` is reserved/read-only. A kind must not contain more than 1500 bytes when UTF-8 encoded. Cannot be `  ""  ` .

Must be valid UTF-8 bytes. Legacy values that are not valid UTF-8 are encoded as `  __bytes<X>__  ` where `  <X>  ` is the base-64 encoding of the bytes.

Union field `  id_type  ` . The type of ID. `  id_type  ` can be only one of the following:

`  id  `

`  string ( int64 format)  `

The auto-allocated ID of the entity.

Never equal to zero. Values less than zero are discouraged and may not be supported in the future.

`  name  `

`  string  `

The name of the entity.

A name matching regex `  __.*__  ` is reserved/read-only. A name must not be more than 1500 bytes when UTF-8 encoded. Cannot be `  ""  ` .

Must be valid UTF-8 bytes. Legacy values that are not valid UTF-8 are encoded as `  __bytes<X>__  ` where `  <X>  ` is the base-64 encoding of the bytes.

## Entity

A Datastore data object.

Must not exceed 1 MiB - 4 bytes.

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
  &quot;key&quot;: {
    object (Key)
  },
  &quot;properties&quot;: {
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

`  key  `

`  object ( Key  ` )

The entity's key.

An entity must have a key, unless otherwise documented (for example, an entity in `  Value.entity_value  ` may have no key). An entity's kind is its key path's last element's kind, or null if it has no key.

`  properties  `

`  map (key: string, value: object ( Value  ` ))

The entity's properties. The map's keys are property names. A property name matching regex `  __.*__  ` is reserved. A reserved property name is forbidden in certain documented contexts. The map keys, represented as UTF-8, must not exceed 1,500 bytes and cannot be empty.

An object containing a list of `  "key": value  ` pairs. Example: `  { "name": "wrench", "mass": "1.3kg", "count": "3" }  ` .
