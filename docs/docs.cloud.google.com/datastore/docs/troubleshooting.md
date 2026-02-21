This page shows you how to resolve issues with Firestore in Datastore mode.

## Latency

The table below describes possible causes of increased latency:

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Latency cause</th>
<th>Types of operations affected</th>
<th>Resolution</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Sustained traffic exceeding the <a href="/datastore/docs/best-practices#ramping_up_traffic">500-50-5 rule</a> .</td>
<td>read, write</td>
<td><p>For rapid traffic increases, Datastore mode attempts to automatically scale to meet the increased demand. When Datastore mode scales, latency begins to decrease.</p>
<p>Hot-spots (high read, write, and delete rates to a narrow entity range) limit the ability of Datastore mode to scale. Review <a href="./best-practices#designing_for_scale">designing for scale</a> and identify hot-spots in your application.</p></td>
</tr>
<tr class="even">
<td>Contention, either from updating a single entity too frequently or from transactions.</td>
<td>read, write</td>
<td><p>Reduce the write rate to individual entities.</p>
<p>Review <a href="/datastore/docs/concepts/transactions#isolation_and_consistency">transaction isolation and consistency</a> and how you use transactions.</p></td>
</tr>
<tr class="odd">
<td>Slow merge-join queries.</td>
<td>read</td>
<td>For example, queries with multiple equality filters ( <code dir="ltr" translate="no">       ==      </code> ) but not backed by composite indexes can result in slow merge-join queries. To improve performance, add composite indexes for these queries, see <a href="/datastore/docs/concepts/optimize-indexes">Optimizing indexes</a> .</td>
</tr>
<tr class="even">
<td>Large reads that return many entities.</td>
<td>read</td>
<td>Use <a href="/datastore/docs/concepts/queries#cursors_limits_and_offsets">query cursors</a> to split large reads.</td>
</tr>
<tr class="odd">
<td>Too many recent deletes.</td>
<td>read<br />
This greatly affects operations that list kinds in a database.</td>
<td>If latency is caused by too many recent deletes, the issue should automatically resolve after some time. If the issue does not resolve, <a href="https://cloud.google.com/support-hub">contact support</a> .</td>
</tr>
<tr class="even">
<td>Index fanout, especially for array properties.</td>
<td>write</td>
<td>Review <a href="/datastore/docs/concepts/indexes#exploding_index">exploding indexes</a> and your usage of array properties.</td>
</tr>
</tbody>
</table>

## Error Codes

This section lists issues that you might encounter and provides suggestions for how to fix each of them.

### DEADLINE\_EXCEEDED

``` text
DEADLINE_EXCEEDED

A deadline was exceeded on the server.
```

To resolve this issue, see the [guide to troubleshooting latency](#latency) .

### ABORTED

The following situations can increase `  ABORTED  ` errors:

  - An entity receiving too many updates per second.
  - Contention from overlapping transactions.
  - Traffic increases that exceed the 500-50-5 rule or encounter hot-spots.

<!-- end list -->

``` text
ABORTED

Too much contention on these datastore entities. Please try again.
```

Or

``` text
ABORTED

Aborted due to cross-transaction contention. This occurs when multiple
transactions attempt to access the same data, requiring Datastore mode
to abort at least one in order to enforce serializability.
```

To resolve this issue:

  - For rapid traffic increases, Datastore mode attempts to automatically scale to meet the increased demand. When Datastore mode scales, latency begins to decrease.
  - Hot-spots limit the ability of Datastore mode to scale up, review [designing for scale](./best-practices#designing_for_scale) to identify hot-spots.
  - Review [data contention in transactions](/datastore/docs/concepts/transactions#isolation_and_consistency) and your usage of transactions.
  - Reduce the write rate to individual entities.

### RESOURCE\_EXHAUSTED

The following situations can lead to `  RESOURCE_EXHAUSTED  ` errors:

You exceeded the [free tier quota](/datastore/pricing#free_quota) and billing is not enabled for your project.

``` text
RESOURCE_EXHAUSTED

Some resource has been exhausted, perhaps a per-user quota, or perhaps the entire file system is out of space.
```

To resolve this issue:

  - Wait for the daily reset of your free tier quota or [enable billing for your project](/billing/docs/how-to/modify-project#enable_billing_for_a_project) .

### INVALID\_ARGUMENT

The following situations can cause `  INVALID_ARGUMENT  ` errors:

  - Attempting to commit an entity with an **indexed** property value greater than 1500 bytes. This limit applies to the UTF-8 encoding of the property value.
  - Attempting to commit an entity with **un-indexed** property values greater than 1,048,487 bytes (1 MiB - 89 bytes). This limit applies to the sum of the property values in an entity. For example, four properties of 256 KiB each exceed the limit.

1,500 bytes (indexed) and 1,048,487 bytes (un-indexed) are [limits](/datastore/docs/concepts/limits) for property values. You cannot exceed these limits and they are not quotas that can be adjusted.

``` text
INVALID_ARGUMENT: The value of property property-name is longer than 1500 bytes
```

or

``` text
INVALID_ARGUMENT: The value of property property_name is longer than 1048487 bytes
```

To resolve this issue:

  - For indexed property values, split the property into multiple properties. If possible, create an un-indexed property and move data that doesn't need to be indexed into the un-indexed property.
  - For un-indexed property values, split the property into multiple properties or implement compression for the property value.
