# Generic Functions Reference

**Preview — Firestore in Native mode (with Pipeline Operations) for Enterprise Edition**

This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . You can process personal data for this feature as outlined in the [Cloud Data Processing Addendum](https://docs.cloud.google.com/terms/data-processing-addendum) , subject to the obligations and restrictions described in the agreement under which you access Google Cloud. Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

## **Generic Functions**

|                                     |                                                                                 |
| ----------------------------------- | ------------------------------------------------------------------------------- |
| Name                                | Description                                                                     |
| `         CURRENT_DOCUMENT        ` | Returns the document currently being processed in the pipeline.                 |
| `         CONCAT        `           | Concatenates two or more values of same type.                                   |
| `         LENGTH        `           | Calculates the length of a `String` , `Bytes` , `Array` , `Vector` , or `Map` . |
| `         REVERSE        `          | Reverses a `String` , `Bytes` , or `Array` .                                    |

### CURRENT\_DOCUMENT

**Syntax:**

    current_document() -> MAP

**Description:**

Evaluates to a map that holds all fields defined in the current scope. This is useful when merging or aggregating multiple documents together or when wanting to dynamically inspect the field names in the document.

For example, to get a list of documents grouped by a field:

### Node.js

    const cities = await db.pipeline()
      .collection("/restaurants")
      .aggregate({
        groups: [ field("location.state").as("state") ],
        accumulators: [ arrayAgg(currentDocument().as("restaurants")) ]
       })
      .execute();

### CONCAT

**Syntax:**

    concat[T <: STRING | BYTES | ARRAY](values:T ...) -> T

**Description:**

Concatenates two or more values of same type.

**Examples:**

| values                  | `concat(values)` |
| :---------------------- | :--------------- |
| "abc", "def"            | "abcdef"         |
| \[1, 2\], \[3, 4\]      | \[1, 2, 3, 4\]   |
| b"abc", b"def"          | b"abcdef"        |
| "abc", \[1,2,3\], "ghi" | error            |
| \[1,2,3\]               | error            |
| "abc", null             | null             |

##### Node.js

    concat(constant("Author ID: "), field("authorId"));test.firestore.js

### Web

    concat(constant("Author ID: "), field("authorId"));test.firestore.js

##### Swift

    let displayString = Constant("Author ID: ").concat([Field("authorId")])PipelineSnippets.swift

##### Kotlin  
Android

    val displayString = constant("Author ID: ").concat(field("authorId"))
    DocSnippets.kt

##### Java  
Android

    Expression displayString = constant("Author ID: ").concat(field("authorId"));DocSnippets.java

##### Python

    Constant.of("Author ID: ").concat(Field.of("authorId"))firestore_pipelines.py

### LENGTH

**Syntax:**

    length[T <: STRING | BYTES | ARRAY | VECTOR | MAP](value: T) -> INT64

**Description:**

Calculates the length of a `String` , `Bytes` , `Array` , `Vector` , or `Map` value.

**Examples:**

| value          | `length(value)` |
| :------------- | :-------------- |
| "hello"        | 5               |
| \[1, 2, 3, 4\] | 4               |
| b"abcde"       | 5               |
| null           | null            |
| 1              | error           |

### REVERSE

**Syntax:**

    reverse[T <: STRING | BYTES | ARRAY](value: T) -> T

**Description:**

Reverses a `String` , `Bytes` , or `Array` value.

**Examples:**

| value       | `reverse(value)` |
| :---------- | :--------------- |
| "hello"     | "olleh"          |
| \[1, 2, 3\] | \[3, 2, 1\]      |
| b"abc"      | b"cba"           |
| 23          | error            |
| null        | null             |

## What's next

  - See the [Pipeline Queries overview](https://docs.cloud.google.com/firestore/docs/pipeline/overview)
