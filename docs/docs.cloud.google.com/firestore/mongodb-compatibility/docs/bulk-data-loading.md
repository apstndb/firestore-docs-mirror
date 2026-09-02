---
name: documents/docs.cloud.google.com/firestore/mongodb-compatibility/docs/bulk-data-loading
uri: https://docs.cloud.google.com/firestore/mongodb-compatibility/docs/bulk-data-loading
title: Best practices for bulk data loading
description: Learn about best practices for bulk data loading for a Firestore with MongoDB compatibility database.
data_source: docs.cloud.google.com
---

# Best practices for bulk data loading

bulk loading data to Firestore with MongoDB compatibility with tools like `mongoimport` and `mongorestore` .

Firestore is a highly distributed system offering automatic scaling to meet the needs of your business. Firestore dynamically splits and combines your data based on the load received by the system.

Load-based splitting happens automatically without any required pre-configuration. The Firestore load-based splitting system has some important, unique characteristics compared to other document databases that are important to keep in mind as you model your data.

Firestore's distributed nature can require changing some design choices to change, particularly for workloads that were optimized for databases where the primary replica is the bottleneck for write throughput.

## Best Practices

Workloads that process large amounts of data in a single threaded client can create a bottleneck. Clients might be able to use single threading to bulk load data, as the throughput of the client and server are similarly matched. A Firestore database can handle significantly more parallelism, but this requires that you configure clients to send requests in parallel.

### `mongoimport`

When using the `mongoimport` tool, requests are made sequentially by default. To improve the load time into Firestore, set the number of workers with the `--numInsertionWorkers` flag. The correct setting might require tuning based on the size of your client.

### `mongorestore`

When using the `mongorestore` tool, remove the `retryWrites=false` parameter from your connection string in order to improve resilience to transient failures.

> **Note:** Support for `retryWrites` in Firestore with MongoDB compatibility is limited to the `mongorestore` tool.

To improve the load time into Firestore, you can also increase the number of insertion workers per collection with the `--numInsertionWorkersPerCollection` flag and the number of parallel collections with the `--numParallelCollections` flag. The correct settings might require tuning based on the size of your client.

### async programming

When developing your own software using MongoDB compatible operations, you can improve parallelism in the following ways:

  - *Async frameworks* : using async frameworks let you process and respond to requests in parallel. It is not necessary to develop any complex pooling or queuing when making calls to your database. Each request flow can use independent connections and make their database calls in parallel.
  - *Use parallelized compute offerings* : using services like Cloud Run, your system can scale the number of computation workers required to process data.

### Transient Failures

When working with a large distributed system like Firestore, you might encounter transient failures such as network blips or contention on a document.

When bulk loading large amounts of information, it's important to maintain a retry strategy for failed writes without failing the larger bulk load operation.

> **Note:** Firestore with MongoDB compatibility does not support `retryWrites` . We recommend using transactions to ensure your application guarantees idempotency.
