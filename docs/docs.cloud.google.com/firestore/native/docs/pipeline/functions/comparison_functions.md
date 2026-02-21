# Comparison Functions Reference

**Preview — Firestore in Native mode (with Pipeline Operations) for Enterprise Edition**

This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](/terms/service-terms#1) . You can process personal data for this feature as outlined in the [Cloud Data Processing Addendum](/terms/data-processing-addendum) , subject to the obligations and restrictions described in the agreement under which you access Google Cloud. Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

## **Comparison Functions**

<table>
<tbody>
<tr class="odd">
<td>Name</td>
<td>Description</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         EQUAL       </code></td>
<td>Equality comparison</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         GREATER_THAN       </code></td>
<td>Greater than comparison</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         GREATER_THAN_OR_EQUAL       </code></td>
<td>Greater than or equal comparison</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         LESS_THAN       </code></td>
<td>Less than comparison</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         LESS_THAN_OR_EQUAL       </code></td>
<td>Less than or equal comparison</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         NOT_EQUAL       </code></td>
<td>Not equals comparison</td>
</tr>
</tbody>
</table>

### EQUAL

**Syntax:**

``` text
equal(x: ANY, y: ANY) -> BOOLEAN
```

**Examples:**

<table>
<thead>
<tr class="header">
<th style="text-align: left;"><code dir="ltr" translate="no">       x      </code></th>
<th style="text-align: left;"><code dir="ltr" translate="no">       y      </code></th>
<th style="text-align: left;"><code dir="ltr" translate="no">       equal(x, y)      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">1L</td>
<td style="text-align: left;">1L</td>
<td style="text-align: left;"><code dir="ltr" translate="no">       TRUE      </code></td>
</tr>
<tr class="even">
<td style="text-align: left;">1.0</td>
<td style="text-align: left;">1L</td>
<td style="text-align: left;"><code dir="ltr" translate="no">       TRUE      </code></td>
</tr>
<tr class="odd">
<td style="text-align: left;">-1.0</td>
<td style="text-align: left;">1L</td>
<td style="text-align: left;"><code dir="ltr" translate="no">       FALSE      </code></td>
</tr>
<tr class="even">
<td style="text-align: left;">NaN</td>
<td style="text-align: left;">NaN</td>
<td style="text-align: left;"><code dir="ltr" translate="no">       TRUE      </code></td>
</tr>
<tr class="odd">
<td style="text-align: left;"><code dir="ltr" translate="no">       NULL      </code></td>
<td style="text-align: left;"><code dir="ltr" translate="no">       NULL      </code></td>
<td style="text-align: left;"><code dir="ltr" translate="no">       TRUE      </code></td>
</tr>
<tr class="even">
<td style="text-align: left;"><code dir="ltr" translate="no">       NULL      </code></td>
<td style="text-align: left;"><code dir="ltr" translate="no">       ABSENT      </code></td>
<td style="text-align: left;"><code dir="ltr" translate="no">       FALSE      </code></td>
</tr>
</tbody>
</table>

**Description:**

Returns `  TRUE  ` if `  x  ` and `  y  ` are equal, and `  FALSE  ` otherwise.

##### Node.js

``` javascript
const result = await db.pipeline()
  .collection("books")
  .select(field("rating").equal(5).as("hasPerfectRating"))
  .execute();test.firestore.js
```

### Web

``` javascript
const result = await execute(db.pipeline()
  .collection("books")
  .select(field("rating").equal(5).as("hasPerfectRating"))
);test.firestore.js
```

##### Swift

``` swift
let result = try await db.pipeline()
  .collection("books")
  .select([Field("rating").equal(5).as("hasPerfectRating")])
  .execute()PipelineSnippets.swift
```

##### Kotlin  
Android

``` kotlin
val result = db.pipeline()
    .collection("books")
    .select(field("rating").equal(5).alias("hasPerfectRating"))
    .execute()DocSnippets.kt
```

##### Java  
Android

``` text
Task<Pipeline.Snapshot> result = db.pipeline()
    .collection("books")
    .select(field("rating").equal(5).alias("hasPerfectRating"))
    .execute();DocSnippets.java
```

##### Python

``` python
from google.cloud.firestore_v1.pipeline_expressions import Field

result = (
    client.pipeline()
    .collection("books")
    .select(Field.of("rating").equal(5).as_("hasPerfectRating"))
    .execute()
)firestore_pipelines.py
```

##### Java

``` java
Pipeline.Snapshot result =
    firestore
        .pipeline()
        .collection("books")
        .select(equal(field("rating"), 5).as("hasPerfectRating"))
        .execute()
        .get();PipelineSnippets.java
```

### GREATER\_THAN

**Syntax:**

``` text
greater_than(x: ANY, y: ANY) -> BOOLEAN
```

**Description:**

Returns `  TRUE  ` if `  x  ` is greater than `  y  ` , and `  FALSE  ` otherwise.

If `  x  ` and `  y  ` are not comparable, returns `  FALSE  ` .

**Examples:**

<table>
<thead>
<tr class="header">
<th style="text-align: left;"><code dir="ltr" translate="no">       x      </code></th>
<th style="text-align: left;"><code dir="ltr" translate="no">       y      </code></th>
<th style="text-align: left;"><code dir="ltr" translate="no">       greater_than(x, y)      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">1L</td>
<td style="text-align: left;">0.0</td>
<td style="text-align: left;"><code dir="ltr" translate="no">       TRUE      </code></td>
</tr>
<tr class="even">
<td style="text-align: left;">1L</td>
<td style="text-align: left;">1L</td>
<td style="text-align: left;"><code dir="ltr" translate="no">       FALSE      </code></td>
</tr>
<tr class="odd">
<td style="text-align: left;">1L</td>
<td style="text-align: left;">2L</td>
<td style="text-align: left;"><code dir="ltr" translate="no">       FALSE      </code></td>
</tr>
<tr class="even">
<td style="text-align: left;">"foo"</td>
<td style="text-align: left;">0L</td>
<td style="text-align: left;"><code dir="ltr" translate="no">       FALSE      </code></td>
</tr>
<tr class="odd">
<td style="text-align: left;">0L</td>
<td style="text-align: left;">"foo"</td>
<td style="text-align: left;"><code dir="ltr" translate="no">       FALSE      </code></td>
</tr>
<tr class="even">
<td style="text-align: left;">NaN</td>
<td style="text-align: left;">0L</td>
<td style="text-align: left;"><code dir="ltr" translate="no">       FALSE      </code></td>
</tr>
<tr class="odd">
<td style="text-align: left;">0L</td>
<td style="text-align: left;">NaN</td>
<td style="text-align: left;"><code dir="ltr" translate="no">       FALSE      </code></td>
</tr>
<tr class="even">
<td style="text-align: left;"><code dir="ltr" translate="no">       NULL      </code></td>
<td style="text-align: left;"><code dir="ltr" translate="no">       NULL      </code></td>
<td style="text-align: left;"><code dir="ltr" translate="no">       FALSE      </code></td>
</tr>
</tbody>
</table>

##### Node.js

``` javascript
const result = await db.pipeline()
  .collection("books")
  .select(field("rating").greaterThan(4).as("hasHighRating"))
  .execute();test.firestore.js
```

### Web

``` javascript
const result = await execute(db.pipeline()
  .collection("books")
  .select(field("rating").greaterThan(4).as("hasHighRating"))
);test.firestore.js
```

##### Swift

``` swift
let result = try await db.pipeline()
  .collection("books")
  .select([Field("rating").greaterThan(4).as("hasHighRating")])
  .execute()PipelineSnippets.swift
```

##### Kotlin  
Android

``` kotlin
val result = db.pipeline()
    .collection("books")
    .select(field("rating").greaterThan(4).alias("hasHighRating"))
    .execute()DocSnippets.kt
```

##### Java  
Android

``` text
Task<Pipeline.Snapshot> result = db.pipeline()
    .collection("books")
    .select(field("rating").greaterThan(4).alias("hasHighRating"))
    .execute();DocSnippets.java
```

##### Python

``` python
from google.cloud.firestore_v1.pipeline_expressions import Field

result = (
    client.pipeline()
    .collection("books")
    .select(Field.of("rating").greater_than(4).as_("hasHighRating"))
    .execute()
)firestore_pipelines.py
```

##### Java

``` java
Pipeline.Snapshot result =
    firestore
        .pipeline()
        .collection("books")
        .select(greaterThan(field("rating"), 4).as("hasHighRating"))
        .execute()
        .get();PipelineSnippets.java
```

### GREATER\_THAN\_OR\_EQUAL

**Syntax:**

``` text
greater_than_or_equal(x: ANY, y: ANY) -> BOOLEAN
```

**Description:**

Returns `  TRUE  ` if `  x  ` is greater than or equal to `  y  ` , and `  FALSE  ` otherwise.

If `  x  ` and `  y  ` are not comparable, returns `  FALSE  ` .

**Examples:**

<table>
<thead>
<tr class="header">
<th style="text-align: left;"><code dir="ltr" translate="no">       x      </code></th>
<th style="text-align: left;"><code dir="ltr" translate="no">       y      </code></th>
<th style="text-align: left;"><code dir="ltr" translate="no">       greater_than_or_equal(x, y)      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">1L</td>
<td style="text-align: left;">0.0</td>
<td style="text-align: left;"><code dir="ltr" translate="no">       TRUE      </code></td>
</tr>
<tr class="even">
<td style="text-align: left;">1L</td>
<td style="text-align: left;">1L</td>
<td style="text-align: left;"><code dir="ltr" translate="no">       TRUE      </code></td>
</tr>
<tr class="odd">
<td style="text-align: left;">1L</td>
<td style="text-align: left;">2L</td>
<td style="text-align: left;"><code dir="ltr" translate="no">       FALSE      </code></td>
</tr>
<tr class="even">
<td style="text-align: left;">"foo"</td>
<td style="text-align: left;">0L</td>
<td style="text-align: left;"><code dir="ltr" translate="no">       FALSE      </code></td>
</tr>
<tr class="odd">
<td style="text-align: left;">0L</td>
<td style="text-align: left;">"foo"</td>
<td style="text-align: left;"><code dir="ltr" translate="no">       FALSE      </code></td>
</tr>
<tr class="even">
<td style="text-align: left;">NaN</td>
<td style="text-align: left;">0L</td>
<td style="text-align: left;"><code dir="ltr" translate="no">       FALSE      </code></td>
</tr>
<tr class="odd">
<td style="text-align: left;">0L</td>
<td style="text-align: left;">NaN</td>
<td style="text-align: left;"><code dir="ltr" translate="no">       FALSE      </code></td>
</tr>
<tr class="even">
<td style="text-align: left;"><code dir="ltr" translate="no">       NULL      </code></td>
<td style="text-align: left;"><code dir="ltr" translate="no">       NULL      </code></td>
<td style="text-align: left;"><code dir="ltr" translate="no">       TRUE      </code></td>
</tr>
</tbody>
</table>

##### Node.js

``` javascript
const result = await db.pipeline()
  .collection("books")
  .select(field("published").greaterThanOrEqual(1900).as("publishedIn20thCentury"))
  .execute();test.firestore.js
```

### Web

``` javascript
const result = await execute(db.pipeline()
  .collection("books")
  .select(field("published").greaterThanOrEqual(1900).as("publishedIn20thCentury"))
);test.firestore.js
```

##### Swift

``` swift
let result = try await db.pipeline()
  .collection("books")
  .select([Field("published").greaterThanOrEqual(1900).as("publishedIn20thCentury")])
  .execute()PipelineSnippets.swift
```

##### Kotlin  
Android

``` kotlin
val result = db.pipeline()
    .collection("books")
    .select(field("published").greaterThanOrEqual(1900).alias("publishedIn20thCentury"))
    .execute()DocSnippets.kt
```

##### Java  
Android

``` text
Task<Pipeline.Snapshot> result = db.pipeline()
    .collection("books")
    .select(field("published").greaterThanOrEqual(1900).alias("publishedIn20thCentury"))
    .execute();DocSnippets.java
```

##### Python

``` python
from google.cloud.firestore_v1.pipeline_expressions import Field

result = (
    client.pipeline()
    .collection("books")
    .select(
        Field.of("published")
        .greater_than_or_equal(1900)
        .as_("publishedIn20thCentury")
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
        .select(greaterThanOrEqual(field("published"), 1900).as("publishedIn20thCentury"))
        .execute()
        .get();PipelineSnippets.java
```

### LESS\_THAN

**Syntax:**

``` text
less_than(x: ANY, y: ANY) -> BOOLEAN
```

**Description:**

Returns `  TRUE  ` if `  x  ` is less than `  y  ` , and `  FALSE  ` otherwise.

If `  x  ` and `  y  ` are not comparable, returns `  FALSE  ` .

**Examples:**

<table>
<thead>
<tr class="header">
<th style="text-align: left;"><code dir="ltr" translate="no">       x      </code></th>
<th style="text-align: left;"><code dir="ltr" translate="no">       y      </code></th>
<th style="text-align: left;"><code dir="ltr" translate="no">       less_than(x, y)      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">1L</td>
<td style="text-align: left;">0.0</td>
<td style="text-align: left;"><code dir="ltr" translate="no">       FALSE      </code></td>
</tr>
<tr class="even">
<td style="text-align: left;">1L</td>
<td style="text-align: left;">1L</td>
<td style="text-align: left;"><code dir="ltr" translate="no">       FALSE      </code></td>
</tr>
<tr class="odd">
<td style="text-align: left;">1L</td>
<td style="text-align: left;">2L</td>
<td style="text-align: left;"><code dir="ltr" translate="no">       TRUE      </code></td>
</tr>
<tr class="even">
<td style="text-align: left;">"foo"</td>
<td style="text-align: left;">0L</td>
<td style="text-align: left;"><code dir="ltr" translate="no">       FALSE      </code></td>
</tr>
<tr class="odd">
<td style="text-align: left;">0L</td>
<td style="text-align: left;">"foo"</td>
<td style="text-align: left;"><code dir="ltr" translate="no">       FALSE      </code></td>
</tr>
<tr class="even">
<td style="text-align: left;">NaN</td>
<td style="text-align: left;">0L</td>
<td style="text-align: left;"><code dir="ltr" translate="no">       FALSE      </code></td>
</tr>
<tr class="odd">
<td style="text-align: left;">0L</td>
<td style="text-align: left;">NaN</td>
<td style="text-align: left;"><code dir="ltr" translate="no">       FALSE      </code></td>
</tr>
<tr class="even">
<td style="text-align: left;"><code dir="ltr" translate="no">       NULL      </code></td>
<td style="text-align: left;"><code dir="ltr" translate="no">       NULL      </code></td>
<td style="text-align: left;"><code dir="ltr" translate="no">       FALSE      </code></td>
</tr>
</tbody>
</table>

##### Node.js

``` javascript
const result = await db.pipeline()
  .collection("books")
  .select(field("published").lessThan(1923).as("isPublicDomainProbably"))
  .execute();test.firestore.js
```

### Web

``` javascript
const result = await execute(db.pipeline()
  .collection("books")
  .select(field("published").lessThan(1923).as("isPublicDomainProbably"))
);test.firestore.js
```

##### Swift

``` swift
let result = try await db.pipeline()
  .collection("books")
  .select([Field("published").lessThan(1923).as("isPublicDomainProbably")])
  .execute()PipelineSnippets.swift
```

##### Kotlin  
Android

``` kotlin
val result = db.pipeline()
    .collection("books")
    .select(field("published").lessThan(1923).alias("isPublicDomainProbably"))
    .execute()DocSnippets.kt
```

##### Java  
Android

``` text
Task<Pipeline.Snapshot> result = db.pipeline()
    .collection("books")
    .select(field("published").lessThan(1923).alias("isPublicDomainProbably"))
    .execute();DocSnippets.java
```

##### Python

``` python
from google.cloud.firestore_v1.pipeline_expressions import Field

result = (
    client.pipeline()
    .collection("books")
    .select(Field.of("published").less_than(1923).as_("isPublicDomainProbably"))
    .execute()
)firestore_pipelines.py
```

##### Java

``` java
Pipeline.Snapshot result =
    firestore
        .pipeline()
        .collection("books")
        .select(lessThan(field("published"), 1923).as("isPublicDomainProbably"))
        .execute()
        .get();PipelineSnippets.java
```

### LESS\_THAN\_OR\_EQUAL

**Syntax:**

``` text
less_than_or_equal(x: ANY, y: ANY) -> BOOLEAN
```

**Description:**

Returns `  TRUE  ` if `  x  ` is less than or equal to `  y  ` , and `  FALSE  ` otherwise.

If `  x  ` and `  y  ` are not comparable, returns `  FALSE  ` .

**Examples:**

<table>
<thead>
<tr class="header">
<th style="text-align: left;"><code dir="ltr" translate="no">       x      </code></th>
<th style="text-align: left;"><code dir="ltr" translate="no">       y      </code></th>
<th style="text-align: left;"><code dir="ltr" translate="no">       less_than(x, y)      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">1L</td>
<td style="text-align: left;">0.0</td>
<td style="text-align: left;"><code dir="ltr" translate="no">       FALSE      </code></td>
</tr>
<tr class="even">
<td style="text-align: left;">1L</td>
<td style="text-align: left;">1L</td>
<td style="text-align: left;"><code dir="ltr" translate="no">       TRUE      </code></td>
</tr>
<tr class="odd">
<td style="text-align: left;">1L</td>
<td style="text-align: left;">2L</td>
<td style="text-align: left;"><code dir="ltr" translate="no">       TRUE      </code></td>
</tr>
<tr class="even">
<td style="text-align: left;">"foo"</td>
<td style="text-align: left;">0L</td>
<td style="text-align: left;"><code dir="ltr" translate="no">       FALSE      </code></td>
</tr>
<tr class="odd">
<td style="text-align: left;">0L</td>
<td style="text-align: left;">"foo"</td>
<td style="text-align: left;"><code dir="ltr" translate="no">       FALSE      </code></td>
</tr>
<tr class="even">
<td style="text-align: left;">NaN</td>
<td style="text-align: left;">0L</td>
<td style="text-align: left;"><code dir="ltr" translate="no">       FALSE      </code></td>
</tr>
<tr class="odd">
<td style="text-align: left;">0L</td>
<td style="text-align: left;">NaN</td>
<td style="text-align: left;"><code dir="ltr" translate="no">       FALSE      </code></td>
</tr>
<tr class="even">
<td style="text-align: left;"><code dir="ltr" translate="no">       NULL      </code></td>
<td style="text-align: left;"><code dir="ltr" translate="no">       NULL      </code></td>
<td style="text-align: left;"><code dir="ltr" translate="no">       TRUE      </code></td>
</tr>
</tbody>
</table>

##### Node.js

``` javascript
const result = await db.pipeline()
  .collection("books")
  .select(field("rating").lessThanOrEqual(2).as("hasBadRating"))
  .execute();test.firestore.js
```

### Web

``` javascript
const result = await execute(db.pipeline()
  .collection("books")
  .select(field("rating").lessThanOrEqual(2).as("hasBadRating"))
);test.firestore.js
```

##### Swift

``` swift
let result = try await db.pipeline()
  .collection("books")
  .select([Field("rating").lessThanOrEqual(2).as("hasBadRating")])
  .execute()PipelineSnippets.swift
```

##### Kotlin  
Android

``` kotlin
val result = db.pipeline()
    .collection("books")
    .select(field("rating").lessThanOrEqual(2).alias("hasBadRating"))
    .execute()DocSnippets.kt
```

##### Java  
Android

``` text
Task<Pipeline.Snapshot> result = db.pipeline()
    .collection("books")
    .select(field("rating").lessThanOrEqual(2).alias("hasBadRating"))
    .execute();DocSnippets.java
```

##### Python

``` python
from google.cloud.firestore_v1.pipeline_expressions import Field

result = (
    client.pipeline()
    .collection("books")
    .select(Field.of("rating").less_than_or_equal(2).as_("hasBadRating"))
    .execute()
)firestore_pipelines.py
```

##### Java

``` java
Pipeline.Snapshot result =
    firestore
        .pipeline()
        .collection("books")
        .select(lessThanOrEqual(field("rating"), 2).as("hasBadRating"))
        .execute()
        .get();PipelineSnippets.java
```

### NOT\_EQUAL

**Syntax:**

``` text
not_equal(x: ANY, y: ANY) -> BOOLEAN
```

**Description:**

Returns `  TRUE  ` if `  x  ` is not equal to `  y  ` , and `  FALSE  ` otherwise.

**Examples:**

<table>
<thead>
<tr class="header">
<th style="text-align: left;"><code dir="ltr" translate="no">       x      </code></th>
<th style="text-align: left;"><code dir="ltr" translate="no">       y      </code></th>
<th style="text-align: left;"><code dir="ltr" translate="no">       not_equal(x, y)      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">1L</td>
<td style="text-align: left;">1L</td>
<td style="text-align: left;"><code dir="ltr" translate="no">       FALSE      </code></td>
</tr>
<tr class="even">
<td style="text-align: left;">1.0</td>
<td style="text-align: left;">1L</td>
<td style="text-align: left;"><code dir="ltr" translate="no">       FALSE      </code></td>
</tr>
<tr class="odd">
<td style="text-align: left;">-1.0</td>
<td style="text-align: left;">1L</td>
<td style="text-align: left;"><code dir="ltr" translate="no">       TRUE      </code></td>
</tr>
<tr class="even">
<td style="text-align: left;">NaN</td>
<td style="text-align: left;">0L</td>
<td style="text-align: left;"><code dir="ltr" translate="no">       TRUE      </code></td>
</tr>
<tr class="odd">
<td style="text-align: left;">NaN</td>
<td style="text-align: left;">NaN</td>
<td style="text-align: left;"><code dir="ltr" translate="no">       FALSE      </code></td>
</tr>
<tr class="even">
<td style="text-align: left;"><code dir="ltr" translate="no">       NULL      </code></td>
<td style="text-align: left;"><code dir="ltr" translate="no">       NULL      </code></td>
<td style="text-align: left;"><code dir="ltr" translate="no">       FALSE      </code></td>
</tr>
<tr class="odd">
<td style="text-align: left;"><code dir="ltr" translate="no">       NULL      </code></td>
<td style="text-align: left;"><code dir="ltr" translate="no">       ABSENT      </code></td>
<td style="text-align: left;"><code dir="ltr" translate="no">       TRUE      </code></td>
</tr>
</tbody>
</table>

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

## What's next

  - See the [Pipeline Queries overview](/firestore/docs/pipeline/overview)
