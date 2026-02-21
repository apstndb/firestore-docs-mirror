**Preview**

This product or feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](/terms/service-terms#1) . Pre-GA products and features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

The following values are returned as results to operations performed with [Query Explain](/datastore/docs/query-explain-analyze) .

**Note:** The Query Explain is designed for useful ad hoc analysis; its report format will evolve to maximize ease of reading and understanding, not suitability for machine processing. The returned metrics are expected to change as Datastore mode evolves (metrics may be added, removed, or updated) and are not covered by the same deprecation policy as other Firestore APIs. See the tables below for more information about stability

## Plan records

<table>
<thead>
<tr class="header">
<th>Key</th>
<th>Type</th>
<th>Subject to change?</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>indexes_used</td>
<td>List of <a href="https://protobuf.dev/reference/protobuf/google.protobuf/#struct">Generic Structs</a></td>
<td>Yes, the contents in the Struct response are subject to change.</td>
<td>List of indexes selected for this query. See <a href="#query-analyze-reference-indexes-used">below</a> .</td>
</tr>
</tbody>
</table>

### Indexes used

The contents of indexes used are subject to change as Datastore mode evolves.

<table>
<thead>
<tr class="header">
<th>Key</th>
<th>Type</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>query_scope</td>
<td>String</td>
<td>The scope at which a query is run. For example <code dir="ltr" translate="no">       Collection      </code> , <code dir="ltr" translate="no">       Collection Group      </code> and <code dir="ltr" translate="no">       Includes Ancestors      </code> .</td>
</tr>
<tr class="even">
<td>properties</td>
<td>String</td>
<td>The index fields in a format, for example <code dir="ltr" translate="no">       (age ASC, __name__ ASC)      </code> .</td>
</tr>
</tbody>
</table>

## Execution statistics

Aggregated execution statistics for the query.

<table>
<thead>
<tr class="header">
<th>Key</th>
<th>Type</th>
<th>Field subject to change?</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>results_returned</td>
<td>long</td>
<td>No</td>
<td>Total number of results returned, including entities, projections, aggregation results, keys.</td>
</tr>
<tr class="even">
<td>execution_duration</td>
<td>Duration</td>
<td>No</td>
<td>Total time to execute the query in the backend.</td>
</tr>
<tr class="odd">
<td>read_operations</td>
<td>long</td>
<td>No</td>
<td>Total billable read operations.</td>
</tr>
<tr class="even">
<td>debug_stats</td>
<td>Generic Struct</td>
<td>Yes, the contents in the Struct response are subject to change.</td>
<td>Debugging statistics from the execution of the query. See <a href="#query-analyze-reference-debug-stats">below</a> .</td>
</tr>
</tbody>
</table>

### Debug statistics

The following results are helpful for debugging use cases and analysis of raw, optional statistics.

The contents of debug stats are subject to change as Datastore mode evolves.

<table>
<thead>
<tr class="header">
<th>Key</th>
<th>Type</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>index_entries_scanned</td>
<td>String</td>
<td>Total number of index entries inspected during the query.</td>
</tr>
<tr class="even">
<td>documents_scanned</td>
<td>String</td>
<td>Total number of documents scanned during the query.</td>
</tr>
<tr class="odd">
<td>billing_details</td>
<td>Generic Struct</td>
<td>Billing details including metrics like: "documents_billable", "index_entries_billable", "min_query_cost".</td>
</tr>
</tbody>
</table>

## What's next

  - [Learn more about running queries with explain and analyze](/datastore/docs/query-explain-analyze)
  - [Learn more about optimizing queries and indexes](/datastore/docs/concepts/optimize-indexes)
