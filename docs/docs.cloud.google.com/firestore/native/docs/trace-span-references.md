# Trace span attributes and events

**Preview**

This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

[Client-side traces](/firestore/native/docs/client-side-traces) , which are collected by executing RPCs, provide several pieces of information for every request from a client, including spans with timestamps of when the client sent the RPC request and when the client received the RPC response. The spans include latency introduced by the network and client system.

Client-side traces can include the following information:

## Span metadata

<table>
<thead>
<tr class="header">
<th>Span ID</th>
<th>Unique ID of this span</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Parent Span ID</td>
<td>ID of the parent span, not set for root span</td>
</tr>
<tr class="even">
<td>Project ID</td>
<td>Google Cloud project ID that ingested the trace</td>
</tr>
<tr class="odd">
<td>Start Time</td>
<td>Span start time</td>
</tr>
<tr class="even">
<td>End Time</td>
<td>Span end time</td>
</tr>
</tbody>
</table>

## Span attributes

**Client Version**

otel.scope.version

String

**Client Environment**

gcp.firestore.memory\_utilization

double (percentage)

**Client Connection Properties**

gcp.firestore.settings.channel.needs\_credentials

boolean

gcp.firestore.settings.channel.needs\_endpoint

boolean

gcp.firestore.settings.channel.needs\_headers

boolean

gcp.firestore.settings.channel.should\_auto\_close

boolean

gcp.firestore.settings.channel.transport\_name

string Ex. "grpc"

gcp.firestore.settings.credentials.authentication\_type

string Ex. "OAuth2"

gcp.firestore.settings.host

string Ex. "firestore.googleapis.com:443"

**Database Properties**

gcp.firestore.settings.project\_id

string  
Google Cloud project ID that contains the Firestore database

gcp.firestore.settings.database\_id

string  
Database external ID (name)

**Client RPC Retry Settings**

gcp.firestore.settings.retrySettings.initial\_retry\_delay

string  
Duration in seconds Ex. 0.01s

gcp.firestore.settings.retrySettings.initial\_rpc\_timeout

gcp.firestore.settings.retrySettings.max\_attempts

integer (count)

gcp.firestore.settings.retrySettings.max\_retry\_delay

string  
Duration in seconds Ex. 0.1s

gcp.firestore.settings.retrySettings.max\_rpc\_timeout

gcp.firestore.settings.retrySettings.retry\_delay\_multiplier

double

gcp.firestore.settings.retrySettings.rpc\_timeout\_multiplier

double

gcp.firestore.settings.retrySettings.total\_timeout

string  
Duration in seconds

**OpenTelemetry Configuration**

otel.scope.name

string Ex. "com.google.cloud.firestore"

service.name

Sparky

telemetry.sdk.language

string Ex. "java"

telemetry.sdk.name

opentelemetry

telemetry.sdk.version

Ex. 1.29.0

## Logs and events

Client-side traces provide the following logs and events.

### gRPC events

**RPC Properties**

message.id

integer, Ex. 1, 2

message.type

SENT or RECEIVED

### AggregateQuery events

**Event: "RunAggregationQuery Stream Started."**

attempt

Integer greater than or equal to 0 (Ex: 2). 0 for the initial attempt

**Event: "RunAggregationQuery Response Received."**

attempt

Integer greater than or equal to 0 (Ex: 2). 0 for the initial attempt

**Event: "RunAggregationQuery: Retryable Error."**

error.message

string

**Event: "RunAggregationQuery: Error."**

error.message

string

### BatchGetDocuments Events

**Event: "BatchGetDocuments: Start"**

doc\_count

Integer

transactional

boolean

**Event: "BatchGetDocuments: First Response Received"**

// Once every 100 responses are received  
**Event: "BatchGetDocuments: Received 100 responses"**

**Event: "BatchGetDocuments: Completed with ${N} responses"**

response\_count

Integer

### RunQuery Events

**Event: "RunQuery"**

transactional

boolean

retry\_query\_with\_cursor

boolean

**Event: "RunQuery: First Response Received"**

// Once every 100 responses are received  
**Event: "RunQuery: Received 100 documents"**

// Only if/when half-close is performed by the server  
**Event: "RunQuery: Received RunQueryResponse.Done"**

**Event: "RunQuery: Retryable Error."**

error.message

string

**Event: "RunQuery: Error."**

error.message

string

**Event: "RunQuery: Completed."**

response\_count

Integer

### Transaction Events

**Span: "Transaction.Run"**

transaction\_type

string ("READ\_ONLY" or "READ\_WRITE")

attempts\_allowed

Integer

attempts\_remaining

Integer

// Only if/when a transaction is retried  
**Event: "Initiate transaction retry"**

### Commit Events

**Span: "BulkWriter.Commit"**

doc\_count

Integer

**Span: "Batch.Commit"**

doc\_count

Integer

**Span: "Transaction.Commit"**

doc\_count

Integer

### Exceptional Event

**Span Status = ERROR**

exception.message

string

exception.type

string

exception.stacktrace

string
