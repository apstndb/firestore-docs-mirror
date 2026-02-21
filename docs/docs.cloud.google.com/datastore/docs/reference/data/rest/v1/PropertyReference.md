  - [JSON representation](#SCHEMA_REPRESENTATION)

A reference to a property relative to the kind expressions.

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

A reference to a property.

Requires:

  - MUST be a dot-delimited ( `  .  ` ) string of segments, where each segment conforms to `  entity property name  ` limitations.
