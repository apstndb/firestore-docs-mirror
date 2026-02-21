# Optimize query performance

**Preview — Firestore in Native mode (with Pipeline Operations) for Enterprise Edition**

This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](/terms/service-terms#1) . You can process personal data for this feature as outlined in the [Cloud Data Processing Addendum](/terms/data-processing-addendum) , subject to the obligations and restrictions described in the agreement under which you access Google Cloud. Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

To troubleshoot slow queries, use [Query Explain](/firestore/docs/pipeline/enterprise-query-explain) to obtain the query execution plan and the runtime execution profile. The following section describe steps you can take to optimize query performance depending on the execution profile:

## Limit the number of results

Use the records returned field in the execution tree to identify if the query is returning many documents. Consider limiting the number of documents returned by using the `  limit(...)  ` stage. This reduces the serialized byte size of the results when returned to the clients over the network. In cases where the `  Limit  ` node is preceded by a `  MajorSort  ` node, the query engine can coalesce the `  Limit  ` and the `  MajorSort  ` nodes and replaces a full in-memory materialization and sort with a TopN sort, reducing the memory requirement for the query.

## Limit the Result Document Size

Consider limiting the size of the document returned by using by using a `  select(...)  ` to only return the fields required or `  remove_fields(...)  ` to discard overly large fields. This helps reduce the compute and memory cost of processing intermediate results and the serialized byte size of the results when returned to the clients over the network. In cases where all fields referenced in the query are covered by a regular index, this also allows the query to be fully covered by the index scan, avoiding the need to fetch documents from the primary storage.

## Use indexes

Use the following instructions to set up and optimize indexes.

### Identify if the query is using an index

You can identify if the query is using an index by checking the leaf nodes in the execution tree. If the leaf node of the execution tree is a [TableScan node](/firestore/docs/pipeline/enterprise-query-explain#tablescan) , that means the query is not using an index and is scanning documents from primary storage. If an index is being used, the leaf node of the execution tree will display the index ID and index fields of the index.

### Identify a better index

An index is useful for a query if it can reduce the number of documents that the query engine needs to fetch from primary storage or if its field ordering can deliver the Sort requirement of the query.

If an index is used for a query, but the query engine is still fetching and discarding many documents, as identified by a Scan node that returns many records followed by a [Filter node](/firestore/docs/pipeline/enterprise-query-explain-reference#filter) that returns few records, this is a sign that the query predicate satisfied using the index is not selective. To create a more suitable index, see [Create indexes](#create_indexes) .

If an index is used for a query, but the query engine is still performing an in-memory reordering of the result set, as identified by a [MajorSort node](/firestore/docs/pipeline/enterprise-query-explain-reference#majorsort) in the query execution tree, this is a sign that the index used can't be used to deliver the Sort requirement of the query. To create a more suitable index, see the next section.

### Create Indexes

Follow the index management documentation to [create indexes](query-data/enterprise-indexing) . To ensure your query can use indexes, create regular (not Multikey) indexes with fields in the following order:

1.  All fields that will be used in equality operators. To maximize chance of reuse across queries, order fields in decreasing order of occurrence of the fields in equality operators among queries.
2.  All fields that will be sorted on (in the same order).
3.  Fields that will be used in range or inequality operators in decreasing order of query constraint selectivity.
4.  Fields that will be returned as part of a query in the index: including such fields in the index allows the index to cover the query and avoid having to fetch document from the primary storage.

### Use query hints

If you have created a more suitable index for the query but the query engine is not using that index, you can override the query engine's index preference by using a query hint.
