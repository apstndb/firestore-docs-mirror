---
name: documents/docs.cloud.google.com/firestore/native/docs/pipeline/dml
uri: https://docs.cloud.google.com/firestore/native/docs/pipeline/dml
title: Modify data with Pipeline operations
description: A cloud-hosted NoSQL database that's simple enough for rapid prototyping yet scalable and flexible enough to grow to any size.
data_source: docs.cloud.google.com
---

# Modify data with Pipeline operations

Use the `update(...)` and `delete(...)` Data manipulation language (DML) stages to construct data pipelines that can query for documents and then delete or modify data.

## Edition requirements

The operations described on this page require Firestore Enterprise edition.

## Before you begin

You should be familiar with how to [query a database with Pipeline operations](https://docs.cloud.google.com/firestore/native/docs/pipeline/overview) .

## Update documents

Use the [`update(...)`](https://docs.cloud.google.com/firestore/native/docs/pipeline/stages/output/update) DML stage to construct data pipelines that can query for documents and then add or modify data.

All DML stages must come at the end of the pipeline. The documents coming into this stage must include the `__name__` field to identify which documents to update. The operation fails if any of the documents you attempt to update don't exist.

For example, the following operation backfills a data model change to all documents in a collection group. The pipeline adds a `preferences.color` field to all documents in the `users` collection group that are missing that field.

##### Node.js

```
const snapshot = await db.pipeline()
   .collectionGroup("users")
   .where(not(exists(field("preferences.color"))))
   .addFields(constant(null).as("preferences.color"))
   .removeFields("color")
   .update()
   .execute();
```

##### Python

```
from google.cloud.firestore_v1.pipeline_expressions import Constant, Field, Not

snapshot = (
    client.pipeline()
    .collection_group("users")
    .where(Not(Field.of("preferences.color").exists()))
    .add_fields(Constant.of(None).as_("preferences.color"))
    .remove_fields("color")
    .update()
    .execute()
)
```

##### Java

```
Pipeline.Snapshot snapshot = firestore.pipeline()
   .collectionGroup("users")
   .where(not(exists(field("preferences.color"))))
   .addFields(constant((String) null).as("preferences.color"))
   .removeFields("color")
   .update()
   .execute().get();
```

##### Go

```
snapshot := client.Pipeline().
    CollectionGroup("users").
    Where(firestore.Not(firestore.FieldExists(firestore.FieldOf("preferences.color")))).
    AddFields(firestore.Selectables(
        firestore.ConstantOfNull().As("preferences.color"),
    )).
    RemoveFields(firestore.Fields("color")).
    Update().
    Execute(ctx)
```

## Delete documents

Use the [`delete(...)`](https://docs.cloud.google.com/firestore/native/docs/pipeline/stages/output/delete) DML stage to construct data pipelines that can query for documents and then delete data. To prevent accidental bulk deletions, pipelines ending in `delete(...)` should include at least one `where(...)` stage. All DML stages must come at the end of the pipeline.

For example, the following pipeline deletes all `users` documents with `address.users` set to `USA` and with `__create_time__` less than 10 days:

##### Node.js

```
const pipeline = db.pipeline()
  .collectionGroup("users")
  .where(field("address.country").equal("USA"))
  .where(field("__create_time__").timestampAdd("day", 10).lessThan(currentTimestamp()))
  .delete();
await pipeline.execute();
```

##### Python

```
from google.cloud.firestore_v1.pipeline_expressions import CurrentTimestamp, Field

snapshot = (
    client.pipeline()
    .collection_group("users")
    .where(Field.of("address.country").equal("USA"))
    .where(
        Field.of("__create_time__")
        .timestamp_add("day", 10)
        .less_than(CurrentTimestamp())
    )
    .delete()
    .execute()
)
```

##### Java

```
Pipeline.Snapshot deleteResults = firestore.pipeline()
  .collectionGroup("users")
  .where(field("address.country").equal("USA"))
  .where(field("__create_time__").add(constant(10)).lessThan(currentTimestamp()))
  .delete()
  .execute().get();
```

##### Go

```
snapshot := client.Pipeline().
    CollectionGroup("users").
    Where(firestore.FieldOf("address.country").Equal("USA")).
    Where(firestore.FieldOf("__create_time__").Add(firestore.ConstantOf(10)).LessThan(firestore.CurrentTimestamp())).
    Delete().
    Execute(ctx)
```

## Execution Modes and Consistency

DML stages can be executed either inside an explicit transaction or outside of a transaction:

### Transactional execution

Transactional DML provides atomic, all-or-nothing consistency across documents and supports the full set of pipeline query stages. This makes it ideal for workloads that require strict consistency guarantees—where partial updates are unacceptable—or that rely on complex query stages, provided the modifications fit within transaction size limits.

Running a DML pipeline inside an explicit transaction (using `runTransaction` / `transaction.execute(pipeline)` or the `atomic: true` option) has the following behavior:

- All mutations either commit together or roll back completely on failure.
- All pipeline query stages are supported before a DML stage (including `where` , `add_fields` , `union` , `find_nearest` , and `aggregate` subqueries).
- In a transaction, all read operations must execute before any write operations. Because a DML pipeline performs writes, you cannot execute reads after running a DML pipeline in the same transaction. For example, you cannot call a DML pipeline multiple times in a single transaction, nor can you read documents after executing a DML pipeline. Attempting to execute a read after a DML pipeline runs fails with a `FAILED_PRECONDITION` error: `Cannot have reads after the first write in a Firestore transaction.`
- The operation is subject to Firestore Enterprise edition transaction limits.

### Non-transactional execution

Non-transactional DML is designed for bulk modifications across a large number of documents without running into transaction size limitations. By locking at the document level rather than across the entire operation, it allows other concurrent operations to proceed while updating documents at scale.

When DML stages run outside of an explicit transaction:

- **Independent updates and partial success** : Each document is updated independently of each other, and operations are not atomic across documents. The pipeline halts on the first error, and previously modified documents remain written to the database, which allows for partial success to occur.
- **Stage support** :
  - Advanced and multi-query stages (such as `aggregate(...)` , `distinct(...)` , `unnest(...)` , `find_nearest(...)` , `union(...)` , joins, and subqueries) are not supported before DML outside of a transaction. Use a transaction if your pipeline requires these stages.
- **Security Rules 20-lookup limit** : Each batch of documents executes in its own transaction and re-evaluates security rules. If your security rules use `get()` or `exists()` lookups, each batch executes a lookup, reaching the per-request limit of 20 lookups after writing approximately 200 documents and failing with `PERMISSION_DENIED` . Use [Custom Claims](https://firebase.google.com/docs/auth/admin/custom-claims) instead of `get()` or `exists()` lookups to avoid this limit.

## Limitations

Note the following limitations for DML stages:

- DML stages must be the last stage in a pipeline definition before calling `.execute()` .
- When run outside of a transaction, each document is updated independently of each other and allows for partial success to occur.
- Non-transactional DML operations subject to Security Rules with `get()` or `exists()` lookups are capped at approximately 200 documents due to the 20-lookup limit.
- Transactional DML operations are bounded by Firestore Enterprise edition transaction limits. Because Firestore transactions don't allow reads after the first write, you cannot call a DML pipeline multiple times within a single transaction, nor can you read documents after executing a DML pipeline. Attempting to execute a read after a DML write fails with a `FAILED_PRECONDITION` error: `Cannot have reads after the first write in a Firestore transaction.`
- If the stage preceding the DML stage produces multiple documents with the same `__name__` or evaluates to the same destination document ID, each mutation is processed sequentially:
  - For `upsert(...)` and `update(...)` : Multiple mutations targeting the same document follow "last one wins" semantics, where the last mutation processed determines the final state of the document.
  - For `delete(...)` : The first attempt deletes the document, and subsequent attempts for the same document are no-ops.
  - For `insert(...)` : The first attempt creates the document, and subsequent attempts targeting the same document ID fail with an `ALREADY_EXISTS` error.
