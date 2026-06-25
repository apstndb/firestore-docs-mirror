---
name: documents/docs.cloud.google.com/firestore/native/docs/pipeline/functions/aggregate_functions
uri: https://docs.cloud.google.com/firestore/native/docs/pipeline/functions/aggregate_functions
title: Aggregate Functions Reference
description: Explains how to use aggregate functions like COUNT, SUM, AVG, MIN, and MAX in Firestore Pipeline operations.
data_source: docs.cloud.google.com
---

# Aggregate Functions Reference

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
      .execute();

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
    );

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
      .execute()

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
        .execute()

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
        .execute();

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
    )

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
            .get();

##### Go

    // Total number of books in the collection
    countAll, err := client.Pipeline().Collection("books").
     Aggregate(firestore.Accumulators(firestore.CountAll().As("count"))).
     Execute(ctx).Results().GetAll()
    if err != nil {
     fmt.Fprintf(w, "GetAll failed: %v", err)
     return err
    }
    
    // Number of books with nonnull `ratings` field
    countField, err := client.Pipeline().
     Collection("books").
     Aggregate(firestore.Accumulators(firestore.Count("ratings").As("count"))).
     Execute(ctx).Results().GetAll()
    if err != nil {
     fmt.Fprintf(w, "GetAll failed: %v", err)
     return err
    }

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
      .execute();

### Web

    const result = await execute(db.pipeline()
      .collection("books")
      .aggregate(
        field("rating").greaterThan(4).countIf().as("filteredCount")
      )
    );

##### Swift

    let result = try await db.pipeline()
      .collection("books")
      .aggregate([
        AggregateFunction("count_if", [Field("rating").greaterThan(4)]).as("filteredCount")
      ])
      .execute()

##### Kotlin  
Android

    val result = db.pipeline()
        .collection("books")
        .aggregate(
            AggregateFunction.countIf(field("rating").greaterThan(4)).alias("filteredCount")
        )
        .execute()

##### Java  
Android

    Task<Pipeline.Snapshot> result = db.pipeline()
        .collection("books")
        .aggregate(
            AggregateFunction.countIf(field("rating").greaterThan(4)).alias("filteredCount")
        )
        .execute();

##### Python

    from google.cloud.firestore_v1.pipeline_expressions import Field
    
    result = (
        client.pipeline()
        .collection("books")
        .aggregate(Field.of("rating").greater_than(4).count_if().as_("filteredCount"))
        .execute()
    )

##### Java

    Pipeline.Snapshot result =
        firestore
            .pipeline()
            .collection("books")
            .aggregate(countIf(field("rating").greaterThan(4)).as("filteredCount"))
            .execute()
            .get();

##### Go

    snapshot := client.Pipeline().
     Collection("books").
     Aggregate(firestore.Accumulators(
         firestore.CountIf(firestore.FieldOf("rating").GreaterThan(4)).As("filteredCount"),
     )).
     Execute(ctx)

### COUNT\_DISTINCT

**Syntax:**

    count_distinct(expression: ANY) -> INT64

**Description:**

Returns the number of unique non- `NULL` , non- `ABSENT` values of `expression` .

##### Node.js

    const result = await db.pipeline()
      .collection("books")
      .aggregate(field("author").countDistinct().as("unique_authors"))
      .execute();

### Web

    const result = await execute(db.pipeline()
      .collection("books")
      .aggregate(field("author").countDistinct().as("unique_authors"))
    );

##### Swift

    let result = try await db.pipeline()
      .collection("books")
      .aggregate([AggregateFunction("count_distinct", [Field("author")]).as("unique_authors")])
      .execute()

##### Kotlin  
Android

    val result = db.pipeline()
        .collection("books")
        .aggregate(AggregateFunction.countDistinct("author").alias("unique_authors"))
        .execute()

##### Java  
Android

    Task<Pipeline.Snapshot> result = db.pipeline()
        .collection("books")
        .aggregate(AggregateFunction.countDistinct("author").alias("unique_authors"))
        .execute();

##### Python

    from google.cloud.firestore_v1.pipeline_expressions import Field
    
    result = (
        client.pipeline()
        .collection("books")
        .aggregate(Field.of("author").count_distinct().as_("unique_authors"))
        .execute()
    )

##### Java

    Pipeline.Snapshot result =
        firestore
            .pipeline()
            .collection("books")
            .aggregate(countDistinct("author").as("unique_authors"))
            .execute()
            .get();

##### Go

    snapshot := client.Pipeline().
     Collection("books").
     Aggregate(firestore.Accumulators(
         firestore.CountDistinct("author").As("unique_authors"),
     )).
     Execute(ctx)

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
      .execute();

### Web

    const result = await execute(db.pipeline()
      .collection("cities")
      .aggregate(field("population").sum().as("totalPopulation"))
    );

##### Swift

    let result = try await db.pipeline()
      .collection("cities")
      .aggregate([Field("population").sum().as("totalPopulation")])
      .execute()

##### Kotlin  
Android

    val result = db.pipeline()
        .collection("cities")
        .aggregate(AggregateFunction.sum("population").alias("totalPopulation"))
        .execute()

##### Java  
Android

    Task<Pipeline.Snapshot> result = db.pipeline()
        .collection("cities")
        .aggregate(AggregateFunction.sum("population").alias("totalPopulation"))
        .execute();

##### Python

    from google.cloud.firestore_v1.pipeline_expressions import Field
    
    result = (
        client.pipeline()
        .collection("cities")
        .aggregate(Field.of("population").sum().as_("totalPopulation"))
        .execute()
    )

##### Java

    Pipeline.Snapshot result =
        firestore
            .pipeline()
            .collection("cities")
            .aggregate(sum("population").as("totalPopulation"))
            .execute()
            .get();

##### Go

    snapshot := client.Pipeline().
     Collection("cities").
     Aggregate(firestore.Accumulators(
         firestore.Sum("population").As("totalPopulation"),
     )).
     Execute(ctx)

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
      .execute();

### Web

    const result = await execute(db.pipeline()
      .collection("cities")
      .aggregate(field("population").average().as("averagePopulation"))
    );

##### Swift

    let result = try await db.pipeline()
      .collection("cities")
      .aggregate([Field("population").average().as("averagePopulation")])
      .execute()

##### Kotlin  
Android

    val result = db.pipeline()
        .collection("cities")
        .aggregate(AggregateFunction.average("population").alias("averagePopulation"))
        .execute()

##### Java  
Android

    Task<Pipeline.Snapshot> result = db.pipeline()
        .collection("cities")
        .aggregate(AggregateFunction.average("population").alias("averagePopulation"))
        .execute();

##### Python

    from google.cloud.firestore_v1.pipeline_expressions import Field
    
    result = (
        client.pipeline()
        .collection("cities")
        .aggregate(Field.of("population").average().as_("averagePopulation"))
        .execute()
    )

##### Java

    Pipeline.Snapshot result =
        firestore
            .pipeline()
            .collection("cities")
            .aggregate(average("population").as("averagePopulation"))
            .execute()
            .get();

##### Go

    snapshot := client.Pipeline().
     Collection("cities").
     Aggregate(firestore.Accumulators(
         firestore.Average("population").As("averagePopulation"),
     )).
     Execute(ctx)

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
      .execute();

### Web

    const result = await execute(db.pipeline()
      .collection("books")
      .aggregate(field("price").minimum().as("minimumPrice"))
    );

##### Swift

    let result = try await db.pipeline()
      .collection("books")
      .aggregate([Field("price").minimum().as("minimumPrice")])
      .execute()

##### Kotlin  
Android

    val result = db.pipeline()
        .collection("books")
        .aggregate(AggregateFunction.minimum("price").alias("minimumPrice"))
        .execute()

##### Java  
Android

    Task<Pipeline.Snapshot> result = db.pipeline()
        .collection("books")
        .aggregate(AggregateFunction.minimum("price").alias("minimumPrice"))
        .execute();

##### Python

    from google.cloud.firestore_v1.pipeline_expressions import Field
    
    result = (
        client.pipeline()
        .collection("books")
        .aggregate(Field.of("price").minimum().as_("minimumPrice"))
        .execute()
    )

##### Java

    Pipeline.Snapshot result =
        firestore
            .pipeline()
            .collection("books")
            .aggregate(minimum("price").as("minimumPrice"))
            .execute()
            .get();

##### Go

    snapshot := client.Pipeline().
     Collection("books").
     Aggregate(firestore.Accumulators(
         firestore.Minimum("price").As("minimumPrice"),
     )).
     Execute(ctx)

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
      .execute();

### Web

    const result = await execute(db.pipeline()
      .collection("books")
      .aggregate(field("price").maximum().as("maximumPrice"))
    );

##### Swift

    let result = try await db.pipeline()
      .collection("books")
      .aggregate([Field("price").maximum().as("maximumPrice")])
      .execute()

##### Kotlin  
Android

    val result = db.pipeline()
        .collection("books")
        .aggregate(AggregateFunction.maximum("price").alias("maximumPrice"))
        .execute()

##### Java  
Android

    Task<Pipeline.Snapshot> result = db.pipeline()
        .collection("books")
        .aggregate(AggregateFunction.maximum("price").alias("maximumPrice"))
        .execute();

##### Python

    from google.cloud.firestore_v1.pipeline_expressions import Field
    
    result = (
        client.pipeline()
        .collection("books")
        .aggregate(Field.of("price").maximum().as_("maximumPrice"))
        .execute()
    )

##### Java

    Pipeline.Snapshot result =
        firestore
            .pipeline()
            .collection("books")
            .aggregate(maximum("price").as("maximumPrice"))
            .execute()
            .get();

##### Go

    snapshot := client.Pipeline().
     Collection("books").
     Aggregate(firestore.Accumulators(
         firestore.Maximum("price").As("maximumPrice"),
     )).
     Execute(ctx)

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
