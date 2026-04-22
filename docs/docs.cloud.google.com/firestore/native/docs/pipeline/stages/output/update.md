# Update (Output Stage)

> **Preview**
> 
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

The `update(...)` stage updates existing documents.

## Examples

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

## Behavior

All data manipulation language (DML) stages must come at the end of the pipeline.

The documents coming into this stage must include the `__name__` field to identify which documents to update. The operation fails if any of the documents don't exist. Most Input stages (like [`collection(...)`](https://docs.cloud.google.com/firestore/native/docs/pipeline/stages/input/collection) , [`collection_group(...)`](https://docs.cloud.google.com/firestore/native/docs/pipeline/stages/input/collection_group) , [`database(...)`](https://docs.cloud.google.com/firestore/native/docs/pipeline/stages/input/database) , and [`documents(...)`](https://docs.cloud.google.com/firestore/native/docs/pipeline/stages/input/documents) ) include the `__name__` field by default.

You can optionally provide `transformations` to apply right before writing the documents. These act identically to adding an [`add_fields(...)`](https://docs.cloud.google.com/firestore/native/docs/pipeline/stages/transformation/add_fields) right before the final output stage and the expressions run in the context of the previous documents.

The response includes a summary of the number of documents modified. For example, the following response confirms that the pipeline modified three documents:

    {documents_modified: 3L}

## Limitations

  - DML stages don't support Firestore Security Rules. DML operation attempts through Firestore Security Rules are denied.

  - During the Preview for this feature, you cannot run DML stages in a transaction. For more information on consistency behavior see [Consistency](https://docs.cloud.google.com/firestore/native/docs/pipeline/dml#consistency) .

  - If the stage preceding the DML stage produces multiple documents with the same `__name__` , each instance is processed. For `update(...)` , this means the same target document might be modified multiple times. For `delete(...)` , subsequent attempts after the first will be no-ops.
