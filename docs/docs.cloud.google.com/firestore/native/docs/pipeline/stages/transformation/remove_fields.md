# Remove Fields (Transformation Stage)

**Preview — Firestore in Native mode (with Pipeline Operations) for Enterprise Edition**

This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](/terms/service-terms#1) . You can process personal data for this feature as outlined in the [Cloud Data Processing Addendum](/terms/data-processing-addendum) , subject to the obligations and restrictions described in the agreement under which you access Google Cloud. Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

## Description

Remove fields from the documents produced by the previous stage.

The generated documents will contain all fields from the previous stage except for the fields specified to be removed.

## Syntax

### Node.js

``` text
const results = await db.pipeline()
  .collection("/cities")
  .removeFields('population', 'location.state')
  .execute();
```

## Client examples

##### Node.js

``` javascript
const results = await db.pipeline()
  .collection("cities")
  .removeFields("population", "location.state")
  .execute();test.firestore.js
```

### Web

``` javascript
const results = await execute(db.pipeline()
  .collection("cities")
  .removeFields("population", "location.state"));test.firestore.js
```

##### Swift

``` swift
let results = try await db.pipeline()
  .collection("cities")
  .removeFields(["population", "location.state"])
  .execute()PipelineSnippets.swift
```

##### Kotlin  
Android

``` kotlin
val results = db.pipeline()
    .collection("cities")
    .removeFields("population", "location.state")
    .execute()DocSnippets.kt
```

##### Java  
Android

``` text
Task<Pipeline.Snapshot> results = db.pipeline()
        .collection("cities")
        .removeFields("population", "location.state")
        .execute();DocSnippets.java
```

##### Python

``` python
results = (
    client.pipeline()
    .collection("cities")
    .remove_fields("population", "location.state")
    .execute()
)firestore_pipelines.py
```

##### Java

``` java
Pipeline.Snapshot results =
    firestore
        .pipeline()
        .collection("cities")
        .removeFields("population", "location.state")
        .execute()
        .get();PipelineSnippets.java
```

## Behavior

### Remove Nested Fields

The `  remove_fields  ` stage respects nested field syntax, and will remove keys from a map.

For example, to remove the nested state field from the dataset:

### Node.js

``` text
await db.collection('cities').doc('SF').set({name: 'San Francisco', location: {country: 'USA', state: 'California'}});
await db.collection('cities').doc('TO').set({name: 'Toronto', location: {country: 'Canada', province: 'Ontario'}});
```

The following pipeline can be used:

### Node.js

``` text
const results = await db.pipeline()
  .collection("/cities")
  .removeFields('location.state')
  .execute();
```

Which produces the following documents:

``` text
{name: 'San Francisco', location: {country: 'USA'}}
{name: 'Toronto', location: {country: 'Canada', province: 'Ontario'}}
```

Removal of elements within an array is unsupported.

### Remove on Non-Existent Fields

If a nested or top-level field given to `  remove_fields  ` does not exist in a document, the stage won't edit the document for that field. Other existing fields will still be removed.
