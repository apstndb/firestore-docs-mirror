# Monitor usage

This page describes how you can monitor your Firestore usage and spot potential problems in your app.

## Usage dashboard

Use the usage dashboards in the Google Cloud console and Firebase console to view document reads, writes, and deletes over time.

#### Access control

The usage dashboards require the `  monitoring.timeSeries.list  ` IAM permission. The Project Owner, Editor, and Viewer roles grant this permission. You can also grant this permission through a [Cloud Monitoring role](https://cloud.google.com/monitoring/access-control#monitoring_2) or a [custom role](https://cloud.google.com/iam/docs/creating-custom-roles) .

### Database usage dashboard

To view usage metrics for a Firestore database, open the database **Usage** page in the Google Cloud console.

1.  In the Google Cloud console, go to the **Databases** page.

2.  Select the required database from the list of databases.

3.  In the navigation menu, click **Usage** .

4.  Click the link in the message that appears on the page to view your database usage.

### Aggregated usage dashboard

If your project has multiple Firestore databases, you can view aggregated usage metrics in the Google Cloud console or Firebase console.

### Google Cloud console

In the Google Cloud console, go to the **Project usage** page.

The project usage dashboard shows document operations over time as follows:

### Firebase console

### Usage dashboard and billing reports

The Firestore usage dashboards in the Firebase and Cloud consoles provide an estimate of usage. They can help you identify spikes in usage. However, the dashboard is not an exact view of billed operations. Billed usage is likely higher. In all cases of discrepancy, the billing report takes precedence over the usage dashboard.

Operations that cause discrepancies between the usage dashboard and billed usage include:

  - Import and export operations. Reads and writes performed by these operations do not show up in the usage dashboard.

  - No-op verify-only writes. Writes that only verify the existence or non-existence of a document contribute to billed read operations, but they show as \`UPDATE\_NOOP\` and \`DELETE\_NOOP\` respectively in the write usage dashboard.

  - No-op writes. Operations that do not result in a change to the database, such as an update that does not change field values or a write to a deleted document may show in the usage dashboard as \`UPDATE\_NOOP\` or \`DELETE\_NOOP\`. Even though they show as \`NOOP\`, they still contribute to billed operations.

  - Collapsed writes. In cases with multiple writes to the same document in quick succession, the usage dashboard might collapse multiple writes together and count them as one. When billing usage, each write is still counted separately.
    
    The usage dashboard also collapses writes for field transforms like server timestamps, numeric increments, and array union operations. For field transforms, the usage dashboard might count multiple operations as a single operation.

  - Queries that return zero results. Queries with zero results incur a cost of one read operation. This usage is billed but does not appear in the usage dashboard.

  - Read operations from [index entries read](/firestore/pricing#index-reads) . This usage is billed but does not appear in the usage dashboard. For example, aggregation queries bill for index entries read but this usage does not appear in the usage dashboard.

The usage dashboard for deletes does not capture automatic expiration operations performed by Time-to-live (TTL) policies. Please refer to the TTL metrics from [Cloud Monitoring](#monitoring-metrics) .

## Security rule usage

Additionally, the Firebase console provides a Firebase Security Rules evaluation dashboard, a useful, at-a-glance view of rules invocations. You can also monitor Firebase Security Rules usage through [Cloud Monitoring](https://cloud.google.com/monitoring/api/metrics_gcp#gcp-firestore) . This provides the same rule evaluation metrics, along with the ability to build custom dashboards, analyze trends, and configure alerts (for example, when denied requests spike). See the [Cloud Monitoring metrics reference](https://cloud.google.com/monitoring/api/metrics_gcp#gcp-firestore) for the complete list of available metrics.

## Cloud Monitoring metrics

[Cloud Monitoring](https://cloud.google.com/monitoring/docs/) collects metrics, events, and metadata from Google Cloud products. The usage dashboard in the Firestore console reports the same metrics data. To set up custom dashboards and usage alerts, use Cloud Monitoring.

Cloud Monitoring includes the following Firestore metrics:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Metric Name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Document Reads</td>
<td><p>The number of successful document reads. You can break this metric down by the type of read: LOOKUP or QUERY.</p>
<p>This metric does not include reads from managed export or bulk delete operations.</p></td>
</tr>
<tr class="even">
<td>Document Writes</td>
<td><p>The number of successful document writes. You can break the metric down by the type of write: CREATE or UPDATE.</p>
<p>This metric does not include writes from managed import operations.</p></td>
</tr>
<tr class="odd">
<td>Document Deletes</td>
<td>The number of successful document deletes.</td>
</tr>
<tr class="even">
<td>Active Connections</td>
<td><p>The number of active connections to your database.</p>
<p>Each active <a href="/firestore/docs/reference/libraries#mobile_and_web_sdks">mobile and web SDK</a> maintains a single connection, which can be shared across multiple snapshot listeners. The <a href="/firestore/docs/reference/libraries#server_client_libraries">server client libraries</a> create one connection per snapshot listener.</p></td>
</tr>
<tr class="odd">
<td>Snapshot Listeners</td>
<td><p>The number of snapshot listeners across all active connections.</p></td>
</tr>
<tr class="even">
<td>Time-to-live deletion count</td>
<td><p>Total count of documents deleted by <a href="/firestore/native/docs/ttl">Time-to-live (TTL) policies</a> .</p></td>
</tr>
<tr class="odd">
<td>Time-to-live expiration to deletion delays</td>
<td><p>Time elapsed between when a document expired under a <a href="/firestore/native/docs/ttl">Time-to-live (TTL) policy</a> and when it was actually deleted.</p></td>
</tr>
</tbody>
</table>

**Note:** The preceding list covers only the most commonly used Firestore metrics. Additional metrics, such as latency measurements, index entry reads, and system-level metrics, are also available through Cloud Monitoring. See the [full reference of Firestore metrics](https://cloud.google.com/monitoring/api/metrics_gcp#gcp-firestore) for the complete set.

  - Realtime updates usage  
    Use the active connections and snapshot listeners metrics to measure your usage of [realtime updates](/firestore/native/docs/query-data/listen) .
    
    Let's say a user opens your app on their phone. The app then connects to Firestore and subscribes to 10 queries. This increases your metrics by 1 active connection and 10 snapshot listeners.

  - Sampling rate  
    The Firestore metrics are sampled every minute, but updates may take up to 4 minutes to show up in your dashboards.

### Latency metrics

Backend latency metrics are available through common Google Cloud [firestore](//cloud.google.com//monitoring/api/metrics_gcp_d_h#gcp-firestore) metrics.

For example, a graph of [p50 latency](https://console.cloud.google.com/monitoring/metrics-explorer;duration=P7D?pageState=%7B%22domainObjectDeprecationId%22:%2212ACB359-342F-4174-8878-0B5FCECCB7E6%22,%22xyChart%22:%7B%22constantLines%22:%5B%5D,%22dataSets%22:%5B%7B%22plotType%22:%22LINE%22,%22targetAxis%22:%22Y1%22,%22timeSeriesFilter%22:%7B%22aggregations%22:%5B%7B%22crossSeriesReducer%22:%22REDUCE_PERCENTILE_50%22,%22groupByFields%22:%5B%5D,%22perSeriesAligner%22:%22ALIGN_DELTA%22%7D%5D,%22apiSource%22:%22DEFAULT_CLOUD%22,%22crossSeriesReducer%22:%22REDUCE_PERCENTILE_50%22,%22filter%22:%22metric.type%3D%5C%22firestore.googleapis.com%2Fapi%2Frequest_latencies%5C%22%20resource.type%3D%5C%22firestore.googleapis.com%2FDatabase%5C%22%20metric.label.%5C%22service%5C%22%3D%5C%22firestore.googleapis.com%5C%22%22,%22groupByFields%22:%5B%5D,%22minAlignmentPeriod%22:%2260s%22,%22perSeriesAligner%22:%22ALIGN_DELTA%22%7D%7D%5D,%22options%22:%7B%22mode%22:%22COLOR%22%7D,%22y1Axis%22:%7B%22label%22:%22%22,%22scale%22:%22LINEAR%22%7D%7D%7D) can be found in the Cloud Console's metrics explorer view.

### Set up a Cloud Monitoring dashboard

To view a pre-defined dashboard or to set up a dashboard, see [Use the monitoring dashboard](https://cloud.google.com/firestore/docs/use-monitoring-dashboard) .

## What's next

  - [Learn more about Cloud Monitoring.](https://cloud.google.com/monitoring/docs/)
  - Learn about [best practices for monitoring Firestore performance](https://cloud.google.com/firestore/docs/understand-performance-monitoring) .
