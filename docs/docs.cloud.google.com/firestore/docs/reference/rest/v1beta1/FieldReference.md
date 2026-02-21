A reference to a field in a document, ex: `  stats.operations  ` .

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
  &quot;fieldPath&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  fieldPath  `

`  string  `

A reference to a field in a document.

Requires:

  - MUST be a dot-delimited ( `  .  ` ) string of segments, where each segment conforms to `  document field name  ` limitations.
