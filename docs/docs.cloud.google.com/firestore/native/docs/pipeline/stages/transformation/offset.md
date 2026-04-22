# Offset (Transformation Stage)

## Description

Skips the first `N` input documents.

## Examples

##### Node.js

    const results = await db.pipeline()
      .collection("cities")
      .offset(10)
      .execute();test.firestore.js

### Web

    const results = await execute(db.pipeline()
      .collection("cities")
      .offset(10));test.firestore.js

##### Swift

    let results = try await db.pipeline()
      .collection("cities")
      .offset(10)
      .execute()PipelineSnippets.swift

##### Kotlin  
Android

    val results = db.pipeline()
        .collection("cities")
        .offset(10)
        .execute()DocSnippets.kt

##### Java  
Android

    Task<Pipeline.Snapshot> results = db.pipeline()
            .collection("cities")
            .offset(10)
            .execute();DocSnippets.java

##### Python

    results = client.pipeline().collection("cities").offset(10).execute()firestore_pipelines.py

##### Java

    Pipeline.Snapshot results =
        firestore.pipeline().collection("cities").offset(10).execute().get();PipelineSnippets.java

## Behavior

The `offset(...)` stage will skip the first `N` input documents. Unless a [`sort(...)`](https://docs.cloud.google.com/firestore/native/docs/pipeline/stages/transformation/sort) stage is used before the offset, the order in which documents are returned is unstable and repeated executions might produce different results.
