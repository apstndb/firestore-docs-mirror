# Documents (Input Stage)

**Preview — Firestore in Native mode (with Pipeline Operations) for Enterprise Edition**

This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](/terms/service-terms#1) . You can process personal data for this feature as outlined in the [Cloud Data Processing Addendum](/terms/data-processing-addendum) , subject to the obligations and restrictions described in the agreement under which you access Google Cloud. Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

## Description

Returns documents by looking up a fixed set of predefined documents.

The stage must take one or more documents as input and cannot contain documents with duplicate paths. If a referenced document does not exist, no results will be produced for that document path.

This stage behaves similar to Firestore's `  batchGet  ` and allows filtering on the results directly rather than performing post-filtering steps after the batch operation.

## Syntax

### Node.js

``` text
const results = await db.pipeline()
  .documents(
    db.collection("cities").doc("SF"),
    db.collection("cities").doc("NY"))
  .execute();
```

## Client examples

### Web

``` javascript
const results = await execute(db.pipeline()
  .documents([
    doc(db, "cities", "SF"),
    doc(db, "cities", "DC"),
    doc(db, "cities", "NY")
  ])
);test.firestore.js
```

##### Swift

``` swift
let results = try await db.pipeline()
  .documents([
    db.collection("cities").document("SF"),
    db.collection("cities").document("DC"),
    db.collection("cities").document("NY")
  ]).execute()PipelineSnippets.swift
```

##### Kotlin  
Android

``` kotlin
val results = db.pipeline()
    .documents(
        db.collection("cities").document("SF"),
        db.collection("cities").document("DC"),
        db.collection("cities").document("NY")
    ).execute()DocSnippets.kt
```

##### Java  
Android

``` text
Task<Pipeline.Snapshot> results = db.pipeline()
    .documents(
        db.collection("cities").document("SF"),
        db.collection("cities").document("DC"),
        db.collection("cities").document("NY")
    ).execute();DocSnippets.java
```

##### Python

``` python
results = (
    client.pipeline()
    .documents(
        client.collection("cities").document("SF"),
        client.collection("cities").document("DC"),
        client.collection("cities").document("NY"),
    )
    .execute()
)firestore_pipelines.py
```

##### Java

``` java
Pipeline.Snapshot results =
    firestore
        .pipeline()
        .documents(
            firestore.collection("cities").document("SF"),
            firestore.collection("cities").document("DC"),
            firestore.collection("cities").document("NY"))
        .execute()
        .get();PipelineSnippets.java
```

## Behavior

In order to use the `  documents  ` stage, it must appear as the first stage in the pipeline.

The order of documents returned from the `  documents  ` stage is unstable and shouldn't be relied upon. A subsequent sort stage can be used to obtain a deterministic ordering.

For example, for the following documents:

### Node.js

``` text
await db.collection('cities').doc('SF').set({name: 'San Francsico', state: 'California'});
await db.collection('cities').doc('NYC').set({name: 'New York City', state: 'New York'});
await db.collection('cities').doc('CHI').set({name: 'Chicago', state: 'Illinois'});
```

The `  documents  ` stage can be used to retrieve only the `  SF  ` and `  NYC  ` documents and then sort them in ascending order of name.

### Node.js

``` text
const results = await db.pipeline()
  .documents(
    db.collection('cities').doc('SF'),
    db.collection('cities').doc('NYC'))
  .sort(field("name").ascending())
  .execute();
```

This query produces the following documents:

``` text
  {name: 'New York City', state: 'New York'}
  {name: 'San Francsico', state: 'California'}
```
