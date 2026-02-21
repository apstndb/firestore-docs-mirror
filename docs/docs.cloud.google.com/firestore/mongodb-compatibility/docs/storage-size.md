# Storage size calculations

This page describes the storage size of documents, fields, and index entries in Firestore with MongoDB compatibility.

You can learn about the costs of this storage at the [Pricing](https://cloud.google.com/firestore/enterprise/pricing) page.

## String size

String sizes are calculated as the number of [UTF-8 encoded](https://en.wikipedia.org/wiki/UTF-8) bytes + 1.

The following are stored as strings:

  - Collection name
  - Field names
  - String field values (including `  _id  ` )

For example:

  - The collection name `  tasks  ` uses 5 bytes + 1 byte, for a total of 6 bytes.
  - The field name `  description  ` uses 11 bytes + 1 byte, for a total of 12 bytes.

## Field value size

The following table shows the size of field values by type.

<table>
<thead>
<tr class="header">
<th>Type</th>
<th>Size</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Array</td>
<td>The sum of the sizes of its values</td>
</tr>
<tr class="even">
<td>Boolean</td>
<td>1 byte</td>
</tr>
<tr class="odd">
<td>Binary data</td>
<td>Byte length + 1 for a non-generic (non-0) subtype</td>
</tr>
<tr class="even">
<td>Date</td>
<td>8 bytes</td>
</tr>
<tr class="odd">
<td>Double</td>
<td>8 bytes</td>
</tr>
<tr class="even">
<td>Double128</td>
<td>16 bytes</td>
</tr>
<tr class="odd">
<td>32-bit integer</td>
<td>4 bytes</td>
</tr>
<tr class="even">
<td>64-bit integer (long)</td>
<td>8 bytes</td>
</tr>
<tr class="odd">
<td>Object</td>
<td>The sum of the string sizes of each field name and the sizes of each field falue in the embedded object</td>
</tr>
<tr class="even">
<td>Min Key</td>
<td>1 byte</td>
</tr>
<tr class="odd">
<td>Max Key</td>
<td>1 byte</td>
</tr>
<tr class="even">
<td>Null</td>
<td>1 byte</td>
</tr>
<tr class="odd">
<td>Regular expression</td>
<td>(Pattern length + 1) + (Options length + 1)</td>
</tr>
<tr class="even">
<td>Timestamp</td>
<td>8 bytes</td>
</tr>
<tr class="odd">
<td>String</td>
<td>Number of UTF-8 encoded bytes + 1</td>
</tr>
</tbody>
</table>

For example, a boolean field named `  done  ` would use 6 bytes:

  - 5 bytes for the `  done  ` field name
  - 1 byte for the boolean value

## Document size

The size of a document is the sum of:

  - The [string size](#string-size) of the collection name
  - The sum of the [string size](#string-size) of each field name (except `  _id  ` )
  - The sum of the size of each [field value](#field-size) (including `  _id  ` )
  - 48 additional bytes

This example is for a document in collection `  tasks  ` :

``` text
{
  "_id": "my_task_id",
  "type": "Personal",
  "done": false,
  "priority": 1,
  "description": "Learn Cloud Firestore"
}
```

The total size of the fields is 78 bytes:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Field name and value</th>
<th>Field size in bytes</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       "_id": "my_task_id"      </code></td>
<td>11 for the field's string value</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       "type": "Personal"      </code></td>
<td>14<br />
5 for the field name + 9 for the field's string value</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       "done": false      </code></td>
<td>6<br />
5 for the field name + 1 for the field's boolean value</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       "priority": 1      </code></td>
<td>17<br />
9 for the field name + 4 for the field's 32-bit integer value</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       "description": "Learn Cloud Firestore"      </code></td>
<td>34<br />
12 for the field name + 22 for the field's string value</td>
</tr>
</tbody>
</table>

So the document size is 6 + 78 + 48 = 132 bytes:

  - 6 for the collection name
  - 78 bytes for the fields
  - 48 additional bytes

## Index entry size

The size of an index entry in an index is the sum of:

  - The [string size](#string-size) of the collection name
  - The size of the `  _id  ` field value
  - The sum of the indexed [field values](#field-size)
  - 48 additional bytes

Consider a document in the `  tasks  ` collection:

``` text
{
  "_id": "my_task_id",
  "type": "Personal",
  "done": false,
  "priority": 1,
  "description": "Learn Cloud Firestore"
}
```

For an index on the `  done  ` and `  priority  ` fields (both ascending), the total size of the index entry in this index is 70 bytes:

  - 6 bytes for the collection name `  tasks  `
  - 11 bytes for the `  _id  ` field value
  - 1 byte for the boolean field value
  - 4 bytes for the 32-bit integer field value
  - 48 additional bytes

For sparse indexes, if a document doesn't include any of the fields, then no index entry is created. If a document contains at least one of the indexed fields, an index entry is created with absent indexed fields set to `  NULL  ` .

## What's next

Learn about [pricing](https://cloud.google.com/firestore/enterprise/pricing) .
