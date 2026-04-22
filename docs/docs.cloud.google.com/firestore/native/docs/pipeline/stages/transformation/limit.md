# Limit (Transformation Stage)

## Description

Limits the number of documents returned by the pipeline.

## Examples

### Web

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

##### Swift

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

##### Kotlin  
Android

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

##### Java  
Android

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

##### Python

    from google.cloud.firestore_v1.pipeline_expressions import Field
    
    pipeline = (
        client.pipeline()
        .collection("cities")
        .where(Field.of("population").greater_than(100_000))
        .sort(Field.of("name").ascending())
        .limit(10)
    )firestore_pipelines.py

##### Java

    Pipeline pipeline =
        firestore
            .pipeline()
            .collection("cities")
            .where(field("population").greaterThan(100_000))
            .sort(ascending(field("name")))
            .limit(10);PipelineSnippets.java

## Behavior

The `limit(...)` stage will only return the first `N` documents. Unless a [`sort(...)`](https://docs.cloud.google.com/firestore/native/docs/pipeline/stages/transformation/sort) stage is used before the limit, the order in which documents are returned is unstable and repeated executions may produce different results.
