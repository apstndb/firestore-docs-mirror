---
name: documents/docs.cloud.google.com/datastore/docs/reference/data/rest/Shared.Types/ArrayValue
uri: https://docs.cloud.google.com/datastore/docs/reference/data/rest/Shared.Types/ArrayValue
title: ArrayValue
description: A highly-scalable NoSQL database for your web and mobile applications that automatically handles sharding and replication.
data_source: docs.cloud.google.com
update_time: "2025-10-17T22:06:14Z"
---

  - [JSON representation](https://docs.cloud.google.com/datastore/docs/reference/data/rest/Shared.Types/ArrayValue#SCHEMA_REPRESENTATION)

An array value.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;values&quot;: [{object (Value)}]}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`values[]`

` object ( Value  ` )

Values in the array. The order of values in an array is preserved as long as all values have identical settings for 'excludeFromIndexes'.
