# Arithmetic Functions Reference

**Preview — Firestore in Native mode (with Pipeline Operations) for Enterprise Edition**

This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](/terms/service-terms#1) . You can process personal data for this feature as outlined in the [Cloud Data Processing Addendum](/terms/data-processing-addendum) , subject to the obligations and restrictions described in the agreement under which you access Google Cloud. Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

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

## What's next

  - See the [Pipeline Queries overview](/firestore/docs/pipeline/overview)
