# Use the Cloud Monitoring dashboard

This page describes how to use a Cloud Monitoring dashboard to view available metrics, create a custom dashboard, and set alerts.

## View Firestore metrics

To view the different Firestore metrics and create charts, use one the following:

  - The **Monitoring** page in the Firestore section of the Google Cloud console. This page includes a pre-defined monitoring dashboard. You can also create up to one custom dashboard. To access the **Monitoring** page for a database, follow these steps:
    
    1.  In the Google Cloud console, open the Firestore **Databases** page.
    
    2.  Select a database from the list.
    
    3.  In the navigation menu, click **Monitoring** to open a dashboard.

  - The metrics explorer within Cloud Monitoring in Google Cloud console. For more information about creating charts, see [Create charts with Metrics Explorer](https://cloud.google.com/monitoring/charts/metrics-explorer) .

## View the Cloud Monitoring dashboard

In Cloud Monitoring, custom dashboards allow you to display information that is relevant to you in an organized way. For example, you might create a dashboard to display the performance metrics and alerting policies for your project in your production environment.

For more information about setting up a custom dashboard, see [Manage custom dashboard](https://cloud.google.com/monitoring/charts/dashboards) and [Add dashboard widgets](https://cloud.google.com/monitoring/charts) .

#### Monitor error rates

You can create a monitoring dashboard to monitor error rates and ensure availability of your database. Availability refers to the rate at which your database responds within an expected timeframe with a successful status code. The [Firestore SLA](https://cloud.google.com/firestore/sla) defines the specific details of what is classified as a valid request.

The error rate is determined by dividing the number of requests that resulted in an error response by the total number of requests sent.

An example dashboard for calculating error rates can be created by calculating the A/B ratio for `  api/request_count  ` of valid requests with `  4xx  ` or `  5xx  ` error codes contrasted with the `  api/request_count  ` of all valid requests.

**Figure 1.** Understand availability with error rate.

In figure 1, you can see how to visualize the error rate ratio using the **api/request\_count** metrics in the Metrics explorer.

## Create an alerting policy

Cloud Monitoring allows you to create [alerts](https://cloud.google.com/monitoring/alerts) to notify you when a change in a metric condition occurs. You can use these alerts to be notified of potential problems before they impact your users.

For more information about creating alerts, see [Create metric-threshold alerting policies](https://cloud.google.com/monitoring/alerts/using-alerting-ui) .

Consider the following example where we create a latency alert policy. The alerting policy checks p99 latency over a 5 minute rolling window. If the p99 latency stays above 250ms for 5 minutes, the alert is triggered.

### Console

1.  In the Google Cloud console, go to the **Monitoring** page then select *notifications* **Alerting** .

2.  Select **Create policy** .

3.  Select the **Request Latencies** metric from the **Consumed API** resource.

4.  Add a service filter for `  firestore.googleapis.com  ` for Firestore in Native mode databases.

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
