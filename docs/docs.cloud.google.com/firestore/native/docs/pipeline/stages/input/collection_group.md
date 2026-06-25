---
name: documents/docs.cloud.google.com/firestore/native/docs/pipeline/stages/input/collection_group
uri: https://docs.cloud.google.com/firestore/native/docs/pipeline/stages/input/collection_group
title: Collection Group (Input Stage)
description: Describes how to use the collection_group stage in Firestore Pipeline Operations. Covers returning all documents from a given collection ID, regardless of its parent.
data_source: docs.cloud.google.com
---

# Collection Group (Input Stage)

## Description

Returns all documents from any collection with the specified collection ID, regardless of its parent.

## Examples

### Web

    const results = await execute(db.pipeline()
      .collectionGroup("games")
      .sort(field("name").ascending())
      );

##### Swift

    let results = try await db.pipeline()
      .collectionGroup("games")
      .sort([Field("name").ascending()])
      .execute()

##### Kotlin  
Android

    val results = db.pipeline()
        .collectionGroup("games")
        .sort(field("name").ascending())
        .execute()

##### Java  
Android

``` 
      Task<Pipeline.Snapshot> results = db.pipeline()
    .collectionGroup("games")
    .sort(field("name").ascending())
    .execute();
    
```

##### Python

    from google.cloud.firestore_v1.pipeline_expressions import Field
    
    results = (
        client.pipeline()
        .collection_group("games")
        .sort(Field.of("name").ascending())
        .execute()
    )

##### Java

    Pipeline.Snapshot results =
        firestore
            .pipeline()
            .collectionGroup("games")
            .sort(ascending(field("name")))
            .execute()
            .get();

##### Go

    snapshot := client.Pipeline().
     CollectionGroup("games").
     Sort(firestore.Orders(firestore.Ascending(firestore.FieldOf("name")))).
     Execute(ctx)

## Behavior

In order to use the `collection_group(...)` stage, it must appear as the first stage in the pipeline.

The order of documents returned from the `collection_group(...)` stage is unstable and cannot be relied upon. Firestore will attempt to execute the query in the most efficient way possible, which can change the order depending on the schema or index configuration. A subsequent [`sort(...)`](https://docs.cloud.google.com/firestore/native/docs/pipeline/stages/transformation/sort) stage can be used to obtain a deterministic ordering.

For example, for the following documents:

### Node.js

    await db.collection("cities/SF/departments").doc("building").set({name: "SF Building Deparment", employees: 750});
    await db.collection("cities/NY/departments").doc("building").set({name: "NY Building Deparment", employees: 1000});
    await db.collection("cities/CHI/departments").doc("building").set({name: "CHI Building Deparment", employees: 900});
    await db.collection("cities/NY/departments").doc("finance").set({name: "NY Finance Deparment", employees: 1200});

The `collection_group(...)` stage can be used to return documents from every departments collection across all parent collections in the database.

### Node.js

    const results = await db.pipeline()
      .collectionGroup("departments")
      .sort(field("employees").ascending())
      .execute();

This query produces the following documents:

``` 
  { name: "SF Building Deparment", employees: 750 }
  { name: "CHI Building Deparment", employees: 900 }
  { name: "NY Building Deparment", employees: 1000 }
  { name: "NY Finance Deparment", employees: 1200 }
```
