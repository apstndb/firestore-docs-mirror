---
name: documents/docs.cloud.google.com/firestore/native/docs/pipeline/stages/output/delete
uri: https://docs.cloud.google.com/firestore/native/docs/pipeline/stages/output/delete
title: Delete (Output Stage)
description: Learn how to use the delete stage in Firestore Pipeline Operations to remove documents based on query results.
data_source: docs.cloud.google.com
---

# Delete (Output Stage)

## Description

`delete()` is a Data manipulation language (DML) stage that allows a query to remove documents based on the results of a query. This stage can be attached to the end of a query and will delete all documents that the `__name__` field from the previous stage references.

## Examples

### Delete stale data

For example, the following query deletes all `users` documents with `address.users` set to `USA` and with `__create_time__` less than 10 days:

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

## Behavior

The following sections describe the execution behavior, responses, and restrictions for the `delete()` stage.

### Response

The `delete()` stage always emits a single document like `{ documents_modified: 28L }` describing how many documents were deleted.

### Full Collection Delete

Deleting all documents from a collection is possible by attaching `delete()` to the input collection stage:

##### Node.js

\`\`\`js const results = await db.pipeline() .collection("/users") .delete() .execute(); \`\`\`

##### Java

\`\`\`java Pipeline pipeline = db.pipeline() .collection("/users") .delete(); pipeline.execute(); \`\`\`

> **Tip:** To prevent accidental data loss, test your pipeline without the `delete()` stage first to preview the documents that will be affected.

### Final Stage

The `delete()` stage must come at the end of a pipeline, no further stages can be provided.

### Delete All / Bounding Workload

By default the `delete()` stage will remove all documents referenced by the previous stage. If you want to bound the size of the workload, or you know that the filter conditions match exactly one document, a `limit(...)` stage can be added before the final `delete()` to bound the total work.

### Cross Collection Mutations

The final `delete()` stage will apply mutations to *any* document referenced by `__name__` (assuming all necessary authentication is provided). This includes deleting documents from multiple different collections or collection groups as part of the same request.

### `__name__` Required

The `delete()` stage requires that the previous stage provides a `__name__` field that contains a document reference to remove. Failure to do so will result in a runtime error, and when run outside of a transaction can result in partial success.

Most Input stages, such as [`collection(...)`](https://docs.cloud.google.com/firestore/native/docs/pipeline/stages/input/collection) , [`collection_group(...)`](https://docs.cloud.google.com/firestore/native/docs/pipeline/stages/input/collection_group) , [`database(...)`](https://docs.cloud.google.com/firestore/native/docs/pipeline/stages/input/database) , and [`documents(...)`](https://docs.cloud.google.com/firestore/native/docs/pipeline/stages/input/documents) , include the `__name__` field by default so this is only relevant if using a projection (such as [`select(...)`](https://docs.cloud.google.com/firestore/native/docs/pipeline/stages/transformation/select) ) or performing a transformation on the documents (such as [`aggregate(...)`](https://docs.cloud.google.com/firestore/native/docs/pipeline/stages/transformation/aggregate) ).

### Response

The response includes a summary of the number of documents modified. For example, the following response confirms that the pipeline modified three documents:

```
{documents_modified: 3L}
```

### Limitations

- DML stages can now be run within transactions. The `insert()` and `upsert()` stages need to be run within a transaction in most cases.

- When executing a pipeline with DML stages within a new transaction, you can use the `atomic` option to automatically run within a transaction and commit upon successful execution of the pipeline.

- When running within a transaction, there are no restrictions on other stages (such as `where` , `addFields` , `union` , `findNearest` , and `aggregate` subqueries). Transactional DML operations are bounded by Firestore Enterprise edition transaction limits. Because transactions don't allow reads after the first write, you cannot call a DML pipeline multiple times within a single transaction or read documents after a DML pipeline executes. Attempting to execute a read after a DML write fails with a `FAILED_PRECONDITION` error: `Cannot have reads after the first write in a Firestore transaction.`

- When running outside of a transaction:

  - Each document is updated independently of each other, and writes are not atomic across documents. The pipeline halts on the first error, allowing for partial success to occur.
  - Advanced multi-query stages ( `aggregate` , `distinct` , `unnest` , `find_nearest` , `union` , joins, and subqueries) are not supported.

- Under Firebase Security Rules, each batch of documents re-evaluates rules and executes lookups. If rules use `get()` or `exists()` , the global 20-lookup limit is reached after writing approximately 200 documents, and the operation fails with `PERMISSION_DENIED` . Use Custom Claims instead of `get()` / `exists()` lookups to avoid this limit.

- If the stage preceding the DML stage produces multiple documents with the same `__name__` or evaluates to the same destination document ID, each mutation is processed sequentially:

  - For `upsert(...)` and `update(...)` : Multiple mutations targeting the same document follow "last one wins" semantics, where the last mutation processed determines the final state of the document.
  - For `delete(...)` : The first attempt deletes the document, and subsequent attempts for the same document are no-ops.
  - For `insert(...)` : The first attempt creates the document, and subsequent attempts targeting the same document ID fail with an `ALREADY_EXISTS` error.

### Transactional Execution

DML operations can be executed as part of a read-write transaction by either providing an explicit transaction to the pipeline execution call or by using the `atomic` option.

Firestore transactions require all reads to execute before any writes. Because a DML pipeline executes writes, you cannot perform reads (such as document lookups or query reads) after running a DML pipeline in the same transaction. For example, you cannot call a DML pipeline multiple times in a single transaction. Attempting to read after a DML pipeline executes fails with a `FAILED_PRECONDITION` error: `Cannot have reads after the first write in a Firestore transaction.`

#### Using an explicit transaction

##### Node.js

\`\`\`js // Execute a pipeline with DML stage within an explicit transaction const pipeline = db.pipeline() .collection("users") .where(field("active").equal(false)) .addFields(constant("inactive").as("status")) .update(); await db.runTransaction(async (transaction) =\> { return transaction.execute(pipeline); }); \`\`\`

##### Java

\`\`\`java // Execute a pipeline with DML stage within an explicit transaction Pipeline pipeline = db.pipeline() .collection("users") .where(field("active").equal(false)) .addFields(constant("inactive").as("status")) .update(); db.runTransaction(transaction -\> { transaction.execute(pipeline); return null; }); \`\`\`

#### Using the `atomic` option

##### Node.js

\`\`\`js // Execute a pipeline const results = await db.pipeline() .collection("users") .where(field("active").equal(false)) .addFields(constant("inactive").as("status")) .update() .execute({ atomic: true }); \`\`\`

##### Java

\`\`\`java // Execute a pipeline passing atomic option to execute() Pipeline pipeline = db.pipeline() .collection("users") .where(field("active").equal(false)) .addFields(constant("inactive").as("status")) .update(); pipeline.execute(new PipelineExecuteOptions().withAtomic(true)); \`\`\`
