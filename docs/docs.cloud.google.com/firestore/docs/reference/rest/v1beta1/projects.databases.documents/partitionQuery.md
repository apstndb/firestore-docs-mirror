---
name: documents/docs.cloud.google.com/firestore/docs/reference/rest/v1beta1/projects.databases.documents/partitionQuery
uri: https://docs.cloud.google.com/firestore/docs/reference/rest/v1beta1/projects.databases.documents/partitionQuery
title: 'Method: projects.databases.documents.partitionQuery'
description: A cloud-hosted NoSQL database that's simple enough for rapid prototyping yet scalable and flexible enough to grow to any size.
data_source: docs.cloud.google.com
---

Partitions a query by returning partition cursors that can be used to run the query in parallel. The returned partition cursors are split points that can be used by documents.runQuery as starting/end points for the query results.

### HTTP request

Choose a location:

  
`POST https://firestore.googleapis.com/v1beta1/{parent=projects/*/databases/*/documents}:partitionQuery`

The URLs use [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

| Parameters |                                                                                                                                                                                                                 |
|------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `parent`   | `string` Required. The parent resource name. In the format: `projects/{projectId}/databases/{databaseId}/documents` . Document resource names are not supported; only database resource names can be specified. |

### Request body

The request body contains data with the following structure:

**JSON representation**

```
{
  "partitionCount": string,
  "pageToken": string,
  "pageSize": integer,

  // Union field query_type can be only one of the following:
  "structuredQuery": {
    object (StructuredQuery)
  }
  // End of list of possible types for union field query_type.

  // Union field consistency_selector can be only one of the following:
  "readTime": string
  // End of list of possible types for union field consistency_selector.
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
<td><code>partitionCount</code></td>
<td><p><code>string ( </code><a href="https://developers.google.com/discovery/v1/type-format"><code>int64</code></a><code> format)</code></p>
<p>The desired maximum number of partition points. The partitions may be returned across multiple pages of results. The number must be positive. The actual number of partitions returned may be fewer.</p>
<p>For example, this may be set to one fewer than the number of parallel queries to be run, or in running a data pipeline job, one fewer than the number of workers or compute instances available.</p></td>
</tr>
<tr class="even">
<td><code>pageToken</code></td>
<td><p><code>string</code></p>
<p>The <code>nextPageToken</code> value returned from a previous call to documents.partitionQuery that may be used to get an additional set of results. There are no ordering guarantees between sets of results. Thus, using multiple sets of results will require merging the different result sets.</p>
<p>For example, two subsequent calls using a pageToken may return:</p>
<ul>
<li>cursor B, cursor M, cursor Q</li>
<li>cursor A, cursor U, cursor W</li>
</ul>
<p>To obtain a complete result set ordered with respect to the results of the query supplied to documents.partitionQuery, the results sets should be merged: cursor A, cursor B, cursor M, cursor Q, cursor U, cursor W</p></td>
</tr>
<tr class="odd">
<td><code>pageSize</code></td>
<td><p><code>integer</code></p>
<p>The maximum number of partitions to return in this call, subject to <code>partitionCount</code> .</p>
<p>For example, if <code>partitionCount</code> = 10 and <code>pageSize</code> = 8, the first call to documents.partitionQuery will return up to 8 partitions and a <code>nextPageToken</code> if more results exist. A second call to documents.partitionQuery will return up to 2 partitions, to complete the total of 10 specified in <code>partitionCount</code> .</p></td>
</tr>
<tr class="even">
<td>Union field <code>query_type</code> . The query to partition. <code>query_type</code> can be only one of the following:</td>
<td></td>
</tr>
<tr class="odd">
<td><code>structuredQuery</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/firestore/docs/reference/rest/v1beta1/StructuredQuery"><code>StructuredQuery</code></a><code> )</code></p>
<p>A structured query. Query must specify collection with all descendants and be ordered by name ascending. Other filters, order bys, limits, offsets, and start/end cursors are not supported.</p></td>
</tr>
<tr class="even">
<td>Union field <code>consistency_selector</code> . The consistency mode for this request. If not set, defaults to strong consistency. <code>consistency_selector</code> can be only one of the following:</td>
<td></td>
</tr>
<tr class="odd">
<td><code>readTime</code></td>
<td><p><code>string ( </code><a href="https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp"><code>Timestamp</code></a><code> format)</code></p>
<p>Reads documents as they were at the given time.</p>
<p>This must be a microsecond precision timestamp within the past one hour, or if Point-in-Time Recovery is enabled, can additionally be a whole minute timestamp within the past 7 days.</p>
<p>Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: <code>"2014-10-02T15:01:23Z"</code> , <code>"2014-10-02T15:01:23.045123456Z"</code> or <code>"2014-10-02T15:01:23+05:30"</code> .</p></td>
</tr>
</tbody>
</table>

### Response body

The response for [`Firestore.PartitionQuery`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1beta1/projects.databases.documents/partitionQuery#google.firestore.v1beta1.Firestore.PartitionQuery) .

If successful, the response body contains data with the following structure:

**JSON representation**

```
{
  "partitions": [
    {
      object (Cursor)
    }
  ],
  "nextPageToken": string
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
<td><code>partitions[]</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/firestore/docs/reference/rest/v1beta1/Cursor"><code>Cursor</code></a><code> )</code></p>
<p>Partition results. Each partition is a split point that can be used by documents.runQuery as a starting or end point for the query results. The documents.runQuery requests must be made with the same query supplied to this documents.partitionQuery request. The partition cursors will be ordered according to same ordering as the results of the query supplied to documents.partitionQuery.</p>
<p>For example, if a documents.partitionQuery request returns partition cursors A and B, running the following three queries will return the entire result set of the original query:</p>
<ul>
<li>query, endAt A</li>
<li>query, startAt A, endAt B</li>
<li>query, startAt B</li>
</ul>
<p>An empty result may indicate that the query has too few results to be partitioned, or that the query is not yet supported for partitioning.</p></td>
</tr>
<tr class="even">
<td><code>nextPageToken</code></td>
<td><p><code>string</code></p>
<p>A page token that may be used to request an additional set of results, up to the number specified by <code>partitionCount</code> in the documents.partitionQuery request. If blank, there are no more results.</p></td>
</tr>
</tbody>
</table>

### Authorization scopes

Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/datastore`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .
