# Quotas and limits

This page describes the request quotas and limits for Firestore with MongoDB compatibility.

## Free tier usage

Firestore with MongoDB compatibility offers a free tier that lets you get started with Firestore with MongoDB compatibility at no cost. The free tier amounts are listed in the following table.

Free tier amounts are applied daily and reset at midnight Pacific time.

The free tier applies to only one Firestore with MongoDB compatibility database per project. The first database that is created in a project without a free tier database will get the free tier. If the database with the free tier applied is deleted, the next database created will receive the free tier.

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
<td>Write units</td>
<td>40,000 per day</td>
</tr>
<tr class="even">
<td>Outbound data transfer</td>
<td>10 GiB per month</td>
</tr>
</tbody>
</table>

The following operations and features don't include free usage. You must [enable billing](https://cloud.google.com/billing/docs/how-to/modify-project) to use these features:

  - Managed deletes (TTL)
  - Backup data
  - Restore operations

For more information about how these features are billed, see [Storage pricing](/firestore/enterprise/pricing#storage-size) .

## Standard limits

The following tables show the limits that apply to Firestore with MongoDB compatibility. These are hard limits unless otherwise noted.

### Databases

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
<p><a href="https://cloud.google.com/support-hub">Contact support</a> to request an increase to this limit.</p></td>
</tr>
<tr class="even">
<td>Maximum number of <a href="/firestore/mongodb-compatibility/docs/cmek">customer-managed encryption keys (CMEK) databases</a> per project</td>
<td><p>0</p>
<p>By default the quota is 0 because this feature is behind an allowlist. You can request to increase the quota by filling in <a href="https://docs.google.com/forms/d/e/1FAIpQLSfKs8wJf4IXu1NizvfyU2vT59JDbdPvkehMVZ2ab5l_aDLIIA/viewform?resourcekey=0-O15dlRFvA0JIDmh6VFUEcA">the CMEK access request form</a> .</p></td>
</tr>
</tbody>
</table>

### Collections, documents, and fields

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
<td>Constraints on collection names</td>
<td><ul>
<li>Must be valid UTF-8 characters</li>
<li>Must be no longer than 1,500 bytes</li>
<li>Can't match the regular expression <code dir="ltr" translate="no">         __.*__        </code></li>
<li>Can't contain <code dir="ltr" translate="no">         $        </code></li>
<li>Can't be the empty string ( <code dir="ltr" translate="no">         ""        </code> )</li>
<li>Can't contain the null character</li>
<li>Can't begin with `system.` and can't contain `.system.`.</li>
</ul></td>
</tr>
<tr class="even">
<td>Constraints on document IDs ( <code dir="ltr" translate="no">       _id      </code> )</td>
<td><ul>
<li>Must be an ObjectId, String, 64-bit integer, 32-bit integer, Double, Binary, or Object. Other BSON types are not supported.</li>
<li>Must be no larger than 1,500 bytes</li>
<li><p>For Object-typed IDs:</p>
<ul>
<li>Each value within an Object-typed ID must also be of a supported ID type (ObjectId, String, 64-bit integer, 32-bit integer, Double, Binary, or Object) or an Array of values, each of which is of a supported ID type.</li>
</ul></li>
<li><p>For String-typed IDs:</p>
<ul>
<li>Must be valid UTF-8 characters</li>
<li>Can't match the regular expression <code dir="ltr" translate="no">           __.*__          </code></li>
</ul></li>
</ul></td>
</tr>
<tr class="odd">
<td>Maximum size for a document</td>
<td>4 MiB</td>
</tr>
<tr class="even">
<td>Constraints on field names</td>
<td><ul>
<li>Must be valid UTF-8 characters</li>
<li>Can't be the empty string ( <code dir="ltr" translate="no">         ""        </code> )</li>
<li>Can't match the regular expression <code dir="ltr" translate="no">         __.*__        </code></li>
</ul></td>
</tr>
<tr class="odd">
<td>Maximum size of a field name</td>
<td>1,500 bytes</td>
</tr>
<tr class="even">
<td>Maximum size of a field path</td>
<td>1,500 bytes</td>
</tr>
<tr class="odd">
<td>Maximum size of a field value</td>
<td>4 MiB - 89 bytes</td>
</tr>
<tr class="even">
<td>Maximum depth of fields in a map or array</td>
<td><p>20</p>
<p>Map and array fields add one level to the overall depth of an object. For example, the following object has a total depth of three levels:</p>
<pre class="text" dir="ltr" data-is-upgraded="" translate="no"><code>{
  nested_object: {      #depth 1
    nested_array: [     #depth 2
      {
        foo: &quot;bar&quot;      #depth 3
      }
    ]
  }
}</code></pre></td>
</tr>
</tbody>
</table>

### Reads, writes, and transactions

<table>
<thead>
<tr class="header">
<th>Limit</th>
<th>Details</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Memory limit for a query</td>
<td>128 MiB</td>
</tr>
<tr class="even">
<td>Time limit for a transaction</td>
<td>270 seconds, with a 60-second idle expiration time</td>
</tr>
</tbody>
</table>

### Indexes

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
<td><p>1000</p>
<p><a href="https://cloud.google.com/support-hub">Contact support</a> to request an increase to this limit.</p></td>
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
<td><p>7.5 KiB</p></td>
</tr>
<tr class="odd">
<td>Maximum sum of the sizes of a document's index entries</td>
<td><p>8 MiB</p></td>
</tr>
</tbody>
</table>

### Time to live (TTL)

<table>
<thead>
<tr class="header">
<th>Limit</th>
<th>Details</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Maximum number of TTL configurations for a database</td>
<td><p>500</p></td>
</tr>
</tbody>
</table>

### Saved queries limits

**Preview — Saved queries**

This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

<table>
<thead>
<tr class="header">
<th>Value</th>
<th>Limit</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Maximum number of saved queries per project (including saved queries for other Google Cloud products)</td>
<td>10,000</td>
</tr>
<tr class="even">
<td>Maximum size for each query</td>
<td>1 MiB</td>
</tr>
</tbody>
</table>
