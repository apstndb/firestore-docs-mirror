  - [JSON representation](#SCHEMA_REPRESENTATION)

The response for `  google.datastore.admin.v1.DatastoreAdmin.ExportEntities  ` .

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
  &quot;outputUrl&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  outputUrl  `

`  string  `

Location of the output metadata file. This can be used to begin an import into Cloud Datastore (this project or another project). See `  google.datastore.admin.v1.ImportEntitiesRequest.input_url  ` . Only present if the operation completed successfully.
