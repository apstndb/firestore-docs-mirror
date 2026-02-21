  - [JSON representation](#SCHEMA_REPRESENTATION)

Metadata for ImportEntities operations.

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
  &quot;inputUrl&quot;: string
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

Description of which entities are being imported.

`  inputUrl  `

`  string  `

The location of the import metadata file. This will be the same value as the `  google.datastore.admin.v1.ExportEntitiesResponse.output_url  ` field.
