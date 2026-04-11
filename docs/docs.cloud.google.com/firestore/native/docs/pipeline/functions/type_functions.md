# Type Functions Reference

**Preview — Firestore in Native mode (with Pipeline Operations) for Enterprise Edition**

This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . You can process personal data for this feature as outlined in the [Cloud Data Processing Addendum](https://docs.cloud.google.com/terms/data-processing-addendum) , subject to the obligations and restrictions described in the agreement under which you access Google Cloud. Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

## **Type Functions**

|                            |                                                         |
| -------------------------- | ------------------------------------------------------- |
| Name                       | Description                                             |
| `         TYPE        `    | Returns the type of the value as a `STRING` .           |
| `         IS_TYPE        ` | Returns `true` if the value matches the specified type. |

### TYPE

**Syntax:**

    type(input: ANY) -> STRING

**Description:**

Returns a string representation of the `input` type.

If given an absent value, returns `NULL` .

**Examples:**

| `input`                  | `type(input)` |
| ------------------------ | ------------- |
| NULL                     | "null"        |
| true                     | "boolean"     |
| 1                        | "int32"       |
| \-3L                     | "int64"       |
| 3.14                     | "float64"     |
| 2024-01-01T00:00:00Z UTC | "timestamp"   |
| "foo"                    | "string"      |
| b"foo"                   | "bytes"       |
| \[1, 2\]                 | "array"       |
| {"a": 1}                 | "map"         |
| `path("c/d")`            | "reference"   |
| `vector([1.0, 2.0])`     | "vector"      |
| ABSENT                   | NULL          |

**Client examples**

##### Node.js

    const result = await db.pipeline()
      .collection("books")
      .select(field("title").notEqual("1984").as("not1984"))
      .execute();test.firestore.js

### Web

    const result = await execute(db.pipeline()
      .collection("books")
      .select(field("title").notEqual("1984").as("not1984"))
    );test.firestore.js

##### Swift

    let result = try await db.pipeline()
      .collection("books")
      .select([Field("title").notEqual("1984").as("not1984")])
      .execute()PipelineSnippets.swift

##### Kotlin  
Android

    val result = db.pipeline()
        .collection("books")
        .select(field("title").notEqual("1984").alias("not1984"))
        .execute()DocSnippets.kt

##### Java  
Android

    Task<Pipeline.Snapshot> result = db.pipeline()
        .collection("books")
        .select(field("title").notEqual("1984").alias("not1984"))
        .execute();DocSnippets.java

##### Python

    from google.cloud.firestore_v1.pipeline_expressions import Field
    
    result = (
        client.pipeline()
        .collection("books")
        .select(Field.of("title").not_equal("1984").as_("not1984"))
        .execute()
    )firestore_pipelines.py

##### Java

    Pipeline.Snapshot result =
        firestore
            .pipeline()
            .collection("books")
            .select(notEqual(field("title"), "1984").as("not1984"))
            .execute()
            .get();PipelineSnippets.java

### IS\_TYPE

**Syntax:**

    is_type(input: ANY, type: STRING) -> BOOLEAN

**Description:**

Returns `true` if the `input` matches the specified `type` , otherwise `false` . If given an absent `input` , returns `NULL` .

Supported `type` strings are:

  - `"null"`
  - `"boolean"`
  - `"int32"`
  - `"int64"`
  - `"float64"`
  - `"decimal128"`
  - `"number"`
  - `"timestamp"`
  - `"string"`
  - `"bytes"`
  - `"array"`
  - `"map"`
  - `"reference"`
  - `"vector"`
  - `"geo_point"`
  - `"max_key"`
  - `"min_key"`
  - `"object_id"`
  - `"regex"`
  - `"bson_timestamp"`

**Examples:**

| `input`              | `type`    | `is_type(input, type)` |
| :------------------- | :-------- | :--------------------- |
| NULL                 | "null"    | true                   |
| true                 | "boolean" | true                   |
| 3.14                 | "float64" | true                   |
| "foo"                | "string"  | true                   |
| b"foo"               | "string"  | false                  |
| \[1, 2\]             | "array"   | true                   |
| {"a": 1}             | "map"     | true                   |
| `vector([1.0, 2.0])` | "vector"  | true                   |
| ABSENT               | "string"  | NULL                   |
| "bar"                | "other"   | ERROR                  |

## What's next

  - See the [Pipeline Queries overview](https://docs.cloud.google.com/firestore/docs/pipeline/overview)
