# String Functions Reference

**Preview — Firestore in Native mode (with Pipeline Operations) for Enterprise Edition**

This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](/terms/service-terms#1) . You can process personal data for this feature as outlined in the [Cloud Data Processing Addendum](/terms/data-processing-addendum) , subject to the obligations and restrictions described in the agreement under which you access Google Cloud. Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

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

## What's next

  - See the [Pipeline Queries overview](/firestore/docs/pipeline/overview)
