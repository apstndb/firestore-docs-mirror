# Documents (Input Stage)

## Description

Returns documents by looking up a fixed set of predefined documents.

The stage must take one or more documents as input and cannot contain documents with duplicate paths. If a referenced document does not exist, no results will be produced for that document path.

This stage behaves similar to Firestore's `batchGet` and allows filtering on the results directly rather than performing post-filtering steps after the batch operation.

## Examples

### Web

    const results = await execute(db.pipeline()
      .documents([
        doc(db, "cities", "SF"),
        doc(db, "cities", "DC"),
        doc(db, "cities", "NY")
      ])
    );test.firestore.js

##### Swift

    let results = try await db.pipeline()
      .documents([
        db.collection("cities").document("SF"),
        db.collection("cities").document("DC"),
        db.collection("cities").document("NY")
      ]).execute()PipelineSnippets.swift

##### Kotlin  
Android

    val results = db.pipeline()
        .documents(
            db.collection("cities").document("SF"),
            db.collection("cities").document("DC"),
            db.collection("cities").document("NY")
        ).execute()DocSnippets.kt

##### Java  
Android

``` 
      Task<Pipeline.Snapshot> results = db.pipeline()
    .documents(
        db.collection("cities").document("SF"),
        db.collection("cities").document("DC"),
        db.collection("cities").document("NY")
    ).execute();DocSnippets.java
    
```

##### Python

    results = (
        client.pipeline()
        .documents(
            client.collection("cities").document("SF"),
            client.collection("cities").document("DC"),
            client.collection("cities").document("NY"),
        )
        .execute()
    )firestore_pipelines.py

##### Java

    Pipeline.Snapshot results =
        firestore
            .pipeline()
            .documents(
                firestore.collection("cities").document("SF"),
                firestore.collection("cities").document("DC"),
                firestore.collection("cities").document("NY"))
            .execute()
            .get();PipelineSnippets.java

## Behavior

In order to use the `documents(...)` stage, it must appear as the first stage in the pipeline.

The order of documents returned from the `documents(...)` stage is unstable and cannot be relied upon. A subsequent sort stage can be used to obtain a deterministic ordering.

For example, for the following documents:

### Node.js

    await db.collection("cities").doc("SF").set({name: "San Francsico", state: "California"});
    await db.collection("cities").doc("NYC").set({name: "New York City", state: "New York"});
    await db.collection("cities").doc("CHI").set({name: "Chicago", state: "Illinois"});

The `documents(...)` stage can be used to retrieve only the `SF` and `NYC` documents and then sort them in ascending order of name.

### Node.js

    const results = await db.pipeline()
      .documents(
        db.collection("cities").doc("SF"),
        db.collection("cities").doc("NYC"))
      .sort(field("name").ascending())
      .execute();

This query produces the following documents:

``` 
  { name: "New York City", state: "New York" }
  { name: "San Francsico", state: "California" }
```
