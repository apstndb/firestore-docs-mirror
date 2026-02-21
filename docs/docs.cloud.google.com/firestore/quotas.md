# Quotas and limits

This page identifies the request quotas and limits for Firestore.

## Free Tier usage

Firestore offers a free tier that lets you get started with Firestore at no cost. The free tier amounts are listed in the following table.

Free tier amounts are applied daily and reset at midnight Pacific time.

The free tier applies to only one Firestore database per project. The first database that is created in a project without a free tier database will get the free tier. If the database with the free tier applied is deleted, the next database created will receive the free tier.

### Standard edition

<table>
<thead>
<tr class="header">
<th>Free tier</th>
<th>Quota</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Stored data</td>
<td>1 GiB</td>
</tr>
<tr class="even">
<td>Document reads</td>
<td>50,000 per day</td>
</tr>
<tr class="odd">
<td>Document writes</td>
<td>20,000 per day</td>
</tr>
<tr class="even">
<td>Document deletes</td>
<td>20,000 per day</td>
</tr>
<tr class="odd">
<td>Outbound data transfer</td>
<td>10 GiB per month</td>
</tr>
</tbody>
</table>

### Enterprise edition

<table>
<thead>
<tr class="header">
<th>Free tier</th>
<th>Quota</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Stored data</td>
<td>1 GiB</td>
</tr>
<tr class="even">
<td>Read units</td>
<td>50,000 per day</td>
</tr>
<tr class="odd">
<td>Real-time update units</td>
<td>50,000 per day</td>
</tr>
<tr class="even">
<td>Write units</td>
<td>40,000 per day</td>
</tr>
<tr class="odd">
<td>Outbound data transfer</td>
<td>10 GiB per month</td>
</tr>
</tbody>
</table>

The following operations and features don't include free usage. You must [enable billing](/billing/docs/how-to/modify-project) to use these features:

  - Managed deletes (TTL)
  - PITR data
  - Backup data
  - Restore operations
  - Clone operations

## Limits

The following tables show the limits that apply to Firestore. These are hard limits unless otherwise noted.

### Databases

### Standard edition

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Limit</th>
<th>Details</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Maximum number of databases per project</td>
<td><p>100</p>
<p>You can <a href="/support-hub">contact support</a> to request an increase to this limit.</p></td>
</tr>
<tr class="even">
<td>Maximum number of <a href="/firestore/docs/cmek">customer-managed encryption keys (CMEK) databases</a> per project</td>
<td><p>0</p>
<p>By default the quota is 0 because this feature is behind an allowlist. You can request to increase the quota by filling in <a href="https://docs.google.com/forms/d/e/1FAIpQLSfKs8wJf4IXu1NizvfyU2vT59JDbdPvkehMVZ2ab5l_aDLIIA/viewform?resourcekey=0-O15dlRFvA0JIDmh6VFUEcA">the CMEK access request form</a> .</p></td>
</tr>
</tbody>
</table>

### Enterprise edition

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Limit</th>
<th>Details</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Maximum number of databases per project</td>
<td><p>100</p>
<p>You can <a href="/support-hub">contact support</a> to request an increase to this limit.</p></td>
</tr>
<tr class="even">
<td>Maximum number of <a href="/firestore/docs/cmek">customer-managed encryption keys (CMEK) databases</a> per project</td>
<td><p>0</p>
<p>By default the quota is 0 because this feature is behind an allowlist. You can request to increase the quota by filling in <a href="https://docs.google.com/forms/d/e/1FAIpQLSfKs8wJf4IXu1NizvfyU2vT59JDbdPvkehMVZ2ab5l_aDLIIA/viewform?resourcekey=0-O15dlRFvA0JIDmh6VFUEcA">the CMEK access request form</a> .</p></td>
</tr>
</tbody>
</table>

### Collections, documents, and fields

### Standard edition

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Limit</th>
<th>Details</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Constraints on collection IDs</td>
<td><ul>
<li>Must be valid UTF-8 characters</li>
<li>Must be no longer than 1,500 bytes</li>
<li>Cannot contain a forward slash ( <code dir="ltr" translate="no">            /           </code> )</li>
<li>Cannot solely consist of a single period ( <code dir="ltr" translate="no">            .           </code> ) or double periods ( <code dir="ltr" translate="no">            ..           </code> )</li>
<li>Cannot match the regular expression <code dir="ltr" translate="no">            __.*__           </code></li>
</ul></td>
</tr>
<tr class="even">
<td>Maximum depth of subcollections</td>
<td>100</td>
</tr>
<tr class="odd">
<td>Constraints on document IDs</td>
<td><ul>
<li>Must be valid UTF-8 characters</li>
<li>Must be no longer than 1,500 bytes</li>
<li>Cannot contain a forward slash ( <code dir="ltr" translate="no">            /           </code> )</li>
<li>Cannot solely consist of a single period ( <code dir="ltr" translate="no">            .           </code> ) or double periods ( <code dir="ltr" translate="no">            ..           </code> )</li>
<li>Cannot match the regular expression <code dir="ltr" translate="no">            __.*__           </code></li>
<li>If you import Datastore entities into a Firestore database, numeric entity IDs are exposed as <code dir="ltr" translate="no">            __id[0-9]+__           </code></li>
</ul></td>
</tr>
<tr class="even">
<td>Maximum size for a document name</td>
<td>6 KiB</td>
</tr>
<tr class="odd">
<td>Maximum size for a document</td>
<td>1 MiB (1,048,576 bytes)</td>
</tr>
<tr class="even">
<td>Constraints on field names</td>
<td><ul>
<li>Must be valid UTF-8 characters</li>
<li>Cannot match the regular expression <code dir="ltr" translate="no">            __.*__           </code></li>
</ul></td>
</tr>
<tr class="odd">
<td>Maximum size of a field name</td>
<td>1,500 bytes</td>
</tr>
<tr class="even">
<td>Constraints on field paths</td>
<td><ul>
<li>Must separate field names with a single period ( <code dir="ltr" translate="no">            .           </code> )</li>
<li>May be passed as a dot-delimited ( <code dir="ltr" translate="no">            .           </code> ) string of segments where each segment is either a simple field name or a quoted field name (defined below).</li>
</ul>
A simple field name is one where all of the following are true:
<ul>
<li>Contains only the characters <code dir="ltr" translate="no">            a-z           </code> , <code dir="ltr" translate="no">            A-Z           </code> , <code dir="ltr" translate="no">            0-9           </code> , and underscore ( <code dir="ltr" translate="no">            _           </code> )</li>
<li>Does not start with <code dir="ltr" translate="no">            0-9           </code></li>
</ul>
A quoted field name starts and ends with the backtick character ( <code dir="ltr" translate="no">          `         </code> ). For example, <code dir="ltr" translate="no">          foo.`x&amp;y`         </code> refers to the <code dir="ltr" translate="no">          x&amp;y         </code> field nested under the <code dir="ltr" translate="no">          foo         </code> field. To construct a field name with the backtick character, escape the backtick character with the backslash character ( <code dir="ltr" translate="no">          \         </code> ). For convenience, you can avoid quoted field names by passing the field path as a FieldPath object ( <a href="https://firebase.google.com/docs/reference/js/firestore_.fieldpath">for example, see JavaScript FieldPath</a> ).</td>
</tr>
<tr class="odd">
<td>Maximum size of a field path</td>
<td>1,500 bytes</td>
</tr>
<tr class="even">
<td>Maximum size of a field value</td>
<td>1 MiB - 89 bytes (1,048,487 bytes)</td>
</tr>
<tr class="odd">
<td>Maximum depth of fields in a map or array</td>
<td><p>20</p>
<p>Map and array fields add one level to the overall depth of an object. For example, the following object has a total depth of three levels:</p>
<pre class="text" dir="ltr" data-is-upgraded="" translate="no"><code>{
  nested_map: {         #depth 1
    nested_array: [     #depth 2
      {
        foo: &quot;bar&quot;      #depth 3
      }
    ]
  }
}
      </code></pre></td>
</tr>
</tbody>
</table>

### Enterprise edition

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Limit</th>
<th>Details</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Constraints on collection IDs</td>
<td><ul>
<li>Must be valid UTF-8 characters</li>
<li>Must be no longer than 1,500 bytes</li>
<li>Cannot contain a forward slash ( <code dir="ltr" translate="no">            /           </code> )</li>
<li>Cannot solely consist of a single period ( <code dir="ltr" translate="no">            .           </code> ) or double periods ( <code dir="ltr" translate="no">            ..           </code> )</li>
<li>Cannot match the regular expression <code dir="ltr" translate="no">            __.*__           </code></li>
</ul></td>
</tr>
<tr class="even">
<td>Maximum depth of subcollections</td>
<td>100</td>
</tr>
<tr class="odd">
<td>Constraints on document IDs</td>
<td><ul>
<li>Must be valid UTF-8 characters</li>
<li>Must be no longer than 1,500 bytes</li>
<li>Cannot contain a forward slash ( <code dir="ltr" translate="no">            /           </code> )</li>
<li>Cannot solely consist of a single period ( <code dir="ltr" translate="no">            .           </code> ) or double periods ( <code dir="ltr" translate="no">            ..           </code> )</li>
<li>Cannot match the regular expression <code dir="ltr" translate="no">            __.*__           </code></li>
<li>If you import Datastore entities into a Firestore database, numeric entity IDs are exposed as <code dir="ltr" translate="no">            __id[0-9]+__           </code></li>
</ul></td>
</tr>
<tr class="even">
<td>Maximum size for a document name</td>
<td>6 KiB</td>
</tr>
<tr class="odd">
<td>Maximum size for a document</td>
<td>1 MiB (1,048,576 bytes)</td>
</tr>
<tr class="even">
<td>Constraints on field names</td>
<td><ul>
<li>Must be valid UTF-8 characters</li>
<li>Cannot match the regular expression <code dir="ltr" translate="no">            __.*__           </code></li>
</ul></td>
</tr>
<tr class="odd">
<td>Maximum size of a field name</td>
<td>1,500 bytes</td>
</tr>
<tr class="even">
<td>Constraints on field paths</td>
<td><ul>
<li>Must separate field names with a single period ( <code dir="ltr" translate="no">            .           </code> )</li>
<li>May be passed as a dot-delimited ( <code dir="ltr" translate="no">            .           </code> ) string of segments where each segment is either a simple field name or a quoted field name (defined below).</li>
</ul>
A simple field name is one where all of the following are true:
<ul>
<li>Contains only the characters <code dir="ltr" translate="no">            a-z           </code> , <code dir="ltr" translate="no">            A-Z           </code> , <code dir="ltr" translate="no">            0-9           </code> , and underscore ( <code dir="ltr" translate="no">            _           </code> )</li>
<li>Does not start with <code dir="ltr" translate="no">            0-9           </code></li>
</ul>
A quoted field name starts and ends with the backtick character ( <code dir="ltr" translate="no">          `         </code> ). For example, <code dir="ltr" translate="no">          foo.`x&amp;y`         </code> refers to the <code dir="ltr" translate="no">          x&amp;y         </code> field nested under the <code dir="ltr" translate="no">          foo         </code> field. To construct a field name with the backtick character, escape the backtick character with the backslash character ( <code dir="ltr" translate="no">          \         </code> ). For convenience, you can avoid quoted field names by passing the field path as a FieldPath object ( <a href="https://firebase.google.com/docs/reference/js/firestore_.fieldpath">for example, see JavaScript FieldPath</a> ).</td>
</tr>
<tr class="odd">
<td>Maximum size of a field path</td>
<td>1,500 bytes</td>
</tr>
<tr class="even">
<td>Maximum size of a field value</td>
<td>1 MiB - 89 bytes (1,048,487 bytes)</td>
</tr>
<tr class="odd">
<td>Maximum depth of fields in a map or array</td>
<td><p>20</p>
<p>Map and array fields add one level to the overall depth of an object. For example, the following object has a total depth of three levels:</p>
<pre class="text" dir="ltr" data-is-upgraded="" translate="no"><code>{
  nested_map: {         #depth 1
    nested_array: [     #depth 2
      {
        foo: &quot;bar&quot;      #depth 3
      }
    ]
  }
}
      </code></pre></td>
</tr>
</tbody>
</table>

### Writes and transactions

### Standard edition

<table>
<thead>
<tr class="header">
<th>Limit</th>
<th>Details</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Maximum API request size</td>
<td>10 MiB</td>
</tr>
<tr class="even">
<td>Time limit for a transaction</td>
<td>270 seconds, with a 60-second idle expiration time</td>
</tr>
<tr class="odd">
<td>Maximum number of field transformations that can be performed on a single document in a <code dir="ltr" translate="no">          Commit         </code> operation or in a transaction</td>
<td>500</td>
</tr>
</tbody>
</table>

### Enterprise edition

<table>
<thead>
<tr class="header">
<th>Limit</th>
<th>Details</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Maximum API request size</td>
<td>10 MiB</td>
</tr>
<tr class="even">
<td>Time limit for a transaction</td>
<td>270 seconds, with a 60-second idle expiration time</td>
</tr>
<tr class="odd">
<td>Maximum number of field transformations that can be performed on a single document in a <code dir="ltr" translate="no">          Commit         </code> operation or in a transaction</td>
<td>500</td>
</tr>
</tbody>
</table>

### Indexes

### Standard edition

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Limit</th>
<th>Details</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Maximum number of composite indexes for a database</td>
<td><ul>
<li><p>200 when you have not enabled billing for your Google Cloud project.</p>
<p>If you need more quota, you must <a href="https://cloud.google.com/billing/docs/how-to/modify-project">enable billing for your Google Cloud project.</a></p></li>
<li><p>1000 when you enable billing for your Google Cloud project.</p>
<p>You can <a href="/support-hub">contact support</a> to request an increase to this limit.</p></li>
</ul></td>
</tr>
<tr class="even">
<td>Maximum number of single-field configurations for a database</td>
<td><ul>
<li><p>200 when you have not enabled billing for your Google Cloud project.</p>
<p>If you need more quota, you must <a href="https://cloud.google.com/billing/docs/how-to/modify-project">enable billing for your Google Cloud project.</a></p></li>
<li>1000 when you enable billing for your Google Cloud project.</li>
</ul>
<p>One field level configuration can contain multiple configurations for the same field. For example, a single-field indexing exemption and a TTL policy on the same field count as one field configuration towards the limit.</p></td>
</tr>
<tr class="odd">
<td><p>Maximum number of index entries for each document</p></td>
<td><p>40,000</p>
<p>The number of index entries is the sum of the following for a document:</p>
<ul>
<li>The number of single-field index entries</li>
<li>The number of composite index entries</li>
</ul>
<p>To see how Firestore turns a document and a set of indexes into index entries, see <a href="/firestore/docs/concepts/index-overview#index_entries">this index entry count example</a> .</p></td>
</tr>
<tr class="even">
<td>Maximum number of fields in a composite index</td>
<td>100</td>
</tr>
<tr class="odd">
<td>Maximum size of an index entry</td>
<td><p>7.5 KiB</p>
<p>To see how Firestore calculates index entry size, see <a href="/firestore/docs/storage-size#index-entry-size">index entry size</a> .</p></td>
</tr>
<tr class="even">
<td>Maximum sum of the sizes of a document's index entries</td>
<td><p>8 MiB</p>
<p>The total size is the sum of the following for a document:</p>
The sum of the size of a document's single-field index entries
The sum of the size of a document's composite index entries</td>
</tr>
<tr class="odd">
<td>Maximum size of an indexed field value</td>
<td><p>1500 bytes</p>
<p>Field values over 1500 bytes are truncated. Queries involving truncated field values may return inconsistent results.</p></td>
</tr>
</tbody>
</table>

### Enterprise edition

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Limit</th>
<th>Details</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Maximum number of indexes for a database</td>
<td><ul>
<li><p>200 when you have not enabled billing for your Google Cloud project.</p>
<p>If you need more quota, you must <a href="https://cloud.google.com/billing/docs/how-to/modify-project">enable billing for your Google Cloud project.</a></p></li>
<li><p>1000 when you enable billing for your Google Cloud project.</p>
<p>You can <a href="/support-hub">contact support</a> to request an increase to this limit.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Maximum number of index entries for each document</p></td>
<td><p>40,000</p></td>
</tr>
<tr class="odd">
<td>Maximum number of fields in an index</td>
<td>100</td>
</tr>
<tr class="even">
<td>Maximum size of an index entry</td>
<td><p>7.5 KiB</p>
<p>To see how Firestore calculates index entry size, see <a href="/firestore/docs/storage-size#index-entry-size">index entry size</a> .</p></td>
</tr>
<tr class="odd">
<td>Maximum sum of the sizes of a document's index entries</td>
<td><p>8 MiB</p></td>
</tr>
</tbody>
</table>

### Time-to-live (TTL)

### Standard edition

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Limit</th>
<th>Details</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Maximum number of TTL configurations for a database</td>
<td><ul>
<li><p>200 when you have not enabled billing for your Google Cloud project.</p>
<p>If you need more quota, you must <a href="https://cloud.google.com/billing/docs/how-to/modify-project">enable billing for your Google Cloud project.</a></p></li>
<li>1000 when you enable billing for your Google Cloud project.</li>
</ul></td>
</tr>
</tbody>
</table>

### Enterprise edition

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Limit</th>
<th>Details</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Maximum number of single-field configurations for a database</td>
<td><ul>
<li><p>200 when you have not enabled billing for your Google Cloud project.</p>
<p>If you need more quota, you must <a href="https://cloud.google.com/billing/docs/how-to/modify-project">enable billing for your Google Cloud project.</a></p></li>
<li>1000 when you enable billing for your Google Cloud project.</li>
</ul>
<p>One field level configuration can contain multiple configurations for the same field. For example, a single-field indexing exemption and a TTL policy on the same field count as one field configuration towards the limit.</p></td>
</tr>
</tbody>
</table>

### Export/Import

The following limits apply to [managed import and export operations](/firestore/docs/manage-data/export-import) :

### Standard edition

<table>
<thead>
<tr class="header">
<th>Limit</th>
<th>Details</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Maximum total number of both export and import requests for a project allowed per minute</td>
<td>20</td>
</tr>
<tr class="even">
<td>Maximum number of concurrent exports and imports</td>
<td>50</td>
</tr>
<tr class="odd">
<td>Maximum number of collection ID filters for export and import requests</td>
<td>100</td>
</tr>
</tbody>
</table>

### Enterprise edition

<table>
<thead>
<tr class="header">
<th>Limit</th>
<th>Details</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Maximum total number of both export and import requests for a project allowed per minute</td>
<td>20</td>
</tr>
<tr class="even">
<td>Maximum number of concurrent exports and imports</td>
<td>50</td>
</tr>
<tr class="odd">
<td>Maximum number of collection ID filters for export and import requests</td>
<td>100</td>
</tr>
</tbody>
</table>

### Security rules

### Standard edition

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Limit</th>
<th>Details</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Maximum number of <code dir="ltr" translate="no">          exists()         </code> , <code dir="ltr" translate="no">          get()         </code> , and <code dir="ltr" translate="no">          getAfter()         </code> calls per request</td>
<td><ul>
<li>10 for single-document requests and query requests.</li>
<li><p>20 for multi-document reads, transactions, and batched writes. The previous limit of 10 also applies to each operation.</p>
<p>For example, imagine you create a batched write request with 3 write operations and that your security rules use 2 document access calls to validate each write. In this case, each write uses 2 of its 10 access calls and the batched write request uses 6 of its 20 access calls.</p></li>
</ul>
<p>Exceeding either limit results in a permission denied error.</p>
<p>Some document access calls may be cached, and cached calls do not count towards the limits.</p></td>
</tr>
<tr class="even">
<td>Maximum nested <code dir="ltr" translate="no">          match         </code> statement depth</td>
<td>10</td>
</tr>
<tr class="odd">
<td>Maximum path length, in path segments, allowed within a set of nested <code dir="ltr" translate="no">          match         </code> statements</td>
<td>100</td>
</tr>
<tr class="even">
<td>Maximum number of path capture variables allowed within a set of nested <code dir="ltr" translate="no">          match         </code> statements</td>
<td>20</td>
</tr>
<tr class="odd">
<td>Maximum function call depth</td>
<td>20</td>
</tr>
<tr class="even">
<td>Maximum number of function arguments</td>
<td>7</td>
</tr>
<tr class="odd">
<td>Maximum number of <code dir="ltr" translate="no">          let         </code> variable bindings per function</td>
<td>10</td>
</tr>
<tr class="even">
<td>Maximum number of recursive or cyclical function calls</td>
<td>0 (not permitted)</td>
</tr>
<tr class="odd">
<td>Maximum number of expressions evaluated per request</td>
<td>1,000</td>
</tr>
<tr class="even">
<td>Maximum size of a ruleset</td>
<td>Rulesets must obey two size limits:
<ul>
<li>a 256 KB limit on the size of the ruleset text source published from the Firebase console or from the CLI using <code dir="ltr" translate="no">            firebase deploy           </code> .</li>
<li>a 250 KB limit on the size of the compiled ruleset that results when Firebase processes the source and makes it active on the back-end.</li>
</ul></td>
</tr>
</tbody>
</table>

### Enterprise edition

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Limit</th>
<th>Details</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Maximum number of <code dir="ltr" translate="no">          exists()         </code> , <code dir="ltr" translate="no">          get()         </code> , and <code dir="ltr" translate="no">          getAfter()         </code> calls per request</td>
<td><ul>
<li>10 for single-document requests and query requests.</li>
<li><p>20 for multi-document reads, transactions, and batched writes. The previous limit of 10 also applies to each operation.</p>
<p>For example, imagine you create a batched write request with 3 write operations and that your security rules use 2 document access calls to validate each write. In this case, each write uses 2 of its 10 access calls and the batched write request uses 6 of its 20 access calls.</p></li>
</ul>
<p>Exceeding either limit results in a permission denied error.</p>
<p>Some document access calls may be cached, and cached calls do not count towards the limits.</p></td>
</tr>
<tr class="even">
<td>Maximum nested <code dir="ltr" translate="no">          match         </code> statement depth</td>
<td>10</td>
</tr>
<tr class="odd">
<td>Maximum path length, in path segments, allowed within a set of nested <code dir="ltr" translate="no">          match         </code> statements</td>
<td>100</td>
</tr>
<tr class="even">
<td>Maximum number of path capture variables allowed within a set of nested <code dir="ltr" translate="no">          match         </code> statements</td>
<td>20</td>
</tr>
<tr class="odd">
<td>Maximum function call depth</td>
<td>20</td>
</tr>
<tr class="even">
<td>Maximum number of function arguments</td>
<td>7</td>
</tr>
<tr class="odd">
<td>Maximum number of <code dir="ltr" translate="no">          let         </code> variable bindings per function</td>
<td>10</td>
</tr>
<tr class="even">
<td>Maximum number of recursive or cyclical function calls</td>
<td>0 (not permitted)</td>
</tr>
<tr class="odd">
<td>Maximum number of expressions evaluated per request</td>
<td>1,000</td>
</tr>
<tr class="even">
<td>Maximum size of a ruleset</td>
<td>Rulesets must obey two size limits:
<ul>
<li>a 256 KB limit on the size of the ruleset text source published from the Firebase console or from the CLI using <code dir="ltr" translate="no">            firebase deploy           </code> .</li>
<li>a 250 KB limit on the size of the compiled ruleset that results when Firebase processes the source and makes it active on the back-end.</li>
</ul></td>
</tr>
</tbody>
</table>
