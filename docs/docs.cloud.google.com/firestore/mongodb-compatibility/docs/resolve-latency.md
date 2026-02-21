# Resolve latency issues

This page shows you how to resolve latency issues with Firestore with MongoDB compatibility.

## Latency

The following table describes possible causes of increased latency:

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
<td>Sustained, increasing traffic.</td>
<td>read, write</td>
<td><p>For rapid traffic increases, Firestore with MongoDB compatibility attempts to automatically scale to meet the increased demand. When Firestore with MongoDB compatibility scales, latency begins to decrease.</p>
<p>Hot-spots (high read, write, and delete rates to a narrow document range) limit the ability of Firestore with MongoDB compatibility to scale. Review <a href="/firestore/mongodb-compatibility/docs/understand-reads-writes-scale#avoid_hotspots">Avoid hot-spots</a> and identify hot-spots in your application.</p></td>
</tr>
<tr class="even">
<td>Contention, either from updating a single document too frequently or from transactions.</td>
<td>read, write</td>
<td><p>Reduce the write rate to individual documents.</p>
<p>Reduce the number of documents updated in a single write transaction.</p></td>
</tr>
<tr class="odd">
<td>Large reads that return many documents.</td>
<td>read</td>
<td>Use pagination to split large reads.</td>
</tr>
<tr class="even">
<td>Too many recent deletes.</td>
<td>read<br />
This greatly affects operations that list collections in a database.</td>
<td>If latency is caused by too many recent deletes, the issue should automatically resolve after some time. If the issue does not resolve, <a href="https://cloud.google.com/support-hub">contact support</a> .</td>
</tr>
<tr class="odd">
<td>Index fanout, especially for array fields and embedded document fields.</td>
<td>write</td>
<td>Review your indexing of array fields and embedded document fields.</td>
</tr>
<tr class="even">
<td>Large writes.</td>
<td>write</td>
<td><p>Try reducing the number of writes in each operation.</p>
<p>For bulk data entry where you don't require atomicity, use parallelized individual writes.</p></td>
</tr>
</tbody>
</table>
