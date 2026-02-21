  - [JSON representation](#SCHEMA_REPRESENTATION)

Measures the progress of a particular metric.

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
  &quot;workCompleted&quot;: string,
  &quot;workEstimated&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  workCompleted  `

`  string ( int64 format)  `

The amount of work that has been completed. Note that this may be greater than workEstimated.

`  workEstimated  `

`  string ( int64 format)  `

An estimate of how much work needs to be performed. May be zero if the work estimate is unavailable.
