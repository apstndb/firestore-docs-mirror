# Understand reads and writes at scale

Read this document to make informed decisions on architecting your applications for high performance and reliability. This document includes advanced Firestore topics. If you're just starting out with Firestore, see the [quickstart guide](/firestore/mongodb-compatibility/docs/create-and-query-database) .

To make sure that your applications continue to perform well as your database size and traffic increase, it helps to understand the mechanics of reads and writes in the Firestore backend. You must also understand the interaction of your read and writes with the storage layer and the underlying constraints that may affect performance.

See the following sections for best practices before architecting your application.

## Understand the high level components

The following diagram shows the high level components involved in a Firestore API request.

### SDKs, client libraries, and drivers

Firestore supports SDKs, client libraries, and drivers for different platforms.

### Google Front End (GFE)

This is an infrastructure service common to all Google Cloud services. The GFE accepts incoming requests and forwards them to the relevant Google service (Firestore service in this context).

### Firestore service

The Firestore service performs checks on the API request, which includes authentication, authorization, quota checks, and also manages transactions. This Firestore service includes a *storage client* that interacts with the storage layer for the data reads and writes.

### Firestore storage layer

The Firestore storage layer is responsible for storing both the data and metadata, and the associated database features provided by Firestore. The following sections describe how data is organized in the Firestore storage layer and how the system scales. Learning about how data is organized can help you design a scalable data model and better understand the best practices in Firestore.

#### Key Ranges and Splits

Firestore is a NoSQL, document-oriented database. You store data in *documents* which are organized in *collections* . The collection name and document ID form a unique key for a document. Documents in the same collection are stored together in keyspace. Within that keyspace the document ID is hashed. The term *key range* refers to a contiguous range of keys in storage.

Firestore automatically partitions data within collections across multiple storage servers. These partitions are referred to as *splits* .

Documents can generate index entries which are lexicographically ordered and participate in the same sort of splitting and placement as the document data.

**Key Point:** Understanding how Firestore manages key ranges and splits is important for scalable data modeling.

#### Synchronous Replication

Every write is synchronously replicated to a majority of replicas using [Paxos](https://en.wikipedia.org/wiki/Paxos_\(computer_science\)) . One replica per split is considered a leader and coordinates the replication process. In the event of leader failure a new leader is elected. Replicas are located in different [zones](https://cloud.google.com/docs/geography-and-regions#regions_and_zones) to be resilient to potential zone failure. The overall result of this is a scalable and highly available system that provides low latencies for both reads and writes, irrespective of heavy workloads and at very large scale.

#### Single Region versus Multi-Region

When you create a database, you must select a [single regional location](/firestore/mongodb-compatibility/docs/locations#location-r) or a [multi-region location](/firestore/mongodb-compatibility/docs/locations#location-mr) .

A single regional location is a specific geographic location, like *us-west1* . The splits of data of a Firestore database have replicas in different zones within the selected region, as explained earlier.

A multi-region location consists of a defined set of regions where Firestore stores replicas of the database. In a multi-region deployment of Firestore, two regions have *full replicas* of the entire data in the database. A third region has a *witness replica* that doesn't maintain a full set of data, but participates in replication. Data is available to be written and read even with the loss of an entire region, because Firestore replicates the data between multiple regions.

For more information about the locations of a region, see [Firestore locations](/firestore/mongodb-compatibility/docs/locations) .

**Key Point:** Choosing between single-region versus multi-region configurations has key performance, availability, and cost trade-offs.

## Understand the life of a write

A driver can write data by creating, updating, or deleting a single document. A write to a single document requires updating both the document and its associated index entries atomically in the storage layer. Firestore also supports atomic operations consisting of multiple reads and writes to one or more documents.

For all kinds of writes, Firestore provides the [ACID properties](https://en.wikipedia.org/wiki/ACID) (atomicity, consistency, isolation, and durability) of relational databases. Firestore also provides [*serializability*](/firestore/docs/transaction-data-contention#serializable_isolation) , which means that all transactions appear as if executed in a serial order.

### High-level steps in a write transaction

When the driver issues a write or commits a transaction, using any of the methods mentioned earlier, internally this is executed as a [database read-write transaction](https://en.wikipedia.org/wiki/Database_transaction) in the storage layer. The transaction enables Firestore to provide the ACID properties mentioned earlier.

As the first step of a transaction, Firestore reads the existing document, and determines the mutations to be made to the data in the document.

This also includes making updates to any relevant indexes:

  - Indexed fields that are being added to the documents need corresponding inserts into the indexes.
  - Indexed fields that are being removed from the documents need corresponding deletes in the indexes.
  - Indexed fields that are being modified in the documents, need both deletes (for old values) and inserts (for new values) in the indexes.

To calculate the mutations mentioned earlier, Firestore reads the *indexing configuration* for the project. The indexing configuration stores information about the indexes for a project.

Once the mutations are calculated, Firestore collects them inside a transaction and then commits it.

**Key Point:** Firestore internally always uses transactions to provide ACID properties for writes.

### Understand a write transaction in the storage layer

As discussed earlier, a write in Firestore involves a read-write transaction in the storage layer. Depending on the layout of data, a write might involve one or more splits.

In the following diagram, the Firestore database has eight splits (marked 1-8) hosted on three different storage servers in a single zone, and each split is replicated in 3(or more) different zones. Each split has a Paxos leader, which might be in a different zone for different splits.

Consider a Firestore database that has the `  Restaurants  ` collection as follows:

The driver requests the following change to a document in the `  Restaurant  ` collection by updating the value of the `  priceCategory  ` field.

The following high-level steps describe what happens as part of the write:

1.  Create a read-write transaction.
2.  Read the `  restaurant1  ` document in the `  Restaurants  ` collection.
3.  Read the indexes for the document.
4.  Compute the mutations to be made to the data. In this case, there are five mutations:
      - M1: Update the row for `  restaurant1  ` to reflect the change in value of the *`  priceCategory  `* field.
      - M2 and M3: Delete the old index entries for *`  priceCategory  `* .
      - M4 and M5: Add new index entries for *`  priceCategory  `* .
5.  Commit these mutations.

The storage client in the Firestore service looks up the splits that owns the keys of the rows to be changed. Consider a case where Split 3 serves M1, and Split 6 serves M2-M5. There is a distributed transaction, involving all these splits as *participants* . The participant splits may also include any other split from which data was read earlier as part of the read-write transaction.

The following steps describe what happens as part of the commit:

1.  The storage client issues a commit. The commit contains the mutations M1-M5.
2.  Splits 3 and 6 are the participants in this transaction. One of the participants is chosen as the *coordinator* , such as Split 3. The job of the coordinator is to make sure the transaction either commits or aborts atomically across all participants.
      - The leader replicas of these splits are responsible for work done by the participants and coordinators.
3.  Each participant and coordinator runs a Paxos algorithm with their respective replicas.
      - The leader runs a Paxos algorithm with the replicas. Quorum is achieved if most of the replicas reply with an `  ok to commit  ` response to the leader.
      - Each participant then notifies the coordinator when they are *prepared* (first phase of two-phase commit). If any participant cannot commit the transaction, the whole transaction `  aborts  ` .
4.  Once the coordinator knows all participants, including itself, are prepared, it communicates the *`  accept  `* transaction outcome to all the participants (second phase of two-phase commit). In this phase, each participant records the commit decision to stable storage and the transaction is committed.
5.  The coordinator responds to the storage client in Firestore that the transaction has been committed. In parallel, the coordinator and all the participants apply the mutations to the data.

When the Firestore database is small, it may happen that a single split owns all the keys in the mutations M1-M5. In such a case, there is only one participant in the transaction and the two-phase commit mentioned earlier is not required, thus making the writes faster.

#### Writes in multi-region

In a multi-region deployment, the spread of replicas across regions increases availability, but comes with a performance cost. The communication between replicas in different regions takes longer round trip times. Hence, the baseline latency for Firestore operations is slightly more compared to single region deployments.

We configure the replicas in a way that leadership for splits always stays in the primary region. The primary region is the one from which traffic is incoming to the Firestore server. This decision of leadership reduces the round-trip delay in communication between the storage client in Firestore and the replica leader (or coordinator for multi-split transactions).

**Key Point:** Firestore uses transactions to do writes, which requires acquiring shared locks for read and exclusive locks for write. When a transaction reads many rows no other transaction can write to that set of rows till this transaction either commits or aborts, causing higher latencies and lock contention errors. Hence, try to avoid large reads inside a transaction.

**Key Point:** Write/transaction latency increases as the number of splits/participants increases. There is no explicit mechanism to control the number of participants. However, you can do the following to reduce the number of participants:

  - High index fanout is when many index entries need to be written. High index fanout for a document write increases the number or database rows to be mutated, which increases the number of participants. Don't index on fields not used for querying.
  - The number of participants increases as the number of documents updated in a write transaction increase. For lower latency, keep the number of documents updated in a single write transaction low.

## Understand the life of a read

This section delves into reads in Firestore. Queries, in particular, consist of a mix of document reads and index entry reads.

The data reads from the storage layer are internally done by using a database transaction to ensure consistent reads. However, unlike the transactions used for writes, these transactions don't take locks. Instead, they work by choosing a timestamp, then executing all reads at that timestamp. Since they don't acquire locks, they don't block concurrent read-write transactions. To execute this transaction, the storage client in Firestore specifies a timestamp bound, which tells the storage layer how to choose a read timestamp. The type of timestamp bound chosen by the storage client in Firestore is determined by the read options for the Read request.

### Understand a read transaction in the storage layer

This section describes the types of reads and how they are processed in the storage layer in Firestore.

#### Strong reads

By default, Firestore reads are *strongly consistent* . This strong consistency means that a Firestore read returns the latest version of the data that reflects all writes that have been committed up until the start of the read.

#### Single Split read

The storage client in Firestore looks up the splits that own the keys of the rows to be read. Assume that it needs to do a read from Split 3 from the earlier [section](#understand_a_write_transaction_in_the_storage_layer) . The client sends the read request to the nearest replica to reduce round trip latency.

At this point, the following cases might happen depending on the chosen replica:

  - Read request goes to a leader replica (Zone A).
      - As the leader is always up-to-date, the read can proceed directly.
  - Read request goes to a non-leader replica (such as, Zone B)
      - Split 3 may know by its internal state that it has enough information to serve the read and the split does so.
      - Split 3 is unsure if it has seen the latest data. It sends a message to the leader to ask for the timestamp of the last transaction it needs to apply to serve the read. Once that transaction is applied, the read can proceed.

Firestore then returns the response to its client.

#### Multi-split read

In the situation where the reads have to be done from multiple splits, the same mechanism happens across all the splits. Once the data has been returned from all the splits, the storage client in Firestore combines the results. Firestore then responds to its client with this data.

**Key Point:** The latency overhead increases as the number of splits involved in a read increase. Keeping your queries' result sets small, whenever possible, will help.

## Avoid hotspots

The *splits* in Firestore are automatically broken into smaller pieces to distribute the work of serving traffic to more storage servers when needed or when the key space expands. Splits created to handle excess traffic are retained for around \~24 hours even if the traffic goes away. So if there are recurring traffic spikes, the splits are maintained and more splits are introduced whenever required. These mechanisms help Firestore databases to autoscale under increasing traffic load or database size. However, there are some limitations to be aware..

Splitting storage and load takes time, and ramping up traffic too fast may cause high latency or deadline exceeded errors, commonly referred to as ***hotspots*** , while the service adjusts. The best practice is to distribute operations across the key range, while ramping up traffic gradually on a collection in a database.

Though splits are created automatically with increasing load, Firestore can split a key range only until it's serving a single document using a dedicated set of replicated storage servers. As a result, high and sustained volumes of concurrent operations on a single document may lead to a hotspot on that document. If you encounter sustained high latencies on a single document, you should consider modifying your data model to split or replicate the data across multiple documents.

Contention errors happen when multiple operations try to read and write the same document simultaneously.

**Key Point:** Avoid high read or write rates to a single document, or documents in a key range containing a few documents, or your application will experience high latency and contention errors.

**Key Point:** Indexing fields with monotonically increasing/decreasing values, such as timestamps, can lead to hotspots which affect latency for applications with high read and write rates.

Note that by following the practices outlined on this page, Firestore can scale to serve arbitrarily large workloads without you having to adjust any configuration.
