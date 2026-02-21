  - [JSON representation](#SCHEMA_REPRESENTATION)

The result of fetching an entity from Datastore.

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
  &quot;entity&quot;: {
    object (Entity)
  },
  &quot;version&quot;: string,
  &quot;createTime&quot;: string,
  &quot;updateTime&quot;: string,
  &quot;cursor&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  entity  `

`  object ( Entity  ` )

The resulting entity.

`  version  `

`  string ( int64 format)  `

The version of the entity, a strictly positive number that monotonically increases with changes to the entity.

This field is set for `  FULL  ` entity results.

For `  missing  ` entities in `  LookupResponse  ` , this is the version of the snapshot that was used to look up the entity, and it is always set except for eventually consistent reads.

`  createTime  `

`  string ( Timestamp  ` format)

The time at which the entity was created. This field is set for `  FULL  ` entity results. If this entity is missing, this field will not be set.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `  "2014-10-02T15:01:23Z"  ` , `  "2014-10-02T15:01:23.045123456Z"  ` or `  "2014-10-02T15:01:23+05:30"  ` .

`  updateTime  `

`  string ( Timestamp  ` format)

The time at which the entity was last changed. This field is set for `  FULL  ` entity results. If this entity is missing, this field will not be set.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `  "2014-10-02T15:01:23Z"  ` , `  "2014-10-02T15:01:23.045123456Z"  ` or `  "2014-10-02T15:01:23+05:30"  ` .

`  cursor  `

`  string ( bytes format)  `

A cursor that points to the position after the result entity. Set only when the `  EntityResult  ` is part of a `  QueryResultBatch  ` message.

A base64-encoded string.
