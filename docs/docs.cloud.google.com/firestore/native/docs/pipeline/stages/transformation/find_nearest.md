# Find Nearest (Transformation Stage)

**Preview — Firestore in Native mode (with Pipeline Operations) for Enterprise Edition**

This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](/terms/service-terms#1) . You can process personal data for this feature as outlined in the [Cloud Data Processing Addendum](/terms/data-processing-addendum) , subject to the obligations and restrictions described in the agreement under which you access Google Cloud. Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

## Description

Performs a nearest neighbor vector search on the given `  embedding  ` field using the requested distance\_measure

## Syntax

### Node.js

``` text
const results = await db.pipeline()
  .collection("cities")
  .findNearest({
      field: 'embedding',
      vectorValue: vector([1.5, 2.345]),
      distanceMeasure: 'euclidean',
  })
  .execute();
```

## Client examples

##### Node.js

``` javascript
const results = await db.pipeline()
  .collection("cities")
  .findNearest({
      field: "embedding",
      vectorValue: [1.5, 2.345],
      distanceMeasure: "euclidean"
  })
  .execute();test.firestore.js
```

### Web

``` javascript
const results = await execute(db.pipeline()
  .collection("cities")
  .findNearest({
      field: "embedding",
      vectorValue: [1.5, 2.345],
      distanceMeasure: "euclidean"
  }));test.firestore.js
```

##### Swift

``` swift
let results = try await db.pipeline()
  .collection("cities")
  .findNearest(
    field: Field("embedding"),
    vectorValue: VectorValue([1.5, 2.345]),
    distanceMeasure: .euclidean
  )
  .execute()PipelineSnippets.swift
```

##### Kotlin  
Android

``` kotlin
val results = db.pipeline()
    .collection("cities")
    .findNearest(
        "embedding",
        FieldValue.vector(doubleArrayOf(1.5, 2.345)),
        FindNearestStage.DistanceMeasure.EUCLIDEAN
    )
    .execute()DocSnippets.kt
```

##### Java  
Android

``` text
Task<Pipeline.Snapshot> results = db.pipeline()
        .collection("cities")
        .findNearest(
            "embedding",
            new double[] {1.5, 2.345},
            FindNearestStage.DistanceMeasure.EUCLIDEAN
        )
        .execute();DocSnippets.java
```

##### Python

``` python
from google.cloud.firestore_v1.vector import Vector
from google.cloud.firestore_v1.base_vector_query import DistanceMeasure

results = (
    client.pipeline()
    .collection("cities")
    .find_nearest(
        field="embedding",
        vector_value=Vector([1.5, 2.345]),
        distance_measure=DistanceMeasure.EUCLIDEAN,
    )
    .execute()
)firestore_pipelines.py
```

##### Java

``` java
Pipeline.Snapshot results =
    firestore
        .pipeline()
        .collection("cities")
        .findNearest(
            "embedding",
            new double[] {1.5, 2.345},
            FindNearest.DistanceMeasure.EUCLIDEAN,
            new FindNearestOptions())
        .execute()
        .get();PipelineSnippets.java
```

## Behavior

### Distance Measure

The `  find_nearest  ` stage supports the following options for vector distance:

  - `  euclidean  ` : Measures the `  euclidean  ` distance between the vectors. To learn more, see [Euclidean](https://en.wikipedia.org/wiki/Euclidean_distance) .
  - `  cosine  ` : Compares vectors based on the angle between them which lets you measure similarity that isn't based on the vectors magnitude. We recommend using `  dot_product  ` with unit normalized vectors instead of COSINE distance, which is mathematically equivalent with better performance. To learn more see [Cosine similarity](https://en.wikipedia.org/wiki/Cosine_similarity) .
  - `  dot_product  ` : Similar to `  cosine  ` but is affected by the magnitude of the vectors. To learn more, see [Dot product](https://en.wikipedia.org/wiki/Dot_product) .

### Choose the distance measure

Depending on whether or not all your vector embeddings are normalized, you can determine which distance measure to use to find the distance measure. A normalized vector embedding has a magnitude (length) of exactly 1.0.

In addition, if you know which distance measure your model was trained with, use that distance measure to compute the distance between your vector embeddings.

**Normalized data**

If you have a dataset where all vector embeddings are normalized, then all three distance measures provide the same semantic search results. In essence, although each distance measure returns a different value, those values sort the same way. When embeddings are normalized, `  dot_product  ` is usually the most computationally efficient, but the difference is negligible in most cases. However, if your application is highly performance sensitive, `  dot_product  ` might help with performance tuning.

**Non-normalized data**

If you have a dataset where vector embeddings aren't normalized, then it's not mathematically correct to use `  dot_product  ` as a distance measure because dot product doesn't measure distance. Depending on how the embeddings were generated and what type of search is preferred, either the `  cosine  ` or `  euclidean  ` distance measure produces search results that are subjectively better than the other distance measures. Experimentation with either `  cosine  ` or `  euclidean  ` might be necessary to determine which is best for your use case.

**Unsure if data is normalized or non-normalized**

If you're unsure whether or not your data is normalized and you want to use `  dot_product  ` , we recommend that you use `  cosine  ` instead. `  cosine  ` is like `  dot_product  ` with normalization built in. Distance measured using `  cosine  ` ranges from `  0  ` to `  2  ` . A result that is close to `  0  ` indicates the vectors are very similar.

### Limit the results

You can limit the number of documents returned by the query by setting the limit field.

### Node.js

``` text
const results = await db.pipeline()
  .collection("cities")
  .findNearest({
      field: 'embedding',
      vectorValue: vector([1.5, 2.345]),
      distanceMeasure: 'euclidean',
      limit: 10,
  })
  .execute();
```

### Retrieving the Calculated Vector Distance

You can retrieve the calculated vector distance by assigning a distance\_field output property name on the `  find_nearest  ` stage, as shown in the following example:

As an example, for the following collection:

### Node.js

``` text
await db.collection('cities').doc('SF').set({name: 'San Francisco', embedding: vector([1.0, -1.0])});
await db.collection('cities').doc('TO').set({name: 'Toronto', embedding: vector([5.0, -10.0])});
await db.collection('cities').doc('AT').set({name: 'Atlantis', embedding: vector([2.0, -4.0])});
```

Perform a vector search with a requested output distance\_field :

### Node.js

``` text
const results = await db.pipeline()
  .collection("cities")
  .findNearest({
      field: 'embedding',
      vectorValue: vector([1.3, 2.345]),
      distanceMeasure: 'euclidean',
      distanceField: 'computedDistance',
  })
  .execute();
```

Which produces the following documents:

``` text
{name: 'San Francisco', embedding: vector([1.0, -1.0]), computedDistance: 3.3584259705999178},
{name: 'Atlantis', embedding: vector([2.0, -4.0]), computedDistance: 6.383496299051172},
{name: 'Toronto', embedding: vector([5.0, -10.0]), computedDistance: 12.887553103673328}
```

## Limitations

As you work with vector embeddings, note the following limitation:

  - The maximum supported embedding dimension is 2048. To store larger indexes, use [dimensionality reduction](https://en.wikipedia.org/wiki/Dimensionality_reduction) .
