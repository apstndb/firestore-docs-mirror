# Offset (Transformation Stage)

**Preview — Firestore in Native mode (with Pipeline Operations) for Enterprise Edition**

This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . You can process personal data for this feature as outlined in the [Cloud Data Processing Addendum](https://docs.cloud.google.com/terms/data-processing-addendum) , subject to the obligations and restrictions described in the agreement under which you access Google Cloud. Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

## Description

Skips the first `  N  ` input documents.

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

The `  offset(...)  ` stage will skip the first `  N  ` input documents. Unless a `  sort(...)  ` stage is used before the offset, the order in which documents are returned is unstable and repeated executions might produce different results.
