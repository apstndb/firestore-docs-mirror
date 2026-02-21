# Enterprise edition index overview

**Preview — Firestore in Native mode (with Pipeline Operations) for Enterprise Edition**

This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](/terms/service-terms#1) . You can process personal data for this feature as outlined in the [Cloud Data Processing Addendum](/terms/data-processing-addendum) , subject to the obligations and restrictions described in the agreement under which you access Google Cloud. Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

Indexing behavior depends on the edition of the database. This page describes indexing for Firestore Enterprise edition. For Firestore Standard edition, see [Firestore Standard edition index overview](/firestore/docs/pipeline/concepts/standard-index-overview) .

This section describes indexing for Firestore Enterprise edition. **Firestore Enterprise edition does not create any indexes by default** . To reduce costs and improve database performance, create indexes for your most commonly used queries.

Indexes have a large impact on the performance of a database. If an index exists for a query, the database can efficiently return results by reducing the amount of data that needs to be scanned and reducing the work needed to sort the results. However, index entries increase storage costs and the amount of work done during a write operation on indexed fields.

## Index definition and structure

An index consists of the following:

  - a collection ID
  - a list of fields in the given collection
  - an order, either ascending or descending, for each field

An index can also enable the [sparse](#sparse_indexes) or [unique](#unique_indexes) options.

### Index ordering

The order and sort direction of each field uniquely defines the index. For example, the following indexes are two distinct indexes and not interchangeable:

<table>
<thead>
<tr class="header">
<th>Collection</th>
<th>Fields</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>cities</td>
<td>country (ascending), population (descending)</td>
</tr>
<tr class="even">
<td>cities</td>
<td>population (descending), country (ascending),</td>
</tr>
</tbody>
</table>

When creating an index to support a query, include the fields in the same order as your query.

### Index density

By default, index entries store data from all documents in a collection. This is known as a non-sparse index. An index entry will be added for a document regardless of whether the document contains any of the fields specified in the index. Non-existent fields are treated as having a NULL value when generating index entries. To change this behavior, you can define the index as a sparse index.

#### Sparse indexes

A sparse index indexes only the documents in the collection that contain a value (including null) for at least one of the indexed fields. A sparse index reduces storage costs and can improve performance.

## Unique indexes

Set the unique index option to enforce unique values for the indexed fields. For indexes on multiple fields, each combination of values must be unique across the index. The database rejects any update and insert operations that attempt to create index entries with duplicate values. If the data of the indexed fields contains duplicate values and you attempt to create a unique index, then the index build fails with an error message in the operation details.

### Absent fields in a unique index

If you insert a document with missing fields for the unique index, the index sets `  null  ` values for the missing fields. The resulting index entry must be unique or the operation fails.

For example, with this index:

<table>
<thead>
<tr class="header">
<th>Collection</th>
<th>Fields indexed</th>
<th>Query scope</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>cities</td>
<td>name (ascending)</td>
<td>Collection</td>
</tr>
</tbody>
</table>

If you add the document `  {"abbreviation": "LA"}  ` to the collection, the unique index creates an entry with `  name  ` set to `  null  ` . If you then try to add the document `  {"abbreviation": "NYC"}  ` , the operation fails because the resulting entry for the unique index is the same.

The same behavior applies to unique indexes with multiple fields. When creating or updating a document, missing indexed fields are set to `  null  ` and the resulting index entry must be unique in the index.

## Troubleshoot index building errors

You might encounter index building errors when managing your indexes. An indexing operation can fail if the database encounters a problem with the data. Indexing operations can fail for the following reasons:

  - You have reached an index limit. For example, the operation may have reached the maximum number of index entries per document. If index creation fails, you see an error message. If you have not reached an index limit, retry the index operation.
  - You set the unique index option and the data of the indexed fields would create duplicate index entries. To proceed, remove duplicate combinations of values from the data.

**Warning:** An ongoing index building error might impact creation of new indexes. Resolving the errors before creating indexes under the same collection.
