---
name: documents/docs.cloud.google.com/firestore/native/docs/trace-span-references
uri: https://docs.cloud.google.com/firestore/native/docs/trace-span-references
title: Trace span attributes and events
description: A cloud-hosted NoSQL database that's simple enough for rapid prototyping yet scalable and flexible enough to grow to any size.
data_source: docs.cloud.google.com
---

# Trace span attributes and events

> **Preview**
>
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

[Client-side traces](https://docs.cloud.google.com/firestore/native/docs/client-side-traces) , which are collected by executing RPCs, provide several pieces of information for every request from a client, including spans with timestamps of when the client sent the RPC request and when the client received the RPC response. The spans include latency introduced by the network and client system.

Client-side traces can include the following information:

## Span metadata

| Span ID        | Unique ID of this span                          |
|----------------|-------------------------------------------------|
| Parent Span ID | ID of the parent span, not set for root span    |
| Project ID     | Google Cloud project ID that ingested the trace |
| Start Time     | Span start time                                 |
| End Time       | Span end time                                   |

## Span attributes

| **Client Version**                                          |                                                                     |
|-------------------------------------------------------------|---------------------------------------------------------------------|
| otel.scope.version                                          | String                                                              |
| **Client Environment**                                      |                                                                     |
| gcp.firestore.memory_utilization                            | double (percentage)                                                 |
| **Client Connection Properties**                            |                                                                     |
| gcp.firestore.settings.channel.needs_credentials            | boolean                                                             |
| gcp.firestore.settings.channel.needs_endpoint               | boolean                                                             |
| gcp.firestore.settings.channel.needs_headers                | boolean                                                             |
| gcp.firestore.settings.channel.should_auto_close            | boolean                                                             |
| gcp.firestore.settings.channel.transport_name               | string Ex. "grpc"                                                   |
| gcp.firestore.settings.credentials.authentication_type      | string Ex. "OAuth2"                                                 |
| gcp.firestore.settings.host                                 | string Ex. "firestore.googleapis.com:443"                           |
| **Database Properties**                                     |                                                                     |
| gcp.firestore.settings.project_id                           | string Google Cloud project ID that contains the Firestore database |
| gcp.firestore.settings.database_id                          | string Database external ID (name)                                  |
| **Client RPC Retry Settings**                               |                                                                     |
| gcp.firestore.settings.retrySettings.initial_retry_delay    | string Duration in seconds Ex. 0.01s                                |
| gcp.firestore.settings.retrySettings.initial_rpc_timeout    |                                                                     |
| gcp.firestore.settings.retrySettings.max_attempts           | integer (count)                                                     |
| gcp.firestore.settings.retrySettings.max_retry_delay        | string Duration in seconds Ex. 0.1s                                 |
| gcp.firestore.settings.retrySettings.max_rpc_timeout        |                                                                     |
| gcp.firestore.settings.retrySettings.retry_delay_multiplier | double                                                              |
| gcp.firestore.settings.retrySettings.rpc_timeout_multiplier | double                                                              |
| gcp.firestore.settings.retrySettings.total_timeout          | string Duration in seconds                                          |
| **OpenTelemetry Configuration**                             |                                                                     |
| otel.scope.name                                             | string Ex. "com.google.cloud.firestore"                             |
| service.name                                                | Sparky                                                              |
| telemetry.sdk.language                                      | string Ex. "java"                                                   |
| telemetry.sdk.name                                          | opentelemetry                                                       |
| telemetry.sdk.version                                       | Ex. 1.29.0                                                          |

## Logs and events

Client-side traces provide the following logs and events.

### gRPC events

| **RPC Properties** |                   |
|--------------------|-------------------|
| message.id         | integer, Ex. 1, 2 |
| message.type       | SENT or RECEIVED  |

### AggregateQuery events

| **Event: "RunAggregationQuery Stream Started."** |                                                                       |
|--------------------------------------------------|-----------------------------------------------------------------------|
| attempt                                          | Integer greater than or equal to 0 (Ex: 2). 0 for the initial attempt |

| **Event: "RunAggregationQuery Response Received."** |                                                                       |
|-----------------------------------------------------|-----------------------------------------------------------------------|
| attempt                                             | Integer greater than or equal to 0 (Ex: 2). 0 for the initial attempt |

| **Event: "RunAggregationQuery: Retryable Error."** |        |
|----------------------------------------------------|--------|
| error.message                                      | string |

| **Event: "RunAggregationQuery: Error."** |        |
|------------------------------------------|--------|
| error.message                            | string |

### BatchGetDocuments Events

| **Event: "BatchGetDocuments: Start"** |         |
|---------------------------------------|---------|
| doc_count                             | Integer |
| transactional                         | boolean |

| **Event: "BatchGetDocuments: First Response Received"** |
|---------------------------------------------------------|

| // Once every 100 responses are received **Event: "BatchGetDocuments: Received 100 responses"** |
|-------------------------------------------------------------------------------------------------|

| **Event: "BatchGetDocuments: Completed with \${N} responses"** |         |
|----------------------------------------------------------------|---------|
| response_count                                                 | Integer |

### RunQuery Events

| **Event: "RunQuery"**   |         |
|-------------------------|---------|
| transactional           | boolean |
| retry_query_with_cursor | boolean |

| **Event: "RunQuery: First Response Received"** |
|------------------------------------------------|

| // Once every 100 responses are received **Event: "RunQuery: Received 100 documents"** |
|----------------------------------------------------------------------------------------|

| // Only if/when half-close is performed by the server **Event: "RunQuery: Received RunQueryResponse.Done"** |
|-------------------------------------------------------------------------------------------------------------|

| **Event: "RunQuery: Retryable Error."** |        |
|-----------------------------------------|--------|
| error.message                           | string |

| **Event: "RunQuery: Error."** |        |
|-------------------------------|--------|
| error.message                 | string |

| **Event: "RunQuery: Completed."** |         |
|-----------------------------------|---------|
| response_count                    | Integer |

### Transaction Events

| **Span: "Transaction.Run"** |                                      |
|-----------------------------|--------------------------------------|
| transaction_type            | string ("READ_ONLY" or "READ_WRITE") |
| attempts_allowed            | Integer                              |
| attempts_remaining          | Integer                              |

| // Only if/when a transaction is retried **Event: "Initiate transaction retry"** |
|----------------------------------------------------------------------------------|

### Commit Events

| **Span: "BulkWriter.Commit"** |         |
|-------------------------------|---------|
| doc_count                     | Integer |

| **Span: "Batch.Commit"** |         |
|--------------------------|---------|
| doc_count                | Integer |

| **Span: "Transaction.Commit"** |         |
|--------------------------------|---------|
| doc_count                      | Integer |

### Exceptional Event

| **Span Status = ERROR** |        |
|-------------------------|--------|
| exception.message       | string |
| exception.type          | string |
| exception.stacktrace    | string |
