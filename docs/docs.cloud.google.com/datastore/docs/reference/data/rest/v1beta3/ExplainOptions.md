  - [JSON representation](#SCHEMA_REPRESENTATION)

Explain options for the query.

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
  &quot;analyze&quot;: boolean
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  analyze  `

`  boolean  `

Optional. Whether to execute this query.

When false (the default), the query will be planned, returning only metrics from the planning stages.

When true, the query will be planned and executed, returning the full query results along with both planning and execution stage metrics.
