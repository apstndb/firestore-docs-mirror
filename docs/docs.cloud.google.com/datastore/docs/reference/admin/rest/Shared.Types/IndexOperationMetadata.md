---
name: documents/docs.cloud.google.com/datastore/docs/reference/admin/rest/Shared.Types/IndexOperationMetadata
uri: https://docs.cloud.google.com/datastore/docs/reference/admin/rest/Shared.Types/IndexOperationMetadata
title: IndexOperationMetadata
description: A highly-scalable NoSQL database for your web and mobile applications that automatically handles sharding and replication.
data_source: docs.cloud.google.com
update_time: "2025-10-17T22:06:14Z"
---

  - [JSON representation](https://docs.cloud.google.com/datastore/docs/reference/admin/rest/Shared.Types/IndexOperationMetadata#SCHEMA_REPRESENTATION)

Metadata for Index operations.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;common&quot;: {object (CommonMetadata)},&quot;progressEntities&quot;: {object (Progress)},&quot;indexId&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`common`

` object ( CommonMetadata  ` )

Metadata common to all Datastore Admin operations.

`progressEntities`

` object ( Progress  ` )

An estimate of the number of entities processed.

`indexId`

`string`

The index resource ID that this operation is acting on.
