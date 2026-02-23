# Best practices

Use the best practices listed here as a quick reference when building an application that uses Firestore.

## Database location

When you create your database instance, select the [database location](/firestore/native/docs/locations) closest to your users and compute resources. Far-reaching network hops are more error-prone and increase query latency.

To maximize the availability and durability of your application, select a [multi-region location](/firestore/native/docs/locations#location-mr) and place critical compute resources in at least two regions.

Select a [regional location](/firestore/native/docs/locations#location-r) for lower costs, for lower write latency if your application is sensitive to latency, or for [co-location with other GCP resources](https://cloud.google.com/about/locations/#products-available-by-region) .

## Document IDs

  - Avoid the document IDs `  .  ` and `  ..  ` .

  - Avoid using `  /  ` forward slashes in document IDs.

  - Do not use monotonically increasing document IDs such as:
    
      - `  Customer1  ` , `  Customer2  ` , `  Customer3  ` , ...
      - `  Product 1  ` , `  Product 2  ` , `  Product 3  ` , ...
    
    Such sequential IDs can lead to [hotspots](#hotspots) that impact latency.

## Field Names

  - Avoid the following characters in field names because they require extra escaping:
    
      - `  .  ` period
      - `  [  ` left bracket
      - `  ]  ` right bracket
      - `  *  ` asterisk
      - ``  `  `` backtick

## Indexes

### Reduce write latency

The main contributor to write latency is index fanout. The best practices to reduce index fanout are:

  - Set [collection-level index exemptions](./query-data/indexing#add_a_collection-level_exemption) . An easy default is to disable Descending & Array indexing. Removing unused indexed values will also lower [storage costs](/firestore/pricing#storage-size) .

  - Reduce the number of documents in a transaction. For writing a large number of documents, consider using a bulk writer instead of the atomic batch writer.

### Index exemptions

For most apps, you can rely on automatic indexing as well as any error message links to manage your indexes. However, you may want to add [single-field exemptions](/firestore/docs/concepts/index-overview#single-field_index_exemptions) in the following cases:

Case

Description

Large string fields

If you have a string field that often holds long string values that you don't use for querying, you can cut storage costs by exempting the field from indexing.

High write rates to a collection containing documents with sequential values

If you index a field that increases or decreases sequentially between documents in a collection, like a timestamp, then the maximum write rate to the collection is 500 writes per second. If you don't query based on the field with sequential values, you can exempt the field from indexing to bypass this limit.

In an IoT use case with a high write rate, for example, a collection containing documents with a timestamp field might approach the 500 writes per second limit.

TTL fields

If you use [TTL (time-to-live) policies](/firestore/native/docs/ttl) , note that the TTL field must be a timestamp. Indexing on TTL fields is enabled by default and can affect performance at higher traffic rates. As a best practice, add automatic indexing exemptions for your TTL fields.

Large array or map fields

Large array or map fields can approach the limit of 40,000 index entries per document. If you are not querying based on a large array or map field, you should exempt it from indexing.

## Read and write operations

  - The exact maximum rate that an app can update a single document depends highly on the workload. For more information, see [Updates to a single document](#updates_to_a_single_document) .

  - Use asynchronous calls where available instead of synchronous calls. Asynchronous calls minimize latency impact. For example, consider an application that needs the result of a document lookup and the results of a query before rendering a response. If the lookup and the query do not have a data dependency, there is no need to synchronously wait until the lookup completes before initiating the query.

  - Do not use offsets. Instead, use [cursors](/firestore/docs/query-data/query-cursors) . Using an offset only avoids returning the skipped documents to your application, but these documents are still retrieved internally. The skipped documents affect the latency of the query, and your application is billed for the read operations required to retrieve them.

### Transactions retries

The Firestore [SDKs and client libraries](/firestore/docs/reference/libraries) automatically retry failed transactions to deal with transient errors. If your application accesses Firestore through the [REST](/firestore/docs/reference/rest) or [RPC](/firestore/docs/reference/rpc) APIs directly instead of through an SDK, your application should implement transaction retries to increase reliability.

### Real-time updates

For best practices related to real-time updates, see [Understand real-time queries at scale](/firestore/native/docs/real-time_queries_at_scale) .

## Designing for scale

The following best practices describe how to avoid situations that create contention issues.

### Updates to a single document

As you design your app, consider how quickly your app updates single documents. The best way to characterize your workload's performance is to perform load testing. The exact maximum rate that an app can update a single document depends highly on the workload. Factors include the write rate, contention among requests, and the number affected indexes.

A document write operation updates the document and any associated indexes, and Firestore synchronously applies the write operation across a quorum of replicas. At high enough write rates, the database will start to encounter contention, higher latency, or other errors.

### High read, write, and delete rates to a narrow document range

Avoid high read or write rates to lexicographically close documents, or your application will experience contention errors. This issue is known as hotspotting, and your application can experience hotspotting if it does any of the following:

  - Creates new documents at a very [high rate](#ramping_up_traffic) and allocates its own monotonically increasing IDs.
    
    Firestore allocates document IDs using a scatter algorithm. You should not encounter hotspotting on writes if you create new documents using automatic document IDs.

  - Creates new documents at a high rate in a collection with few documents.

  - Creates new documents with a monotonically increasing field, like a timestamp, at a very high rate.

  - Deletes documents in a collection at a high rate.

  - Writes to the database at a very high rate without gradually increasing traffic.

### Avoid skipping over deleted data

Avoid queries that skip over recently deleted data. A query may have to skip over a large number of index entries if the early query results have recently been deleted.

An example of a workload that might have to skip over a lot of deleted data is one that tries to find the oldest queued work items. The query might look like:

``` text
docs = db.collection('WorkItems').order_by('created').limit(100)
delete_batch = db.batch()
for doc in docs.stream():
  finish_work(doc)
  delete_batch.delete(doc.reference)
delete_batch.commit()
```

Each time this query runs it scans over the index entries for the `  created  ` field on any recently deleted documents. This slows down queries.

To improve the performance, use the `  start_at  ` method to find the best place to start. For example:

``` text
completed_items = db.collection('CompletionStats').document('all stats').get()
docs = db.collection('WorkItems').start_at(
    {'created': completed_items.get('last_completed')}).order_by(
        'created').limit(100)
delete_batch = db.batch()
last_completed = None
for doc in docs.stream():
  finish_work(doc)
  delete_batch.delete(doc.reference)
  last_completed = doc.get('created')

if last_completed:
  delete_batch.update(completed_items.reference,
                      {'last_completed': last_completed})
  delete_batch.commit()
```

NOTE: The example above uses a monotonically increasing field which is an anti-pattern for high write rates.

### Ramping up traffic

You should gradually ramp up traffic to new collections or lexicographically close documents to give Firestore sufficient time to prepare documents for increased traffic. We recommend starting with a maximum of 500 operations per second to a new collection and then increasing traffic by 50% every 5 minutes. You can similarly ramp up your write traffic, but keep in mind the [Firestore Standard Limits](/firestore/quotas#writes_and_transactions) . Be sure that operations are distributed relatively evenly throughout the key range. This is called the "500/50/5" rule.

#### Migrating traffic to a new collection

Gradual ramp up is particularly important if you migrate app traffic from one collection to another. A simple way to handle this migration is to read from the old collection, and if the document does not exist, then read from the new collection. However, this could cause a sudden increase of traffic to lexicographically close documents in the new collection. Firestore may be unable to efficiently prepare the new collection for increased traffic, especially when it contains few documents.

A similar problem can occur if you change the document IDs of many documents within the same collection.

The best strategy for migrating traffic to a new collection depends on your data model. Below is an example strategy known as *parallel reads* . You will need to determine whether or not this strategy is effective for your data, and an important consideration will be the cost impact of parallel operations during the migration.

##### Parallel reads

To implement parallel reads as you migrate traffic to a new collection, read from the old collection first. If the document is missing, then read from the new collection. A high rate of reads of non-existent documents can lead to hotspotting, so be sure to gradually increase load to the new collection. A better strategy is to copy the old document to the new collection then delete the old document. Ramp up parallel reads gradually to ensure that Firestore can handle traffic to the new collection.

A possible strategy for gradually ramping up reads or writes to a new collection is to use a deterministic hash of the user ID to select a random percentage of users attempting to write new documents. Be sure that the result of the user ID hash is not skewed either by your function or by user behavior.

Meanwhile, run a batch job that copies all your data from the old documents to the new collection. Your batch job should avoid writes to sequential document IDs in order to prevent hotspots. When the batch job finishes, you can read only from the new collection.

A refinement of this strategy is to migrate small batches of users at a time. Add a field to the user document which tracks migration status of that user. Select a batch of users to migrate based on a hash of the user ID. Use a batch job to migrate documents for that batch of users, and use parallel reads for users in the middle of migration.

Note that you cannot easily roll back unless you do dual writes of both the old and new entities during the migration phase. This would increase Firestore costs incurred.

## Privacy

  - Avoid storing sensitive information in a Cloud Project ID. A Cloud Project ID might be retained beyond the life of your project.
  - As a data compliance best practice, we recommend not storing sensitive information in document names and document field names.
