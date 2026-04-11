# Optimize query performance

**Preview — Firestore in Native mode (with Pipeline Operations) for Enterprise Edition**

This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . You can process personal data for this feature as outlined in the [Cloud Data Processing Addendum](https://docs.cloud.google.com/terms/data-processing-addendum) , subject to the obligations and restrictions described in the agreement under which you access Google Cloud. Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

To troubleshoot slow queries, use [Query Explain](https://docs.cloud.google.com/firestore/native/docs/enterprise-query-explain) to obtain the query execution plan and the runtime execution profile. The following section describe steps you can take to optimize query performance depending on the execution profile:

## Limit the number of results

Use the records returned field in the execution tree to identify if the query is returning many documents. Consider limiting the number of documents returned by using the `limit(...)` stage. This reduces the serialized byte size of the results when returned to the clients over the network. In cases where the `Limit` node is preceded by a `MajorSort` node, the query engine can coalesce the `Limit` and the `MajorSort` nodes and replaces a full in-memory materialization and sort with a TopN sort, reducing the memory requirement for the query.

## Limit the Result Document Size

Consider limiting the size of the document returned by using by using a `select(...)` to only return the fields required or `remove_fields(...)` to discard overly large fields. This helps reduce the compute and memory cost of processing intermediate results and the serialized byte size of the results when returned to the clients over the network. In cases where all fields referenced in the query are covered by a regular index, this also allows the query to be fully covered by the index scan, avoiding the need to fetch documents from the primary storage.

## Use indexes

Use the following instructions to set up and optimize indexes.

### Identify if the query is using an index

You can identify if the query is using an index by checking the leaf nodes in the execution tree. If the leaf node of the execution tree is a [TableScan node](https://docs.cloud.google.com/firestore/native/docs/enterprise-query-explain-reference#tablescan) , that means the query is not using an index and is scanning documents from primary storage. If an index is being used, the leaf node of the execution tree will display the index ID and index fields of the index.

### Identify a better index

An index is useful for a query if it can reduce the number of documents that the query engine needs to fetch from primary storage or if its field ordering can deliver the Sort requirement of the query.

If an index is used for a query, but the query engine is still fetching and discarding many documents, as identified by a Scan node that returns many records followed by a [Filter node](https://docs.cloud.google.com/firestore/native/docs/enterprise-query-explain-reference#filter) that returns few records, this is a sign that the query predicate satisfied using the index is not selective. To create a more suitable index, see [Create indexes](https://docs.cloud.google.com/firestore/native/docs/enterprise-optimize-query-performance#create_indexes) .

If an index is used for a query, but the query engine is still performing an in-memory reordering of the result set, as identified by a [MajorSort node](https://docs.cloud.google.com/firestore/native/docs/enterprise-query-explain-reference#majorsort) in the query execution tree, this is a sign that the index used can't be used to deliver the Sort requirement of the query. To create a more suitable index, see the next section.

### Create Indexes

Follow the index management documentation to [create indexes](https://docs.cloud.google.com/firestore/native/docs/enterprise-indexing) . To ensure your query can use indexes, create regular (not Multikey) indexes with fields in the following order:

1.  All fields that will be used in equality operators. To maximize chance of reuse across queries, order fields in decreasing order of occurrence of the fields in equality operators among queries.
2.  All fields that will be sorted on (in the same order).
3.  Fields that will be used in range or inequality operators in decreasing order of query constraint selectivity.
4.  Fields that will be returned as part of a query in the index: including such fields in the index allows the index to cover the query and avoid having to fetch document from the primary storage.

### Force an index or table scan

When you query Firestore in Native Mode, it automatically uses any indexes that are likely to make the query more efficient. As a result, you don't need to specify an index for your queries. However, for queries that are critical for your workload, we recommend that you use the `forceIndex` option for more consistent performance.

In a few cases, Firestore in Native Mode might choose an index that causes query latency to increase. If you've followed the troubleshooting steps for performance regressions and confirmed that it makes sense to try a different index for the query, you can specify the index using the `forceIndex` option.

You can use the `forceIndex` option on any input stage in Pipeline operations to override Firestore in Native Mode's default query plan and specify an index to use, or to force a table scan.

#### Force a specific index

To force the query to use a specific index, provide the index ID as a string to the `forceIndex` option. You can find the index ID from the console or from error messages.

The following example forces the planner to use index with ID `CICAgOi36pgK` :

    // Force Planner to use Index ID CICAgOi36pgK
    db.pipeline()
      .collectionGroup({ collectionId: "customers", forceIndex: "CICAgOi36pgK" })
      .limit(100)

Here are some use cases for forcing a specific index:

  - Testing the performance of different indexes.
  - Ensuring a specific, known-optimal index is used for a query.
  - Overriding the optimizer when its default choice is suboptimal for a particular query.

If the specified index is not found, the query fails.

#### Force a table scan

A table scan reads documents in the collection or collection group without using any secondary indexes. To force a table scan, set `forceIndex` to `primary` .

The following example forces a table scan:

    // Force Planner to only do a Full-Table Scan
    db.pipeline()
      .collectionGroup({ collectionId: "customers", forceIndex: "primary" })
      .limit(100)

You might use a table scan in the following cases:

  - For very small collections where index overhead is not justified.
  - For queries that access most of the documents in a collection.
  - For debugging and performance comparisons.

**Caution:** Table scans on large collections are slow and don't scale. They read all documents in the collection, which significantly increases read operation costs. For most production scenarios, we recommend relying on indexes instead of forcing table scans.

#### Use `forceIndex` with Query Explain

You can use [Query Explain](https://docs.cloud.google.com/firestore/native/docs/enterprise-query-explain) , especially with the `analyze` option, to observe the effects of `forceIndex` :

  - Verify that Firestore in Native Mode used the specified index in `forceIndex` by checking the leaf nodes of the execution tree for the index ID.
  - Confirm that a `TableScan` node appears in the plan when using `forceIndex: "primary"` .
  - Compare the performance metrics—such as latency, documents scanned, and index entries scanned—with and without `forceIndex` to fine-tune query performance.

#### Best practices for `forceIndex`

While `forceIndex` provides more control over query execution, Firestore in Native Mode's query optimizer is generally efficient for most use cases. Consider the following best practices when using `forceIndex` :

  - Use `forceIndex` judiciously. If you observe suboptimal performance with the default query plan, use [Query Explain](https://docs.cloud.google.com/firestore/native/docs/enterprise-query-explain) to diagnose the issue before forcing an index.
  - When using `forceIndex` , make sure to test your queries with realistic data volumes to understand their performance and cost characteristics.ß
  - Avoid using `forceIndex: "primary"` on large collections in production environments.
