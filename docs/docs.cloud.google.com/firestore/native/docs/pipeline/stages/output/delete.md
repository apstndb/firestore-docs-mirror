---
name: documents/docs.cloud.google.com/firestore/native/docs/pipeline/stages/output/delete
uri: https://docs.cloud.google.com/firestore/native/docs/pipeline/stages/output/delete
title: Delete (Output Stage)
description: Learn how to use the delete stage in Firestore Pipeline Operations to remove documents based on query results.
data_source: docs.cloud.google.com
---

# Delete (Output Stage)

> **Preview**
> 
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

`delete()` is a Data manipulation language (DML) stage that allows a query to remove documents based on the results of a query. This stage can be attached to the end of a query and will delete all documents that the `__name__` field from the previous stage references.

## Examples

For example, the following query deletes all `users` documents with `address.users` set to `USA` and with `__create_time__` less than 10 days:

##### Node.js

    const pipeline = db.pipeline()
      .collectionGroup("users")
      .where(field("address.country").equal("USA"))
      .where(field("__create_time__").timestampAdd("day", 10).lessThan(currentTimestamp()))
      .delete();
    await pipeline.execute();

##### Python

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

##### Java

    Pipeline.Snapshot deleteResults = firestore.pipeline()
      .collectionGroup("users")
      .where(field("address.country").equal("USA"))
      .where(field("__create_time__").add(constant(10)).lessThan(currentTimestamp()))
      .delete()
      .execute().get();

## Behavior

### Response

The `delete()` stage always emits a single document like `{ documents_modified: 28L }` describing how many documents were deleted.

### Full Collection Delete

Deleting all documents from a collection is possible by appending `delete()` to the input stage like:

### Node.js

    const results = await db.pipeline()
      .collection("/users")
      .delete()
      .execute();

Making sure the `where(...)` stage before the final `delete()` properly limits the documents to only update the expected documents. It is good practice to run the query without the final `delete()` stage first to validate that only the intended documents are removed.

### Final Stage

The `delete()` stage must come at the end of a pipeline, no further stages can be provided.

### Delete All

By default the `delete()` stage will remove all documents referenced by the previous stage. If you want to bound the size of the workload, or you know that the filter conditions match exactly one document a `limit(1)` can be added before the final `delete()` to bound the total work.

### Cross Collection Mutations

The final `delete()` stage will apply mutations to *any* document referenced by `__name__` (assuming all necessary authentication is provided). This includes deleting documents from multiple different collections or collection groups as part of the same request.

### `__name__` Required

The `delete()` stage requires that the previous stage provides a `__name__` field that contains a document reference to remove. Failure to do so will result in a runtime error, and when run outside of a transaction can result in partial success.

Most Input stages, such as [`collection(...)`](https://docs.cloud.google.com/firestore/native/docs/pipeline/stages/input/collection) , [`collection_group(...)`](https://docs.cloud.google.com/firestore/native/docs/pipeline/stages/input/collection_group) , [`database(...)`](https://docs.cloud.google.com/firestore/native/docs/pipeline/stages/input/database) , and [`documents(...)`](https://docs.cloud.google.com/firestore/native/docs/pipeline/stages/input/documents) , include the `__name__` field by default so this is only relevant if using a projection (such as [`select(...)`](https://docs.cloud.google.com/firestore/native/docs/pipeline/stages/transformation/select) ) or performing a transformation on the documents (such as [`aggregate(...)`](https://docs.cloud.google.com/firestore/native/docs/pipeline/stages/transformation/aggregate) ).

The response includes a summary of the number of documents modified. For example, the following response confirms that the pipeline modified three documents:

    {documents_modified: 3L}

## Limitations

  - DML stages don't support Firestore Security Rules. DML operation attempts through Firestore Security Rules are denied.

  - During the Preview for this feature, you cannot run DML stages in a transaction. For more information on consistency behavior see [Consistency](https://docs.cloud.google.com/firestore/native/docs/pipeline/dml#consistency) .

  - If the stage preceding the DML stage produces multiple documents with the same `__name__` , each instance is processed. For `update(...)` , this means the same target document might be modified multiple times. For `delete(...)` , subsequent attempts after the first will be no-ops.
