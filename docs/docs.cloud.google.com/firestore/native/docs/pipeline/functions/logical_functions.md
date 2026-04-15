# Logical Functions Reference

> **Preview — Firestore in Native mode (with Pipeline Operations) for Enterprise Edition**
> 
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . You can process personal data for this feature as outlined in the [Cloud Data Processing Addendum](https://docs.cloud.google.com/terms/data-processing-addendum) , subject to the obligations and restrictions described in the agreement under which you access Google Cloud. Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

## **Logical Functions**

|                                  |                                                            |
| -------------------------------- | ---------------------------------------------------------- |
| Name                             | Description                                                |
| `         AND        `           | Performs a logical AND                                     |
| `         OR        `            | Performs a logical OR                                      |
| `         XOR        `           | Performs a logical XOR                                     |
| `         NOT        `           | Performs a logical NOT                                     |
| `         NOR        `           | Performs a logical NOR                                     |
| `         CONDITIONAL        `   | Branches evaluation based on a conditional expression.     |
| `         IF_NULL        `       | Returns the first non-null value                           |
| `         SWITCH_ON        `     | Branches evaluation based on a series of conditions        |
| `         EQUAL_ANY        `     | Checks if a value is equal to any elements in an array     |
| `         NOT_EQUAL_ANY        ` | Checks if a value is not equal to any elements in an array |
| `         MAXIMUM        `       | Returns the maximum value in a set of values               |
| `         MINIMUM        `       | Returns the minimum value in a set of values               |

### AND

**Syntax:**

    and(x: BOOLEAN...) -> BOOLEAN

**Description:**

Returns the logical AND of two or more boolean values.

Returns `NULL` if the result can't be derived due to any of the given values being `ABSENT` or `NULL` .

**Examples:**

| `x`      | `y`      | `and(x, y)` |
| :------- | :------- | :---------- |
| `TRUE`   | `TRUE`   | `TRUE`      |
| `FALSE`  | `TRUE`   | `FALSE`     |
| `NULL`   | `TRUE`   | `NULL`      |
| `ABSENT` | `TRUE`   | `NULL`      |
| `NULL`   | `FALSE`  | `FALSE`     |
| `FALSE`  | `ABSENT` | `FALSE`     |

##### Node.js

    const result = await db.pipeline()
      .collection("books")
      .select(
        and(field("rating").greaterThan(4), field("price").lessThan(10))
          .as("under10Recommendation")
      )
      .execute();test.firestore.js

### Web

    const result = await execute(db.pipeline()
      .collection("books")
      .select(
        and(field("rating").greaterThan(4), field("price").lessThan(10))
          .as("under10Recommendation")
      )
    );test.firestore.js

##### Swift

    let result = try await db.pipeline()
      .collection("books")
      .select([
        (Field("rating").greaterThan(4) && Field("price").lessThan(10))
          .as("under10Recommendation")
      ])
      .execute()PipelineSnippets.swift

##### Kotlin  
Android

    val result = db.pipeline()
        .collection("books")
        .select(
            Expression.and(field("rating").greaterThan(4),
              field("price").lessThan(10))
                .alias("under10Recommendation")
        )
        .execute()DocSnippets.kt

##### Java  
Android

    Task<Pipeline.Snapshot> result = db.pipeline()
        .collection("books")
        .select(
            Expression.and(
                field("rating").greaterThan(4),
                field("price").lessThan(10)
            ).alias("under10Recommendation")
        )
        .execute();DocSnippets.java

##### Python

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

##### Java

    Pipeline.Snapshot result =
        firestore
            .pipeline()
            .collection("books")
            .select(
                and(greaterThan(field("rating"), 4), lessThan(field("price"), 10))
                    .as("under10Recommendation"))
            .execute()
            .get();PipelineSnippets.java

### OR

**Syntax:**

    or(x: BOOLEAN...) -> BOOLEAN

**Description:**

Returns the logical OR of two or more boolean values.

Returns `NULL` if the result can't be derived due to any of the given values being `ABSENT` or `NULL` .

**Examples:**

| `x`      | `y`      | `or(x, y)` |
| :------- | :------- | :--------- |
| `TRUE`   | `TRUE`   | `TRUE`     |
| `FALSE`  | `TRUE`   | `TRUE`     |
| `NULL`   | `TRUE`   | `TRUE`     |
| `ABSENT` | `TRUE`   | `TRUE`     |
| `NULL`   | `FALSE`  | `NULL`     |
| `FALSE`  | `ABSENT` | `NULL`     |

##### Node.js

    const result = await db.pipeline()
      .collection("books")
      .select(
        or(field("genre").equal("Fantasy"), field("tags").arrayContains("adventure"))
          .as("matchesSearchFilters")
      )
      .execute();test.firestore.js

### Web

    const result = await execute(db.pipeline()
      .collection("books")
      .select(
        or(field("genre").equal("Fantasy"), field("tags").arrayContains("adventure"))
          .as("matchesSearchFilters")
      )
    );test.firestore.js

##### Swift

    let result = try await db.pipeline()
      .collection("books")
      .select([
        (Field("genre").equal("Fantasy") || Field("tags").arrayContains("adventure"))
          .as("matchesSearchFilters")
      ])
      .execute()PipelineSnippets.swift

##### Kotlin  
Android

    val result = db.pipeline()
        .collection("books")
        .select(
            Expression.or(field("genre").equal("Fantasy"),
              field("tags").arrayContains("adventure"))
                .alias("matchesSearchFilters")
        )
        .execute()DocSnippets.kt

##### Java  
Android

    Task<Pipeline.Snapshot> result = db.pipeline()
        .collection("books")
        .select(
            Expression.or(
                field("genre").equal("Fantasy"),
                field("tags").arrayContains("adventure")
            ).alias("matchesSearchFilters")
        )
        .execute();DocSnippets.java

##### Python

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

##### Java

    Pipeline.Snapshot result =
        firestore
            .pipeline()
            .collection("books")
            .select(
                or(equal(field("genre"), "Fantasy"), arrayContains(field("tags"), "adventure"))
                    .as("matchesSearchFilters"))
            .execute()
            .get();PipelineSnippets.java

### XOR

**Syntax:**

    xor(x: BOOLEAN...) -> BOOLEAN

**Description:**

Returns the logical XOR of two or more boolean values.

Returns `NULL` if any of the given values are `ABSENT` or `NULL` .

**Examples:**

| `x`      | `y`      | `xor(x, y)` |
| :------- | :------- | :---------- |
| `TRUE`   | `TRUE`   | `FALSE`     |
| `FALSE`  | `FALSE`  | `FALSE`     |
| `FALSE`  | `TRUE`   | `TRUE`      |
| `NULL`   | `TRUE`   | `NULL`      |
| `ABSENT` | `TRUE`   | `NULL`      |
| `NULL`   | `FALSE`  | `NULL`      |
| `FALSE`  | `ABSENT` | `NULL`      |

##### Node.js

    const result = await execute(db.pipeline()
      .collection("books")
      .select(
        xor(field("tags").arrayContains("magic"), field("tags").arrayContains("nonfiction"))
          .as("matchesSearchFilters")
      )
    );test.firestore.js

### Web

    const result = await execute(db.pipeline()
      .collection("books")
      .select(
        xor(field("tags").arrayContains("magic"), field("tags").arrayContains("nonfiction"))
          .as("matchesSearchFilters")
      )
    );test.firestore.js

##### Swift

    let result = try await db.pipeline()
      .collection("books")
      .select([
        (Field("tags").arrayContains("magic") ^ Field("tags").arrayContains("nonfiction"))
          .as("matchesSearchFilters")
      ])
      .execute()PipelineSnippets.swift

##### Kotlin  
Android

    val result = db.pipeline()
        .collection("books")
        .select(
            Expression.xor(field("tags").arrayContains("magic"),
              field("tags").arrayContains("nonfiction"))
                .alias("matchesSearchFilters")
        )
        .execute()DocSnippets.kt

##### Java  
Android

    Task<Pipeline.Snapshot> result = db.pipeline()
        .collection("books")
        .select(
            Expression.xor(
                field("tags").arrayContains("magic"),
                field("tags").arrayContains("nonfiction")
            ).alias("matchesSearchFilters")
        )
        .execute();DocSnippets.java

##### Python

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

##### Java

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

### NOR

**Syntax:**

    nor(x: BOOLEAN...) -> BOOLEAN

**Description:**

Returns the logical NOR of two or more boolean values.

Returns `NULL` if the result can't be derived due to any of the given values being `ABSENT` or `NULL` .

**Examples:**

| `x`      | `y`      | `nor(x, y)` |
| :------- | :------- | :---------- |
| `TRUE`   | `TRUE`   | `FALSE`     |
| `FALSE`  | `TRUE`   | `FALSE`     |
| `FALSE`  | `FALSE`  | `TRUE`      |
| `NULL`   | `TRUE`   | `FALSE`     |
| `ABSENT` | `TRUE`   | `FALSE`     |
| `NULL`   | `FALSE`  | `NULL`      |
| `FALSE`  | `ABSENT` | `NULL`      |

### NOT

**Syntax:**

    not(x: BOOLEAN) -> BOOLEAN

**Description:**

Returns the logical NOT of a boolean value.

##### Node.js

    const result = await execute(db.pipeline()
      .collection("books")
      .select(
        field("tags").arrayContains("nonfiction").not()
          .as("isFiction")
      )
    );test.firestore.js

### Web

    const result = await execute(db.pipeline()
      .collection("books")
      .select(
        field("tags").arrayContains("nonfiction").not()
          .as("isFiction")
      )
    );test.firestore.js

##### Swift

    let result = try await db.pipeline()
      .collection("books")
      .select([
        (!Field("tags").arrayContains("nonfiction"))
          .as("isFiction")
      ])
      .execute()PipelineSnippets.swift

##### Kotlin  
Android

    val result = db.pipeline()
        .collection("books")
        .select(
            Expression.not(
                field("tags").arrayContains("nonfiction")
            ).alias("isFiction")
        )
        .execute()DocSnippets.kt

##### Java  
Android

    Task<Pipeline.Snapshot> result = db.pipeline()
        .collection("books")
        .select(
            Expression.not(
                field("tags").arrayContains("nonfiction")
            ).alias("isFiction")
        )
        .execute();DocSnippets.java

##### Python

    from google.cloud.firestore_v1.pipeline_expressions import Field, Not
    
    result = (
        client.pipeline()
        .collection("books")
        .select(Not(Field.of("tags").array_contains("nonfiction")).as_("isFiction"))
        .execute()
    )firestore_pipelines.py

##### Java

    Pipeline.Snapshot result =
        firestore
            .pipeline()
            .collection("books")
            .select(not(arrayContains(field("tags"), "nonfiction")).as("isFiction"))
            .execute()
            .get();PipelineSnippets.java

### CONDITIONAL

**Syntax:**

    conditional(condition: BOOLEAN, true_case: ANY, false_case: ANY) -> ANY

**Description:**

Evaluates and returns the `true_case` if the `condition` evaluates to `TRUE` .

Evaluates and returns the `false_case` if the condition resolves to `FALSE` , `NULL` , or an `ABSENT` value.

**Examples:**

| `condition` | `true_case` | `false_case` | `conditional(condition, true_case, false_case)` |
| :---------- | :---------- | :----------- | :---------------------------------------------- |
| `TRUE`      | 1L          | 0L           | 1L                                              |
| `FALSE`     | 1L          | 0L           | 0L                                              |
| `NULL`      | 1L          | 0L           | 0L                                              |
| `ABSENT`    | 1L          | 0L           | 0L                                              |

##### Node.js

    const result = await execute(db.pipeline()
      .collection("books")
      .select(
        field("tags").arrayConcat([
          field("pages").greaterThan(100)
            .conditional(constant("longRead"), constant("shortRead"))
        ]).as("extendedTags")
      )
    );test.firestore.js

### Web

    const result = await execute(db.pipeline()
      .collection("books")
      .select(
        field("tags").arrayConcat([
          field("pages").greaterThan(100)
            .conditional(constant("longRead"), constant("shortRead"))
        ]).as("extendedTags")
      )
    );test.firestore.js

##### Swift

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

##### Kotlin  
Android

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

##### Java  
Android

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

##### Python

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

##### Java

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

### IF\_NULL

**Syntax:**

    if_null(expr: ANY, replacement: ANY) -> ANY

**Description:**

Returns `expr` if it is not `NULL` , otherwise evaluates and returns `replacement` . The `replacement` expression is not evaluated if `expr` is used.

**Examples:**

| `expr`   | `replacement` | `if_null(expr, replacement)` |
| :------- | :------------ | :--------------------------- |
| 1L       | 2L            | 1L                           |
| `NULL`   | 2L            | 2L                           |
| `ABSENT` | 2L            | `ABSENT`                     |

### SWITCH\_ON

**Syntax:**

    switch_on(cond1: BOOLEAN, res1: ANY, cond2: BOOLEAN, res2: ANY, ..., [default: ANY]) -> ANY

**Description:**

Evaluates a series of conditions and returns the result associated with the first `TRUE` condition. If no conditions evaluate to `TRUE` , the `default` value is returned if provided. If no `default` value is provided, an error is thrown if no other conditions evaluated to `TRUE` .

To provide a `default` value, pass it as the final argument such that there is an odd number of arguments.

**Examples:**

| `x` | `switch_on(eq(x, 1L), "one", eq(x, 2L), "two", "other")` |
| :-- | :------------------------------------------------------- |
| 1L  | "one"                                                    |
| 2L  | "two"                                                    |
| 3L  | "other"                                                  |

### EQUAL\_ANY

**Syntax:**

    equal_any(value: ANY, search_space: ARRAY) -> BOOLEAN

**Description:**

Returns `TRUE` if `value` is in the `search_space` array.

**Examples:**

| `value`  | `search_space`  | `equal_any(value, search_space)` |
| :------- | :-------------- | :------------------------------- |
| 0L       | \[1L, 2L, 3L\]  | `FALSE`                          |
| 2L       | \[1L, 2L, 3L\]  | `TRUE`                           |
| `NULL`   | \[1L, 2L, 3L\]  | `FALSE`                          |
| `NULL`   | \[1L, `NULL` \] | `TRUE`                           |
| `ABSENT` | \[1L, `NULL` \] | `FALSE`                          |
| NaN      | \[1L, NaN, 3L\] | `TRUE`                           |

##### Node.js

    const result = await execute(db.pipeline()
      .collection("books")
      .select(
        field("genre").equalAny(["Science Fiction", "Psychological Thriller"])
          .as("matchesGenreFilters")
      )
    );test.firestore.js

### Web

    const result = await execute(db.pipeline()
      .collection("books")
      .select(
        field("genre").equalAny(["Science Fiction", "Psychological Thriller"])
          .as("matchesGenreFilters")
      )
    );test.firestore.js

##### Swift

    let result = try await db.pipeline()
      .collection("books")
      .select([
        Field("genre").equalAny(["Science Fiction", "Psychological Thriller"])
          .as("matchesGenreFilters")
      ])
      .execute()PipelineSnippets.swift

##### Kotlin  
Android

    val result = db.pipeline()
        .collection("books")
        .select(
            field("genre").equalAny(listOf("Science Fiction", "Psychological Thriller"))
                .alias("matchesGenreFilters")
        )
        .execute()DocSnippets.kt

##### Java  
Android

    Task<Pipeline.Snapshot> result = db.pipeline()
        .collection("books")
        .select(
            field("genre").equalAny(Arrays.asList("Science Fiction", "Psychological Thriller"))
                .alias("matchesGenreFilters")
        )
        .execute();DocSnippets.java

##### Python

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

##### Java

    Pipeline.Snapshot result =
        firestore
            .pipeline()
            .collection("books")
            .select(
                equalAny(field("genre"), Arrays.asList("Science Fiction", "Psychological Thriller"))
                    .as("matchesGenreFilters"))
            .execute()
            .get();PipelineSnippets.java

### NOT\_EQUAL\_ANY

**Syntax:**

    not_equal_any(value: ANY, search_space: ARRAY) -> BOOLEAN

**Description:**

Returns `TRUE` if `value` is not in the `search_space` array.

**Examples:**

| `value`  | `search_space`  | `not_equal_any(value, search_space)` |
| :------- | :-------------- | :----------------------------------- |
| 0L       | \[1L, 2L, 3L\]  | `TRUE`                               |
| 2L       | \[1L, 2L, 3L\]  | `FALSE`                              |
| `NULL`   | \[1L, 2L, 3L\]  | `TRUE`                               |
| `NULL`   | \[1L, `NULL` \] | `FALSE`                              |
| `ABSENT` | \[1L, `NULL` \] | `TRUE`                               |
| NaN      | \[1L, NaN, 3L\] | `FALSE`                              |

##### Node.js

    const result = await execute(db.pipeline()
      .collection("books")
      .select(
        field("author").notEqualAny(["George Orwell", "F. Scott Fitzgerald"])
          .as("byExcludedAuthors")
      )
    );test.firestore.js

### Web

    const result = await execute(db.pipeline()
      .collection("books")
      .select(
        field("author").notEqualAny(["George Orwell", "F. Scott Fitzgerald"])
          .as("byExcludedAuthors")
      )
    );test.firestore.js

##### Swift

    let result = try await db.pipeline()
      .collection("books")
      .select([
        Field("author").notEqualAny(["George Orwell", "F. Scott Fitzgerald"])
          .as("byExcludedAuthors")
      ])
      .execute()PipelineSnippets.swift

##### Kotlin  
Android

    val result = db.pipeline()
        .collection("books")
        .select(
            field("author").notEqualAny(listOf("George Orwell", "F. Scott Fitzgerald"))
                .alias("byExcludedAuthors")
        )
        .execute()DocSnippets.kt

##### Java  
Android

    Task<Pipeline.Snapshot> result = db.pipeline()
        .collection("books")
        .select(
            field("author").notEqualAny(Arrays.asList("George Orwell", "F. Scott Fitzgerald"))
                .alias("byExcludedAuthors")
        )
        .execute();DocSnippets.java

##### Python

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

##### Java

    Pipeline.Snapshot result =
        firestore
            .pipeline()
            .collection("books")
            .select(
                notEqualAny(field("author"), Arrays.asList("George Orwell", "F. Scott Fitzgerald"))
                    .as("byExcludedAuthors"))
            .execute()
            .get();PipelineSnippets.java

### MAXIMUM

**Syntax:**

    maximum(x: ANY...) -> ANY
    maximum(x: ARRAY) -> ANY

**Description:**

Returns the maximum non- `NULL` , non- `ABSENT` value in a series of values `x` .

If there are no non- `NULL` , non- `ABSENT` values, `NULL` is returned.

If there are multiple maximum equivalent values, any one of those values can be returned. Value type ordering follows [documented ordering](https://docs.cloud.google.com/firestore/docs/concepts/data-types#value_type_ordering) .

**Examples:**

| `x`      | `y`       | `maximum(x, y)` |
| :------- | :-------- | :-------------- |
| `FALSE`  | `TRUE`    | `TRUE`          |
| `FALSE`  | \-10L     | \-10L           |
| 0.0      | \-5L      | 0.0             |
| "foo"    | "bar"     | "foo"           |
| "foo"    | \["foo"\] | \["foo"\]       |
| `ABSENT` | `ABSENT`  | `NULL`          |
| `NULL`   | `NULL`    | `NULL`          |

##### Node.js

    const result = await execute(db.pipeline()
      .collection("books")
      .aggregate(field("price").maximum().as("maximumPrice"))
    );test.firestore.js

### Web

    const result = await execute(db.pipeline()
      .collection("books")
      .aggregate(field("price").maximum().as("maximumPrice"))
    );test.firestore.js

##### Swift

    let result = try await db.pipeline()
      .collection("books")
      .select([
        Field("rating").logicalMaximum([1]).as("flooredRating")
      ])
      .execute()PipelineSnippets.swift

##### Kotlin  
Android

    val result = db.pipeline()
        .collection("books")
        .select(
            field("rating").logicalMaximum(1).alias("flooredRating")
        )
        .execute()DocSnippets.kt

##### Java  
Android

    Task<Pipeline.Snapshot> result = db.pipeline()
        .collection("books")
        .select(
            field("rating").logicalMaximum(1).alias("flooredRating")
        )
        .execute();DocSnippets.java

##### Python

    from google.cloud.firestore_v1.pipeline_expressions import Field
    
    result = (
        client.pipeline()
        .collection("books")
        .select(Field.of("rating").logical_maximum(1).as_("flooredRating"))
        .execute()
    )firestore_pipelines.py

##### Java

    Pipeline.Snapshot result =
        firestore
            .pipeline()
            .collection("books")
            .select(logicalMaximum(field("rating"), 1).as("flooredRating"))
            .execute()
            .get();PipelineSnippets.java

### MINIMUM

**Syntax:**

    minimum(x: ANY...) -> ANY
    minimum(x: ARRAY) -> ANY

**Description:**

Returns the minimum non- `NULL` , non- `ABSENT` value in a series of values `x` .

If there are no non- `NULL` , non- `ABSENT` values, `NULL` is returned.

If there are multiple minimum equivalent values, any one of those values can be returned. Value type ordering follows [documented ordering](https://docs.cloud.google.com/firestore/docs/concepts/data-types#value_type_ordering) .

**Examples:**

| `x`      | `y`       | `minimum(x, y)` |
| :------- | :-------- | :-------------- |
| `FALSE`  | `TRUE`    | `FALSE`         |
| `FALSE`  | \-10L     | `FALSE`         |
| 0.0      | \-5L      | \-5L            |
| "foo"    | "bar"     | "bar"           |
| "foo"    | \["foo"\] | "foo"           |
| `ABSENT` | `ABSENT`  | `NULL`          |
| `NULL`   | `NULL`    | `NULL`          |

##### Node.js

    const result = await execute(db.pipeline()
      .collection("books")
      .aggregate(field("price").minimum().as("minimumPrice"))
    );test.firestore.js

### Web

    const result = await execute(db.pipeline()
      .collection("books")
      .aggregate(field("price").minimum().as("minimumPrice"))
    );test.firestore.js

##### Swift

    let result = try await db.pipeline()
      .collection("books")
      .select([
        Field("rating").logicalMinimum([5]).as("cappedRating")
      ])
      .execute()PipelineSnippets.swift

##### Kotlin  
Android

    val result = db.pipeline()
        .collection("books")
        .select(
            field("rating").logicalMinimum(5).alias("cappedRating")
        )
        .execute()DocSnippets.kt

##### Java  
Android

    Task<Pipeline.Snapshot> result = db.pipeline()
        .collection("books")
        .select(
            field("rating").logicalMinimum(5).alias("cappedRating")
        )
        .execute();DocSnippets.java

##### Python

    from google.cloud.firestore_v1.pipeline_expressions import Field
    
    result = (
        client.pipeline()
        .collection("books")
        .select(Field.of("rating").logical_minimum(5).as_("cappedRating"))
        .execute()
    )firestore_pipelines.py

##### Java

    Pipeline.Snapshot result =
        firestore
            .pipeline()
            .collection("books")
            .select(logicalMinimum(field("rating"), 5).as("cappedRating"))
            .execute()
            .get();PipelineSnippets.java

## What's next

  - See the [Pipeline Queries overview](https://docs.cloud.google.com/firestore/docs/pipeline/overview)
