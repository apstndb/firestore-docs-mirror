# Query interfaces overview

This page explains the different interfaces available for accessing data in a Firestore in Native mode database.

## Operation interfaces

Native mode supports two interfaces for accessing data:

### Pipeline operations

The newer query interface for Firestore. Pipeline operations support a stage-based composable syntax. You construct an operation by defining a series of sequential stages that are executed in order. This allows for complex operations, such as filtering on the result of an aggregation, which was not previously possible in the original interface (Core operations).

Pipeline operations are available only in Firestore Enterprise edition and are in the [Preview](https://cloud.google.com/products#product-launch-stages) launch stage.

### Core operations

Core operations are the original interface for Firestore. Core operations uses a method-chaining syntax ( `  .where()  ` , `  .orderBy()  ` , `  .get()  ` ) on document or collection references to retrieve documents. The ordering of query stages is implied and aggregation support is limited.

Core operations are available in both Enterprise and Standard editions, but index defaults are very different between editions. See the next section for details.

## Interface differences between editions

With the introduction of Native mode support in the Enterprise edition, both Firestore Core and Pipeline operations are available. When using Core operations in Enterprise edition, the new index behaviour and pricing model removes many of the restrictions of Standard edition.

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><strong>Feature</strong></td>
<td><strong>Standard edition</strong></td>
<td><strong>Enterprise edition</strong></td>
</tr>
<tr class="even">
<td><strong>Supported querying operations</strong></td>
<td>Limited to Firestore Core operations.</td>
<td>Supports Firestore Core and Pipeline operations, and Firestore with MongoDB compatible operations.</td>
</tr>
<tr class="odd">
<td><strong>Indexing Requirement</strong></td>
<td>All queries require indexes.</td>
<td>Indexes are not required for queries.</td>
</tr>
<tr class="even">
<td><strong>Index creation</strong></td>
<td><strong>Automatic indexes</strong> are created for single fields. You can manually create composite indexes.</td>
<td><strong>No automatic indexes</strong> are created. Indexes need to be manually managed.</td>
</tr>
<tr class="odd">
<td><strong>Query Performance &amp; Cost</strong></td>
<td>Queries are generally <strong>performant</strong> due to index requirements.</td>
<td>Optimize query performance and costs by creating indexes. You can identify missing indexes using Query Explain and Query Insights.
<p>Queries without indexes may risk being <strong>non-performant and costly</strong> as the dataset grows, requiring monitoring and tuning.</p></td>
</tr>
<tr class="even">
<td><strong>Indexing Overhead Cost</strong></td>
<td>No charge for index writes, as indexes are automatic.</td>
<td>Writing index entries <strong>consume write units</strong> when an associated document is written (1 write unit per 1 KiB of index entry size). You save on storage costs by not creating index entries for every field.</td>
</tr>
<tr class="odd">
<td><strong>Billing Model (Reads/Writes/Deletes)</strong></td>
<td>Charged per <strong>document read, write, and delete</strong> .</td>
<td>Charged per <strong>read and write</strong> (tranche). Reads are charged in <strong>Read Units</strong> (4 KiB tranches). Writes and deletes are merged into <strong>Write Units</strong> (1 KiB tranches).</td>
</tr>
<tr class="even">
<td><strong>Base Pricing (per million)</strong>
<p>Prices shown are for the <em>us-central1</em> region</p></td>
<td>Reads: <strong>$0.03 per 100,000 documents</strong> (or $0.30 per million).
<p>Writes: <strong>$0.09 per 100,000 documents</strong> (or $0.90 per million).</p>
<p>Deletes: <strong>$0.01 per 100,000 documents</strong> (or $0.10 per million)</p></td>
<td>Read Units: <strong>$0.05 per 1 million</strong> read units.
<p>Write Units: <strong>$0.26 per 1 million</strong> write units. Prices are generally <strong>lower if documents are under 4KiB</strong> compared to the Standard Read cost.</p></td>
</tr>
<tr class="odd">
<td><strong>Real-time Updates</strong>
<p>Prices shown are for the <em>us-central1</em> region</p></td>
<td>Realtime updates are <strong>included billed as Reads at $0.03 per 100,000 documents</strong> .</td>
<td>Realtime updates have a <strong>new separate SKU</strong> (Realtime Update Units), charged per 4 KiB tranche. Realtime updates cost <strong>$0.30 per million read units</strong> .</td>
</tr>
</tbody>
</table>

## What's next

  - [Learn how to construct Pipeline operations](/firestore/native/docs/pipeline/overview)
  - [Get data with Core operations](/firestore/native/docs/query-data/get-data)
