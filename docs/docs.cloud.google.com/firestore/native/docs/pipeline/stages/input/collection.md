# Collection (Input Stage)

**Preview — Firestore in Native mode (with Pipeline Operations) for Enterprise Edition**

This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](/terms/service-terms#1) . You can process personal data for this feature as outlined in the [Cloud Data Processing Addendum](/terms/data-processing-addendum) , subject to the obligations and restrictions described in the agreement under which you access Google Cloud. Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

## Description

Returns all documents from a given collection. The collection can be nested.

## Syntax

### Node.js

``` text
const results = await db.pipeline()
  .collection('/cities/SF/departments')
  .execute();
```

## Client examples

### Web

``` javascript
const results = await execute(db.pipeline()
  .collection("users/bob/games")
  .sort(field("name").ascending())
  );test.firestore.js
```

##### Swift

``` swift
let results = try await db.pipeline()
  .collection("users/bob/games")
  .sort([Field("name").ascending()])
  .execute()PipelineSnippets.swift
```

##### Kotlin  
Android

``` kotlin
val results = db.pipeline()
    .collection("users/bob/games")
    .sort(field("name").ascending())
    .execute()DocSnippets.kt
```

##### Java  
Android

``` text
Task<Pipeline.Snapshot> results = db.pipeline()
    .collection("users/bob/games")
    .sort(field("name").ascending())
    .execute();DocSnippets.java
```

##### Python

``` python
from google.cloud.firestore_v1.pipeline_expressions import Field

results = (
    client.pipeline()
    .collection("users/bob/games")
    .sort(Field.of("name").ascending())
    .execute()
)firestore_pipelines.py
```

##### Java

``` java
Pipeline.Snapshot results =
    firestore
        .pipeline()
        .collection("users/bob/games")
        .sort(ascending(field("name")))
        .execute()
        .get();PipelineSnippets.java
```

## Behavior

In order to use the `  collection  ` stage, it must appear as the first stage in the pipeline.

The order of documents returned from the `  collection  ` stage is unstable and shouldn't be relied upon. A subsequent sort stage can be used to obtain a deterministic ordering.

For example, for the following documents:

### Node.js

``` text
await db.collection('cities').doc('SF').set({name: 'San Francsico', state: 'California'});
await db.collection('cities').doc('NYC').set({name: 'New York City', state: 'New York'});
await db.collection('cities').doc('CHI').set({name: 'Chicago', state: 'Illinois'});
await db.collection('states').doc('CA').set({name: 'California'});
```

The `  collection  ` stage can be used to retrieve all cities in the `  cities  ` collection and then sort them in ascending order of name.

### Node.js

``` text
const results = await db.pipeline()
  .collection('/cities')
  .sort(field('name').ascending())
  .execute();
```

This query produces the following documents:

``` text
  {name: 'Chicago', state: 'Illinois'}
  {name: 'New York City', state: 'New York'}
  {name: 'San Francisco', state: 'California'}
```

### Subcollections

The `  collection  ` stage can also be used to target collections under a specific parent by providing the full path to the stage.

For example, for the following documents:

### Node.js

``` text
await db.collection('cities/SF/departments').doc('building').set({name: 'SF Building Deparment', employees: 750});
await db.collection('cities/NY/departments').doc('building').set({name: 'NY Building Deparment', employees: 1000});
await db.collection('cities/CHI/departments').doc('building').set({name: 'CHI Building Deparment', employees: 900});
await db.collection('cities/NY/departments').doc('finance').set({name: 'NY Finance Deparment', employees: 1200});
```

For this example, we only want the departments of New York city.

### Node.js

``` text
const results = await db.pipeline()
  .collection('/cities/NY/departments')
  .sort(field('employees').ascending())
  .execute();
```

This will return all departments under the full path `  cities/NY/departments  ` .

``` text
  {name: 'NY Building Deparment', employees: 1000}
  {name: 'NY Finance Deparment', employees: 1200}
```
