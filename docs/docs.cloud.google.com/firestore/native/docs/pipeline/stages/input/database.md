# Database (Input Stage)

## Description

Returns all the documents within a database across different collections and nested levels.

## Examples

### Web

    // Count all documents in the database
    const results = await execute(db.pipeline()
      .database()
      .aggregate(countAll().as("total"))
      );test.firestore.js

##### Swift

    // Count all documents in the database
    let results = try await db.pipeline()
      .database()
      .aggregate([CountAll().as("total")])
      .execute()PipelineSnippets.swift

##### Kotlin  
Android

    // Count all documents in the database
    val results = db.pipeline()
        .database()
        .aggregate(AggregateFunction.countAll().alias("total"))
        .execute()DocSnippets.kt

##### Java  
Android

``` 
      // Count all documents in the database
Task<Pipeline.Snapshot> results = db.pipeline()
    .database()
    .aggregate(AggregateFunction.countAll().alias("total"))
    .execute();DocSnippets.java
    
```

##### Python

    from google.cloud.firestore_v1.pipeline_expressions import Count
    
    # Count all documents in the database
    results = client.pipeline().database().aggregate(Count().as_("total")).execute()firestore_pipelines.py

##### Java

    // Count all documents in the database
    Pipeline.Snapshot results =
        firestore.pipeline().database().aggregate(countAll().as("total")).execute().get();PipelineSnippets.java

## Behavior

In order to use the `database(...)` stage, it must appear as the first stage in the pipeline.

The order of documents returned from the `database(...)` stage is unstable and cannot be relied upon. A subsequent [`sort(...)`](https://docs.cloud.google.com/firestore/native/docs/pipeline/stages/transformation/sort) stage can be used to obtain a deterministic ordering.

For example, for the following documents:

### Node.js

    await db.collection("cities").doc("SF").set({name: "San Francsico", state: "California", population: 800000});
    await db.collection("states").doc("CA").set({name: "California", population: 39000000});
    await db.collection("countries").doc("USA").set({name: "United States of America", population: 340000000});

The `database(...)` stage can be used to retrieve all the documents in the database.

### Node.js

    const results = await db.pipeline()
      .database()
      .sort(field("population").ascending())
      .execute();

This query produces the following documents:

``` 
  { name: "San Francsico", state: "California", population: 800000 }
  { name: "California", population: 39000000 }
  { name: "United States of America", population: 340000000 }
```
