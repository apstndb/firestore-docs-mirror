# Map Functions Reference

**Preview — Firestore in Native mode (with Pipeline Operations) for Enterprise Edition**

This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](/terms/service-terms#1) . You can process personal data for this feature as outlined in the [Cloud Data Processing Addendum](/terms/data-processing-addendum) , subject to the obligations and restrictions described in the agreement under which you access Google Cloud. Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

## **Map Functions**

<table>
<tbody>
<tr class="odd">
<td>Name</td>
<td>Description</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         MAP       </code></td>
<td>Constructs a map value from a series of key-value pairs</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         MAP_GET       </code></td>
<td>Returns the value in a map given a specified key</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         MAP_SET       </code></td>
<td>Returns a copy of a map with a series of updated keys</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         MAP_REMOVE       </code></td>
<td>Returns a copy of a map with a series of keys removed</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         MAP_MERGE       </code></td>
<td>Merges a series of maps together.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         CURRENT_CONTEXT       </code></td>
<td>Returns the current context as a map.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         MAP_KEYS       </code></td>
<td>Returns an array of all keys in a map.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         MAP_VALUES       </code></td>
<td>Returns an array of all values in a map.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         MAP_ENTRIES       </code></td>
<td>Returns an array of key-value pairs of a map.</td>
</tr>
</tbody>
</table>

### MAP

**Syntax:**

``` text
map(key: STRING, value: ANY, ...) -> MAP
```

**Description:**

Constructs a map from a series of key-value pairs.

### MAP\_GET

**Syntax:**

``` text
map_get(map: ANY, key: STRING) -> ANY
```

**Description:**

Returns the value in a map given a specified key. Returns an `  ABSENT  ` value if the `  key  ` does not exist in the map, or if the `  map  ` argument is not a `  MAP  ` .

##### Node.js

``` javascript
const result = await db.pipeline()
  .collection("books")
  .select(
    field("awards").mapGet("pulitzer").as("hasPulitzerAward")
  )
  .execute();test.firestore.js
```

### Web

``` javascript
const result = await execute(db.pipeline()
  .collection("books")
  .select(
    field("awards").mapGet("pulitzer").as("hasPulitzerAward")
  )
);test.firestore.js
```

##### Swift

``` swift
let result = try await db.pipeline()
  .collection("books")
  .select([
    Field("awards").mapGet("pulitzer").as("hasPulitzerAward")
  ])
  .execute()PipelineSnippets.swift
```

##### Kotlin  
Android

``` kotlin
val result = db.pipeline()
    .collection("books")
    .select(
        field("awards").mapGet("pulitzer").alias("hasPulitzerAward")
    )
    .execute()DocSnippets.kt
```

##### Java  
Android

``` text
Task<Pipeline.Snapshot> result = db.pipeline()
    .collection("books")
    .select(
        field("awards").mapGet("pulitzer").alias("hasPulitzerAward")
    )
    .execute();DocSnippets.java
```

##### Python

``` python
from google.cloud.firestore_v1.pipeline_expressions import Field

result = (
    client.pipeline()
    .collection("books")
    .select(Field.of("awards").map_get("pulitzer").as_("hasPulitzerAward"))
    .execute()
)firestore_pipelines.py
```

##### Java

``` java
Pipeline.Snapshot result =
    firestore
        .pipeline()
        .collection("books")
        .select(mapGet(field("awards"), "pulitzer").as("hasPulitzerAward"))
        .execute()
        .get();PipelineSnippets.java
```

### MAP\_SET

**Syntax:**

``` text
map_set(map: MAP, key: STRING, value: ANY, ...) -> MAP
```

**Description:**

Returns a copy of the `  map  ` value with its contents updated by a series of key-value pairs.

If the given resolves to an absent value, the associated key is removed from the map.

If the `  map  ` argument is not a `  MAP  ` , returns an absent value.

### MAP\_REMOVE

**Syntax:**

``` text
map_remove(map: MAP, key: STRING...) -> MAP
```

**Description:**

Returns a copy of the `  map  ` value with a series of keys removed.

### MAP\_MERGE

**Syntax:**

``` text
map_merge(maps: MAP...) -> MAP
```

Merges the contents of 2 or more maps. If multiple maps have conflicting values, the last value is used.

### CURRENT\_CONTEXT

**Syntax:**

``` text
current_context() -> MAP
```

Returns a map consisting of all available fields in the current point of execution.

### MAP\_KEYS

**Syntax:**

``` text
map_keys(map: MAP) -> ARRAY<STRING>
```

**Description:**

Returns an array containing all keys of the `  map  ` value.

### MAP\_VALUES

**Syntax:**

``` text
map_values(map: MAP) -> ARRAY<ANY>
```

**Description:**

Returns an array containing all values of the `  map  ` value.

### MAP\_ENTRIES

**Syntax:**

``` text
map_entries(map: MAP) -> ARRAY<MAP>
```

**Description:**

Returns an array containing all key-value pairs in the `  map  ` value.

Each key-value pair will be in the form of a map with two entries, `  k  ` and `  v  ` .

**Examples:**

<table>
<thead>
<tr class="header">
<th style="text-align: left;"><code dir="ltr" translate="no">       map      </code></th>
<th style="text-align: left;"><code dir="ltr" translate="no">       map_entries(map)      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">{}</td>
<td style="text-align: left;">[]</td>
</tr>
<tr class="even">
<td style="text-align: left;">{"foo" : 2L}</td>
<td style="text-align: left;">[{"k": "foo", "v" : 2L}]</td>
</tr>
<tr class="odd">
<td style="text-align: left;">{"foo" : "bar", "bar" : "foo"}</td>
<td style="text-align: left;">[{"k": "foo", "v" : "bar" }, {"k" : "bar", "v": "foo"}]</td>
</tr>
</tbody>
</table>

## What's next

  - See the [Pipeline Queries overview](/firestore/docs/pipeline/overview)
