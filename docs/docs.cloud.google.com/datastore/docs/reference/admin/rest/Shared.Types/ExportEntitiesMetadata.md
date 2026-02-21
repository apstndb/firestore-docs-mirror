  - [JSON representation](#SCHEMA_REPRESENTATION)

Metadata for ExportEntities operations.

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
  &quot;common&quot;: {
    object (CommonMetadata)
  },
  &quot;progressEntities&quot;: {
    object (Progress)
  },
  &quot;progressBytes&quot;: {
    object (Progress)
  },
  &quot;entityFilter&quot;: {
    object (EntityFilter)
  },
  &quot;outputUrlPrefix&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  common  `

`  object ( CommonMetadata  ` )

Metadata common to all Datastore Admin operations.

`  progressEntities  `

`  object ( Progress  ` )

An estimate of the number of entities processed.

`  progressBytes  `

`  object ( Progress  ` )

An estimate of the number of bytes processed.

`  entityFilter  `

`  object ( EntityFilter  ` )

Description of which entities are being exported.

`  outputUrlPrefix  `

`  string  `

Location for the export metadata and data files. This will be the same value as the `  google.datastore.admin.v1.ExportEntitiesRequest.output_url_prefix  ` field. The final output location is provided in `  google.datastore.admin.v1.ExportEntitiesResponse.output_url  ` .
