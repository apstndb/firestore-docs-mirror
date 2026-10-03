---
name: documents/docs.cloud.google.com/datastore/docs/reference/data/rest/v1/PropertyReference
uri: https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/PropertyReference
title: PropertyReference
description: A highly-scalable NoSQL database for your web and mobile applications that automatically handles sharding and replication.
data_source: docs.cloud.google.com
---

- [JSON representation](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/PropertyReference#SCHEMA_REPRESENTATION)

A reference to a property relative to the kind expressions.

**JSON representation**

```
{
  "name": string
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
<td><code>name</code></td>
<td><p><code>string</code></p>
<p>A reference to a property.</p>
<p>Requires:</p>
<ul>
<li>MUST be a dot-delimited ( <code>.</code> ) string of segments, where each segment conforms to <a href="https://docs.cloud.google.com/static/datastore/docs/reference/data/rest/Shared.Types/Value#Entity.FIELDS.properties"><code>entity property name</code></a> limitations.</li>
</ul></td>
</tr>
</tbody>
</table>
