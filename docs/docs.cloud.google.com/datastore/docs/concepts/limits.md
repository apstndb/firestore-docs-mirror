This page describes production limits for Firestore in Datastore mode.

**Note:** These values are subject to change.

## Firestore in Datastore mode limits

In addition to these limits, see the [best practices](/datastore/docs/best-practices) for Firestore in Datastore mode.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Limit</th>
<th>Amount</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Maximum number of databases per project</td>
<td><p>100</p>
<p>You can <a href="https://cloud.google.com/support-hub">contact support</a> to request an increase to this limit.</p></td>
</tr>
<tr class="even">
<td>Maximum number of <a href="/datastore/docs/cmek">customer-managed encryption keys (CMEK) databases</a> per project</td>
<td><p>0</p>
<p>By default the quota is 0 because this feature is behind an allowlist. You can request to increase the quota by filling in <a href="https://docs.google.com/forms/d/e/1FAIpQLSfKs8wJf4IXu1NizvfyU2vT59JDbdPvkehMVZ2ab5l_aDLIIA/viewform?resourcekey=0-O15dlRFvA0JIDmh6VFUEcA">the CMEK access request form</a> .</p></td>
</tr>
<tr class="odd">
<td>Maximum API request size.
This limit applies when Datastore mode is used outside of Google App Engine. If Datastore mode is used from App Engine, the limit depends on the client library that is used.</td>
<td>10 MiB</td>
</tr>
<tr class="even">
<td>Maximum size for a transaction</td>
<td>10 MiB</td>
</tr>
<tr class="odd">
<td>Maximum <a href="/datastore/docs/concepts/storage-size">size</a> for an entity</td>
<td>1,048,572 bytes<br />
(1 MiB - 4 bytes)</td>
</tr>
<tr class="even">
<td><p>Maximum number of property transformations that can be performed on a single entity in a <code dir="ltr" translate="no">        Commit       </code> operation or in a transaction.</p>
<p>For array transforms like <code dir="ltr" translate="no">        "appendMissingElements"       </code> , each array element counts towards the limit.</p></td>
<td>500</td>
</tr>
<tr class="odd">
<td>Maximum size for an entity key</td>
<td>6 KiB</td>
</tr>
<tr class="even">
<td>Maximum depth of nested entity values</td>
<td>20</td>
</tr>
<tr class="odd">
<td>Maximum number of keys allowed for a <code dir="ltr" translate="no">       Lookup      </code> operation in the Datastore API</td>
<td>1,000</td>
</tr>
<tr class="even">
<td>Maximum size of an indexed string property's UTF-8 encoding</td>
<td>1,500 bytes</td>
</tr>
<tr class="odd">
<td>Maximum size for an unindexed property</td>
<td>1,048,487 bytes<br />
(1 MiB - 89 bytes)</td>
</tr>
<tr class="even">
<td>Maximum sum of the sizes of an entity's <a href="https://cloud.google.com/datastore/docs/concepts/indexes#composite_indexes">composite index</a> entries</td>
<td>2 MiB</td>
</tr>
<tr class="odd">
<td>Maximum number of composite indexes for a database</td>
<td><ul>
<li><p>200 when you have not enabled billing for your Google Cloud project.</p>
<p>If you need more quota, you must <a href="https://cloud.google.com/billing/docs/how-to/modify-project">enable billing for your Google Cloud project.</a></p></li>
<li><p>1000 when you enable billing for your Google Cloud project.</p>
<p>You can <a href="https://cloud.google.com/support-hub">contact support</a> to request an increase to this limit.</p></li>
</ul></td>
</tr>
<tr class="even">
<td>Maximum sum of the following for an entity:
<ul>
<li>the number of indexed property values</li>
<li>the number of composite index entries</li>
</ul></td>
<td>20,000</td>
</tr>
<tr class="odd">
<td>Maximum number of properties in a composite index</td>
<td>2 MiB</td>
</tr>
<tr class="even">
<td>Maximum total number of both export and import requests for a project allowed per minute</td>
<td>20</td>
</tr>
<tr class="odd">
<td>Maximum number of concurrent exports and imports</td>
<td>50</td>
</tr>
<tr class="even">
<td>Maximum number of entity filters for export and import requests
When the export or import request specifies an <code dir="ltr" translate="no">       entity_filter      </code> , each combination of filtered kind and namespace counts as a separate filter towards this limit. For example:
A request with <code dir="ltr" translate="no">       kinds=['foo', 'bar']      </code> and <code dir="ltr" translate="no">       namespace_ids=['', 'ns1']      </code><br />
results in 4 filters towards this limit: <code dir="ltr" translate="no">       [('', 'foo'), ('', 'bar'), ('ns1', 'foo'), ('ns1', 'bar')]      </code></td>
<td>100</td>
</tr>
<tr class="odd">
<td>Maximum number of time-to-live (TTL) policies allowed per database.</td>
<td>1000</td>
</tr>
</tbody>
</table>

## legacy Cloud Datastore limits

If you have not yet upgraded from Datastore to [Firestore in Datastore mode](/datastore/docs/firestore-or-datastore#cloud_firestore_in_datastore_mode) , the following limits also apply to your database instance:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Limit</th>
<th>Amount</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Maximum number of entity groups that can be accessed in a transaction</td>
<td>25</td>
</tr>
<tr class="even">
<td>Maximum rate of transactions reading from or writing to an entity group</td>
<td><a href="/datastore/docs/concepts/cloud-datastore-transactions#transactions_and_entity_groups">1 per sec</a></td>
</tr>
<tr class="odd">
<td>Maximum write rate to an entity group.
Note you can batch writes together for an entity group. This allows you to write multiple entities to an entity group within this limit.</td>
<td>1 per second</td>
</tr>
</tbody>
</table>

## What's next

  - Learn about [Pricing and Quota](/datastore/docs/pricing)
  - Learn about [Storage Size Calculations](/datastore/docs/concepts/storage-size)
