The [Java client for Datastore mode](https://github.com/googleapis/java-datastore) offers gRPC as a transport layer option. Using [gRPC connection pooling](https://grpc.io/docs/guides/performance/) enables distributing RPCs over multiple connections, which can improve performance.

## Before you begin

[Install](https://github.com/googleapis/java-datastore?tab=readme-ov-file#quickstart) the latest version of the `  google-cloud-datastore  ` library.

## How to enable the gRPC transport behavior

To enable the gRPC transport behavior, add `  setTransportOptions  ` to your client instantiation:

##### Java

``` text
DatastoreOptions datastoreOptions =
       DatastoreOptions.newBuilder()
               .setProjectId("my-project")
               .setDatabaseId("my-database")
               .setTransportOptions(GrpcTransportOptions.newBuilder().build())
               .build();
```

Setting the transport options explicitly to `  GrpcTransportOptions  ` configures the client to use gRPC instead of HTTP when making calls to the server.

## Deactivate the gRPC transport behavior

You can deactivate the gRPC transport behavior by reverting to the HTTP transport behavior. To do this, remove the `  .setTransportOptions  ` line of code or replace `  GrpcTransportOptions  ` with `  HttpTransportOptions  ` . You must also rebuild and restart your application.

##### Java

``` text
// Use this code to deactivate the gRPC transport behavior
// by reverting to the HTTP transport behavior.
DatastoreOptions datastoreOptions = DatastoreOptions.newBuilder()
            .setProjectId("my-project")
            .setDatabaseId("my-database")
            .build();

// You can also use this code to revert to the HTTP transport behavior
DatastoreOptions datastoreOptions =
            DatastoreOptions.newBuilder()
                    .setProjectId("my-project")
                    .setDatabaseId("my-database")
                    .setTransportOptions(HttpTransportOptions.newBuilder()
                            .setConnectTimeout(1000)
                            .build())
                    .build();
```

**Note:** Only clients that explicitly set `  GrpcTransportOptions  ` change behavior with the release of this feature. Client instantiations that already use `  setTransportOptions  ` with `  HttpTransportOptions  ` won't change behavior due to this feature.

### Verify transport options

To verify which type of `  TransportOptions  ` the client uses, examine the transport options type:

##### Java

``` text
// Compares datastore transport options type

boolean isGRPC = datastore.getOptions().getTransportOptions() instanceof GrpcTransportOptions;

boolean isHTTP = datastore.getOptions().getTransportOptions() instanceof HTTPTransportOptions;
```

## Connection pool configuration

A *connection pool* , also known as a channel pool, is a cache of database connections that the client shares and reuses to improve connection latency and performance. To improve the performance of your application, configure the connection pool.

This section helps you determine the optimal connection pool size and demonstrates how to configure it within the Java client library.

### Determine the best connection pool size

The default connection pool size is right for most applications, and in most cases, there's no need to change it. However, you might want to change your connection pool size because of high throughput or buffered requests.

Ideally, to leave room for traffic fluctuations, a connection pool has about twice the number of connections it takes for maximum saturation. Because a connection can handle a maximum of 100 concurrent requests, we recommend that you have between 10 and 50 outstanding requests per connection. The middleware layer enforces the limit of 100 concurrent streams per gRPC connection, and this limit isn't configurable. To calculate the optimal number of connections in your connection pool, using an estimated per-client QPS and average latency numbers, do the following:

From your client-side metrics, gather the following information and make the following calculations:

1.  Determine the maximum number of queries per second (QPS) per client when your application runs a workload.
2.  Determine the average latency (the response time for a single request) in ms.
3.  Determine the number of requests that you can send serially per second by dividing 1,000 by the average latency value.
4.  Divide the QPS in seconds by the number of serial requests per second.
5.  Divide the result by 50 requests per channel to determine the minimum optimal connection pool size. (If your calculation is less than 2, use at least 2 channels anyway, to ensure redundancy.)
6.  Divide the same result by 10 requests per channel to determine the maximum optimal connection pool size.

To perform these steps, use the following equations:

``` text
(QPS sec ÷ (1,000 ÷ latency ms)) ÷ 50 streams = Minimum optimal number of
connections

(QPS sec ÷ (1,000 ÷ latency ms)) ÷ 10 streams = Maximum optimal number of
connections
```

For example, if your application typically sends 50,000 requests per second, and the average latency is 10 ms. Divide 1,000 by 10 ms to determine that you can send 100 requests serially per second. Divide that number into 50,000 to get the parallelism needed to send 50,000 QPS: 500.

Each channel can have at most 100 requests out concurrently, and your target channel utilization is between 10 and 50 concurrent streams. Therefore, to calculate the minimum connection pool size, divide 500 by 50 to get 10. To find the maximum connection pool size, divide 500 by 10 to get 50.

This means that your connection pool size for this example is between 10 and 50 connections. It's also important to monitor your traffic after making these changes and adjust the number of connections in your pool, as necessary.

### Set the pool size

The following code sample demonstrates how to configure the connection pool in the client libraries using `  DatastoreOptions  ` .

##### Java

``` text
InstantiatingGrpcChannelProvider channelProvider =
        DatastoreSettings.defaultGrpcTransportProviderBuilder()
                .setChannelPoolSettings(
                       ChannelPoolSettings.builder()
                                .setInitialChannelCount(MIN_VAL)
                                .setMaxChannelCount(MAX_VAL)
                                .build())
                .build();

DatastoreOptions options = DatastoreOptions.newBuilder()
         .setProjectId("my-project")
         .setChannelProvider(channelProvider)
         .setTransportOptions(GrpcTransportOptions.newBuilder().build())
         .build();
```

## What's next

For more information about connection pools and best practices for performance, see:

  - [ChannelPoolSettings](/java/docs/reference/gax/latest/com.google.api.gax.grpc.ChannelPoolSettings)
  - [Performance Best Practices](https://grpc.io/docs/guides/performance/)
