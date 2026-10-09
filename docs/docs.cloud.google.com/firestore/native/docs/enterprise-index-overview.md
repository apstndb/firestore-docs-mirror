---
name: documents/docs.cloud.google.com/firestore/native/docs/enterprise-index-overview
uri: https://docs.cloud.google.com/firestore/native/docs/enterprise-index-overview
title: Enterprise edition index overview
description: A cloud-hosted NoSQL database that's simple enough for rapid prototyping yet scalable and flexible enough to grow to any size.
data_source: docs.cloud.google.com
---

# Enterprise edition index overview

Indexing behavior depends on the edition of the database. This page describes indexing for Firestore Enterprise edition. For Firestore Standard edition, see [Firestore Standard edition index overview](https://docs.cloud.google.com/firestore/docs/pipeline/concepts/standard-index-overview) .

This section describes indexing for Firestore Enterprise edition. **Firestore Enterprise edition does not create any indexes by default** . To reduce costs and improve database performance, create indexes for your most commonly used queries.

Indexes have a large impact on the performance of a database. If an index exists for a query, the database can efficiently return results by reducing the amount of data that needs to be scanned and reducing the work needed to sort the results. However, index entries increase storage costs and the amount of work done during a write operation on indexed fields.

## Index definition and structure

An index consists of the following:

- a collection ID
- a list of fields in the given collection
- an index mode, either ascending, descending, or array-contains, for each field

An index can also enable the [sparse](https://docs.cloud.google.com/firestore/native/docs/enterprise-index-overview#sparse_indexes) or [unique](https://docs.cloud.google.com/firestore/native/docs/enterprise-index-overview#unique_indexes) options.

### Index ordering

The order and sort direction of each field uniquely defines the index. For example, the following indexes are two distinct indexes and not interchangeable:

| Collection | Fields                                        |
|------------|-----------------------------------------------|
| cities     | country (ascending), population (descending)  |
| cities     | population (descending), country (ascending), |

When creating an index to support a query, include the fields in the same order as your query.

### Index density

By default, index entries store data from all documents in a collection. This is known as a non-sparse index. An index entry will be added for a document regardless of whether the document contains any of the fields specified in the index. Non-existent fields are treated as having a NULL value when generating index entries. To change this behavior, you can define the index as a sparse index.

#### Sparse indexes

A sparse index indexes only the documents in the collection that contain a value (including null) for at least one of the indexed fields. A sparse index reduces storage costs and can improve performance.

## Array-contains indexes

To optimize query performance when querying an array field using `array-contains` or `array-contains-any` , you can index the field in `array-contains` mode. An index can have at most one field in `array-contains` mode.

By indexing an array field in `array-contains` mode, the query engine can quickly locate documents containing specific array values. Without an index, queries check the array values by performing a full scan of the collection, which increases query latencies and read costs as the size of the collection grows.

To index an array field, the field must meet the following requirement:

- **Non-empty array requirement:** An index entry is created only if the array field exists in the document and is a non-empty array. Documents with missing, non-array, or empty array fields are not indexed.

### How density relates to array-contains indexes

For indexes that include an `array-contains` field, the index density rules apply only to the ordered indexed fields. If the non-empty array requirement is met, the density rules apply to the remaining ordered indexed fields in the index:

- **Non-sparse index ( `DENSE` ):** An index entry is generated for the document. Any missing ordered indexed fields in the index are stored as `null` in the index entry.
- **Sparse index ( `SPARSE` ):** An index entry is generated only if at least one of the ordered indexed fields exists in the document.

#### Example: Index entry generation

Consider the index `users (tags[*], status ASC)` :

| Document                                         | `NON-SPARSE` index                                                                                | `SPARSE` index                                                                                    |
|--------------------------------------------------|---------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------|
| `{ tags: ["news"], status: "active" }`           | **Indexed** : • (tags: `"news"` , status: `"active"` )                                            | **Indexed** : • (tags: `"news"` , status: `"active"` )                                            |
| `{ tags: ["news", "sports"], status: "active" }` | **Indexed** : • (tags: `"news"` , status: `"active"` ) • (tags: `"sports"` , status: `"active"` ) | **Indexed** : • (tags: `"news"` , status: `"active"` ) • (tags: `"sports"` , status: `"active"` ) |
| `{ tags: ["news", "news"], status: "active" }`   | **Indexed** : • (tags: `"news"` , status: `"active"` ) (deduplicated)                             | **Indexed** : • (tags: `"news"` , status: `"active"` ) (deduplicated)                             |
| `{ tags: [null], status: "active" }`             | **Indexed** : • (tags: `null` , status: `"active"` )                                              | **Indexed** : • (tags: `null` , status: `"active"` )                                              |
| `{ tags: ["news"] }`                             | **Indexed** : • (tags: `"news"` , status: `null` )                                                | **Not indexed** (missing `status` field)                                                          |
| `{ tags: "news", status: "active" }`             | **Not indexed** (field is not an array)                                                           | **Not indexed** (field is not an array)                                                           |
| `{ tags: null, status: "active" }`               | **Not indexed** (field is not an array)                                                           | **Not indexed** (field is not an array)                                                           |
| `{ status: "active" }`                           | **Not indexed** (missing `tags` field)                                                            | **Not indexed** (missing `tags` field)                                                            |
| `{ tags: [], status: "active" }`                 | **Not indexed** (empty array)                                                                     | **Not indexed** (empty array)                                                                     |

#### Query example

##### Web

```
// Query for users where 'tags' contains 'news' and 'status' is 'active'
const query = db.collection("users")
  .where("tags", "array-contains", "news")
  .where("status", "==", "active");

// Documents returned by the query:
// [
//   {
//     "id": "alice",
//     "tags": ["news", "tech"],
//     "status": "active"
//   }
// ]
```

## Unique indexes

Set the unique index option to enforce unique values for the indexed fields. For indexes on multiple fields, each combination of values must be unique across the index. The database rejects any update and insert operations that attempt to create index entries with duplicate values. If the data of the indexed fields contains duplicate values and you attempt to create a unique index, then the index build fails with an error message in the operation details.

### Absent fields in a unique index

If you insert a document with missing fields for the unique index, the index sets `null` values for the missing fields. The resulting index entry must be unique or the operation fails.

For example, with this index:

| Collection | Fields indexed   | Query scope |
|------------|------------------|-------------|
| cities     | name (ascending) | Collection  |

If you add the document `{"abbreviation": "LA"}` to the collection, the unique index creates an entry with `name` set to `null` . If you then try to add the document `{"abbreviation": "NYC"}` , the operation fails because the resulting entry for the unique index is the same.

The same behavior applies to unique indexes with multiple fields. When creating or updating a document, missing indexed fields are set to `null` and the resulting index entry must be unique in the index.

### Unique indexes on array values

A unique `array-contains` index prohibits documents with overlapping array elements.

This type of index does **not** enforce that an array has unique values within a single document.

For example, with a unique index on a field named `tags` :

The following document, `doc1` , is valid to insert:

```
{
  "tags": [ "news", "tech", "news", "music" ]
}
```

The index permits duplicate values ( `"news"` ) within the same array of a single document.

If you attempt to insert a second document, `doc2` , with a duplicate element, the operation fails:

```
{
  "tags": [ "sports", "music" ]
}
```

The operation fails because `"music"` is already present in `doc1` 's array and mapped in the index.

If you need to ensure that elements within the same array in a single document are unique, handle this in your application logic.

#### Empty arrays, missing fields, and null values

Normally, missing fields in a unique index are treated as `null` and must be unique across documents (see [Absent fields in a unique index](https://docs.cloud.google.com/firestore/native/docs/enterprise-index-overview#unique-index-missing-fields) ). However, for unique indexes on array fields:

- **Empty arrays, missing fields, and standalone nulls:** If the array field is empty, missing entirely, or holds a standalone `null` value (not inside an array), no index keys are generated for the document. Therefore, multiple documents can have empty fields or standalone `null` values without triggering duplicate key errors.
- **Null elements inside an array:** If the array contains a `null` value as an element (for example, `["news", null]` ), the `null` element is indexed. Any subsequent document containing a `null` element in its indexed array field will fail with a duplicate key error.

## Troubleshoot index building errors

You might encounter index building errors when managing your indexes. An indexing operation can fail if the database encounters a problem with the data. Indexing operations can fail for the following reasons:

- You have reached an index limit. For example, the operation may have reached the maximum number of index entries per document. If index creation fails, you see an error message. If you have not reached an index limit, retry the index operation.
- You set the unique index option and the data of the indexed fields would create duplicate index entries. To proceed, remove duplicate combinations of values from the data.

> **Warning:** An ongoing index building error might impact creation of new indexes. Resolving the errors before creating indexes under the same collection.
