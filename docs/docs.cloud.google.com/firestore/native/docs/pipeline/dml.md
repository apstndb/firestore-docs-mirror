# Modify data with Pipeline operations

> **Preview**
> 
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

Use the `update(...)` and `delete(...)` Data manipulation language (DML) stages to construct data pipelines that can query for documents and then delete or modify data.

## Edition requirements

The operations described on this page require Firestore Enterprise edition.

## Before you begin

You should be familiar with how to [query a database with Pipeline operations](https://docs.cloud.google.com/firestore/native/docs/pipeline/overview) .

## Update documents

Use the [`update(...)`](https://docs.cloud.google.com/firestore/native/docs/pipeline/stages/dml/update) DML stage to construct data pipelines that can query for documents and then add or modify data.

All DML stages must come at the end of the pipeline. The documents coming into this stage must include the `__name__` field to identify which documents to update. The operation fails if any of the documents you attempt to update don't exist.

For example, the following operation backfills a data model change to all documents in a collection group. The pipeline adds a `preferences.color` field to all all documents in the `users` collection group that are missing that field.

##### Node.js

    const snapshot = await db.pipeline()
       .collectionGroup("users")
       .where(not(exists(field("preferences.color"))))
       .addFields(constant(null).as("preferences.color"))
       .removeFields("color")
       .update()
       .execute();test.firestore.js

##### Python

    from google.cloud.firestore_v1.pipeline_expressions import Constant, Field, Not
    
    snapshot = (
        client.pipeline()
        .collection_group("users")
        .where(Not(Field.of("preferences.color").exists()))
        .add_fields(Constant.of(None).as_("preferences.color"))
        .remove_fields("color")
        .update()
        .execute()
    )firestore_pipelines.py

##### Java

    Pipeline.Snapshot snapshot = firestore.pipeline()
       .collectionGroup("users")
       .where(not(exists(field("preferences.color"))))
       .addFields(constant((String) null).as("preferences.color"))
       .removeFields("color")
       .update()
       .execute().get();PipelineSnippets.java

## Delete documents

Use the [`delete(...)` stage](https://docs.cloud.google.com/firestore/native/docs/pipeline/stages/dml/delete) DML stages to construct data pipelines that can query for documents and then delete data. To prevent accidental bulk deletions, pipelines ending in `delete(...)` should include at least one `where(...)` stage. All DML stages must come at the end of the pipeline.

For example, the following pipeline deletes all `users` documents with `address.users` set to `USA` and with `__create_time__` less than 10 days:

##### Node.js

    const pipeline = db.pipeline()
      .collectionGroup("users")
      .where(field("address.country").equal("USA"))
      .where(field("__create_time__").timestampAdd("day", 10).lessThan(currentTimestamp()))
      .delete();
    await pipeline.execute();test.firestore.js

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
    )firestore_pipelines.py

##### Java

    Pipeline.Snapshot deleteResults = firestore.pipeline()
      .collectionGroup("users")
      .where(field("address.country").equal("USA"))
      .where(field("__create_time__").add(constant(10)).lessThan(currentTimestamp()))
      .delete()
      .execute().get();PipelineSnippets.java

## Consistency

Pipeline operations with `update(...)` and `delete()` stages aren't supported within a transaction. DML stages run outside of a transaction with the following behavior:

  - Each document is updated independently. This means operations are not atomic across documents. The operation fails on first error and partial success is possible.
  - The following stages are supported:
      - `collection(...)`
      - `collection_group(...)`
      - `where(...)`
      - `select(...)`
      - `add_fields(...)`
      - `remove_fields(...)`
      - `let(...)`
      - `sort(...)`
      - `limit(...)`
      - `offset(...)`
  - The following are stages are not supported:
      - `aggregate(...)`
      - `distinct(...)`
      - `unnest(...)`
      - `find_nearest(...)`
      - Multi-query stages like `union(...)` , joins, and sub-queries are not allowed before a DML stage.

## Limitations

Note the following limitations for DML stages:

  - DML stages must be the last stages in a pipeline definition before calling `.execute()` .
  - Pipeline operations with `update(...)` and `delete()` stages aren't supported within a transaction.
  - If the stage preceding the DML stage produces multiple documents with the same `__name__` , each instance is processed. For `update(...)` , this means the same target document might be modified multiple times. For `delete(...)` , subsequent attempts after the first will be no-ops.
