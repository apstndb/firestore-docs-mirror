# Firestore with MongoDB compatibility overview

Firestore with MongoDB compatibility lets you use existing MongoDB application code, drivers, tools, and the open-source ecosystem of MongoDB integrations with Firestore.

Firestore offers a differentiated serverless document database service, featuring multi-region replication with strong consistency, virtually unlimited scalability, industry-leading high availability of up to 99.999% SLA, and single-digit milliseconds read performance.

Firestore with MongoDB compatibility is available as part of [Firestore Enterprise edition](/firestore/native/docs/editions-overview) .

## Key capabilities

Firestore with MongoDB compatibility offers a number of key capabilities:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Differentiator</strong></th>
<th><strong>Description</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>MongoDB compatibility</strong></td>
<td>Firestore provides a MongoDB compatible API allowing you to use Firestore as the database for your existing MongoDB applications.</td>
</tr>
<tr class="even">
<td><strong>Serverless</strong></td>
<td>Firestore uses a pay-per-use model. Firestore does not require any pre-provisioning of resources and auto scales to match your load.</td>
</tr>
<tr class="odd">
<td><strong>Virtually unlimited scale</strong></td>
<td>Firestore seamlessly scales compute and storage on-demand without the need to configure capacity, sharding or provision storage &amp; I/O.</td>
</tr>
<tr class="even">
<td><strong>Industry-leading High Availability</strong></td>
<td>All Firestore databases offer high availability, with 99.99% availability for regional and 99.999% availability for multi-regional deployments.<br />
<br />
Firestore has automatic multi-region data replication, strongly-consistent queries, atomic batch operations, and transaction support.</td>
</tr>
<tr class="odd">
<td><strong>Single digit milliseconds read latency</strong></td>
<td>Firestore offers single digit millisecond read latency.</td>
</tr>
<tr class="even">
<td><strong>Enterprise-grade security and monitoring</strong></td>
<td>Secure Firestore with centralized Google Cloud governance encompassing Identity and Access Management,VPC Service Controls (VPC-SC), Access Transparency, Access Approval, Cloud Monitoring, and Cloud Logging. Achieve enhanced visibility and simplified management of your Firestore database fleet with our integrated Database Center. Benefit from a unified fleet view and simplified management through centralized control and AI assistance.</td>
</tr>
</tbody>
</table>

## How does it work?

Firestore is a cloud-first, NoSQL document database offering MongoDB compatibility.

Following the Firestore with MongoDB compatibility data model, you store data in documents that contain fields mapping to values. These documents are stored in collections, which are containers for your documents that you can use to organize your data and build queries. Documents support many different [data types](/firestore/mongodb-compatibility/docs/supported-data-types-drivers) , from strings and numbers, to complex, embedded objects.

Additionally, querying in Firestore is expressive, efficient, and flexible. You can use standard MongoDB driver or the MongoDB Query Language (MQL). You can create shallow queries to retrieve data at the document level without needing to retrieve the entire collection, and add sorting, filtering, and limits to your queries or cursors to paginate your results.

Finally, Firestore with MongoDB compatibility is fully integrated with Google Cloud governance services including [Identity and Access Management (IAM)](/firestore/mongodb-compatibility/docs/security/iam) Cloud Monitoring, and Cloud Audit Logs.

## What's next

  - [Get started with Firestore with MongoDB compatibility](/firestore/mongodb-compatibility/docs/create-and-query-database)
