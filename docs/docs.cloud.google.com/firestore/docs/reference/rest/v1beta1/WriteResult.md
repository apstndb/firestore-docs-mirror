The result of applying a write.

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
  &quot;updateTime&quot;: string,
  &quot;transformResults&quot;: [
    {
      object (Value)
    }
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  updateTime  `

`  string ( Timestamp  ` format)

The last update time of the document after applying the write. Not set after a `  delete  ` .

If the write did not actually change the document, this will be the previous updateTime.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `  "2014-10-02T15:01:23Z"  ` , `  "2014-10-02T15:01:23.045123456Z"  ` or `  "2014-10-02T15:01:23+05:30"  ` .

`  transformResults[]  `

`  object ( Value  ` )

The results of applying each `  DocumentTransform.FieldTransform  ` , in the same order.
