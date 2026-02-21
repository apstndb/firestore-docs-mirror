[Client-side traces](/datastore/docs/client-side-traces) , which are collected by executing RPCs, provide several pieces of information for every request from a client, including spans with timestamps of when the client sent the RPC request and when the client received the RPC response. The spans include latency introduced by the network and client system.

Client-side traces can include the following information:

## Span metadata

<table>
<tbody>
<tr class="odd">
<td>Span ID</td>
<td>Unique ID of this span</td>
</tr>
<tr class="even">
<td>Parent Span ID</td>
<td>ID of the parent span, not set for root span</td>
</tr>
<tr class="odd">
<td>Project ID</td>
<td>Google Cloud project ID that ingested the trace</td>
</tr>
<tr class="even">
<td>Start Time</td>
<td>Span start time</td>
</tr>
<tr class="odd">
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

gcp.datastore.memory\_utilization

double (percentage)

**Client Connection Properties**

gcp.datastore.settings.channel.needs\_credentials

boolean

gcp.datastore.settings.channel.needs\_endpoint

boolean

gcp.datastore.settings.channel.needs\_headers

boolean

gcp.datastore.settings.channel.should\_auto\_close

boolean

gcp.datastore.settings.channel.transport\_name

string Ex. "grpc"

gcp.datastore.settings.credentials.authentication\_type

string Ex. "OAuth2"

gcp.datastore.settings.host

string Ex. "datastore.googleapis.com:443"

**Database Properties**

gcp.datastore.settings.project\_id

string  
Google Cloud project ID that contains the Datastore database

gcp.datastore.settings.database\_id

string  
Database external ID (name)

**Client RPC Retry Settings**

gcp.datastore.settings.retrySettings.initial\_retry\_delay

string  
Duration in seconds Ex. 0.01s

gcp.datastore.settings.retrySettings.initial\_rpc\_timeout

gcp.datastore.settings.retrySettings.max\_attempts

integer (count)

gcp.datastore.settings.retrySettings.max\_retry\_delay

string  
Duration in seconds Ex. 0.1s

gcp.datastore.settings.retrySettings.max\_rpc\_timeout

gcp.datastore.settings.retrySettings.retry\_delay\_multiplier

double

gcp.datastore.settings.retrySettings.rpc\_timeout\_multiplier

double

gcp.datastore.settings.retrySettings.total\_timeout

string  
Duration in seconds

**OpenTelemetry Configuration**

otel.scope.name

string Ex. "com.google.cloud.datastore"

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

### Lookup events

**Event:**  
**"Lookup complete"**  
**"Transaction.Lookup complete"**

Received

Integer

Missing

Integer

Deferred

Integer

transactional

Boolean

transaction\_id

String

### Commit Events

**Event:**  
**"Commit complete"**  
**"Transaction.Commit complete"**

doc\_count

Integer

transactional

Boolean

transaction\_id

String

### RunQuery Events

**Event:**  
**"RunQuery complete"**  
**"Transaction.RunQuery complete"**

doc\_count

Integer

transactional

Boolean

transaction\_id

String

read\_conistencey

`  STRONG  ` or `  EVENTUAL  `

more\_results

One of:

  - `  NOT_FINISHED  `
  - `  MORE_RESULTS_AFTER_LIMIT  `
  - `  MORE_RESULTS_AFTER_CURSOR  `
  - `  NO_MORE_RESULTS  `

## What's next

  - [Learn how to configure client-side traces](/datastore/docs/client-side-traces)
