---
name: documents/docs.cloud.google.com/firestore/docs/reference/rest/Shared.Types/ExportDocumentsResponse
uri: https://docs.cloud.google.com/firestore/docs/reference/rest/Shared.Types/ExportDocumentsResponse
title: ExportDocumentsResponse
description: A cloud-hosted NoSQL database that's simple enough for rapid prototyping yet scalable and flexible enough to grow to any size.
data_source: docs.cloud.google.com
---

Returned in the `  google.longrunning.Operation  ` response field.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;outputUriPrefix&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`outputUriPrefix`

`string`

Location of the output files. This can be used to begin an import into Cloud Firestore (this project or another project) after the operation completes successfully.
