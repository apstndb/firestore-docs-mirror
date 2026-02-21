# Logical Functions Reference

**Preview — Firestore in Native mode (with Pipeline Operations) for Enterprise Edition**

This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](/terms/service-terms#1) . You can process personal data for this feature as outlined in the [Cloud Data Processing Addendum](/terms/data-processing-addendum) , subject to the obligations and restrictions described in the agreement under which you access Google Cloud. Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

## **Logical Functions**

<table>
<tbody>
<tr class="odd">
<td>Name</td>
<td>Description</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         AND       </code></td>
<td>Performs a logical AND</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         OR       </code></td>
<td>Performs a logical OR</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         XOR       </code></td>
<td>Performs a logical XOR</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         NOT       </code></td>
<td>Performs a logical NOT</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         CONDITIONAL       </code></td>
<td>Branches evaluation based on a conditional expression.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         EQUAL_ANY       </code></td>
<td>Checks if a value is equal to any elements in an array</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         NOT_EQUAL_ANY       </code></td>
<td>Checks if a value is not equal to any elements in an array</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         MAXIMUM       </code></td>
<td>Returns the maximum value in a set of values</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         MINIMUM       </code></td>
<td>Returns the minimum value in a set of values</td>
</tr>
</tbody>
</table>

### AND

**Syntax:**

``` text
and(x: BOOLEAN...) -> BOOLEAN
```

**Description:**

Returns the logical AND of two or more boolean values.

Returns `  NULL  ` if the result can't be derived due to any of the given values being `  ABSENT  ` or `  NULL  ` .

**Examples:**

<table>
<thead>
<tr class="header">
<th style="text-align: left;"><code dir="ltr" translate="no">       x      </code></th>
<th style="text-align: left;"><code dir="ltr" translate="no">       y      </code></th>
<th style="text-align: left;"><code dir="ltr" translate="no">       and(x, y)      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;"><code dir="ltr" translate="no">       TRUE      </code></td>
<td style="text-align: left;"><code dir="ltr" translate="no">       TRUE      </code></td>
<td style="text-align: left;"><code dir="ltr" translate="no">       TRUE      </code></td>
</tr>
<tr class="even">
<td style="text-align: left;"><code dir="ltr" translate="no">       FALSE      </code></td>
<td style="text-align: left;"><code dir="ltr" translate="no">       TRUE      </code></td>
<td style="text-align: left;"><code dir="ltr" translate="no">       FALSE      </code></td>
</tr>
<tr class="odd">
<td style="text-align: left;"><code dir="ltr" translate="no">       NULL      </code></td>
<td style="text-align: left;"><code dir="ltr" translate="no">       TRUE      </code></td>
<td style="text-align: left;"><code dir="ltr" translate="no">       NULL      </code></td>
</tr>
<tr class="even">
<td style="text-align: left;"><code dir="ltr" translate="no">       ABSENT      </code></td>
<td style="text-align: left;"><code dir="ltr" translate="no">       TRUE      </code></td>
<td style="text-align: left;"><code dir="ltr" translate="no">       NULL      </code></td>
</tr>
<tr class="odd">
<td style="text-align: left;"><code dir="ltr" translate="no">       NULL      </code></td>
<td style="text-align: left;"><code dir="ltr" translate="no">       FALSE      </code></td>
<td style="text-align: left;"><code dir="ltr" translate="no">       FALSE      </code></td>
</tr>
<tr class="even">
<td style="text-align: left;"><code dir="ltr" translate="no">       FALSE      </code></td>
<td style="text-align: left;"><code dir="ltr" translate="no">       ABSENT      </code></td>
<td style="text-align: left;"><code dir="ltr" translate="no">       FALSE      </code></td>
</tr>
</tbody>
</table>

##### Node.js

``` javascript
const result = await db.pipeline()
  .collection("books")
  .select(
    and(field("rating").greaterThan(4), field("price").lessThan(10))
      .as("under10Recommendation")
  )
  .execute();test.firestore.js
```

### Web

``` javascript
const result = await execute(db.pipeline()
  .collection("books")
  .select(
    and(field("rating").greaterThan(4), field("price").lessThan(10))
      .as("under10Recommendation")
  )
);test.firestore.js
```

##### Swift

``` swift
let result = try await db.pipeline()
  .collection("books")
  .select([
    (Field("rating").greaterThan(4) && Field("price").lessThan(10))
      .as("under10Recommendation")
  ])
  .execute()PipelineSnippets.swift
```

##### Kotlin  
Android

``` kotlin
val result = db.pipeline()
    .collection("books")
    .select(
        Expression.and(field("rating").greaterThan(4),
          field("price").lessThan(10))
            .alias("under10Recommendation")
    )
    .execute()DocSnippets.kt
```

##### Java  
Android

``` text
Task<Pipeline.Snapshot> result = db.pipeline()
    .collection("books")
    .select(
        Expression.and(
            field("rating").greaterThan(4),
            field("price").lessThan(10)
        ).alias("under10Recommendation")
    )
    .execute();DocSnippets.java
```

##### Python

``` python
from google.cloud.firestore_v1.pipeline_expressions import Field, And

result = (
    client.pipeline()
    .collection("books")
    .select(
        And(
            Field.of("rating").greater_than(4), Field.of("price").less_than(10)
        ).as_("under10Recommendation")
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
            and(greaterThan(field("rating"), 4), lessThan(field("price"), 10))
                .as("under10Recommendation"))
        .execute()
        .get();PipelineSnippets.java
```

### OR

**Syntax:**

``` text
or(x: BOOLEAN...) -> BOOLEAN
```

**Description:**

Returns the logical OR of two or more boolean values.

Returns `  NULL  ` if the result can't be derived due to any of the given values being `  ABSENT  ` or `  NULL  ` .

**Examples:**

<table>
<thead>
<tr class="header">
<th style="text-align: left;"><code dir="ltr" translate="no">       x      </code></th>
<th style="text-align: left;"><code dir="ltr" translate="no">       y      </code></th>
<th style="text-align: left;"><code dir="ltr" translate="no">       or(x, y)      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;"><code dir="ltr" translate="no">       TRUE      </code></td>
<td style="text-align: left;"><code dir="ltr" translate="no">       TRUE      </code></td>
<td style="text-align: left;"><code dir="ltr" translate="no">       TRUE      </code></td>
</tr>
<tr class="even">
<td style="text-align: left;"><code dir="ltr" translate="no">       FALSE      </code></td>
<td style="text-align: left;"><code dir="ltr" translate="no">       TRUE      </code></td>
<td style="text-align: left;"><code dir="ltr" translate="no">       TRUE      </code></td>
</tr>
<tr class="odd">
<td style="text-align: left;"><code dir="ltr" translate="no">       NULL      </code></td>
<td style="text-align: left;"><code dir="ltr" translate="no">       TRUE      </code></td>
<td style="text-align: left;"><code dir="ltr" translate="no">       TRUE      </code></td>
</tr>
<tr class="even">
<td style="text-align: left;"><code dir="ltr" translate="no">       ABSENT      </code></td>
<td style="text-align: left;"><code dir="ltr" translate="no">       TRUE      </code></td>
<td style="text-align: left;"><code dir="ltr" translate="no">       TRUE      </code></td>
</tr>
<tr class="odd">
<td style="text-align: left;"><code dir="ltr" translate="no">       NULL      </code></td>
<td style="text-align: left;"><code dir="ltr" translate="no">       FALSE      </code></td>
<td style="text-align: left;"><code dir="ltr" translate="no">       NULL      </code></td>
</tr>
<tr class="even">
<td style="text-align: left;"><code dir="ltr" translate="no">       FALSE      </code></td>
<td style="text-align: left;"><code dir="ltr" translate="no">       ABSENT      </code></td>
<td style="text-align: left;"><code dir="ltr" translate="no">       NULL      </code></td>
</tr>
</tbody>
</table>

##### Node.js

``` javascript
const result = await db.pipeline()
  .collection("books")
  .select(
    or(field("genre").equal("Fantasy"), field("tags").arrayContains("adventure"))
      .as("matchesSearchFilters")
  )
  .execute();test.firestore.js
```

### Web

``` javascript
const result = await execute(db.pipeline()
  .collection("books")
  .select(
    or(field("genre").equal("Fantasy"), field("tags").arrayContains("adventure"))
      .as("matchesSearchFilters")
  )
);test.firestore.js
```

##### Swift

``` swift
let result = try await db.pipeline()
  .collection("books")
  .select([
    (Field("genre").equal("Fantasy") || Field("tags").arrayContains("adventure"))
      .as("matchesSearchFilters")
  ])
  .execute()PipelineSnippets.swift
```

##### Kotlin  
Android

``` kotlin
val result = db.pipeline()
    .collection("books")
    .select(
        Expression.or(field("genre").equal("Fantasy"),
          field("tags").arrayContains("adventure"))
            .alias("matchesSearchFilters")
    )
    .execute()DocSnippets.kt
```

##### Java  
Android

``` text
Task<Pipeline.Snapshot> result = db.pipeline()
    .collection("books")
    .select(
        Expression.or(
            field("genre").equal("Fantasy"),
            field("tags").arrayContains("adventure")
        ).alias("matchesSearchFilters")
    )
    .execute();DocSnippets.java
```

##### Python

``` python
from google.cloud.firestore_v1.pipeline_expressions import Field, And, Or

result = (
    client.pipeline()
    .collection("books")
    .select(
        Or(
            Field.of("genre").equal("Fantasy"),
            Field.of("tags").array_contains("adventure"),
        ).as_("matchesSearchFilters")
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
            or(equal(field("genre"), "Fantasy"), arrayContains(field("tags"), "adventure"))
                .as("matchesSearchFilters"))
        .execute()
        .get();PipelineSnippets.java
```

### XOR

**Syntax:**

``` text
xor(x: BOOLEAN...) -> BOOLEAN
```

**Description:**

Returns the logical XOR of two or more boolean values.

Returns `  NULL  ` if any of the given values are `  ABSENT  ` or `  NULL  ` .

**Examples:**

<table>
<thead>
<tr class="header">
<th style="text-align: left;"><code dir="ltr" translate="no">       x      </code></th>
<th style="text-align: left;"><code dir="ltr" translate="no">       y      </code></th>
<th style="text-align: left;"><code dir="ltr" translate="no">       xor(x, y)      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;"><code dir="ltr" translate="no">       TRUE      </code></td>
<td style="text-align: left;"><code dir="ltr" translate="no">       TRUE      </code></td>
<td style="text-align: left;"><code dir="ltr" translate="no">       FALSE      </code></td>
</tr>
<tr class="even">
<td style="text-align: left;"><code dir="ltr" translate="no">       FALSE      </code></td>
<td style="text-align: left;"><code dir="ltr" translate="no">       FALSE      </code></td>
<td style="text-align: left;"><code dir="ltr" translate="no">       FALSE      </code></td>
</tr>
<tr class="odd">
<td style="text-align: left;"><code dir="ltr" translate="no">       FALSE      </code></td>
<td style="text-align: left;"><code dir="ltr" translate="no">       TRUE      </code></td>
<td style="text-align: left;"><code dir="ltr" translate="no">       TRUE      </code></td>
</tr>
<tr class="even">
<td style="text-align: left;"><code dir="ltr" translate="no">       NULL      </code></td>
<td style="text-align: left;"><code dir="ltr" translate="no">       TRUE      </code></td>
<td style="text-align: left;"><code dir="ltr" translate="no">       NULL      </code></td>
</tr>
<tr class="odd">
<td style="text-align: left;"><code dir="ltr" translate="no">       ABSENT      </code></td>
<td style="text-align: left;"><code dir="ltr" translate="no">       TRUE      </code></td>
<td style="text-align: left;"><code dir="ltr" translate="no">       NULL      </code></td>
</tr>
<tr class="even">
<td style="text-align: left;"><code dir="ltr" translate="no">       NULL      </code></td>
<td style="text-align: left;"><code dir="ltr" translate="no">       FALSE      </code></td>
<td style="text-align: left;"><code dir="ltr" translate="no">       NULL      </code></td>
</tr>
<tr class="odd">
<td style="text-align: left;"><code dir="ltr" translate="no">       FALSE      </code></td>
<td style="text-align: left;"><code dir="ltr" translate="no">       ABSENT      </code></td>
<td style="text-align: left;"><code dir="ltr" translate="no">       NULL      </code></td>
</tr>
</tbody>
</table>

##### Node.js

``` javascript
const result = await execute(db.pipeline()
  .collection("books")
  .select(
    xor(field("tags").arrayContains("magic"), field("tags").arrayContains("nonfiction"))
      .as("matchesSearchFilters")
  )
);test.firestore.js
```

### Web

``` javascript
const result = await execute(db.pipeline()
  .collection("books")
  .select(
    xor(field("tags").arrayContains("magic"), field("tags").arrayContains("nonfiction"))
      .as("matchesSearchFilters")
  )
);test.firestore.js
```

##### Swift

``` swift
let result = try await db.pipeline()
  .collection("books")
  .select([
    (Field("tags").arrayContains("magic") ^ Field("tags").arrayContains("nonfiction"))
      .as("matchesSearchFilters")
  ])
  .execute()PipelineSnippets.swift
```

##### Kotlin  
Android

``` kotlin
val result = db.pipeline()
    .collection("books")
    .select(
        Expression.xor(field("tags").arrayContains("magic"),
          field("tags").arrayContains("nonfiction"))
            .alias("matchesSearchFilters")
    )
    .execute()DocSnippets.kt
```

##### Java  
Android

``` text
Task<Pipeline.Snapshot> result = db.pipeline()
    .collection("books")
    .select(
        Expression.xor(
            field("tags").arrayContains("magic"),
            field("tags").arrayContains("nonfiction")
        ).alias("matchesSearchFilters")
    )
    .execute();DocSnippets.java
```

##### Python

``` python
from google.cloud.firestore_v1.pipeline_expressions import Field, Xor

result = (
    client.pipeline()
    .collection("books")
    .select(
        Xor(
            [
                Field.of("tags").array_contains("magic"),
                Field.of("tags").array_contains("nonfiction"),
            ]
        ).as_("matchesSearchFilters")
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
            xor(
                    arrayContains(field("tags"), "magic"),
                    arrayContains(field("tags"), "nonfiction"))
                .as("matchesSearchFilters"))
        .execute()
        .get();PipelineSnippets.java
```

### NOT

**Syntax:**

``` text
not(x: BOOLEAN) -> BOOLEAN
```

**Description:**

Returns the logical NOT of a boolean value.

##### Node.js

``` javascript
const result = await execute(db.pipeline()
  .collection("books")
  .select(
    field("tags").arrayContains("nonfiction").not()
      .as("isFiction")
  )
);test.firestore.js
```

### Web

``` javascript
const result = await execute(db.pipeline()
  .collection("books")
  .select(
    field("tags").arrayContains("nonfiction").not()
      .as("isFiction")
  )
);test.firestore.js
```

##### Swift

``` swift
let result = try await db.pipeline()
  .collection("books")
  .select([
    (!Field("tags").arrayContains("nonfiction"))
      .as("isFiction")
  ])
  .execute()PipelineSnippets.swift
```

##### Kotlin  
Android

``` kotlin
val result = db.pipeline()
    .collection("books")
    .select(
        Expression.not(
            field("tags").arrayContains("nonfiction")
        ).alias("isFiction")
    )
    .execute()DocSnippets.kt
```

##### Java  
Android

``` text
Task<Pipeline.Snapshot> result = db.pipeline()
    .collection("books")
    .select(
        Expression.not(
            field("tags").arrayContains("nonfiction")
        ).alias("isFiction")
    )
    .execute();DocSnippets.java
```

##### Python

``` python
from google.cloud.firestore_v1.pipeline_expressions import Field, Not

result = (
    client.pipeline()
    .collection("books")
    .select(Not(Field.of("tags").array_contains("nonfiction")).as_("isFiction"))
    .execute()
)firestore_pipelines.py
```

##### Java

``` java
Pipeline.Snapshot result =
    firestore
        .pipeline()
        .collection("books")
        .select(not(arrayContains(field("tags"), "nonfiction")).as("isFiction"))
        .execute()
        .get();PipelineSnippets.java
```

### CONDITIONAL

**Syntax:**

``` text
conditional(condition: BOOLEAN, true_case: ANY, false_case: ANY) -> ANY
```

**Description:**

Evaluates and returns the `  true_case  ` if the `  condition  ` evaluates to `  TRUE  ` .

Evaluates and returns the `  false_case  ` if the condition resolves to `  FALSE  ` , `  NULL  ` , or an `  ABSENT  ` value.

**Examples:**

<table>
<thead>
<tr class="header">
<th style="text-align: left;"><code dir="ltr" translate="no">       condition      </code></th>
<th style="text-align: left;"><code dir="ltr" translate="no">       true_case      </code></th>
<th style="text-align: left;"><code dir="ltr" translate="no">       false_case      </code></th>
<th style="text-align: left;"><code dir="ltr" translate="no">       conditional(condition, true_case, false_case)      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;"><code dir="ltr" translate="no">       TRUE      </code></td>
<td style="text-align: left;">1L</td>
<td style="text-align: left;">0L</td>
<td style="text-align: left;">1L</td>
</tr>
<tr class="even">
<td style="text-align: left;"><code dir="ltr" translate="no">       FALSE      </code></td>
<td style="text-align: left;">1L</td>
<td style="text-align: left;">0L</td>
<td style="text-align: left;">0L</td>
</tr>
<tr class="odd">
<td style="text-align: left;"><code dir="ltr" translate="no">       NULL      </code></td>
<td style="text-align: left;">1L</td>
<td style="text-align: left;">0L</td>
<td style="text-align: left;">0L</td>
</tr>
<tr class="even">
<td style="text-align: left;"><code dir="ltr" translate="no">       ABSENT      </code></td>
<td style="text-align: left;">1L</td>
<td style="text-align: left;">0L</td>
<td style="text-align: left;">0L</td>
</tr>
</tbody>
</table>

##### Node.js

``` javascript
const result = await execute(db.pipeline()
  .collection("books")
  .select(
    field("tags").arrayConcat([
      field("pages").greaterThan(100)
        .conditional(constant("longRead"), constant("shortRead"))
    ]).as("extendedTags")
  )
);test.firestore.js
```

### Web

``` javascript
const result = await execute(db.pipeline()
  .collection("books")
  .select(
    field("tags").arrayConcat([
      field("pages").greaterThan(100)
        .conditional(constant("longRead"), constant("shortRead"))
    ]).as("extendedTags")
  )
);test.firestore.js
```

##### Swift

``` swift
let result = try await db.pipeline()
  .collection("books")
  .select([
    Field("tags").arrayConcat([
      ConditionalExpression(
        Field("pages").greaterThan(100),
        then: Constant("longRead"),
        else: Constant("shortRead")
      )
    ]).as("extendedTags")
  ])
  .execute()PipelineSnippets.swift
```

##### Kotlin  
Android

``` kotlin
val result = db.pipeline()
    .collection("books")
    .select(
        field("tags").arrayConcat(
            Expression.conditional(
                field("pages").greaterThan(100),
                constant("longRead"),
                constant("shortRead")
            )
        ).alias("extendedTags")
    )
    .execute()DocSnippets.kt
```

##### Java  
Android

``` text
Task<Pipeline.Snapshot> result = db.pipeline()
    .collection("books")
    .select(
        field("tags").arrayConcat(
            Expression.conditional(
                field("pages").greaterThan(100),
                constant("longRead"),
                constant("shortRead")
            )
        ).alias("extendedTags")
    )
    .execute();DocSnippets.java
```

##### Python

``` python
from google.cloud.firestore_v1.pipeline_expressions import (
    Field,
    Constant,
    Conditional,
)

result = (
    client.pipeline()
    .collection("books")
    .select(
        Field.of("tags")
        .array_concat(
            Conditional(
                Field.of("pages").greater_than(100),
                Constant.of("longRead"),
                Constant.of("shortRead"),
            )
        )
        .as_("extendedTags")
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
            arrayConcat(
                    field("tags"),
                    conditional(
                        greaterThan(field("pages"), 100),
                        constant("longRead"),
                        constant("shortRead")))
                .as("extendedTags"))
        .execute()
        .get();PipelineSnippets.java
```

### EQUAL\_ANY

**Syntax:**

``` text
equal_any(value: ANY, search_space: ARRAY) -> BOOLEAN
```

**Description:**

Returns `  TRUE  ` if `  value  ` is in the `  search_space  ` array.

**Examples:**

<table>
<thead>
<tr class="header">
<th style="text-align: left;"><code dir="ltr" translate="no">       value      </code></th>
<th style="text-align: left;"><code dir="ltr" translate="no">       search_space      </code></th>
<th style="text-align: left;"><code dir="ltr" translate="no">       equal_any(value, search_space)      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">0L</td>
<td style="text-align: left;">[1L, 2L, 3L]</td>
<td style="text-align: left;"><code dir="ltr" translate="no">       FALSE      </code></td>
</tr>
<tr class="even">
<td style="text-align: left;">2L</td>
<td style="text-align: left;">[1L, 2L, 3L]</td>
<td style="text-align: left;"><code dir="ltr" translate="no">       TRUE      </code></td>
</tr>
<tr class="odd">
<td style="text-align: left;"><code dir="ltr" translate="no">       NULL      </code></td>
<td style="text-align: left;">[1L, 2L, 3L]</td>
<td style="text-align: left;"><code dir="ltr" translate="no">       FALSE      </code></td>
</tr>
<tr class="even">
<td style="text-align: left;"><code dir="ltr" translate="no">       NULL      </code></td>
<td style="text-align: left;">[1L, <code dir="ltr" translate="no">       NULL      </code> ]</td>
<td style="text-align: left;"><code dir="ltr" translate="no">       TRUE      </code></td>
</tr>
<tr class="odd">
<td style="text-align: left;"><code dir="ltr" translate="no">       ABSENT      </code></td>
<td style="text-align: left;">[1L, <code dir="ltr" translate="no">       NULL      </code> ]</td>
<td style="text-align: left;"><code dir="ltr" translate="no">       FALSE      </code></td>
</tr>
<tr class="even">
<td style="text-align: left;">NaN</td>
<td style="text-align: left;">[1L, NaN, 3L]</td>
<td style="text-align: left;"><code dir="ltr" translate="no">       TRUE      </code></td>
</tr>
</tbody>
</table>

##### Node.js

``` javascript
const result = await execute(db.pipeline()
  .collection("books")
  .select(
    field("genre").equalAny(["Science Fiction", "Psychological Thriller"])
      .as("matchesGenreFilters")
  )
);test.firestore.js
```

### Web

``` javascript
const result = await execute(db.pipeline()
  .collection("books")
  .select(
    field("genre").equalAny(["Science Fiction", "Psychological Thriller"])
      .as("matchesGenreFilters")
  )
);test.firestore.js
```

##### Swift

``` swift
let result = try await db.pipeline()
  .collection("books")
  .select([
    Field("genre").equalAny(["Science Fiction", "Psychological Thriller"])
      .as("matchesGenreFilters")
  ])
  .execute()PipelineSnippets.swift
```

##### Kotlin  
Android

``` kotlin
val result = db.pipeline()
    .collection("books")
    .select(
        field("genre").equalAny(listOf("Science Fiction", "Psychological Thriller"))
            .alias("matchesGenreFilters")
    )
    .execute()DocSnippets.kt
```

##### Java  
Android

``` text
Task<Pipeline.Snapshot> result = db.pipeline()
    .collection("books")
    .select(
        field("genre").equalAny(Arrays.asList("Science Fiction", "Psychological Thriller"))
            .alias("matchesGenreFilters")
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
        .equal_any(["Science Fiction", "Psychological Thriller"])
        .as_("matchesGenreFilters")
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
            equalAny(field("genre"), Arrays.asList("Science Fiction", "Psychological Thriller"))
                .as("matchesGenreFilters"))
        .execute()
        .get();PipelineSnippets.java
```

### NOT\_EQUAL\_ANY

**Syntax:**

``` text
not_equal_any(value: ANY, search_space: ARRAY) -> BOOLEAN
```

**Description:**

Returns `  TRUE  ` if `  value  ` is not in the `  search_space  ` array.

**Examples:**

<table>
<thead>
<tr class="header">
<th style="text-align: left;"><code dir="ltr" translate="no">       value      </code></th>
<th style="text-align: left;"><code dir="ltr" translate="no">       search_space      </code></th>
<th style="text-align: left;"><code dir="ltr" translate="no">       not_equal_any(value, search_space)      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">0L</td>
<td style="text-align: left;">[1L, 2L, 3L]</td>
<td style="text-align: left;"><code dir="ltr" translate="no">       TRUE      </code></td>
</tr>
<tr class="even">
<td style="text-align: left;">2L</td>
<td style="text-align: left;">[1L, 2L, 3L]</td>
<td style="text-align: left;"><code dir="ltr" translate="no">       FALSE      </code></td>
</tr>
<tr class="odd">
<td style="text-align: left;"><code dir="ltr" translate="no">       NULL      </code></td>
<td style="text-align: left;">[1L, 2L, 3L]</td>
<td style="text-align: left;"><code dir="ltr" translate="no">       TRUE      </code></td>
</tr>
<tr class="even">
<td style="text-align: left;"><code dir="ltr" translate="no">       NULL      </code></td>
<td style="text-align: left;">[1L, <code dir="ltr" translate="no">       NULL      </code> ]</td>
<td style="text-align: left;"><code dir="ltr" translate="no">       FALSE      </code></td>
</tr>
<tr class="odd">
<td style="text-align: left;"><code dir="ltr" translate="no">       ABSENT      </code></td>
<td style="text-align: left;">[1L, <code dir="ltr" translate="no">       NULL      </code> ]</td>
<td style="text-align: left;"><code dir="ltr" translate="no">       TRUE      </code></td>
</tr>
<tr class="even">
<td style="text-align: left;">NaN</td>
<td style="text-align: left;">[1L, NaN, 3L]</td>
<td style="text-align: left;"><code dir="ltr" translate="no">       FALSE      </code></td>
</tr>
</tbody>
</table>

##### Node.js

``` javascript
const result = await execute(db.pipeline()
  .collection("books")
  .select(
    field("author").notEqualAny(["George Orwell", "F. Scott Fitzgerald"])
      .as("byExcludedAuthors")
  )
);test.firestore.js
```

### Web

``` javascript
const result = await execute(db.pipeline()
  .collection("books")
  .select(
    field("author").notEqualAny(["George Orwell", "F. Scott Fitzgerald"])
      .as("byExcludedAuthors")
  )
);test.firestore.js
```

##### Swift

``` swift
let result = try await db.pipeline()
  .collection("books")
  .select([
    Field("author").notEqualAny(["George Orwell", "F. Scott Fitzgerald"])
      .as("byExcludedAuthors")
  ])
  .execute()PipelineSnippets.swift
```

##### Kotlin  
Android

``` kotlin
val result = db.pipeline()
    .collection("books")
    .select(
        field("author").notEqualAny(listOf("George Orwell", "F. Scott Fitzgerald"))
            .alias("byExcludedAuthors")
    )
    .execute()DocSnippets.kt
```

##### Java  
Android

``` text
Task<Pipeline.Snapshot> result = db.pipeline()
    .collection("books")
    .select(
        field("author").notEqualAny(Arrays.asList("George Orwell", "F. Scott Fitzgerald"))
            .alias("byExcludedAuthors")
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
        Field.of("author")
        .not_equal_any(["George Orwell", "F. Scott Fitzgerald"])
        .as_("byExcludedAuthors")
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
            notEqualAny(field("author"), Arrays.asList("George Orwell", "F. Scott Fitzgerald"))
                .as("byExcludedAuthors"))
        .execute()
        .get();PipelineSnippets.java
```

### MAXIMUM

**Syntax:**

``` text
maximum(x: ANY...) -> ANY
maximum(x: ARRAY) -> ANY
```

**Description:**

Returns the maximum non- `  NULL  ` , non- `  ABSENT  ` value in a series of values `  x  ` .

If there are no non- `  NULL  ` , non- `  ABSENT  ` values, `  NULL  ` is returned.

If there are multiple maximum equivalent values, any one of those values can be returned. Value type ordering follows [documented ordering](/firestore/docs/concepts/data-types#value_type_ordering) .

**Examples:**

<table>
<thead>
<tr class="header">
<th style="text-align: left;"><code dir="ltr" translate="no">       x      </code></th>
<th style="text-align: left;"><code dir="ltr" translate="no">       y      </code></th>
<th style="text-align: left;"><code dir="ltr" translate="no">       maximum(x, y)      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;"><code dir="ltr" translate="no">       FALSE      </code></td>
<td style="text-align: left;"><code dir="ltr" translate="no">       TRUE      </code></td>
<td style="text-align: left;"><code dir="ltr" translate="no">       TRUE      </code></td>
</tr>
<tr class="even">
<td style="text-align: left;"><code dir="ltr" translate="no">       FALSE      </code></td>
<td style="text-align: left;">-10L</td>
<td style="text-align: left;">-10L</td>
</tr>
<tr class="odd">
<td style="text-align: left;">0.0</td>
<td style="text-align: left;">-5L</td>
<td style="text-align: left;">0.0</td>
</tr>
<tr class="even">
<td style="text-align: left;">"foo"</td>
<td style="text-align: left;">"bar"</td>
<td style="text-align: left;">"foo"</td>
</tr>
<tr class="odd">
<td style="text-align: left;">"foo"</td>
<td style="text-align: left;">["foo"]</td>
<td style="text-align: left;">["foo"]</td>
</tr>
<tr class="even">
<td style="text-align: left;"><code dir="ltr" translate="no">       ABSENT      </code></td>
<td style="text-align: left;"><code dir="ltr" translate="no">       ABSENT      </code></td>
<td style="text-align: left;"><code dir="ltr" translate="no">       NULL      </code></td>
</tr>
<tr class="odd">
<td style="text-align: left;"><code dir="ltr" translate="no">       NULL      </code></td>
<td style="text-align: left;"><code dir="ltr" translate="no">       NULL      </code></td>
<td style="text-align: left;"><code dir="ltr" translate="no">       NULL      </code></td>
</tr>
</tbody>
</table>

##### Node.js

``` javascript
const result = await execute(db.pipeline()
  .collection("books")
  .aggregate(field("price").maximum().as("maximumPrice"))
);test.firestore.js
```

### Web

``` javascript
const result = await execute(db.pipeline()
  .collection("books")
  .aggregate(field("price").maximum().as("maximumPrice"))
);test.firestore.js
```

##### Swift

``` swift
let result = try await db.pipeline()
  .collection("books")
  .select([
    Field("rating").logicalMaximum([1]).as("flooredRating")
  ])
  .execute()PipelineSnippets.swift
```

##### Kotlin  
Android

``` kotlin
val result = db.pipeline()
    .collection("books")
    .select(
        field("rating").logicalMaximum(1).alias("flooredRating")
    )
    .execute()DocSnippets.kt
```

##### Java  
Android

``` text
Task<Pipeline.Snapshot> result = db.pipeline()
    .collection("books")
    .select(
        field("rating").logicalMaximum(1).alias("flooredRating")
    )
    .execute();DocSnippets.java
```

##### Python

``` python
from google.cloud.firestore_v1.pipeline_expressions import Field

result = (
    client.pipeline()
    .collection("books")
    .select(Field.of("rating").logical_maximum(1).as_("flooredRating"))
    .execute()
)firestore_pipelines.py
```

##### Java

``` java
Pipeline.Snapshot result =
    firestore
        .pipeline()
        .collection("books")
        .select(logicalMaximum(field("rating"), 1).as("flooredRating"))
        .execute()
        .get();PipelineSnippets.java
```

### MINIMUM

**Syntax:**

``` text
minimum(x: ANY...) -> ANY
minimum(x: ARRAY) -> ANY
```

**Description:**

Returns the minimum non- `  NULL  ` , non- `  ABSENT  ` value in a series of values `  x  ` .

If there are no non- `  NULL  ` , non- `  ABSENT  ` values, `  NULL  ` is returned.

If there are multiple minimum equivalent values, any one of those values can be returned. Value type ordering follows [documented ordering](/firestore/docs/concepts/data-types#value_type_ordering) .

**Examples:**

<table>
<thead>
<tr class="header">
<th style="text-align: left;"><code dir="ltr" translate="no">       x      </code></th>
<th style="text-align: left;"><code dir="ltr" translate="no">       y      </code></th>
<th style="text-align: left;"><code dir="ltr" translate="no">       minimum(x, y)      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;"><code dir="ltr" translate="no">       FALSE      </code></td>
<td style="text-align: left;"><code dir="ltr" translate="no">       TRUE      </code></td>
<td style="text-align: left;"><code dir="ltr" translate="no">       FALSE      </code></td>
</tr>
<tr class="even">
<td style="text-align: left;"><code dir="ltr" translate="no">       FALSE      </code></td>
<td style="text-align: left;">-10L</td>
<td style="text-align: left;"><code dir="ltr" translate="no">       FALSE      </code></td>
</tr>
<tr class="odd">
<td style="text-align: left;">0.0</td>
<td style="text-align: left;">-5L</td>
<td style="text-align: left;">-5L</td>
</tr>
<tr class="even">
<td style="text-align: left;">"foo"</td>
<td style="text-align: left;">"bar"</td>
<td style="text-align: left;">"bar"</td>
</tr>
<tr class="odd">
<td style="text-align: left;">"foo"</td>
<td style="text-align: left;">["foo"]</td>
<td style="text-align: left;">"foo"</td>
</tr>
<tr class="even">
<td style="text-align: left;"><code dir="ltr" translate="no">       ABSENT      </code></td>
<td style="text-align: left;"><code dir="ltr" translate="no">       ABSENT      </code></td>
<td style="text-align: left;"><code dir="ltr" translate="no">       NULL      </code></td>
</tr>
<tr class="odd">
<td style="text-align: left;"><code dir="ltr" translate="no">       NULL      </code></td>
<td style="text-align: left;"><code dir="ltr" translate="no">       NULL      </code></td>
<td style="text-align: left;"><code dir="ltr" translate="no">       NULL      </code></td>
</tr>
</tbody>
</table>

##### Node.js

``` javascript
const result = await execute(db.pipeline()
  .collection("books")
  .aggregate(field("price").minimum().as("minimumPrice"))
);test.firestore.js
```

### Web

``` javascript
const result = await execute(db.pipeline()
  .collection("books")
  .aggregate(field("price").minimum().as("minimumPrice"))
);test.firestore.js
```

##### Swift

``` swift
let result = try await db.pipeline()
  .collection("books")
  .select([
    Field("rating").logicalMinimum([5]).as("cappedRating")
  ])
  .execute()PipelineSnippets.swift
```

##### Kotlin  
Android

``` kotlin
val result = db.pipeline()
    .collection("books")
    .select(
        field("rating").logicalMinimum(5).alias("cappedRating")
    )
    .execute()DocSnippets.kt
```

##### Java  
Android

``` text
Task<Pipeline.Snapshot> result = db.pipeline()
    .collection("books")
    .select(
        field("rating").logicalMinimum(5).alias("cappedRating")
    )
    .execute();DocSnippets.java
```

##### Python

``` python
from google.cloud.firestore_v1.pipeline_expressions import Field

result = (
    client.pipeline()
    .collection("books")
    .select(Field.of("rating").logical_minimum(5).as_("cappedRating"))
    .execute()
)firestore_pipelines.py
```

##### Java

``` java
Pipeline.Snapshot result =
    firestore
        .pipeline()
        .collection("books")
        .select(logicalMinimum(field("rating"), 5).as("cappedRating"))
        .execute()
        .get();PipelineSnippets.java
```

## What's next

  - See the [Pipeline Queries overview](/firestore/docs/pipeline/overview)
