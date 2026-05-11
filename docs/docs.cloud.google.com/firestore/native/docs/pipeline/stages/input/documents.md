---
name: documents/docs.cloud.google.com/firestore/native/docs/pipeline/stages/input/documents
uri: https://docs.cloud.google.com/firestore/native/docs/pipeline/stages/input/documents
title: Documents (Input Stage)
description: Describes how to use the documents stage in Firestore Pipeline Operations. Covers returning documents by looking up a fixed set of predefined documents.
data_source: docs.cloud.google.com
---

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
    );

##### Swift

    let results = try await db.pipeline()
      .documents([
        db.collection("cities").document("SF"),
        db.collection("cities").document("DC"),
        db.collection("cities").document("NY")
      ]).execute()

##### Kotlin  
Android

    val results = db.pipeline()
        .documents(
            db.collection("cities").document("SF"),
            db.collection("cities").document("DC"),
            db.collection("cities").document("NY")
        ).execute()

##### Java  
Android

``` 
      Task<Pipeline.Snapshot> results = db.pipeline()
    .documents(
        db.collection("cities").document("SF"),
        db.collection("cities").document("DC"),
        db.collection("cities").document("NY")
    ).execute();
    
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
    )

##### Java

    Pipeline.Snapshot results =
        firestore
            .pipeline()
            .documents(
                firestore.collection("cities").document("SF"),
                firestore.collection("cities").document("DC"),
                firestore.collection("cities").document("NY"))
            .execute()
            .get();

## Behavior

In order to use the `documents(...)` stage, it must appear as the first stage in the pipeline.

The order of documents returned from the `documents(...)` stage is unstable and cannot be relied upon. A subsequent [`sort(...)`](https://docs.cloud.google.com/firestore/native/docs/pipeline/stages/transformation/sort) stage can be used to obtain a deterministic ordering.

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
