---
name: documents/docs.cloud.google.com/firestore/docs/reference/rest/v1beta1/FieldReference
uri: https://docs.cloud.google.com/firestore/docs/reference/rest/v1beta1/FieldReference
title: FieldReference
description: A cloud-hosted NoSQL database that's simple enough for rapid prototyping yet scalable and flexible enough to grow to any size.
data_source: docs.cloud.google.com
---

A reference to a field in a document, ex: `stats.operations` .

**JSON representation**

```
{
  "fieldPath": string
}
```

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>fieldPath</code></td>
<td><p><code>string</code></p>
<p>A reference to a field in a document.</p>
<p>Requires:</p>
<ul>
<li>MUST be a dot-delimited ( <code>.</code> ) string of segments, where each segment conforms to <a href="https://docs.cloud.google.com/firestore/docs/reference/rest/v1beta1/projects.databases.documents#Document.FIELDS.fields"><code>document field name</code></a> limitations.</li>
</ul></td>
</tr>
</tbody>
</table>
