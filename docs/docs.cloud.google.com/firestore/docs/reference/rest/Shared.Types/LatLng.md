An object that represents a latitude/longitude pair. This is expressed as a pair of doubles to represent degrees latitude and degrees longitude. Unless specified otherwise, this object must conform to the [WGS84 standard](https://en.wikipedia.org/wiki/World_Geodetic_System#1984_version) . Values must be within normalized ranges.

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
  &quot;latitude&quot;: number,
  &quot;longitude&quot;: number
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  latitude  `

`  number  `

The latitude in degrees. It must be in the range \[-90.0, +90.0\].

`  longitude  `

`  number  `

The longitude in degrees. It must be in the range \[-180.0, +180.0\].
