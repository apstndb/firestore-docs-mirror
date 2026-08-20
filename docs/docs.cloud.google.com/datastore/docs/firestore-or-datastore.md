---
name: documents/docs.cloud.google.com/datastore/docs/firestore-or-datastore
uri: https://docs.cloud.google.com/datastore/docs/firestore-or-datastore
title: Choose between Firestore APIs
description: A highly-scalable NoSQL database for your web and mobile applications that automatically handles sharding and replication.
data_source: docs.cloud.google.com
---

When you create a Firestore database, you have the option to make it compatible with Datastore APIs. This is a database level setting for backwards compatibility that disables access to new Firestore capabilities. You don't have to enable Firestore in Datastore mode (Datastore) compatibility for all databases in a project.

We recommend that you use Datastore compatibility only for applications with a dependency on the Datastore APIs, such as legacy App Engine apps. Datastore compatibility is an API layer on top of Firestore with the same availability, performance, consistency, and scalability. Beyond better integration with App Engine, Datastore compatibility doesn't offer any benefits over using Firestore directly.

## Firestore

Firestore is an enterprise-grade NoSQL document database with MongoDB compatibility, built for automatic scaling, high performance, and ease of application development. Firestore is the successor to Datastore. You can use Firestore for server-side backend architectures that handle millions of operations, as well as mobile and web apps.

Firestore offers the following features beyond legacy Datastore capabilities:

  - A strongly consistent storage layer
  - A collection and document data model
  - Real-time updates
  - Mobile and web client libraries

Firestore is backward compatible with Datastore, but the new data model, real-time updates, and mobile and web client library features aren't. If you want to access all Firestore features, don't configure your database for Datastore compatibility.

### Datastore compatibility limitations

Unless you're working with a legacy App Engine application built on Datastore, we recommend that you don't use Datastore compatibility as it blocks access to many valuable Firestore capabilities, such as the following:

  - Rich query capabilities: the database accepts Datastore API requests and denies Firestore API requests which offer rich query capabilities.
  - More index types: the database uses Datastore indexes instead of Firestore indexes which offer a wider variety of index types and higher configurability.
  - Real-time capabilities: Firestore real-time capabilities won't be available.

## What's next

  - To get started with Firestore client libraries, see [Create a Firestore database and connect a server client library](https://docs.cloud.google.com/firestore/native/docs/create-database-server-client-library) .

  - To get started with Firestore with Datastore compatibility, see [Get started with Datastore client libraries](https://docs.cloud.google.com/datastore/docs/reference/libraries) .
