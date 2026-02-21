# Best practices for bulk data loading

This page describes the best practices when bulk loading data to Firestore with MongoDB compatibility with tools like `  mongoimport  ` .

Firestore is a highly distributed system offering automatic scaling to meet the needs of your business. Firestore dynamically splits and combines your data based on the load received by the system.

Load-based splitting happens automatically without any required pre-configuration. The Firestore load-based splitting system has some important, unique characteristics compared to other document databases that are important to keep in mind as you model your data.

Firestore's distributed nature can require changing some design choices to change, particularly for workloads that were optimized for databases where the primary replica is the bottleneck for write throughput.

## Best Practices

Workloads that process large amounts of data in a single threaded client can create a bottleneck. Clients might be able to use single threading to bulk load data, as the throughput of the client and server are similarly matched. A Firestore database can handle significantly more parallelism, but this requires that you configure clients to send requests in parallel.

### `     mongoimport    `

When using the `  mongoimport  ` tool, requests are made sequentially by default. To improve the load time into Firestore, set the number of workers with the `  --numInsertionWorkers  ` flag. The correct setting might require tuning based on the size of your client, but we generally recommend starting with at least `  32  ` .

### async programming

When developing your own software using MongoDB compatible APIs, you can improve parallelism in the following ways:

  - *Async frameworks* : using async frameworks let you process and respond to requests in parallel. It is not necessary to develop any complex pooling or queuing when making calls to your database. Each request flow can use independent connections and make their database calls in parallel.
  - *Use parallelized compute offerings* : using services like Cloud Run, your system can scale the number of computation workers required to process data.

### Transient Failures

When working with a large distributed system like Firestore, you might encounter transient failures such as network blips or contention on a document.

When bulk loading large amounts of information, it's important to maintain a retry strategy for failed writes without failing the larger bulk load operation.

**Note:** Firestore with MongoDB compatibility does not support `  retryWrites  ` . We recommend using transactions to ensure your application guarantees idempotency.
