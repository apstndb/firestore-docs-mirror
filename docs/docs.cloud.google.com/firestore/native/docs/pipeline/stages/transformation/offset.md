---
name: documents/docs.cloud.google.com/firestore/native/docs/pipeline/stages/transformation/offset
uri: https://docs.cloud.google.com/firestore/native/docs/pipeline/stages/transformation/offset
title: Offset (Transformation Stage)
description: Describes how to use the offset stage in Firestore Pipeline Operations. Covers skipping the first N documents produced from the previous stage.
data_source: docs.cloud.google.com
---

# Offset (Transformation Stage)

## Description

Skips the first `N` input documents.

## Examples

##### Node.js

    const results = await db.pipeline()
      .collection("cities")
      .offset(10)
      .execute();

### Web

    const results = await execute(db.pipeline()
      .collection("cities")
      .offset(10));

##### Swift

    let results = try await db.pipeline()
      .collection("cities")
      .offset(10)
      .execute()

##### Kotlin  
Android

    val results = db.pipeline()
        .collection("cities")
        .offset(10)
        .execute()

##### Java  
Android

    Task<Pipeline.Snapshot> results = db.pipeline()
            .collection("cities")
            .offset(10)
            .execute();

##### Python

    results = client.pipeline().collection("cities").offset(10).execute()

##### Java

    Pipeline.Snapshot results =
        firestore.pipeline().collection("cities").offset(10).execute().get();

##### Go

    snapshot := client.Pipeline().Collection("cities").Offset(10).Execute(ctx)

## Behavior

The `offset(...)` stage will skip the first `N` input documents. Unless a [`sort(...)`](https://docs.cloud.google.com/firestore/native/docs/pipeline/stages/transformation/sort) stage is used before the offset, the order in which documents are returned is unstable and repeated executions might produce different results.
