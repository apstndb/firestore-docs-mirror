# Offset (Transformation Stage)

**Preview — Firestore in Native mode (with Pipeline Operations) for Enterprise Edition**

This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](/terms/service-terms#1) . You can process personal data for this feature as outlined in the [Cloud Data Processing Addendum](/terms/data-processing-addendum) , subject to the obligations and restrictions described in the agreement under which you access Google Cloud. Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

## Description

Skips the first `  N  ` input documents.

## Syntax

### Node.js

``` text
const results = await db.pipeline()
  .collection("/cities")
  .offset(10)
  .execute();
```

## Client examples

##### Node.js

``` javascript
const results = await db.pipeline()
  .collection("cities")
  .offset(10)
  .execute();test.firestore.js
```

### Web

``` javascript
const results = await execute(db.pipeline()
  .collection("cities")
  .offset(10));test.firestore.js
```

##### Swift

``` swift
let results = try await db.pipeline()
  .collection("cities")
  .offset(10)
  .execute()PipelineSnippets.swift
```

##### Kotlin  
Android

``` kotlin
val results = db.pipeline()
    .collection("cities")
    .offset(10)
    .execute()DocSnippets.kt
```

##### Java  
Android

``` text
Task<Pipeline.Snapshot> results = db.pipeline()
        .collection("cities")
        .offset(10)
        .execute();DocSnippets.java
```

##### Python

``` python
results = client.pipeline().collection("cities").offset(10).execute()firestore_pipelines.py
```

##### Java

``` java
Pipeline.Snapshot results =
    firestore.pipeline().collection("cities").offset(10).execute().get();PipelineSnippets.java
```

## Behavior

The `  offset  ` stage will skip the first `  N  ` input documents. Unless a `  sort  ` stage is used before the offset, the order in which documents are returned is unstable and repeated executions might produce different results.
