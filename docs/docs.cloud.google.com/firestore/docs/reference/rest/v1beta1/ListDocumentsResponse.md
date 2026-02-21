The response for `  Firestore.ListDocuments  ` .

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
  &quot;documents&quot;: [
    {
      object (Document)
    }
  ],
  &quot;nextPageToken&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  documents[]  `

`  object ( Document  ` )

The Documents found.

`  nextPageToken  `

`  string  `

A token to retrieve the next page of documents.

If this field is omitted, there are no subsequent pages.
