# Sample (Transformation Stage)

**Preview — Firestore in Native mode (with Pipeline Operations) for Enterprise Edition**

This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](/terms/service-terms#1) . You can process personal data for this feature as outlined in the [Cloud Data Processing Addendum](/terms/data-processing-addendum) , subject to the obligations and restrictions described in the agreement under which you access Google Cloud. Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

## Description

Returns a non-deterministic sample from the results of the previous stage.

There are two supported modes:

  - `  DOCUMENTS  ` mode allows for sampling a set number of documents
      - This mode is similar to `  GoogleSQL.RESERVOIR  ` in that it outputs a sample of size `  n  ` , where any sample of size `  n  ` is equally possible.
  - `  PERCENT  ` mode allows for sampling a percentage of documents
      - This mode is similar to `  GoogleSQL.BERNOULLI  ` in that each document is independently selected with an equal `  percent  ` probability. This results in `  #documents * percent / 100  ` documents being returned on average.

## Syntax

### Node.js

``` text
  const sampled = await db.pipeline()
    .database()
    .sample(50)
    .execute();

  const sampled = await db.pipeline()
    .database()
    .sample({ percent: 0.5 })
    .execute();
```

## Behavior

### Documents Mode

Documents mode retrieves a specified number of documents in a random order. The specified number must be a non-negative `  INT64  ` value.

For example, for the following collection:

### Node.js

``` text
await db.collection('cities').doc('SF').set({name: 'San Francsico', state: 'California'});
await db.collection('cities').doc('NYC').set({name: 'New York City', state: 'New York'});
await db.collection('cities').doc('CHI').set({name: 'Chicago', state: 'Illinois'});
```

The sample stage in document mode can be used to retrieve a non-deterministic subset of results from this collection.

### Node.js

``` text
const sampled = await db.pipeline()
    .collection("/cities")
    .sample(1)
    .execute();
```

In this example, only 1 document at random would be returned at random.

``` text
  {name: 'New York City', state: 'New York'}
```

If the supplied number is greater than the total number of documents returned, all documents are returned in a random order.

### Node.js

``` text
const sampled = await db.pipeline()
    .collection("/cities")
    .sample(5)
    .execute();
```

This will result in the following documents:

``` text
  {name: 'New York City', state: 'New York'}
  {name: 'Chicago', state: 'Illinois'}
  {name: 'San Francisco', state: 'California'}
```

#### Client examples

### Web

``` javascript
let results;

// Get a sample of 100 documents in a database
results = await execute(db.pipeline()
  .database()
  .sample(100)
);

// Randomly shuffle a list of 3 documents
results = await execute(db.pipeline()
  .documents([
    doc(db, "cities", "SF"),
    doc(db, "cities", "NY"),
    doc(db, "cities", "DC"),
  ])
  .sample(3)
);test.firestore.js
```

##### Swift

``` swift
var results: Pipeline.Snapshot

// Get a sample of 100 documents in a database
results = try await db.pipeline()
  .database()
  .sample(count: 100)
  .execute()

// Randomly shuffle a list of 3 documents
results = try await db.pipeline()
  .documents([
    db.collection("cities").document("SF"),
    db.collection("cities").document("NY"),
    db.collection("cities").document("DC"),
  ])
  .sample(count: 3)
  .execute()PipelineSnippets.swift
```

##### Kotlin  
Android

``` kotlin
var results: Task<Pipeline.Snapshot>

// Get a sample of 100 documents in a database
results = db.pipeline()
    .database()
    .sample(100)
    .execute()

// Randomly shuffle a list of 3 documents
results = db.pipeline()
    .documents(
        db.collection("cities").document("SF"),
        db.collection("cities").document("NY"),
        db.collection("cities").document("DC")
    )
    .sample(3)
    .execute()DocSnippets.kt
```

##### Java  
Android

``` text
Task<Pipeline.Snapshot> results;

// Get a sample of 100 documents in a database
results = db.pipeline()
    .database()
    .sample(100)
    .execute();

// Randomly shuffle a list of 3 documents
results = db.pipeline()
    .documents(
        db.collection("cities").document("SF"),
        db.collection("cities").document("NY"),
        db.collection("cities").document("DC")
    )
    .sample(3)
    .execute();DocSnippets.java
```

##### Python

``` python
# Get a sample of 100 documents in a database
results = client.pipeline().database().sample(100).execute()

# Randomly shuffle a list of 3 documents
results = (
    client.pipeline()
    .documents(
        client.collection("cities").document("SF"),
        client.collection("cities").document("NY"),
        client.collection("cities").document("DC"),
    )
    .sample(3)
    .execute()
)firestore_pipelines.py
```

##### Java

``` java
// Get a sample of 100 documents in a database
Pipeline.Snapshot results1 = firestore.pipeline().database().sample(100).execute().get();

// Randomly shuffle a list of 3 documents
Pipeline.Snapshot results2 =
    firestore
        .pipeline()
        .documents(
            firestore.collection("cities").document("SF"),
            firestore.collection("cities").document("NY"),
            firestore.collection("cities").document("DC"))
        .sample(3)
        .execute()
        .get();PipelineSnippets.java
```

### Percent Mode

In percent mode, each document has a specified `  percent  ` chance of being returned. Unlike documents mode, the order here is not random and instead preserves the pre-existing document order. This percent input must be a double value between `  0.0  ` and `  1.0  ` .

Since each document is independently selected, the output is non-deterministic and on average, `  #documents * percent / 100  ` documents will be returned.

For example, for the following collection:

### Node.js

``` text
await db.collection('cities').doc('SF').set({name: 'San Francsico', state: 'California'});
await db.collection('cities').doc('NYC').set({name: 'New York City', state: 'New York'});
await db.collection('cities').doc('CHI').set({name: 'Chicago', state: 'Illinois'});
await db.collection('cities').doc('ATL').set({name: 'Atlanta', state: 'Georgia'});
```

The sample stage in percent mode can be used to retrieve (on average) 50% of the documents from the collection stage.

### Node.js

``` text
  const sampled = await db.pipeline()
    .collection("/cities")
    .sample({ percent: 0.5 })
    .execute();
```

This will result in a non-deterministic sample of (on average) 50% of documents from the `  cities  ` collection. The following is one possible output.

``` text
  {name: 'New York City', state: 'New York'}
  {name: 'Chicago', state: 'Illinois'}
```

In percent mode, because each document has the same probability of being selected, it is possible for no documents or all documents to be returned.

#### Client examples

### Web

``` javascript
// Get a sample of on average 50% of the documents in the database
const results = await execute(db.pipeline()
  .database()
  .sample({ percentage: 0.5 })
);test.firestore.js
```

##### Swift

``` swift
// Get a sample of on average 50% of the documents in the database
let results = try await db.pipeline()
  .database()
  .sample(percentage: 0.5)
  .execute()PipelineSnippets.swift
```

##### Kotlin  
Android

``` kotlin
// Get a sample of on average 50% of the documents in the database
val results = db.pipeline()
    .database()
    .sample(SampleStage.withPercentage(0.5))
    .execute()DocSnippets.kt
```

##### Java  
Android

``` text
// Get a sample of on average 50% of the documents in the database
Task<Pipeline.Snapshot> results = db.pipeline()
    .database()
    .sample(SampleStage.withPercentage(0.5))
    .execute();DocSnippets.java
```

##### Python

``` python
from google.cloud.firestore_v1.pipeline_stages import SampleOptions

# Get a sample of on average 50% of the documents in the database
results = (
    client.pipeline().database().sample(SampleOptions.percentage(0.5)).execute()
)firestore_pipelines.py
```

##### Java

``` java
// Get a sample of on average 50% of the documents in the database
Pipeline.Snapshot results =
    firestore.pipeline().database().sample(Sample.withPercentage(0.5)).execute().get();PipelineSnippets.java
```
