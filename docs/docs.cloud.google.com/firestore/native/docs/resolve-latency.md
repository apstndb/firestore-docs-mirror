# Resolve latency issues

This page shows you how to resolve latency issues with Firestore.

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
<td>Sustained traffic exceeding the <a href="/firestore/native/docs/best-practices#ramping_up_traffic">500-50-5 rule</a> .</td>
<td>read, write</td>
<td><p>For rapid traffic increases, Firestore attempts to automatically scale to meet the increased demand. When Firestore scales, latency begins to decrease.</p>
<p>Hot-spots (high read, write, and delete rates to a narrow document range) limit the ability of Firestore to scale. Review <a href="./best-practices#designing_for_scale">designing for scale</a> and identify hot-spots in your application.</p></td>
</tr>
<tr class="even">
<td>Contention, either from updating a single document too frequently or from transactions.</td>
<td>read, write</td>
<td><p>Reduce the write rate to individual documents.</p>
<p>Review <a href="/firestore/native/docs/transaction-data-contention">data contention in transactions</a> and how you use transactions.</p></td>
</tr>
<tr class="odd">
<td>Slow merge-join queries.</td>
<td>read</td>
<td>For example, queries with multiple equality filters ( <code dir="ltr" translate="no">       ==      </code> ) but not backed by composite indexes can result in slow merge-join queries. To improve performance, add composite indexes for these queries, see Reason #3 in <a href="https://firebase.googleblog.com/2019/08/why-is-my-cloud-firestore-query-slow.html">Why is my Firestore query slow?</a></td>
</tr>
<tr class="even">
<td>Large reads that return many documents.</td>
<td>read</td>
<td>Use <a href="/firestore/docs/query-data/query-cursors">pagination</a> to split large reads.</td>
</tr>
<tr class="odd">
<td>Too many recent deletes.</td>
<td>read<br />
This greatly affects operations that list collections in a database.</td>
<td>If latency is caused by too many recent deletes, the issue should automatically resolve after some time. If the issue does not resolve, <a href="https://cloud.google.com/support-hub">contact support</a> .</td>
</tr>
<tr class="even">
<td>Adding and removing listeners too quickly.</td>
<td>realtime listener queries</td>
<td>See the <a href="/firestore/native/docs/real-time_queries_at_scale">best practices for realtime updates.</a></td>
</tr>
<tr class="odd">
<td>Listening to large documents or to a query with many results.</td>
<td>realtime listener queries</td>
<td>See the <a href="/firestore/native/docs/real-time_queries_at_scale">best practices for realtime updates</a></td>
</tr>
<tr class="even">
<td>Index fanout, especially for array fields and map fields.</td>
<td>write</td>
<td>Review your usage of array fields and map fields. For map fields, you can disable subfields from indexing. You can also use <a href="/firestore/docs/query-data/indexing#add_a_collection-level_exemption">collection level exemptions</a> .</td>
</tr>
<tr class="odd">
<td>Large writes and batched writes.</td>
<td>write</td>
<td><p>Try reducing the number of writes in each batched write. Batched writes are atomic and many writes in a single batch can increase latency and contention. For example, a batch of 10 writes performs better than a batch of 500 writes.</p>
<p>For bulk data entry where you don't require atomicity, use a <a href="/firestore/docs/reference/libraries#server_client_libraries">server client library</a> with parallelized individual writes. Batched writes perform better than serialized writes but not better than parallel writes.</p></td>
</tr>
</tbody>
</table>
