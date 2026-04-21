# Storage size calculations

This page describes the storage size of documents, document names, fields, and index entries in Firestore.

You can learn about the costs of this storage at [Firestore Pricing](https://docs.cloud.google.com/firestore/pricing) .

## String size

String sizes are calculated as the number of [UTF-8 encoded](https://en.wikipedia.org/wiki/UTF-8) bytes + 1.

The following are stored as strings:

  - Collection IDs
  - String document IDs
  - Document names
  - Field names
  - String field values

For example:

  - The collection ID `tasks` uses 5 bytes + 1 byte, for a total of 6 bytes.
  - The field name `description` uses 11 bytes + 1 byte, for a total of 12 bytes.

## Document ID size

The size of a document ID is either the [string size](https://docs.cloud.google.com/firestore/native/docs/storage-size#string-size) for a string ID or 8 bytes for an integer ID.

> **Note:** The Firestore client libraries always use string document IDs.

## Document name size

The size of a document name is the sum of:

  - The size of each collection ID and document ID in the path to the document
  - 16 additional bytes

For a document in the subcollection `users/jeff/tasks` with a string document ID of `my_task_id` , the document name size is 6 + 5 + 6 + 11 + 16 = 44 bytes:

  - 6 bytes for the `users` collection ID
  - 5 bytes for the `jeff` document ID
  - 6 bytes for the `tasks` collection ID
  - 11 bytes for the `my_task_id` document ID
  - 16 additional bytes

> **Note:** Any documents in subcollections under the document, for example `users/jeff/tasks/my_task_id/comments/D8PvloqiczrzXik3SWjZ` , aren't counted towards the document name size or the 1 MiB limit for the `users/jeff/tasks/my_task_id` document.

## Field value size

The following table shows the size of field values by type.

| Type                  | Size                                                                                                                                            |
| --------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------- |
| Array                 | The sum of the sizes of its values                                                                                                              |
| Boolean               | 1 byte                                                                                                                                          |
| Bytes                 | Byte length                                                                                                                                     |
| Date and time         | 8 bytes                                                                                                                                         |
| Floating-point number | 8 bytes                                                                                                                                         |
| Geographical point    | 16 bytes                                                                                                                                        |
| Integer               | 8 bytes                                                                                                                                         |
| Map                   | The size of the map, calculated the same way as [document size](https://docs.cloud.google.com/firestore/native/docs/storage-size#document-size) |
| Null                  | 1 byte                                                                                                                                          |
| Reference             | The [document name size](https://docs.cloud.google.com/firestore/native/docs/storage-size#document-name-size)                                   |
| Text string           | Number of UTF-8 encoded bytes + 1                                                                                                               |
| Vector                | 8 bytes per dimension                                                                                                                           |

For example, a boolean field named `done` would use 6 bytes:

  - 5 bytes for the `done` field name
  - 1 byte for the boolean value

> **Note:** Field values in an index are truncated after 1500 bytes, see [indexing limits](https://docs.cloud.google.com/firestore/native/docs/quotas#indexes) .

## Document size

The size of a document is the sum of:

  - The [document name size](https://docs.cloud.google.com/firestore/native/docs/storage-size#document-name-size)
  - The sum of the [string size](https://docs.cloud.google.com/firestore/native/docs/storage-size#string-size) of each field name
  - The sum of the size of each [field value](https://docs.cloud.google.com/firestore/native/docs/storage-size#field-size)
  - 32 additional bytes

This example is for a document in subcollection `users/jeff/tasks` with a string document ID of `my_task_id` :

``` 
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
<td><code dir="ltr" translate="no">"type": "Personal"</code></td>
<td>14<br />
5 for the field name + 9 for the field's string value</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">"done": false</code></td>
<td>6<br />
5 for the field name + 1 for the field's boolean value</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">"priority": 1</code></td>
<td>17<br />
9 for the field name + 8 for the field's integer value</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">"description": "Learn Cloud Firestore"</code></td>
<td>34<br />
12 for the field name + 22 for the field's string value</td>
</tr>
</tbody>
</table>

So the document size is 44 + 71 + 32 = 147 bytes:

  - 44 bytes for the document name
  - 71 bytes for the fields
  - 32 additional bytes

> **Note:** Any documents in subcollections under the document, for example `users/jeff/tasks/my_task_id/comments/D8PvloqiczrzXik3SWjZ` , aren't counted towards the document name size or the 1 MiB limit for the `users/jeff/tasks/my_task_id` document.

## Index entry size

Index entry sizes are calculated as follows for single-field and composite indexes.

### Single-field index entry size

The size of a single-field index entry depends on whether an index is scoped to a collection or a collection group.

#### Collection scope

The size of an entry in a single-field index with collection scope is the sum of:

  - The [document name size](https://docs.cloud.google.com/firestore/native/docs/storage-size#document-name-size) of the indexed document
  - The [document name size](https://docs.cloud.google.com/firestore/native/docs/storage-size#document-name-size) of the indexed document's parent document
  - The [string size](https://docs.cloud.google.com/firestore/native/docs/storage-size#string-size) of the indexed field name
  - The size of the indexed [field value](https://docs.cloud.google.com/firestore/native/docs/storage-size#field-size)
  - 32 additional bytes

Consider a document in the sub-collection `users/jeff/tasks` with a string document ID of `my_task_id` :

``` 
 - "type": "Personal"
 - "done": false
 - "priority": 1
 - "description": "Learn Cloud Firestore"
```

For a single-field index with collection scope that indexes the `done` field, the total size of the entry in this index is 109 bytes:

  - 44 bytes for the document name `users/jeff/tasks/my_task_id`
  - 27 bytes for the parent document's document name `users/jeff`
  - 5 bytes for the `done` field name
  - 1 byte for the boolean field value
  - 32 additional bytes

#### Collection group scope

The size of an entry in a single-field index with collection group scope is the sum of:

  - The [document name size](https://docs.cloud.google.com/firestore/native/docs/storage-size#document-name-size) of the indexed document
  - The [string size](https://docs.cloud.google.com/firestore/native/docs/storage-size#string-size) of the indexed field name
  - The size of the indexed [field value](https://docs.cloud.google.com/firestore/native/docs/storage-size#field-size)
  - 48 additional bytes

Consider a document in the sub-collection `users/jeff/tasks` with a string document ID of `my_task_id` :

``` 
 - "type": "Personal"
 - "done": false
 - "priority": 1
 - "description": "Learn Cloud Firestore"
```

For a single-field index with collection group scope that indexes the `done` field, the total size of the entry in this index is 98 bytes:

  - 44 bytes for the document name `users/jeff/tasks/my_task_id`
  - 5 bytes for the `done` field name
  - 1 byte for the boolean field value
  - 48 additional bytes

### Composite index entry size

The size of an entry in a composite index depends on whether the index is scoped to a collection or a collection group.

#### Collection scope

The size of an index entry in a composite index with collection scope is the sum of:

  - The [document name size](https://docs.cloud.google.com/firestore/native/docs/storage-size#document-name-size) of the indexed document
  - The [document name size](https://docs.cloud.google.com/firestore/native/docs/storage-size#document-name-size) of the indexed document's parent document
  - The sum of the indexed [field values](https://docs.cloud.google.com/firestore/native/docs/storage-size#field-size)
  - 32 additional bytes

Consider a document in the sub-collection `users/jeff/tasks` with a string document ID of `my_task_id` :

``` 
 - "type": "Personal"
 - "done": false
 - "priority": 1
 - "description": "Learn Cloud Firestore"
```

For a composite index with collection scope that indexes the `done` and `priority` fields (both ascending), the total size of the entry in this index is 112 bytes:

  - 44 bytes for the document name `users/jeff/tasks/my_task_id`
  - 27 bytes for the parent document's document name `users/jeff`
  - 1 byte for the boolean field value
  - 8 bytes for the integer field value
  - 32 additional bytes

#### Collection group scope

The size of an index entry in a composite index with collection group scope is the sum of:

  - The [document name size](https://docs.cloud.google.com/firestore/native/docs/storage-size#document-name-size) of the indexed document
  - The sum of the indexed [field values](https://docs.cloud.google.com/firestore/native/docs/storage-size#field-size)
  - 32 additional bytes

Consider a document in the sub-collection `users/jeff/tasks` with a string document ID of `my_task_id` :

``` 
 - "type": "Personal"
 - "done": false
 - "priority": 1
 - "description": "Learn Cloud Firestore"
```

For a composite index with collection group scope that indexes the `done` and `priority` fields (both ascending), the total size of the index entry in this index is 85 bytes:

  - 44 bytes for the document name `users/jeff/tasks/my_task_id`
  - 1 byte for the boolean field value
  - 8 bytes for the integer field value
  - 32 additional bytes

## Text search index entry size

The size of a text search index entry in an index is the sum of:

  - The string size of the collection name
  - The size of the document ID value
  - The sum of bytes from indexed field values (x2)
  - 48 additional bytes for general metadata

Consider an example for an insert event for a document with document ID `my_task_id` in the `tasks` collection:

    {
         "type": "Personal",
         "done": false,
         "priority": 1,
         "description": "Learn Cloud Firestore"
    }

The total size of a text search index entry on `description` is 105 bytes based on:

  - 6 bytes for the collection name `tasks`
  - 11 bytes for the document ID value
  - 44 bytes, based on 22 bytes for the `description` field x2
  - 48 additional bytes for general metadata

## Geospatial index entry size

The size of a geospatial index entry in an index is the sum of:

  - The string size of the collection name
  - The size of the document ID value
  - 128 bytes for each indexed geo point
  - 48 additional bytes for general metadata

Consider an example for an insert event for a document with document ID `my_place` in the `places` collection:

    {
         "type": "Restaurant",
         "visited": false,
         "priority": 1,
         "location": GeoPoint(longitude, latitude)
    }

The total size of a geospatial index entry on `location` is 192 bytes based on:

  - 7 bytes for the collection name `places`
  - 9 bytes for the document ID
  - 128 bytes for the `location` field
  - 48 additional bytes for general metadata

## What's next

Learn about [Firestore pricing](https://docs.cloud.google.com/firestore/pricing) .
