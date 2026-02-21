# Firestore editions overview

This page describes Firestore editions and key features.

Firestore is available in the following editions:

  - **Enterprise edition** : provides the most advanced Firestore capabilities, maximizing developer flexibility and control. It supports the Firestore with MongoDB compatibility API along with the Firestore APIs and Firebase SDKs to perform real-time and offline queries.
    
    Enterprise edition features an advanced query engine with over 180 capabilities, customizable indexing options, and up to five times faster performance. The Enterprise edition utilizes a modern pricing model based on tranches of bytes read and written, storage consumed, and network egress incurred.

  - **Standard edition** : provides the core Firestore capabilities including a standard query engine, automated indexing to help performance, and Firebase SDKs with real-time synchronization and offline queries. Standard edition utilizes a simplified pricing model based on documents read and written, storage consumed, and network egress incurred.

## Editions features

The following table summarizes the features available for each edition:

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th></th>
<th><strong>Enterprise</strong></th>
<th><strong>Standard</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Query Engine</td>
<td><p>Advanced query engine</p>
<ul>
<li>More than 180 stages and operators, including support for aggregations, arithmetic, arrays, sets, type conversions, and joining data.</li>
<li>You can perform queries with or without an index.</li>
</ul></td>
<td><p>Standard query engine</p>
<ul>
<li>Standard query capabilities for basic comparisons and matches.</li>
<li>All queries require covered indexes.</li>
</ul></td>
</tr>
<tr class="even">
<td>Document Size Limits</td>
<td><ul>
<li>4 MiB with MongoDB compatibility</li>
<li>1 MiB with Firestore in Native mode</li>
</ul></td>
<td>1 MiB</td>
</tr>
<tr class="odd">
<td>Supports Firestore with MongoDB compatibility</td>
<td>Yes</td>
<td>No</td>
</tr>
<tr class="even">
<td>Supports Firestore in Native mode: server-side, web, and mobile SDKs with real-time and offline support</td>
<td>Yes (Preview)</td>
<td>Yes</td>
</tr>
<tr class="odd">
<td>Indexing</td>
<td>Fully customizable, with support for advanced indexes like unique, dense, and sparse.</td>
<td>Automatic, basic indexing on all document fields</td>
</tr>
<tr class="even">
<td>Change data capture</td>
<td>Triggers</td>
<td>Triggers</td>
</tr>
<tr class="odd">
<td>Observability</td>
<td><ul>
<li>Cloud Monitoring</li>
<li>Query Explain</li>
<li>Query Insights</li>
<li>Database Center</li>
</ul></td>
<td><ul>
<li>Cloud Monitoring</li>
<li>Query Explain</li>
<li>Query Insights</li>
<li>Database Center</li>
</ul></td>
</tr>
<tr class="even">
<td>Data protection</td>
<td><ul>
<li>Scheduled backups</li>
<li>Point-in-time recovery</li>
</ul></td>
<td>Scheduled backups
Point-in-time recovery</td>
</tr>
<tr class="odd">
<td>Encryption</td>
<td><ul>
<li>Google-owned and Google-managed encryption key</li>
<li>Customer-managed encryption keys</li>
</ul></td>
<td><ul>
<li>Google-owned and Google-managed encryption key</li>
<li>Customer-managed encryption keys</li>
</ul></td>
</tr>
<tr class="even">
<td>Storage</td>
<td>SSD</td>
<td>Hybrid storage (SSD &amp; HDD)</td>
</tr>
<tr class="odd">
<td>Performance</td>
<td>Best</td>
<td>Good</td>
</tr>
<tr class="even">
<td>Committed Use Discounts</td>
<td>20% for 1 year; 40% for 3 years</td>
<td>20% for 1 year; 40% for 3 years</td>
</tr>
</tbody>
</table>

## Data access modes

Firestore supports the following data access modes to read and write data:

  - **Firestore with MongoDB compatibility mode** : this interface supports Firestore with MongoDB compatibility and lets you re-use existing MongoDB drivers, tools, and open-source ecosystem integrations with Firestore.
  - **Firestore in Native mode** : this interface supports all of the latest and most innovative capabilities of Firestore, including real-time synchronization and offline caching in the Firestore client libraries.
  - **Firestore in Datastore mode** : this interface is best utilized by Datastore and App Engine Datastore apps.

### Data access modes that each edition supports

Available data access modes depend on the edition of the database. You must select a data access mode when you create the database. You can't change this mode.

  - **Firestore Enterprise edition** : supports the MongoDB compatibility APIs or the Firestore in Native mode API.
  - **Firestore Standard edition** : supports the Firestore Native API or the Datastore API.

## Maximize performance

Firestore Enterprise edition is ideal for applications that require maximum performance. Firestore Enterprise edition offers up to five times improved performance over Standard edition performance, especially at tail latencies. This gain is primarily due to the advanced query engine and faster SSD-based storage.

## Maximize scaling

Firestore Enterprise edition is able to better handle bursty network traffic at a rate up to 8x higher than Standard edition.

## Pricing

For more information about Firestore editions pricing, see [Firestore Enterprise edition pricing](https://cloud.google.com/firestore/enterprise/pricing) and [Firestore Standard edition pricing](https://cloud.google.com/firestore/pricing) . Both Firestore edition pricing models are based on operations conducted, storage consumed, and network egress incurred. Firestore Enterprise edition measures operations conducted using tranches of bytes read and written whereas Standard edition measures the number of documents read or written.

You can get started on Firestore in either edition with daily free usage.

## Mix and match editions in a project

You can create both Firestore Enterprise edition and Standard edition databases in the same project.

## Migrate data between editions

To try the advanced query engine and other Enterprise edition features, create a new Enterprise edition database. Firestore data is compatible with both edition. To migrate data between editions, use the [import and export features](/firestore/native/docs/manage-data/export-import) of Firestore.

## What's next

  - [Learn about client libraries for Firestore in Native mode.](/firestore/native/docs/reference/libraries)
  - For apps that use the Datastore API, see [Firestore in Datastore mode](/datastore/docs/firestore-or-datastore) .
  - [Learn how to create a Firestore with MongoDB compatibility database and connect to it with the mongosh tool](/firestore/mongodb-compatibility/docs/create-and-query-database) .
