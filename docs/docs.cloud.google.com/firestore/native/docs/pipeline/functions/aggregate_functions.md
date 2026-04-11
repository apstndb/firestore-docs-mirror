# Aggregate Functions Reference

**Preview — Firestore in Native mode (with Pipeline Operations) for Enterprise Edition**

This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . You can process personal data for this feature as outlined in the [Cloud Data Processing Addendum](https://docs.cloud.google.com/terms/data-processing-addendum) , subject to the obligations and restrictions described in the agreement under which you access Google Cloud. Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

## **Aggregate**

All aggregate functions can be used as top-level expressions in the `aggregate(...)` stage.

|                                       |                                                                        |
| ------------------------------------- | ---------------------------------------------------------------------- |
| Name                                  | Description                                                            |
| `         COUNT        `              | Returns the number of documents.                                       |
| `         COUNT_IF        `           | Returns the count of documents where an expression evaluates to `TRUE` |
| `         COUNT_DISTINCT        `     | Returns the count of unique, non `NULL` values                         |
| `         SUM        `                | Returns the sum of all `NUMERIC` values                                |
| `         AVERAGE        `            | Returns the average of all `NUMERIC` values                            |
| `         MINIMUM        `            | Returns the minimum non `NULL` value                                   |
| `         MAXIMUM        `            | Returns the maximum non `NULL` value                                   |
| `         FIRST        `              | Returns the `expression` value for the first document.                 |
| `         LAST        `               | Returns the `expression` value for the last document.                  |
| `         ARRAY_AGG        `          | Returns an array of all input values.                                  |
| `         ARRAY_AGG_DISTINCT        ` | Returns an array of all distinct input values.                         |

### COUNT

**Syntax:**

    count() -> INT64
    count(expression: ANY) -> INT64

**Description:**

Returns the count of documents from the previous stage where `expression` evaluates to any non- `NULL` value. If no `expression` is provided, returns the total count of documents from the previous stage.

##### Node.js

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

### Web

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

##### Swift

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

##### Kotlin  
Android

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

##### Java  
Android

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

##### Python

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

##### Java

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

### COUNT\_IF

**Syntax:**

    count_if(expression: BOOLEAN) -> INT64

**Description:**

Returns the number of documents from the previous stage where `expression` evaluates to `TRUE` .

##### Node.js

    const result = await db.pipeline()
      .collection("books")
      .aggregate(
        field("rating").greaterThan(4).countIf().as("filteredCount")
      )
      .execute();test.firestore.js

### Web

    const result = await execute(db.pipeline()
      .collection("books")
      .aggregate(
        field("rating").greaterThan(4).countIf().as("filteredCount")
      )
    );test.firestore.js

##### Swift

    let result = try await db.pipeline()
      .collection("books")
      .aggregate([
        AggregateFunction("count_if", [Field("rating").greaterThan(4)]).as("filteredCount")
      ])
      .execute()PipelineSnippets.swift

##### Kotlin  
Android

    val result = db.pipeline()
        .collection("books")
        .aggregate(
            AggregateFunction.countIf(field("rating").greaterThan(4)).alias("filteredCount")
        )
        .execute()DocSnippets.kt

##### Java  
Android

    Task<Pipeline.Snapshot> result = db.pipeline()
        .collection("books")
        .aggregate(
            AggregateFunction.countIf(field("rating").greaterThan(4)).alias("filteredCount")
        )
        .execute();DocSnippets.java

##### Python

    from google.cloud.firestore_v1.pipeline_expressions import Field
    
    result = (
        client.pipeline()
        .collection("books")
        .aggregate(Field.of("rating").greater_than(4).count_if().as_("filteredCount"))
        .execute()
    )firestore_pipelines.py

##### Java

    Pipeline.Snapshot result =
        firestore
            .pipeline()
            .collection("books")
            .aggregate(countIf(field("rating").greaterThan(4)).as("filteredCount"))
            .execute()
            .get();PipelineSnippets.java

### COUNT\_DISTINCT

**Syntax:**

    count_distinct(expression: ANY) -> INT64

**Description:**

Returns the number of unique non- `NULL` , non- `ABSENT` values of `expression` .

##### Node.js

    const result = await db.pipeline()
      .collection("books")
      .aggregate(field("author").countDistinct().as("unique_authors"))
      .execute();test.firestore.js

### Web

    const result = await execute(db.pipeline()
      .collection("books")
      .aggregate(field("author").countDistinct().as("unique_authors"))
    );test.firestore.js

##### Swift

    let result = try await db.pipeline()
      .collection("books")
      .aggregate([AggregateFunction("count_distinct", [Field("author")]).as("unique_authors")])
      .execute()PipelineSnippets.swift

##### Kotlin  
Android

    val result = db.pipeline()
        .collection("books")
        .aggregate(AggregateFunction.countDistinct("author").alias("unique_authors"))
        .execute()DocSnippets.kt

##### Java  
Android

    Task<Pipeline.Snapshot> result = db.pipeline()
        .collection("books")
        .aggregate(AggregateFunction.countDistinct("author").alias("unique_authors"))
        .execute();DocSnippets.java

##### Python

    from google.cloud.firestore_v1.pipeline_expressions import Field
    
    result = (
        client.pipeline()
        .collection("books")
        .aggregate(Field.of("author").count_distinct().as_("unique_authors"))
        .execute()
    )firestore_pipelines.py

##### Java

    Pipeline.Snapshot result =
        firestore
            .pipeline()
            .collection("books")
            .aggregate(countDistinct("author").as("unique_authors"))
            .execute()
            .get();PipelineSnippets.java

### SUM

**Syntax:**

    sum(expression: ANY) -> NUMBER

**Description:**

Returns the sum for all numerical values, ignoring non-numeric values. Returns `NaN` if any values are `NaN` .

The output will have the same type as the widest input type except in these cases:

  - An `INTEGER` will be converted to a `DOUBLE` if it cannot be represented as an `INTEGER` .

##### Node.js

    const result = await db.pipeline()
      .collection("cities")
      .aggregate(field("population").sum().as("totalPopulation"))
      .execute();test.firestore.js

### Web

    const result = await execute(db.pipeline()
      .collection("cities")
      .aggregate(field("population").sum().as("totalPopulation"))
    );test.firestore.js

##### Swift

    let result = try await db.pipeline()
      .collection("cities")
      .aggregate([Field("population").sum().as("totalPopulation")])
      .execute()PipelineSnippets.swift

##### Kotlin  
Android

    val result = db.pipeline()
        .collection("cities")
        .aggregate(AggregateFunction.sum("population").alias("totalPopulation"))
        .execute()DocSnippets.kt

##### Java  
Android

    Task<Pipeline.Snapshot> result = db.pipeline()
        .collection("cities")
        .aggregate(AggregateFunction.sum("population").alias("totalPopulation"))
        .execute();DocSnippets.java

##### Python

    from google.cloud.firestore_v1.pipeline_expressions import Field
    
    result = (
        client.pipeline()
        .collection("cities")
        .aggregate(Field.of("population").sum().as_("totalPopulation"))
        .execute()
    )firestore_pipelines.py

##### Java

    Pipeline.Snapshot result =
        firestore
            .pipeline()
            .collection("cities")
            .aggregate(sum("population").as("totalPopulation"))
            .execute()
            .get();PipelineSnippets.java

### AVERAGE

**Syntax:**

    average(expression: ANY) -> FLOAT64

**Description:**

Returns the average for all numerical values, ignoring non-numeric values. Evaluates to `NaN` if any values are `NaN` , or `NULL` if no numerical values are aggregated.

The output will have the same type as the input type except in these cases:

  - An `INTEGER` will be converted to a `DOUBLE` if it cannot be represented as an `INTEGER` .

##### Node.js

    const result = await db.pipeline()
      .collection("cities")
      .aggregate(field("population").average().as("averagePopulation"))
      .execute();test.firestore.js

### Web

    const result = await execute(db.pipeline()
      .collection("cities")
      .aggregate(field("population").average().as("averagePopulation"))
    );test.firestore.js

##### Swift

    let result = try await db.pipeline()
      .collection("cities")
      .aggregate([Field("population").average().as("averagePopulation")])
      .execute()PipelineSnippets.swift

##### Kotlin  
Android

    val result = db.pipeline()
        .collection("cities")
        .aggregate(AggregateFunction.average("population").alias("averagePopulation"))
        .execute()DocSnippets.kt

##### Java  
Android

    Task<Pipeline.Snapshot> result = db.pipeline()
        .collection("cities")
        .aggregate(AggregateFunction.average("population").alias("averagePopulation"))
        .execute();DocSnippets.java

##### Python

    from google.cloud.firestore_v1.pipeline_expressions import Field
    
    result = (
        client.pipeline()
        .collection("cities")
        .aggregate(Field.of("population").average().as_("averagePopulation"))
        .execute()
    )firestore_pipelines.py

##### Java

    Pipeline.Snapshot result =
        firestore
            .pipeline()
            .collection("cities")
            .aggregate(average("population").as("averagePopulation"))
            .execute()
            .get();PipelineSnippets.java

### MINIMUM

**Syntax:**

    minimum(expression: ANY) -> ANY

**Description:**

Returns the minimum non- `NULL` , non-absent value of the `expression` when evaluated on each document.

If there are no non- `NULL` , non-absent values, `NULL` is returned. This includes when no documents are considered.

If there are multiple minimum equivalent values, any one of those values can be returned. Value type ordering follows [documented ordering](https://docs.cloud.google.com/firestore/docs/concepts/data-types#value_type_ordering) .

##### Node.js

    const result = await db.pipeline()
      .collection("books")
      .aggregate(field("price").minimum().as("minimumPrice"))
      .execute();test.firestore.js

### Web

    const result = await execute(db.pipeline()
      .collection("books")
      .aggregate(field("price").minimum().as("minimumPrice"))
    );test.firestore.js

##### Swift

    let result = try await db.pipeline()
      .collection("books")
      .aggregate([Field("price").minimum().as("minimumPrice")])
      .execute()PipelineSnippets.swift

##### Kotlin  
Android

    val result = db.pipeline()
        .collection("books")
        .aggregate(AggregateFunction.minimum("price").alias("minimumPrice"))
        .execute()DocSnippets.kt

##### Java  
Android

    Task<Pipeline.Snapshot> result = db.pipeline()
        .collection("books")
        .aggregate(AggregateFunction.minimum("price").alias("minimumPrice"))
        .execute();DocSnippets.java

##### Python

    from google.cloud.firestore_v1.pipeline_expressions import Field
    
    result = (
        client.pipeline()
        .collection("books")
        .aggregate(Field.of("price").minimum().as_("minimumPrice"))
        .execute()
    )firestore_pipelines.py

##### Java

    Pipeline.Snapshot result =
        firestore
            .pipeline()
            .collection("books")
            .aggregate(minimum("price").as("minimumPrice"))
            .execute()
            .get();PipelineSnippets.java

### MAXIMUM

**Syntax:**

    maximum(expression: ANY) -> ANY

**Description:**

Returns the maximum non- `NULL` , non-absent value of the `expression` when evaluated on each document.

If there are no non- `NULL` , non-absent values, `NULL` is returned. This includes when no documents are considered.

If there are multiple maximum equivalent values, any one of those values can be returned. Value type ordering follows [documented ordering](https://docs.cloud.google.com/firestore/docs/concepts/data-types#value_type_ordering) .

##### Node.js

    const result = await db.pipeline()
      .collection("books")
      .aggregate(field("price").maximum().as("maximumPrice"))
      .execute();test.firestore.js

### Web

    const result = await execute(db.pipeline()
      .collection("books")
      .aggregate(field("price").maximum().as("maximumPrice"))
    );test.firestore.js

##### Swift

    let result = try await db.pipeline()
      .collection("books")
      .aggregate([Field("price").maximum().as("maximumPrice")])
      .execute()PipelineSnippets.swift

##### Kotlin  
Android

    val result = db.pipeline()
        .collection("books")
        .aggregate(AggregateFunction.maximum("price").alias("maximumPrice"))
        .execute()DocSnippets.kt

##### Java  
Android

    Task<Pipeline.Snapshot> result = db.pipeline()
        .collection("books")
        .aggregate(AggregateFunction.maximum("price").alias("maximumPrice"))
        .execute();DocSnippets.java

##### Python

    from google.cloud.firestore_v1.pipeline_expressions import Field
    
    result = (
        client.pipeline()
        .collection("books")
        .aggregate(Field.of("price").maximum().as_("maximumPrice"))
        .execute()
    )firestore_pipelines.py

##### Java

    Pipeline.Snapshot result =
        firestore
            .pipeline()
            .collection("books")
            .aggregate(maximum("price").as("maximumPrice"))
            .execute()
            .get();PipelineSnippets.java

### FIRST

**Syntax:**

    first(expression: ANY) -> ANY

**Description:**

Returns the value of `expression` for the first returned document.

### LAST

**Syntax:**

    last(expression: ANY) -> ANY

**Description:**

Returns the value of `expression` for the last returned document.

### ARRAY\_AGG

**Syntax:**

    array_agg(expression: ANY) -> ARRAY<ANY>

**Description:**

Returns an array containing all values of `expression` when evaluated on each document.

If the expression resolves to an absent value, it is converted to `NULL` .

The order of elements in the output array is not stable and shouldn't be relied upon.

### ARRAY\_AGG\_DISTINCT

**Syntax:**

    array_agg_distinct(expression: ANY) -> ARRAY<ANY>

**Description:**

Returns an array containing all distinct values of `expression` when evaluated on each document.

If the expression resolves to an absent value, it is converted to `NULL` .

The order of elements in the output array is not stable and shouldn't be relied upon.

## What's next

  - See the [Pipeline Queries overview](https://docs.cloud.google.com/firestore/docs/pipeline/overview)
