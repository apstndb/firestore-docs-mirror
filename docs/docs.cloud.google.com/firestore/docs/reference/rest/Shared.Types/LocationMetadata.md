The metadata message for `  google.cloud.location.Location.metadata  ` .

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
  &quot;availableStoragePlacements&quot;: [
    string
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  availableStoragePlacements[]  `

`  string  `

The storage placements available in the location. When the location represents a Standard Managed Multi-Region (SMMR) like "us", this field lists the available Google-Managed Multi-Regions (GMMRs) within it, such as "nam5" or "eur3".
