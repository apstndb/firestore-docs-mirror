---
name: documents/docs.cloud.google.com/firestore/native/docs/pipeline/stages/transformation/remove_fields
uri: https://docs.cloud.google.com/firestore/native/docs/pipeline/stages/transformation/remove_fields
title: Remove Fields (Transformation Stage)
description: Describes how to use the remove_fields stage in Firestore Pipeline Operations. Covers removing fields from the documents produced by the previous stage.
data_source: docs.cloud.google.com
update_time: "2026-05-09T10:46:16Z"
---

# Remove Fields (Transformation Stage)

## Description

Remove fields from the documents produced by the previous stage.

The generated documents will contain all fields from the previous stage except for the fields specified to be removed.

## Examples

##### Node.js

    const results = await db.pipeline()
      .collection("cities")
      .removeFields("population", "location.state")
      .execute();

### Web

    const results = await execute(db.pipeline()
      .collection("cities")
      .removeFields("population", "location.state"));

##### Swift

    let results = try await db.pipeline()
      .collection("cities")
      .removeFields(["population", "location.state"])
      .execute()

##### Kotlin  
Android

    val results = db.pipeline()
        .collection("cities")
        .removeFields("population", "location.state")
        .execute()

##### Java  
Android

    Task<Pipeline.Snapshot> results = db.pipeline()
            .collection("cities")
            .removeFields("population", "location.state")
            .execute();

##### Python

    results = (
        client.pipeline()
        .collection("cities")
        .remove_fields("population", "location.state")
        .execute()
    )

##### Java

    Pipeline.Snapshot results =
        firestore
            .pipeline()
            .collection("cities")
            .removeFields("population", "location.state")
            .execute()
            .get();

## Behavior

### Remove Nested Fields

The `remove_fields(...)` stage respects nested field syntax, and will remove keys from a map.

For example, to remove the nested state field from the dataset:

### Node.js

    await db.collection("cities").doc("SF").set({name: "San Francisco", location: {country: "USA", state: "California"}});
    await db.collection("cities").doc("TO").set({name: "Toronto", location: {country: "Canada", province: "Ontario"}});

The following pipeline can be used:

### Node.js

    const results = await db.pipeline()
      .collection("/cities")
      .removeFields("location.state")
      .execute();

Which produces the following documents:

    { name: "San Francisco", location: { country: "USA" } }
    { name: "Toronto", location: { country: "Canada", province: "Ontario" } }

Removal of elements within an array is unsupported.

### Remove on Non-Existent Fields

If a nested or top-level field given to `remove_fields(...)` does not exist in a document, the stage won't edit the document for that field. Other existing fields will still be removed.
