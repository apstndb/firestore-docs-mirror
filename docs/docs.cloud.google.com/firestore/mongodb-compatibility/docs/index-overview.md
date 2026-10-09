---
name: documents/docs.cloud.google.com/firestore/mongodb-compatibility/docs/index-overview
uri: https://docs.cloud.google.com/firestore/mongodb-compatibility/docs/index-overview
title: Indexes overview
description: Overview of indexes for Firestore with MongoDB compatibility.
data_source: docs.cloud.google.com
---

# Indexes overview

This page describes indexing for Firestore with MongoDB compatibility. Firestore with MongoDB compatibility does not create any indexes by default. To improve database performance, create indexes for your most commonly used queries.

Indexes have a large impact on the performance of a database. If an index exists for a query, the database can efficiently return results by reducing the amount of data that needs to be scanned and reducing the work needed to sort the results. However, index entries increase storage costs and the amount of work done during a write operation on indexed fields.

## Index definition and structure

An index consists of the following:

- a collection ID
- a list of fields in the given collection
- an order, either ascending or descending, for each field

An index can also enable the [sparse](https://docs.cloud.google.com/firestore/mongodb-compatibility/docs/index-overview#sparse_indexes) , [multikey](https://docs.cloud.google.com/firestore/mongodb-compatibility/docs/index-overview#multikey) , or [unique](https://docs.cloud.google.com/firestore/mongodb-compatibility/docs/index-overview#unique_indexes) options.

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

## Multikey indexes for array values

If you are creating an index on a field that contains array values, you must create a multikey index. A regular index cannot index array values. A multikey index supports up to one array field in the index definition and can be used for operations that traverse array values.

Only use multikey indexes if you know that you need to index array values. Regular indexes have advantages when processing a query. For example, regular indexes can filter values within a range more efficiently.

The following situations lead to errors when working with array values and multikey indexes:

- An operation attempts to add an array value to a field indexed by a regular index. To add the array value, you must delete existing regular indexes on that field, and recreate them as multikey indexes.
- You attempt to create a regular index on a field that contains an array value. You must either create a multikey index or delete the array values.
- An operation attempts to index multiple fields with array values. You cannot have more than one field with an array value in a multikey index. To proceed, modify your data model or your index definitions.
- You attempt to create a multikey index where two field paths share a common prefix like `users.posts` and `users.zip` .

## Unique indexes

Set the unique index option to enforce unique values for the indexed fields. For indexes on multiple fields, each combination of values must be unique across the index. The database rejects any update and insert operations that attempt to create index entries with duplicate values. If the data of the indexed fields contains duplicate values and you attempt to create a unique index, then the index build fails with an error message in the operation details.

### Absent fields in a unique index

If you insert a document with missing fields for the unique index, the index sets `null` values for the missing fields. The resulting index entry must be unique or the operation fails.

For example, with this index:

```
db.cities.createIndex( { "name": 1 }, { unique: true } )
```

If you add the document `{"abbreviation": "LA"}` to the collection, the unique index creates an entry with `name` set to `null` . If you then try to add the document `{"abbreviation": "NYC"}` , the operation fails because the resulting entry for the unique index is the same.

The same behavior applies to unique indexes with multiple fields. When creating or updating a document, missing indexed fields are set to `null` and the resulting index entry must be unique in the index.

### Unique indexes on array values

A unique multikey index can be used to enforce that documents don't have overlapping array elements.

This type of index does **not** enforce that an array has unique values within a single document.

For example, with a unique index:

```
db.collection.createIndex( { "tags": 1 }, { unique: true } )
```

The following document is valid to insert:

```
{
  "_id": 1,
  "tags": [ "news", "tech", "news", "music" ]
}
```

The index permits duplicate values ( `"news"` ) within the same array of a single document.

If you attempt to insert a second document with a duplicate element, the operation fails:

```
{
  "_id": 2,
  "tags": [ "sports", "music" ]
}
```

The operation fails because `"music"` is already present in document `1` 's array and mapped in the index.

If you need to ensure that elements within the same array in a single document are unique, handle this in your application logic by using updating operators such as `$addToSet` instead of `$push` .

#### Empty arrays, missing fields, and null values

Normally, missing fields in a unique index are treated as `null` and must be unique across documents (see [Absent fields in a unique index](https://docs.cloud.google.com/firestore/mongodb-compatibility/docs/index-overview#unique-index-missing-fields) ). However, for unique indexes on array fields:

- **Empty arrays, missing fields, and standalone nulls:** If the array field is empty, missing entirely, or holds a standalone `null` value (not inside an array), no index keys are generated for the document. Therefore, multiple documents can have empty fields or standalone `null` values without triggering duplicate key errors.
- **Null elements inside an array:** If the array contains a `null` value as an element (for example, `["news", null]` ), the `null` element is indexed. Any subsequent document containing a `null` element in its indexed array field will fail with a duplicate key error.

## TTL indexes

Use [TTL indexes](https://docs.cloud.google.com/firestore/mongodb-compatibility/docs/ttl) to automatically remove stale data from your databases. A TTL index designates a given field as the expiration time for documents in a given collection. With TTL, you can decrease storage costs by cleaning out obsolete data. Data is typically deleted within 24 hours after its expiration time.

## Troubleshoot index building errors

You might encounter index building errors when managing your indexes. An indexing operation can fail if the database encounters a problem with the data. Indexing operations can fail for the following reasons:

- You have reached an index limit. For example, the operation may have reached the maximum number of index entries per document. If index creation fails, you see an error message. If you have not reached an index limit, retry the index operation.
- A multikey index is required. At least one of the indexed fields contains an array value. To proceed, you must either use a multikey index or delete the array values.
- An operation attempts to index multiple fields with array values. You cannot have more than one field with an array value in a multikey index. To proceed, modify your data model or your index definitions.
- You set the unique index option and the data of the indexed fields would create duplicate index entries. To proceed, remove duplicate combinations of values from the data.

> **Warning:** An ongoing index building error might impact creation of new indexes. Resolving the errors before creating indexes under the same collection.

## What's next

- Learn how to [create and manage indexes](https://docs.cloud.google.com/firestore/mongodb-compatibility/docs/indexing) or [TTL indexes](https://docs.cloud.google.com/firestore/mongodb-compatibility/docs/ttl)
