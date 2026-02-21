**Preview — LangChain**

This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

This page introduces how to build LLM-powered applications using [LangChain](https://www.langchain.com/) . The overviews on this page link to procedure guides in GitHub.

## What is LangChain?

LangChain is an LLM orchestration framework that helps developers build generative AI applications or retrieval-augmented generation (RAG) workflows. It provides the structure, tools, and components to streamline complex LLM workflows.

For more information about LangChain, see the [Google LangChain](https://python.langchain.com/docs/integrations/platforms/google) page. For more information about the LangChain framework, see the [LangChain](https://python.langchain.com/docs/get_started/introduction) product documentation.

## LangChain components for Datastore mode

Datastore mode offers the following LangChain interfaces:

  - [Document loader](#document-loader)
  - [Chat message history](#chat-message-history)

## Document loader for Datastore mode

The document loader saves, loads, and deletes a LangChain `  Document  ` objects. For example, you can load data for processing into embeddings and either store it in vector store or use it as a tool to provide specific context to chains.

To load documents from document loader in Datastore mode, use the `  DatastoreLoader  ` class. `  FirestoreLoader  ` methods return one or more documents from a table. Use the `  DatastoreSaver  ` class to save and delete documents.

For more information, see the [LangChain Document loaders](https://python.langchain.com/docs/modules/data_connection/document_loaders/) topic.

### Document loader procedure guide

The [Datastore mode guide for document loader](https://github.com/googleapis/langchain-google-datastore-python/blob/main/docs/document_loader.ipynb) shows you how to do the following:

  - Install the integration package and LangChain
  - Load documents from a table
  - Add a filter to the loader
  - Customize the connection and authentication
  - Customize Document construction by specifying customer content and metadata
  - How to use and customize a `  DatastoreSaver  ` to store and delete documents

## Chat message history for Datastore mode

Question and answer applications require a history of the things said in the conversation to give the application context for answering further questions from the user. The LangChain `  ChatMessageHistory  ` class lets the application save messages to a database and retrieve them when needed to formulate further answers. A message can be a question, an answer, a statement, a greeting or any other piece of text that the user or application gives during the conversation. `  ChatMessageHistory  ` stores each message and chains messages together for each conversation.

Datastore mode extends this class with `  DatastoreChatMessageHistory  ` .

### Chat message history procedure guide

The [Datastore mode guide for chat message history](https://github.com/googleapis/langchain-google-datastore-python/blob/main/docs/chat_message_history.ipynb) shows you how to do the following:

  - Install LangChain and authenticate to Google Cloud
  - Create a `  DatastoreChatMessageHistory  ` object and add messages
  - Use a client to customize the connection and authentication
