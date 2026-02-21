A position in a query result set.

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
  &quot;values&quot;: [
    {
      object (Value)
    }
  ],
  &quot;before&quot;: boolean
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  values[]  `

`  object ( Value  ` )

The values that represent a position, in the order they appear in the order by clause of a query.

Can contain fewer values than specified in the order by clause.

`  before  `

`  boolean  `

If the position is just before or just after the given values, relative to the sort order defined by the query.
