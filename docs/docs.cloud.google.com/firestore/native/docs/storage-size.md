# Storage size calculations

This page describes the storage size of documents, document names, fields, and index entries in Firestore.

You can learn about the costs of this storage at [Firestore Pricing](/firestore/pricing) .

## String size

String sizes are calculated as the number of [UTF-8 encoded](https://en.wikipedia.org/wiki/UTF-8) bytes + 1.

The following are stored as strings:

  - Collection IDs
  - String document IDs
  - Document names
  - Field names
  - String field values

For example:

  - The collection ID `  tasks  ` uses 5 bytes + 1 byte, for a total of 6 bytes.
  - The field name `  description  ` uses 11 bytes + 1 byte, for a total of 12 bytes.

## Document ID size

The size of a document ID is either the [string size](#string-size) for a string ID or 8 bytes for an integer ID.

**Note:** The Firestore client libraries always use string document IDs.

## Document name size

The size of a document name is the sum of:

  - The size of each collection ID and document ID in the path to the document
  - 16 additional bytes

For a document in the subcollection `  users/jeff/tasks  ` with a string document ID of `  my_task_id  ` , the document name size is 6 + 5 + 6 + 11 + 16 = 44 bytes:

  - 6 bytes for the `  users  ` collection ID
  - 5 bytes for the `  jeff  ` document ID
  - 6 bytes for the `  tasks  ` collection ID
  - 11 bytes for the `  my_task_id  ` document ID
  - 16 additional bytes

**Note:** Any documents in subcollections under the document, for example `  users/jeff/tasks/my_task_id/comments/D8PvloqiczrzXik3SWjZ  ` , aren't counted towards the document name size or the 1 MiB limit for the `  users/jeff/tasks/my_task_id  ` document.

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
<td>Bytes</td>
<td>Byte length</td>
</tr>
<tr class="even">
<td>Date and time</td>
<td>8 bytes</td>
</tr>
<tr class="odd">
<td>Floating-point number</td>
<td>8 bytes</td>
</tr>
<tr class="even">
<td>Geographical point</td>
<td>16 bytes</td>
</tr>
<tr class="odd">
<td>Integer</td>
<td>8 bytes</td>
</tr>
<tr class="even">
<td>Map</td>
<td>The size of the map, calculated the same way as <a href="#document-size">document size</a></td>
</tr>
<tr class="odd">
<td>Null</td>
<td>1 byte</td>
</tr>
<tr class="even">
<td>Reference</td>
<td>The <a href="#document-name-size">document name size</a></td>
</tr>
<tr class="odd">
<td>Text string</td>
<td>Number of UTF-8 encoded bytes + 1</td>
</tr>
<tr class="even">
<td>Vector</td>
<td>8 bytes per dimension</td>
</tr>
</tbody>
</table>

For example, a boolean field named `  done  ` would use 6 bytes:

  - 5 bytes for the `  done  ` field name
  - 1 byte for the boolean value

**Note:** Field values in an index are truncated after 1500 bytes, see [indexing limits](/firestore/native/docs/quotas#indexes) .

## Document size

The size of a document is the sum of:

  - The [document name size](#document-name-size)
  - The sum of the [string size](#string-size) of each field name
  - The sum of the size of each [field value](#field-size)
  - 32 additional bytes

This example is for a document in subcollection `  users/jeff/tasks  ` with a string document ID of `  my_task_id  ` :

``` text
 - "type": "Personal"
 - "done": false
 - "priority": 1
 - "description": "Learn Cloud Firestore"
```

The total size of the fields is 71 bytes:

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
<td><code dir="ltr" translate="no">       "type": "Personal"      </code></td>
<td>14<br />
5 for the field name + 9 for the field's string value</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       "done": false      </code></td>
<td>6<br />
5 for the field name + 1 for the field's boolean value</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       "priority": 1      </code></td>
<td>17<br />
9 for the field name + 8 for the field's integer value</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       "description": "Learn Cloud Firestore"      </code></td>
<td>34<br />
12 for the field name + 22 for the field's string value</td>
</tr>
</tbody>
</table>

So the document size is 44 + 71 + 32 = 147 bytes:

  - 44 bytes for the document name
  - 71 bytes for the fields
  - 32 additional bytes

**Note:** Any documents in subcollections under the document, for example `  users/jeff/tasks/my_task_id/comments/D8PvloqiczrzXik3SWjZ  ` , aren't counted towards the document name size or the 1 MiB limit for the `  users/jeff/tasks/my_task_id  ` document.

## Index entry size

Index entry sizes are calculated as follows for single-field and composite indexes.

### Single-field index entry size

The size of a single-field index entry depends on whether an index is scoped to a collection or a collection group.

#### Collection scope

The size of an entry in a single-field index with collection scope is the sum of:

  - The [document name size](#document-name-size) of the indexed document
  - The [document name size](#document-name-size) of the indexed document's parent document
  - The [string size](#string-size) of the indexed field name
  - The size of the indexed [field value](#field-size)
  - 32 additional bytes

Consider a document in the sub-collection `  users/jeff/tasks  ` with a string document ID of `  my_task_id  ` :

``` text
 - "type": "Personal"
 - "done": false
 - "priority": 1
 - "description": "Learn Cloud Firestore"
```

For a single-field index with collection scope that indexes the `  done  ` field, the total size of the entry in this index is 109 bytes:

  - 44 bytes for the document name `  users/jeff/tasks/my_task_id  `
  - 27 bytes for the parent document's document name `  users/jeff  `
  - 5 bytes for the `  done  ` field name
  - 1 byte for the boolean field value
  - 32 additional bytes

#### Collection group scope

The size of an entry in a single-field index with collection group scope is the sum of:

  - The [document name size](#document-name-size) of the indexed document
  - The [string size](#string-size) of the indexed field name
  - The size of the indexed [field value](#field-size)
  - 48 additional bytes

Consider a document in the sub-collection `  users/jeff/tasks  ` with a string document ID of `  my_task_id  ` :

``` text
 - "type": "Personal"
 - "done": false
 - "priority": 1
 - "description": "Learn Cloud Firestore"
```

For a single-field index with collection group scope that indexes the `  done  ` field, the total size of the entry in this index is 98 bytes:

  - 44 bytes for the document name `  users/jeff/tasks/my_task_id  `
  - 5 bytes for the `  done  ` field name
  - 1 byte for the boolean field value
  - 48 additional bytes

### Composite index entry size

The size of an entry in a composite index depends on whether the index is scoped to a collection or a collection group.

#### Collection scope

The size of an index entry in a composite index with collection scope is the sum of:

  - The [document name size](#document-name-size) of the indexed document
  - The [document name size](#document-name-size) of the indexed document's parent document
  - The sum of the indexed [field values](#field-size)
  - 32 additional bytes

Consider a document in the sub-collection `  users/jeff/tasks  ` with a string document ID of `  my_task_id  ` :

``` text
 - "type": "Personal"
 - "done": false
 - "priority": 1
 - "description": "Learn Cloud Firestore"
```

For a composite index with collection scope that indexes the `  done  ` and `  priority  ` fields (both ascending), the total size of the entry in this index is 112 bytes:

  - 44 bytes for the document name `  users/jeff/tasks/my_task_id  `
  - 27 bytes for the parent document's document name `  users/jeff  `
  - 1 byte for the boolean field value
  - 8 bytes for the integer field value
  - 32 additional bytes

#### Collection group scope

The size of an index entry in a composite index with collection group scope is the sum of:

  - The [document name size](#document-name-size) of the indexed document
  - The sum of the indexed [field values](#field-size)
  - 32 additional bytes

Consider a document in the sub-collection `  users/jeff/tasks  ` with a string document ID of `  my_task_id  ` :

``` text
 - "type": "Personal"
 - "done": false
 - "priority": 1
 - "description": "Learn Cloud Firestore"
```

For a composite index with collection group scope that indexes the `  done  ` and `  priority  ` fields (both ascending), the total size of the index entry in this index is 85 bytes:

  - 44 bytes for the document name `  users/jeff/tasks/my_task_id  `
  - 1 byte for the boolean field value
  - 8 bytes for the integer field value
  - 32 additional bytes

## What's next

Learn about [Firestore pricing](/firestore/pricing) .
