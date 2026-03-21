# Generic Functions Reference

**Preview — Firestore in Native mode (with Pipeline Operations) for Enterprise Edition**

This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](/terms/service-terms#1) . You can process personal data for this feature as outlined in the [Cloud Data Processing Addendum](/terms/data-processing-addendum) , subject to the obligations and restrictions described in the agreement under which you access Google Cloud. Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

## **Generic Functions**

<table>
<tbody>
<tr class="odd">
<td>Name</td>
<td>Description</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         CURRENT_DOCUMENT       </code></td>
<td>Returns the document currently being processed in the pipeline.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         CONCAT       </code></td>
<td>Concatenates two or more values of same type.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         LENGTH       </code></td>
<td>Calculates the length of a <code dir="ltr" translate="no">       String      </code> , <code dir="ltr" translate="no">       Bytes      </code> , <code dir="ltr" translate="no">       Array      </code> , <code dir="ltr" translate="no">       Vector      </code> , or <code dir="ltr" translate="no">       Map      </code> .</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         REVERSE       </code></td>
<td>Reverses a <code dir="ltr" translate="no">       String      </code> , <code dir="ltr" translate="no">       Bytes      </code> , or <code dir="ltr" translate="no">       Array      </code> .</td>
</tr>
</tbody>
</table>

### CURRENT\_DOCUMENT

**Syntax:**

``` text
current_document() -> MAP
```

**Description:**

Evaluates to a map that holds all fields defined in the current scope. This is useful when merging or aggregating multiple documents together or when wanting to dynamically inspect the field names in the document.

For example, to get a list of documents grouped by a field:

### Node.js

``` text
const cities = await db.pipeline()
  .collection("/restaurants")
  .aggregate({
    groups: [ field("location.state").as("state") ],
    accumulators: [ arrayAgg(currentDocument().as("restaurants")) ]
   })
  .execute();
```

### CONCAT

**Syntax:**

``` text
concat[T <: STRING | BYTES | ARRAY](values:T ...) -> T
```

**Description:**

Concatenates two or more values of same type.

**Examples:**

<table>
<thead>
<tr class="header">
<th style="text-align: left;">values</th>
<th style="text-align: left;"><code dir="ltr" translate="no">       concat(values)      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">"abc", "def"</td>
<td style="text-align: left;">"abcdef"</td>
</tr>
<tr class="even">
<td style="text-align: left;">[1, 2], [3, 4]</td>
<td style="text-align: left;">[1, 2, 3, 4]</td>
</tr>
<tr class="odd">
<td style="text-align: left;">b"abc", b"def"</td>
<td style="text-align: left;">b"abcdef"</td>
</tr>
<tr class="even">
<td style="text-align: left;">"abc", [1,2,3], "ghi"</td>
<td style="text-align: left;">error</td>
</tr>
<tr class="odd">
<td style="text-align: left;">[1,2,3]</td>
<td style="text-align: left;">error</td>
</tr>
<tr class="even">
<td style="text-align: left;">"abc", null</td>
<td style="text-align: left;">null</td>
</tr>
</tbody>
</table>

##### Node.js

``` javascript
concat(constant("Author ID: "), field("authorId"));test.firestore.js
```

### Web

``` javascript
concat(constant("Author ID: "), field("authorId"));test.firestore.js
```

##### Swift

``` swift
let displayString = Constant("Author ID: ").concat([Field("authorId")])PipelineSnippets.swift
```

##### Kotlin  
Android

``` kotlin
val displayString = constant("Author ID: ").concat(field("authorId"))
DocSnippets.kt
```

##### Java  
Android

``` text
Expression displayString = constant("Author ID: ").concat(field("authorId"));DocSnippets.java
```

##### Python

``` python
Constant.of("Author ID: ").concat(Field.of("authorId"))firestore_pipelines.py
```

### LENGTH

**Syntax:**

``` text
length[T <: STRING | BYTES | ARRAY | VECTOR | MAP](value: T) -> INT64
```

**Description:**

Calculates the length of a `  String  ` , `  Bytes  ` , `  Array  ` , `  Vector  ` , or `  Map  ` value.

**Examples:**

<table>
<thead>
<tr class="header">
<th style="text-align: left;">value</th>
<th style="text-align: left;"><code dir="ltr" translate="no">       length(value)      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">"hello"</td>
<td style="text-align: left;">5</td>
</tr>
<tr class="even">
<td style="text-align: left;">[1, 2, 3, 4]</td>
<td style="text-align: left;">4</td>
</tr>
<tr class="odd">
<td style="text-align: left;">b"abcde"</td>
<td style="text-align: left;">5</td>
</tr>
<tr class="even">
<td style="text-align: left;">null</td>
<td style="text-align: left;">null</td>
</tr>
<tr class="odd">
<td style="text-align: left;">1</td>
<td style="text-align: left;">error</td>
</tr>
</tbody>
</table>

### REVERSE

**Syntax:**

``` text
reverse[T <: STRING | BYTES | ARRAY](value: T) -> T
```

**Description:**

Reverses a `  String  ` , `  Bytes  ` , or `  Array  ` value.

**Examples:**

<table>
<thead>
<tr class="header">
<th style="text-align: left;">value</th>
<th style="text-align: left;"><code dir="ltr" translate="no">       reverse(value)      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">"hello"</td>
<td style="text-align: left;">"olleh"</td>
</tr>
<tr class="even">
<td style="text-align: left;">[1, 2, 3]</td>
<td style="text-align: left;">[3, 2, 1]</td>
</tr>
<tr class="odd">
<td style="text-align: left;">b"abc"</td>
<td style="text-align: left;">b"cba"</td>
</tr>
<tr class="even">
<td style="text-align: left;">23</td>
<td style="text-align: left;">error</td>
</tr>
<tr class="odd">
<td style="text-align: left;">null</td>
<td style="text-align: left;">null</td>
</tr>
</tbody>
</table>

## What's next

  - See the [Pipeline Queries overview](/firestore/docs/pipeline/overview)
