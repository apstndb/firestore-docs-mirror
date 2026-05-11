---
name: documents/docs.cloud.google.com/firestore/docs/reference/rest/Shared.Types/CreateIndexRequest
uri: https://docs.cloud.google.com/firestore/docs/reference/rest/Shared.Types/CreateIndexRequest
title: CreateIndexRequest
description: A cloud-hosted NoSQL database that's simple enough for rapid prototyping yet scalable and flexible enough to grow to any size.
data_source: docs.cloud.google.com
---

The request for `FirestoreAdmin.CreateIndex` .

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;parent&quot;: string,&quot;index&quot;: {object (Index)}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`parent`

`string`

Required. A parent name of the form `projects/{projectId}/databases/{databaseId}/collectionGroups/{collectionId}`

`index`

` object ( Index  ` )

Required. The composite index to create.
