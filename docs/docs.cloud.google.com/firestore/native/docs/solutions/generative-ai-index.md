# Get started with generative AI

This page helps you get started with implementing generative AI features in your app. It describes the features and integrations for Firestore that involve generative AI.

## Quickstart for vector search with Firestore

Creating innovative AI-powered solutions for use cases such as product recommendations and chatbots often requires vector similarity search, or vector search for short. You can perform vector search on Firestore data without the hassle of copying data to another vector search solution, maintaining operational simplicity and efficiency.

The core workflow for vector search in Firestore consists of 4 steps.

### looks\_one Generate vector embeddings

The first step in utilizing vector search is to generate vector embeddings. Embeddings are representations of different kinds of data like text, images, and video that capture semantic or syntactic similarities between the entities they represent. Embeddings can be calculated using a service, such as the Vertex AI text-embeddings API.

### looks\_two Store embeddings in Firestore

Once the embeddings are generated you can store them in Firestore using one of the supported SDKs. Here is what that operation looks like in the NodeJS SDK:

``` text
const db = new Firestore();
let collectionRef = db.collection("beans");
await collectionRef.add({
  name: "Kahawa coffee beans",
  type: "arabica",
  description: "Information about the Kahawa coffee beans.",
  embedding_field: FieldValue.vector([0.1, 0.3, ..., 0.2]), // a vector with 768 dimensions
});
```

### looks\_3 Create a vector index

The next step is to create a Firestore KNN vector index where the vector embeddings are stored. During the preview release, you will need to create the index using the `  gcloud  ` command line tool.

### looks\_4 Perform the vector search

Once you have added all the vector embeddings and created the vector index, you are ready to run the search. You will then utilize the `  find_nearest  ` call on a collection reference to pass the query vector embedding with which to compare the stored embeddings and to specify the distance function you want to utilize.

Once again, explore the workflow and more use cases in our [blog post](//cloud.google.com/blog/products/databases/get-started-with-firestore-vector-similarity-search) .

## Solution: vector search

**Summary:** Store and query vector embeddings.

**Use case:** This feature is used by the other tools and features.

## Solution: extension for vector search with Firebase

**Summary:** Use the Firebase extension to automatically embed and query your Firestore documents with the vector search feature.

**Use case:** Perform automatic vector search in your Firebase projects.

## Solution: LangChain integrations

**Summary:** Use Firestore as a vector store, document loader, or chat message history source for LangChain.

**Use case:** Build generative AI applications or retrieval-augmented generation (RAG) workflows.

## Solution: Genkit

**Summary:** Genkit is an open source framework that helps you build, deploy, and monitor production-ready AI-powered apps.

**Use case:** Use Genkit and Firestore to create apps that generate custom content, use semantic search, handle unstructured inputs, answer questions with your business data, and much more\!
