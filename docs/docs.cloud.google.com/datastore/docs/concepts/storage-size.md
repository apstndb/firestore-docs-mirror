This page describes the storage size of entities, keys, properties, and index entries in Firestore in Datastore mode. You can learn about the costs of this storage at [Datastore mode Pricing](/datastore/docs/pricing) .

## String size

String sizes are calculated as the number of [UTF-8 encoded](https://en.wikipedia.org/wiki/UTF-8) bytes + 1.

The following are stored as strings:

  - Keys
  - Kind names
  - Namespace names (the default namespace has size 0)
  - Property names
  - String property values

For example:

  - The name of the `  Task  ` kind uses 4 bytes + 1 byte, for a total of 5 bytes.
  - The name of the `  description  ` property uses 11 bytes + 1 byte, for a total of 12 bytes.
  - The name of the `  my_name_space  ` namespace uses 13 bytes + 1 byte, for a total of 14 bytes.

## Key size

The size of a key is the sum of

  - The namespace string size (if not in the default namespace)
  - The full key path string size (integer IDs are 8 bytes each)
  - 16 bytes

For a key of kind `  Task  ` in the default namespace with a numeric ID and no ancestor:

``` text
Task id:5730082031140864
```

The key size is 5 + 8 + 16 = 29 bytes:

  - 5 bytes for the `  Task  ` kind name
  - 8 bytes for the numeric ID
  - 16 bytes for a key

For a key of kind `  Task  ` in the default namespace with a string ID and no ancestor:

``` text
Task name:my_task_id
```

The key size is 5 + 11 + 16 = 32 bytes:

  - 5 bytes for the `  Task  ` kind name
  - 11 bytes for the `  my_task_id  ` string ID
  - 16 bytes for a key

For a `  Task  ` entity with a `  TaskList  ` ancestor in the default namespace:

``` text
TaskList id:5654313976201216 > Task id:5629499534213120
```

The ancestor uses 9 + 8 = 17 bytes:

  - 9 bytes for the `  TaskList  ` kind name
  - 8 bytes for the numeric ID

So the key size of a `  Task  ` entity with a `  TaskList  ` ancestor uses 17 + 5 + 8 + 16 = 46 bytes:

  - 17 bytes for the ancestor
  - 5 bytes for the `  Task  ` kind name
  - 8 bytes for the numeric ID
  - 16 bytes for a key

If this entity is in the `  my_name_space  ` namespace, the key size is 14 + 46 = 60 bytes, because the `  my_name_space  ` name uses 14 bytes.

## Property size

The size of a property is the sum of

  - The property name string size
  - The property value’s size

The following shows the size of property values by type.

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
<td>the sum of the sizes of its values</td>
</tr>
<tr class="even">
<td>Blob</td>
<td>byte length</td>
</tr>
<tr class="odd">
<td>Boolean</td>
<td>1 byte</td>
</tr>
<tr class="even">
<td>Double</td>
<td>8 bytes</td>
</tr>
<tr class="odd">
<td>Embedded entity</td>
<td>the <a href="#entity_size">entity size</a></td>
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
<td>Key</td>
<td>the <a href="#key_size">key size</a></td>
</tr>
<tr class="odd">
<td>Null</td>
<td>1 byte</td>
</tr>
<tr class="even">
<td>String</td>
<td>number of UTF-8 encoded bytes + 1</td>
</tr>
<tr class="odd">
<td>Timestamp</td>
<td>8 bytes</td>
</tr>
</tbody>
</table>

For example, a property named `  done  ` with a type of Boolean would use 6 bytes:

  - 5 bytes for the `  done  ` property name
  - 1 byte for the Boolean value

## Entity size

The size of an entity is the sum of

  - The [key size](#key_size)
  - The sum of the [property sizes](#property_size)
  - 32 bytes

This example is for an entity of kind `  Task  ` in the default namespace with a numeric ID and no ancestor:

``` text
Task id:5730082031140864
 - "type": "Personal"
 - "done": false
 - "priority": 1
 - "description": "Learn Google Cloud Datastore"
```

The total size of the properties is 78 bytes:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Property name and value</th>
<th>Property size in bytes</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       "type": "Personal"      </code></td>
<td>14<br />
5 for the property name + 9 for the property's string value</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       "done": false      </code></td>
<td>6<br />
5 for the property name + 1 for the property's Boolean value</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       "priority": 1      </code></td>
<td>17<br />
9 for the property name + 8 for the property's integer value</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       "description": "Learn Google Cloud Datastore"      </code></td>
<td>41<br />
12 for the property name + 29 for the property's string value</td>
</tr>
</tbody>
</table>

So the entity size is 29 + 78 + 32 = 139 bytes:

  - 29 bytes for the key
  - 78 bytes for the properties
  - 32 bytes for an entity

## Index entry size

The size of an index entry is calculated as follows for built-in and composite indexes.

### Built-in indexes

The size of a built-in index entry is the sum of:

  - The [key size](#key_size) of the indexed entity
  - The sum of the indexed property names
  - The sum of the indexed [property values](#property-value-sizes)
  - The size of the indexed entity kind name
  - 32 bytes

For example, take an entity of kind `  Task  ` in the default namespace with a numeric ID and no ancestor:

``` text
Task id:5730082031140864
 - "type": "Personal"
 - "done": false
 - "priority": 1
 - "description": "Learn Google Cloud Datastore"
```

If `  done  ` is an indexed property, the [built-in index](/datastore/docs/concepts/indexes#built_in_indexes) entry for the single property `  done  ` index consists of the key, the `  done  ` property name and value, the `  Task  ` kind name, and 32 bytes for an index entry. The total size of this index entry is 72 bytes:

  - 29 for the key
  - 6 for the `  done  ` property name and Boolean value
  - 5 for the `  Task  ` kind name
  - 32 for an index entry

By default, Datastore mode databases automatically predefine two single property indexes for each property of each entity kind, one in ascending order and one in descending order. So this entity would have an index entry of size 72 bytes in the single property `  done  ` index in ascending order and it would have an index entry of size 72 bytes in the single property `  done  ` index in descending order.

### Composite indexes

The size of a composite index entry is the sum of:

  - The [key size](#key_size) of the indexed entity
  - The sum of the indexed [property values](#property-value-sizes)
  - 32 bytes

For example, take an entity of kind `  Task  ` in the default namespace with a numeric ID and no ancestor:

``` text
indexes:
- kind: Task
  properties:
  - name: done
    direction: asc
  - name: priority
    direction: asc
```

Consider a [composite index](/datastore/docs/concepts/indexes#composite_indexes) that uses the `  done  ` and `  priority  ` properties (both ascending):

The total size of the index entry in this index is 70 bytes:

  - 29 for the key
  - 1 for the `  done  ` property Boolean value
  - 8 for the `  priority  ` property integer value
  - 32 for an index entry

If you do not want Firestore in Datastore mode to maintain an index for a property, [exclude the property from your indexes](/datastore/docs/concepts/indexes#unindexed_properties) . Note that excluding a property removes it from any composite indexes.

## What's next

  - Learn about [Datastore mode Pricing](/datastore/docs/pricing) .
  - Learn about [Datastore mode Indexes](/datastore/docs/concepts/indexes) .
