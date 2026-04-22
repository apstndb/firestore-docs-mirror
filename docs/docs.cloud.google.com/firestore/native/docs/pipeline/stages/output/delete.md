# Delete (Output Stage)

> **Preview**
> 
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

The `delete()` stage deletes all documents in the output of the preceding stage.

## Examples

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

## Behavior

All data manipulation language (DML) stages must come at the end of the pipeline. The documents coming into this stage must include the `__name__` field to identify which documents to delete. Most Input stages (like [`collection(...)`](https://docs.cloud.google.com/firestore/native/docs/pipeline/stages/input/collection) , [`collection_group(...)`](https://docs.cloud.google.com/firestore/native/docs/pipeline/stages/input/collection_group) , [`database(...)`](https://docs.cloud.google.com/firestore/native/docs/pipeline/stages/input/database) , and [`documents(...)`](https://docs.cloud.google.com/firestore/native/docs/pipeline/stages/input/documents) ) include the `__name__` field by default.

The response includes a summary of the number of documents modified. For example, the following response confirms that the pipeline modified three documents:

    {documents_modified: 3L}

## Limitations

  - DML stages don't support Firestore Security Rules. DML operation attempts through Firestore Security Rules are denied.

  - During the Preview for this feature, you cannot run DML stages in a transaction. For more information on consistency behavior see [Consistency](https://docs.cloud.google.com/firestore/native/docs/pipeline/dml#consistency) .

  - If the stage preceding the DML stage produces multiple documents with the same `__name__` , each instance is processed. For `update(...)` , this means the same target document might be modified multiple times. For `delete(...)` , subsequent attempts after the first will be no-ops.
