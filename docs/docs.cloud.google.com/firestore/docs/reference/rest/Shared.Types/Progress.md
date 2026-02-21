Describes the progress of the operation. Unit of work is generic and must be interpreted based on where `  Progress  ` is used.

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
  &quot;estimatedWork&quot;: string,
  &quot;completedWork&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  estimatedWork  `

`  string ( int64 format)  `

The amount of work estimated.

`  completedWork  `

`  string ( int64 format)  `

The amount of work completed.
