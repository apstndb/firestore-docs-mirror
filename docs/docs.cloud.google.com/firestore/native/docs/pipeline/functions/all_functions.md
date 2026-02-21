# All Functions Reference

**Preview — Firestore in Native mode (with Pipeline Operations) for Enterprise Edition**

This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](/terms/service-terms#1) . You can process personal data for this feature as outlined in the [Cloud Data Processing Addendum](/terms/data-processing-addendum) , subject to the obligations and restrictions described in the agreement under which you access Google Cloud. Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

## **Aggregate**

All aggregate functions can be used as top-level expressions in the `  aggregate(...)  ` stage.

<table>
<tbody>
<tr class="odd">
<td>Name</td>
<td>Description</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         COUNT       </code></td>
<td>Returns the number of documents.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         COUNT_IF       </code></td>
<td>Returns the count of documents where an expression evaluates to <code dir="ltr" translate="no">       TRUE      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         COUNT_DISTINCT       </code></td>
<td>Returns the count of unique, non <code dir="ltr" translate="no">       NULL      </code> values</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         SUM       </code></td>
<td>Returns the sum of all <code dir="ltr" translate="no">       NUMERIC      </code> values</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         AVERAGE       </code></td>
<td>Returns the average of all <code dir="ltr" translate="no">       NUMERIC      </code> values</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         MINIMUM       </code></td>
<td>Returns the minimum non <code dir="ltr" translate="no">       NULL      </code> value</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         MAXIMUM       </code></td>
<td>Returns the maximum non <code dir="ltr" translate="no">       NULL      </code> value</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         FIRST       </code></td>
<td>Returns the <code dir="ltr" translate="no">       expression      </code> value for the first document.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         LAST       </code></td>
<td>Returns the <code dir="ltr" translate="no">       expression      </code> value for the last document.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         ARRAY_AGG       </code></td>
<td>Returns an array of all input values.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         ARRAY_AGG_DISTINCT       </code></td>
<td>Returns an array of all distinct input values.</td>
</tr>
</tbody>
</table>

### COUNT

**Syntax:**

``` text
count() -> INT64
count(expression: ANY) -> INT64
```

**Description:**

Returns the count of documents from the previous stage where `  expression  ` evaluates to any non- `  NULL  ` value. If no `  expression  ` is provided, returns the total count of documents from the previous stage.

##### Node.js

``` javascript
// Total number of books in the collection
const countOfAll = await db.pipeline()
  .collection("books")
  .aggregate(countAll().as("count"))
  .execute();

// Number of books with nonnull `ratings` field
const countField = await db.pipeline()
  .collection("books")
  .aggregate(field("ratings").count().as("count"))
  .execute();test.firestore.js
```

### Web

``` javascript
// Total number of books in the collection
const countOfAll = await execute(db.pipeline()
  .collection("books")
  .aggregate(countAll().as("count"))
);

// Number of books with nonnull `ratings` field
const countField = await execute(db.pipeline()
  .collection("books")
  .aggregate(field("ratings").count().as("count"))
);test.firestore.js
```

##### Swift

``` swift
// Total number of books in the collection
let countAll = try await db.pipeline()
  .collection("books")
  .aggregate([CountAll().as("count")])
  .execute()

// Number of books with nonnull `ratings` field
let countField = try await db.pipeline()
  .collection("books")
  .aggregate([Field("ratings").count().as("count")])
  .execute()PipelineSnippets.swift
```

##### Kotlin  
Android

``` kotlin
// Total number of books in the collection
val countAll = db.pipeline()
    .collection("books")
    .aggregate(AggregateFunction.countAll().alias("count"))
    .execute()

// Number of books with nonnull `ratings` field
val countField = db.pipeline()
    .collection("books")
    .aggregate(AggregateFunction.count("ratings").alias("count"))
    .execute()DocSnippets.kt
```

##### Java  
Android

``` text
// Total number of books in the collection
Task<Pipeline.Snapshot> countAll = db.pipeline()
    .collection("books")
    .aggregate(AggregateFunction.countAll().alias("count"))
    .execute();

// Number of books with nonnull `ratings` field
Task<Pipeline.Snapshot> countField = db.pipeline()
    .collection("books")
    .aggregate(AggregateFunction.count("ratings").alias("count"))
    .execute();DocSnippets.java
```

##### Python

``` python
from google.cloud.firestore_v1.pipeline_expressions import Count

# Total number of books in the collection
count_all = (
    client.pipeline().collection("books").aggregate(Count().as_("count")).execute()
)

# Number of books with nonnull `ratings` field
count_field = (
    client.pipeline()
    .collection("books")
    .aggregate(Count("ratings").as_("count"))
    .execute()
)firestore_pipelines.py
```

##### Java

``` java
// Total number of books in the collection
Pipeline.Snapshot countAll =
    firestore.pipeline().collection("books").aggregate(countAll().as("count")).execute().get();

// Number of books with nonnull `ratings` field
Pipeline.Snapshot countField =
    firestore
        .pipeline()
        .collection("books")
        .aggregate(count("ratings").as("count"))
        .execute()
        .get();PipelineSnippets.java
```

### COUNT\_IF

**Syntax:**

``` text
count_if(expression: BOOLEAN) -> INT64
```

**Description:**

Returns the number of documents from the previous stage where `  expression  ` evaluates to `  TRUE  ` .

##### Node.js

``` javascript
const result = await db.pipeline()
  .collection("books")
  .aggregate(
    field("rating").greaterThan(4).countIf().as("filteredCount")
  )
  .execute();test.firestore.js
```

### Web

``` javascript
const result = await execute(db.pipeline()
  .collection("books")
  .aggregate(
    field("rating").greaterThan(4).countIf().as("filteredCount")
  )
);test.firestore.js
```

##### Swift

``` swift
let result = try await db.pipeline()
  .collection("books")
  .aggregate([
    AggregateFunction("count_if", [Field("rating").greaterThan(4)]).as("filteredCount")
  ])
  .execute()PipelineSnippets.swift
```

##### Kotlin  
Android

``` kotlin
val result = db.pipeline()
    .collection("books")
    .aggregate(
        AggregateFunction.countIf(field("rating").greaterThan(4)).alias("filteredCount")
    )
    .execute()DocSnippets.kt
```

##### Java  
Android

``` text
Task<Pipeline.Snapshot> result = db.pipeline()
    .collection("books")
    .aggregate(
        AggregateFunction.countIf(field("rating").greaterThan(4)).alias("filteredCount")
    )
    .execute();DocSnippets.java
```

##### Python

``` python
from google.cloud.firestore_v1.pipeline_expressions import Field

result = (
    client.pipeline()
    .collection("books")
    .aggregate(Field.of("rating").greater_than(4).count_if().as_("filteredCount"))
    .execute()
)firestore_pipelines.py
```

##### Java

``` java
Pipeline.Snapshot result =
    firestore
        .pipeline()
        .collection("books")
        .aggregate(countIf(field("rating").greaterThan(4)).as("filteredCount"))
        .execute()
        .get();PipelineSnippets.java
```

### COUNT\_DISTINCT

**Syntax:**

``` text
count_distinct(expression: ANY) -> INT64
```

**Description:**

Returns the number of unique non- `  NULL  ` , non- `  ABSENT  ` values of `  expression  ` .

##### Node.js

``` javascript
const result = await db.pipeline()
  .collection("books")
  .aggregate(field("author").countDistinct().as("unique_authors"))
  .execute();test.firestore.js
```

### Web

``` javascript
const result = await execute(db.pipeline()
  .collection("books")
  .aggregate(field("author").countDistinct().as("unique_authors"))
);test.firestore.js
```

##### Swift

``` swift
let result = try await db.pipeline()
  .collection("books")
  .aggregate([AggregateFunction("count_distinct", [Field("author")]).as("unique_authors")])
  .execute()PipelineSnippets.swift
```

##### Kotlin  
Android

``` kotlin
val result = db.pipeline()
    .collection("books")
    .aggregate(AggregateFunction.countDistinct("author").alias("unique_authors"))
    .execute()DocSnippets.kt
```

##### Java  
Android

``` text
Task<Pipeline.Snapshot> result = db.pipeline()
    .collection("books")
    .aggregate(AggregateFunction.countDistinct("author").alias("unique_authors"))
    .execute();DocSnippets.java
```

##### Python

``` python
from google.cloud.firestore_v1.pipeline_expressions import Field

result = (
    client.pipeline()
    .collection("books")
    .aggregate(Field.of("author").count_distinct().as_("unique_authors"))
    .execute()
)firestore_pipelines.py
```

##### Java

``` java
Pipeline.Snapshot result =
    firestore
        .pipeline()
        .collection("books")
        .aggregate(countDistinct("author").as("unique_authors"))
        .execute()
        .get();PipelineSnippets.java
```

### SUM

**Syntax:**

``` text
sum(expression: ANY) -> NUMBER
```

**Description:**

Returns the sum for all numerical values, ignoring non-numeric values. Returns `  NaN  ` if any values are `  NaN  ` .

The output will have the same type as the widest input type except in these cases:

  - An `  INTEGER  ` will be converted to a `  DOUBLE  ` if it cannot be represented as an `  INTEGER  ` .

##### Node.js

``` javascript
const result = await db.pipeline()
  .collection("cities")
  .aggregate(field("population").sum().as("totalPopulation"))
  .execute();test.firestore.js
```

### Web

``` javascript
const result = await execute(db.pipeline()
  .collection("cities")
  .aggregate(field("population").sum().as("totalPopulation"))
);test.firestore.js
```

##### Swift

``` swift
let result = try await db.pipeline()
  .collection("cities")
  .aggregate([Field("population").sum().as("totalPopulation")])
  .execute()PipelineSnippets.swift
```

##### Kotlin  
Android

``` kotlin
val result = db.pipeline()
    .collection("cities")
    .aggregate(AggregateFunction.sum("population").alias("totalPopulation"))
    .execute()DocSnippets.kt
```

##### Java  
Android

``` text
Task<Pipeline.Snapshot> result = db.pipeline()
    .collection("cities")
    .aggregate(AggregateFunction.sum("population").alias("totalPopulation"))
    .execute();DocSnippets.java
```

##### Python

``` python
from google.cloud.firestore_v1.pipeline_expressions import Field

result = (
    client.pipeline()
    .collection("cities")
    .aggregate(Field.of("population").sum().as_("totalPopulation"))
    .execute()
)firestore_pipelines.py
```

##### Java

``` java
Pipeline.Snapshot result =
    firestore
        .pipeline()
        .collection("cities")
        .aggregate(sum("population").as("totalPopulation"))
        .execute()
        .get();PipelineSnippets.java
```

### AVERAGE

**Syntax:**

``` text
average(expression: ANY) -> FLOAT64
```

**Description:**

Returns the average for all numerical values, ignoring non-numeric values. Evaluates to `  NaN  ` if any values are `  NaN  ` , or `  NULL  ` if no numerical values are aggregated.

The output will have the same type as the input type except in these cases:

  - An `  INTEGER  ` will be converted to a `  DOUBLE  ` if it cannot be represented as an `  INTEGER  ` .

##### Node.js

``` javascript
const result = await db.pipeline()
  .collection("cities")
  .aggregate(field("population").average().as("averagePopulation"))
  .execute();test.firestore.js
```

### Web

``` javascript
const result = await execute(db.pipeline()
  .collection("cities")
  .aggregate(field("population").average().as("averagePopulation"))
);test.firestore.js
```

##### Swift

``` swift
let result = try await db.pipeline()
  .collection("cities")
  .aggregate([Field("population").average().as("averagePopulation")])
  .execute()PipelineSnippets.swift
```

##### Kotlin  
Android

``` kotlin
val result = db.pipeline()
    .collection("cities")
    .aggregate(AggregateFunction.average("population").alias("averagePopulation"))
    .execute()DocSnippets.kt
```

##### Java  
Android

``` text
Task<Pipeline.Snapshot> result = db.pipeline()
    .collection("cities")
    .aggregate(AggregateFunction.average("population").alias("averagePopulation"))
    .execute();DocSnippets.java
```

##### Python

``` python
from google.cloud.firestore_v1.pipeline_expressions import Field

result = (
    client.pipeline()
    .collection("cities")
    .aggregate(Field.of("population").average().as_("averagePopulation"))
    .execute()
)firestore_pipelines.py
```

##### Java

``` java
Pipeline.Snapshot result =
    firestore
        .pipeline()
        .collection("cities")
        .aggregate(average("population").as("averagePopulation"))
        .execute()
        .get();PipelineSnippets.java
```

### MINIMUM

**Syntax:**

``` text
minimum(expression: ANY) -> ANY
```

**Description:**

Returns the minimum non- `  NULL  ` , non-absent value of the `  expression  ` when evaluated on each document.

If there are no non- `  NULL  ` , non-absent values, `  NULL  ` is returned. This includes when no documents are considered.

If there are multiple minimum equivalent values, any one of those values can be returned. Value type ordering follows [documented ordering](/docs/firestore/manage-data/data-types#value_type_ordering) .

##### Node.js

``` javascript
const result = await db.pipeline()
  .collection("books")
  .aggregate(field("price").minimum().as("minimumPrice"))
  .execute();test.firestore.js
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
  .aggregate([Field("price").minimum().as("minimumPrice")])
  .execute()PipelineSnippets.swift
```

##### Kotlin  
Android

``` kotlin
val result = db.pipeline()
    .collection("books")
    .aggregate(AggregateFunction.minimum("price").alias("minimumPrice"))
    .execute()DocSnippets.kt
```

##### Java  
Android

``` text
Task<Pipeline.Snapshot> result = db.pipeline()
    .collection("books")
    .aggregate(AggregateFunction.minimum("price").alias("minimumPrice"))
    .execute();DocSnippets.java
```

##### Python

``` python
from google.cloud.firestore_v1.pipeline_expressions import Field

result = (
    client.pipeline()
    .collection("books")
    .aggregate(Field.of("price").minimum().as_("minimumPrice"))
    .execute()
)firestore_pipelines.py
```

##### Java

``` java
Pipeline.Snapshot result =
    firestore
        .pipeline()
        .collection("books")
        .aggregate(minimum("price").as("minimumPrice"))
        .execute()
        .get();PipelineSnippets.java
```

### MAXIMUM

**Syntax:**

``` text
maximum(expression: ANY) -> ANY
```

**Description:**

Returns the maximum non- `  NULL  ` , non-absent value of the `  expression  ` when evaluated on each document.

If there are no non- `  NULL  ` , non-absent values, `  NULL  ` is returned. This includes when no documents are considered.

If there are multiple maximum equivalent values, any one of those values can be returned. Value type ordering follows [documented ordering](/docs/firestore/manage-data/data-types#value_type_ordering) .

##### Node.js

``` javascript
const result = await db.pipeline()
  .collection("books")
  .aggregate(field("price").maximum().as("maximumPrice"))
  .execute();test.firestore.js
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
  .aggregate([Field("price").maximum().as("maximumPrice")])
  .execute()PipelineSnippets.swift
```

##### Kotlin  
Android

``` kotlin
val result = db.pipeline()
    .collection("books")
    .aggregate(AggregateFunction.maximum("price").alias("maximumPrice"))
    .execute()DocSnippets.kt
```

##### Java  
Android

``` text
Task<Pipeline.Snapshot> result = db.pipeline()
    .collection("books")
    .aggregate(AggregateFunction.maximum("price").alias("maximumPrice"))
    .execute();DocSnippets.java
```

##### Python

``` python
from google.cloud.firestore_v1.pipeline_expressions import Field

result = (
    client.pipeline()
    .collection("books")
    .aggregate(Field.of("price").maximum().as_("maximumPrice"))
    .execute()
)firestore_pipelines.py
```

##### Java

``` java
Pipeline.Snapshot result =
    firestore
        .pipeline()
        .collection("books")
        .aggregate(maximum("price").as("maximumPrice"))
        .execute()
        .get();PipelineSnippets.java
```

### FIRST

**Syntax:**

``` text
first(expression: ANY) -> ANY
```

**Description:**

Returns the value of `  expression  ` for the first returned document.

### LAST

**Syntax:**

``` text
last(expression: ANY) -> ANY
```

**Description:**

Returns the value of `  expression  ` for the last returned document.

### ARRAY\_AGG

**Syntax:**

``` text
array_agg(expression: ANY) -> ARRAY<ANY>
```

**Description:**

Returns an array containing all values of `  expression  ` when evaluated on each document.

If the expression resolves to an absent value, it is converted to `  NULL  ` .

The order of elements in the output array is not stable and shouldn't be relied upon.

### ARRAY\_AGG\_DISTINCT

**Syntax:**

``` text
array_agg_distinct(expression: ANY) -> ARRAY<ANY>
```

**Description:**

Returns an array containing all distinct values of `  expression  ` when evaluated on each document.

If the expression resolves to an absent value, it is converted to `  NULL  ` .

The order of elements in the output array is not stable and shouldn't be relied upon.

## **Arithmetic Functions**

All arithmetic functions in Firestore have the following behaviors:

  - Evaluates to `  NULL  ` if any of the input parameters is `  NULL  ` .
  - Evaluates to `  NaN  ` if any of the arguments is `  NaN  ` .
  - Generates an error if an overflow or underflow occurs.

Additionally, when an arithmetic function takes multiple numeric arguments of different types (for example: `  add(5.0, 6)  ` ), Firestore implicitly converts arguments to the widest input type. If only `  INT32  ` inputs are provided, the return type will be `  INT64  ` .

<table>
<tbody>
<tr class="odd">
<td>Name</td>
<td>Description</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         ABS       </code></td>
<td>Returns the absolute value of a <code dir="ltr" translate="no">       number      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         ADD       </code></td>
<td>Returns the value of <code dir="ltr" translate="no">       x + y      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         SUBTRACT       </code></td>
<td>Returns the value of <code dir="ltr" translate="no">       x - y      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         MULTIPLY       </code></td>
<td>Returns the value of <code dir="ltr" translate="no">       x * y      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         DIVIDE       </code></td>
<td>Returns the value of <code dir="ltr" translate="no">       x / y      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         MOD       </code></td>
<td>Returns the remainder of the division of <code dir="ltr" translate="no">       x / y      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         CEIL       </code></td>
<td>Returns the ceiling of a <code dir="ltr" translate="no">       number      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         FLOOR       </code></td>
<td>Returns the floor of a <code dir="ltr" translate="no">       number      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         ROUND       </code></td>
<td>Rounds a <code dir="ltr" translate="no">       number      </code> to <code dir="ltr" translate="no">       places      </code> decimal places</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         POW       </code></td>
<td>Returns the value of <code dir="ltr" translate="no">       base^exponent      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         SQRT       </code></td>
<td>Returns the square root of a <code dir="ltr" translate="no">       number      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         EXP       </code></td>
<td>Returns Euler's number raised to the power of <code dir="ltr" translate="no">       exponent      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         LN       </code></td>
<td>Returns the natural logarithm of a <code dir="ltr" translate="no">       number      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         LOG       </code></td>
<td>Returns the logarithm of a <code dir="ltr" translate="no">       number      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         LOG10       </code></td>
<td>Returns the logarithm of a <code dir="ltr" translate="no">       number      </code> to base <code dir="ltr" translate="no">       10      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         RAND       </code></td>
<td>Returns a pseudo-random floating point number</td>
</tr>
</tbody>
</table>

### ABS

**Syntax:**

``` text
abs[N <: INT32 | INT64 | FLOAT64](number: N) -> N
```

**Description:**

Returns the absolute value of a `  number  ` .

  - Throws an error when the function would overflow an `  INT32  ` or `  INT64  ` value.

**Examples:**

<table>
<thead>
<tr class="header">
<th style="text-align: left;">number</th>
<th style="text-align: left;"><code dir="ltr" translate="no">       abs(number)      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">10</td>
<td style="text-align: left;">10</td>
</tr>
<tr class="even">
<td style="text-align: left;">-10</td>
<td style="text-align: left;">10</td>
</tr>
<tr class="odd">
<td style="text-align: left;">10L</td>
<td style="text-align: left;">10L</td>
</tr>
<tr class="even">
<td style="text-align: left;">-0.0</td>
<td style="text-align: left;">0.0</td>
</tr>
<tr class="odd">
<td style="text-align: left;">10.5</td>
<td style="text-align: left;">10.5</td>
</tr>
<tr class="even">
<td style="text-align: left;">-10.5</td>
<td style="text-align: left;">10.5</td>
</tr>
<tr class="odd">
<td style="text-align: left;">-2 <sup>31</sup></td>
<td style="text-align: left;"><code dir="ltr" translate="no">       [error]      </code></td>
</tr>
<tr class="even">
<td style="text-align: left;">-2 <sup>63</sup></td>
<td style="text-align: left;"><code dir="ltr" translate="no">       [error]      </code></td>
</tr>
</tbody>
</table>

### ADD

**Syntax:**

``` text
add[N <: INT32 | INT64 | FLOAT64](x: N, y: N) -> N
```

**Description:**

Returns the value of `  x + y  ` .

**Examples:**

<table>
<thead>
<tr class="header">
<th style="text-align: left;">x</th>
<th style="text-align: left;">y</th>
<th style="text-align: left;"><code dir="ltr" translate="no">       add(x, y)      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">20</td>
<td style="text-align: left;">3</td>
<td style="text-align: left;">23</td>
</tr>
<tr class="even">
<td style="text-align: left;">10.0</td>
<td style="text-align: left;">1</td>
<td style="text-align: left;">11.0</td>
</tr>
<tr class="odd">
<td style="text-align: left;">22.5</td>
<td style="text-align: left;">2.0</td>
<td style="text-align: left;">24.5</td>
</tr>
<tr class="even">
<td style="text-align: left;">INT64.MAX</td>
<td style="text-align: left;">1</td>
<td style="text-align: left;"><code dir="ltr" translate="no">       [error]      </code></td>
</tr>
<tr class="odd">
<td style="text-align: left;">INT64.MIN</td>
<td style="text-align: left;">-1</td>
<td style="text-align: left;"><code dir="ltr" translate="no">       [error]      </code></td>
</tr>
</tbody>
</table>

##### Node.js

``` javascript
const result = await db.pipeline()
  .collection("books")
  .select(field("soldBooks").add(field("unsoldBooks")).as("totalBooks"))
  .execute();test.firestore.js
```

### Web

``` javascript
const result = await execute(db.pipeline()
  .collection("books")
  .select(field("soldBooks").add(field("unsoldBooks")).as("totalBooks"))
);test.firestore.js
```

##### Swift

``` swift
let result = try await db.pipeline()
  .collection("books")
  .select([Field("soldBooks").add(Field("unsoldBooks")).as("totalBooks")])
  .execute()PipelineSnippets.swift
```

##### Kotlin  
Android

``` kotlin
val result = db.pipeline()
    .collection("books")
    .select(Expression.add(field("soldBooks"), field("unsoldBooks")).alias("totalBooks"))
    .execute()DocSnippets.kt
```

##### Java  
Android

``` text
Task<Pipeline.Snapshot> result = db.pipeline()
    .collection("books")
    .select(Expression.add(field("soldBooks"), field("unsoldBooks")).alias("totalBooks"))
    .execute();DocSnippets.java
    
```

##### Python

``` python
from google.cloud.firestore_v1.pipeline_expressions import Field

result = (
    client.pipeline()
    .collection("books")
    .select(Field.of("soldBooks").add(Field.of("unsoldBooks")).as_("totalBooks"))
    .execute()
)firestore_pipelines.py
```

##### Java

``` java
Pipeline.Snapshot result =
    firestore
        .pipeline()
        .collection("books")
        .select(add(field("soldBooks"), field("unsoldBooks")).as("totalBooks"))
        .execute()
        .get();PipelineSnippets.java
```

### SUBTRACT

**Syntax:**

``` text
subtract[N <: INT32 | INT64 | FLOAT64](x: N, y: N) -> N
```

**Description:**

Returns the value of `  x - y  ` .

**Examples:**

<table>
<thead>
<tr class="header">
<th style="text-align: left;">x</th>
<th style="text-align: left;">y</th>
<th style="text-align: left;"><code dir="ltr" translate="no">       subtract(x, y)      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">20</td>
<td style="text-align: left;">3</td>
<td style="text-align: left;">17</td>
</tr>
<tr class="even">
<td style="text-align: left;">10.0</td>
<td style="text-align: left;">1</td>
<td style="text-align: left;">9.0</td>
</tr>
<tr class="odd">
<td style="text-align: left;">22.5</td>
<td style="text-align: left;">2.0</td>
<td style="text-align: left;">20.5</td>
</tr>
<tr class="even">
<td style="text-align: left;">INT64.MAX</td>
<td style="text-align: left;">-1</td>
<td style="text-align: left;"><code dir="ltr" translate="no">       [error]      </code></td>
</tr>
<tr class="odd">
<td style="text-align: left;">INT64.MIN</td>
<td style="text-align: left;">1</td>
<td style="text-align: left;"><code dir="ltr" translate="no">       [error]      </code></td>
</tr>
</tbody>
</table>

##### Node.js

``` javascript
const storeCredit = 7;
const result = await db.pipeline()
  .collection("books")
  .select(field("price").subtract(constant(storeCredit)).as("totalCost"))
  .execute();test.firestore.js
```

### Web

``` javascript
const storeCredit = 7;
const result = await execute(db.pipeline()
  .collection("books")
  .select(field("price").subtract(constant(storeCredit)).as("totalCost"))
);test.firestore.js
```

##### Swift

``` swift
let storeCredit = 7
let result = try await db.pipeline()
  .collection("books")
  .select([Field("price").subtract(Constant(storeCredit)).as("totalCost")])
  .execute()PipelineSnippets.swift
```

##### Kotlin  
Android

``` kotlin
val storeCredit = 7
val result = db.pipeline()
    .collection("books")
    .select(Expression.subtract(field("price"), storeCredit).alias("totalCost"))
    .execute()DocSnippets.kt
```

##### Java  
Android

``` text
int storeCredit = 7;
Task<Pipeline.Snapshot> result = db.pipeline()
    .collection("books")
    .select(Expression.subtract(field("price"), storeCredit).alias("totalCost"))
    .execute();DocSnippets.java
    
```

##### Python

``` python
from google.cloud.firestore_v1.pipeline_expressions import Field

store_credit = 7
result = (
    client.pipeline()
    .collection("books")
    .select(Field.of("price").subtract(store_credit).as_("totalCost"))
    .execute()
)firestore_pipelines.py
```

##### Java

``` java
int storeCredit = 7;
Pipeline.Snapshot result =
    firestore
        .pipeline()
        .collection("books")
        .select(subtract(field("price"), storeCredit).as("totalCost"))
        .execute()
        .get();PipelineSnippets.java
```

### MULTIPLY

**Syntax:**

``` text
multiply[N <: INT32 | INT64 | FLOAT64](x: N, y: N) -> N
```

**Description:**

Returns the value of `  x * y  ` .

**Examples:**

<table>
<thead>
<tr class="header">
<th style="text-align: left;">x</th>
<th style="text-align: left;">y</th>
<th style="text-align: left;"><code dir="ltr" translate="no">       multiply(x, y)      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">20</td>
<td style="text-align: left;">3</td>
<td style="text-align: left;">60</td>
</tr>
<tr class="even">
<td style="text-align: left;">10.0</td>
<td style="text-align: left;">1</td>
<td style="text-align: left;">10.0</td>
</tr>
<tr class="odd">
<td style="text-align: left;">22.5</td>
<td style="text-align: left;">2.0</td>
<td style="text-align: left;">45.0</td>
</tr>
<tr class="even">
<td style="text-align: left;">INT64.MAX</td>
<td style="text-align: left;">2</td>
<td style="text-align: left;"><code dir="ltr" translate="no">       [error]      </code></td>
</tr>
<tr class="odd">
<td style="text-align: left;">INT64.MIN</td>
<td style="text-align: left;">2</td>
<td style="text-align: left;"><code dir="ltr" translate="no">       [error]      </code></td>
</tr>
<tr class="even">
<td style="text-align: left;">FLOAT64.MAX</td>
<td style="text-align: left;">FLOAT64.MAX</td>
<td style="text-align: left;"><code dir="ltr" translate="no">       +inf      </code></td>
</tr>
</tbody>
</table>

##### Node.js

``` javascript
const result = await db.pipeline()
  .collection("books")
  .select(field("price").multiply(field("soldBooks")).as("revenue"))
  .execute();test.firestore.js
```

### Web

``` javascript
const result = await execute(db.pipeline()
  .collection("books")
  .select(field("price").multiply(field("soldBooks")).as("revenue"))
);test.firestore.js
```

##### Swift

``` swift
let result = try await db.pipeline()
  .collection("books")
  .select([Field("price").multiply(Field("soldBooks")).as("revenue")])
  .execute()PipelineSnippets.swift
```

##### Kotlin  
Android

``` kotlin
val result = db.pipeline()
    .collection("books")
    .select(Expression.multiply(field("price"), field("soldBooks")).alias("revenue"))
    .execute()DocSnippets.kt
```

##### Java  
Android

``` text
Task<Pipeline.Snapshot> result = db.pipeline()
    .collection("books")
    .select(Expression.multiply(field("price"), field("soldBooks")).alias("revenue"))
    .execute();DocSnippets.java
    
```

##### Python

``` python
from google.cloud.firestore_v1.pipeline_expressions import Field

result = (
    client.pipeline()
    .collection("books")
    .select(Field.of("price").multiply(Field.of("soldBooks")).as_("revenue"))
    .execute()
)firestore_pipelines.py
```

##### Java

``` java
Pipeline.Snapshot result =
    firestore
        .pipeline()
        .collection("books")
        .select(multiply(field("price"), field("soldBooks")).as("revenue"))
        .execute()
        .get();PipelineSnippets.java
```

### DIVIDE

**Syntax:**

``` text
divide[N <: INT32 | INT64 | FLOAT64](x: N, y: N) -> N
```

**Description:**

Returns the value of `  x / y  ` . Integer division is truncated.

**Examples:**

<table>
<thead>
<tr class="header">
<th style="text-align: left;">x</th>
<th style="text-align: left;">y</th>
<th style="text-align: left;"><code dir="ltr" translate="no">       divide(x, y)      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">20</td>
<td style="text-align: left;">3</td>
<td style="text-align: left;">6</td>
</tr>
<tr class="even">
<td style="text-align: left;">10.0</td>
<td style="text-align: left;">3</td>
<td style="text-align: left;">3.333...</td>
</tr>
<tr class="odd">
<td style="text-align: left;">22.5</td>
<td style="text-align: left;">2</td>
<td style="text-align: left;">11.25</td>
</tr>
<tr class="even">
<td style="text-align: left;">10</td>
<td style="text-align: left;">0</td>
<td style="text-align: left;"><code dir="ltr" translate="no">       [error]      </code></td>
</tr>
<tr class="odd">
<td style="text-align: left;">1.0</td>
<td style="text-align: left;">0.0</td>
<td style="text-align: left;"><code dir="ltr" translate="no">       +inf      </code></td>
</tr>
<tr class="even">
<td style="text-align: left;">-1.0</td>
<td style="text-align: left;">0.0</td>
<td style="text-align: left;"><code dir="ltr" translate="no">       -inf      </code></td>
</tr>
</tbody>
</table>

##### Node.js

``` javascript
const result = await db.pipeline()
  .collection("books")
  .select(field("ratings").divide(field("soldBooks")).as("reviewRate"))
  .execute();test.firestore.js
```

### Web

``` javascript
const result = await execute(db.pipeline()
  .collection("books")
  .select(field("ratings").divide(field("soldBooks")).as("reviewRate"))
);test.firestore.js
```

##### Swift

``` swift
let result = try await db.pipeline()
  .collection("books")
  .select([Field("ratings").divide(Field("soldBooks")).as("reviewRate")])
  .execute()PipelineSnippets.swift
```

##### Kotlin  
Android

``` kotlin
val result = db.pipeline()
    .collection("books")
    .select(Expression.divide(field("ratings"), field("soldBooks")).alias("reviewRate"))
    .execute()DocSnippets.kt
```

##### Java  
Android

``` text
Task<Pipeline.Snapshot> result = db.pipeline()
    .collection("books")
    .select(Expression.divide(field("ratings"), field("soldBooks")).alias("reviewRate"))
    .execute();DocSnippets.java
    
```

##### Python

``` python
from google.cloud.firestore_v1.pipeline_expressions import Field

result = (
    client.pipeline()
    .collection("books")
    .select(Field.of("ratings").divide(Field.of("soldBooks")).as_("reviewRate"))
    .execute()
)firestore_pipelines.py
```

##### Java

``` java
Pipeline.Snapshot result =
    firestore
        .pipeline()
        .collection("books")
        .select(divide(field("ratings"), field("soldBooks")).as("reviewRate"))
        .execute()
        .get();PipelineSnippets.java
```

### MOD

**Syntax:**

``` text
mod[N <: INT32 | INT64 | FLOAT64](x: N, y: N) -> N
```

**Description:**

Returns the remainder of `  x / y  ` .

  - Throws an `  error  ` when `  y  ` is zero for integer types ( `  INT64  ` ).
  - Returns `  NaN  ` when `  y  ` is zero for float types ( `  FLOAT64  ` ).

**Examples:**

<table>
<thead>
<tr class="header">
<th style="text-align: left;">x</th>
<th style="text-align: left;">y</th>
<th style="text-align: left;"><code dir="ltr" translate="no">       mod(x, y)      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">20</td>
<td style="text-align: left;">3</td>
<td style="text-align: left;">2</td>
</tr>
<tr class="even">
<td style="text-align: left;">-10</td>
<td style="text-align: left;">3</td>
<td style="text-align: left;">-1</td>
</tr>
<tr class="odd">
<td style="text-align: left;">10</td>
<td style="text-align: left;">-3</td>
<td style="text-align: left;">1</td>
</tr>
<tr class="even">
<td style="text-align: left;">-10</td>
<td style="text-align: left;">-3</td>
<td style="text-align: left;">-1</td>
</tr>
<tr class="odd">
<td style="text-align: left;">10</td>
<td style="text-align: left;">1</td>
<td style="text-align: left;">0</td>
</tr>
<tr class="even">
<td style="text-align: left;">22.5</td>
<td style="text-align: left;">2</td>
<td style="text-align: left;">0.5</td>
</tr>
<tr class="odd">
<td style="text-align: left;">22.5</td>
<td style="text-align: left;">0.0</td>
<td style="text-align: left;"><code dir="ltr" translate="no">       NaN      </code></td>
</tr>
<tr class="even">
<td style="text-align: left;">25</td>
<td style="text-align: left;">0</td>
<td style="text-align: left;"><code dir="ltr" translate="no">       [error]      </code></td>
</tr>
</tbody>
</table>

##### Node.js

``` javascript
const displayCapacity = 1000;
const result = await db.pipeline()
  .collection("books")
  .select(field("unsoldBooks").mod(constant(displayCapacity)).as("warehousedBooks"))
  .execute();test.firestore.js
```

### Web

``` javascript
const displayCapacity = 1000;
const result = await execute(db.pipeline()
  .collection("books")
  .select(field("unsoldBooks").mod(constant(displayCapacity)).as("warehousedBooks"))
);test.firestore.js
```

##### Swift

``` swift
let displayCapacity = 1000
let result = try await db.pipeline()
  .collection("books")
  .select([Field("unsoldBooks").mod(Constant(displayCapacity)).as("warehousedBooks")])
  .execute()PipelineSnippets.swift
```

##### Kotlin  
Android

``` kotlin
val displayCapacity = 1000
val result = db.pipeline()
    .collection("books")
    .select(Expression.mod(field("unsoldBooks"), displayCapacity).alias("warehousedBooks"))
    .execute()DocSnippets.kt
```

##### Java  
Android

``` text
int displayCapacity = 1000;
Task<Pipeline.Snapshot> result = db.pipeline()
    .collection("books")
    .select(Expression.mod(field("unsoldBooks"), displayCapacity).alias("warehousedBooks"))
    .execute();DocSnippets.java
    
```

##### Python

``` python
from google.cloud.firestore_v1.pipeline_expressions import Field

display_capacity = 1000
result = (
    client.pipeline()
    .collection("books")
    .select(Field.of("unsoldBooks").mod(display_capacity).as_("warehousedBooks"))
    .execute()
)firestore_pipelines.py
```

##### Java

``` java
int displayCapacity = 1000;
Pipeline.Snapshot result =
    firestore
        .pipeline()
        .collection("books")
        .select(mod(field("unsoldBooks"), displayCapacity).as("warehousedBooks"))
        .execute()
        .get();PipelineSnippets.java
```

### CEIL

**Syntax:**

``` text
ceil[N <: INT32 | INT64 | FLOAT64](number: N) -> N
```

**Description:**

Returns the smallest integer value that isn't less than `  number  ` .

**Examples:**

<table>
<thead>
<tr class="header">
<th style="text-align: left;">number</th>
<th style="text-align: left;"><code dir="ltr" translate="no">       ceil(number)      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">20</td>
<td style="text-align: left;">20</td>
</tr>
<tr class="even">
<td style="text-align: left;">10</td>
<td style="text-align: left;">10</td>
</tr>
<tr class="odd">
<td style="text-align: left;">0</td>
<td style="text-align: left;">0</td>
</tr>
<tr class="even">
<td style="text-align: left;">24L</td>
<td style="text-align: left;">24L</td>
</tr>
<tr class="odd">
<td style="text-align: left;">-0.4</td>
<td style="text-align: left;">-0.0</td>
</tr>
<tr class="even">
<td style="text-align: left;">0.4</td>
<td style="text-align: left;">1.0</td>
</tr>
<tr class="odd">
<td style="text-align: left;">22.5</td>
<td style="text-align: left;">23.0</td>
</tr>
<tr class="even">
<td style="text-align: left;"><code dir="ltr" translate="no">       +inf      </code></td>
<td style="text-align: left;"><code dir="ltr" translate="no">       +inf      </code></td>
</tr>
<tr class="odd">
<td style="text-align: left;"><code dir="ltr" translate="no">       -inf      </code></td>
<td style="text-align: left;"><code dir="ltr" translate="no">       -inf      </code></td>
</tr>
</tbody>
</table>

##### Node.js

``` javascript
const booksPerShelf = 100;
const result = await db.pipeline()
  .collection("books")
  .select(
    field("unsoldBooks").divide(constant(booksPerShelf)).ceil().as("requiredShelves")
  )
  .execute();test.firestore.js
```

### Web

``` javascript
const booksPerShelf = 100;
const result = await execute(db.pipeline()
  .collection("books")
  .select(
    field("unsoldBooks").divide(constant(booksPerShelf)).ceil().as("requiredShelves")
  )
);test.firestore.js
```

##### Swift

``` swift
let booksPerShelf = 100
let result = try await db.pipeline()
  .collection("books")
  .select([
    Field("unsoldBooks").divide(Constant(booksPerShelf)).ceil().as("requiredShelves")
  ])
  .execute()PipelineSnippets.swift
```

##### Kotlin  
Android

``` kotlin
val booksPerShelf = 100
val result = db.pipeline()
    .collection("books")
    .select(
        Expression.divide(field("unsoldBooks"), booksPerShelf).ceil().alias("requiredShelves")
    )
    .execute()DocSnippets.kt
```

##### Java  
Android

``` text
int booksPerShelf = 100;
Task<Pipeline.Snapshot> result = db.pipeline()
    .collection("books")
    .select(
        Expression.divide(field("unsoldBooks"), booksPerShelf).ceil().alias("requiredShelves")
    )
    .execute();DocSnippets.java
    
```

##### Python

``` python
from google.cloud.firestore_v1.pipeline_expressions import Field

books_per_shelf = 100
result = (
    client.pipeline()
    .collection("books")
    .select(
        Field.of("unsoldBooks")
        .divide(books_per_shelf)
        .ceil()
        .as_("requiredShelves")
    )
    .execute()
)firestore_pipelines.py
```

##### Java

``` java
int booksPerShelf = 100;
Pipeline.Snapshot result =
    firestore
        .pipeline()
        .collection("books")
        .select(ceil(divide(field("unsoldBooks"), booksPerShelf)).as("requiredShelves"))
        .execute()
        .get();PipelineSnippets.java
```

### FLOOR

**Syntax:**

``` text
floor[N <: INT32 | INT64 | FLOAT64](number: N) -> N
```

**Description:**

Returns the largest integer value that isn't greater than `  number  ` .

**Examples:**

<table>
<thead>
<tr class="header">
<th style="text-align: left;">number</th>
<th style="text-align: left;"><code dir="ltr" translate="no">       floor(number)      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">20</td>
<td style="text-align: left;">20</td>
</tr>
<tr class="even">
<td style="text-align: left;">10</td>
<td style="text-align: left;">10</td>
</tr>
<tr class="odd">
<td style="text-align: left;">0</td>
<td style="text-align: left;">0</td>
</tr>
<tr class="even">
<td style="text-align: left;">2147483648</td>
<td style="text-align: left;">2147483648</td>
</tr>
<tr class="odd">
<td style="text-align: left;">-0.4</td>
<td style="text-align: left;">-1.0</td>
</tr>
<tr class="even">
<td style="text-align: left;">0.4</td>
<td style="text-align: left;">0.0</td>
</tr>
<tr class="odd">
<td style="text-align: left;">22.5</td>
<td style="text-align: left;">22.0</td>
</tr>
<tr class="even">
<td style="text-align: left;"><code dir="ltr" translate="no">       +inf      </code></td>
<td style="text-align: left;"><code dir="ltr" translate="no">       +inf      </code></td>
</tr>
<tr class="odd">
<td style="text-align: left;"><code dir="ltr" translate="no">       -inf      </code></td>
<td style="text-align: left;"><code dir="ltr" translate="no">       -inf      </code></td>
</tr>
</tbody>
</table>

##### Node.js

``` javascript
const result = await db.pipeline()
  .collection("books")
  .addFields(
    field("wordCount").divide(field("pages")).floor().as("wordsPerPage")
  )
  .execute();test.firestore.js
```

### Web

``` javascript
const result = await execute(db.pipeline()
  .collection("books")
  .addFields(
    field("wordCount").divide(field("pages")).floor().as("wordsPerPage")
  )
);test.firestore.js
```

##### Swift

``` swift
let result = try await db.pipeline()
  .collection("books")
  .addFields([
    Field("wordCount").divide(Field("pages")).floor().as("wordsPerPage")
  ])
  .execute()PipelineSnippets.swift
```

##### Kotlin  
Android

``` kotlin
val result = db.pipeline()
    .collection("books")
    .addFields(
        Expression.divide(field("wordCount"), field("pages")).floor().alias("wordsPerPage")
    )
    .execute()DocSnippets.kt
```

##### Java  
Android

``` text
Task<Pipeline.Snapshot> result = db.pipeline()
    .collection("books")
    .addFields(
        Expression.divide(field("wordCount"), field("pages")).floor().alias("wordsPerPage")
    )
    .execute();DocSnippets.java
    
```

##### Python

``` python
from google.cloud.firestore_v1.pipeline_expressions import Field

result = (
    client.pipeline()
    .collection("books")
    .add_fields(
        Field.of("wordCount").divide(Field.of("pages")).floor().as_("wordsPerPage")
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
        .addFields(floor(divide(field("wordCount"), field("pages"))).as("wordsPerPage"))
        .execute()
        .get();PipelineSnippets.java
```

### ROUND

**Syntax:**

``` text
round[N <: INT32 | INT64 | FLOAT64 | DECIMAL128](number: N) -> N
round[N <: INT32 | INT64 | FLOAT64 | DECIMAL128](number: N, places: INT64) -> N
```

**Description:**

Rounds `  places  ` digits off a `  number  ` . Rounds digits from the right of the decimal point if `  places  ` is positive, and to the left of the decimal point if it is negative.

  - If only `  number  ` is provided, rounds to the nearest whole value.
  - Rounds away from zero in halfway cases.
  - An `  error  ` is thrown if rounding with a negative `  places  ` value results in overflow.

**Examples:**

<table>
<thead>
<tr class="header">
<th style="text-align: left;">number</th>
<th style="text-align: left;">places</th>
<th style="text-align: left;"><code dir="ltr" translate="no">       round(number, places)      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">15.5</td>
<td style="text-align: left;">0</td>
<td style="text-align: left;">16.0</td>
</tr>
<tr class="even">
<td style="text-align: left;">-15.5</td>
<td style="text-align: left;">0</td>
<td style="text-align: left;">-16.0</td>
</tr>
<tr class="odd">
<td style="text-align: left;">15</td>
<td style="text-align: left;">1</td>
<td style="text-align: left;">15</td>
</tr>
<tr class="even">
<td style="text-align: left;">15</td>
<td style="text-align: left;">0</td>
<td style="text-align: left;">15</td>
</tr>
<tr class="odd">
<td style="text-align: left;">15</td>
<td style="text-align: left;">-1</td>
<td style="text-align: left;">20</td>
</tr>
<tr class="even">
<td style="text-align: left;">15</td>
<td style="text-align: left;">-2</td>
<td style="text-align: left;">0</td>
</tr>
<tr class="odd">
<td style="text-align: left;">15.48924</td>
<td style="text-align: left;">1</td>
<td style="text-align: left;">15.5</td>
</tr>
<tr class="even">
<td style="text-align: left;">2 <sup>31</sup> -1</td>
<td style="text-align: left;">-1</td>
<td style="text-align: left;"><code dir="ltr" translate="no">       [error]      </code></td>
</tr>
<tr class="odd">
<td style="text-align: left;">2 <sup>63</sup> -1L</td>
<td style="text-align: left;">-1</td>
<td style="text-align: left;"><code dir="ltr" translate="no">       [error]      </code></td>
</tr>
</tbody>
</table>

##### Node.js

``` javascript
const result = await db.pipeline()
  .collection("books")
  .select(field("soldBooks").multiply(field("price")).round().as("partialRevenue"))
  .aggregate(field("partialRevenue").sum().as("totalRevenue"))
  .execute();test.firestore.js
```

### Web

``` javascript
const result = await execute(db.pipeline()
  .collection("books")
  .select(field("soldBooks").multiply(field("price")).round().as("partialRevenue"))
  .aggregate(field("partialRevenue").sum().as("totalRevenue"))
  );test.firestore.js
```

##### Swift

``` swift
let result = try await db.pipeline()
  .collection("books")
  .select([Field("soldBooks").multiply(Field("price")).round().as("partialRevenue")])
  .aggregate([Field("partialRevenue").sum().as("totalRevenue")])
  .execute()PipelineSnippets.swift
```

##### Kotlin  
Android

``` kotlin
val result = db.pipeline()
    .collection("books")
    .select(Expression.multiply(field("soldBooks"), field("price")).round().alias("partialRevenue"))
    .aggregate(AggregateFunction.sum("partialRevenue").alias("totalRevenue"))
    .execute()DocSnippets.kt
```

##### Java  
Android

``` text
Task<Pipeline.Snapshot> result = db.pipeline()
    .collection("books")
    .select(Expression.multiply(field("soldBooks"), field("price")).round().alias("partialRevenue"))
    .aggregate(AggregateFunction.sum("partialRevenue").alias("totalRevenue"))
    .execute();DocSnippets.java
    
```

##### Python

``` python
from google.cloud.firestore_v1.pipeline_expressions import Field

result = (
    client.pipeline()
    .collection("books")
    .select(
        Field.of("soldBooks")
        .multiply(Field.of("price"))
        .round()
        .as_("partialRevenue")
    )
    .aggregate(Field.of("partialRevenue").sum().as_("totalRevenue"))
    .execute()
)firestore_pipelines.py
```

##### Java

``` java
Pipeline.Snapshot result =
    firestore
        .pipeline()
        .collection("books")
        .select(round(multiply(field("soldBooks"), field("price"))).as("partialRevenue"))
        .aggregate(sum("partialRevenue").as("totalRevenue"))
        .execute()
        .get();PipelineSnippets.java
```

### POW

**Syntax:**

``` text
pow(base: FLOAT64, exponent: FLOAT64) -> FLOAT64
```

**Description:**

Returns the value `  base  ` raised to the power of `  exponent  ` .

  - Throws an error if `  base <= 0  ` and `  exponent  ` is negative.

  - For any `  exponent  ` , `  pow(1, exponent)  ` is 1.

  - For any `  base  ` , `  pow(base, 0)  ` is 1.

**Examples:**

<table>
<thead>
<tr class="header">
<th style="text-align: left;">base</th>
<th style="text-align: left;">exponent</th>
<th style="text-align: left;"><code dir="ltr" translate="no">       pow(base, exponent)      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">2</td>
<td style="text-align: left;">3</td>
<td style="text-align: left;">8.0</td>
</tr>
<tr class="even">
<td style="text-align: left;">2</td>
<td style="text-align: left;">-3</td>
<td style="text-align: left;">0.125</td>
</tr>
<tr class="odd">
<td style="text-align: left;"><code dir="ltr" translate="no">       +inf      </code></td>
<td style="text-align: left;">0</td>
<td style="text-align: left;">1.0</td>
</tr>
<tr class="even">
<td style="text-align: left;">1</td>
<td style="text-align: left;"><code dir="ltr" translate="no">       +inf      </code></td>
<td style="text-align: left;">1.0</td>
</tr>
<tr class="odd">
<td style="text-align: left;">-1</td>
<td style="text-align: left;">0.5</td>
<td style="text-align: left;"><code dir="ltr" translate="no">       [error]      </code></td>
</tr>
<tr class="even">
<td style="text-align: left;">0</td>
<td style="text-align: left;">-1</td>
<td style="text-align: left;"><code dir="ltr" translate="no">       [error]      </code></td>
</tr>
</tbody>
</table>

##### Node.js

``` javascript
const googleplex = { latitude: 37.4221, longitude: 122.0853 };
const result = await db.pipeline()
  .collection("cities")
  .addFields(
    field("lat").subtract(constant(googleplex.latitude))
      .multiply(111 /* km per degree */)
      .pow(2)
      .as("latitudeDifference"),
    field("lng").subtract(constant(googleplex.longitude))
      .multiply(111 /* km per degree */)
      .pow(2)
      .as("longitudeDifference")
  )
  .select(
    field("latitudeDifference").add(field("longitudeDifference")).sqrt()
      // Inaccurate for large distances or close to poles
      .as("approximateDistanceToGoogle")
  )
  .execute();test.firestore.js
```

### Web

``` javascript
const googleplex = { latitude: 37.4221, longitude: 122.0853 };
const result = await execute(db.pipeline()
  .collection("cities")
  .addFields(
    field("lat").subtract(constant(googleplex.latitude))
      .multiply(111 /* km per degree */)
      .pow(2)
      .as("latitudeDifference"),
    field("lng").subtract(constant(googleplex.longitude))
      .multiply(111 /* km per degree */)
      .pow(2)
      .as("longitudeDifference")
  )
  .select(
    field("latitudeDifference").add(field("longitudeDifference")).sqrt()
      // Inaccurate for large distances or close to poles
      .as("approximateDistanceToGoogle")
  )
);test.firestore.js
```

##### Swift

``` swift
let googleplex = CLLocation(latitude: 37.4221, longitude: 122.0853)
let result = try await db.pipeline()
  .collection("cities")
  .addFields([
    Field("lat").subtract(Constant(googleplex.coordinate.latitude))
      .multiply(111 /* km per degree */)
      .pow(2)
      .as("latitudeDifference"),
    Field("lng").subtract(Constant(googleplex.coordinate.latitude))
      .multiply(111 /* km per degree */)
      .pow(2)
      .as("longitudeDifference")
  ])
  .select([
    Field("latitudeDifference").add(Field("longitudeDifference")).sqrt()
      // Inaccurate for large distances or close to poles
      .as("approximateDistanceToGoogle")
  ])
  .execute()PipelineSnippets.swift
```

##### Kotlin  
Android

``` kotlin
val googleplex = GeoPoint(37.4221, -122.0853)
val result = db.pipeline()
    .collection("cities")
    .addFields(
        field("lat").subtract(googleplex.latitude)
            .multiply(111 /* km per degree */)
            .pow(2)
            .alias("latitudeDifference"),
        field("lng").subtract(googleplex.longitude)
            .multiply(111 /* km per degree */)
            .pow(2)
            .alias("longitudeDifference")
    )
    .select(
        field("latitudeDifference").add(field("longitudeDifference")).sqrt()
            // Inaccurate for large distances or close to poles
            .alias("approximateDistanceToGoogle")
    )
    .execute()DocSnippets.kt
```

##### Java  
Android

``` text
GeoPoint googleplex = new GeoPoint(37.4221, -122.0853);
Task<Pipeline.Snapshot> result = db.pipeline()
    .collection("cities")
    .addFields(
        field("lat").subtract(googleplex.getLatitude())
            .multiply(111 /* km per degree */)
            .pow(2)
            .alias("latitudeDifference"),
        field("lng").subtract(googleplex.getLongitude())
            .multiply(111 /* km per degree */)
            .pow(2)
            .alias("longitudeDifference")
    )
    .select(
        field("latitudeDifference").add(field("longitudeDifference")).sqrt()
            // Inaccurate for large distances or close to poles
            .alias("approximateDistanceToGoogle")
    )
    .execute();DocSnippets.java
    
```

##### Python

``` python
from google.cloud.firestore_v1.pipeline_expressions import Field

googleplexLat = 37.4221
googleplexLng = -122.0853
result = (
    client.pipeline()
    .collection("cities")
    .add_fields(
        Field.of("lat")
        .subtract(googleplexLat)
        .multiply(111)  # km per degree
        .pow(2)
        .as_("latitudeDifference"),
        Field.of("lng")
        .subtract(googleplexLng)
        .multiply(111)  # km per degree
        .pow(2)
        .as_("longitudeDifference"),
    )
    .select(
        Field.of("latitudeDifference")
        .add(Field.of("longitudeDifference"))
        .sqrt()
        # Inaccurate for large distances or close to poles
        .as_("approximateDistanceToGoogle")
    )
    .execute()
)firestore_pipelines.py
```

##### Java

``` java
double googleplexLat = 37.4221;
double googleplexLng = -122.0853;
Pipeline.Snapshot result =
    firestore
        .pipeline()
        .collection("cities")
        .addFields(
            pow(multiply(subtract(field("lat"), googleplexLat), 111), 2)
                .as("latitudeDifference"),
            pow(multiply(subtract(field("lng"), googleplexLng), 111), 2)
                .as("longitudeDifference"))
        .select(
            sqrt(add(field("latitudeDifference"), field("longitudeDifference")))
                // Inaccurate for large distances or close to poles
                .as("approximateDistanceToGoogle"))
        .execute()
        .get();PipelineSnippets.java
```

### SQRT

**Syntax:**

``` text
sqrt[N <: FLOAT64 | DECIMAL128](number: N) -> N
```

**Description:**

Returns the square root of a `  number  ` .

  - Throws an `  error  ` if `  number  ` is negative.

**Examples:**

<table>
<thead>
<tr class="header">
<th style="text-align: left;">number</th>
<th style="text-align: left;"><code dir="ltr" translate="no">       sqrt(number)      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">25</td>
<td style="text-align: left;">5.0</td>
</tr>
<tr class="even">
<td style="text-align: left;">12.002</td>
<td style="text-align: left;">3.464...</td>
</tr>
<tr class="odd">
<td style="text-align: left;">0.0</td>
<td style="text-align: left;">0.0</td>
</tr>
<tr class="even">
<td style="text-align: left;"><code dir="ltr" translate="no">       NaN      </code></td>
<td style="text-align: left;"><code dir="ltr" translate="no">       NaN      </code></td>
</tr>
<tr class="odd">
<td style="text-align: left;"><code dir="ltr" translate="no">       +inf      </code></td>
<td style="text-align: left;"><code dir="ltr" translate="no">       +inf      </code></td>
</tr>
<tr class="even">
<td style="text-align: left;"><code dir="ltr" translate="no">       -inf      </code></td>
<td style="text-align: left;"><code dir="ltr" translate="no">       [error]      </code></td>
</tr>
<tr class="odd">
<td style="text-align: left;"><code dir="ltr" translate="no">       x &lt; 0      </code></td>
<td style="text-align: left;"><code dir="ltr" translate="no">       [error]      </code></td>
</tr>
</tbody>
</table>

##### Node.js

``` javascript
const googleplex = { latitude: 37.4221, longitude: 122.0853 };
const result = await db.pipeline()
  .collection("cities")
  .addFields(
    field("lat").subtract(constant(googleplex.latitude))
      .multiply(111 /* km per degree */)
      .pow(2)
      .as("latitudeDifference"),
    field("lng").subtract(constant(googleplex.longitude))
      .multiply(111 /* km per degree */)
      .pow(2)
      .as("longitudeDifference")
  )
  .select(
    field("latitudeDifference").add(field("longitudeDifference")).sqrt()
      // Inaccurate for large distances or close to poles
      .as("approximateDistanceToGoogle")
  )
  .execute();test.firestore.js
```

### Web

``` javascript
const googleplex = { latitude: 37.4221, longitude: 122.0853 };
const result = await execute(db.pipeline()
  .collection("cities")
  .addFields(
    field("lat").subtract(constant(googleplex.latitude))
      .multiply(111 /* km per degree */)
      .pow(2)
      .as("latitudeDifference"),
    field("lng").subtract(constant(googleplex.longitude))
      .multiply(111 /* km per degree */)
      .pow(2)
      .as("longitudeDifference")
  )
  .select(
    field("latitudeDifference").add(field("longitudeDifference")).sqrt()
      // Inaccurate for large distances or close to poles
      .as("approximateDistanceToGoogle")
  )
);test.firestore.js
```

##### Swift

``` swift
let googleplex = CLLocation(latitude: 37.4221, longitude: 122.0853)
let result = try await db.pipeline()
  .collection("cities")
  .addFields([
    Field("lat").subtract(Constant(googleplex.coordinate.latitude))
      .multiply(111 /* km per degree */)
      .pow(2)
      .as("latitudeDifference"),
    Field("lng").subtract(Constant(googleplex.coordinate.latitude))
      .multiply(111 /* km per degree */)
      .pow(2)
      .as("longitudeDifference")
  ])
  .select([
    Field("latitudeDifference").add(Field("longitudeDifference")).sqrt()
      // Inaccurate for large distances or close to poles
      .as("approximateDistanceToGoogle")
  ])
  .execute()PipelineSnippets.swift
```

##### Kotlin  
Android

``` kotlin
val googleplex = GeoPoint(37.4221, -122.0853)
val result = db.pipeline()
    .collection("cities")
    .addFields(
        field("lat").subtract(googleplex.latitude)
            .multiply(111 /* km per degree */)
            .pow(2)
            .alias("latitudeDifference"),
        field("lng").subtract(googleplex.longitude)
            .multiply(111 /* km per degree */)
            .pow(2)
            .alias("longitudeDifference")
    )
    .select(
        field("latitudeDifference").add(field("longitudeDifference")).sqrt()
            // Inaccurate for large distances or close to poles
            .alias("approximateDistanceToGoogle")
    )
    .execute()DocSnippets.kt
```

##### Java  
Android

``` text
GeoPoint googleplex = new GeoPoint(37.4221, -122.0853);
Task<Pipeline.Snapshot> result = db.pipeline()
    .collection("cities")
    .addFields(
        field("lat").subtract(googleplex.getLatitude())
            .multiply(111 /* km per degree */)
            .pow(2)
            .alias("latitudeDifference"),
        field("lng").subtract(googleplex.getLongitude())
            .multiply(111 /* km per degree */)
            .pow(2)
            .alias("longitudeDifference")
    )
    .select(
        field("latitudeDifference").add(field("longitudeDifference")).sqrt()
            // Inaccurate for large distances or close to poles
            .alias("approximateDistanceToGoogle")
    )
    .execute();DocSnippets.java
    
```

##### Python

``` python
from google.cloud.firestore_v1.pipeline_expressions import Field

googleplexLat = 37.4221
googleplexLng = -122.0853
result = (
    client.pipeline()
    .collection("cities")
    .add_fields(
        Field.of("lat")
        .subtract(googleplexLat)
        .multiply(111)  # km per degree
        .pow(2)
        .as_("latitudeDifference"),
        Field.of("lng")
        .subtract(googleplexLng)
        .multiply(111)  # km per degree
        .pow(2)
        .as_("longitudeDifference"),
    )
    .select(
        Field.of("latitudeDifference")
        .add(Field.of("longitudeDifference"))
        .sqrt()
        # Inaccurate for large distances or close to poles
        .as_("approximateDistanceToGoogle")
    )
    .execute()
)firestore_pipelines.py
```

##### Java

``` java
double googleplexLat = 37.4221;
double googleplexLng = -122.0853;
Pipeline.Snapshot result =
    firestore
        .pipeline()
        .collection("cities")
        .addFields(
            pow(multiply(subtract(field("lat"), googleplexLat), 111), 2)
                .as("latitudeDifference"),
            pow(multiply(subtract(field("lng"), googleplexLng), 111), 2)
                .as("longitudeDifference"))
        .select(
            sqrt(add(field("latitudeDifference"), field("longitudeDifference")))
                // Inaccurate for large distances or close to poles
                .as("approximateDistanceToGoogle"))
        .execute()
        .get();PipelineSnippets.java
```

### EXP

**Syntax:**

``` text
exp(exponent: FLOAT64) -> FLOAT64
```

**Description:**

Returns the value of Euler's number raised to the power of `  exponent  ` , also called the natural exponential function.

**Examples:**

<table>
<thead>
<tr class="header">
<th style="text-align: left;">exponent</th>
<th style="text-align: left;"><code dir="ltr" translate="no">       exp(exponent)      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">0.0</td>
<td style="text-align: left;">1.0</td>
</tr>
<tr class="even">
<td style="text-align: left;">10</td>
<td style="text-align: left;"><code dir="ltr" translate="no">       e^10      </code> ( <code dir="ltr" translate="no">       FLOAT64      </code> )</td>
</tr>
<tr class="odd">
<td style="text-align: left;"><code dir="ltr" translate="no">       +inf      </code></td>
<td style="text-align: left;"><code dir="ltr" translate="no">       +inf      </code></td>
</tr>
<tr class="even">
<td style="text-align: left;"><code dir="ltr" translate="no">       -inf      </code></td>
<td style="text-align: left;">0</td>
</tr>
</tbody>
</table>

##### Node.js

``` javascript
const result = await db.pipeline()
  .collection("books")
  .select(field("rating").exp().as("expRating"))
  .execute();test.firestore.js
```

### Web

``` javascript
const result = await execute(db.pipeline()
  .collection("books")
  .select(field("rating").exp().as("expRating"))
);test.firestore.js
```

##### Swift

``` swift
let result = try await db.pipeline()
  .collection("books")
  .select([Field("rating").exp().as("expRating")])
  .execute()PipelineSnippets.swift
```

##### Kotlin  
Android

``` kotlin
val result = db.pipeline()
    .collection("books")
    .select(field("rating").exp().alias("expRating"))
    .execute()DocSnippets.kt
```

##### Java  
Android

``` text
Task<Pipeline.Snapshot> result = db.pipeline()
    .collection("books")
    .select(field("rating").exp().alias("expRating"))
    .execute();DocSnippets.java
    
```

##### Python

``` python
from google.cloud.firestore_v1.pipeline_expressions import Field

result = (
    client.pipeline()
    .collection("books")
    .select(Field.of("rating").exp().as_("expRating"))
    .execute()
)firestore_pipelines.py
```

##### Java

``` java
Pipeline.Snapshot result =
    firestore
        .pipeline()
        .collection("books")
        .select(exp(field("rating")).as("expRating"))
        .execute()
        .get();PipelineSnippets.java
```

### LN

**Syntax:**

``` text
ln(number: FLOAT64) -> FLOAT64
```

**Description:**

Returns the natural logarithm of `  number  ` . This function is equivalent to `  log(number)  ` .

**Examples:**

<table>
<thead>
<tr class="header">
<th style="text-align: left;">number</th>
<th style="text-align: left;"><code dir="ltr" translate="no">       ln(number)      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">1</td>
<td style="text-align: left;">0.0</td>
</tr>
<tr class="even">
<td style="text-align: left;">2L</td>
<td style="text-align: left;">0.693...</td>
</tr>
<tr class="odd">
<td style="text-align: left;">1.0</td>
<td style="text-align: left;">0.0</td>
</tr>
<tr class="even">
<td style="text-align: left;"><code dir="ltr" translate="no">       e      </code> ( <code dir="ltr" translate="no">       FLOAT64      </code> )</td>
<td style="text-align: left;">1.0</td>
</tr>
<tr class="odd">
<td style="text-align: left;"><code dir="ltr" translate="no">       -inf      </code></td>
<td style="text-align: left;"><code dir="ltr" translate="no">       NaN      </code></td>
</tr>
<tr class="even">
<td style="text-align: left;"><code dir="ltr" translate="no">       +inf      </code></td>
<td style="text-align: left;"><code dir="ltr" translate="no">       +inf      </code></td>
</tr>
<tr class="odd">
<td style="text-align: left;"><code dir="ltr" translate="no">       x &lt;= 0      </code></td>
<td style="text-align: left;"><code dir="ltr" translate="no">       [error]      </code></td>
</tr>
</tbody>
</table>

##### Node.js

``` javascript
const result = await db.pipeline()
  .collection("books")
  .select(field("rating").ln().as("lnRating"))
  .execute();test.firestore.js
```

### Web

``` javascript
const result = await execute(db.pipeline()
  .collection("books")
  .select(field("rating").ln().as("lnRating"))
);test.firestore.js
```

##### Swift

``` swift
let result = try await db.pipeline()
  .collection("books")
  .select([Field("rating").ln().as("lnRating")])
  .execute()PipelineSnippets.swift
```

##### Kotlin  
Android

``` kotlin
val result = db.pipeline()
    .collection("books")
    .select(field("rating").ln().alias("lnRating"))
    .execute()DocSnippets.kt
```

##### Java  
Android

``` text
Task<Pipeline.Snapshot> result = db.pipeline()
    .collection("books")
    .select(field("rating").ln().alias("lnRating"))
    .execute();DocSnippets.java
    
```

##### Python

``` python
from google.cloud.firestore_v1.pipeline_expressions import Field

result = (
    client.pipeline()
    .collection("books")
    .select(Field.of("rating").ln().as_("lnRating"))
    .execute()
)firestore_pipelines.py
```

##### Java

``` java
Pipeline.Snapshot result =
    firestore
        .pipeline()
        .collection("books")
        .select(ln(field("rating")).as("lnRating"))
        .execute()
        .get();PipelineSnippets.java
```

### LOG

**Syntax:**

``` text
log(number: FLOAT64, base: FLOAT64) -> FLOAT64
log(number: FLOAT64) -> FLOAT64
```

**Description:**

Returns the logarithm of a `  number  ` to `  base  ` .

  - If only `  number  ` is provided, returns the logarithm of `  number  ` to `  base  ` (synonymous to `  ln(number)  ` ).

**Examples:**

<table>
<thead>
<tr class="header">
<th style="text-align: left;">number</th>
<th style="text-align: left;">base</th>
<th style="text-align: left;"><code dir="ltr" translate="no">       log(number, base)      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">100</td>
<td style="text-align: left;">10</td>
<td style="text-align: left;">2.0</td>
</tr>
<tr class="even">
<td style="text-align: left;"><code dir="ltr" translate="no">       -inf      </code></td>
<td style="text-align: left;"><code dir="ltr" translate="no">       Numeric      </code></td>
<td style="text-align: left;"><code dir="ltr" translate="no">       NaN      </code></td>
</tr>
<tr class="odd">
<td style="text-align: left;"><code dir="ltr" translate="no">       Numeric      </code> .</td>
<td style="text-align: left;"><code dir="ltr" translate="no">       +inf      </code></td>
<td style="text-align: left;"><code dir="ltr" translate="no">       NaN      </code></td>
</tr>
<tr class="even">
<td style="text-align: left;"><code dir="ltr" translate="no">       number &lt;= 0      </code></td>
<td style="text-align: left;"><code dir="ltr" translate="no">       Numeric      </code></td>
<td style="text-align: left;"><code dir="ltr" translate="no">       [error]      </code></td>
</tr>
<tr class="odd">
<td style="text-align: left;"><code dir="ltr" translate="no">       Numeric      </code></td>
<td style="text-align: left;"><code dir="ltr" translate="no">       base &lt;= 0      </code></td>
<td style="text-align: left;"><code dir="ltr" translate="no">       [error]      </code></td>
</tr>
<tr class="even">
<td style="text-align: left;"><code dir="ltr" translate="no">       Numeric      </code></td>
<td style="text-align: left;">1.0</td>
<td style="text-align: left;"><code dir="ltr" translate="no">       [error]      </code></td>
</tr>
</tbody>
</table>

### LOG10

**Syntax:**

``` text
log10(x: FLOAT64) -> FLOAT64
```

**Description:**

Returns the logarithm of a `  number  ` to base `  10  ` .

**Examples:**

<table>
<thead>
<tr class="header">
<th style="text-align: left;">number</th>
<th style="text-align: left;"><code dir="ltr" translate="no">       log10(number)      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">100</td>
<td style="text-align: left;">2.0</td>
</tr>
<tr class="even">
<td style="text-align: left;"><code dir="ltr" translate="no">       -inf      </code></td>
<td style="text-align: left;"><code dir="ltr" translate="no">       NaN      </code></td>
</tr>
<tr class="odd">
<td style="text-align: left;"><code dir="ltr" translate="no">       +inf      </code></td>
<td style="text-align: left;"><code dir="ltr" translate="no">       +inf      </code></td>
</tr>
<tr class="even">
<td style="text-align: left;"><code dir="ltr" translate="no">       x &lt;= 0      </code></td>
<td style="text-align: left;"><code dir="ltr" translate="no">       [error]      </code></td>
</tr>
</tbody>
</table>

### RAND

**Syntax:**

``` text
rand() -> FLOAT64
```

**Description:**

Return a pseudo-random floating point number, chosen uniformly between `  0.0  ` (inclusive) and `  1.0  ` (exclusive).

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
<td><code dir="ltr" translate="no">         ARRAY_GET       </code></td>
<td>Returns the element at a given index in an <code dir="ltr" translate="no">       ARRAY      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         ARRAY_LENGTH       </code></td>
<td>Returns the number of elements in an <code dir="ltr" translate="no">       ARRAY      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         ARRAY_REVERSE       </code></td>
<td>Reverses the order of elements in an <code dir="ltr" translate="no">       ARRAY      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         SUM       </code></td>
<td>Returns the sum of all <code dir="ltr" translate="no">       NUMERIC      </code> values in an <code dir="ltr" translate="no">       ARRAY      </code> .</td>
</tr>
<tr class="odd">
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

### ARRAY\_GET

**Syntax:**

``` text
array_get(array: ARRAY, index: INT64) -> ANY
```

**Description:**

Returns the element at the 0-based `  index  ` in `  array  ` .

  - If `  index  ` is negative, elements are accessed from the end of array, where `  -1  ` is the last element.
  - If `  array  ` is not of type `  ARRAY  ` , the function returns an absent value.
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
<td style="text-align: left;">absent</td>
</tr>
<tr class="even">
<td style="text-align: left;">null</td>
<td style="text-align: left;">0</td>
<td style="text-align: left;">absent</td>
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

If there are multiple maximum equivalent values, any one of those values can be returned. Value type ordering follows [documented ordering](/docs/firestore/manage-data/data-types#value_type_ordering) .

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

If there are multiple minimum equivalent values, any one of those values can be returned. Value type ordering follows [documented ordering](/docs/firestore/manage-data/data-types#value_type_ordering) .

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

## **String Functions**

<table>
<tbody>
<tr class="odd">
<td>Name</td>
<td>Description</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         BYTE_LENGTH       </code></td>
<td>Returns the number of <code dir="ltr" translate="no">       BYTES      </code> in a <code dir="ltr" translate="no">       STRING      </code> or <code dir="ltr" translate="no">       BYTES      </code> value</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         CHAR_LENGTH       </code></td>
<td>Returns the number of unicode characters in a <code dir="ltr" translate="no">       STRING      </code> value</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         STARTS_WITH       </code></td>
<td>Returns <code dir="ltr" translate="no">       TRUE      </code> if a <code dir="ltr" translate="no">       STRING      </code> begins with a given prefix</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         ENDS_WITH       </code></td>
<td>Returns <code dir="ltr" translate="no">       TRUE      </code> if a <code dir="ltr" translate="no">       STRING      </code> ends with a given postfix</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         LIKE       </code></td>
<td>Returns <code dir="ltr" translate="no">       TRUE      </code> if a <code dir="ltr" translate="no">       STRING      </code> matches a pattern</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         REGEX_CONTAINS       </code></td>
<td>Returns <code dir="ltr" translate="no">       TRUE      </code> if a value is a partial or full match for a regular expression</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         REGEX_MATCH       </code></td>
<td>Returns <code dir="ltr" translate="no">       TRUE      </code> if any part of a value matches a regular expression</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         STRING_CONCAT       </code></td>
<td>Concatenates multiple <code dir="ltr" translate="no">       STRING      </code> into a <code dir="ltr" translate="no">       STRING      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         STRING_CONTAINS       </code></td>
<td>Returns <code dir="ltr" translate="no">       TRUE      </code> if a value contains a <code dir="ltr" translate="no">       STRING      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         TO_UPPER       </code></td>
<td>Converts a <code dir="ltr" translate="no">       STRING      </code> or <code dir="ltr" translate="no">       BYTES      </code> value to uppercase.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         TO_LOWER       </code></td>
<td>Converts a <code dir="ltr" translate="no">       STRING      </code> or <code dir="ltr" translate="no">       BYTES      </code> value to lowercase.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         SUBSTRING       </code></td>
<td>Gets a substring of a <code dir="ltr" translate="no">       STRING      </code> or <code dir="ltr" translate="no">       BYTES      </code> value.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         STRING_REVERSE       </code></td>
<td>Reverses a <code dir="ltr" translate="no">       STRING      </code> or <code dir="ltr" translate="no">       BYTES      </code> value.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         TRIM       </code></td>
<td>Trims leading and trailing characters from a <code dir="ltr" translate="no">       STRING      </code> or <code dir="ltr" translate="no">       BYTES      </code> value.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         SPLIT       </code></td>
<td>Splits a <code dir="ltr" translate="no">       STRING      </code> or <code dir="ltr" translate="no">       BYTES      </code> value into an array.</td>
</tr>
</tbody>
</table>

### BYTE\_LENGTH

**Syntax:**

``` text
byte_length[T <: STRING | BYTES](value: T) -> INT64
```

**Description:**

Returns the number of `  BYTES  ` in a `  STRING  ` or `  BYTES  ` value.

**Examples:**

<table>
<thead>
<tr class="header">
<th style="text-align: left;">value</th>
<th style="text-align: left;"><code dir="ltr" translate="no">       byte_length(value)      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">"abc"</td>
<td style="text-align: left;">3</td>
</tr>
<tr class="even">
<td style="text-align: left;">"xyzabc"</td>
<td style="text-align: left;">6</td>
</tr>
<tr class="odd">
<td style="text-align: left;">b"abc"</td>
<td style="text-align: left;">3</td>
</tr>
</tbody>
</table>

##### Node.js

``` javascript
const result = await db.pipeline()
  .collection("books")
  .select(
    field("title").byteLength().as("titleByteLength")
  )
  .execute();test.firestore.js
```

### Web

``` javascript
const result = await execute(db.pipeline()
  .collection("books")
  .select(
    field("title").byteLength().as("titleByteLength")
  )
);test.firestore.js
```

##### Swift

``` swift
let result = try await db.pipeline()
  .collection("books")
  .select([
    Field("title").byteLength().as("titleByteLength")
  ])
  .execute()PipelineSnippets.swift
```

##### Kotlin  
Android

``` kotlin
val result = db.pipeline()
    .collection("books")
    .select(
        field("title").byteLength().alias("titleByteLength")
    )
    .execute()DocSnippets.kt
```

##### Java  
Android

``` text
Task<Pipeline.Snapshot> result = db.pipeline()
    .collection("books")
    .select(
        field("title").byteLength().alias("titleByteLength")
    )
    .execute();DocSnippets.java
```

##### Python

``` python
from google.cloud.firestore_v1.pipeline_expressions import Field

result = (
    client.pipeline()
    .collection("books")
    .select(Field.of("title").byte_length().as_("titleByteLength"))
    .execute()
)firestore_pipelines.py
```

##### Java

``` java
Pipeline.Snapshot result =
    firestore
        .pipeline()
        .collection("books")
        .select(byteLength(field("title")).as("titleByteLength"))
        .execute()
        .get();PipelineSnippets.java
```

### CHAR\_LENGTH

**Syntax:**

``` text
char_length(value: STRING) -> INT64
```

**Description:**

Returns the number of unicode code points in `  STRING  ` value.

**Examples:**

<table>
<thead>
<tr class="header">
<th style="text-align: left;">value</th>
<th style="text-align: left;"><code dir="ltr" translate="no">       char_length(value)      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">"abc"</td>
<td style="text-align: left;">3</td>
</tr>
<tr class="even">
<td style="text-align: left;">"hello"</td>
<td style="text-align: left;">5</td>
</tr>
<tr class="odd">
<td style="text-align: left;">"world"</td>
<td style="text-align: left;">5</td>
</tr>
</tbody>
</table>

##### Node.js

``` javascript
const result = await db.pipeline()
  .collection("books")
  .select(
    field("title").charLength().as("titleCharLength")
  )
  .execute();test.firestore.js
```

### Web

``` javascript
const result = await execute(db.pipeline()
  .collection("books")
  .select(
    field("title").charLength().as("titleCharLength")
  )
);test.firestore.js
```

##### Swift

``` swift
let result = try await db.pipeline()
  .collection("books")
  .select([
    Field("title").charLength().as("titleCharLength")
  ])
  .execute()PipelineSnippets.swift
```

##### Kotlin  
Android

``` kotlin
val result = db.pipeline()
    .collection("books")
    .select(
        field("title").charLength().alias("titleCharLength")
    )
    .execute()DocSnippets.kt
```

##### Java  
Android

``` text
Task<Pipeline.Snapshot> result = db.pipeline()
    .collection("books")
    .select(
        field("title").charLength().alias("titleCharLength")
    )
    .execute();DocSnippets.java
```

##### Python

``` python
from google.cloud.firestore_v1.pipeline_expressions import Field

result = (
    client.pipeline()
    .collection("books")
    .select(Field.of("title").char_length().as_("titleCharLength"))
    .execute()
)firestore_pipelines.py
```

##### Java

``` java
Pipeline.Snapshot result =
    firestore
        .pipeline()
        .collection("books")
        .select(charLength(field("title")).as("titleCharLength"))
        .execute()
        .get();PipelineSnippets.java
```

### STARTS\_WITH

**Syntax:**

``` text
starts_with(value: STRING, prefix: STRING) -> BOOLEAN
```

**Description:**

Returns `  TRUE  ` if `  value  ` begins with `  prefix  ` .

**Examples:**

<table>
<thead>
<tr class="header">
<th style="text-align: left;">value</th>
<th style="text-align: left;">prefix</th>
<th style="text-align: left;"><code dir="ltr" translate="no">       starts_with(value, prefix)      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">"abc"</td>
<td style="text-align: left;">"a"</td>
<td style="text-align: left;">true</td>
</tr>
<tr class="even">
<td style="text-align: left;">"abc"</td>
<td style="text-align: left;">"b"</td>
<td style="text-align: left;">false</td>
</tr>
<tr class="odd">
<td style="text-align: left;">"abc"</td>
<td style="text-align: left;">""</td>
<td style="text-align: left;">true</td>
</tr>
</tbody>
</table>

##### Node.js

``` javascript
const result = await db.pipeline()
  .collection("books")
  .select(
    field("title").startsWith("The")
      .as("needsSpecialAlphabeticalSort")
  )
  .execute();test.firestore.js
```

### Web

``` javascript
const result = await execute(db.pipeline()
  .collection("books")
  .select(
    field("title").startsWith("The")
      .as("needsSpecialAlphabeticalSort")
  )
);test.firestore.js
```

##### Swift

``` swift
let result = try await db.pipeline()
  .collection("books")
  .select([
    Field("title").startsWith("The")
      .as("needsSpecialAlphabeticalSort")
  ])
  .execute()PipelineSnippets.swift
```

##### Kotlin  
Android

``` kotlin
val result = db.pipeline()
    .collection("books")
    .select(
        field("title").startsWith("The")
            .alias("needsSpecialAlphabeticalSort")
    )
    .execute()DocSnippets.kt
```

##### Java  
Android

``` text
Task<Pipeline.Snapshot> result = db.pipeline()
    .collection("books")
    .select(
        field("title").startsWith("The")
            .alias("needsSpecialAlphabeticalSort")
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
        Field.of("title").starts_with("The").as_("needsSpecialAlphabeticalSort")
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
        .select(startsWith(field("title"), "The").as("needsSpecialAlphabeticalSort"))
        .execute()
        .get();PipelineSnippets.java
```

### ENDS\_WITH

**Syntax:**

``` text
ends_with(value: STRING, postfix: STRING) -> BOOLEAN
```

**Description:**

Returns `  TRUE  ` if `  value  ` ends with `  postfix  ` .

**Examples:**

<table>
<thead>
<tr class="header">
<th style="text-align: left;">value</th>
<th style="text-align: left;">postfix</th>
<th style="text-align: left;"><code dir="ltr" translate="no">       ends_with(value, postfix)      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">"abc"</td>
<td style="text-align: left;">"c"</td>
<td style="text-align: left;">true</td>
</tr>
<tr class="even">
<td style="text-align: left;">"abc"</td>
<td style="text-align: left;">"b"</td>
<td style="text-align: left;">false</td>
</tr>
<tr class="odd">
<td style="text-align: left;">"abc"</td>
<td style="text-align: left;">""</td>
<td style="text-align: left;">true</td>
</tr>
</tbody>
</table>

##### Node.js

``` javascript
const result = await db.pipeline()
  .collection("inventory/devices/laptops")
  .select(
    field("name").endsWith("16 inch")
      .as("16InLaptops")
  )
  .execute();test.firestore.js
```

##### Swift

``` swift
let result = try await db.pipeline()
  .collection("inventory/devices/laptops")
  .select([
    Field("name").endsWith("16 inch")
      .as("16InLaptops")
  ])
  .execute()PipelineSnippets.swift
```

##### Kotlin  
Android

``` kotlin
val result = db.pipeline()
    .collection("inventory/devices/laptops")
    .select(
        field("name").endsWith("16 inch")
            .alias("16InLaptops")
    )
    .execute()DocSnippets.kt
```

##### Java  
Android

``` text
Task<Pipeline.Snapshot> result = db.pipeline()
    .collection("inventory/devices/laptops")
    .select(
        field("name").endsWith("16 inch")
            .alias("16InLaptops")
    )
    .execute();DocSnippets.java
```

##### Python

``` python
from google.cloud.firestore_v1.pipeline_expressions import Field

result = (
    client.pipeline()
    .collection("inventory/devices/laptops")
    .select(Field.of("name").ends_with("16 inch").as_("16InLaptops"))
    .execute()
)firestore_pipelines.py
```

##### Java

``` java
Pipeline.Snapshot result =
    firestore
        .pipeline()
        .collection("inventory/devices/laptops")
        .select(endsWith(field("name"), "16 inch").as("16InLaptops"))
        .execute()
        .get();PipelineSnippets.java
```

### LIKE

**Syntax:**

``` text
like(value: STRING, pattern: STRING) -> BOOLEAN
```

**Description:**

Returns `  TRUE  ` if `  value  ` matches `  pattern  ` .

**Examples:**

<table>
<thead>
<tr class="header">
<th style="text-align: left;">value</th>
<th style="text-align: left;">pattern</th>
<th style="text-align: left;"><code dir="ltr" translate="no">       like(value, pattern)      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">"Firestore"</td>
<td style="text-align: left;">"Fire%"</td>
<td style="text-align: left;">true</td>
</tr>
<tr class="even">
<td style="text-align: left;">"Firestore"</td>
<td style="text-align: left;">"%store"</td>
<td style="text-align: left;">true</td>
</tr>
<tr class="odd">
<td style="text-align: left;">"Datastore"</td>
<td style="text-align: left;">"Data_tore"</td>
<td style="text-align: left;">true</td>
</tr>
<tr class="even">
<td style="text-align: left;">"100%"</td>
<td style="text-align: left;">"100\%"</td>
<td style="text-align: left;">true</td>
</tr>
</tbody>
</table>

##### Node.js

``` javascript
const result = await db.pipeline()
  .collection("books")
  .select(
    field("genre").like("%Fiction")
      .as("anyFiction")
  )
  .execute();test.firestore.js
```

### Web

``` javascript
const result = await execute(db.pipeline()
  .collection("books")
  .select(
    field("genre").like("%Fiction")
      .as("anyFiction")
  )
);test.firestore.js
```

##### Swift

``` swift
let result = try await db.pipeline()
  .collection("books")
  .select([
    Field("genre").like("%Fiction")
      .as("anyFiction")
  ])
  .execute()PipelineSnippets.swift
```

##### Kotlin  
Android

``` kotlin
val result = db.pipeline()
    .collection("books")
    .select(
        field("genre").like("%Fiction")
            .alias("anyFiction")
    )
    .execute()DocSnippets.kt
```

##### Java  
Android

``` text
Task<Pipeline.Snapshot> result = db.pipeline()
    .collection("books")
    .select(
        field("genre").like("%Fiction")
            .alias("anyFiction")
    )
    .execute();DocSnippets.java
```

##### Python

``` python
from google.cloud.firestore_v1.pipeline_expressions import Field

result = (
    client.pipeline()
    .collection("books")
    .select(Field.of("genre").like("%Fiction").as_("anyFiction"))
    .execute()
)firestore_pipelines.py
```

##### Java

``` java
Pipeline.Snapshot result =
    firestore
        .pipeline()
        .collection("books")
        .select(like(field("genre"), "%Fiction").as("anyFiction"))
        .execute()
        .get();PipelineSnippets.java
```

### REGEX\_CONTAINS

**Syntax:**

``` text
regex_contains(value: STRING, pattern: STRING) -> BOOLEAN
```

**Description:**

Returns `  TRUE  ` if some part of `  value  ` matches `  pattern  ` . If `  pattern  ` is not a valid regular expression, this function returns an `  error  ` .

Regular expressions follow the syntax of the [re2](https://github.com/google/re2/wiki/Syntax) library.

**Examples:**

<table>
<thead>
<tr class="header">
<th style="text-align: left;">value</th>
<th style="text-align: left;">pattern</th>
<th style="text-align: left;"><code dir="ltr" translate="no">       regex_contains(value, pattern)      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">"Firestore"</td>
<td style="text-align: left;">"Fire"</td>
<td style="text-align: left;">true</td>
</tr>
<tr class="even">
<td style="text-align: left;">"Firestore"</td>
<td style="text-align: left;">"store$"</td>
<td style="text-align: left;">true</td>
</tr>
<tr class="odd">
<td style="text-align: left;">"Firestore"</td>
<td style="text-align: left;">"data"</td>
<td style="text-align: left;">false</td>
</tr>
</tbody>
</table>

##### Node.js

``` javascript
const result = await db.pipeline()
  .collection("documents")
  .select(
    field("title").regexContains("Firestore (Enterprise|Standard)")
      .as("isFirestoreRelated")
  )
  .execute();test.firestore.js
```

### Web

``` javascript
const result = await execute(db.pipeline()
  .collection("documents")
  .select(
    field("title").regexContains("Firestore (Enterprise|Standard)")
      .as("isFirestoreRelated")
  )
);test.firestore.js
```

##### Swift

``` swift
let result = try await db.pipeline()
  .collection("documents")
  .select([
    Field("title").regexContains("Firestore (Enterprise|Standard)")
      .as("isFirestoreRelated")
  ])
  .execute()PipelineSnippets.swift
```

##### Kotlin  
Android

``` kotlin
val result = db.pipeline()
    .collection("documents")
    .select(
        field("title").regexContains("Firestore (Enterprise|Standard)")
            .alias("isFirestoreRelated")
    )
    .execute()DocSnippets.kt
```

##### Java  
Android

``` text
Task<Pipeline.Snapshot> result = db.pipeline()
    .collection("documents")
    .select(
        field("title").regexContains("Firestore (Enterprise|Standard)")
            .alias("isFirestoreRelated")
    )
    .execute();DocSnippets.java
```

##### Python

``` python
from google.cloud.firestore_v1.pipeline_expressions import Field

result = (
    client.pipeline()
    .collection("documents")
    .select(
        Field.of("title")
        .regex_contains("Firestore (Enterprise|Standard)")
        .as_("isFirestoreRelated")
    )
    .execute()
)firestore_pipelines.py
```

##### Java

``` java
Pipeline.Snapshot result =
    firestore
        .pipeline()
        .collection("documents")
        .select(
            regexContains(field("title"), "Firestore (Enterprise|Standard)")
                .as("isFirestoreRelated"))
        .execute()
        .get();PipelineSnippets.java
```

### REGEX\_MATCH

**Syntax:**

``` text
regex_match(value: STRING, pattern: STRING) -> BOOLEAN
```

**Description:**

Returns `  TRUE  ` if `  value  ` fully matches `  pattern  ` . If `  pattern  ` is not a valid regular expression, this function returns an `  error  ` .

Regular expressions follow the syntax of the [re2](https://github.com/google/re2/wiki/Syntax) library.

**Examples:**

<table>
<thead>
<tr class="header">
<th style="text-align: left;">value</th>
<th style="text-align: left;">pattern</th>
<th style="text-align: left;"><code dir="ltr" translate="no">       regex_match(value, pattern)      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">"Firestore"</td>
<td style="text-align: left;">"F.*store"</td>
<td style="text-align: left;">true</td>
</tr>
<tr class="even">
<td style="text-align: left;">"Firestore"</td>
<td style="text-align: left;">"Fire"</td>
<td style="text-align: left;">false</td>
</tr>
<tr class="odd">
<td style="text-align: left;">"Firestore"</td>
<td style="text-align: left;">"^F.*e$"</td>
<td style="text-align: left;">true</td>
</tr>
</tbody>
</table>

##### Node.js

``` javascript
const result = await db.pipeline()
  .collection("documents")
  .select(
    field("title").regexMatch("Firestore (Enterprise|Standard)")
      .as("isFirestoreExactly")
  )
  .execute();test.firestore.js
```

### Web

``` javascript
const result = await execute(db.pipeline()
  .collection("documents")
  .select(
    field("title").regexMatch("Firestore (Enterprise|Standard)")
      .as("isFirestoreExactly")
  )
);test.firestore.js
```

##### Swift

``` swift
let result = try await db.pipeline()
  .collection("documents")
  .select([
    Field("title").regexMatch("Firestore (Enterprise|Standard)")
      .as("isFirestoreExactly")
  ])
  .execute()PipelineSnippets.swift
```

##### Kotlin  
Android

``` kotlin
val result = db.pipeline()
    .collection("documents")
    .select(
        field("title").regexMatch("Firestore (Enterprise|Standard)")
            .alias("isFirestoreExactly")
    )
    .execute()DocSnippets.kt
```

##### Java  
Android

``` text
Task<Pipeline.Snapshot> result = db.pipeline()
    .collection("documents")
    .select(
        field("title").regexMatch("Firestore (Enterprise|Standard)")
            .alias("isFirestoreExactly")
    )
    .execute();DocSnippets.java
```

##### Python

``` python
from google.cloud.firestore_v1.pipeline_expressions import Field

result = (
    client.pipeline()
    .collection("documents")
    .select(
        Field.of("title")
        .regex_match("Firestore (Enterprise|Standard)")
        .as_("isFirestoreExactly")
    )
    .execute()
)firestore_pipelines.py
```

##### Java

``` java
Pipeline.Snapshot result =
    firestore
        .pipeline()
        .collection("documents")
        .select(
            regexMatch(field("title"), "Firestore (Enterprise|Standard)")
                .as("isFirestoreExactly"))
        .execute()
        .get();PipelineSnippets.java
```

### STRING\_CONCAT

**Syntax:**

``` text
string_concat(values: STRING...) -> STRING
```

**Description:**

Concatenates two or more `  STRING  ` values into a single result.

**Examples:**

<table>
<thead>
<tr class="header">
<th style="text-align: left;">arguments</th>
<th style="text-align: left;"><code dir="ltr" translate="no">       string_concat(values...)      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;"><code dir="ltr" translate="no">       ()      </code></td>
<td style="text-align: left;">error</td>
</tr>
<tr class="even">
<td style="text-align: left;"><code dir="ltr" translate="no">       ("a")      </code></td>
<td style="text-align: left;">"a"</td>
</tr>
<tr class="odd">
<td style="text-align: left;"><code dir="ltr" translate="no">       ("abc", "def")      </code></td>
<td style="text-align: left;">"abcdef"</td>
</tr>
<tr class="even">
<td style="text-align: left;"><code dir="ltr" translate="no">       ("a", "", "c")      </code></td>
<td style="text-align: left;">"ac"</td>
</tr>
</tbody>
</table>

##### Node.js

``` javascript
const result = await db.pipeline()
  .collection("books")
  .select(
    field("title").stringConcat(" by ", field("author"))
      .as("fullyQualifiedTitle")
  )
  .execute();test.firestore.js
```

### Web

``` javascript
const result = await execute(db.pipeline()
  .collection("books")
  .select(
    field("title").stringConcat(" by ", field("author"))
      .as("fullyQualifiedTitle")
  )
);test.firestore.js
```

##### Swift

``` swift
let result = try await db.pipeline()
  .collection("books")
  .select([
    Field("title").concat([" by ", Field("author")])
      .as("fullyQualifiedTitle")
  ])
  .execute()PipelineSnippets.swift
```

##### Kotlin  
Android

``` kotlin
val result = db.pipeline()
    .collection("books")
    .select(
        field("title").concat(" by ", field("author"))
            .alias("fullyQualifiedTitle")
    )
    .execute()DocSnippets.kt
```

##### Java  
Android

``` text
Task<Pipeline.Snapshot> result = db.pipeline()
    .collection("books")
    .select(
        field("title").concat(" by ", field("author"))
            .alias("fullyQualifiedTitle")
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
        Field.of("title")
        .concat(" by ", Field.of("author"))
        .as_("fullyQualifiedTitle")
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
        .select(stringConcat(field("title"), " by ", field("author")).as("fullyQualifiedTitle"))
        .execute()
        .get();PipelineSnippets.java
```

### STRING\_CONTAINS

**Syntax:**

``` text
string_contains(value: STRING, substring: STRING) -> BOOLEAN
```

**Description:**

Checks if `  value  ` contains the literal String `  substring  ` .

**Examples:**

<table>
<thead>
<tr class="header">
<th style="text-align: left;">value</th>
<th style="text-align: left;">substring</th>
<th style="text-align: left;"><code dir="ltr" translate="no">       string_contains(value, substring)      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">"abc"</td>
<td style="text-align: left;">"b"</td>
<td style="text-align: left;">true</td>
</tr>
<tr class="even">
<td style="text-align: left;">"abc"</td>
<td style="text-align: left;">"d"</td>
<td style="text-align: left;">false</td>
</tr>
<tr class="odd">
<td style="text-align: left;">"abc"</td>
<td style="text-align: left;">""</td>
<td style="text-align: left;">true</td>
</tr>
<tr class="even">
<td style="text-align: left;">"a.c"</td>
<td style="text-align: left;">"."</td>
<td style="text-align: left;">true</td>
</tr>
<tr class="odd">
<td style="text-align: left;">"☃☃☃"</td>
<td style="text-align: left;">"☃"</td>
<td style="text-align: left;">true</td>
</tr>
</tbody>
</table>

##### Node.js

``` javascript
const result = await db.pipeline()
  .collection("articles")
  .select(
    field("body").stringContains("Firestore")
      .as("isFirestoreRelated")
  )
  .execute();test.firestore.js
```

### Web

``` javascript
const result = await execute(db.pipeline()
  .collection("articles")
  .select(
    field("body").stringContains("Firestore")
      .as("isFirestoreRelated")
  )
);test.firestore.js
```

##### Swift

``` swift
let result = try await db.pipeline()
  .collection("articles")
  .select([
    Field("body").stringContains("Firestore")
      .as("isFirestoreRelated")
  ])
  .execute()PipelineSnippets.swift
```

##### Kotlin  
Android

``` kotlin
val result = db.pipeline()
    .collection("articles")
    .select(
        field("body").stringContains("Firestore")
            .alias("isFirestoreRelated")
    )
    .execute()DocSnippets.kt
```

##### Java  
Android

``` text
Task<Pipeline.Snapshot> result = db.pipeline()
    .collection("articles")
    .select(
        field("body").stringContains("Firestore")
            .alias("isFirestoreRelated")
    )
    .execute();DocSnippets.java
```

##### Python

``` python
from google.cloud.firestore_v1.pipeline_expressions import Field

result = (
    client.pipeline()
    .collection("articles")
    .select(Field.of("body").string_contains("Firestore").as_("isFirestoreRelated"))
    .execute()
)firestore_pipelines.py
```

##### Java

``` java
Pipeline.Snapshot result =
    firestore
        .pipeline()
        .collection("articles")
        .select(stringContains(field("body"), "Firestore").as("isFirestoreRelated"))
        .execute()
        .get();PipelineSnippets.java
```

### TO\_UPPER

**Syntax:**

``` text
to_upper[T <: STRING | BYTES](value: T) -> T
```

**Description:**

Converts a `  STRING  ` or `  BYTES  ` value to uppercase.

If a byte or char does not correspond to a UTF-8 lowercase alphabetic character, it is passed through unchanged.

**Examples:**

<table>
<thead>
<tr class="header">
<th style="text-align: left;">value</th>
<th style="text-align: left;"><code dir="ltr" translate="no">       to_upper(value)      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">"abc"</td>
<td style="text-align: left;">"ABC"</td>
</tr>
<tr class="even">
<td style="text-align: left;">"AbC"</td>
<td style="text-align: left;">"ABC"</td>
</tr>
<tr class="odd">
<td style="text-align: left;">b"abc"</td>
<td style="text-align: left;">b"ABC"</td>
</tr>
<tr class="even">
<td style="text-align: left;">b"a1c"</td>
<td style="text-align: left;">b"A1C"</td>
</tr>
</tbody>
</table>

##### Node.js

``` javascript
const result = await db.pipeline()
  .collection("authors")
  .select(
    field("name").toUpper()
      .as("uppercaseName")
  )
  .execute();test.firestore.js
```

### Web

``` javascript
const result = await execute(db.pipeline()
  .collection("authors")
  .select(
    field("name").toUpper()
      .as("uppercaseName")
  )
);test.firestore.js
```

##### Swift

``` swift
let result = try await db.pipeline()
  .collection("authors")
  .select([
    Field("name").toUpper()
      .as("uppercaseName")
  ])
  .execute()PipelineSnippets.swift
```

##### Kotlin  
Android

``` kotlin
val result = db.pipeline()
    .collection("authors")
    .select(
        field("name").toUpper()
            .alias("uppercaseName")
    )
    .execute()DocSnippets.kt
```

##### Java  
Android

``` text
Task<Pipeline.Snapshot> result = db.pipeline()
    .collection("authors")
    .select(
        field("name").toUpper()
            .alias("uppercaseName")
    )
    .execute();DocSnippets.java
```

##### Python

``` python
from google.cloud.firestore_v1.pipeline_expressions import Field

result = (
    client.pipeline()
    .collection("authors")
    .select(Field.of("name").to_upper().as_("uppercaseName"))
    .execute()
)firestore_pipelines.py
```

##### Java

``` java
Pipeline.Snapshot result =
    firestore
        .pipeline()
        .collection("authors")
        .select(toUpper(field("name")).as("uppercaseName"))
        .execute()
        .get();PipelineSnippets.java
```

### TO\_LOWER

**Syntax:**

``` text
to_lower[T <: STRING | BYTES](value: T) -> T
```

**Description:**

Converts a `  STRING  ` or `  BYTES  ` value to lowercase.

If a byte or char does not correspond to a UTF-8 uppercase alphabetic character, it is passed through unchanged.

**Examples:**

<table>
<thead>
<tr class="header">
<th style="text-align: left;">value</th>
<th style="text-align: left;"><code dir="ltr" translate="no">       to_lower(value)      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">"ABC"</td>
<td style="text-align: left;">"abc"</td>
</tr>
<tr class="even">
<td style="text-align: left;">"AbC"</td>
<td style="text-align: left;">"abc"</td>
</tr>
<tr class="odd">
<td style="text-align: left;">"A1C"</td>
<td style="text-align: left;">"a1c"</td>
</tr>
<tr class="even">
<td style="text-align: left;">b"ABC"</td>
<td style="text-align: left;">b"abc"</td>
</tr>
</tbody>
</table>

##### Node.js

``` javascript
const result = await db.pipeline()
  .collection("authors")
  .select(
    field("genre").toLower().equal("fantasy")
      .as("isFantasy")
  )
  .execute();test.firestore.js
```

### Web

``` javascript
const result = await execute(db.pipeline()
  .collection("authors")
  .select(
    field("genre").toLower().equal("fantasy")
      .as("isFantasy")
  )
);test.firestore.js
```

##### Swift

``` swift
let result = try await db.pipeline()
  .collection("authors")
  .select([
    Field("genre").toLower().equal("fantasy")
      .as("isFantasy")
  ])
  .execute()PipelineSnippets.swift
```

##### Kotlin  
Android

``` kotlin
val result = db.pipeline()
    .collection("authors")
    .select(
        field("genre").toLower().equal("fantasy")
            .alias("isFantasy")
    )
    .execute()DocSnippets.kt
```

##### Java  
Android

``` text
Task<Pipeline.Snapshot> result = db.pipeline()
    .collection("authors")
    .select(
        field("genre").toLower().equal("fantasy")
            .alias("isFantasy")
    )
    .execute();DocSnippets.java
```

##### Python

``` python
from google.cloud.firestore_v1.pipeline_expressions import Field

result = (
    client.pipeline()
    .collection("authors")
    .select(Field.of("genre").to_lower().equal("fantasy").as_("isFantasy"))
    .execute()
)firestore_pipelines.py
```

##### Java

``` java
Pipeline.Snapshot result =
    firestore
        .pipeline()
        .collection("authors")
        .select(equal(toLower(field("genre")), "fantasy").as("isFantasy"))
        .execute()
        .get();PipelineSnippets.java
```

### SUBSTRING

**Syntax:**

``` text
substring[T <: STRING | BYTES](input: T, position: INT64) -> T
substring[T <: STRING | BYTES](input: T, position: INT64, length: INT64) -> T
```

**Description:**

Returns a substring of `  input  ` starting at `  position  ` (zero-based index) and including up to `  length  ` entries. If no `  length  ` is provided, returns the substring from `  position  ` to the end of the `  input  ` .

  - If `  input  ` is a `  STRING  ` value, `  position  ` and `  length  ` are measured in unicode code points. If it is a `  BYTES  ` value, they are measured in bytes.

  - If `  position  ` is greater than the length of the `  input  ` , an empty substring is returned. If `  position  ` plus `  length  ` is greater than the length of `  input  ` , the substring is truncated to the end of `  input  ` .

  - If `  position  ` is negative, the position is taken from the end of the input. If the negative `  position  ` is greater than the size of the input, the position is set to zero. `  length  ` must be non-negative.

**Examples:**

When `  length  ` is not provided:

<table>
<thead>
<tr class="header">
<th style="text-align: left;">input</th>
<th style="text-align: left;">position</th>
<th style="text-align: left;"><code dir="ltr" translate="no">       substring(input, position)      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">"abc"</td>
<td style="text-align: left;">0</td>
<td style="text-align: left;">"abc"</td>
</tr>
<tr class="even">
<td style="text-align: left;">"abc"</td>
<td style="text-align: left;">1</td>
<td style="text-align: left;">"bc"</td>
</tr>
<tr class="odd">
<td style="text-align: left;">"abc"</td>
<td style="text-align: left;">3</td>
<td style="text-align: left;">""</td>
</tr>
<tr class="even">
<td style="text-align: left;">"abc"</td>
<td style="text-align: left;">-1</td>
<td style="text-align: left;">"c"</td>
</tr>
<tr class="odd">
<td style="text-align: left;">b"abc"</td>
<td style="text-align: left;">1</td>
<td style="text-align: left;">b"bc"</td>
</tr>
</tbody>
</table>

When `  length  ` is provided:

<table>
<thead>
<tr class="header">
<th style="text-align: left;">input</th>
<th style="text-align: left;">position</th>
<th style="text-align: left;">length</th>
<th style="text-align: left;"><code dir="ltr" translate="no">       substring(input, position, length)      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">"abc"</td>
<td style="text-align: left;">0</td>
<td style="text-align: left;">1</td>
<td style="text-align: left;">"a"</td>
</tr>
<tr class="even">
<td style="text-align: left;">"abc"</td>
<td style="text-align: left;">1</td>
<td style="text-align: left;">2</td>
<td style="text-align: left;">"bc"</td>
</tr>
<tr class="odd">
<td style="text-align: left;">"abc"</td>
<td style="text-align: left;">-1</td>
<td style="text-align: left;">1</td>
<td style="text-align: left;">"c"</td>
</tr>
<tr class="even">
<td style="text-align: left;">b"abc"</td>
<td style="text-align: left;">0</td>
<td style="text-align: left;">1</td>
<td style="text-align: left;">b"a"</td>
</tr>
</tbody>
</table>

##### Node.js

``` javascript
const result = await db.pipeline()
  .collection("books")
  .where(field("title").startsWith("The "))
  .select(
    field("title").substring(4)
      .as("titleWithoutLeadingThe")
  )
  .execute();test.firestore.js
```

### Web

``` javascript
const result = await execute(db.pipeline()
  .collection("books")
  .where(field("title").startsWith("The "))
  .select(
    field("title").substring(4)
      .as("titleWithoutLeadingThe")
  )
);test.firestore.js
```

##### Swift

``` swift
let result = try await db.pipeline()
  .collection("books")
  .where(Field("title").startsWith("The "))
  .select([
    Field("title").substring(position: 4)
      .as("titleWithoutLeadingThe")
  ])
  .execute()PipelineSnippets.swift
```

##### Kotlin  
Android

``` kotlin
val result = db.pipeline()
    .collection("books")
    .where(field("title").startsWith("The "))
    .select(
        field("title")
          .substring(constant(4),
            field("title").charLength().subtract(4))
            .alias("titleWithoutLeadingThe")
    )
    .execute()DocSnippets.kt
```

##### Java  
Android

``` text
Task<Pipeline.Snapshot> result = db.pipeline()
    .collection("books")
    .where(field("title").startsWith("The "))
    .select(
        field("title").substring(
          constant(4),
            field("title").charLength().subtract(4))
            .alias("titleWithoutLeadingThe")
    )
    .execute();DocSnippets.java
```

##### Python

``` python
from google.cloud.firestore_v1.pipeline_expressions import Field

result = (
    client.pipeline()
    .collection("books")
    .where(Field.of("title").starts_with("The "))
    .select(Field.of("title").substring(4).as_("titleWithoutLeadingThe"))
    .execute()
)firestore_pipelines.py
```

##### Java

``` java
Pipeline.Snapshot result =
    firestore
        .pipeline()
        .collection("books")
        .where(startsWith(field("title"), "The "))
        .select(
            substring(field("title"), constant(4), field("title").charLength())
                .as("titleWithoutLeadingThe"))
        .execute()
        .get();PipelineSnippets.java
```

### STRING\_REVERSE

**Syntax:**

``` text
string_reverse[T <: STRING | BYTES](input: T) -> T
```

**Description:**

Returns the supplied input in reverse order.

Characters are delineated by Unicode code points when the input is a `  STRING  ` , and bytes when the input is a `  BYTES  ` value.

**Examples:**

<table>
<thead>
<tr class="header">
<th style="text-align: left;">input</th>
<th style="text-align: left;"><code dir="ltr" translate="no">       string_reverse(input)      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">"abc"</td>
<td style="text-align: left;">"cba"</td>
</tr>
<tr class="even">
<td style="text-align: left;">"a🌹b"</td>
<td style="text-align: left;">"b🌹a"</td>
</tr>
<tr class="odd">
<td style="text-align: left;">"hello"</td>
<td style="text-align: left;">"olleh"</td>
</tr>
<tr class="even">
<td style="text-align: left;">b"abc"</td>
<td style="text-align: left;">b"cba"</td>
</tr>
</tbody>
</table>

##### Node.js

``` javascript
const result = await db.pipeline()
  .collection("books")
  .select(
    field("name").reverse().as("reversedName")
  )
  .execute();test.firestore.js
```

### Web

``` javascript
const result = await execute(db.pipeline()
  .collection("books")
  .select(
    field("name").reverse().as("reversedName")
  )
);test.firestore.js
```

##### Swift

``` swift
let result = try await db.pipeline()
  .collection("books")
  .select([
    Field("name").reverse().as("reversedName")
  ])
  .execute()PipelineSnippets.swift
```

##### Kotlin  
Android

``` kotlin
val result = db.pipeline()
    .collection("books")
    .select(
        field("name").reverse().alias("reversedName")
    )
    .execute()DocSnippets.kt
```

##### Java  
Android

``` text
Task<Pipeline.Snapshot> result = db.pipeline()
    .collection("books")
    .select(
        field("name").reverse().alias("reversedName")
    )
    .execute();DocSnippets.java
```

##### Python

``` python
from google.cloud.firestore_v1.pipeline_expressions import Field

result = (
    client.pipeline()
    .collection("books")
    .select(Field.of("name").string_reverse().as_("reversedName"))
    .execute()
)firestore_pipelines.py
```

##### Java

``` java
Pipeline.Snapshot result =
    firestore
        .pipeline()
        .collection("books")
        .select(reverse(field("name")).as("reversedName"))
        .execute()
        .get();PipelineSnippets.java
```

### TRIM

**Syntax:**

``` text
trim[T <: STRING | BYTES](input: T, values_to_trim: T) -> T
trim[T <: STRING | BYTES](input: T) -> T
```

**Description:**

Trims a specified set of `  BYTES  ` or `  CHARS  ` from the beginning and end of the supplied `  input  ` .

  - If no `  values_to_trim  ` are provided, trims whitespace characters.

**Examples:**

When `  values_to_trim  ` is not provided:

<table>
<thead>
<tr class="header">
<th style="text-align: left;">input</th>
<th style="text-align: left;"><code dir="ltr" translate="no">       trim(input)      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">" foo "</td>
<td style="text-align: left;">"foo"</td>
</tr>
<tr class="even">
<td style="text-align: left;">b" foo "</td>
<td style="text-align: left;">b"foo"</td>
</tr>
<tr class="odd">
<td style="text-align: left;">"foo"</td>
<td style="text-align: left;">"foo"</td>
</tr>
<tr class="even">
<td style="text-align: left;">""</td>
<td style="text-align: left;">""</td>
</tr>
<tr class="odd">
<td style="text-align: left;">" "</td>
<td style="text-align: left;">""</td>
</tr>
<tr class="even">
<td style="text-align: left;">"\t foo \n"</td>
<td style="text-align: left;">"foo"</td>
</tr>
<tr class="odd">
<td style="text-align: left;">b"\t foo \n"</td>
<td style="text-align: left;">b"foo"</td>
</tr>
<tr class="even">
<td style="text-align: left;">"\r\f\v foo \r\f\v"</td>
<td style="text-align: left;">"foo"</td>
</tr>
<tr class="odd">
<td style="text-align: left;">b"\r\f\v foo \r\f\v"</td>
<td style="text-align: left;">b"foo"</td>
</tr>
</tbody>
</table>

When `  values_to_trim  ` is provided:

<table>
<thead>
<tr class="header">
<th style="text-align: left;">input</th>
<th style="text-align: left;">values_to_trim</th>
<th style="text-align: left;"><code dir="ltr" translate="no">       trim(input, values_to_trim)      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">"abcbfooaacb"</td>
<td style="text-align: left;">"abc"</td>
<td style="text-align: left;">"foo"</td>
</tr>
<tr class="even">
<td style="text-align: left;">"abcdaabadbac"</td>
<td style="text-align: left;">"abc"</td>
<td style="text-align: left;">"daabad"</td>
</tr>
<tr class="odd">
<td style="text-align: left;">b"C1C2C3"</td>
<td style="text-align: left;">b"C1"</td>
<td style="text-align: left;">b"C2C3"</td>
</tr>
<tr class="even">
<td style="text-align: left;">b"C1C2"</td>
<td style="text-align: left;">"foo"</td>
<td style="text-align: left;">error</td>
</tr>
<tr class="odd">
<td style="text-align: left;">"foo"</td>
<td style="text-align: left;">b"C1"</td>
<td style="text-align: left;">error</td>
</tr>
</tbody>
</table>

### Web

``` javascript
const result = await execute(db.pipeline()
  .collection("books")
  .select(
    field("name").trim().as("whitespaceTrimmedName")
  )
);test.firestore.js
```

##### Swift

``` swift
let result = try await db.pipeline()
  .collection("books")
  .select([
    Field("name").trim(" \n\t").as("whitespaceTrimmedName")
  ])
  .execute()PipelineSnippets.swift
```

##### Kotlin  
Android

``` kotlin
val result = db.pipeline()
    .collection("books")
    .select(
        field("name").trim().alias("whitespaceTrimmedName")
    )
    .execute()DocSnippets.kt
```

##### Java  
Android

``` text
Task<Pipeline.Snapshot> result = db.pipeline()
    .collection("books")
    .select(
        field("name").trim().alias("whitespaceTrimmedName")
    )
    .execute();DocSnippets.java
```

##### Python

``` python
from google.cloud.firestore_v1.pipeline_expressions import Field

result = (
    client.pipeline()
    .collection("books")
    .select(Field.of("name").trim().as_("whitespaceTrimmedName"))
    .execute()
)firestore_pipelines.py
```

##### Java

``` java
Pipeline.Snapshot result =
    firestore
        .pipeline()
        .collection("books")
        .select(trim(field("name")).as("whitespaceTrimmedName"))
        .execute()
        .get();PipelineSnippets.java
```

### SPLIT

**Syntax:**

``` text
split(input: STRING) -> ARRAY<STRING>
split[T <: STRING | BYTES](input: T, delimiter: T) -> ARRAY<T>
```

**Description:**

Splits a `  STRING  ` or `  BYTES  ` value, using a delimiter.

  - For `  STRING  ` the default delimiter is the comma `  ,  ` . The delimiter is treated as a single string.

  - For `  BYTES  ` , you must specify a delimiter.

  - Splitting on an empty delimiter produces an array of Unicode codepoints for `  STRING  ` values, and an array of `  BYTES  ` for `  BYTES  ` values.

  - Splitting an empty `  STRING  ` returns an `  ARRAY  ` with a single empty `  STRING  ` .

**Examples:**

When `  delimiter  ` is not provided:

<table>
<thead>
<tr class="header">
<th style="text-align: left;">input</th>
<th style="text-align: left;"><code dir="ltr" translate="no">       split(input)      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">"foo,bar,foo"</td>
<td style="text-align: left;">["foo", "bar", "foo"]</td>
</tr>
<tr class="even">
<td style="text-align: left;">"foo"</td>
<td style="text-align: left;">["foo"]</td>
</tr>
<tr class="odd">
<td style="text-align: left;">",foo,"</td>
<td style="text-align: left;">["", "foo", ""]</td>
</tr>
<tr class="even">
<td style="text-align: left;">""</td>
<td style="text-align: left;">[""]</td>
</tr>
<tr class="odd">
<td style="text-align: left;">b"C120C2C4"</td>
<td style="text-align: left;">error</td>
</tr>
</tbody>
</table>

When `  delimiter  ` is provided:

<table>
<thead>
<tr class="header">
<th style="text-align: left;">input</th>
<th style="text-align: left;">delimiter</th>
<th style="text-align: left;"><code dir="ltr" translate="no">       split(input, delimiter)      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">"foo bar foo"</td>
<td style="text-align: left;">" "</td>
<td style="text-align: left;">["foo", "bar", "foo"]</td>
</tr>
<tr class="even">
<td style="text-align: left;">"foo bar foo"</td>
<td style="text-align: left;">"z"</td>
<td style="text-align: left;">["foo bar foo"]</td>
</tr>
<tr class="odd">
<td style="text-align: left;">"abc"</td>
<td style="text-align: left;">""</td>
<td style="text-align: left;">["a", "b", "c"]</td>
</tr>
<tr class="even">
<td style="text-align: left;">b"C1,C2,C4"</td>
<td style="text-align: left;">b","</td>
<td style="text-align: left;">[b"C1", b"C2", b"C4"]</td>
</tr>
<tr class="odd">
<td style="text-align: left;">b"ABC"</td>
<td style="text-align: left;">b""</td>
<td style="text-align: left;">[b"A", b"B", b"C"]</td>
</tr>
<tr class="even">
<td style="text-align: left;">"foo"</td>
<td style="text-align: left;">b"C1"</td>
<td style="text-align: left;">error</td>
</tr>
</tbody>
</table>

## **Timestamp Functions**

<table>
<tbody>
<tr class="odd">
<td>Name</td>
<td>Description</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         CURRENT_TIMESTAMP       </code></td>
<td>Generates a <code dir="ltr" translate="no">       TIMESTAMP      </code> corresponding to the request time.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         TIMESTAMP_TRUNC       </code></td>
<td>Truncates a <code dir="ltr" translate="no">       TIMESTAMP      </code> to a given granularity.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         UNIX_MICROS_TO_TIMESTAMP       </code></td>
<td>Converts the number of microseconds since <code dir="ltr" translate="no">       1970-01-01 00:00:00 UTC      </code> to a <code dir="ltr" translate="no">       TIMESTAMP      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         UNIX_MILLIS_TO_TIMESTAMP       </code></td>
<td>Converts the number of milliseconds since <code dir="ltr" translate="no">       1970-01-01 00:00:00 UTC      </code> to a <code dir="ltr" translate="no">       TIMESTAMP      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         UNIX_SECONDS_TO_TIMESTAMP       </code></td>
<td>Converts the number of seconds since <code dir="ltr" translate="no">       1970-01-01 00:00:00 UTC      </code> to a <code dir="ltr" translate="no">       TIMESTAMP      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         TIMESTAMP_ADD       </code></td>
<td>Adds a time interval to a <code dir="ltr" translate="no">       TIMESTAMP      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         TIMESTAMP_SUB       </code></td>
<td>Subtracts a time interval to a <code dir="ltr" translate="no">       TIMESTAMP      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         TIMESTAMP_TO_UNIX_MICROS       </code></td>
<td>Converts a <code dir="ltr" translate="no">       TIMESTAMP      </code> to the number of microseconds since <code dir="ltr" translate="no">       1970-01-01 00:00:00 UTC      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         TIMESTAMP_TO_UNIX_MILLIS       </code></td>
<td>Converts a <code dir="ltr" translate="no">       TIMESTAMP      </code> to the number of milliseconds since <code dir="ltr" translate="no">       1970-01-01 00:00:00 UTC      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         TIMESTAMP_TO_UNIX_SECONDS       </code></td>
<td>Converts a <code dir="ltr" translate="no">       TIMESTAMP      </code> to the number of seconds since <code dir="ltr" translate="no">       1970-01-01 00:00:00 UTC      </code></td>
</tr>
</tbody>
</table>

### CURRENT\_TIMESTAMP

**Syntax:**

``` text
current_timestamp() -> TIMESTAMP
```

**Description:**

Gets the timestamp at the beginning of request time `  input  ` (interpreted as the number of microseconds since `  1970-01-01 00:00:00 UTC  ` ).

This is stable within a query, and will always resolve to the same value if called multiple times.

### TIMESTAMP\_TRUNC

**Syntax:**

``` text
timestamp_trunc(timestamp: TIMESTAMP, granularity: STRING[, timezone: STRING]) -> TIMESTAMP
```

**Description:**

Truncates a timestamp down to a given granularity.

The `  granularity  ` argument must be a string and one of the following:

  - `  microsecond  `
  - `  millisecond  `
  - `  second  `
  - `  minute  `
  - `  hour  `
  - `  day  `
  - `  week  `
  - `  week([weekday])  `
  - `  month  `
  - `  quarter  `
  - `  year  `
  - `  isoyear  `

If the `  timezone  ` argument is provided, truncation will be based on the given timezone's calendar boundaries (e.g. day truncation will truncate to midnight in the given timezone). The truncation will respect daylight savings time.

If `  timezone  ` is not provided, truncation will be based on `  UTC  ` calendar boundaries.

The `  timezone  ` argument should be a string representation of a timezone from the tz database, for example `  America/New_York  ` . A custom time offset can also be used by specifying an offset from `  GMT  ` .

**Examples:**

<table>
<thead>
<tr class="header">
<th style="text-align: left;"><code dir="ltr" translate="no">       timestamp      </code></th>
<th style="text-align: left;"><code dir="ltr" translate="no">       granularity      </code></th>
<th style="text-align: left;"><code dir="ltr" translate="no">       timezone      </code></th>
<th style="text-align: left;"><code dir="ltr" translate="no">       timestamp_trunc(timestamp, granularity, timezone)      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">2000-01-01 10:20:30:123456 UTC</td>
<td style="text-align: left;">"second"</td>
<td style="text-align: left;">Not provided</td>
<td style="text-align: left;">2001-01-01 10:20:30 UTC</td>
</tr>
<tr class="even">
<td style="text-align: left;">1997-05-31 04:30:30 UTC</td>
<td style="text-align: left;">"day"</td>
<td style="text-align: left;">Not provided</td>
<td style="text-align: left;">1997-05-31 00:00:00 UTC</td>
</tr>
<tr class="odd">
<td style="text-align: left;">1997-05-31 04:30:30 UTC</td>
<td style="text-align: left;">"day"</td>
<td style="text-align: left;">"America/Los_Angeles"</td>
<td style="text-align: left;">1997-05-30 07:00:00 UTC</td>
</tr>
<tr class="even">
<td style="text-align: left;">2001-03-16 04:00:00 UTC</td>
<td style="text-align: left;">"week(friday)</td>
<td style="text-align: left;">Not provided</td>
<td style="text-align: left;">2001-03-16 00:00:00 UTC</td>
</tr>
<tr class="odd">
<td style="text-align: left;">2001-03-23 04:00:00 UTC</td>
<td style="text-align: left;">"week(friday)</td>
<td style="text-align: left;">"America/Los_Angeles"</td>
<td style="text-align: left;">2001-03-23 17:00:00 UTC</td>
</tr>
<tr class="even">
<td style="text-align: left;">2026-01-24 20:00:00 UTC</td>
<td style="text-align: left;">"month"</td>
<td style="text-align: left;">"GMT+06:32:43"</td>
<td style="text-align: left;">2026-01-01T06:32:43 UTC</td>
</tr>
</tbody>
</table>

### UNIX\_MICROS\_TO\_TIMESTAMP

**Syntax:**

``` text
unix_micros_to_timestamp(input: INT64) -> TIMESTAMP
```

**Description:**

Converts `  input  ` (interpreted as the number of microseconds since `  1970-01-01 00:00:00 UTC  ` ) to a `  TIMESTAMP  ` . Throws an `  error  ` if `  input  ` cannot be converted to a valid `  TIMESTAMP  ` .

**Examples:**

<table>
<thead>
<tr class="header">
<th style="text-align: left;"><code dir="ltr" translate="no">       input      </code></th>
<th style="text-align: left;"><code dir="ltr" translate="no">       unix_micros_to_timestamp(input)      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">0L</td>
<td style="text-align: left;">1970-01-01 00:00:00 UTC</td>
</tr>
<tr class="even">
<td style="text-align: left;">400123456L</td>
<td style="text-align: left;">1970-01-01 00:06:40.123456 UTC</td>
</tr>
<tr class="odd">
<td style="text-align: left;">-1000000L</td>
<td style="text-align: left;">1969-12-31 23:59:59 UTC</td>
</tr>
</tbody>
</table>

##### Node.js

``` javascript
const result = await db.pipeline()
  .collection("documents")
  .select(
    field("createdAtMicros").unixMicrosToTimestamp().as("createdAtString")
  )
  .execute();test.firestore.js
```

### Web

``` javascript
const result = await execute(db.pipeline()
  .collection("documents")
  .select(
    field("createdAtMicros").unixMicrosToTimestamp().as("createdAtString")
  )
);test.firestore.js
```

##### Swift

``` swift
let result = try await db.pipeline()
  .collection("documents")
  .select([
    Field("createdAtMicros").unixMicrosToTimestamp().as("createdAtString")
  ])
  .execute()PipelineSnippets.swift
```

##### Kotlin  
Android

``` kotlin
val result = db.pipeline()
    .collection("documents")
    .select(
        field("createdAtMicros").unixMicrosToTimestamp().alias("createdAtString")
    )
    .execute()DocSnippets.kt
```

##### Java  
Android

``` text
Task<Pipeline.Snapshot> result = db.pipeline()
    .collection("documents")
    .select(
        field("createdAtMicros").unixMicrosToTimestamp().alias("createdAtString")
    )
    .execute();DocSnippets.java
```

##### Python

``` python
from google.cloud.firestore_v1.pipeline_expressions import Field

result = (
    client.pipeline()
    .collection("documents")
    .select(
        Field.of("createdAtMicros")
        .unix_micros_to_timestamp()
        .as_("createdAtString")
    )
    .execute()
)firestore_pipelines.py
```

##### Java

``` java
Pipeline.Snapshot result =
    firestore
        .pipeline()
        .collection("documents")
        .select(unixMicrosToTimestamp(field("createdAtMicros")).as("createdAtString"))
        .execute()
        .get();PipelineSnippets.java
```

### UNIX\_MILLIS\_TO\_TIMESTAMP

**Syntax:**

``` text
unix_millis_to_timestamp(input: INT64) -> TIMESTAMP
```

**Description:**

Converts `  input  ` (interpreted as the number of milliseconds since `  1970-01-01 00:00:00 UTC  ` ) to a `  TIMESTAMP  ` . Throws an `  error  ` if `  input  ` cannot be converted to a valid `  TIMESTAMP  ` .

**Examples:**

<table>
<thead>
<tr class="header">
<th style="text-align: left;"><code dir="ltr" translate="no">       input      </code></th>
<th style="text-align: left;"><code dir="ltr" translate="no">       unix_millis_to_timestamp(input)      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">0L</td>
<td style="text-align: left;">1970-01-01 00:00:00 UTC</td>
</tr>
<tr class="even">
<td style="text-align: left;">4000123L</td>
<td style="text-align: left;">1970-01-01 01:06:40.123 UTC</td>
</tr>
<tr class="odd">
<td style="text-align: left;">-1000000L</td>
<td style="text-align: left;">1969-12-31 23:43:20 UTC</td>
</tr>
</tbody>
</table>

##### Node.js

``` javascript
const result = await db.pipeline()
  .collection("documents")
  .select(
    field("createdAtMillis").unixMillisToTimestamp().as("createdAtString")
  )
  .execute();test.firestore.js
```

### Web

``` javascript
const result = await execute(db.pipeline()
  .collection("documents")
  .select(
    field("createdAtMillis").unixMillisToTimestamp().as("createdAtString")
  )
);test.firestore.js
```

##### Swift

``` swift
let result = try await db.pipeline()
  .collection("documents")
  .select([
    Field("createdAtMillis").unixMillisToTimestamp().as("createdAtString")
  ])
  .execute()PipelineSnippets.swift
```

##### Kotlin  
Android

``` kotlin
val result = db.pipeline()
    .collection("documents")
    .select(
        field("createdAtMillis").unixMillisToTimestamp().alias("createdAtString")
    )
    .execute()DocSnippets.kt
```

##### Java  
Android

``` text
Task<Pipeline.Snapshot> result = db.pipeline()
    .collection("documents")
    .select(
        field("createdAtMillis").unixMillisToTimestamp().alias("createdAtString")
    )
    .execute();DocSnippets.java
```

##### Python

``` python
from google.cloud.firestore_v1.pipeline_expressions import Field

result = (
    client.pipeline()
    .collection("documents")
    .select(
        Field.of("createdAtMillis")
        .unix_millis_to_timestamp()
        .as_("createdAtString")
    )
    .execute()
)firestore_pipelines.py
```

##### Java

``` java
Pipeline.Snapshot result =
    firestore
        .pipeline()
        .collection("documents")
        .select(unixMillisToTimestamp(field("createdAtMillis")).as("createdAtString"))
        .execute()
        .get();PipelineSnippets.java
```

### UNIX\_SECONDS\_TO\_TIMESTAMP

**Syntax:**

``` text
unix_seconds_to_timestamp(input: INT64) -> TIMESTAMP
```

**Description:**

Converts `  input  ` (interpreted as the number of seconds since `  1970-01-01 00:00:00 UTC  ` ) to a `  TIMESTAMP  ` . Throws an `  error  ` if `  input  ` cannot be converted to a valid `  TIMESTAMP  ` .

**Examples:**

<table>
<thead>
<tr class="header">
<th style="text-align: left;"><code dir="ltr" translate="no">       input      </code></th>
<th style="text-align: left;"><code dir="ltr" translate="no">       unix_seconds_to_timestamp(input)      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">0L</td>
<td style="text-align: left;">1970-01-01 00:00:00 UTC</td>
</tr>
<tr class="even">
<td style="text-align: left;">60L</td>
<td style="text-align: left;">1970-01-01 00:01:00 UTC</td>
</tr>
<tr class="odd">
<td style="text-align: left;">-300L</td>
<td style="text-align: left;">1969-12-31 23:55:00 UTC</td>
</tr>
</tbody>
</table>

##### Node.js

``` javascript
const result = await db.pipeline()
  .collection("documents")
  .select(
    field("createdAtSeconds").unixSecondsToTimestamp().as("createdAtString")
  )
  .execute();test.firestore.js
```

### Web

``` javascript
const result = await execute(db.pipeline()
  .collection("documents")
  .select(
    field("createdAtSeconds").unixSecondsToTimestamp().as("createdAtString")
  )
);test.firestore.js
```

##### Swift

``` swift
let result = try await db.pipeline()
  .collection("documents")
  .select([
    Field("createdAtSeconds").unixSecondsToTimestamp().as("createdAtString")
  ])
  .execute()PipelineSnippets.swift
```

##### Kotlin  
Android

``` kotlin
val result = db.pipeline()
    .collection("documents")
    .select(
        field("createdAtSeconds").unixSecondsToTimestamp().alias("createdAtString")
    )
    .execute()DocSnippets.kt
```

##### Java  
Android

``` text
Task<Pipeline.Snapshot> result = db.pipeline()
    .collection("documents")
    .select(
        field("createdAtSeconds").unixSecondsToTimestamp().alias("createdAtString")
    )
    .execute();DocSnippets.java
```

##### Python

``` python
from google.cloud.firestore_v1.pipeline_expressions import Field

result = (
    client.pipeline()
    .collection("documents")
    .select(
        Field.of("createdAtSeconds")
        .unix_seconds_to_timestamp()
        .as_("createdAtString")
    )
    .execute()
)firestore_pipelines.py
```

##### Java

``` java
Pipeline.Snapshot result =
    firestore
        .pipeline()
        .collection("documents")
        .select(unixSecondsToTimestamp(field("createdAtSeconds")).as("createdAtString"))
        .execute()
        .get();PipelineSnippets.java
```

### TIMESTAMP\_ADD

**Syntax:**

``` text
timestamp_add(timestamp: TIMESTAMP, unit: STRING, amount: INT64) -> TIMESTAMP
```

**Description:**

Adds an `  amount  ` of `  unit  ` from `  timestamp  ` . The `  amount  ` argument can be negative, in that case it is equivalent to [TIMESTAMP\_SUB](#timestamp_sub) .

The `  unit  ` argument must be a string and one of the following:

  - `  microsecond  `
  - `  millisecond  `
  - `  second  `
  - `  minute  `
  - `  hour  `
  - `  day  `

Throws an error if the resulting timestamp does not fit within the `  TIMESTAMP  ` range.

**Examples:**

<table>
<thead>
<tr class="header">
<th style="text-align: left;"><code dir="ltr" translate="no">       timestamp      </code></th>
<th style="text-align: left;"><code dir="ltr" translate="no">       unit      </code></th>
<th style="text-align: left;"><code dir="ltr" translate="no">       amount      </code></th>
<th style="text-align: left;"><code dir="ltr" translate="no">       timestamp_add(timestamp, unit, amount)      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">2025-02-20 00:00:00 UTC</td>
<td style="text-align: left;">"minute"</td>
<td style="text-align: left;">2L</td>
<td style="text-align: left;">2025-02-20 00:02:00 UTC</td>
</tr>
<tr class="even">
<td style="text-align: left;">2025-02-20 00:00:00 UTC</td>
<td style="text-align: left;">"hour"</td>
<td style="text-align: left;">-4L</td>
<td style="text-align: left;">2025-02-19 20:00:00 UTC</td>
</tr>
<tr class="odd">
<td style="text-align: left;">2025-02-20 00:00:00 UTC</td>
<td style="text-align: left;">"day"</td>
<td style="text-align: left;">5L</td>
<td style="text-align: left;">2025-02-25 00:00:00 UTC</td>
</tr>
</tbody>
</table>

##### Node.js

``` javascript
const result = await db.pipeline()
  .collection("documents")
  .select(
    field("createdAt").timestampAdd("day", 3653).as("expiresAt")
  )
  .execute();test.firestore.js
```

### Web

``` javascript
const result = await execute(db.pipeline()
  .collection("documents")
  .select(
    field("createdAt").timestampAdd("day", 3653).as("expiresAt")
  )
);test.firestore.js
```

##### Swift

``` swift
let result = try await db.pipeline()
  .collection("documents")
  .select([
    Field("createdAt").timestampAdd(3653, .day).as("expiresAt")
  ])
  .execute()PipelineSnippets.swift
```

##### Kotlin  
Android

``` kotlin
val result = db.pipeline()
    .collection("documents")
    .select(
        field("createdAt")
          .timestampAdd("day", 3653)
          .alias("expiresAt")
    )
    .execute()DocSnippets.kt
```

##### Java  
Android

``` text
Task<Pipeline.Snapshot> result = db.pipeline()
    .collection("documents")
    .select(
        field("createdAt").timestampAdd("day", 3653).alias("expiresAt")
    )
    .execute();DocSnippets.java
```

##### Python

``` python
from google.cloud.firestore_v1.pipeline_expressions import Field

result = (
    client.pipeline()
    .collection("documents")
    .select(Field.of("createdAt").timestamp_add("day", 3653).as_("expiresAt"))
    .execute()
)firestore_pipelines.py
```

##### Java

``` java
Pipeline.Snapshot result =
    firestore
        .pipeline()
        .collection("documents")
        .select(timestampAdd(field("createdAt"), "day", 3653).as("expiresAt"))
        .execute()
        .get();PipelineSnippets.java
```

### TIMESTAMP\_SUB

**Syntax:**

``` text
timestamp_sub(timestamp: TIMESTAMP, unit: STRING, amount: INT64) -> TIMESTAMP
```

**Description:**

Subtracts an `  amount  ` of `  unit  ` from `  timestamp  ` . The `  amount  ` argument can be negative, in that case it is equivalent to [TIMESTAMP\_ADD](#timestamp_add) .

The `  unit  ` argument must be a string and one of the following:

  - `  microsecond  `
  - `  millisecond  `
  - `  second  `
  - `  minute  `
  - `  hour  `
  - `  day  `

Throws an error if the resulting timestamp does not fit within the `  TIMESTAMP  ` range.

**Examples:**

<table>
<thead>
<tr class="header">
<th style="text-align: left;"><code dir="ltr" translate="no">       timestamp      </code></th>
<th style="text-align: left;"><code dir="ltr" translate="no">       unit      </code></th>
<th style="text-align: left;"><code dir="ltr" translate="no">       amount      </code></th>
<th style="text-align: left;"><code dir="ltr" translate="no">       timestamp_sub(timestamp, unit, amount)      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">2026-07-04 00:00:00 UTC</td>
<td style="text-align: left;">"minute"</td>
<td style="text-align: left;">40L</td>
<td style="text-align: left;">2026-07-03 23:20:00 UTC</td>
</tr>
<tr class="even">
<td style="text-align: left;">2026-07-04 00:00:00 UTC</td>
<td style="text-align: left;">"hour"</td>
<td style="text-align: left;">-24L</td>
<td style="text-align: left;">2026-07-05 00:00:00 UTC</td>
</tr>
<tr class="odd">
<td style="text-align: left;">2026-07-04 00:00:00 UTC</td>
<td style="text-align: left;">"day"</td>
<td style="text-align: left;">3L</td>
<td style="text-align: left;">2026-07-01 00:00:00 UTC</td>
</tr>
</tbody>
</table>

##### Node.js

``` javascript
const result = await db.pipeline()
  .collection("documents")
  .select(
    field("expiresAt").timestampSubtract("day", 14).as("sendWarningTimestamp")
  )
  .execute();test.firestore.js
```

### Web

``` javascript
const result = await execute(db.pipeline()
  .collection("documents")
  .select(
    field("expiresAt").timestampSubtract("day", 14).as("sendWarningTimestamp")
  )
);test.firestore.js
```

##### Swift

``` swift
let result = try await db.pipeline()
  .collection("documents")
  .select([
    Field("expiresAt").timestampSubtract(14, .day).as("sendWarningTimestamp")
  ])
  .execute()PipelineSnippets.swift
```

##### Kotlin  
Android

``` kotlin
val result = db.pipeline()
    .collection("documents")
    .select(
        field("expiresAt")
          .timestampSubtract("day", 14)
          .alias("sendWarningTimestamp")
    )
    .execute()DocSnippets.kt
```

##### Java  
Android

``` text
Task<Pipeline.Snapshot> result = db.pipeline()
    .collection("documents")
    .select(
        field("expiresAt").timestampSubtract("day", 14).alias("sendWarningTimestamp")
    )
    .execute();DocSnippets.java
```

##### Python

``` python
from google.cloud.firestore_v1.pipeline_expressions import Field

result = (
    client.pipeline()
    .collection("documents")
    .select(
        Field.of("expiresAt")
        .timestamp_subtract("day", 14)
        .as_("sendWarningTimestamp")
    )
    .execute()
)firestore_pipelines.py
```

##### Java

``` java
Pipeline.Snapshot result =
    firestore
        .pipeline()
        .collection("documents")
        .select(timestampSubtract(field("expiresAt"), "day", 14).as("sendWarningTimestamp"))
        .execute()
        .get();PipelineSnippets.java
```

### TIMESTAMP\_TO\_UNIX\_MICROS

**Syntax:**

``` text
timestamp_to_unix_micros(input: TIMESTAMP) -> INT64
```

**Description:**

Converts `  input  ` to the number of microseconds since `  1970-01-01 00:00:00 UTC  ` . Truncates higher levels of precision by rounding down to the beginning of the microsecond.

**Examples:**

<table>
<thead>
<tr class="header">
<th style="text-align: left;"><code dir="ltr" translate="no">       input      </code></th>
<th style="text-align: left;"><code dir="ltr" translate="no">       timestamp_to_unix_micros(input)      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">1970-01-01 00:00:00 UTC</td>
<td style="text-align: left;">0L</td>
</tr>
<tr class="even">
<td style="text-align: left;">1970-01-01 00:06:40.123456 UTC</td>
<td style="text-align: left;">400123456L</td>
</tr>
<tr class="odd">
<td style="text-align: left;">1969-12-31 23:59:59 UTC</td>
<td style="text-align: left;">-1000000L</td>
</tr>
</tbody>
</table>

##### Node.js

``` javascript
const result = await db.pipeline()
  .collection("documents")
  .select(
    field("dateString").timestampToUnixMicros().as("unixMicros")
  )
  .execute();test.firestore.js
```

### Web

``` javascript
const result = await execute(db.pipeline()
  .collection("documents")
  .select(
    field("dateString").timestampToUnixMicros().as("unixMicros")
  )
);test.firestore.js
```

##### Swift

``` swift
let result = try await db.pipeline()
  .collection("documents")
  .select([
    Field("dateString").timestampToUnixMicros().as("unixMicros")
  ])
  .execute()PipelineSnippets.swift
```

##### Kotlin  
Android

``` kotlin
val result = db.pipeline()
    .collection("documents")
    .select(
        field("dateString").timestampToUnixMicros().alias("unixMicros")
    )
    .execute()DocSnippets.kt
```

##### Java  
Android

``` text
Task<Pipeline.Snapshot> result = db.pipeline()
    .collection("documents")
    .select(
        field("dateString").timestampToUnixMicros().alias("unixMicros")
    )
    .execute();DocSnippets.java
```

##### Python

``` python
from google.cloud.firestore_v1.pipeline_expressions import Field

result = (
    client.pipeline()
    .collection("documents")
    .select(Field.of("dateString").timestamp_to_unix_micros().as_("unixMicros"))
    .execute()
)firestore_pipelines.py
```

##### Java

``` java
Pipeline.Snapshot result =
    firestore
        .pipeline()
        .collection("documents")
        .select(timestampToUnixMicros(field("dateString")).as("unixMicros"))
        .execute()
        .get();PipelineSnippets.java
```

### TIMESTAMP\_TO\_UNIX\_MILLIS

**Syntax:**

``` text
timestamp_to_unix_millis(input: TIMESTAMP) -> INT64
```

**Description:**

Converts `  input  ` to the number of milliseconds since `  1970-01-01 00:00:00 UTC  ` . Truncates higher levels of precision by rounding down to the beginning of the millisecond.

**Examples:**

<table>
<thead>
<tr class="header">
<th style="text-align: left;"><code dir="ltr" translate="no">       input      </code></th>
<th style="text-align: left;"><code dir="ltr" translate="no">       timestamp_to_unix_millis(input)      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">1970-01-01 00:00:00 UTC</td>
<td style="text-align: left;">0L</td>
</tr>
<tr class="even">
<td style="text-align: left;">1970-01-01 01:06:40.123 UTC</td>
<td style="text-align: left;">4000123L</td>
</tr>
<tr class="odd">
<td style="text-align: left;">1969-12-31 23:43:20</td>
<td style="text-align: left;">-1000000L</td>
</tr>
</tbody>
</table>

##### Node.js

``` javascript
const result = await db.pipeline()
  .collection("documents")
  .select(
    field("dateString").timestampToUnixMillis().as("unixMillis")
  )
  .execute();test.firestore.js
```

### Web

``` javascript
const result = await execute(db.pipeline()
  .collection("documents")
  .select(
    field("dateString").timestampToUnixMillis().as("unixMillis")
  )
);test.firestore.js
```

##### Swift

``` swift
let result = try await db.pipeline()
  .collection("documents")
  .select([
    Field("dateString").timestampToUnixMillis().as("unixMillis")
  ])
  .execute()PipelineSnippets.swift
```

##### Kotlin  
Android

``` kotlin
val result = db.pipeline()
    .collection("documents")
    .select(
        field("dateString").timestampToUnixMillis().alias("unixMillis")
    )
    .execute()DocSnippets.kt
```

##### Java  
Android

``` text
Task<Pipeline.Snapshot> result = db.pipeline()
    .collection("documents")
    .select(
        field("dateString").timestampToUnixMillis().alias("unixMillis")
    )
    .execute();DocSnippets.java
```

##### Python

``` python
from google.cloud.firestore_v1.pipeline_expressions import Field

result = (
    client.pipeline()
    .collection("documents")
    .select(Field.of("dateString").timestamp_to_unix_millis().as_("unixMillis"))
    .execute()
)firestore_pipelines.py
```

##### Java

``` java
Pipeline.Snapshot result =
    firestore
        .pipeline()
        .collection("documents")
        .select(timestampToUnixMillis(field("dateString")).as("unixMillis"))
        .execute()
        .get();PipelineSnippets.java
```

### TIMESTAMP\_TO\_UNIX\_SECONDS

**Syntax:**

``` text
timestamp_to_unix_seconds(input: TIMESTAMP) -> INT64
```

**Description:**

Converts `  input  ` to the number of seconds since `  1970-01-01 00:00:00 UTC  ` . Truncates higher levels of precision by rounding down to the beginning of the second.

**Examples:**

<table>
<thead>
<tr class="header">
<th style="text-align: left;"><code dir="ltr" translate="no">       input      </code></th>
<th style="text-align: left;"><code dir="ltr" translate="no">       timestamp_to_unix_seconds(input)      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">1970-01-01 00:00:00 UTC</td>
<td style="text-align: left;">0L</td>
</tr>
<tr class="even">
<td style="text-align: left;">1970-01-01 00:01:00 UTC</td>
<td style="text-align: left;">60L</td>
</tr>
<tr class="odd">
<td style="text-align: left;">1969-12-31 23:55:00 UTC</td>
<td style="text-align: left;">-300L</td>
</tr>
</tbody>
</table>

##### Node.js

``` javascript
const result = await db.pipeline()
  .collection("documents")
  .select(
    field("dateString").timestampToUnixSeconds().as("unixSeconds")
  )
  .execute();test.firestore.js
```

### Web

``` javascript
const result = await execute(db.pipeline()
  .collection("documents")
  .select(
    field("dateString").timestampToUnixSeconds().as("unixSeconds")
  )
);test.firestore.js
```

##### Swift

``` swift
let result = try await db.pipeline()
  .collection("documents")
  .select([
    Field("dateString").timestampToUnixSeconds().as("unixSeconds")
  ])
  .execute()PipelineSnippets.swift
```

##### Kotlin  
Android

``` kotlin
val result = db.pipeline()
    .collection("documents")
    .select(
        field("dateString").timestampToUnixSeconds().alias("unixSeconds")
    )
    .execute()DocSnippets.kt
```

##### Java  
Android

``` text
Task<Pipeline.Snapshot> result = db.pipeline()
    .collection("documents")
    .select(
        field("dateString").timestampToUnixSeconds().alias("unixSeconds")
    )
    .execute();DocSnippets.java
```

##### Python

``` python
from google.cloud.firestore_v1.pipeline_expressions import Field

result = (
    client.pipeline()
    .collection("documents")
    .select(Field.of("dateString").timestamp_to_unix_seconds().as_("unixSeconds"))
    .execute()
)firestore_pipelines.py
```

##### Java

``` java
Pipeline.Snapshot result =
    firestore
        .pipeline()
        .collection("documents")
        .select(timestampToUnixSeconds(field("dateString")).as("unixSeconds"))
        .execute()
        .get();PipelineSnippets.java
```

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

## **Vector Functions**

<table>
<tbody>
<tr class="odd">
<td>Name</td>
<td>Description</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         COSINE_DISTANCE       </code></td>
<td>Returns the cosine distance between two vectors</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         DOT_PRODUCT       </code></td>
<td>Returns the dot product between two vectors</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         EUCLIDEAN_DISTANCE       </code></td>
<td>Returns the euclidean distance between two vectors</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         MANHATTAN_DISTANCE       </code></td>
<td>Returns the manhattan distance between two vectors</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         VECTOR_LENGTH       </code></td>
<td>Returns the number of elements in a vector</td>
</tr>
</tbody>
</table>

### COSINE\_DISTANCE

**Syntax:**

``` text
cosine_distance(x: VECTOR, y: VECTOR) -> FLOAT64
```

**Description:**

Returns the cosine distance between `  x  ` and `  y  ` .

##### Node.js

``` javascript
const sampleVector = [0.0, 1, 2, 3, 4, 5];
const result = await db.pipeline()
  .collection("books")
  .select(
    field("embedding").cosineDistance(sampleVector).as("cosineDistance")
  )
  .execute();test.firestore.js
```

### Web

``` javascript
const sampleVector = [0.0, 1, 2, 3, 4, 5];
const result = await execute(db.pipeline()
  .collection("books")
  .select(
    field("embedding").cosineDistance(sampleVector).as("cosineDistance")));test.firestore.js
```

##### Swift

``` swift
let sampleVector = [0.0, 1, 2, 3, 4, 5]
let result = try await db.pipeline()
  .collection("books")
  .select([
    Field("embedding").cosineDistance(sampleVector).as("cosineDistance")
  ])
  .execute()PipelineSnippets.swift
```

##### Kotlin  
Android

``` kotlin
val sampleVector = doubleArrayOf(0.0, 1.0, 2.0, 3.0, 4.0, 5.0)
val result = db.pipeline()
    .collection("books")
    .select(
        field("embedding").cosineDistance(sampleVector).alias("cosineDistance")
    )
    .execute()DocSnippets.kt
```

##### Java  
Android

``` text
double[] sampleVector = {0.0, 1.0, 2.0, 3.0, 4.0, 5.0};
Task<Pipeline.Snapshot> result = db.pipeline()
    .collection("books")
    .select(
        field("embedding").cosineDistance(sampleVector).alias("cosineDistance")
    )
    .execute();DocSnippets.java
```

##### Python

``` python
from google.cloud.firestore_v1.pipeline_expressions import Field
from google.cloud.firestore_v1.vector import Vector

sample_vector = Vector([0.0, 1.0, 2.0, 3.0, 4.0, 5.0])
result = (
    client.pipeline()
    .collection("books")
    .select(
        Field.of("embedding").cosine_distance(sample_vector).as_("cosineDistance")
    )
    .execute()
)firestore_pipelines.py
```

##### Java

``` java
double[] sampleVector = new double[] {0.0, 1.0, 2.0, 3.0, 4.0, 5.0};
Pipeline.Snapshot result =
    firestore
        .pipeline()
        .collection("books")
        .select(cosineDistance(field("embedding"), sampleVector).as("cosineDistance"))
        .execute()
        .get();PipelineSnippets.java
```

### DOT\_PRODUCT

**Syntax:**

``` text
dot_product(x: VECTOR, y: VECTOR) -> FLOAT64
```

**Description:**

Returns the dot product of `  x  ` and `  y  ` .

##### Node.js

``` javascript
const sampleVector = [0.0, 1, 2, 3, 4, 5];
const result = await db.pipeline()
  .collection("books")
  .select(
    field("embedding").dotProduct(sampleVector).as("dotProduct")
  )
  .execute();test.firestore.js
```

### Web

``` javascript
const sampleVector = [0.0, 1, 2, 3, 4, 5];
const result = await execute(db.pipeline()
  .collection("books")
  .select(
    field("embedding").dotProduct(sampleVector).as("dotProduct")
  )
);test.firestore.js
```

##### Swift

``` swift
let sampleVector = [0.0, 1, 2, 3, 4, 5]
let result = try await db.pipeline()
  .collection("books")
  .select([
    Field("embedding").dotProduct(sampleVector).as("dotProduct")
  ])
  .execute()PipelineSnippets.swift
```

##### Kotlin  
Android

``` kotlin
val sampleVector = doubleArrayOf(0.0, 1.0, 2.0, 3.0, 4.0, 5.0)
val result = db.pipeline()
    .collection("books")
    .select(
        field("embedding").dotProduct(sampleVector).alias("dotProduct")
    )
    .execute()DocSnippets.kt
```

##### Java  
Android

``` text
double[] sampleVector = {0.0, 1.0, 2.0, 3.0, 4.0, 5.0};
Task<Pipeline.Snapshot> result = db.pipeline()
    .collection("books")
    .select(
        field("embedding").dotProduct(sampleVector).alias("dotProduct")
    )
    .execute();DocSnippets.java
```

##### Python

``` python
from google.cloud.firestore_v1.pipeline_expressions import Field
from google.cloud.firestore_v1.vector import Vector

sample_vector = Vector([0.0, 1.0, 2.0, 3.0, 4.0, 5.0])
result = (
    client.pipeline()
    .collection("books")
    .select(Field.of("embedding").dot_product(sample_vector).as_("dotProduct"))
    .execute()
)firestore_pipelines.py
```

##### Java

``` java
double[] sampleVector = new double[] {0.0, 1.0, 2.0, 3.0, 4.0, 5.0};
Pipeline.Snapshot result =
    firestore
        .pipeline()
        .collection("books")
        .select(dotProduct(field("embedding"), sampleVector).as("dotProduct"))
        .execute()
        .get();PipelineSnippets.java
```

### EUCLIDEAN\_DISTANCE

**Syntax:**

``` text
euclidean_distance(x: VECTOR, y: VECTOR) -> FLOAT64
```

**Description:**

Computes the euclidean distance between `  x  ` and `  y  ` .

##### Node.js

``` javascript
const sampleVector = [0.0, 1, 2, 3, 4, 5];
const result = await db.pipeline()
  .collection("books")
  .select(
    field("embedding").euclideanDistance(sampleVector).as("euclideanDistance")
  )
  .execute();test.firestore.js
```

### Web

``` javascript
const sampleVector = [0.0, 1, 2, 3, 4, 5];
const result = await execute(db.pipeline()
  .collection("books")
  .select(
    field("embedding").euclideanDistance(sampleVector).as("euclideanDistance")
  )
);test.firestore.js
```

##### Swift

``` swift
let sampleVector = [0.0, 1, 2, 3, 4, 5]
let result = try await db.pipeline()
  .collection("books")
  .select([
    Field("embedding").euclideanDistance(sampleVector).as("euclideanDistance")
  ])
  .execute()PipelineSnippets.swift
```

##### Kotlin  
Android

``` kotlin
val sampleVector = doubleArrayOf(0.0, 1.0, 2.0, 3.0, 4.0, 5.0)
val result = db.pipeline()
    .collection("books")
    .select(
        field("embedding").euclideanDistance(sampleVector).alias("euclideanDistance")
    )
    .execute()DocSnippets.kt
```

##### Java  
Android

``` text
double[] sampleVector = {0.0, 1.0, 2.0, 3.0, 4.0, 5.0};
Task<Pipeline.Snapshot> result = db.pipeline()
    .collection("books")
    .select(
        field("embedding").euclideanDistance(sampleVector).alias("euclideanDistance")
    )
    .execute();DocSnippets.java
```

##### Python

``` python
from google.cloud.firestore_v1.pipeline_expressions import Field
from google.cloud.firestore_v1.vector import Vector

sample_vector = Vector([0.0, 1.0, 2.0, 3.0, 4.0, 5.0])
result = (
    client.pipeline()
    .collection("books")
    .select(
        Field.of("embedding")
        .euclidean_distance(sample_vector)
        .as_("euclideanDistance")
    )
    .execute()
)firestore_pipelines.py
```

##### Java

``` java
double[] sampleVector = new double[] {0.0, 1.0, 2.0, 3.0, 4.0, 5.0};
Pipeline.Snapshot result =
    firestore
        .pipeline()
        .collection("books")
        .select(euclideanDistance(field("embedding"), sampleVector).as("euclideanDistance"))
        .execute()
        .get();PipelineSnippets.java
```

### MANHATTAN\_DISTANCE

**Syntax:**

``` text
manhattan_distance(x: VECTOR, y: VECTOR) -> FLOAT64
```

**Description:**

Computes the manhattan distance between `  x  ` and `  y  ` .

### VECTOR\_LENGTH

**Syntax:**

``` text
vector_length(vector: VECTOR) -> INT64
```

**Description:**

Returns the number of elements in a `  VECTOR  ` .

##### Node.js

``` javascript
const result = await db.pipeline()
  .collection("books")
  .select(
    field("embedding").vectorLength().as("vectorLength")
  )
  .execute();test.firestore.js
```

### Web

``` javascript
const result = await execute(db.pipeline()
  .collection("books")
  .select(
    field("embedding").vectorLength().as("vectorLength")
  )
);test.firestore.js
```

##### Swift

``` swift
let result = try await db.pipeline()
  .collection("books")
  .select([
    Field("embedding").vectorLength().as("vectorLength")
  ])
  .execute()PipelineSnippets.swift
```

##### Kotlin  
Android

``` kotlin
val result = db.pipeline()
    .collection("books")
    .select(
        field("embedding").vectorLength().alias("vectorLength")
    )
    .execute()DocSnippets.kt
```

##### Java  
Android

``` text
Task<Pipeline.Snapshot> result = db.pipeline()
    .collection("books")
    .select(
        field("embedding").vectorLength().alias("vectorLength")
    )
    .execute();DocSnippets.java
```

##### Python

``` python
from google.cloud.firestore_v1.pipeline_expressions import Field

result = (
    client.pipeline()
    .collection("books")
    .select(Field.of("embedding").vector_length().as_("vectorLength"))
    .execute()
)firestore_pipelines.py
```

##### Java

``` java
Pipeline.Snapshot result =
    firestore
        .pipeline()
        .collection("books")
        .select(vectorLength(field("embedding")).as("vectorLength"))
        .execute()
        .get();PipelineSnippets.java
```

## What's next

  - See the [Pipeline Queries overview](/firestore/docs/pipeline/overview)
