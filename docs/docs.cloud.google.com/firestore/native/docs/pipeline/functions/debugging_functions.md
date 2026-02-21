# Debugging Functions Reference

**Preview — Firestore in Native mode (with Pipeline Operations) for Enterprise Edition**

This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](/terms/service-terms#1) . You can process personal data for this feature as outlined in the [Cloud Data Processing Addendum](/terms/data-processing-addendum) , subject to the obligations and restrictions described in the agreement under which you access Google Cloud. Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

## **Debugging Functions**

<table>
<tbody>
<tr class="odd">
<td>Name</td>
<td>Description</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         EXISTS       </code></td>
<td>Returns <code dir="ltr" translate="no">       TRUE      </code> if the value is not an absent value</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         IS_ABSENT       </code></td>
<td>Returns <code dir="ltr" translate="no">       TRUE      </code> if the value is an absent value</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         IF_ABSENT       </code></td>
<td>Replaces the value with an expression if it is absent</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         IS_ERROR       </code></td>
<td>Catches and checks if an error has been thrown by the underlying expression</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         IF_ERROR       </code></td>
<td>Replaces the value with an expression if it has thrown an error</td>
</tr>
</tbody>
</table>

### EXISTS

**Syntax:**

``` text
exists(value: ANY) -> BOOLEAN
```

**Description:**

Returns `  TRUE  ` if `  value  ` is not the absent value.

**Examples:**

<table>
<thead>
<tr class="header">
<th style="text-align: left;"><code dir="ltr" translate="no">       value      </code></th>
<th style="text-align: left;"><code dir="ltr" translate="no">       exists(value)      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">0L</td>
<td style="text-align: left;"><code dir="ltr" translate="no">       TRUE      </code></td>
</tr>
<tr class="even">
<td style="text-align: left;">"foo"</td>
<td style="text-align: left;"><code dir="ltr" translate="no">       TRUE      </code></td>
</tr>
<tr class="odd">
<td style="text-align: left;"><code dir="ltr" translate="no">       NULL      </code></td>
<td style="text-align: left;"><code dir="ltr" translate="no">       TRUE      </code></td>
</tr>
<tr class="even">
<td style="text-align: left;"><code dir="ltr" translate="no">       ABSENT      </code></td>
<td style="text-align: left;"><code dir="ltr" translate="no">       FALSE      </code></td>
</tr>
</tbody>
</table>

##### Node.js

``` javascript
const result = await db.pipeline()
  .collection("books")
  .select(field("rating").exists().as("hasRating"))
  .execute();test.firestore.js
```

### Web

**Example:**

``` javascript
const result = await execute(db.pipeline()
  .collection("books")
  .select(field("rating").exists().as("hasRating"))
);test.firestore.js
```

##### Swift

``` swift
let result = try await db.pipeline()
  .collection("books")
  .select([Field("rating").exists().as("hasRating")])
  .execute()PipelineSnippets.swift
```

##### Kotlin  
Android

**Example:**

``` kotlin
val result = db.pipeline()
    .collection("books")
    .select(field("rating").exists().alias("hasRating"))
    .execute()DocSnippets.kt
```

##### Java  
Android

**Example:**

``` text
Task<Pipeline.Snapshot> result = db.pipeline()
    .collection("books")
    .select(field("rating").exists().alias("hasRating"))
    .execute();DocSnippets.java
```

##### Python

``` python
from google.cloud.firestore_v1.pipeline_expressions import Field

result = (
    client.pipeline()
    .collection("books")
    .select(Field.of("rating").exists().as_("hasRating"))
    .execute()
)firestore_pipelines.py
```

##### Java

``` java
Pipeline.Snapshot result =
    firestore
        .pipeline()
        .collection("books")
        .select(exists(field("rating")).as("hasRating"))
        .execute()
        .get();PipelineSnippets.java
```

### IS\_ABSENT

**Syntax:**

``` text
is_absent(value: ANY) -> BOOLEAN
```

**Description:**

Returns `  TRUE  ` if `  value  ` is the absent value, and `  FALSE  ` otherwise. Absent values are values that are missing from the input, such as a missing document field.

**Examples:**

<table>
<thead>
<tr class="header">
<th style="text-align: left;"><code dir="ltr" translate="no">       value      </code></th>
<th style="text-align: left;"><code dir="ltr" translate="no">       is_absent(value)      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">0L</td>
<td style="text-align: left;"><code dir="ltr" translate="no">       FALSE      </code></td>
</tr>
<tr class="even">
<td style="text-align: left;">"foo"</td>
<td style="text-align: left;"><code dir="ltr" translate="no">       FALSE      </code></td>
</tr>
<tr class="odd">
<td style="text-align: left;"><code dir="ltr" translate="no">       NULL      </code></td>
<td style="text-align: left;"><code dir="ltr" translate="no">       FALSE      </code></td>
</tr>
<tr class="even">
<td style="text-align: left;"><code dir="ltr" translate="no">       ABSENT      </code></td>
<td style="text-align: left;"><code dir="ltr" translate="no">       TRUE      </code></td>
</tr>
</tbody>
</table>

### IF\_ABSENT

**Syntax:**

``` text
if_absent(value: ANY, replacement: ANY) -> ANY
```

**Description:**

If `  value  ` is an absent value, evaluates and returns `  replacement  ` . Otherwise returns `  value  ` .

**Examples:**

<table>
<thead>
<tr class="header">
<th style="text-align: left;"><code dir="ltr" translate="no">       value      </code></th>
<th style="text-align: left;"><code dir="ltr" translate="no">       replacement      </code></th>
<th style="text-align: left;"><code dir="ltr" translate="no">       if_absent(value, replacement)      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">5L</td>
<td style="text-align: left;">0L</td>
<td style="text-align: left;">5L</td>
</tr>
<tr class="even">
<td style="text-align: left;"><code dir="ltr" translate="no">       NULL      </code></td>
<td style="text-align: left;">0L</td>
<td style="text-align: left;"><code dir="ltr" translate="no">       NULL      </code></td>
</tr>
<tr class="odd">
<td style="text-align: left;"><code dir="ltr" translate="no">       ABSENT      </code></td>
<td style="text-align: left;">0L</td>
<td style="text-align: left;">0L</td>
</tr>
</tbody>
</table>

### IS\_ERROR

**Syntax:**

``` text
is_error(try: ANY) -> BOOLEAN
```

**Description:**

Returns `  TRUE  ` if an error is thrown during the evaluation of `  try  ` . Returns `  FALSE  ` otherwise.

### IF\_ERROR

**Syntax:**

``` text
if_error(try: ANY, catch: ANY) -> ANY
```

**Description:**

If an error is thrown during the evaluation of `  try  ` , evaluates and returns `  replacement  ` . Otherwise returns the resolved value of `  try  ` .

## What's next

  - See the [Pipeline Queries overview](/firestore/docs/pipeline/overview)
