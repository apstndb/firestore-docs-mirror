# Limit (Transformation Stage)

**Preview — Firestore in Native mode (with Pipeline Operations) for Enterprise Edition**

This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](/terms/service-terms#1) . You can process personal data for this feature as outlined in the [Cloud Data Processing Addendum](/terms/data-processing-addendum) , subject to the obligations and restrictions described in the agreement under which you access Google Cloud. Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

## Description

Limits the number of documents returned by the pipeline.

## Syntax

### Node.js

``` text
const results = await db.pipeline()
  .collection("/cities")
  .limit(10)
  .execute();
```

## Client examples

### Web

``` javascript
const pipeline = db.pipeline()
  // Step 1: Start a query with collection scope
  .collection("cities")
  // Step 2: Filter the collection
  .where(field("population").greaterThan(100000))
  // Step 3: Sort the remaining documents
  .sort(field("name").ascending())
  // Step 4: Return the top 10. Note applying the limit earlier in the
  // pipeline would have unintentional results.
  .limit(10);test.firestore.js
```

##### Swift

``` swift
let pipeline = db.pipeline()
  // Step 1: Start a query with collection scope
  .collection("cities")
  // Step 2: Filter the collection
  .where(Field("population").greaterThan(100000))
  // Step 3: Sort the remaining documents
  .sort([Field("name").ascending()])
  // Step 4: Return the top 10. Note applying the limit earlier in the pipeline would have
  // unintentional results.
  .limit(10)PipelineSnippets.swift
```

##### Kotlin  
Android

``` kotlin
val pipeline = db.pipeline()
    // Step 1: Start a query with collection scope
    .collection("cities")
    // Step 2: Filter the collection
    .where(field("population").greaterThan(100000))
    // Step 3: Sort the remaining documents
    .sort(field("name").ascending())
    // Step 4: Return the top 10. Note applying the limit earlier in the pipeline would have
    // unintentional results.
    .limit(10)DocSnippets.kt
```

##### Java  
Android

``` text
Pipeline pipeline = db.pipeline()
    // Step 1: Start a query with collection scope
    .collection("cities")
    // Step 2: Filter the collection
    .where(field("population").greaterThan(100000))
    // Step 3: Sort the remaining documents
    .sort(field("name").ascending())
    // Step 4: Return the top 10. Note applying the limit earlier in the pipeline would have
    // unintentional results.
    .limit(10);DocSnippets.java
```

##### Python

``` python
from google.cloud.firestore_v1.pipeline_expressions import Field

pipeline = (
    client.pipeline()
    .collection("cities")
    .where(Field.of("population").greater_than(100_000))
    .sort(Field.of("name").ascending())
    .limit(10)
)firestore_pipelines.py
```

##### Java

``` java
Pipeline pipeline =
    firestore
        .pipeline()
        .collection("cities")
        .where(field("population").greaterThan(100_000))
        .sort(ascending(field("name")))
        .limit(10);PipelineSnippets.java
```

## Behavior

The `  limit  ` stage will only return the first `  N  ` documents. Unless a `  sort  ` stage is used before the limit, the order in which documents are returned is unstable and repeated executions may produce different results.
