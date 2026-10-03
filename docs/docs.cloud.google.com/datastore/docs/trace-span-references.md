---
name: documents/docs.cloud.google.com/datastore/docs/trace-span-references
uri: https://docs.cloud.google.com/datastore/docs/trace-span-references
title: Trace span attributes and events
description: A highly-scalable NoSQL database for your web and mobile applications that automatically handles sharding and replication.
data_source: docs.cloud.google.com
---

[Client-side traces](https://docs.cloud.google.com/datastore/docs/client-side-traces) , which are collected by executing RPCs, provide several pieces of information for every request from a client, including spans with timestamps of when the client sent the RPC request and when the client received the RPC response. The spans include latency introduced by the network and client system.

Client-side traces can include the following information:

## Span metadata

|                |                                                 |
|----------------|-------------------------------------------------|
| Span ID        | Unique ID of this span                          |
| Parent Span ID | ID of the parent span, not set for root span    |
| Project ID     | Google Cloud project ID that ingested the trace |
| Start Time     | Span start time                                 |
| End Time       | Span end time                                   |

## Span attributes

| **Client Version**                                          |                                                                     |
|-------------------------------------------------------------|---------------------------------------------------------------------|
| otel.scope.version                                          | String                                                              |
| **Client Environment**                                      |                                                                     |
| gcp.datastore.memory_utilization                            | double (percentage)                                                 |
| **Client Connection Properties**                            |                                                                     |
| gcp.datastore.settings.channel.needs_credentials            | boolean                                                             |
| gcp.datastore.settings.channel.needs_endpoint               | boolean                                                             |
| gcp.datastore.settings.channel.needs_headers                | boolean                                                             |
| gcp.datastore.settings.channel.should_auto_close            | boolean                                                             |
| gcp.datastore.settings.channel.transport_name               | string Ex. "grpc"                                                   |
| gcp.datastore.settings.credentials.authentication_type      | string Ex. "OAuth2"                                                 |
| gcp.datastore.settings.host                                 | string Ex. "datastore.googleapis.com:443"                           |
| **Database Properties**                                     |                                                                     |
| gcp.datastore.settings.project_id                           | string Google Cloud project ID that contains the Datastore database |
| gcp.datastore.settings.database_id                          | string Database external ID (name)                                  |
| **Client RPC Retry Settings**                               |                                                                     |
| gcp.datastore.settings.retrySettings.initial_retry_delay    | string Duration in seconds Ex. 0.01s                                |
| gcp.datastore.settings.retrySettings.initial_rpc_timeout    |                                                                     |
| gcp.datastore.settings.retrySettings.max_attempts           | integer (count)                                                     |
| gcp.datastore.settings.retrySettings.max_retry_delay        | string Duration in seconds Ex. 0.1s                                 |
| gcp.datastore.settings.retrySettings.max_rpc_timeout        |                                                                     |
| gcp.datastore.settings.retrySettings.retry_delay_multiplier | double                                                              |
| gcp.datastore.settings.retrySettings.rpc_timeout_multiplier | double                                                              |
| gcp.datastore.settings.retrySettings.total_timeout          | string Duration in seconds                                          |
| **OpenTelemetry Configuration**                             |                                                                     |
| otel.scope.name                                             | string Ex. "com.google.cloud.datastore"                             |
| service.name                                                | Sparky                                                              |
| telemetry.sdk.language                                      | string Ex. "java"                                                   |
| telemetry.sdk.name                                          | opentelemetry                                                       |
| telemetry.sdk.version                                       | Ex. 1.29.0                                                          |

## Logs and events

Client-side traces provide the following logs and events.

### Lookup events

| **Event:** **"Lookup complete"** **"Transaction.Lookup complete"** |         |
|--------------------------------------------------------------------|---------|
| Received                                                           | Integer |
| Missing                                                            | Integer |
| Deferred                                                           | Integer |
| transactional                                                      | Boolean |
| transaction_id                                                     | String  |

### Commit Events

| **Event:** **"Commit complete"** **"Transaction.Commit complete"** |         |
|--------------------------------------------------------------------|---------|
| doc_count                                                          | Integer |
| transactional                                                      | Boolean |
| transaction_id                                                     | String  |

### RunQuery Events

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Event:</strong><br />
<strong>"RunQuery complete"</strong><br />
<strong>"Transaction.RunQuery complete"</strong></th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>doc_count</td>
<td>Integer</td>
</tr>
<tr class="even">
<td>transactional</td>
<td>Boolean</td>
</tr>
<tr class="odd">
<td>transaction_id</td>
<td>String</td>
</tr>
<tr class="even">
<td>read_conistencey</td>
<td><code>STRONG</code> or <code>EVENTUAL</code></td>
</tr>
<tr class="odd">
<td>more_results</td>
<td>One of:
<ul>
<li><code>NOT_FINISHED</code></li>
<li><code>MORE_RESULTS_AFTER_LIMIT</code></li>
<li><code>MORE_RESULTS_AFTER_CURSOR</code></li>
<li><code>NO_MORE_RESULTS</code></li>
</ul></td>
</tr>
</tbody>
</table>

## What's next

- [Learn how to configure client-side traces](https://docs.cloud.google.com/datastore/docs/client-side-traces)
