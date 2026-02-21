# Monitor databases with Cloud Monitoring

This page describes how to use Cloud Monitoring metrics for Firestore with MongoDB compatibility to monitor your database.

## Cloud Monitoring metrics for Firestore with MongoDB compatibility

The following sections give an overview of the metrics available for Firestore with MongoDB compatibility.

### Monitored Resources

A monitored resource in Cloud Monitoring represents a logical or physical entity, such as a virtual machine, a database, or an application. Monitored resources contain a unique set of metrics that can be explored, reported through a dashboard, or used to create alerts. Each resource also has a set of resource labels, which are key-value pairs that hold additional information about the resource. Resource labels are available for all metrics associated with the resource.

Using the [Cloud Monitoring API](https://cloud.google.com/monitoring/api/resources) , Firestore with MongoDB compatibility performance is monitored with the following resource:

<table>
<tbody>
<tr class="odd">
<td><strong>Resources</strong></td>
<td><strong>Description</strong></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       firestore.googleapis.com/Database      </code></td>
<td>Monitored resource type that provides breakdowns for <code dir="ltr" translate="no">       project      </code> , <code dir="ltr" translate="no">       location      </code> , and <code dir="ltr" translate="no">       database_id      </code> .</td>
</tr>
</tbody>
</table>

### Metrics

For a complete list of metrics for Firestore, see [Firestore metrics](https://cloud.google.com/monitoring/api/metrics_gcp_d_h#gcp-firestore) . The following section describes some of the available metrics.

### Service runtime metrics

The [`  serviceruntime  `](https://cloud.google.com/monitoring/api/metrics_gcp_p_z#gcp-serviceruntime) metrics provide a high-level overview of a project's traffic. These metrics are available for most Google Cloud APIs. The [`  consumed_api  `](https://cloud.google.com/monitoring/api/resources#tag_consumed_api) monitored resource type contains these common metrics. These metrics are sampled every 30 minutes resulting in data being smoothed out.

An important resource label for the `  serviceruntime  ` metrics is `  method  ` . This label represents the underlying RPC method called. The SDK method that you call may not necessarily be named the same as the underlying RPC method. The reason is that the SDK provides high-level API abstraction. However, when trying to understand how your application interacts with Firestore, it is important to understand the metrics based on the name of the RPC method.

If you need to know what the underlying RPC method is for a given SDK method, see the [API documentation](https://cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1) .

#### api/request\_latencies

The `  api/request_latencies  ` metric provides latency distributions across all completed requests.

Firestore records metrics from the **Firestore Service** component. Latency metrics include the time that Firestore receives the request to the time that Firestore finishes sending the response, including interactions with the storage layer. Due to this, round-trip latency (rtt) between the client and the Firestore service is not included in these metrics.

### Document operation metrics

Firestore provides read, write, and delete counts. The write metric provides a breakdown between the 'CREATE' and 'UPDATE' operation. These metrics are aligned with CRUD operations.

The following metrics can be used to understand whether your database is read heavy or write heavy, and the rate of new documents versus deleted documents.

  - `  document/delete_ops_count  ` : The number of successful document deletes.
  - `  document/read_ops_count  ` : The number of successful document reads from queries or lookups.
  - `  document/write_ops_count  ` : The number of successful document writes.

**Note:** The `  document/delete_ops_count  ` metric doesn't include documents deleted because of TTL policies. For information about metrics that capture deletes due to TTL policies, see [TTL Metrics](#ttl_metrics) .

### Billing metrics

Use these metrics to understand billing usage. These metrics don't include billing from administrator operations (indexing, import, export, and bulk delete).

  - `  api/billable_read_units  ` : The number of billable read units. Usage can be broken down by service name and API method.
  - `  api/billable_write_units  ` : The number of billable write units. Usage can be broken down by service name and API method.
  - `  document/billable_managed_delete_write_units  ` : The number of billable write units from managed delete services like [TTL](/firestore/mongodb-compatibility/docs/ttl) .

### Index metrics

Index write rates can be contrasted with the `  document/write_ops_count  ` metric to understand index fanout.

  - `  index/write_count  ` : Count of index writes.

### TTL Metrics

The TTL metrics for Firestore with MongoDB compatibility metrics are used to monitor the effect of the [TTL policy](/firestore/mongodb-compatibility/docs/ttl) enforced.

  - `  document/ttl_deletion_count  ` : Total count of documents deleted by TTL services.
  - `  document/ttl_expiration_to_deletion_delays  ` : Time elapsed between when a document with a TTL expired, and when it was actually deleted.

## View predefined dashboards and create custom dashboards

Firestore with MongoDB compatibility supports predefined dashboards that use Cloud Monitoring metrics. You can also create custom dashboards.

### View database usage metrics

Open the usage dashboards in the Google Cloud console to view document reads, writes, and deletes over time.

#### Access control

The usage dashboards require the `  monitoring.timeSeries.list  ` Identity and Access Management (IAM) permission. The Project Owner, Editor, and Viewer roles grant this permission. You can also grant this permission through a [Cloud Monitoring role](https://cloud.google.com/monitoring/access-control#monitoring_2) or a [custom role](https://cloud.google.com/iam/docs/creating-custom-roles) .

#### Database usage dashboard

To view usage metrics for a Firestore with MongoDB compatibility database, do the following.

1.  In the Google Cloud console, go to the **Databases** page.

2.  Select the required database from the list of databases.

3.  In the navigation menu, click **Usage** .

#### Usage dashboard and billing reports

The Firestore usage dashboards in the console provide an estimate of usage. They can help you identify spikes in usage. However, the dashboard is not an exact view of billed operations. Billed usage is likely higher. To monitor billing, see [billing metrics](#billing_metrics) .

In all cases of discrepancy, the billing report takes precedence over the usage dashboard.

Import and export operations cause discrepancies between the usage dashboard and billed usage. Reads and writes performed by these operations don't show up in the usage dashboard.

### View database performance metrics

The **Monitoring** page in the Firestore section of the Google Cloud console includes predefined monitoring dashboards such as **Request Latencies (P50 and P99)** , **Response Codes** , and **Query stats (P50)** . You can also create up to one custom dashboard. To access the **Monitoring** page for a database, follow these steps:

1.  In the Google Cloud console, open the Firestore **Databases** page.

2.  Select a database from the list.

3.  In the navigation menu, click **Monitoring** to open a dashboard.

### Create custom Cloud Monitoring dashboards

In Cloud Monitoring, custom dashboards allow you to display information that is relevant to you in an organized way. For example, you might create a dashboard to display the performance metrics and alerting policies for your project in your production environment.

For more information about setting up a custom dashboard, see [Manage custom dashboard](https://cloud.google.com/monitoring/charts/dashboards) and [Add dashboard widgets](https://cloud.google.com/monitoring/charts) .

### Create an alerting policy

In Cloud Monitoring, you can create [alerts](https://cloud.google.com/monitoring/alerts) to notify you when a change in a metric condition occurs. You can use these alerts to be notified of potential problems before they impact your users.

For more information about creating alerts, see [Create metric-threshold alerting policies](https://cloud.google.com/monitoring/alerts/using-alerting-ui) .

Consider the following example where we create a latency alert policy. The alerting policy checks p99 latency over a 5 minute rolling window. If the p99 latency stays higher than 250ms for 5 minutes, the alert is triggered.

### Console

1.  In the Google Cloud console, go to the **Monitoring** page then select *notifications* **Alerting** .

2.  Select **Create policy** .

3.  Select the **Request Latencies** metric from the **Consumed API** resource.

4.  Add a service filter for `  firestore.googleapis.com  ` for Firestore Native databases.

5.  Click **Next** to configure the trigger.

6.  Select the **Condition Types** as **Threshold** .
    
    A threshold condition is set to a threshold value of 250ms. An alert is triggered when the p99 latency value stays the same for the entire period of the rolling window (5 min).

7.  Set the **Threshold value** as **250** .

8.  Click **Next** to configure notifications.

9.  Set the alert policy name and click **Next** .

10. Review the alert configurations and click **Create Policy** .

### MQL

You can implement the same latency alert policy using a Monitoring Query Language (MQL) query. For more examples of using MQL, see [Sample MQL queries](https://cloud.google.com/monitoring/mql/examples) .

``` text
fetch consumed_api
| metric 'serviceruntime.googleapis.com/api/request_latencies'
| filter (resource.service == 'firestore.googleapis.com')
| group_by 5m,
    [value_request_latencies_percentile:
      percentile(value.request_latencies, 99)]
| every 5m
| condition val() > 0.25 's'
```
