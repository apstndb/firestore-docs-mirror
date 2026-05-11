---
name: documents/docs.cloud.google.com/firestore/native/docs/pipeline/functions/debugging_functions
uri: https://docs.cloud.google.com/firestore/native/docs/pipeline/functions/debugging_functions
title: Debugging Functions Reference
description: Explains how to use debugging functions like EXISTS, IS_ABSENT, and ERROR in Firestore Pipeline operations.
data_source: docs.cloud.google.com
---

# Debugging Functions Reference

## **Debugging Functions**

|                              |                                                                             |
| ---------------------------- | --------------------------------------------------------------------------- |
| Name                         | Description                                                                 |
| `         EXISTS        `    | Returns `TRUE` if the value is not an absent value                          |
| `         IS_ABSENT        ` | Returns `TRUE` if the value is an absent value                              |
| `         IF_ABSENT        ` | Replaces the value with an expression if it is absent                       |
| `         IS_ERROR        `  | Catches and checks if an error has been thrown by the underlying expression |
| `         IF_ERROR        `  | Replaces the value with an expression if it has thrown an error             |
| `         ERROR        `     | Terminates evaluation and returns an error with the specified message       |

### EXISTS

**Syntax:**

    exists(value: ANY) -> BOOLEAN

**Description:**

Returns `TRUE` if `value` is not the absent value.

**Examples:**

| `value`  | `exists(value)` |
| :------- | :-------------- |
| 0L       | `TRUE`          |
| "foo"    | `TRUE`          |
| `NULL`   | `TRUE`          |
| `ABSENT` | `FALSE`         |

##### Node.js

    const result = await db.pipeline()
      .collection("books")
      .select(field("rating").exists().as("hasRating"))
      .execute();

### Web

**Example:**

    const result = await execute(db.pipeline()
      .collection("books")
      .select(field("rating").exists().as("hasRating"))
    );

##### Swift

    let result = try await db.pipeline()
      .collection("books")
      .select([Field("rating").exists().as("hasRating")])
      .execute()

##### Kotlin  
Android

**Example:**

    val result = db.pipeline()
        .collection("books")
        .select(field("rating").exists().alias("hasRating"))
        .execute()

##### Java  
Android

**Example:**

    Task<Pipeline.Snapshot> result = db.pipeline()
        .collection("books")
        .select(field("rating").exists().alias("hasRating"))
        .execute();

##### Python

    from google.cloud.firestore_v1.pipeline_expressions import Field
    
    result = (
        client.pipeline()
        .collection("books")
        .select(Field.of("rating").exists().as_("hasRating"))
        .execute()
    )

##### Java

    Pipeline.Snapshot result =
        firestore
            .pipeline()
            .collection("books")
            .select(exists(field("rating")).as("hasRating"))
            .execute()
            .get();

### IS\_ABSENT

**Syntax:**

    is_absent(value: ANY) -> BOOLEAN

**Description:**

Returns `TRUE` if `value` is the absent value, and `FALSE` otherwise. Absent values are values that are missing from the input, such as a missing document field.

**Examples:**

| `value`  | `is_absent(value)` |
| :------- | :----------------- |
| 0L       | `FALSE`            |
| "foo"    | `FALSE`            |
| `NULL`   | `FALSE`            |
| `ABSENT` | `TRUE`             |

### IF\_ABSENT

**Syntax:**

    if_absent(value: ANY, replacement: ANY) -> ANY

**Description:**

If `value` is an absent value, evaluates and returns `replacement` . Otherwise returns `value` .

**Examples:**

| `value`  | `replacement` | `if_absent(value, replacement)` |
| :------- | :------------ | :------------------------------ |
| 5L       | 0L            | 5L                              |
| `NULL`   | 0L            | `NULL`                          |
| `ABSENT` | 0L            | 0L                              |

### IS\_ERROR

**Syntax:**

    is_error(try: ANY) -> BOOLEAN

**Description:**

Returns `TRUE` if an error is thrown during the evaluation of `try` . Returns `FALSE` otherwise.

### IF\_ERROR

**Syntax:**

    if_error(try: ANY, catch: ANY) -> ANY

**Description:**

If an error is thrown during the evaluation of `try` , evaluates and returns `replacement` . Otherwise returns the resolved value of `try` .

### ERROR

**Syntax:**

    error(message: STRING) -> ANY

**Description:**

Evaluation of the `error` function results in the evaluation of the pipeline to terminate with an error. The given `message` is included in the error.

**Examples:**

| `cond`  | `res` | `switch_on(cond, res, error("no condition matched"))` |
| :------ | :---- | :---------------------------------------------------- |
| `TRUE`  | 1L    | 1L                                                    |
| `FALSE` | 1L    | `ERROR ("no condition matched")`                      |

## What's next

  - See the [Pipeline Queries overview](https://docs.cloud.google.com/firestore/docs/pipeline/overview)
