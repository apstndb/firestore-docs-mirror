# Type Functions Reference

**Preview — Firestore in Native mode (with Pipeline Operations) for Enterprise Edition**

This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](/terms/service-terms#1) . You can process personal data for this feature as outlined in the [Cloud Data Processing Addendum](/terms/data-processing-addendum) , subject to the obligations and restrictions described in the agreement under which you access Google Cloud. Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

## **Type Functions**

<table>
<tbody>
<tr class="odd">
<td>Name</td>
<td>Description</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         TYPE       </code></td>
<td>Returns the type of the value as a <code dir="ltr" translate="no">       STRING      </code> .</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         IS_TYPE       </code></td>
<td>Returns <code dir="ltr" translate="no">       true      </code> if the value matches the specified type.</td>
</tr>
</tbody>
</table>

### TYPE

**Syntax:**

``` text
type(input: ANY) -> STRING
```

**Description:**

Returns a string representation of the `  input  ` type.

If given an absent value, returns `  NULL  ` .

**Examples:**

<table>
<thead>
<tr class="header">
<th><code dir="ltr" translate="no">       input      </code></th>
<th><code dir="ltr" translate="no">       type(input)      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>NULL</td>
<td>"null"</td>
</tr>
<tr class="even">
<td>true</td>
<td>"boolean"</td>
</tr>
<tr class="odd">
<td>1</td>
<td>"int32"</td>
</tr>
<tr class="even">
<td>-3L</td>
<td>"int64"</td>
</tr>
<tr class="odd">
<td>3.14</td>
<td>"float64"</td>
</tr>
<tr class="even">
<td>2024-01-01T00:00:00Z UTC</td>
<td>"timestamp"</td>
</tr>
<tr class="odd">
<td>"foo"</td>
<td>"string"</td>
</tr>
<tr class="even">
<td>b"foo"</td>
<td>"bytes"</td>
</tr>
<tr class="odd">
<td>[1, 2]</td>
<td>"array"</td>
</tr>
<tr class="even">
<td>{"a": 1}</td>
<td>"map"</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       path("c/d")      </code></td>
<td>"reference"</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       vector([1.0, 2.0])      </code></td>
<td>"vector"</td>
</tr>
<tr class="odd">
<td>ABSENT</td>
<td>NULL</td>
</tr>
</tbody>
</table>

**Client examples**

##### Node.js

``` javascript
const result = await db.pipeline()
  .collection("books")
  .select(field("title").notEqual("1984").as("not1984"))
  .execute();test.firestore.js
```

### Web

``` javascript
const result = await execute(db.pipeline()
  .collection("books")
  .select(field("title").notEqual("1984").as("not1984"))
);test.firestore.js
```

##### Swift

``` swift
let result = try await db.pipeline()
  .collection("books")
  .select([Field("title").notEqual("1984").as("not1984")])
  .execute()PipelineSnippets.swift
```

##### Kotlin  
Android

``` kotlin
val result = db.pipeline()
    .collection("books")
    .select(field("title").notEqual("1984").alias("not1984"))
    .execute()DocSnippets.kt
```

##### Java  
Android

``` text
Task<Pipeline.Snapshot> result = db.pipeline()
    .collection("books")
    .select(field("title").notEqual("1984").alias("not1984"))
    .execute();DocSnippets.java
```

##### Python

``` python
from google.cloud.firestore_v1.pipeline_expressions import Field

result = (
    client.pipeline()
    .collection("books")
    .select(Field.of("title").not_equal("1984").as_("not1984"))
    .execute()
)firestore_pipelines.py
```

##### Java

``` java
Pipeline.Snapshot result =
    firestore
        .pipeline()
        .collection("books")
        .select(notEqual(field("title"), "1984").as("not1984"))
        .execute()
        .get();PipelineSnippets.java
```

### IS\_TYPE

**Syntax:**

``` text
is_type(input: ANY, type: STRING) -> BOOLEAN
```

**Description:**

Returns `  true  ` if the `  input  ` matches the specified `  type  ` , otherwise `  false  ` . If given an absent `  input  ` , returns `  NULL  ` .

Supported `  type  ` strings are:

  - `  "null"  `
  - `  "boolean"  `
  - `  "int32"  `
  - `  "int64"  `
  - `  "float64"  `
  - `  "decimal128"  `
  - `  "number"  `
  - `  "timestamp"  `
  - `  "string"  `
  - `  "bytes"  `
  - `  "array"  `
  - `  "map"  `
  - `  "reference"  `
  - `  "vector"  `
  - `  "geo_point"  `
  - `  "max_key"  `
  - `  "min_key"  `
  - `  "object_id"  `
  - `  "regex"  `
  - `  "bson_timestamp"  `

**Examples:**

<table>
<thead>
<tr class="header">
<th style="text-align: left;"><code dir="ltr" translate="no">       input      </code></th>
<th style="text-align: left;"><code dir="ltr" translate="no">       type      </code></th>
<th style="text-align: left;"><code dir="ltr" translate="no">       is_type(input, type)      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">NULL</td>
<td style="text-align: left;">"null"</td>
<td style="text-align: left;">true</td>
</tr>
<tr class="even">
<td style="text-align: left;">true</td>
<td style="text-align: left;">"boolean"</td>
<td style="text-align: left;">true</td>
</tr>
<tr class="odd">
<td style="text-align: left;">3.14</td>
<td style="text-align: left;">"float64"</td>
<td style="text-align: left;">true</td>
</tr>
<tr class="even">
<td style="text-align: left;">"foo"</td>
<td style="text-align: left;">"string"</td>
<td style="text-align: left;">true</td>
</tr>
<tr class="odd">
<td style="text-align: left;">b"foo"</td>
<td style="text-align: left;">"string"</td>
<td style="text-align: left;">false</td>
</tr>
<tr class="even">
<td style="text-align: left;">[1, 2]</td>
<td style="text-align: left;">"array"</td>
<td style="text-align: left;">true</td>
</tr>
<tr class="odd">
<td style="text-align: left;">{"a": 1}</td>
<td style="text-align: left;">"map"</td>
<td style="text-align: left;">true</td>
</tr>
<tr class="even">
<td style="text-align: left;"><code dir="ltr" translate="no">       vector([1.0, 2.0])      </code></td>
<td style="text-align: left;">"vector"</td>
<td style="text-align: left;">true</td>
</tr>
<tr class="odd">
<td style="text-align: left;">ABSENT</td>
<td style="text-align: left;">"string"</td>
<td style="text-align: left;">NULL</td>
</tr>
<tr class="even">
<td style="text-align: left;">"bar"</td>
<td style="text-align: left;">"other"</td>
<td style="text-align: left;">ERROR</td>
</tr>
</tbody>
</table>

## What's next

  - See the [Pipeline Queries overview](/firestore/docs/pipeline/overview)
