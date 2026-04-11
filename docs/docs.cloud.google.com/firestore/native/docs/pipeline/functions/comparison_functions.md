# Comparison Functions Reference

**Preview — Firestore in Native mode (with Pipeline Operations) for Enterprise Edition**

This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . You can process personal data for this feature as outlined in the [Cloud Data Processing Addendum](https://docs.cloud.google.com/terms/data-processing-addendum) , subject to the obligations and restrictions described in the agreement under which you access Google Cloud. Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

## **Comparison Functions**

|                                          |                                  |
| ---------------------------------------- | -------------------------------- |
| Name                                     | Description                      |
| `         EQUAL        `                 | Equality comparison              |
| `         GREATER_THAN        `          | Greater than comparison          |
| `         GREATER_THAN_OR_EQUAL        ` | Greater than or equal comparison |
| `         LESS_THAN        `             | Less than comparison             |
| `         LESS_THAN_OR_EQUAL        `    | Less than or equal comparison    |
| `         NOT_EQUAL        `             | Not equals comparison            |
| `         CMP        `                   | General comparison               |

### EQUAL

**Syntax:**

    equal(x: ANY, y: ANY) -> BOOLEAN

**Examples:**

| `x`    | `y`      | `equal(x, y)` |
| :----- | :------- | :------------ |
| 1L     | 1L       | `TRUE`        |
| 1.0    | 1L       | `TRUE`        |
| \-1.0  | 1L       | `FALSE`       |
| NaN    | NaN      | `TRUE`        |
| `NULL` | `NULL`   | `TRUE`        |
| `NULL` | `ABSENT` | `FALSE`       |

**Description:**

Returns `TRUE` if `x` and `y` are equal, and `FALSE` otherwise.

##### Node.js

    const result = await db.pipeline()
      .collection("books")
      .select(field("rating").equal(5).as("hasPerfectRating"))
      .execute();test.firestore.js

### Web

    const result = await execute(db.pipeline()
      .collection("books")
      .select(field("rating").equal(5).as("hasPerfectRating"))
    );test.firestore.js

##### Swift

    let result = try await db.pipeline()
      .collection("books")
      .select([Field("rating").equal(5).as("hasPerfectRating")])
      .execute()PipelineSnippets.swift

##### Kotlin  
Android

    val result = db.pipeline()
        .collection("books")
        .select(field("rating").equal(5).alias("hasPerfectRating"))
        .execute()DocSnippets.kt

##### Java  
Android

    Task<Pipeline.Snapshot> result = db.pipeline()
        .collection("books")
        .select(field("rating").equal(5).alias("hasPerfectRating"))
        .execute();DocSnippets.java

##### Python

    from google.cloud.firestore_v1.pipeline_expressions import Field
    
    result = (
        client.pipeline()
        .collection("books")
        .select(Field.of("rating").equal(5).as_("hasPerfectRating"))
        .execute()
    )firestore_pipelines.py

##### Java

    Pipeline.Snapshot result =
        firestore
            .pipeline()
            .collection("books")
            .select(equal(field("rating"), 5).as("hasPerfectRating"))
            .execute()
            .get();PipelineSnippets.java

### GREATER\_THAN

**Syntax:**

    greater_than(x: ANY, y: ANY) -> BOOLEAN

**Description:**

Returns `TRUE` if `x` is greater than `y` , and `FALSE` otherwise.

If `x` and `y` are not comparable, returns `FALSE` .

**Examples:**

| `x`    | `y`    | `greater_than(x, y)` |
| :----- | :----- | :------------------- |
| 1L     | 0.0    | `TRUE`               |
| 1L     | 1L     | `FALSE`              |
| 1L     | 2L     | `FALSE`              |
| "foo"  | 0L     | `FALSE`              |
| 0L     | "foo"  | `FALSE`              |
| NaN    | 0L     | `FALSE`              |
| 0L     | NaN    | `FALSE`              |
| `NULL` | `NULL` | `FALSE`              |

##### Node.js

    const result = await db.pipeline()
      .collection("books")
      .select(field("rating").greaterThan(4).as("hasHighRating"))
      .execute();test.firestore.js

### Web

    const result = await execute(db.pipeline()
      .collection("books")
      .select(field("rating").greaterThan(4).as("hasHighRating"))
    );test.firestore.js

##### Swift

    let result = try await db.pipeline()
      .collection("books")
      .select([Field("rating").greaterThan(4).as("hasHighRating")])
      .execute()PipelineSnippets.swift

##### Kotlin  
Android

    val result = db.pipeline()
        .collection("books")
        .select(field("rating").greaterThan(4).alias("hasHighRating"))
        .execute()DocSnippets.kt

##### Java  
Android

    Task<Pipeline.Snapshot> result = db.pipeline()
        .collection("books")
        .select(field("rating").greaterThan(4).alias("hasHighRating"))
        .execute();DocSnippets.java

##### Python

    from google.cloud.firestore_v1.pipeline_expressions import Field
    
    result = (
        client.pipeline()
        .collection("books")
        .select(Field.of("rating").greater_than(4).as_("hasHighRating"))
        .execute()
    )firestore_pipelines.py

##### Java

    Pipeline.Snapshot result =
        firestore
            .pipeline()
            .collection("books")
            .select(greaterThan(field("rating"), 4).as("hasHighRating"))
            .execute()
            .get();PipelineSnippets.java

### GREATER\_THAN\_OR\_EQUAL

**Syntax:**

    greater_than_or_equal(x: ANY, y: ANY) -> BOOLEAN

**Description:**

Returns `TRUE` if `x` is greater than or equal to `y` , and `FALSE` otherwise.

If `x` and `y` are not comparable, returns `FALSE` .

**Examples:**

| `x`    | `y`    | `greater_than_or_equal(x, y)` |
| :----- | :----- | :---------------------------- |
| 1L     | 0.0    | `TRUE`                        |
| 1L     | 1L     | `TRUE`                        |
| 1L     | 2L     | `FALSE`                       |
| "foo"  | 0L     | `FALSE`                       |
| 0L     | "foo"  | `FALSE`                       |
| NaN    | 0L     | `FALSE`                       |
| 0L     | NaN    | `FALSE`                       |
| `NULL` | `NULL` | `TRUE`                        |

##### Node.js

    const result = await db.pipeline()
      .collection("books")
      .select(field("published").greaterThanOrEqual(1900).as("publishedIn20thCentury"))
      .execute();test.firestore.js

### Web

    const result = await execute(db.pipeline()
      .collection("books")
      .select(field("published").greaterThanOrEqual(1900).as("publishedIn20thCentury"))
    );test.firestore.js

##### Swift

    let result = try await db.pipeline()
      .collection("books")
      .select([Field("published").greaterThanOrEqual(1900).as("publishedIn20thCentury")])
      .execute()PipelineSnippets.swift

##### Kotlin  
Android

    val result = db.pipeline()
        .collection("books")
        .select(field("published").greaterThanOrEqual(1900).alias("publishedIn20thCentury"))
        .execute()DocSnippets.kt

##### Java  
Android

    Task<Pipeline.Snapshot> result = db.pipeline()
        .collection("books")
        .select(field("published").greaterThanOrEqual(1900).alias("publishedIn20thCentury"))
        .execute();DocSnippets.java

##### Python

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

##### Java

    Pipeline.Snapshot result =
        firestore
            .pipeline()
            .collection("books")
            .select(greaterThanOrEqual(field("published"), 1900).as("publishedIn20thCentury"))
            .execute()
            .get();PipelineSnippets.java

### LESS\_THAN

**Syntax:**

    less_than(x: ANY, y: ANY) -> BOOLEAN

**Description:**

Returns `TRUE` if `x` is less than `y` , and `FALSE` otherwise.

If `x` and `y` are not comparable, returns `FALSE` .

**Examples:**

| `x`    | `y`    | `less_than(x, y)` |
| :----- | :----- | :---------------- |
| 1L     | 0.0    | `FALSE`           |
| 1L     | 1L     | `FALSE`           |
| 1L     | 2L     | `TRUE`            |
| "foo"  | 0L     | `FALSE`           |
| 0L     | "foo"  | `FALSE`           |
| NaN    | 0L     | `FALSE`           |
| 0L     | NaN    | `FALSE`           |
| `NULL` | `NULL` | `FALSE`           |

##### Node.js

    const result = await db.pipeline()
      .collection("books")
      .select(field("published").lessThan(1923).as("isPublicDomainProbably"))
      .execute();test.firestore.js

### Web

    const result = await execute(db.pipeline()
      .collection("books")
      .select(field("published").lessThan(1923).as("isPublicDomainProbably"))
    );test.firestore.js

##### Swift

    let result = try await db.pipeline()
      .collection("books")
      .select([Field("published").lessThan(1923).as("isPublicDomainProbably")])
      .execute()PipelineSnippets.swift

##### Kotlin  
Android

    val result = db.pipeline()
        .collection("books")
        .select(field("published").lessThan(1923).alias("isPublicDomainProbably"))
        .execute()DocSnippets.kt

##### Java  
Android

    Task<Pipeline.Snapshot> result = db.pipeline()
        .collection("books")
        .select(field("published").lessThan(1923).alias("isPublicDomainProbably"))
        .execute();DocSnippets.java

##### Python

    from google.cloud.firestore_v1.pipeline_expressions import Field
    
    result = (
        client.pipeline()
        .collection("books")
        .select(Field.of("published").less_than(1923).as_("isPublicDomainProbably"))
        .execute()
    )firestore_pipelines.py

##### Java

    Pipeline.Snapshot result =
        firestore
            .pipeline()
            .collection("books")
            .select(lessThan(field("published"), 1923).as("isPublicDomainProbably"))
            .execute()
            .get();PipelineSnippets.java

### LESS\_THAN\_OR\_EQUAL

**Syntax:**

    less_than_or_equal(x: ANY, y: ANY) -> BOOLEAN

**Description:**

Returns `TRUE` if `x` is less than or equal to `y` , and `FALSE` otherwise.

If `x` and `y` are not comparable, returns `FALSE` .

**Examples:**

| `x`    | `y`    | `less_than(x, y)` |
| :----- | :----- | :---------------- |
| 1L     | 0.0    | `FALSE`           |
| 1L     | 1L     | `TRUE`            |
| 1L     | 2L     | `TRUE`            |
| "foo"  | 0L     | `FALSE`           |
| 0L     | "foo"  | `FALSE`           |
| NaN    | 0L     | `FALSE`           |
| 0L     | NaN    | `FALSE`           |
| `NULL` | `NULL` | `TRUE`            |

##### Node.js

    const result = await db.pipeline()
      .collection("books")
      .select(field("rating").lessThanOrEqual(2).as("hasBadRating"))
      .execute();test.firestore.js

### Web

    const result = await execute(db.pipeline()
      .collection("books")
      .select(field("rating").lessThanOrEqual(2).as("hasBadRating"))
    );test.firestore.js

##### Swift

    let result = try await db.pipeline()
      .collection("books")
      .select([Field("rating").lessThanOrEqual(2).as("hasBadRating")])
      .execute()PipelineSnippets.swift

##### Kotlin  
Android

    val result = db.pipeline()
        .collection("books")
        .select(field("rating").lessThanOrEqual(2).alias("hasBadRating"))
        .execute()DocSnippets.kt

##### Java  
Android

    Task<Pipeline.Snapshot> result = db.pipeline()
        .collection("books")
        .select(field("rating").lessThanOrEqual(2).alias("hasBadRating"))
        .execute();DocSnippets.java

##### Python

    from google.cloud.firestore_v1.pipeline_expressions import Field
    
    result = (
        client.pipeline()
        .collection("books")
        .select(Field.of("rating").less_than_or_equal(2).as_("hasBadRating"))
        .execute()
    )firestore_pipelines.py

##### Java

    Pipeline.Snapshot result =
        firestore
            .pipeline()
            .collection("books")
            .select(lessThanOrEqual(field("rating"), 2).as("hasBadRating"))
            .execute()
            .get();PipelineSnippets.java

### NOT\_EQUAL

**Syntax:**

    not_equal(x: ANY, y: ANY) -> BOOLEAN

**Description:**

Returns `TRUE` if `x` is not equal to `y` , and `FALSE` otherwise.

**Examples:**

| `x`    | `y`      | `not_equal(x, y)` |
| :----- | :------- | :---------------- |
| 1L     | 1L       | `FALSE`           |
| 1.0    | 1L       | `FALSE`           |
| \-1.0  | 1L       | `TRUE`            |
| NaN    | 0L       | `TRUE`            |
| NaN    | NaN      | `FALSE`           |
| `NULL` | `NULL`   | `FALSE`           |
| `NULL` | `ABSENT` | `TRUE`            |

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

### CMP

**Syntax:**

    cmp(x: ANY, y: ANY) -> Int64

**Description:**

Compares `x` & `y` , returning:

  - `1L` if `x` is greater than `y` .
  - `-1L` if `x` is less than `y` .
  - `0L` otherwise.

Unlike other comparison functions, the `cmp(...)` function works across types, following the same ordering used in the `sort(...)` stage. See [value type order](https://docs.cloud.google.com/firestore/native/docs/concepts/data-types) for how values are ordered across types.

**Examples:**

| `x`    | `y`      | `cmp(x, y)` |
| :----- | :------- | :---------- |
| 1L     | 1L       | 0L          |
| 1.0    | 1L       | 0L          |
| \-1.0  | 1L       | \-1L        |
| 42.5D  | "foo"    | \-1L        |
| `NULL` | `NULL`   | 0L          |
| `NULL` | `ABSENT` | 0L          |

## What's next

  - See the [Pipeline Queries overview](https://docs.cloud.google.com/firestore/docs/pipeline/overview)
