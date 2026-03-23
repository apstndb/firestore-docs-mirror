The request for `  FirestoreAdmin.CreateIndex  ` .

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
  &quot;parent&quot;: string,
  &quot;index&quot;: {
    object (Index)
  }
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  parent  `

`  string  `

Required. A parent name of the form `  projects/{projectId}/databases/{databaseId}/collectionGroups/{collectionId}  `

`  index  `

`  object ( Index  ` )

Required. The composite index to create.
