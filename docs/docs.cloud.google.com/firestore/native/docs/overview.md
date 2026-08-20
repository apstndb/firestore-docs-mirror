---
name: documents/docs.cloud.google.com/firestore/native/docs/overview
uri: https://docs.cloud.google.com/firestore/native/docs/overview
title: Firestore overview
description: A cloud-hosted NoSQL database that's simple enough for rapid prototyping yet scalable and flexible enough to grow to any size.
data_source: docs.cloud.google.com
---

# Firestore overview

Firestore is an enterprise-grade, fully-managed document database from Google Cloud that offers multi-region data replication, advanced query capabilities, and ACID compliant transactions. With a 99.999% availability SLA, and disaster recovery features like managed backups, Firestore is a highly available NoSQL database that can support mission-critical workloads.

In addition to idiomatic Firestore client libraries, Firestore also provides a MongoDB-compatible API that lets you use Firestore with existing MongoDB applications. Firestore also supports (but doesn't require) integration with the Firebase mobile and web app development platform.

## Key capabilities

No matter how you access Firestore, you gain access to the following key capabilities:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><strong>Serverless infrastructure</strong></td>
<td>Firestore uses a pay-per-use model. Firestore does not require any pre-provisioning of resources and auto scales to match your load.</td>
</tr>
<tr class="even">
<td><strong>Virtually unlimited scale</strong></td>
<td>Firestore seamlessly scales compute and storage on-demand without the need to configure capacity, sharding or provision storage &amp; I/O.</td>
</tr>
<tr class="odd">
<td><strong>Industry-leading high availability</strong></td>
<td>All Firestore databases offer high availability, with 99.99% availability for regional and 99.999% availability for multi-regional deployments.<br />
<br />
Firestore has automatic multi-region data replication, strongly-consistent queries, atomic batch operations, and transaction support.</td>
</tr>
<tr class="even">
<td><strong>Low latency</strong></td>
<td>Firestore offers single digit millisecond read latency.</td>
</tr>
<tr class="odd">
<td><strong>Enterprise-grade security and monitoring</strong></td>
<td>Secure Firestore with centralized Google Cloud governance encompassing Identity and Access Management (IAM),VPC Service Controls (VPC-SC), Access Transparency, Access Approval, Cloud Monitoring, and Cloud Logging. Achieve enhanced visibility and simplified management of your Firestore database fleet with our integrated Database Center. Benefit from a unified fleet view and simplified management through centralized control and AI assistance.</td>
</tr>
</tbody>
</table>

You can interact with Firestore through multiple interfaces depending on your application's requirements.

## How do I set up an enterprise-grade serverless document database?

Use a Firestore database and connect with the Firestore client libraries, Google Cloud CLI, and Google Cloud console.

Recommended for developers looking for a document database. It is the best way to take advantage of the latest and most advanced Firestore capabilities, enterprise-grade configurability, observability and security. With its comprehensive client library support, Firestore fits into your enterprise architecture and development stack of choice.

[Get started with the Firestore client libraries](https://docs.cloud.google.com/firestore/native/docs/create-database-server-client-library) .

## How do I migrate a MongoDB application to a serverless cloud database?

Use Firestore with MongoDB compatibility and connect with MongoDB client libraries and tools.

Recommended when migrating applications from MongoDB or if you're planning on multi or hybrid cloud deployments that rely on MongoDB outside of Google Cloud. Firestore's MongoDB wire-compatible APIs allow lift-and-shift migrations. You can interact with Firestore using familiar tools like mongosh, mongoimport, Compass in addition to MongoDB client libraries.

[See supported features for Firestore with MongoDB compatibility](https://docs.cloud.google.com/firestore/mongodb-compatibility/docs/supported-features-80) .

## How do I build a web or mobile app with a fully integrated, zero-config backend?

Use Firestore and integrate the Firebase platform with your application.

Recommended for those seeking a backend-as-a-service (BaaS) solution, as opposed to a standalone database. Firebase offers an opinionated, turnkey, end-to-end solution which includes application hosting and integrations with many Google Cloud services like Firestore, Cloud Storage, and Cloud Run functions. Close integration between products lets you interact with Firestore databases using the Firebase SDKs and the Firebase console.

[Learn more about using Firestore with Firebase](https://firebase.google.com/docs/firestore) .

While Firebase is great for development velocity, if your enterprise architecture and governance frameworks require fine-grained control over many aspects of your stack, you gain the most flexibility from working directly with individual Google Cloud products like Firestore.

## How do I port a legacy Datastore app to use Firestore?

Use Firestore with Datastore compatibility and the Datastore client libraries.

Datastore compatibility mode supports legacy applications built on Datastore and App Engine. Datastore compatibility is an API layer on top of Firestore with the same availability, performance, consistency, and scalability. Beyond better integration with App Engine, Datastore compatibility doesn't offer any benefits over using Firestore directly.

[Get started with Firestore with Datastore compatibility](https://docs.cloud.google.com/datastore/docs/store-query-data) .
