# Search with vector embeddings

This page shows you how to use Firestore to perform K-nearest neighbor (KNN) vector searches using the following techniques:

  - Store vector values
  - Create and manage KNN vector indexes
  - Make a K-nearest-neighbor (KNN) query using one of the supported vector distance measures

## Before you begin

Before you store embeddings in Firestore, you must generate vector embeddings. Firestore does not generate the embeddings. You can use a service such as Vertex AI to create vector values, for example, [text embeddings](https://cloud.google.com/vertex-ai/generative-ai/docs/embeddings/get-text-embeddings) from your Firestore data. You can then store these embeddings back in Firestore documents.

To learn more about embeddings, see [What are embeddings?](https://cloud.google.com/vertex-ai/generative-ai/docs/embeddings#embedding-types)

To learn how to get text embeddings with Vertex AI, see [Get text embeddings](https://cloud.google.com/vertex-ai/generative-ai/docs/embeddings/get-text-embeddings) .

## Store vector embeddings

The following examples demonstrate how to store vector embeddings in Firestore.

### Write operation with a vector embedding

The following example shows how to store a vector embedding in a Firestore document:

##### Python

``` python
from google.cloud import firestore
from google.cloud.firestore_v1.vector import Vector

firestore_client = firestore.Client()
collection = firestore_client.collection("coffee-beans")
doc = {
    "name": "Kahawa coffee beans",
    "description": "Information about the Kahawa coffee beans.",
    "embedding_field": Vector([0.18332680, 0.24160706, 0.3416704]),
}

collection.add(doc)vector_search.py
```

##### Node.js

``` text
import {
  Firestore,
  FieldValue,
} from "@google-cloud/firestore";

const db = new Firestore();
const coll = db.collection('coffee-beans');
await coll.add({
  name: "Kahawa coffee beans",
  description: "Information about the Kahawa coffee beans.",
  embedding_field: FieldValue.vector([1.0 , 2.0, 3.0])
});
```

##### Go

``` go
import (
 "context"
 "fmt"
 "io"

 "cloud.google.com/go/firestore"
)

type CoffeeBean struct {
 Name           string             `firestore:"name,omitempty"`
 Description    string             `firestore:"description,omitempty"`
 EmbeddingField firestore.Vector32 `firestore:"embedding_field,omitempty"`
 Color          string             `firestore:"color,omitempty"`
}

func storeVectors(w io.Writer, projectID string) error {
 ctx := context.Background()

 // Create client
 client, err := firestore.NewClient(ctx, projectID)
 if err != nil {
     return fmt.Errorf("firestore.NewClient: %w", err)
 }
 defer client.Close()

 // Vector can be represented by Vector32 or Vector64
 doc := CoffeeBean{
     Name:           "Kahawa coffee beans",
     Description:    "Information about the Kahawa coffee beans.",
     EmbeddingField: []float32{1.0, 2.0, 3.0},
     Color:          "red",
 }
 ref := client.Collection("coffee-beans").NewDoc()
 if _, err = ref.Set(ctx, doc); err != nil {
     fmt.Fprintf(w, "failed to upsert: %v", err)
     return err
 }

 return nil
}
vector_store.go
```

##### Java

``` text
import com.google.cloud.firestore.CollectionReference;
import com.google.cloud.firestore.DocumentReference;
import com.google.cloud.firestore.FieldValue;
import com.google.cloud.firestore.VectorQuery;

CollectionReference coll = firestore.collection("coffee-beans");

Map<String, Object> docData = new HashMap<>();
docData.put("name", "Kahawa coffee beans");
docData.put("description", "Information about the Kahawa coffee beans.");
docData.put("embedding_field", FieldValue.vector(new double[] {1.0, 2.0, 3.0}));

ApiFuture<DocumentReference> future = coll.add(docData);
DocumentReference documentReference = future.get();
```

### Compute vector embeddings with a Cloud Function

To calculate and store vector embeddings whenever a document is updated or created, you can set up a [Cloud Run function](/firestore/native/docs/extend-with-functions-2nd-gen) :

##### Python

``` text
@functions_framework.cloud_event
def store_embedding(cloud_event) -> None:
  """Triggers by a change to a Firestore document.
  """
  firestore_payload = firestore.DocumentEventData()
  payload = firestore_payload._pb.ParseFromString(cloud_event.data)

  collection_id, doc_id = from_payload(payload)
  # Call a function to calculate the embedding
  embedding = calculate_embedding(payload)
  # Update the document
  doc = firestore_client.collection(collection_id).document(doc_id)
  doc.set({"embedding_field": embedding}, merge=True)
```

##### Node.js

``` text
/**
 * A vector embedding will be computed from the
 * value of the `content` field. The vector value
 * will be stored in the `embedding` field. The
 * field names `content` and `embedding` are arbitrary
 * field names chosen for this example.
 */
async function storeEmbedding(event: FirestoreEvent<any>): Promise<void> {
  // Get the previous value of the document's `content` field.
  const previousDocumentSnapshot = event.data.before as QueryDocumentSnapshot;
  const previousContent = previousDocumentSnapshot.get("content");

  // Get the current value of the document's `content` field.
  const currentDocumentSnapshot = event.data.after as QueryDocumentSnapshot;
  const currentContent = currentDocumentSnapshot.get("content");

  // Don't update the embedding if the content field did not change
  if (previousContent === currentContent) {
    return;
  }

  // Call a function to calculate the embedding for the value
  // of the `content` field.
  const embeddingVector = calculateEmbedding(currentContent);

  // Update the `embedding` field on the document.
  await currentDocumentSnapshot.ref.update({
    embedding: embeddingVector,
  });
}
```

##### Go

``` text
  // Not yet supported in the Go client library
```

##### Java

``` text
  // Not yet supported in the Java client library
```

## Create and manage vector indexes

Before you can perform a nearest neighbor search with your vector embeddings, you must create a corresponding index. The following examples demonstrate how to create and manage vector indexes with the Google Cloud CLI. Vector indexes can also be [managed with the Firebase CLI and Terraform](/docs/firestore/query-data/indexing) .

### Create a vector index

Before you create a vector index, upgrade to the latest version of the Google Cloud CLI:

``` text
gcloud components update
```

To create a vector index, use [`  gcloud firestore indexes composite create  `](https://cloud.google.com/sdk/gcloud/reference/alpha/firestore/indexes/composite/create) :

##### gcloud

``` text
gcloud firestore indexes composite create \
--collection-group=collection-group \
--query-scope=COLLECTION \
--field-config field-path=vector-field,vector-config='vector-configuration' \
--database=database-id
```

where:

  - collection-group is the ID of the collection group.
  - vector-field is the name of the field that contains the vector embedding.
  - database-id is the ID of the database.
  - vector-configuration includes the vector `  dimension  ` and index type. The `  dimension  ` is an integer up to 2048. The index type must be `  flat  ` . Format the index configuration as follows: `  {"dimension":" DIMENSION ", "flat": "{}"}  ` .

The following example creates a composite index, including a vector index for field `  vector-field  ` and an ascending index for field `  color  ` . You can use this type of index to [pre-filter data](#pre-filter-data) before a nearest neighbor search.

##### gcloud

``` text
gcloud firestore indexes composite create \
--collection-group=collection-group \
--query-scope=COLLECTION \
--field-config=order=ASCENDING,field-path="color" \
--field-config field-path=vector-field,vector-config='{"dimension":"1024", "flat": "{}"}' \
--database=database-id
```

### List all vector indexes

##### gcloud

``` text
gcloud firestore indexes composite list --database=database-id
```

Replace database-id with the ID of the database.

### Delete a vector index

##### gcloud

``` text
gcloud firestore indexes composite delete index-id --database=database-id
```

where:

  - index-id is the ID of the index to delete. Use [`  indexes composite list  `](#list) to retrieve the index ID.
  - database-id is the ID of the database.

### Describe a vector index

##### gcloud

``` text
gcloud firestore indexes composite describe index-id --database=database-id
```

where:

  - index-id is the ID of the index to describe. Use or [`  indexes composite list  `](#list) to retrieve the index ID.
  - database-id is the ID of the database.

## Make a nearest-neighbor query

You can perform a similarity search to find the nearest neighbors of a vector embedding. Similarity searches require [vector indexes](#create_and_manage_vector_indexes) . If an index doesn't exist, Firestore suggests an index to create using the gcloud CLI.

The following example finds 10 nearest neighbors of the query vector.

##### Python

``` python
from google.cloud.firestore_v1.base_vector_query import DistanceMeasure
from google.cloud.firestore_v1.vector import Vector

collection = db.collection("coffee-beans")

# Requires a single-field vector index
vector_query = collection.find_nearest(
    vector_field="embedding_field",
    query_vector=Vector([0.3416704, 0.18332680, 0.24160706]),
    distance_measure=DistanceMeasure.EUCLIDEAN,
    limit=5,
)vector_search.py
```

##### Node.js

``` text
import {
  Firestore,
  FieldValue,
  VectorQuery,
  VectorQuerySnapshot,
} from "@google-cloud/firestore";

// Requires a single-field vector index
const vectorQuery: VectorQuery = coll.findNearest({
  vectorField: 'embedding_field',
  queryVector: [3.0, 1.0, 2.0],
  limit: 10,
  distanceMeasure: 'EUCLIDEAN'
});

const vectorQuerySnapshot: VectorQuerySnapshot = await vectorQuery.get();
```

##### Go

``` go
import (
 "context"
 "fmt"
 "io"

 "cloud.google.com/go/firestore"
)

func vectorSearchBasic(w io.Writer, projectID string) error {
 ctx := context.Background()

 // Create client
 client, err := firestore.NewClient(ctx, projectID)
 if err != nil {
     return fmt.Errorf("firestore.NewClient: %w", err)
 }
 defer client.Close()

 collection := client.Collection("coffee-beans")

 // Requires a vector index
 // https://firebase.google.com/docs/firestore/vector-search#create_and_manage_vector_indexes
 vectorQuery := collection.FindNearest("embedding_field",
     []float32{3.0, 1.0, 2.0},
     5,
     // More info: https://firebase.google.com/docs/firestore/vector-search#vector_distances
     firestore.DistanceMeasureEuclidean,
     nil)

 docs, err := vectorQuery.Documents(ctx).GetAll()
 if err != nil {
     fmt.Fprintf(w, "failed to get vector query results: %v", err)
     return err
 }

 for _, doc := range docs {
     fmt.Fprintln(w, doc.Data()["name"])
 }
 return nil
}
vector_search_basic.go
```

##### Java

``` text
import com.google.cloud.firestore.VectorQuery;
import com.google.cloud.firestore.VectorQuerySnapshot;

VectorQuery vectorQuery = coll.findNearest(
        "embedding_field",
        new double[] {3.0, 1.0, 2.0},
        /* limit */ 10,
        VectorQuery.DistanceMeasure.EUCLIDEAN);

ApiFuture<VectorQuerySnapshot> future = vectorQuery.get();
VectorQuerySnapshot vectorQuerySnapshot = future.get();
```

### Vector distances

Nearest-neighbor queries support the following options for vector distance:

  - `  EUCLIDEAN  ` : Measures the `  EUCLIDEAN  ` distance between the vectors. To learn more, see [Euclidean](https://en.wikipedia.org/wiki/Euclidean_distance) .
  - `  COSINE  ` : Compares vectors based on the angle between them which lets you measure similarity that isn't based on the vectors magnitude. We recommend using `  DOT_PRODUCT  ` with unit normalized vectors instead of COSINE distance, which is mathematically equivalent with better performance. To learn more, see [Cosine similarity](https://en.wikipedia.org/wiki/Cosine_similarity) .
  - `  DOT_PRODUCT  ` : Similar to `  COSINE  ` but is affected by the magnitude of the vectors. To learn more, see [Dot product](https://en.wikipedia.org/wiki/Dot_product) .

### Choose the distance measure

Depending on whether or not all your vector embeddings are normalized, you can determine which distance measure to use to find the distance measure. A normalized vector embedding has a magnitude (length) of exactly 1.0.

In addition, if you know which distance measure your model was trained with, use that distance measure to compute the distance between your vector embeddings.

**Normalized data**

If you have a dataset where all vector embeddings are normalized, then all three distance measures provide the same semantic search results. In essence, although each distance measure returns a different value, those values sort the same way. When embeddings are normalized, `  DOT_PRODUCT  ` is usually the most computationally efficient, but the difference is negligible in most cases. However, if your application is highly performance sensitive, `  DOT_PRODUCT  ` might help with performance tuning.

**Non-normalized data**

If you have a dataset where vector embeddings aren't normalized, then it's not mathematically correct to use `  DOT_PRODUCT  ` as a distance measure because dot product doesn't measure distance. Depending on how the embeddings were generated and what type of search is preferred, either the `  COSINE  ` or `  EUCLIDEAN  ` distance measure produces search results that are subjectively better than the other distance measures. Experimentation with either `  COSINE  ` or `  EUCLIDEAN  ` might be necessary to determine which is best for your use case.

**Unsure if data is normalized or non-normalized**

If you're unsure whether or not your data is normalized and you want to use `  DOT_PRODUCT  ` , we recommend that you use `  COSINE  ` instead. `  COSINE  ` is like `  DOT_PRODUCT  ` with normalization built in. Distance measured using `  COSINE  ` ranges from `  0  ` to `  2  ` . A result that is close to `  0  ` indicates the vectors are very similar.

### Pre-filter documents

To pre-filter documents before finding the nearest neighbors, you can combine a similarity search with other query operators. The `  and  ` and `  or  ` composite filters are supported. For more information about supported field filters, see [Query operators](https://cloud.google.com/firestore/docs/query-data/queries#query_operators) .

##### Python

``` python
from google.cloud.firestore_v1.base_vector_query import DistanceMeasure
from google.cloud.firestore_v1.vector import Vector

collection = db.collection("coffee-beans")

# Similarity search with pre-filter
# Requires a composite vector index
vector_query = collection.where("color", "==", "red").find_nearest(
    vector_field="embedding_field",
    query_vector=Vector([0.3416704, 0.18332680, 0.24160706]),
    distance_measure=DistanceMeasure.EUCLIDEAN,
    limit=5,
)vector_search.py
```

##### Node.js

``` text
// Similarity search with pre-filter
// Requires composite vector index
const preFilteredVectorQuery: VectorQuery = coll
    .where("color", "==", "red")
    .findNearest({
      vectorField: "embedding_field",
      queryVector: [3.0, 1.0, 2.0],
      limit: 5,
      distanceMeasure: "EUCLIDEAN",
    });

const vectorQueryResults = await preFilteredVectorQuery.get();
```

##### Go

``` go
import (
 "context"
 "fmt"
 "io"

 "cloud.google.com/go/firestore"
)

func vectorSearchPrefilter(w io.Writer, projectID string) error {
 ctx := context.Background()

 // Create client
 client, err := firestore.NewClient(ctx, projectID)
 if err != nil {
     return fmt.Errorf("firestore.NewClient: %w", err)
 }
 defer client.Close()

 collection := client.Collection("coffee-beans")

 // Similarity search with pre-filter
 // Requires a composite vector index
 vectorQuery := collection.Where("color", "==", "red").
     FindNearest("embedding_field",
         []float32{3.0, 1.0, 2.0},
         5,
         // More info: https://firebase.google.com/docs/firestore/vector-search#vector_distances
         firestore.DistanceMeasureEuclidean,
         nil)

 docs, err := vectorQuery.Documents(ctx).GetAll()
 if err != nil {
     fmt.Fprintf(w, "failed to get vector query results: %v", err)
     return err
 }

 for _, doc := range docs {
     fmt.Fprintln(w, doc.Data()["name"])
 }
 return nil
}
vector_search_prefilter.go
```

##### Java

``` text
import com.google.cloud.firestore.VectorQuery;
import com.google.cloud.firestore.VectorQuerySnapshot;

VectorQuery preFilteredVectorQuery = coll
        .whereEqualTo("color", "red")
        .findNearest(
                "embedding_field",
                new double[] {3.0, 1.0, 2.0},
                /* limit */ 10,
                VectorQuery.DistanceMeasure.EUCLIDEAN);

ApiFuture<VectorQuerySnapshot> future = preFilteredVectorQuery.get();
VectorQuerySnapshot vectorQuerySnapshot = future.get();
```

## Retrieve the calculated vector distance

You can retrieve the calculated vector distance by assigning a `  distance_result_field  ` output property name on the `  FindNearest  ` query, as shown in the following example:

##### Python

``` python
from google.cloud.firestore_v1.base_vector_query import DistanceMeasure
from google.cloud.firestore_v1.vector import Vector

collection = db.collection("coffee-beans")

vector_query = collection.find_nearest(
    vector_field="embedding_field",
    query_vector=Vector([0.3416704, 0.18332680, 0.24160706]),
    distance_measure=DistanceMeasure.EUCLIDEAN,
    limit=10,
    distance_result_field="vector_distance",
)

docs = vector_query.stream()

for doc in docs:
    print(f"{doc.id}, Distance: {doc.get('vector_distance')}")vector_search.py
```

##### Node.js

``` text
const vectorQuery: VectorQuery = coll.findNearest(
    {
      vectorField: 'embedding_field',
      queryVector: [3.0, 1.0, 2.0],
      limit: 10,
      distanceMeasure: 'EUCLIDEAN',
      distanceResultField: 'vector_distance'
    });

const snapshot: VectorQuerySnapshot = await vectorQuery.get();

snapshot.forEach((doc) => {
  console.log(doc.id, ' Distance: ', doc.get('vector_distance'));
});
```

##### Go

``` go
import (
 "context"
 "fmt"
 "io"

 "cloud.google.com/go/firestore"
)

func vectorSearchDistanceResultField(w io.Writer, projectID string) error {
 ctx := context.Background()

 client, err := firestore.NewClient(ctx, projectID)
 if err != nil {
     return fmt.Errorf("firestore.NewClient: %w", err)
 }
 defer client.Close()

 collection := client.Collection("coffee-beans")

 // Requires a vector index
 // https://firebase.google.com/docs/firestore/vector-search#create_and_manage_vector_indexes
 vectorQuery := collection.FindNearest("embedding_field",
     []float32{3.0, 1.0, 2.0},
     10,
     firestore.DistanceMeasureEuclidean,
     &firestore.FindNearestOptions{
         DistanceResultField: "vector_distance",
     })

 docs, err := vectorQuery.Documents(ctx).GetAll()
 if err != nil {
     fmt.Fprintf(w, "failed to get vector query results: %v", err)
     return err
 }

 for _, doc := range docs {
     fmt.Fprintf(w, "%v, Distance: %v\n", doc.Data()["name"], doc.Data()["vector_distance"])
 }
 return nil
}
vector_search_result_field.go
```

##### Java

``` text
import com.google.cloud.firestore.VectorQuery;
import com.google.cloud.firestore.VectorQueryOptions;
import com.google.cloud.firestore.VectorQuerySnapshot;

VectorQuery vectorQuery = coll.findNearest(
        "embedding_field",
        new double[] {3.0, 1.0, 2.0},
        /* limit */ 10,
        VectorQuery.DistanceMeasure.EUCLIDEAN,
        VectorQueryOptions.newBuilder().setDistanceResultField("vector_distance").build());

ApiFuture<VectorQuerySnapshot> future = vectorQuery.get();
VectorQuerySnapshot vectorQuerySnapshot = future.get();

for (DocumentSnapshot document : vectorQuerySnapshot.getDocuments()) {
    System.out.println(document.getId() + " Distance: " + document.get("vector_distance"));
}
```

If you want to use a field mask to return a subset of document fields along with a `  distanceResultField  ` , then you must also include the value of `  distanceResultField  ` in the field mask, as shown in the following example:

##### Python

``` python
vector_query = collection.select(["color", "vector_distance"]).find_nearest(
    vector_field="embedding_field",
    query_vector=Vector([0.3416704, 0.18332680, 0.24160706]),
    distance_measure=DistanceMeasure.EUCLIDEAN,
    limit=10,
    distance_result_field="vector_distance",
)vector_search.py
```

##### Node.js

``` text
const vectorQuery: VectorQuery = coll
    .select('name', 'description', 'vector_distance')
    .findNearest({
      vectorField: 'embedding_field',
      queryVector: [3.0, 1.0, 2.0],
      limit: 10,
      distanceMeasure: 'EUCLIDEAN',
      distanceResultField: 'vector_distance'
    });
```

##### Go

``` go
import (
 "context"
 "fmt"
 "io"

 "cloud.google.com/go/firestore"
)

func vectorSearchDistanceResultFieldMasked(w io.Writer, projectID string) error {
 ctx := context.Background()

 client, err := firestore.NewClient(ctx, projectID)
 if err != nil {
     return fmt.Errorf("firestore.NewClient: %w", err)
 }
 defer client.Close()

 collection := client.Collection("coffee-beans")

 // Requires a vector index
 // https://firebase.google.com/docs/firestore/vector-search#create_and_manage_vector_indexes
 vectorQuery := collection.Select("color", "vector_distance").
     FindNearest("embedding_field",
         []float32{3.0, 1.0, 2.0},
         10,
         firestore.DistanceMeasureEuclidean,
         &firestore.FindNearestOptions{
             DistanceResultField: "vector_distance",
         })

 docs, err := vectorQuery.Documents(ctx).GetAll()
 if err != nil {
     fmt.Fprintf(w, "failed to get vector query results: %v", err)
     return err
 }

 for _, doc := range docs {
     fmt.Fprintf(w, "%v, Distance: %v\n", doc.Data()["color"], doc.Data()["vector_distance"])
 }
 return nil
}
vector_search_result_field_masked.go
```

##### Java

``` text
import com.google.cloud.firestore.VectorQuery;
import com.google.cloud.firestore.VectorQueryOptions;
import com.google.cloud.firestore.VectorQuerySnapshot;

VectorQuery vectorQuery = coll
        .select("name", "description", "vector_distance")
        .findNearest(
          "embedding_field",
          new double[] {3.0, 1.0, 2.0},
          /* limit */ 10,
          VectorQuery.DistanceMeasure.EUCLIDEAN,
          VectorQueryOptions.newBuilder()
            .setDistanceResultField("vector_distance")
            .build());

ApiFuture<VectorQuerySnapshot> future = vectorQuery.get();
VectorQuerySnapshot vectorQuerySnapshot = future.get();

for (DocumentSnapshot document : vectorQuerySnapshot.getDocuments()) {
    System.out.println(document.getId() + " Distance: " + document.get("vector_distance"));
}
```

## Specify a distance threshold

You can specify a similarity threshold that returns only documents within the threshold. The behavior of the threshold field depends on the distance measure you choose:

  - `  EUCLIDEAN  ` and `  COSINE  ` distances limit the threshold to documents where distance is less than or equal to the specified threshold. These distance measures decrease as the vectors become more similar.
  - `  DOT_PRODUCT  ` distance limits the threshold to documents where distance is greater than or equal to the specified threshold. Dot product distances increase as the vectors become more similar.

The following example shows how to specify a distance threshold to return up to 10 nearest documents that are, at most, 4.5 units away using the `  EUCLIDEAN  ` distance metric:

##### Python

``` python
from google.cloud.firestore_v1.base_vector_query import DistanceMeasure
from google.cloud.firestore_v1.vector import Vector

collection = db.collection("coffee-beans")

vector_query = collection.find_nearest(
    vector_field="embedding_field",
    query_vector=Vector([0.3416704, 0.18332680, 0.24160706]),
    distance_measure=DistanceMeasure.EUCLIDEAN,
    limit=10,
    distance_threshold=4.5,
)

docs = vector_query.stream()

for doc in docs:
    print(f"{doc.id}")vector_search.py
```

##### Node.js

``` text
const vectorQuery: VectorQuery = coll.findNearest({
  vectorField: 'embedding_field',
  queryVector: [3.0, 1.0, 2.0],
  limit: 10,
  distanceMeasure: 'EUCLIDEAN',
  distanceThreshold: 4.5
});

const snapshot: VectorQuerySnapshot = await vectorQuery.get();

snapshot.forEach((doc) => {
  console.log(doc.id);
});
```

##### Go

``` go
import (
 "context"
 "fmt"
 "io"

 "cloud.google.com/go/firestore"
)

func vectorSearchDistanceThreshold(w io.Writer, projectID string) error {
 ctx := context.Background()

 client, err := firestore.NewClient(ctx, projectID)
 if err != nil {
     return fmt.Errorf("firestore.NewClient: %w", err)
 }
 defer client.Close()

 collection := client.Collection("coffee-beans")

 // Requires a vector index
 // https://firebase.google.com/docs/firestore/vector-search#create_and_manage_vector_indexes
 vectorQuery := collection.FindNearest("embedding_field",
     []float32{3.0, 1.0, 2.0},
     10,
     firestore.DistanceMeasureEuclidean,
     &firestore.FindNearestOptions{
         DistanceThreshold: firestore.Ptr[float64](4.5),
     })

 docs, err := vectorQuery.Documents(ctx).GetAll()
 if err != nil {
     fmt.Fprintf(w, "failed to get vector query results: %v", err)
     return err
 }

 for _, doc := range docs {
     fmt.Fprintln(w, doc.Data()["name"])
 }
 return nil
}
vector_search_distance_threshold.go
```

##### Java

``` text
import com.google.cloud.firestore.VectorQuery;
import com.google.cloud.firestore.VectorQueryOptions;
import com.google.cloud.firestore.VectorQuerySnapshot;

VectorQuery vectorQuery = coll.findNearest(
        "embedding_field",
        new double[] {3.0, 1.0, 2.0},
        /* limit */ 10,
        VectorQuery.DistanceMeasure.EUCLIDEAN,
        VectorQueryOptions.newBuilder()
          .setDistanceThreshold(4.5)
          .build());

ApiFuture<VectorQuerySnapshot> future = vectorQuery.get();
VectorQuerySnapshot vectorQuerySnapshot = future.get();

for (DocumentSnapshot document : vectorQuerySnapshot.getDocuments()) {
    System.out.println(document.getId());
}
```

## Limitations

As you work with vector embeddings, note the following limitations:

  - The maximum supported embedding dimension is 2048. To store larger indexes, use [dimensionality reduction](https://en.wikipedia.org/wiki/Dimensionality_reduction) .
  - The maximum number of documents to return from a nearest-neighbor query is 1000.
  - Vector search does not support [real-time snapshot listeners](/firestore/native/docs/query-data/listen) .
  - Only the Python, Node.js, Go, and Java client libraries support vector search.

## What's next

  - Read about [best practices](/firestore/native/docs/best-practices) for Firestore.
  - Understand [reads and writes at scale](/firestore/native/docs/understand-reads-writes-scale) .
