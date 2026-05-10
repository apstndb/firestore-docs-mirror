---
name: documents/docs.cloud.google.com/firestore/native/docs/pipeline/stages/transformation/union
uri: https://docs.cloud.google.com/firestore/native/docs/pipeline/stages/transformation/union
title: Union (Transformation Stage)
description: Describes how to use the union stage in Firestore Pipeline Operations. Covers merging the documents from another pipeline with those in the current pipeline.
data_source: docs.cloud.google.com
update_time: "2026-05-09T06:58:59Z"
---

# Union (Transformation Stage)

## Description

Merges the documents from another pipeline with those in the current pipeline.

## Examples

##### Node.js

``` 
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

    const results = await execute(db.pipeline()
      .collection("cities/SF/restaurants")
      .where(field("type").equal("Chinese"))
      .union(db.pipeline()
        .collection("cities/NY/restaurants")
        .where(field("type").equal("Italian")))
      .where(field("rating").greaterThanOrEqual(4.5))
      .sort(field("__name__").descending())
    );

##### Swift

    let results = try await db.pipeline()
      .collection("cities/SF/restaurants")
      .where(Field("type").equal("Chinese"))
      .union(with: db.pipeline()
        .collection("cities/NY/restaurants")
        .where(Field("type").equal("Italian")))
      .where(Field("rating").greaterThanOrEqual(4.5))
      .sort([Field("__name__").descending()])
      .execute()

##### Kotlin  
Android

    val results = db.pipeline()
        .collection("cities/SF/restaurants")
        .where(field("type").equal("Chinese"))
        .union(db.pipeline()
            .collection("cities/NY/restaurants")
            .where(field("type").equal("Italian")))
        .where(field("rating").greaterThanOrEqual(4.5))
        .sort(field("__name__").descending())
        .execute()

##### Java  
Android

    Task<Pipeline.Snapshot> results = db.pipeline()
        .collection("cities/SF/restaurants")
        .where(field("type").equal("Chinese"))
        .union(db.pipeline()
            .collection("cities/NY/restaurants")
            .where(field("type").equal("Italian")))
        .where(field("rating").greaterThanOrEqual(4.5))
        .sort(field("__name__").descending())
        .execute();

##### Python

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
    )

##### Java

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
            .get();

## Behavior

This stage runs multiple pipelines in parallel and concatenates the results together.

### Non-Deterministic Order of Results

The order in which results are combined between the two pipelines is non-deterministic. Any perceived order is unstable and shouldn't be relied upon. A following [`sort(...)`](https://docs.cloud.google.com/firestore/native/docs/pipeline/stages/transformation/sort) stage can be added if a stable order is required.

##### Node.js

``` 
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

    val results = db.pipeline()
        .collection("cities/SF/restaurants")
        .where(field("type").equal("Chinese"))
        .union(db.pipeline()
            .collection("cities/NY/restaurants")
            .where(field("type").equal("Italian")))
        .where(field("rating").greaterThanOrEqual(4.5))
        .sort(field("__name__").descending())
        .execute()

##### Java  
Android

    Task<Pipeline.Snapshot> results = db.pipeline()
        .collection("cities/SF/restaurants")
        .where(field("type").equal("Chinese"))
        .union(db.pipeline()
            .collection("cities/NY/restaurants")
            .where(field("type").equal("Italian")))
        .where(field("rating").greaterThanOrEqual(4.5))
        .sort(field("__name__").descending())
        .execute();

##### Python

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
    )

##### Java

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
            .get();

### Duplicate Results

The `union(...)` stage does not deduplicate results. A following [`distinct(...)`](https://docs.cloud.google.com/firestore/native/docs/pipeline/stages/transformation/distinct) or [`aggregate(...)`](https://docs.cloud.google.com/firestore/native/docs/pipeline/stages/transformation/aggregate) stage can be added if duplicate results need to be removed.
