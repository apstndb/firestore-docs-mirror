  - [JSON representation](#SCHEMA_REPRESENTATION)

Metadata common to all Datastore Admin operations.

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
  &quot;operationType&quot;: enum (OperationType),
  &quot;labels&quot;: {
    string: string,
    ...
  },
  &quot;state&quot;: enum (State)
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  startTime  `

`  string ( Timestamp  ` format)

The time that work began on the operation.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `  "2014-10-02T15:01:23Z"  ` , `  "2014-10-02T15:01:23.045123456Z"  ` or `  "2014-10-02T15:01:23+05:30"  ` .

`  endTime  `

`  string ( Timestamp  ` format)

The time the operation ended, either successfully or otherwise.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `  "2014-10-02T15:01:23Z"  ` , `  "2014-10-02T15:01:23.045123456Z"  ` or `  "2014-10-02T15:01:23+05:30"  ` .

`  operationType  `

`  enum ( OperationType  ` )

The type of the operation. Can be used as a filter in ListOperationsRequest.

`  labels  `

`  map (key: string, value: string)  `

The client-assigned labels which were provided when the operation was created. May also include additional labels.

An object containing a list of `  "key": value  ` pairs. Example: `  { "name": "wrench", "mass": "1.3kg", "count": "3" }  ` .

`  state  `

`  enum ( State  ` )

The current state of the Operation.
