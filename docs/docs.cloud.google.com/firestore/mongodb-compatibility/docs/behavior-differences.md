# Behavior differences

This page describes behavioral differences between Firestore with MongoDB compatibility and MongoDB.

For a breakdown of supported features depending on MongoDB version, see:

  - [Supported features: 8.0](/firestore/mongodb-compatibility/docs/supported-features-80)
  - [Supported features: 7.0](/firestore/mongodb-compatibility/docs/supported-features-70)
  - [Supported features: 6.0](/firestore/mongodb-compatibility/docs/supported-features-60)
  - [Supported features: 5.0](/firestore/mongodb-compatibility/docs/supported-features-50)

## Connections and databases

  - Each connection is limited to a single Firestore with MongoDB compatibility database.
  - A database must be created before connecting to it.

## Naming

The following differences apply to naming parts of your data model.

### Collections

  - Collection names matching `  __.*__  ` are not supported.

### Fields

  - Field names matching `  __.*__  ` are not supported.
  - Empty field names are not supported.

## Documents

  - The maximum document size is 4 MiB.
  - The maximum nesting depth of fields is 20. Each Array and Object-typed field adds one level to the overall depth.

### `     _id    `

  - The top-level `  _id  ` field must be an ObjectId, String, 64-bit integer, 32-bit integer, Double, Binary, or Object. Other BSON types are not supported.

## Values

  - The JavaScript, Symbol, DBPointer, and Undefined BSON types are not supported.

### Date

  - Date values must fall in `  [0001-01-01T00:00:00Z, 9999-12-31T23:59:59Z]  ` .

### Decimal128

  - `  NaN  ` , positive infinity, and negative infinity values are canonicalized on write.
  - Arithmetic operations on Decimal128 are not supported.

### Double

  - `  NaN  ` values are canonicalized on write.

### Regular expression

  - Regular expression options must be valid ("i", "m", "s", "u", or "x") and provided in alphabetical order without repeats.

## Queries

  - Natural sort order (queries without an explicit sort) does not match insertion order or order by `  _id  ` ascending.

## Aggregations

  - Aggregations are limited to 250 stages.
  - The `  $merge  ` and `  $out  ` stages are not supported. See the [commands](#commands) section for a complete list of supported stages and operators.
  - The `  $lookup  ` stage does not support the `  let  ` and `  pipeline  ` fields.
  - The `  $facet  ` stage does not support `  $rand  ` or `  $sample  ` in the input stages because it's a volatile expression.

## Writes

  - Documents with names beginning with a dollar sign ("$") cannot be created using the upsert feature of `  update  ` or `  findAndModify  ` .
  - Make sure your connection string includes `  retryWrites=false  ` (or use the method appropriate to your driver) to make sure the driver does not attempt to use this feature. Retryable writes are not supported.

## Transactions

  - Snapshot isolation and serializable transactions are supported.

  - By default, transactions use optimistic concurrency controls with snapshot isolation.

## Read concern

  - Firestore with MongoDB compatibility supports the `  snapshot  ` , `  majority  ` , and `  linearizable  ` read concerns. The default is `  snapshot  ` which refers to snapshot isolation.
    
    Use `  linearizable  ` when the application requires strict consistency and must prevent write skew anomalies. For other workloads, `  snapshot  ` can improve performance and reduce transaction contention.

## Write concern

  - Only `  w: 'majority'  ` and `  w: 1  ` write concerns are supported.

## Read preference

  - Only the `  primary  ` , `  primaryPreferred  ` , `  primary_preferred  ` , `  secondary_preferred  ` , and `  nearest  ` read concerns are supported.

## Indexes

  - Wildcard indexes are not supported.
  - Firestore with MongoDB compatibility does not automatically create an index on `  _id  ` , but it ensures values of `  _id  ` are unique within a collection.
  - Indexes without multi-key enabled are not automatically changed to [multi-key indexes](/firestore/mongodb-compatibility/docs/index-overview#multi-key_indexes_for_array_values) based on write operations. You must enable multi-key when you create the index and the option cannot be changed.

## Errors

  - Error codes and messages may differ between Firestore with MongoDB compatibility and MongoDB.

## Commands

The following behavior differences apply to specific commands.

  - Commands not listed in the following tables are unsupported.
  - `  comment  ` is accepted by most commands but is ignored.
  - `  maxTimeMS  ` is accepted by most commands but may be ignored.

### Queries and writes

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Command</strong></th>
<th><strong>Unsupported Fields</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">        find       </code></p></td>
<td><ul>
<li><code dir="ltr" translate="no">         max        </code></li>
</ul>
<ul>
<li><code dir="ltr" translate="no">         min        </code></li>
</ul>
<ul>
<li><code dir="ltr" translate="no">         returnKey        </code></li>
</ul>
<ul>
<li><code dir="ltr" translate="no">         showRecordId        </code></li>
</ul>
<ul>
<li><code dir="ltr" translate="no">         tailable        </code></li>
</ul>
<ul>
<li><code dir="ltr" translate="no">         oplogReplay        </code></li>
</ul>
<ul>
<li><code dir="ltr" translate="no">         noCursorTimeout        </code></li>
</ul>
<ul>
<li><code dir="ltr" translate="no">         awaitData        </code></li>
</ul>
<ul>
<li><code dir="ltr" translate="no">         allowPartialResults        </code></li>
</ul>
<ul>
<li><code dir="ltr" translate="no">         collation        </code></li>
</ul>
<ul>
<li><code dir="ltr" translate="no">         allowDiskUsage        </code></li>
</ul>
<ul>
<li><code dir="ltr" translate="no">         let        </code></li>
</ul></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">        aggregate       </code></p></td>
<td><ul>
<li><code dir="ltr" translate="no">         collation        </code></li>
</ul>
<ul>
<li><code dir="ltr" translate="no">         let        </code></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">        insert       </code></p></td>
<td><p>(none)</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">        update       </code></p></td>
<td>Within an update statement:<br />
<br />

<ul>
<li><code dir="ltr" translate="no">         collation        </code></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">        delete       </code></p></td>
<td>Within a delete statement:<br />
<br />

<ul>
<li><code dir="ltr" translate="no">         collation        </code></li>
</ul></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">        findAndModify       </code></p></td>
<td><ul>
<li><code dir="ltr" translate="no">         collation        </code></li>
</ul>
<ul>
<li><code dir="ltr" translate="no">         let        </code></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">        count       </code></p></td>
<td><ul>
<li><code dir="ltr" translate="no">         collation        </code></li>
</ul></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">        distinct       </code></p></td>
<td><ul>
<li><code dir="ltr" translate="no">         collation        </code></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">        getMore       </code></p></td>
<td><ul>
<li><code dir="ltr" translate="no">         comment        </code></li>
</ul></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">        killCursors       </code></p></td>
<td><p>(none)</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">        explain       </code></p></td>
<td><p>(none)</p></td>
</tr>
</tbody>
</table>

### Transactions and sessions

<table>
<thead>
<tr class="header">
<th><strong>Command</strong></th>
<th><strong>Unsupported Fields</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">        commitTransaction       </code></p></td>
<td><p>(none)</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">        abortTransaction       </code></p></td>
<td><p>(none)</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">        endSessions       </code></p></td>
<td><p>(none)</p></td>
</tr>
</tbody>
</table>

### Administration

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Command</strong></th>
<th><strong>Unsupported Fields</strong></th>
<th><strong>Notes</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">        listDatabases       </code></p></td>
<td><ul>
<li><code dir="ltr" translate="no">         authorizedDatabases        </code></li>
</ul></td>
<td><code dir="ltr" translate="no">       filter      </code> must be empty if provided.</td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">        listCollections       </code></p></td>
<td><p>(none)</p></td>
<td><code dir="ltr" translate="no">       authorizedCollections      </code> must be false if provided.</td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">        listIndexes       </code></p></td>
<td><p>(none)</p></td>
<td></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">        createIndexes       </code></p></td>
<td><p>(none)</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">        dropIndexes       </code></p></td>
<td><p>(none)</p></td>
<td></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">        createCollection       </code></p></td>
<td><ul>
<li><code dir="ltr" translate="no">         timeseries        </code></li>
</ul>
<ul>
<li><code dir="ltr" translate="no">         expireAfterSeconds        </code></li>
</ul>
<ul>
<li><code dir="ltr" translate="no">         clusteredIndex        </code></li>
</ul>
<ul>
<li><code dir="ltr" translate="no">         changeStreamPreAndPostImages        </code></li>
</ul>
<ul>
<li><code dir="ltr" translate="no">         size        </code></li>
</ul>
<ul>
<li><code dir="ltr" translate="no">         max        </code></li>
</ul>
<ul>
<li><code dir="ltr" translate="no">         storageEngine        </code></li>
</ul>
<ul>
<li><code dir="ltr" translate="no">         validator        </code></li>
</ul>
<ul>
<li><code dir="ltr" translate="no">         validationLevel        </code></li>
</ul>
<ul>
<li><code dir="ltr" translate="no">         validationAction        </code></li>
</ul>
<ul>
<li><code dir="ltr" translate="no">         indexOptionDefaults        </code></li>
</ul>
<ul>
<li><code dir="ltr" translate="no">         viewOn        </code></li>
</ul>
<ul>
<li><code dir="ltr" translate="no">         pipeline        </code></li>
</ul>
<ul>
<li><code dir="ltr" translate="no">         collation        </code></li>
</ul>
<ul>
<li><code dir="ltr" translate="no">         encryptedFields        </code></li>
</ul></td>
<td>This command is a no-op.<br />
<br />
<code dir="ltr" translate="no">       capped      </code> must be false if provided.</td>
</tr>
</tbody>
</table>

## What's next

  - Run the [Quickstart: Create a database and connect to it](/firestore/mongodb-compatibility/docs/create-and-query-database) .
  - For a full list of supported features, see [Supported MongoDB data types, drivers, and features](/firestore/mongodb-compatibility/docs/supported-data-types-drivers) .
