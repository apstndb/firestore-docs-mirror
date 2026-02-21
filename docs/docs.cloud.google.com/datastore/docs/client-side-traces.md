**Preview**

This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

To monitor and debug Firestore in Datastore mode (Datastore) requests end-to-end, you can enable traces in the Java client library. Client-side tracing can provide a signal about the performance as experienced by your application, as well as insights that can help with debugging issues.

Client-side traces, which are collected by executing RPCs from the client, provide the following information:

  - Spans with timestamps of when the client sent the RPC request and when the client received the RPC response, including latency introduced by the network and client system
  - Attributes (key-value pairs) that surface information about the client and its configuration.
  - Logs associated with key events in the spans.
  - Stack traces if a crash occurs on the client.

## OpenTelemetry

Traces for the Java client library are instrumented using [OpenTelemetry](https://opentelemetry.io/docs/what-is-opentelemetry/) APIs. OpenTelemetry is an industry standard, open-source observability framework. OpenTelemetry offers a wide range of tools such as instrumentation APIs and SDKs, collectors, backend-specific exporters and flexible configuration options such as sampling controls, span limits, and more.

### Export traces with exporters and collectors

As part of your configurations, you can export your traces to an observability backend. Most observability service providers offer exporters for you to use, such as [Cloud Trace](https://github.com/GoogleCloudPlatform/opentelemetry-operations-java/tree/main/exporters/trace) .

In addition to an exporter, OpenTelemetry recommends setting up a [Collector](https://opentelemetry.io/docs/collector/) . A Collector lets your service offload data quickly and lets the collector take care of additional handling like retries, batching, and encryption. A Collector runs alongside your application. The collector receives OpenTelemetry protocol (OTLP) messages, processes the messages, and exports them to your observability backend.

## Limitations

Traces spans are available only for the Java client library.

## Billing

In addition to Datastore usage, client-side tracing can incur charges.

There are no charges for collecting traces or usage of the OpenTelemetry framework.

Ingestion of trace spans into your observability backend may be billable. For example, if you use Cloud Trace as your backend, you are billed according to [Cloud Trace pricing](https://cloud.google.com/stackdriver/pricing#trace-costs) . If you use another observability service provider, find out their billing model and associated costs.

To better understand billing, start with a small trace sampling ratio (trace a small percentage of your RPCs) based on your traffic.

## Before you begin

Before you begin:

  - Make sure you set up the service account under which your app writes traces to your observability backend with the necessary [Identity and Access Management roles](/trace/docs/iam) :
    
    <table>
    <thead>
    <tr class="header">
    <th>Trace operation</th>
    <th>IAM role</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Read traces</td>
    <td><code dir="ltr" translate="no">         roles/cloudtrace.user        </code></td>
    </tr>
    <tr class="even">
    <td>Write traces</td>
    <td><code dir="ltr" translate="no">         roles/cloudtrace.agent        </code></td>
    </tr>
    <tr class="odd">
    <td>Read/write traces</td>
    <td><code dir="ltr" translate="no">         roles/cloudtrace.admin        </code></td>
    </tr>
    </tbody>
    </table>

  - Verify Trace API is enabled on this project.

## Configure client-side traces

This section provides example configurations for client-side traces. You can export to a Collector or directly to an observability backend. You also have the following options for configuring client-side traces:

  - You can configure traces with the OpenTelemetry APIs. This requires code changes to your application. See the following examples:
      - [Export to a Collector with OpenTelemetry APIs](#export_to_collector)
      - [Export directly to an observability backend with OpenTelemetry APIs](#export_to_backend)
  - You can configure traces without code changes using auto agents. You need to set the environment variable `  DATASTORE_ENABLE_TRACING=ON  ` . You also need to set other configuration settings as described in [Agent Configuration](https://opentelemetry.io/docs/languages/java/automatic/configuration/) . See the following examples:
      - [Export to a Collector with Auto Agents](#export_to_collector_auto_agent)
      - [Export directly to an observability backend with Auto Agents](#export_to_backend_auto_agent)

### Export traces to a Collector with OpenTelemetry APIs

The following code configures the Datastore Java client library to export spans with a 10% sampling ratio to an OpenTelemetry Collector.

##### Java

``` text
Resource resource = Resource
  .getDefault().merge(Resource.builder().put(SERVICE_NAME, "My App").build());

OtlpGrpcSpanExporter otlpGrpcSpanExporter =
  OtlpGrpcSpanExporter
  .builder()
  .setEndpoint("http://localhost:4317") // Replace with your OTLP endpoint
  .build();

// Using a batch span processor
// You can use `.setScheduleDelay()`, `.setExporterTimeout()`,
// `.setMaxQueueSize`(), and `.setMaxExportBatchSize()` to further customize.
BatchSpanProcessor otlpGrpcSpanProcessor =
  BatchSpanProcessor.builder(otlpGrpcSpanExporter).build();

// Export to a collector that is expecting OTLP using gRPC.
OpenTelemetrySdk otel = OpenTelemetrySdk.builder()
        .setTracerProvider(SdkTracerProvider.builder()
            .setResource(resource)
            .addSpanProcessor(otlpGrpcSpanProcessor)
            .setSampler(Sampler.traceIdRatioBased(0.1))
            .build())
        .build();


DatastoreOptions datastoreOptions = DatastoreOptions
  .newBuilder()
  .setOpenTelemetryOptions(
    DatastoreOpenTelemetryOptions.newBuilder()
      .setTracingEnabled(true)
      .setOpenTelemetry(otel)
      .build())
  .build();

Datastore datastore = datastoreOptions.getService();

    
```

### Export directly to an observability backend with OpenTelemetry APIs

The following code configures the Java client library to directly export trace spans to Cloud Trace with a 10% trace sampling ratio. You can use other observability service providers' exporters to directly export to their backend. If your observability backend supports OTLP ingestion, you can use OpenTelemetry `  OtlpGrpcSpanExporter  ` to export to your backend rather than using a custom exporter.

##### Java

``` text
// TraceExporter needed for this use case
import com.google.cloud.opentelemetry.trace.TraceExporter;

Resource resource = Resource
  .getDefault().merge(Resource.builder().put(SERVICE_NAME, "My App").build());
SpanExporter gcpTraceExporter = TraceExporter.createWithDefaultConfiguration();

// Using a batch span processor
// You can use `.setScheduleDelay()`, `.setExporterTimeout()`,
// `.setMaxQueueSize`(), and `.setMaxExportBatchSize()` to further customize.
SpanProcessor gcpBatchSpanProcessor =
  BatchSpanProcessor.builder(gcpTraceExporter).build();

// Export directly to Cloud Trace with 10% trace sampling ratio
OpenTelemetrySdk otel = OpenTelemetrySdk.builder()
        .setTracerProvider(SdkTracerProvider.builder()
            .setResource(resource)
            .addSpanProcessor(gcpBatchSpanProcessor)
            .setSampler(Sampler.traceIdRatioBased(0.1))
            .build())
        .build();


DatastoreOptions datastoreOptions = DatastoreOptions
  .newBuilder()
  .setOpenTelemetryOptions(
    DatastoreOpenTelemetryOptions.newBuilder()
      .setTracingEnabled(true)
      .setOpenTelemetry(otel)
      .build())
  .build();

Datastore datastore = datastoreOptions.getService();

    
```

### Export to a Collector with Auto Agents

Run your OpenTelemetry Collector with OTLP gRPC receivers enabled. Set the agent's exporter to `  otlp  ` and specify the endpoint where the agent should export the data. The following example uses a 10% sampling ratio and sends traces to the Collector that listens on localhost port `  4317  ` .

##### Terminal

``` text
DATASTORE_ENABLE_TRACING=ON                            \
java                                                   \
-javaagent:path/to/opentelemetry-javaagent.jar         \
-Dotel.traces.exporter=otlp                            \
-Dotel.exporter.otlp.endpoint="http://localhost:4317"  \
-Dotel.traces.sampler=traceidratio                     \
-Dotel.traces.sampler.arg=0.1                          \
-Dotel.service.name="My App"                           \
-jar myapp.jar

    
```

### Export directly to an observability backend with Auto Agents

In addition to setting the environment variable `  DATASTORE_ENABLE_TRACING=ON  ` , you need to add the OpenTelemetry Java agent extension for your specific backend. The following example uses the [Trace exporter extension](https://github.com/GoogleCloudPlatform/opentelemetry-operations-java/blob/main/exporters/auto/README.md#autoinstrumentation-setup) and a 10% trace sampling ratio.

##### Terminal

``` text
DATASTORE_ENABLE_TRACING=ON                                                \
java                                                                       \
-javaagent:path/to/opentelemetry-javaagent.jar                             \
-Dotel.javaagent.extensions=/path/to/exporter-auto-0.26.0-alpha-shaded.jar \
-Dotel.traces.exporter=google_cloud_trace                                  \
-Dotel.traces.sampler=traceidratio                                         \
-Dotel.traces.sampler.arg=0.1                                              \
-Dotel.service.name="My Application"                                       \
-jar myapp.jar

    
```

## Example trace

The following examples show how trace information is displayed in Cloud Trace. For more information about possible attributes and values, see [Trace span attributes and events](/datastore/docs/trace-span-references) .

### Example trace span

### Example event log

### Example attribute values

## What's next

  - View the reference for [Trace span attributes and events.](/datastore/docs/trace-span-references) .
  - Learn about [server-side monitoring](/datastore/docs/understand-performance-monitoring) .
