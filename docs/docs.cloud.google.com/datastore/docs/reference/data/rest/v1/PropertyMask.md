  - [JSON representation](#SCHEMA_REPRESENTATION)

The set of arbitrarily nested property paths used to restrict an operation to only a subset of properties in an entity.

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
  &quot;paths&quot;: [
    string
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  paths[]  `

`  string  `

The paths to the properties covered by this mask.

A path is a list of property names separated by dots ( `  .  ` ), for example `  foo.bar  ` means the property `  bar  ` inside the entity property `  foo  ` inside the entity associated with this path.

If a property name contains a dot `  .  ` or a backslash `  \  ` , then that name must be escaped.

A path must not be empty, and may not reference a value inside an `  array value  ` .
