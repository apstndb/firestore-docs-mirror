---
name: documents/docs.cloud.google.com/firestore/docs/reference/rest/v1/ExplainOptions
uri: https://docs.cloud.google.com/firestore/docs/reference/rest/v1/ExplainOptions
title: ExplainOptions
description: A cloud-hosted NoSQL database that's simple enough for rapid prototyping yet scalable and flexible enough to grow to any size.
data_source: docs.cloud.google.com
update_time: "2025-10-17T23:18:34Z"
---

Explain options for the query.

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
  &quot;analyze&quot;: boolean
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`analyze`

`boolean`

Optional. Whether to execute this query.

When false (the default), the query will be planned, returning only metrics from the planning stages.

When true, the query will be planned and executed, returning the full query results along with both planning and execution stage metrics.
