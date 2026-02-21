# Understand real-time queries at scale

Read this document for guidance on scaling your serverless app beyond thousands of operations per second or hundreds of thousands of concurrent users. This document includes advanced topics to help you understand the system in depth. If you are just starting out with Firestore, see the [quickstart guide](/firestore/docs/quickstarts) instead.

Firestore and the Firebase mobile/web SDKs provide a powerful model for developing serverless apps where client-side code directly accesses the database. The SDKs let clients listen for updates to the data in real time. You can use real-time updates to build responsive apps that don't require server infrastructure. While it's very easy to get something up and running, it helps to understand the constraints in the systems that make up Firestore so that your serverless app scales and performs well when traffic increases.

See the following sections for advice on scaling your app.

## Pick a database location close to your users

The following diagram demonstrates the architecture of a real-time app:

When an app that is running on a user's device (mobile or web) establishes a connection to Firestore, the connection is routed to a Firestore frontend server in the same [region](/firestore/native/docs/locations) where your database is located. For example, if your database is in `  us-east1  ` , the connection also goes to a Firestore frontend also in `  us-east1  ` . These connections are long-lived and stay open until explicitly closed by the app. The frontend reads data from the underlying Firestore storage systems.

The distance between a user's physical location and the Firestore database location affects the latency experienced by the user. For example, a user in India whose app talks to a database in a Google Cloud region in North America might find the experience slower and the app less snappy than if the database was instead located closer, such as in India or in another part of Asia.

**Key Point:** For the best user experience, pick a region as close as possible to where your users are located.

## Design for reliability

The following topics improve or affect your app's reliability:

### Enable offline mode

The Firebase SDKs provide offline data persistence. If the app on the user's device can't connect to Firestore, the app remains usable by working with locally cached data. This ensures data access even when users experience spotty internet connections or completely lose access for several hours or days. For more details on offline mode, see [Enable offline data](/firestore/native/docs/manage-data/enable-offline) .

### Understand automatic retries

The Firebase SDKs take care of retrying operations and re-establishing broken connections. This helps work around transient errors caused by restarting servers or network issues between the client and the database.

### Choose between regional and multi-regional locations

There are several trade-offs when choosing between regional and multi-regional locations. The main difference is how data is replicated. This drives the availability guarantees of your app. A multi-region instance gives stronger serving reliability and increases the durability of your data but the trade-off is cost.

## Understand the real-time query system

Real-time queries, also called snapshot listeners, let the app listen to changes in the database and get low-latency notifications as soon as the data changes. An app can get the same result by periodically polling the database for updates, but it's often slower, more expensive, and requires more code. For examples of how to set up and use real-time queries, see [Get real-time updates](/firestore/native/docs/query-data/listen) . The following sections get into details of how snapshot listeners work and describe some of the best practices for scaling real-time queries while retaining performance.

Imagine two users that connect to Firestore through a messaging app built with one of the mobile SDKs.

Client A writes to the database to add and update documents in a collection called `  chatroom  ` :

``` text
collection chatroom:
    document message1:
      from: 'Sparky'
      message: 'Welcome to Firestore!'

    document message2:
      from: 'Santa'
      message: 'Presents are coming'
```

Client B listens for updates in the same collection using a snapshot listener. Client B gets an immediate notification whenever someone creates a new message. The following diagram shows the architecture behind a snapshot listener:

The following sequence of events takes place when Client B connects a snapshot listener to the database:

1.  Client B opens a connection to Firestore and registers a listener by making a call to `  onSnapshot(collection("chatroom"))  ` through the Firebase SDK. This listener can stay active for hours.
2.  The Firestore frontend queries the underlying storage system to bootstrap the dataset. It loads the entire result set of matching documents. We refer to this as a **polling query** . The system then evaluates the database's [Firebase Security Rules](https://firebase.google.com/docs/rules) to verify that the user can access this data. If the user is authorized, the database returns the data to the user.
3.  Client B's query then moves into **listen mode** . The listener registers with a subscription handler and waits for updates to the data.
4.  Client A now sends a write operation to modify a document.
5.  The database commits the document change to its storage system.
6.  Transactionally, the system commits the same update to an internal changelog. The changelog establishes a strict ordering of changes as they happen.
7.  The changelog in turn fans out the updated data to a pool of subscription handlers.
8.  A **reverse query matcher** executes to see if the updated document matches any currently registered snapshot listeners. In this example, the document matches Client B's snapshot listener. As the name implies, you can think of the reverse query matcher as a normal database query but done in reverse. Instead of searching through documents to find those that match a query, it efficiently searches through queries to find those that match an incoming document. Upon finding a match, the system forwards the document in question to the snapshot listeners. Then the system evaluates the database's [Firebase Security Rules](https://firebase.google.com/docs/rules) to ensure that only authorized users receive the data.
9.  The system forwards the document update to the SDK on client B's device, and the `  onSnapshot  ` callback fires. If local persistence is enabled, the SDK applies the update to the local cache as well.

A key part of Firestore's scalability depends on the fan-out from the changelog to the subscription handlers and the frontend servers. The fan-out lets a single data change to propagate efficiently to serve millions of real-time queries and connected users. By running many replicas of all these components across multiple zones (or multiple regions in the case of a multi-region deployment), Firestore achieves high availability and scalability.

It's worth noting that all read operations issued from mobile and web SDKs follow the model above. They perform a polling query followed by listen mode to maintain consistency guarantees. This also applies to real-time listeners, calls to retrieve a document, and [one-shot queries](/firestore/native/docs/query-data/get-data) . You can think of single document retrievals and one-shot queries as short-lived snapshot listeners that come with similar constraints around performance.

## Apply best practices for scaling real-time queries

Apply the following best practices to design scalable real-time queries.

### Understand high write traffic in the system

This section helps you understand how the system responds to an increasing number of write requests.

The Firestore changelogs that drive the real-time queries automatically scale horizontally as write traffic increases. As the write rate for a database increases beyond what a single server can handle, the changelog is split across multiple servers, and the query processing starts to consume data from multiple subscription handlers instead of one. From the client and SDK's perspective, this is all transparent and no action is required from the app when splits happen. The following diagram demonstrates how real-time queries scale:

Automatic scaling allows you to increase your write traffic without limits, but as the traffic ramps up, the system might take some time to respond. Follow the recommendations of the [5-5-5 rule](/firestore/native/docs/best-practices#ramping_up_traffic) to avoid creating a write hotspot. [Key Visualizer](https://cloud.google.com/firestore/docs/key-visualizer) is a useful tool for analyzing write hotspots.

Many apps have predictable organic growth, which Firestore can accommodate without precautions. Batch workloads like importing a large dataset, however, can ramp up writes too quickly. As you design your app, stay aware of where your write traffic comes from.

**Key Point:** Firestore scales automatically but ramping up writes too quickly leads to contention and performance problems. Make sure to follow the [5-5-5 rule](/firestore/native/docs/best-practices#ramping_up_traffic) to avoid creating a write hotspot.

### Understand how writes and reads interact

You can think of the real-time query system as a pipeline connecting write operations with readers. Any time a document is created, updated, or deleted, the change propagates from the storage system to the currently registered listeners. Firestore's changelog structure guarantees strong consistency, which means that your app never receives notifications of updates that are out of order compared to when the database committed the data changes. This simplifies app development by removing edge cases around data consistency.

This connected pipeline means that a write operation causing hotspots or lock contention can negatively affect read operations. When write operations fail or experience throttling, a read might stall waiting for consistent data from the changelog. If this happens in your app, you might see both slow write operations and correlated slow response times for queries. Avoiding hotspots is the key to steering clear of this problem.

**Key Point:** Writes and snapshot listeners are connected. A problem with write operations might cause slower response times.

### Keep documents and write operations small

When building apps with snapshot listeners, you typically want users to find out about data changes quickly. To achieve this, try to keep things small. The system can push small documents with tens of fields through the system very quickly. Larger documents with hundreds of fields and large data take longer to process.

Likewise, favor short, fast commit and write operations to keep latency low. Large batches might give you higher throughput from the writer's perspective but might actually increase the notification time for snapshot listeners. This is often counterintuitive compared to using other database systems where you might use batching to improve performance.

**Key Point:** Small documents and write operations are faster to process, and lead to more responsive apps.

### Use efficient listeners

As the write rates for your database increase, Firestore splits the data processing across many servers. Firestore's sharding algorithm tries to co-locate data from the same collection or collection group onto the same changelog server. The system tries to maximize the possible write throughput while keeping the number of servers involved in the processing of a query as low as possible.

However, certain patterns might still lead to suboptimal behavior for snapshot listeners. For example, if your app stores most of its data in one large collection, the listener might need to connect to many server to receive all data it needs. This remains true even if you apply a query filter. Connecting to many servers increases the risk of slower responses.

To avoid these slower responses, design your schema and app so that the system can serve listeners without going to many different servers. It might work best to break your data into smaller collections with smaller write rates.

This is similar to thinking about the performance queries in a relational database that require full table scans. In a relational database, a query that requires a full table scan is the equivalent of a snapshot listener that watches a high-churn collection. It might perform slowly compared to a query that the database can serve using a more specific index. A query with a more specific index is like a snapshot listener that watches a single document or a collection that changes less often. You should load test your app to best understand the behavior and need of your use case.

**Key Point:** Snapshot listeners that try to filter too much incoming data might be slow even if the result set is small.

### Keep polling queries fast

Another key part of responsive real-time queries involves making sure that the polling query to bootstrap the data is fast and efficient. The first time a new snapshot listener connects, the listener must load the entire result set and send it to the user's device. Slow queries make your app less responsive. This includes, for example, queries that try to read many documents or queries that don't use the appropriate indexes.

A listener might also move back from a listening state to a polling state under some circumstances. This happens automatically and is transparent to the SDKs and your app. The following conditions might trigger a polling state:

  - The system [re-balances a changelog](#understand_high_write_traffic_in_the_system) due to changes in load.
  - Hotspots cause failed or delayed writes to the database.
  - Transient server restarts temporarily affect listeners.

If your polling queries are fast enough, a polling state becomes transparent to your app's users.

**Key Point:** To build responsive apps, it's important to keep polling queries fast. Keep the datasets for real-time queries small.

### Favor long-lived listeners

Opening and keeping listeners alive for as long as possible is often the most cost-effective way to build an app that uses Firestore. When using Firestore, you are billed for the documents returned to your app and not for maintaining an open connection. A long-lived snapshot listener reads only the data it needs to serve the query throughout its lifetime. This includes an initial polling operation followed by notifications when the data actually changes. One-shot queries, on the other hand, re-read data that may not have changed since the app last executed the query.

In cases where your app must consume a high rate of data, snapshot listeners might not be appropriate. For example, if your use case pushes many documents per second through a connection for an extended period of time, it might be better to opt for one-shot queries that run at a lower frequency.

**Key Point:** For responsive apps, long-lived snapshot listeners are the most efficient way to consume data.

## What's Next

  - Learn [how to use snapshot listeners](/firestore/native/docs/query-data/listen) .
  - Read about more [best practices](/firestore/native/docs/best-practices) .
