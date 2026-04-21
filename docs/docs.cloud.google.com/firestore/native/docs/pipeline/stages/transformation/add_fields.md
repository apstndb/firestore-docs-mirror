# Add Fields (Transformation Stage)

## Description

Add new fields to the documents produced by the previous stage.

The generated documents will contain all the fields from the previous stage along with all newly added fields, overwriting any field that shares the same name from the previous document. The `add_fields(...)` stage allows updating nested fields by specifying a nested field name as the alias.

## Examples

### Web

    const result = await execute(db.pipeline()
      .collection("books")
      .select(field("soldBooks").add(field("unsoldBooks")).as("totalBooks"))
    );test.firestore.js

##### Swift

    let result = try await db.pipeline()
      .collection("books")
      .select([Field("soldBooks").add(Field("unsoldBooks")).as("totalBooks")])
      .execute()PipelineSnippets.swift

##### Kotlin  
Android

    val result = db.pipeline()
        .collection("books")
        .select(Expression.add(field("soldBooks"), field("unsoldBooks")).alias("totalBooks"))
        .execute()DocSnippets.kt

##### Java  
Android

``` 
      Task<Pipeline.Snapshot> result = db.pipeline()
    .collection("books")
    .select(Expression.add(field("soldBooks"), field("unsoldBooks")).alias("totalBooks"))
    .execute();DocSnippets.java
    
```

##### Python

    from google.cloud.firestore_v1.pipeline_expressions import Field
    
    result = (
        client.pipeline()
        .collection("books")
        .select(Field.of("soldBooks").add(Field.of("unsoldBooks")).as_("totalBooks"))
        .execute()
    )firestore_pipelines.py

##### Java

    Pipeline.Snapshot result =
        firestore
            .pipeline()
            .collection("books")
            .select(add(field("soldBooks"), field("unsoldBooks")).as("totalBooks"))
            .execute()
            .get();PipelineSnippets.java

## Behavior

### Overlapping Fields

Assigning an expression an alias that is already in the documents from the previous stage will cause the `add_fields(...)` stage to overwrite the previous field. This can be used to chain up multiple expressions over the same field name, like:

### Node.js

    const results = await db.pipeline()
      .collection("/users")
      .addFields(field('age').abs().as('age'))
      .addFields(field('age').add(10).as('age'))
      .execute();

### Nested Fields

Nested fields (e.g. those with `.` syntax) can be updated as part of this stage. This makes it possible to update a field "in-place" such as in:

### Node.js

    const results = await db.pipeline()
      .collection("/users")
      .addFields(field('address.city').toLower().as('address.city'))
      .execute();

Assigning an expression to a nested field will implicitly create any missing parent fields as well.
