## Introduction

If your app experiences higher-than-usual latency, poor throughput, or timeouts with the Java Datastore client, the issue might stem from the client-side gRPC configuration rather than the Firestore/Datastore backend. This guide will help diagnose and resolve common client-side throttling issues, improper channel pool settings, and excessive channel churn.

## Diagnosis

When using Java clients, enabling verbose gRPC and gax-java logging is crucial for monitoring channel pool dynamics, diagnosing throttling, connection reuse problems, or identifying excessive channel churn.

## Enable logging for Java clients

To enable detailed logging, modify `  logging.properties  ` file as follows:

``` text
## This tracks the lifecycle events of each grpc channel 
io.grpc.ChannelLogger.level=FINEST
## Tracks channel pool events(resizing, shrinking) from GAX level
com.google.api.gax.grpc.ChannelPool.level=FINEST
```

Additionally, update the output logging level in `  logging.properties  ` to capture these logs:

``` text
# This could be changed to a file or other log output
handlers=java.util.logging.ConsoleHandler
java.util.logging.ConsoleHandler.level=FINEST
java.util.logging.ConsoleHandler.formatter=java.util.logging.SimpleFormatter
```

## Apply the configuration

`  logging.properties  ` file can be applied using one of two methods:

**1. Via a JVM System Property**

Add this argument when starting the Java application:

`  -Djava.util.logging.config.file=/path/to/logging.properties  `

**2. Load Programmatically**

This method is useful for integration tests or applications where logging configuration is managed within the code. Ensure this code runs early in the application's lifecycle.

``` text
LogManager logManager = LogManager.getLogManager();
  try (final InputStream is = Main.class.getResourceAsStream("/logging.properties")) {
logManager.readConfiguration(is);
}
```

## Logging example

After enabling verbose logging, you'll see a mix of messages from `  com.google.api.gax.grpc.ChannelPool  ` and `  io.grpc.ChannelLogger  ` :

**Channels under-provisioned which triggered channel pool expanding:**

``` text
09:15:30.123 [pool-1-thread-1] DEBUG com.google.api.gax.grpc.ChannelPool - Detected throughput peak of 40, expanding channel pool size: 4 -> 6. 
09:15:30.124 [grpc-nio-worker-ELG-1-5] DEBUG io.grpc.ChannelLogger - [Channel<5>: (datastore.googleapis.com:443)] Entering IDLE state 
09:15:30.124 [grpc-nio-worker-ELG-1-5] DEBUG io.grpc.ChannelLogger - [Channel<6>: (datastore.googleapis.com:443)] Entering IDLE state 
09:15:30.125 [grpc-nio-worker-ELG-1-5] TRACE io.grpc.ChannelLogger - [Channel<5>: (datastore.googleapis.com:443)] newCall() called 
09:15:30.126 [grpc-nio-worker-ELG-1-5] DEBUG io.grpc.ChannelLogger - [Channel<5>: (datastore.googleapis.com:443)] Entering CONNECTING state 09:15:30.127 [grpc-nio-worker-ELG-1-5] DEBUG io.grpc.ChannelLogger - [Channel<5>: (datastore.googleapis.com:443)] Entering READY state with picker: Picker{result=PickResult{subchannel=Subchannel<7>: (datastore.googleapis.com:443), streamTracerFactory=null, status=Status{code=OK, description=null, cause=null}, drop=false, authority-override=null}} 
09:15:31.201 [grpc-nio-worker-ELG-1-6] TRACE io.grpc.ChannelLogger - [Channel<6>: (datastore.googleapis.com:443)] newCall() called 
09:15:31.202 [grpc-nio-worker-ELG-1-6] DEBUG io.grpc.ChannelLogger - [Channel<6>: (datastore.googleapis.com:443)] Entering CONNECTING state 09:15:31.203 [grpc-nio-worker-ELG-1-6] DEBUG io.grpc.ChannelLogger - [Channel<6>: (datastore.googleapis.com:443)] Entering READY state with picker: Picker{result=PickResult{subchannel=Subchannel<8>: (datastore.googleapis.com:443), streamTracerFactory=null, status=Status{code=OK, description=null, cause=null}, drop=false, authority-override=null}}
```

**Channels over-provisioned which triggered channel pool shrinking:**

``` text
09:13:59.609 [grpc-nio-worker-ELG-1-4] DEBUG io.grpc.ChannelLogger - [Channel<21>: (datastore.googleapis.com:443)] Entering READY state with picker: Picker{result=PickResult{subchannel=Subchannel<23>: (datastore.googleapis.com:443), streamTracerFactory=null, status=Status{code=OK, description=null, cause=null}, drop=false, authority-override=null}}
09:14:01.998 [pool-1-thread-1] DEBUG com.google.api.gax.grpc.ChannelPool - Detected throughput drop to 0, shrinking channel pool size: 8 -> 6.
09:14:01.999 [pool-1-thread-1] TRACE io.grpc.ChannelLogger - [Channel<13>: (datastore.googleapis.com:443)] shutdown() called
09:14:01.999 [pool-1-thread-1] DEBUG io.grpc.ChannelLogger - [Channel<13>: (datastore.googleapis.com:443)] Entering SHUTDOWN state
09:14:01.999 [pool-1-thread-1] DEBUG io.grpc.ChannelLogger - [Channel<13>: (datastore.googleapis.com:443)] Terminated
09:14:01.999 [pool-1-thread-1] TRACE io.grpc.ChannelLogger - [Channel<15>: (datastore.googleapis.com:443)] shutdown() called
09:14:01.999 [pool-1-thread-1] DEBUG io.grpc.ChannelLogger - [Channel<15>: (datastore.googleapis.com:443)] Entering SHUTDOWN state
09:14:01.999 [pool-1-thread-1] DEBUG io.grpc.ChannelLogger - [Channel<15>: (datastore.googleapis.com:443)] Terminated
```

These log entries are useful for:

1.  Monitoring Channel Resizing Decisions
2.  Identifying Channel Reuse versus. Churn
3.  Spotting Transport Connectivity Issues

## Interpreting logs for symptom diagnosis

When troubleshooting performance issues like high latency or errors, start by enabling logging for `  com.google.api.gax.grpc.ChannelPool  ` and `  io.grpc.ChannelLogger  ` . Then, match the symptoms you're observing with the common scenarios in this guide to interpret the logs and find a resolution.

### Symptom 1: High latency at startup or during traffic spikes

You may notice that the first few requests after your application starts are slow, or that latency increases dramatically whenever traffic suddenly increases.

#### Possible cause

This latency often happens when your channel pool is under-provisioned. Each gRPC channel can handle a limited number of concurrent requests (100 limited by Google Middleware). Once this limit is reached, new RPCs will be queued on the client-side, waiting for an available slot. This queuing is the primary source of latency.

While the channel pool is designed to adapt to changes in load, its resizing logic runs periodically (by default, **every minute** ) and expands gradually (by default, adding at most **2** channels at a time). Therefore, there is an inherent delay between the initial traffic spike and the pool's expansion. The latency will occur during this period, while new requests are waiting for either the saturated channels to clear or for the pool to add new channels in its next resize cycle.

#### Logs to look for

Look for logs indicating that the channel pool is expanding. This is the primary evidence that the client is reacting to a traffic peak that has exceeded its current capacity.

**Channel Pool Expansion Log:**

``` text
[pool-1-thread-1] DEBUG com.google.api.gax.grpc.ChannelPool - Detected throughput peak of 40, expanding channel pool size: 4 -> 6.
```

**Interpretation** : The pool has detected a traffic spike and is opening new connections to handle the increased load. Frequent expansion, especially near startup, is a clear sign that your initial configuration isn't sufficient for your typical workload.

#### How to resolve

The goal is to have enough channels ready before the traffic arrives, preventing the client from having to create them under pressure.

**Increase `  initialChannelCount  ` (High Latency at Startup):**

If you observe high latency at startup, the most effective solution is to increase the `  initialChannelCount  ` in the `  ChannelPoolSettings  ` . By default, this value is set to **10** , which could be too low for applications that handle significant traffic at startup.

To find the right value for the application, you should:

1.  Enable `  FINEST  ` level logging for `  com.google.api.gax.grpc.ChannelPool  ` .
2.  Run your application under a typical starting workload or traffic spike.
3.  Observe the channel pool expansion logs to see what size the pool stabilizes at.

For example, if you see logs like this:  
`  [pool-1-thread-1] DEBUG com.google.api.gax.grpc.ChannelPool - Detected throughput peak of 80, expanding channel pool size: 4 -> 6.  `

and then a minute later, you see logs:

`  [pool-1-thread-1] DEBUG com.google.api.gax.grpc.ChannelPool - Detected throughput peak of 95, expanding channel pool size: 6 -> 8.  `

If you see expanded channel pool size stabilized at 8 channels and no more expanding logs can be found, this indicates that your application needed 8 channels to handle its workload. A good starting point would be to set your `  initialChannelCount  ` to 8. This ensures the connections are established upfront, reducing or eliminating latency caused by on-the-fly scaling.

The goal is to ensure the pool has enough capacity to handle peak load without queuing requests.

**Increase `  minChannelCount  ` (Traffic spikes):**

If you experience high latency specifically at the beginning of traffic spikes, it's a sign that your traffic is increasing faster than the channel pool can reactively create new connections. This is common for applications with predictable, sudden bursts of traffic.

The pool stabilizes with a small number of channels during normal traffic and proactively adds more as traffic increases to prevent saturation. This scaling process takes time, causing the initial requests in a burst to be queued, which results in high latency.

Increasing `  minChannelCount  ` sets a higher baseline of permanently open channels. This ensures enough capacity is already available to handle the initial burst, eliminating the scaling delay and the associated latency spike.

**Increase `  maxChannelCount  ` (Traffic spikes):**

If you observe high latency during traffic spikes and your logs show the channel pool is consistently at its maximum size ( `  maxChannelCount  ` ), the current limit is likely too low for your peak traffic. By default, `  maxChannelCount  ` is set to 200. To determine a better value, use the [connection pool configuration guide](/datastore/docs/java-client-grpc#connection_pool_configuration) to calculate the optimal number of connections based on your application's peak Queries Per Second (QPS) and average request latency.

### Symptom 2: Intermittent timeouts or RPC failures

Sometimes the application runs fine most of the time but occasionally suffers from intermittent timeouts, or failed RPCs, even during periods of normal traffic.

#### Possible cause: network instability

Connections between the client and the Datastore service are being dropped. The gRPC client will try to reconnect automatically, but this process can cause temporary failures and latency.

#### Logs to look for

The most critical log for diagnosing network problems is `  TRANSIENT_FAILURE  ` .

  - **Transient Failure Log:**

<!-- end list -->

``` text
[grpc-nio-worker-ELG-1-7] DEBUG io.grpc.ChannelLogger - [Channel<9>: (datastore.googleapis.com:443)] Entering TRANSIENT_FAILURE state
```

  - **Interpretation** : This log is a major red flag indicating the channel has lost its connection. A single, isolated failure might just be a minor network blip. However, if we see these messages frequently or a channel gets stuck in this state, it points to a significant underlying issue.

#### How to resolve

**Investigate your network environment** . Check for issues with firewalls, proxies, routers, or general network instability between the application and `  datastore.googleapis.com  ` .

### Symptom 3: High latency with over 20,000 concurrent requests per client

This specific symptom applies to applications running at a very high scale, typically when a **single client instance must handle more than 20,000 concurrent requests** . The application performs well under normal conditions, but as traffic increases to more than 20,000 concurrent requests per client, you observe a sharp and sudden degradation in performance. Latency jumps significantly and remains high for the entire duration of the peak traffic period. This occurs because the client's connection pool has reached its maximum size and cannot scale out further.

#### Possible cause

The client is suffering from channel saturation because the channel pool has reached its configured `  maxChannelCount  ` . By default, the pool is configured with a limit of **200** channels. Since each gRPC channel can handle up to 100 concurrent requests, this limit is only reached when a single client instance is processing approximately **20,000** requests simultaneously.

Once the pool hits this ceiling, it cannot create more connections. All 200 channels become overloaded, and new requests are queued on the client side, causing the sharp spike in latency.

The following logs can help confirm that the `  maxChannelCount  ` has been reached.

#### Logs to look for

The key indicator is observing that the channel pool stops expanding right at its configured limit, even as the load continues.

  - **Logs** : You will see earlier logs of the pool expanding. With default settings, the last expansion log you see before latency spikes will be the one where the pool reaches 200 channels:

<!-- end list -->

``` text
[pool-1-thread-1] DEBUG com.google.api.gax.grpc.ChannelPool - ... expanding channel pool size: 198 -> 200.
```

  - **Indicator** : During the period of high latency, you will see **no further "expanding channel pool size" logs** . The absence of these logs, combined with the high latency, is a strong indicator that the `  maxChannelCount  ` limit has been reached.

#### How to resolve

The goal is to ensure the pool has enough capacity to handle peak load without queuing requests.

  - **Increase `  maxChannelCount  `** : The primary solution is to increase the `  maxChannelCount  ` setting to a value that can support the application's peak traffic. Refer to the [connection pool configuration guide](/datastore/docs/java-client-grpc#connection_pool_configuration) to calculate the optimal number of connections based on the application's peak Queries Per Second (QPS) and average request latency.

## Appendix

The following sections provide supplementary information to aid in troubleshooting.

### Understand channel states

The following channel states can appear in the logs, providing insights into connection behavior:

<table>
<thead>
<tr class="header">
<th style="text-align: left;">State</th>
<th style="text-align: left;">Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;"><strong>IDLE</strong></td>
<td style="text-align: left;">The channel is created but has no active connections or RPCs. It's waiting for traffic.</td>
</tr>
<tr class="even">
<td style="text-align: left;"><strong>CONNECTING</strong></td>
<td style="text-align: left;">The channel is actively trying to establish a new network transport (connection) to the gRPC server.</td>
</tr>
<tr class="odd">
<td style="text-align: left;"><strong>READY</strong></td>
<td style="text-align: left;">The channel has an established and healthy transport and is ready to send RPCs.</td>
</tr>
<tr class="even">
<td style="text-align: left;"><strong>TRANSIENT_FAILURE</strong></td>
<td style="text-align: left;">The channel encountered a recoverable failure (e.g., network blip, temporary server unavailability). It will automatically attempt to reconnect.</td>
</tr>
<tr class="odd">
<td style="text-align: left;"><strong>SHUTDOWN</strong></td>
<td style="text-align: left;">The channel has been closed, either manually (e.g., <code dir="ltr" translate="no">       shutdown()      </code> called) or due to an idle timeout. No new RPCs can be initiated.</td>
</tr>
</tbody>
</table>

### Tips

  - If you use a structured logging framework like SLF4J or Logback, you must configure equivalent log levels in `  logback.xml  ` or other logger configuration files. The `  java.util.logging  ` levels will be mapped by the logging facade.
