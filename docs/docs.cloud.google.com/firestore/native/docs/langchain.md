# Build LLM-powered applications using LangChain

**Preview — LangChain**

This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

This page introduces how to build LLM-powered applications using [LangChain](https://www.langchain.com/) . The overviews on this page link to procedure guides in GitHub.

## What is LangChain?

LangChain is an LLM orchestration framework that helps developers build generative AI applications or retrieval-augmented generation (RAG) workflows. It provides the structure, tools, and components to streamline complex LLM workflows.

For more information about LangChain, see the [Google LangChain](https://python.langchain.com/docs/integrations/platforms/google) page. For more information about the LangChain framework, see the [LangChain](https://python.langchain.com/docs/get_started/introduction) product documentation.

## LangChain components for Firestore

Firestore offers the following LangChain interfaces:

  - [Vector store](#vector-store)
  - [Document loader](#document-loader)
  - [Chat message history](#chat-message-history)

## Vector store for Firestore

Vector store retrieves and stores documents and metadata from a vector database. Vector store gives an application the ability to perform semantic searches that interpret the meaning of a user query. This type of search is a called a vector search, and it can find topics that match the query conceptually. At query time, vector store retrieves the embedding vectors that are most similar to the embedding of the search request. In LangChain, a Vector store takes care of storing embedded data and performing the vector search for you.

To work with vector store in Firestore, use the `  FirestoreVectorStore  ` class.

For more information, see the [LangChain Vector Stores](https://python.langchain.com/docs/modules/data_connection/vectorstores/) product documentation.

### Vector store procedure guide

The [Firestore guide for vector store](https://github.com/googleapis/langchain-google-firestore-python/blob/main/docs/vectorstores.ipynb) shows you how to do the following:

  - Install the integration package and LangChain
  - Initialize a table for the vector store
  - Set up an embedding service using `  VertexAIEmbeddings  `
  - Initialize `  FirestoreVectorStore  `
  - Update and delete documents
  - Search for similar documents
  - Create a custom vector store to connect to a pre-existing Firestore database that has a table with vector embeddings

## Document loader for Firestore

The document loader saves, loads, and deletes a LangChain `  Document  ` objects. For example, you can load data for processing into embeddings and either store it in vector store or use it as a tool to provide specific context to chains.

To load documents from Firestore, use the `  FirestoreLoader  ` class. `  FirestoreLoader  ` methods return one or more documents from a table. Use the `  FirestoreSaver  ` class to save and delete documents.

For more information, see the [LangChain Document loaders](https://python.langchain.com/docs/modules/data_connection/document_loaders/) topic.

### Document loader procedure guide

The [Firestore guide for document loader](https://github.com/googleapis/langchain-google-firestore-python/blob/main/docs/document_loader.ipynb) shows you how to:

  - Install the integration package and LangChain
  - Load documents from a table
  - Add a filter to the loader
  - Customize the connection and authentication
  - Customize Document construction by specifying customer content and metadata
  - How to use and customize a `  FirestoreSaver  ` to store and delete documents

## Chat message history for Firestore

Question and answer applications require a history of the things said in the conversation to give the application context for answering further questions from the user. The LangChain `  ChatMessageHistory  ` class lets the application save messages to a database and retrieve them when needed to formulate further answers. A message can be a question, an answer, a statement, a greeting or any other piece of text that the user or application gives during the conversation. `  ChatMessageHistory  ` stores each message and chains messages together for each conversation.

Firestore extends this class with `  FirestoreChatMessageHistory  ` .

### Chat message history procedure guide

The [Firestore guide for chat message history](https://github.com/googleapis/langchain-google-firestore-python/blob/main/docs/chat_message_history.ipynb) shows you how to:

  - Install LangChain and authenticate to Google Cloud
  - Initialize the `  FirestoreChatMessageHistory  ` class to add and delete messages
  - Use a client to customize the connection and authentication
