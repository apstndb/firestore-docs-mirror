# Array Functions Reference

**Preview — Firestore in Native mode (with Pipeline Operations) for Enterprise Edition**

This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](/terms/service-terms#1) . You can process personal data for this feature as outlined in the [Cloud Data Processing Addendum](/terms/data-processing-addendum) , subject to the obligations and restrictions described in the agreement under which you access Google Cloud. Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

## **Array Functions**

<table>
<tbody>
<tr class="odd">
<td>Name</td>
<td>Description</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         ARRAY       </code></td>
<td>Returns an <code dir="ltr" translate="no">       ARRAY      </code> containing one element for each input argument</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         ARRAY_CONCAT       </code></td>
<td>Concatenates multiple arrays into a single <code dir="ltr" translate="no">       ARRAY      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         ARRAY_CONTAINS       </code></td>
<td>Returns <code dir="ltr" translate="no">       TRUE      </code> if a given <code dir="ltr" translate="no">       ARRAY      </code> contains a particular value</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         ARRAY_CONTAINS_ALL       </code></td>
<td>Returns <code dir="ltr" translate="no">       TRUE      </code> if all values are present in the <code dir="ltr" translate="no">       ARRAY      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         ARRAY_CONTAINS_ANY       </code></td>
<td>Returns <code dir="ltr" translate="no">       TRUE      </code> if any of the values are present in the <code dir="ltr" translate="no">       ARRAY      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         ARRAY_FILTER       </code></td>
<td>Filters out elements from an <code dir="ltr" translate="no">       ARRAY      </code> that don't satisfy a predicate</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         ARRAY_FIRST       </code></td>
<td>Returns the first element in an <code dir="ltr" translate="no">       ARRAY      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         ARRAY_FIRST_N       </code></td>
<td>Returns the first <code dir="ltr" translate="no">       n      </code> elements in an <code dir="ltr" translate="no">       ARRAY      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         ARRAY_GET       </code></td>
<td>Returns the element at a given index in an <code dir="ltr" translate="no">       ARRAY      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         ARRAY_INDEX_OF       </code></td>
<td>Returns the index of the first occurrence of a value in an <code dir="ltr" translate="no">       ARRAY      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         ARRAY_INDEX_OF_ALL       </code></td>
<td>Returns all indexes of a value in an <code dir="ltr" translate="no">       ARRAY      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         ARRAY_LENGTH       </code></td>
<td>Returns the number of elements in an <code dir="ltr" translate="no">       ARRAY      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         ARRAY_LAST       </code></td>
<td>Returns the last element in an <code dir="ltr" translate="no">       ARRAY      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         ARRAY_LAST_N       </code></td>
<td>Returns the last <code dir="ltr" translate="no">       n      </code> elements in an <code dir="ltr" translate="no">       ARRAY      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         ARRAY_REVERSE       </code></td>
<td>Reverses the order of elements in an <code dir="ltr" translate="no">       ARRAY      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         ARRAY_SLICE       </code></td>
<td>Returns a slice of an <code dir="ltr" translate="no">       ARRAY      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         ARRAY_TRANSFORM       </code></td>
<td>Transforms elements in an <code dir="ltr" translate="no">       ARRAY      </code> by applying expression to each element</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         MAXIMUM       </code></td>
<td>Returns the maximum value in an <code dir="ltr" translate="no">       ARRAY      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         MAXIMUM_N       </code></td>
<td>Returns the <code dir="ltr" translate="no">       n      </code> largest values in an <code dir="ltr" translate="no">       ARRAY      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         MINIMUM       </code></td>
<td>Returns the minimum value in an <code dir="ltr" translate="no">       ARRAY      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         MINIMUM_N       </code></td>
<td>Returns the <code dir="ltr" translate="no">       n      </code> smallest values in an <code dir="ltr" translate="no">       ARRAY      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         SUM       </code></td>
<td>Returns the sum of all <code dir="ltr" translate="no">       NUMERIC      </code> values in an <code dir="ltr" translate="no">       ARRAY      </code> .</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         JOIN       </code></td>
<td>Produces a concatenation of the elements in an <code dir="ltr" translate="no">       ARRAY      </code> as a <code dir="ltr" translate="no">       STRING      </code> value.</td>
</tr>
</tbody>
</table>

### ARRAY

**Syntax:**

``` text
array(values: ANY...) -> ARRAY
```

**Description:**

Constructs an array from the given elements.

  - If an argument does not exist, it is replaced with `  NULL  ` in the resulting array.

**Examples:**

<table>
<thead>
<tr class="header">
<th style="text-align: left;">values</th>
<th style="text-align: left;"><code dir="ltr" translate="no">       array(values)      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">()</td>
<td style="text-align: left;">[]</td>
</tr>
<tr class="even">
<td style="text-align: left;">(1, 2, 3)</td>
<td style="text-align: left;">[1, 2, 3]</td>
</tr>
<tr class="odd">
<td style="text-align: left;">("a", 1, true)</td>
<td style="text-align: left;">["a", 1, true]</td>
</tr>
<tr class="even">
<td style="text-align: left;">(1, null)</td>
<td style="text-align: left;">[1, null]</td>
</tr>
<tr class="odd">
<td style="text-align: left;">(1, [2, 3])</td>
<td style="text-align: left;">[1, [2, 3]]</td>
</tr>
</tbody>
</table>

### ARRAY\_CONCAT

**Syntax:**

``` text
array_concat(arrays: ARRAY...) -> ARRAY
```

**Description:**

Concatenates two or more arrays into a single `  ARRAY  ` .

**Examples:**

<table>
<thead>
<tr class="header">
<th style="text-align: left;">arrays</th>
<th style="text-align: left;"><code dir="ltr" translate="no">       array_concat(arrays)      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">([1, 2], [3, 4])</td>
<td style="text-align: left;">[1, 2, 3, 4]</td>
</tr>
<tr class="even">
<td style="text-align: left;">(["a", "b"], ["c"])</td>
<td style="text-align: left;">["a", "b", "c"]</td>
</tr>
<tr class="odd">
<td style="text-align: left;">([1], [2], [3])</td>
<td style="text-align: left;">[1, 2, 3]</td>
</tr>
<tr class="even">
<td style="text-align: left;">([], [1, 2])</td>
<td style="text-align: left;">[1, 2]</td>
</tr>
</tbody>
</table>

##### Node.js

``` javascript
const result = await db.pipeline()
  .collection("books")
  .select(field("genre").arrayConcat([field("subGenre")]).as("allGenres"))
  .execute();test.firestore.js
```

##### Swift

``` swift
let result = try await db.pipeline()
  .collection("books")
  .select([Field("genre").arrayConcat([Field("subGenre")]).as("allGenres")])
  .execute()PipelineSnippets.swift
```

##### Kotlin  
Android

``` kotlin
val result = db.pipeline()
    .collection("books")
    .select(field("genre").arrayConcat(field("subGenre")).alias("allGenres"))
    .execute()DocSnippets.kt
```

##### Java  
Android

``` text
Task<Pipeline.Snapshot> result = db.pipeline()
    .collection("books")
    .select(field("genre").arrayConcat(field("subGenre")).alias("allGenres"))
    .execute();DocSnippets.java
    
```

##### Python

``` python
from google.cloud.firestore_v1.pipeline_expressions import Field

result = (
    client.pipeline()
    .collection("books")
    .select(Field.of("genre").array_concat(Field.of("subGenre")).as_("allGenres"))
    .execute()
)firestore_pipelines.py
```

##### Java

``` java
Pipeline.Snapshot result =
    firestore
        .pipeline()
        .collection("books")
        .select(arrayConcat(field("genre"), field("subGenre")).as("allGenres"))
        .execute()
        .get();PipelineSnippets.java
```

### ARRAY\_CONTAINS

**Syntax:**

``` text
array_contains(array: ARRAY, value: ANY) -> BOOLEAN
```

**Description:**

Returns `  TRUE  ` if `  value  ` is found in the `  array  ` , and `  FALSE  ` otherwise.

**Examples:**

<table>
<thead>
<tr class="header">
<th style="text-align: left;">array</th>
<th style="text-align: left;">value</th>
<th style="text-align: left;"><code dir="ltr" translate="no">       array_contains(array, value)      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">[1, 2, 3]</td>
<td style="text-align: left;">2</td>
<td style="text-align: left;">true</td>
</tr>
<tr class="even">
<td style="text-align: left;">[[1, 2], [3]]</td>
<td style="text-align: left;">[1, 2]</td>
<td style="text-align: left;">true</td>
</tr>
<tr class="odd">
<td style="text-align: left;">[1, null]</td>
<td style="text-align: left;">null</td>
<td style="text-align: left;">true</td>
</tr>
<tr class="even">
<td style="text-align: left;">"abc"</td>
<td style="text-align: left;">ANY</td>
<td style="text-align: left;">error</td>
</tr>
</tbody>
</table>

##### Node.js

``` javascript
const result = await db.pipeline()
  .collection("books")
  .select(field("genre").arrayContains(constant("mystery")).as("isMystery"))
  .execute();test.firestore.js
```

### Web

``` javascript
const result = await execute(db.pipeline()
  .collection("books")
  .select(field("genre").arrayContains(constant("mystery")).as("isMystery"))
);test.firestore.js
```

##### Swift

``` swift
let result = try await db.pipeline()
  .collection("books")
  .select([Field("genre").arrayContains(Constant("mystery")).as("isMystery")])
  .execute()PipelineSnippets.swift
```

##### Kotlin  
Android

``` kotlin
val result = db.pipeline()
    .collection("books")
    .select(field("genre").arrayContains("mystery").alias("isMystery"))
    .execute()DocSnippets.kt
```

##### Java  
Android

``` text
Task<Pipeline.Snapshot> result = db.pipeline()
    .collection("books")
    .select(field("genre").arrayContains("mystery").alias("isMystery"))
    .execute();DocSnippets.java
    
```

##### Python

``` python
from google.cloud.firestore_v1.pipeline_expressions import Field

result = (
    client.pipeline()
    .collection("books")
    .select(Field.of("genre").array_contains("mystery").as_("isMystery"))
    .execute()
)firestore_pipelines.py
```

##### Java

``` java
Pipeline.Snapshot result =
    firestore
        .pipeline()
        .collection("books")
        .select(arrayContains(field("genre"), "mystery").as("isMystery"))
        .execute()
        .get();PipelineSnippets.java
```

### ARRAY\_CONTAINS\_ALL

**Syntax:**

``` text
array_contains_all(array: ARRAY, search_values: ARRAY) -> BOOLEAN
```

**Description:**

Returns `  TRUE  ` if all `  search_values  ` are found in the `  array  ` , and `  FALSE  ` otherwise.

**Examples:**

<table>
<thead>
<tr class="header">
<th style="text-align: left;">array</th>
<th style="text-align: left;">search_values</th>
<th style="text-align: left;"><code dir="ltr" translate="no">       array_contains_all(array, search_values)      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">[1, 2, 3]</td>
<td style="text-align: left;">[1, 2]</td>
<td style="text-align: left;">true</td>
</tr>
<tr class="even">
<td style="text-align: left;">[1, 2, 3]</td>
<td style="text-align: left;">[1, 4]</td>
<td style="text-align: left;">false</td>
</tr>
<tr class="odd">
<td style="text-align: left;">[1, null]</td>
<td style="text-align: left;">[null]</td>
<td style="text-align: left;">true</td>
</tr>
<tr class="even">
<td style="text-align: left;">[NaN]</td>
<td style="text-align: left;">[NaN]</td>
<td style="text-align: left;">true</td>
</tr>
<tr class="odd">
<td style="text-align: left;">[]</td>
<td style="text-align: left;">[]</td>
<td style="text-align: left;">true</td>
</tr>
<tr class="even">
<td style="text-align: left;">[1, 2, 3]</td>
<td style="text-align: left;">[]</td>
<td style="text-align: left;">true</td>
</tr>
</tbody>
</table>

##### Node.js

``` javascript
const result = await db.pipeline()
  .collection("books")
  .select(
    field("genre")
      .arrayContainsAll([constant("fantasy"), constant("adventure")])
      .as("isFantasyAdventure")
  )
  .execute();test.firestore.js
```

### Web

``` javascript
const result = await execute(db.pipeline()
  .collection("books")
  .select(
    field("genre")
      .arrayContainsAll([constant("fantasy"), constant("adventure")])
      .as("isFantasyAdventure")
  )
);test.firestore.js
```

##### Swift

``` swift
let result = try await db.pipeline()
  .collection("books")
  .select([
    Field("genre")
      .arrayContainsAll([Constant("fantasy"), Constant("adventure")])
      .as("isFantasyAdventure")
  ])
  .execute()PipelineSnippets.swift
```

##### Kotlin  
Android

``` kotlin
val result = db.pipeline()
    .collection("books")
    .select(
        field("genre")
            .arrayContainsAll(listOf("fantasy", "adventure"))
            .alias("isFantasyAdventure")
    )
    .execute()DocSnippets.kt
```

##### Java  
Android

``` text
Task<Pipeline.Snapshot> result = db.pipeline()
    .collection("books")
    .select(
        field("genre")
            .arrayContainsAll(Arrays.asList("fantasy", "adventure"))
            .alias("isFantasyAdventure")
    )
    .execute();DocSnippets.java
    
```

##### Python

``` python
from google.cloud.firestore_v1.pipeline_expressions import Field

result = (
    client.pipeline()
    .collection("books")
    .select(
        Field.of("genre")
        .array_contains_all(["fantasy", "adventure"])
        .as_("isFantasyAdventure")
    )
    .execute()
)firestore_pipelines.py
```

##### Java

``` java
Pipeline.Snapshot result =
    firestore
        .pipeline()
        .collection("books")
        .select(
            arrayContainsAll(field("genre"), Arrays.asList("fantasy", "adventure"))
                .as("isFantasyAdventure"))
        .execute()
        .get();PipelineSnippets.java
```

### ARRAY\_CONTAINS\_ANY

**Syntax:**

``` text
array_contains_any(array: ARRAY, search_values: ARRAY) -> BOOLEAN
```

**Description:**

Returns `  TRUE  ` if any of the `  search_values  ` are found in the `  array  ` , and `  FALSE  ` otherwise.

**Examples:**

<table>
<thead>
<tr class="header">
<th style="text-align: left;">array</th>
<th style="text-align: left;">search_values</th>
<th style="text-align: left;"><code dir="ltr" translate="no">       array_contains_any(array, search_values)      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">[1, 2, 3]</td>
<td style="text-align: left;">[4, 1]</td>
<td style="text-align: left;">true</td>
</tr>
<tr class="even">
<td style="text-align: left;">[1, 2, 3]</td>
<td style="text-align: left;">[4, 5]</td>
<td style="text-align: left;">false</td>
</tr>
<tr class="odd">
<td style="text-align: left;">[1, 2, null]</td>
<td style="text-align: left;">[null]</td>
<td style="text-align: left;">true</td>
</tr>
</tbody>
</table>

##### Node.js

``` javascript
const result = await db.pipeline()
  .collection("books")
  .select(
    field("genre")
      .arrayContainsAny([constant("fantasy"), constant("nonfiction")])
      .as("isMysteryOrFantasy")
  )
  .execute();test.firestore.js
```

### Web

``` javascript
const result = await execute(db.pipeline()
  .collection("books")
  .select(
    field("genre")
      .arrayContainsAny([constant("fantasy"), constant("nonfiction")])
      .as("isMysteryOrFantasy")
  )
);test.firestore.js
```

##### Swift

``` swift
let result = try await db.pipeline()
  .collection("books")
  .select([
    Field("genre")
      .arrayContainsAny([Constant("fantasy"), Constant("nonfiction")])
      .as("isMysteryOrFantasy")
  ])
  .execute()PipelineSnippets.swift
```

##### Kotlin  
Android

``` kotlin
val result = db.pipeline()
    .collection("books")
    .select(
        field("genre")
            .arrayContainsAny(listOf("fantasy", "nonfiction"))
            .alias("isMysteryOrFantasy")
    )
    .execute()DocSnippets.kt
```

##### Java  
Android

``` text
Task<Pipeline.Snapshot> result = db.pipeline()
    .collection("books")
    .select(
        field("genre")
            .arrayContainsAny(Arrays.asList("fantasy", "nonfiction"))
            .alias("isMysteryOrFantasy")
    )
    .execute();DocSnippets.java
    
```

##### Python

``` python
from google.cloud.firestore_v1.pipeline_expressions import Field

result = (
    client.pipeline()
    .collection("books")
    .select(
        Field.of("genre")
        .array_contains_any(["fantasy", "nonfiction"])
        .as_("isMysteryOrFantasy")
    )
    .execute()
)firestore_pipelines.py
```

##### Java

``` java
Pipeline.Snapshot result =
    firestore
        .pipeline()
        .collection("books")
        .select(
            arrayContainsAny(field("genre"), Arrays.asList("fantasy", "nonfiction"))
                .as("isMysteryOrFantasy"))
        .execute()
        .get();PipelineSnippets.java
```

### ARRAY\_FILTER

**Syntax:**

``` text
array_filter(array: ARRAY, predicate: (ANY) -> BOOLEAN) -> ARRAY
```

**Description:**

Filters `  array  ` using a `  predicate  ` expression, returning a new array with only elements that satisfy the predicate.

  - For each element in `  array  ` , `  predicate  ` is evaluated. If it returns `  true  ` , the element is included in the result; otherwise (if it returns `  false  ` or `  null  ` ), it is omitted.
  - If `  predicate  ` evaluates to a non-boolean or non-null value, the function returns an error.

**Examples:**

<table>
<thead>
<tr class="header">
<th style="text-align: left;">array</th>
<th style="text-align: left;">predicate</th>
<th style="text-align: left;"><code dir="ltr" translate="no">       array_filter(array, predicate)      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">[1, 2, 3]</td>
<td style="text-align: left;">x -&gt; x &gt; 1</td>
<td style="text-align: left;">[2, 3]</td>
</tr>
<tr class="even">
<td style="text-align: left;">[1, null, 3]</td>
<td style="text-align: left;">x -&gt; x &gt; 1</td>
<td style="text-align: left;">[3]</td>
</tr>
<tr class="odd">
<td style="text-align: left;">["a", "b", "c"]</td>
<td style="text-align: left;">x -&gt; x != "b"</td>
<td style="text-align: left;">["a", "c"]</td>
</tr>
<tr class="even">
<td style="text-align: left;">[]</td>
<td style="text-align: left;">x -&gt; true</td>
<td style="text-align: left;">[]</td>
</tr>
</tbody>
</table>

### ARRAY\_GET

**Syntax:**

``` text
array_get(array: ARRAY, index: INT64) -> ANY
```

**Description:**

Returns the element at the 0-based `  index  ` in `  array  ` .

  - If `  index  ` is negative, elements are accessed from the end of array, where `  -1  ` is the last element.
  - If `  array  ` is not of type `  ARRAY  ` and not `  null  ` , returns an error.
  - If `  index  ` is out of bounds, the function returns an absent value.
  - If `  index  ` is not of type `  INT64  ` , the function returns an error.

**Examples:**

<table>
<thead>
<tr class="header">
<th style="text-align: left;">array</th>
<th style="text-align: left;">index</th>
<th style="text-align: left;"><code dir="ltr" translate="no">       array_get(array, index)      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">[1, 2, 3]</td>
<td style="text-align: left;">0</td>
<td style="text-align: left;">1</td>
</tr>
<tr class="even">
<td style="text-align: left;">[1, 2, 3]</td>
<td style="text-align: left;">-1</td>
<td style="text-align: left;">3</td>
</tr>
<tr class="odd">
<td style="text-align: left;">[1, 2, 3]</td>
<td style="text-align: left;">3</td>
<td style="text-align: left;">absent</td>
</tr>
<tr class="even">
<td style="text-align: left;">[1, 2, 3]</td>
<td style="text-align: left;">-4</td>
<td style="text-align: left;">absent</td>
</tr>
<tr class="odd">
<td style="text-align: left;">"abc"</td>
<td style="text-align: left;">0</td>
<td style="text-align: left;">error</td>
</tr>
<tr class="even">
<td style="text-align: left;">null</td>
<td style="text-align: left;">0</td>
<td style="text-align: left;">null</td>
</tr>
<tr class="odd">
<td style="text-align: left;"><code dir="ltr" translate="no">       Array      </code></td>
<td style="text-align: left;">"a"</td>
<td style="text-align: left;">error</td>
</tr>
<tr class="even">
<td style="text-align: left;"><code dir="ltr" translate="no">       Array      </code></td>
<td style="text-align: left;">2.0</td>
<td style="text-align: left;">error</td>
</tr>
</tbody>
</table>

### ARRAY\_LENGTH

**Syntax:**

``` text
array_length(array: ARRAY) -> INT64
```

**Description:**

Returns the number of elements in `  array  ` .

**Examples:**

<table>
<thead>
<tr class="header">
<th style="text-align: left;">array</th>
<th style="text-align: left;"><code dir="ltr" translate="no">       array_length(array)      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">[1, 2, 3]</td>
<td style="text-align: left;">3</td>
</tr>
<tr class="even">
<td style="text-align: left;">[]</td>
<td style="text-align: left;">0</td>
</tr>
<tr class="odd">
<td style="text-align: left;">[1, 1, 1]</td>
<td style="text-align: left;">3</td>
</tr>
<tr class="even">
<td style="text-align: left;">[1, null]</td>
<td style="text-align: left;">2</td>
</tr>
</tbody>
</table>

##### Node.js

``` javascript
const result = await db.pipeline()
  .collection("books")
  .select(field("genre").arrayLength().as("genreCount"))
  .execute();test.firestore.js
```

### Web

``` javascript
const result = await execute(db.pipeline()
  .collection("books")
  .select(field("genre").arrayLength().as("genreCount"))
);test.firestore.js
```

##### Swift

``` swift
let result = try await db.pipeline()
  .collection("books")
  .select([Field("genre").arrayLength().as("genreCount")])
  .execute()PipelineSnippets.swift
```

##### Kotlin  
Android

``` kotlin
val result = db.pipeline()
    .collection("books")
    .select(field("genre").arrayLength().alias("genreCount"))
    .execute()DocSnippets.kt
```

##### Java  
Android

``` text
Task<Pipeline.Snapshot> result = db.pipeline()
    .collection("books")
    .select(field("genre").arrayLength().alias("genreCount"))
    .execute();DocSnippets.java
    
```

##### Python

``` python
from google.cloud.firestore_v1.pipeline_expressions import Field

result = (
    client.pipeline()
    .collection("books")
    .select(Field.of("genre").array_length().as_("genreCount"))
    .execute()
)firestore_pipelines.py
```

##### Java

``` java
Pipeline.Snapshot result =
    firestore
        .pipeline()
        .collection("books")
        .select(arrayLength(field("genre")).as("genreCount"))
        .execute()
        .get();PipelineSnippets.java
```

### ARRAY\_REVERSE

**Syntax:**

``` text
array_reverse(array: ARRAY) -> ARRAY
```

**Description:**

Reverses the given `  array  ` .

**Examples:**

<table>
<thead>
<tr class="header">
<th style="text-align: left;">array</th>
<th style="text-align: left;"><code dir="ltr" translate="no">       array_reverse(array)      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">[1, 2, 3]</td>
<td style="text-align: left;">[3, 2, 1]</td>
</tr>
<tr class="even">
<td style="text-align: left;">["a", "b"]</td>
<td style="text-align: left;">["b", "a"]</td>
</tr>
<tr class="odd">
<td style="text-align: left;">[1, 2, 2, 3]</td>
<td style="text-align: left;">[3, 2, 2, 1]</td>
</tr>
</tbody>
</table>

##### Node.js

``` javascript
const result = await db.pipeline()
  .collection("books")
  .select(arrayReverse(field("genre")).as("reversedGenres"))
  .execute();test.firestore.js
```

### Web

``` javascript
const result = await execute(db.pipeline()
  .collection("books")
  .select(field("genre").arrayReverse().as("reversedGenres"))
);test.firestore.js
```

##### Swift

``` swift
let result = try await db.pipeline()
  .collection("books")
  .select([Field("genre").arrayReverse().as("reversedGenres")])
  .execute()PipelineSnippets.swift
```

##### Kotlin  
Android

``` kotlin
val result = db.pipeline()
    .collection("books")
    .select(field("genre").arrayReverse().alias("reversedGenres"))
    .execute()DocSnippets.kt
```

``` text
    Java
Android
Task<Pipeline.Snapshot> result = db.pipeline()
    .collection("books")
    .select(field("genre").arrayReverse().alias("reversedGenres"))
    .execute();DocSnippets.java
  
```

##### Python

``` python
from google.cloud.firestore_v1.pipeline_expressions import Field

result = (
    client.pipeline()
    .collection("books")
    .select(Field.of("genre").array_reverse().as_("reversedGenres"))
    .execute()
)firestore_pipelines.py
```

##### Java

``` java
Pipeline.Snapshot result =
    firestore
        .pipeline()
        .collection("books")
        .select(arrayReverse(field("genre")).as("reversedGenres"))
        .execute()
        .get();PipelineSnippets.java
```

### ARRAY\_FIRST

**Syntax:**

``` text
array_first(array: ARRAY) -> ANY
```

**Description:**

Returns the first element in `  array  ` . This is equivalent to `  array_get(array, 0)  ` .

  - If `  array  ` is empty, returns an absent value.

**Examples:**

<table>
<thead>
<tr class="header">
<th style="text-align: left;">array</th>
<th style="text-align: left;"><code dir="ltr" translate="no">       array_first(array)      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">[1, 2, 3]</td>
<td style="text-align: left;">1</td>
</tr>
<tr class="even">
<td style="text-align: left;">[]</td>
<td style="text-align: left;">absent</td>
</tr>
</tbody>
</table>

### ARRAY\_FIRST\_N

**Syntax:**

``` text
array_first_n(array: ARRAY, n: INT64) -> ARRAY
```

**Description:**

Returns the first `  n  ` elements of `  array  ` . This is equivalent to `  array_slice(array, 0, n)  ` .

  - If `  n  ` is negative, returns an error.

**Examples:**

<table>
<thead>
<tr class="header">
<th style="text-align: left;">array</th>
<th style="text-align: left;">n</th>
<th style="text-align: left;"><code dir="ltr" translate="no">       array_first_n(array, n)      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">[1, 2, 3, 4, 5]</td>
<td style="text-align: left;">3</td>
<td style="text-align: left;">[1, 2, 3]</td>
</tr>
<tr class="even">
<td style="text-align: left;">[1, 2]</td>
<td style="text-align: left;">3</td>
<td style="text-align: left;">[1, 2]</td>
</tr>
<tr class="odd">
<td style="text-align: left;">[1, 2, 3]</td>
<td style="text-align: left;">0</td>
<td style="text-align: left;">[]</td>
</tr>
</tbody>
</table>

### ARRAY\_INDEX\_OF

**Syntax:**

``` text
array_index_of(array: ARRAY, value: ANY) -> INT64
```

**Description:**

Returns the 0-based index of the first occurrence of `  value  ` in `  array  ` . Returns -1 if `  value  ` is not found.

**Examples:**

<table>
<thead>
<tr class="header">
<th style="text-align: left;">array</th>
<th style="text-align: left;">value</th>
<th style="text-align: left;"><code dir="ltr" translate="no">       array_index_of(array, value)      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">[1, 2, 3, 2]</td>
<td style="text-align: left;">2</td>
<td style="text-align: left;">1</td>
</tr>
<tr class="even">
<td style="text-align: left;">[1, 2, 3]</td>
<td style="text-align: left;">4</td>
<td style="text-align: left;">-1</td>
</tr>
<tr class="odd">
<td style="text-align: left;">[1, null, 3]</td>
<td style="text-align: left;">null</td>
<td style="text-align: left;">1</td>
</tr>
</tbody>
</table>

### ARRAY\_INDEX\_OF\_ALL

**Syntax:**

``` text
array_index_of_all(array: ARRAY, value: ANY) -> ARRAY<INT64>
```

**Description:**

Returns an array containing the 0-based indexes of all occurrences of `  value  ` in `  array  ` . Returns `  []  ` if `  value  ` is not found.

**Examples:**

<table>
<thead>
<tr class="header">
<th style="text-align: left;">array</th>
<th style="text-align: left;">value</th>
<th style="text-align: left;"><code dir="ltr" translate="no">       array_index_of_all(array, value)      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">[1, 2, 3, 2]</td>
<td style="text-align: left;">2</td>
<td style="text-align: left;">[1, 3]</td>
</tr>
<tr class="even">
<td style="text-align: left;">[1, 2, 3]</td>
<td style="text-align: left;">4</td>
<td style="text-align: left;">[]</td>
</tr>
<tr class="odd">
<td style="text-align: left;">[1, null, 3, null]</td>
<td style="text-align: left;">null</td>
<td style="text-align: left;">[1, 3]</td>
</tr>
</tbody>
</table>

### ARRAY\_LAST

**Syntax:**

``` text
array_last(array: ARRAY) -> ANY
```

**Description:**

Returns the last element in `  array  ` . This is equivalent to `  array_get(array, -1)  ` .

  - If `  array  ` is empty, returns an absent value.

**Examples:**

<table>
<thead>
<tr class="header">
<th style="text-align: left;">array</th>
<th style="text-align: left;"><code dir="ltr" translate="no">       array_last(array)      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">[1, 2, 3]</td>
<td style="text-align: left;">3</td>
</tr>
<tr class="even">
<td style="text-align: left;">[]</td>
<td style="text-align: left;">absent</td>
</tr>
</tbody>
</table>

### ARRAY\_LAST\_N

**Syntax:**

``` text
array_last_n(array: ARRAY, n: INT64) -> ARRAY
```

**Description:**

Returns the last `  n  ` elements of `  array  ` .

  - If `  n  ` is negative, returns an error.

**Examples:**

<table>
<thead>
<tr class="header">
<th style="text-align: left;">array</th>
<th style="text-align: left;">n</th>
<th style="text-align: left;"><code dir="ltr" translate="no">       array_last_n(array, n)      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">[1, 2, 3, 4, 5]</td>
<td style="text-align: left;">3</td>
<td style="text-align: left;">[3, 4, 5]</td>
</tr>
<tr class="even">
<td style="text-align: left;">[1, 2]</td>
<td style="text-align: left;">3</td>
<td style="text-align: left;">[1, 2]</td>
</tr>
<tr class="odd">
<td style="text-align: left;">[1, 2, 3]</td>
<td style="text-align: left;">0</td>
<td style="text-align: left;">[]</td>
</tr>
</tbody>
</table>

### ARRAY\_SLICE

**Syntax:**

``` text
array_slice(array: ARRAY, offset: INT64, length: INT64) -> ARRAY
```

**Description:**

Returns a subset of `  array  ` starting from 0-based index `  offset  ` , and including `  length  ` elements.

  - If `  offset  ` is negative, it indicates the start position from the end of the array, with `  -1  ` being the last element.
  - If `  length  ` is greater than the number of elements remaining in the array after `  offset  ` , the result extends to the end of the array.
  - `  length  ` must be non-negative, otherwise returns an error.

**Examples:**

<table>
<thead>
<tr class="header">
<th style="text-align: left;">array</th>
<th style="text-align: left;">offset</th>
<th style="text-align: left;">length</th>
<th style="text-align: left;"><code dir="ltr" translate="no">       array_slice(array, offset, length)      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">[1, 2, 3, 4, 5]</td>
<td style="text-align: left;">1</td>
<td style="text-align: left;">3</td>
<td style="text-align: left;">[2, 3, 4]</td>
</tr>
<tr class="even">
<td style="text-align: left;">[1, 2, 3, 4, 5]</td>
<td style="text-align: left;">-2</td>
<td style="text-align: left;">2</td>
<td style="text-align: left;">[4, 5]</td>
</tr>
<tr class="odd">
<td style="text-align: left;">[1, 2, 3]</td>
<td style="text-align: left;">1</td>
<td style="text-align: left;">5</td>
<td style="text-align: left;">[2, 3]</td>
</tr>
<tr class="even">
<td style="text-align: left;">[1, 2, 3]</td>
<td style="text-align: left;">3</td>
<td style="text-align: left;">2</td>
<td style="text-align: left;">[]</td>
</tr>
</tbody>
</table>

### ARRAY\_TRANSFORM

**Syntax:**

``` text
array_transform(array: ARRAY, expression: (ANY) -> ANY) -> ARRAY
array_transform(array: ARRAY, expression: (ANY, INT64) -> ANY) -> ARRAY
```

**Description:**

Transforms `  array  ` by applying `  expression  ` to each element, returning a new array with transformed elements. The output array will always have same size as input array.

  - `  expression  ` can be a unary function `  element -> result  ` , or a binary function `  (element, index) -> result  ` .
  - If `  expression  ` is unary, it is called with each element of `  array  ` .
  - If `  expression  ` is binary, it is called with each element of `  array  ` and its corresponding 0-based index.

**Examples:**

<table>
<thead>
<tr class="header">
<th style="text-align: left;">array</th>
<th style="text-align: left;">expression</th>
<th style="text-align: left;"><code dir="ltr" translate="no">       array_transform(array, expression)      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">[1, 2, 3]</td>
<td style="text-align: left;">x -&gt; x * 2</td>
<td style="text-align: left;">[2, 4, 6]</td>
</tr>
<tr class="even">
<td style="text-align: left;">[1, 2, 3]</td>
<td style="text-align: left;">x -&gt; x + 1</td>
<td style="text-align: left;">[2, 3, 4]</td>
</tr>
<tr class="odd">
<td style="text-align: left;">[10, 20]</td>
<td style="text-align: left;">(x, i) -&gt; x + i</td>
<td style="text-align: left;">[10, 21]</td>
</tr>
<tr class="even">
<td style="text-align: left;">[]</td>
<td style="text-align: left;">x -&gt; 1</td>
<td style="text-align: left;">[]</td>
</tr>
</tbody>
</table>

### MAXIMUM

**Syntax:**

``` text
maximum(array: ARRAY) -> ANY
```

**Description:**

Returns the maximum value in `  array  ` .

  - `  NULL  ` values are ignored during comparison.
  - If `  array  ` is empty or only contains `  NULL  ` values, returns `  NULL  ` .

**Examples:**

<table>
<thead>
<tr class="header">
<th style="text-align: left;">array</th>
<th style="text-align: left;"><code dir="ltr" translate="no">       maximum(array)      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">[1, 5, 2]</td>
<td style="text-align: left;">5</td>
</tr>
<tr class="even">
<td style="text-align: left;">[1, null, 5]</td>
<td style="text-align: left;">5</td>
</tr>
<tr class="odd">
<td style="text-align: left;">["a", "c", "b"]</td>
<td style="text-align: left;">"c"</td>
</tr>
<tr class="even">
<td style="text-align: left;">[null, null]</td>
<td style="text-align: left;">null</td>
</tr>
<tr class="odd">
<td style="text-align: left;">[]</td>
<td style="text-align: left;">null</td>
</tr>
</tbody>
</table>

### MAXIMUM\_N

**Syntax:**

``` text
maximum_n(array: ARRAY, n: INT64) -> ARRAY
```

**Description:**

Returns an array of the `  n  ` largest values in `  array  ` in descending order.

  - `  NULL  ` values are ignored.
  - If `  n  ` is negative, returns an error.

**Examples:**

<table>
<thead>
<tr class="header">
<th style="text-align: left;">array</th>
<th style="text-align: left;">n</th>
<th style="text-align: left;"><code dir="ltr" translate="no">       maximum_n(array, n)      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">[1, 5, 2, 4, 3]</td>
<td style="text-align: left;">3</td>
<td style="text-align: left;">[5, 4, 3]</td>
</tr>
<tr class="even">
<td style="text-align: left;">[1, null, 5]</td>
<td style="text-align: left;">3</td>
<td style="text-align: left;">[5, 1]</td>
</tr>
</tbody>
</table>

### MINIMUM

**Syntax:**

``` text
minimum(array: ARRAY) -> ANY
```

**Description:**

Returns the minimum value in `  array  ` .

  - `  NULL  ` values are ignored during comparison.
  - If `  array  ` is empty or only contains `  NULL  ` values, returns `  NULL  ` .

**Examples:**

<table>
<thead>
<tr class="header">
<th style="text-align: left;">array</th>
<th style="text-align: left;"><code dir="ltr" translate="no">       minimum(array)      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">[1, 5, 2]</td>
<td style="text-align: left;">1</td>
</tr>
<tr class="even">
<td style="text-align: left;">[5, null, 1]</td>
<td style="text-align: left;">1</td>
</tr>
<tr class="odd">
<td style="text-align: left;">["a", "c", "b"]</td>
<td style="text-align: left;">"a"</td>
</tr>
<tr class="even">
<td style="text-align: left;">[null, null]</td>
<td style="text-align: left;">null</td>
</tr>
<tr class="odd">
<td style="text-align: left;">[]</td>
<td style="text-align: left;">null</td>
</tr>
</tbody>
</table>

### MINIMUM\_N

**Syntax:**

``` text
minimum_n(array: ARRAY, n: INT64) -> ARRAY
```

**Description:**

Returns an array of the `  n  ` smallest values in `  array  ` in ascending order.

  - `  NULL  ` values are ignored.
  - If `  n  ` is negative, returns an error.

**Examples:**

<table>
<thead>
<tr class="header">
<th style="text-align: left;">array</th>
<th style="text-align: left;">n</th>
<th style="text-align: left;"><code dir="ltr" translate="no">       minimum_n(array, n)      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">[1, 5, 2, 4, 3]</td>
<td style="text-align: left;">3</td>
<td style="text-align: left;">[1, 2, 3]</td>
</tr>
<tr class="even">
<td style="text-align: left;">[5, null, 1]</td>
<td style="text-align: left;">3</td>
<td style="text-align: left;">[1, 5]</td>
</tr>
</tbody>
</table>

### SUM

**Syntax:**

``` text
sum(array: ARRAY) -> INT64 | FLOAT64
```

**Description:**

Returns the sum of all `  NUMERIC  ` values in an `  ARRAY  ` .

  - Non-numeric values in the array are ignored.
  - If any numeric value in the array is `  NaN  ` , the function returns `  NaN  ` .
  - The return type is determined by the widest numeric type in the array: `  INT64  ` \< `  FLOAT64  ` .
  - If 64-bit integer overflow occurs before any floating point value is summed, an error is returned. If floating point values are summed, overflow will result in +/- infinity.
  - If the array contains no numeric values at all, the function returns `  NULL  ` .

**Examples:**

<table>
<thead>
<tr class="header">
<th style="text-align: left;">array</th>
<th style="text-align: left;"><code dir="ltr" translate="no">       sum(array)      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">[1, 2, 3]</td>
<td style="text-align: left;">6L</td>
</tr>
<tr class="even">
<td style="text-align: left;">[1L, 2L, 3L]</td>
<td style="text-align: left;">6L</td>
</tr>
<tr class="odd">
<td style="text-align: left;">[2000000000, 2000000000]</td>
<td style="text-align: left;">4000000000L</td>
</tr>
<tr class="even">
<td style="text-align: left;">[10, 20.5]</td>
<td style="text-align: left;">30.5</td>
</tr>
<tr class="odd">
<td style="text-align: left;">[1, "a", 2]</td>
<td style="text-align: left;">3L</td>
</tr>
<tr class="even">
<td style="text-align: left;">[INT64.MAX_VALUE, 1]</td>
<td style="text-align: left;">error</td>
</tr>
<tr class="odd">
<td style="text-align: left;">[INT64.MAX_VALUE, 1, -1.0]</td>
<td style="text-align: left;">error</td>
</tr>
<tr class="even">
<td style="text-align: left;">[INT64.MAX_VALUE, 1.0]</td>
<td style="text-align: left;">9.223372036854776e+18</td>
</tr>
</tbody>
</table>

### JOIN

**Syntax:**

``` text
join[T <: STRING | BYTES](array: ARRAY<T>, delimiter: T) -> STRING
join[T <: STRING | BYTES](array: ARRAY<T>, delimiter: T, null_text: T) -> STRING
```

**Description:**

Returns a concatenation of the elements in `  array  ` as a `  STRING  ` . The `  array  ` can be of `  STRING  ` or `  BYTES  ` data types.

  - All elements in `  array  ` , `  delimiter  ` , and `  null_text  ` must be of the same type; they must all be `  STRING  ` s or all be `  BYTES  ` .
  - If `  null_text  ` is provided, any `  NULL  ` values in `  array  ` are replaced with `  null_text  ` .
  - If `  null_text  ` is not provided, `  NULL  ` values in `  array  ` are omitted from the result.

**Examples:**

When `  null_text  ` is not provided:

<table>
<thead>
<tr class="header">
<th style="text-align: left;">array</th>
<th style="text-align: left;">delimiter</th>
<th style="text-align: left;"><code dir="ltr" translate="no">       join(array, delimiter)      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">["a", "b", "c"]</td>
<td style="text-align: left;">","</td>
<td style="text-align: left;">"a,b,c"</td>
</tr>
<tr class="even">
<td style="text-align: left;">["a", null, "c"]</td>
<td style="text-align: left;">","</td>
<td style="text-align: left;">"a,c"</td>
</tr>
<tr class="odd">
<td style="text-align: left;">[b'a', b'b', b'c']</td>
<td style="text-align: left;">b','</td>
<td style="text-align: left;">b'a,b,c'</td>
</tr>
<tr class="even">
<td style="text-align: left;">["a", b'c']</td>
<td style="text-align: left;">","</td>
<td style="text-align: left;">error</td>
</tr>
<tr class="odd">
<td style="text-align: left;">["a", "c"]</td>
<td style="text-align: left;">b','</td>
<td style="text-align: left;">error</td>
</tr>
<tr class="even">
<td style="text-align: left;">[b'a', b'c']</td>
<td style="text-align: left;">","</td>
<td style="text-align: left;">error</td>
</tr>
</tbody>
</table>

When `  null_text  ` is provided:

<table>
<thead>
<tr class="header">
<th style="text-align: left;">array</th>
<th style="text-align: left;">delimiter</th>
<th style="text-align: left;">null_text</th>
<th style="text-align: left;"><code dir="ltr" translate="no">       join(array, delimiter, null_text)      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">["a", null, "c"]</td>
<td style="text-align: left;">","</td>
<td style="text-align: left;">"MISSING"</td>
<td style="text-align: left;">"a,MISSING,c"</td>
</tr>
<tr class="even">
<td style="text-align: left;">[b'a', null, b'c']</td>
<td style="text-align: left;">b','</td>
<td style="text-align: left;">b'NULL'</td>
<td style="text-align: left;">b'a,NULL,c'</td>
</tr>
<tr class="odd">
<td style="text-align: left;">[null, "b", null]</td>
<td style="text-align: left;">","</td>
<td style="text-align: left;">"MISSING"</td>
<td style="text-align: left;">"MISSING,b,MISSING"</td>
</tr>
<tr class="even">
<td style="text-align: left;">[b'a', null, null]</td>
<td style="text-align: left;">b','</td>
<td style="text-align: left;">b'NULL'</td>
<td style="text-align: left;">b'a,NULL,NULL'</td>
</tr>
<tr class="odd">
<td style="text-align: left;">["a", null]</td>
<td style="text-align: left;">","</td>
<td style="text-align: left;">b'N'</td>
<td style="text-align: left;">error</td>
</tr>
<tr class="even">
<td style="text-align: left;">[b'a', null]</td>
<td style="text-align: left;">b','</td>
<td style="text-align: left;">"N"</td>
<td style="text-align: left;">error</td>
</tr>
</tbody>
</table>

## What's next

  - See the [Pipeline Queries overview](/firestore/docs/pipeline/overview)
