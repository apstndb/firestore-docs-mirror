# Database (Input Stage)

**Preview — Firestore in Native mode (with Pipeline Operations) for Enterprise Edition**

This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](/terms/service-terms#1) . You can process personal data for this feature as outlined in the [Cloud Data Processing Addendum](/terms/data-processing-addendum) , subject to the obligations and restrictions described in the agreement under which you access Google Cloud. Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

## Description

Returns all the documents within a database across different collections and nested levels.

## Syntax

### Node.js

``` text
const results = await db.pipeline()
  .database()
  .execute();
```

## Client examples

### Web

``` javascript
// Count all documents in the database
const results = await execute(db.pipeline()
  .database()
  .aggregate(countAll().as("total"))
  );test.firestore.js
```

##### Swift

``` swift
// Count all documents in the database
let results = try await db.pipeline()
  .database()
  .aggregate([CountAll().as("total")])
  .execute()PipelineSnippets.swift
```

##### Kotlin  
Android

``` kotlin
// Count all documents in the database
val results = db.pipeline()
    .database()
    .aggregate(AggregateFunction.countAll().alias("total"))
    .execute()DocSnippets.kt
```

##### Java  
Android

``` text
// Count all documents in the database
Task<Pipeline.Snapshot> results = db.pipeline()
    .database()
    .aggregate(AggregateFunction.countAll().alias("total"))
    .execute();DocSnippets.java
```

##### Python

``` python
from google.cloud.firestore_v1.pipeline_expressions import Count

# Count all documents in the database
results = client.pipeline().database().aggregate(Count().as_("total")).execute()firestore_pipelines.py
```

##### Java

``` java
// Count all documents in the database
Pipeline.Snapshot results =
    firestore.pipeline().database().aggregate(countAll().as("total")).execute().get();PipelineSnippets.java
```

## Behavior

In order to use the `  database  ` stage, it must appear as the first stage in the pipeline.

The order of documents returned from the `  database  ` stage is unstable and shouldn't be relied upon. A subsequent sort stage can be used to obtain a deterministic ordering.

For example, for the following documents:

### Node.js

``` text
await db.collection('cities').doc('SF').set({name: 'San Francsico', state: 'California', population: 800000});
await db.collection('states').doc('CA').set({name: 'California', population: 39000000});
await db.collection('countries').doc('USA').set({name: 'United States of America', population: 340000000});
```

The `  database  ` stage can be used to retrieve all the documents in the database.

### Node.js

``` text
const results = await db.pipeline()
  .database()
  .sort(field('population').ascending())
  .execute();
```

This query produces the following documents:

``` text
  {name: 'San Francsico', state: 'California', population: 800000}
  {name: 'California', population: 39000000}
  {name: 'United States of America', population: 340000000}
```
