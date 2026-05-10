---
name: documents/docs.cloud.google.com/datastore/docs/reference/data/rest/Shared.Types/GqlQueryParameter
uri: https://docs.cloud.google.com/datastore/docs/reference/data/rest/Shared.Types/GqlQueryParameter
title: GqlQueryParameter
description: A highly-scalable NoSQL database for your web and mobile applications that automatically handles sharding and replication.
data_source: docs.cloud.google.com
update_time: "2025-10-17T22:06:14Z"
---

  - [JSON representation](https://docs.cloud.google.com/datastore/docs/reference/data/rest/Shared.Types/GqlQueryParameter#SCHEMA_REPRESENTATION)

A binding parameter for a GQL query.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field parameter_type can be only one of the following:&quot;value&quot;: {object (Value)},&quot;cursor&quot;: string// End of list of possible types for union field parameter_type.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `parameter_type` . The type of parameter. `parameter_type` can be only one of the following:

`value`

` object ( Value  ` )

A value parameter.

`cursor`

`string ( bytes format)`

A query cursor. Query cursors are returned in query result batches.

A base64-encoded string.
