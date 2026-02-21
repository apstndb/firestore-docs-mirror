# Union (Transformation Stage)

**Preview — Firestore in Native mode (with Pipeline Operations) for Enterprise Edition**

This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](/terms/service-terms#1) . You can process personal data for this feature as outlined in the [Cloud Data Processing Addendum](/terms/data-processing-addendum) , subject to the obligations and restrictions described in the agreement under which you access Google Cloud. Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

## Description

Merges the documents from another pipeline with those in the current pipeline.

## Syntax

### Node.js

``` text
const results = await db.pipeline()
  .collection("cities/SF/restaurants")
  .union(db.pipeline().collection("cities/NYC/restaurants"))
  .execute();
```

## Client examples

##### Node.js

``` text
  const results = await db.pipeline()
    .collection("cities/SF/restaurants")
    .where(eq("type", "chinese"))
    .union(db.pipeline()
      .collection("cities/NYC/restaurants")
      .where(eq("type", "italian")))
    .where(gte("rating", 4.5))
    .execute();
    
```

### Web

``` javascript
const results = await execute(db.pipeline()
  .collection("cities/SF/restaurants")
  .where(field("type").equal("Chinese"))
  .union(db.pipeline()
    .collection("cities/NY/restaurants")
    .where(field("type").equal("Italian")))
  .where(field("rating").greaterThanOrEqual(4.5))
  .sort(field("__name__").descending())
);test.firestore.js
```

##### Swift

``` swift
let results = try await db.pipeline()
  .collection("cities/SF/restaurants")
  .where(Field("type").equal("Chinese"))
  .union(with: db.pipeline()
    .collection("cities/NY/restaurants")
    .where(Field("type").equal("Italian")))
  .where(Field("rating").greaterThanOrEqual(4.5))
  .sort([Field("__name__").descending()])
  .execute()PipelineSnippets.swift
```

##### Kotlin  
Android

``` kotlin
val results = db.pipeline()
    .collection("cities/SF/restaurants")
    .where(field("type").equal("Chinese"))
    .union(db.pipeline()
        .collection("cities/NY/restaurants")
        .where(field("type").equal("Italian")))
    .where(field("rating").greaterThanOrEqual(4.5))
    .sort(field("__name__").descending())
    .execute()DocSnippets.kt
```

##### Java  
Android

``` text
Task<Pipeline.Snapshot> results = db.pipeline()
    .collection("cities/SF/restaurants")
    .where(field("type").equal("Chinese"))
    .union(db.pipeline()
        .collection("cities/NY/restaurants")
        .where(field("type").equal("Italian")))
    .where(field("rating").greaterThanOrEqual(4.5))
    .sort(field("__name__").descending())
    .execute();DocSnippets.java
```

##### Python

``` python
from google.cloud.firestore_v1.pipeline_expressions import Field

results = (
    client.pipeline()
    .collection("cities/SF/restaurants")
    .where(Field.of("type").equal("Chinese"))
    .union(
        client.pipeline()
        .collection("cities/NY/restaurants")
        .where(Field.of("type").equal("Italian"))
    )
    .where(Field.of("rating").greater_than_or_equal(4.5))
    .sort(Field.of("__name__").descending())
    .execute()
)firestore_pipelines.py
```

##### Java

``` java
Pipeline.Snapshot results =
    firestore
        .pipeline()
        .collection("cities/SF/restaurants")
        .where(field("type").equal("Chinese"))
        .union(
            firestore
                .pipeline()
                .collection("cities/NY/restaurants")
                .where(field("type").equal("Italian")))
        .where(field("rating").greaterThanOrEqual(4.5))
        .sort(descending(field("__name__")))
        .execute()
        .get();PipelineSnippets.java
```

## Behavior

This stage runs multiple pipelines in parallel and concatenates the results together.

### Non-Deterministic Order of Results

The order in which results are combined between the two pipelines is non-deterministic. Any perceived order is unstable and shouldn't be relied upon. A following `  sort  ` stage can be added if a stable order is required.

##### Node.js

``` text
  const results = await db.pipeline()
    .collection("cities/SF/restaurants")
    .where(eq("type", "chinese"))
    .union(db.pipeline()
      .collection("cities/NYC/restaurants")
      .where(eq("type", "italian")))
    .where(gte("rating", 4.5))
    .sort(Field.of("__name__"))
    .execute();
    
```

##### Kotlin  
Android

``` kotlin
val results = db.pipeline()
    .collection("cities/SF/restaurants")
    .where(field("type").equal("Chinese"))
    .union(db.pipeline()
        .collection("cities/NY/restaurants")
        .where(field("type").equal("Italian")))
    .where(field("rating").greaterThanOrEqual(4.5))
    .sort(field("__name__").descending())
    .execute()DocSnippets.kt
```

##### Java  
Android

``` text
Task<Pipeline.Snapshot> results = db.pipeline()
    .collection("cities/SF/restaurants")
    .where(field("type").equal("Chinese"))
    .union(db.pipeline()
        .collection("cities/NY/restaurants")
        .where(field("type").equal("Italian")))
    .where(field("rating").greaterThanOrEqual(4.5))
    .sort(field("__name__").descending())
    .execute();DocSnippets.java
```

##### Python

``` python
from google.cloud.firestore_v1.pipeline_expressions import Field

results = (
    client.pipeline()
    .collection("cities/SF/restaurants")
    .where(Field.of("type").equal("Chinese"))
    .union(
        client.pipeline()
        .collection("cities/NY/restaurants")
        .where(Field.of("type").equal("Italian"))
    )
    .where(Field.of("rating").greater_than_or_equal(4.5))
    .sort(Field.of("__name__").descending())
    .execute()
)firestore_pipelines.py
```

##### Java

``` java
Pipeline.Snapshot results =
    firestore
        .pipeline()
        .collection("cities/SF/restaurants")
        .where(field("type").equal("Chinese"))
        .union(
            firestore
                .pipeline()
                .collection("cities/NY/restaurants")
                .where(field("type").equal("Italian")))
        .where(field("rating").greaterThanOrEqual(4.5))
        .sort(descending(field("__name__")))
        .execute()
        .get();PipelineSnippets.java
```

### Duplicate Results

The `  union  ` stage does not deduplicate results. A following `  distinct  ` or `  aggregate  ` stage can be added if duplicate results need to be removed.
