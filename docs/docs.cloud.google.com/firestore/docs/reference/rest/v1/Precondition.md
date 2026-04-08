A precondition on a document, used for conditional operations.

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

  // Union field condition_type can be only one of the following:
  &quot;exists&quot;: boolean,
  &quot;updateTime&quot;: string
  // End of list of possible types for union field condition_type.
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `  condition_type  ` . The type of precondition. `  condition_type  ` can be only one of the following:

`  exists  `

`  boolean  `

When set to `  true  ` , the target document must exist. When set to `  false  ` , the target document must not exist.

`  updateTime  `

`  string ( Timestamp  ` format)

When set, the target document must exist and have been last updated at that time. Timestamp must be microsecond aligned.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `  "2014-10-02T15:01:23Z"  ` , `  "2014-10-02T15:01:23.045123456Z"  ` or `  "2014-10-02T15:01:23+05:30"  ` .
