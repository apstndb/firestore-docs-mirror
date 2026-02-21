# Add Fields (Transformation Stage)

**Preview — Firestore in Native mode (with Pipeline Operations) for Enterprise Edition**

This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](/terms/service-terms#1) . You can process personal data for this feature as outlined in the [Cloud Data Processing Addendum](/terms/data-processing-addendum) , subject to the obligations and restrictions described in the agreement under which you access Google Cloud. Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

## Description

Add new fields to the documents produced by the previous stage.

The generated documents will contain all the fields from the previous stage along with all newly added fields, overwriting any field that shares the same name from the previous document.

## Syntax

### Node.js

``` text
const results = await db.pipeline()
  .collection("/users")
  .addFields(field('first_name').concat(' ', field('last_name')).as('full_name'))
  .execute();
```

## Client examples

### Web

``` javascript
const result = await execute(db.pipeline()
  .collection("books")
  .select(field("soldBooks").add(field("unsoldBooks")).as("totalBooks"))
);test.firestore.js
```

##### Swift

``` swift
let result = try await db.pipeline()
  .collection("books")
  .select([Field("soldBooks").add(Field("unsoldBooks")).as("totalBooks")])
  .execute()PipelineSnippets.swift
```

##### Kotlin  
Android

``` kotlin
val result = db.pipeline()
    .collection("books")
    .select(Expression.add(field("soldBooks"), field("unsoldBooks")).alias("totalBooks"))
    .execute()DocSnippets.kt
```

##### Java  
Android

``` text
Task<Pipeline.Snapshot> result = db.pipeline()
    .collection("books")
    .select(Expression.add(field("soldBooks"), field("unsoldBooks")).alias("totalBooks"))
    .execute();DocSnippets.java
```

##### Python

``` python
from google.cloud.firestore_v1.pipeline_expressions import Field

result = (
    client.pipeline()
    .collection("books")
    .select(Field.of("soldBooks").add(Field.of("unsoldBooks")).as_("totalBooks"))
    .execute()
)firestore_pipelines.py
```

##### Java

``` java
Pipeline.Snapshot result =
    firestore
        .pipeline()
        .collection("books")
        .select(add(field("soldBooks"), field("unsoldBooks")).as("totalBooks"))
        .execute()
        .get();PipelineSnippets.java
```

## Behavior

### Overlapping Fields

Assigning an expression an alias that is already in the documents from the previous stage will cause the `  add_fields(...)  ` stage to overwrite the previous field.

This can be used to chain up multiple expressions over the same field name, like:

### Node.js

``` text
const results = await db.pipeline()
  .collection("/users")
  .addFields(field('age').abs().as('age'))
  .addFields(field('age').add(10).as('age'))
  .execute();
```

### Nesting Fields

While the alias assigned to the newly added fields can contain special characters like `  .  ` , these are treated as top-level fields. For example:

### Node.js

``` text
const results = await db.pipeline()
  .collection("/users")
  .addFields(field('address.city').toLower().as('address.city'))
  .execute();
```

adds a new top-level field `  address.city  ` rather than merging the result of the expression back into the nested map under `  address  ` .
