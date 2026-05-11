---
name: documents/docs.cloud.google.com/firestore/native/docs/pipeline/functions/arithmetic_functions
uri: https://docs.cloud.google.com/firestore/native/docs/pipeline/functions/arithmetic_functions
title: Arithmetic Functions Reference
description: Explains how to use arithmetic functions like ABS, ADD, SUBTRACT, and MULTIPLY in Firestore Pipeline operations.
data_source: docs.cloud.google.com
---

# Arithmetic Functions Reference

## **Arithmetic Functions**

All arithmetic functions in Firestore have the following behaviors:

  - Evaluates to `NULL` if any of the input parameters is `NULL` .
  - Evaluates to `NaN` if any of the arguments is `NaN` .
  - Generates an error if an overflow or underflow occurs.

Additionally, when an arithmetic function takes multiple numeric arguments of different types (for example: `add(5.0, 6)` ), Firestore implicitly converts arguments to the widest input type. If only `INT32` inputs are provided, the return type will be `INT64` .

|                             |                                                          |
| --------------------------- | -------------------------------------------------------- |
| Name                        | Description                                              |
| `         ABS        `      | Returns the absolute value of a `number`                 |
| `         ADD        `      | Returns the value of `x + y`                             |
| `         SUBTRACT        ` | Returns the value of `x - y`                             |
| `         MULTIPLY        ` | Returns the value of `x * y`                             |
| `         DIVIDE        `   | Returns the value of `x / y`                             |
| `         MOD        `      | Returns the remainder of the division of `x / y`         |
| `         CEIL        `     | Returns the ceiling of a `number`                        |
| `         FLOOR        `    | Returns the floor of a `number`                          |
| `         ROUND        `    | Rounds a `number` to `places` decimal places             |
| `         TRUNC        `    | Truncates a `number` to `places` decimal places          |
| `         POW        `      | Returns the value of `base^exponent`                     |
| `         SQRT        `     | Returns the square root of a `number`                    |
| `         EXP        `      | Returns Euler's number raised to the power of `exponent` |
| `         LN        `       | Returns the natural logarithm of a `number`              |
| `         LOG        `      | Returns the logarithm of a `number`                      |
| `         LOG10        `    | Returns the logarithm of a `number` to base `10`         |
| `         RAND        `     | Returns a pseudo-random floating point number            |

### ABS

**Syntax:**

    abs[N <: INT32 | INT64 | FLOAT64](number: N) -> N

**Description:**

Returns the absolute value of a `number` .

  - Throws an error when the function would overflow an `INT32` or `INT64` value.

**Examples:**

| number            | `abs(number)` |
| :---------------- | :------------ |
| 10                | 10            |
| \-10              | 10            |
| 10L               | 10L           |
| \-0.0             | 0.0           |
| 10.5              | 10.5          |
| \-10.5            | 10.5          |
| \-2 <sup>31</sup> | `[error]`     |
| \-2 <sup>63</sup> | `[error]`     |

### ADD

**Syntax:**

    add[N <: INT32 | INT64 | FLOAT64](x: N, y: N) -> N

**Description:**

Returns the value of `x + y` .

**Examples:**

| x         | y   | `add(x, y)` |
| :-------- | :-- | :---------- |
| 20        | 3   | 23          |
| 10.0      | 1   | 11.0        |
| 22.5      | 2.0 | 24.5        |
| INT64.MAX | 1   | `[error]`   |
| INT64.MIN | \-1 | `[error]`   |

##### Node.js

    const result = await db.pipeline()
      .collection("books")
      .select(field("soldBooks").add(field("unsoldBooks")).as"))
      .execute();test.firestore.js

### Web

    const result = await execute(db.pipeline()
      .collection("books")
      .select(field("soldBooks").add(field("unsoldBookt;totalBooks"))
    );test.firestore.js

##### Swift

    let result = try await db.pipeline()
      .collection("books")
      .select([Field("soldBooks").add(Field("unsoldBooks")).at;)])
      .execute()PipelineSnippets.swift

##### Kotlin  
Android

    val result = db.pipeline()
        .collection("books")
        .select(Expression.add(field("soldBooks"), field("unsoldBooks")).aliasoks"))
        .execute()DocSnippets.kt

##### Java  
Android

``` 
Task<Pipeline.Snapshot> result = db.pipeline()
    .collection("books")
    .select(Expression.add(field("soldBooks"), field("unsoldBooks")).alias("))
    .execute();DocSnippets.java
    
```

##### Python

    from google.cloud.firestore_v1.pipeline_expressions import Field
    
    result = (
        client.pipeline()
        .collection("books")
        .select(Field.of("soldBooks").add(Field.of("unsoldBooks")).as_(&)
        .execute()
    )firestore_pipelines.py

##### Java

    Pipeline.Snapshot result =
        firestore
            .pipeline()
            .collection("books")
            .select(add(field("soldBooks"), field("unsoldBooks")).as("totalBooks&que()
            .get();PipelineSnippets.java

### SUBTRACT

**Syntax:**

    subtract[N <: INT32 | INT64 | FLOAT64](x: N, y: N) -> N

**Description:**

Returns the value of `x - y` .

**Examples:**

| x         | y   | `subtract(x, y)` |
| :-------- | :-- | :--------------- |
| 20        | 3   | 17               |
| 10.0      | 1   | 9.0              |
| 22.5      | 2.0 | 20.5             |
| INT64.MAX | \-1 | `[error]`        |
| INT64.MIN | 1   | `[error]`        |

##### Node.js

    const storeCredit = 7;
    const result = await db.pipeline()
      .collection("books")
      .select(field("price").subtract(constant(storeCredit)).as("t  .execute();test.firestore.js

### Web

    const storeCredit = 7;
    const result = await execute(db.pipeline()
      .collection("books")
      .select(field("price").subtract(constant(storeCredit))st"))
    );test.firestore.js

##### Swift

    let storeCredit = 7
    let result = try await db.pipeline()
      .collection("books")
      .select([Field("price").subtract(Constant(storeCredit)).as("txecute()PipelineSnippets.swift

##### Kotlin  
Android

    val storeCredit = 7
    val result = db.pipeline()
        .collection("books")
        .select(Expression.subtract(field("price"), storeCredit).alias("to)
        .execute()DocSnippets.kt

##### Java  
Android

``` 
int storeCredit = 7;
Task<Pipeline.Snapshot> result = db.pipeline()
    .collection("books")
    .select(Expression.subtract(field("price"), storeCredit).alias("tot   .execute();DocSnippets.java
    
```

##### Python

    from google.cloud.firestore_v1.pipeline_expressions import Field
    
    store_credit = 7
    result = (
        client.pipeline()
        .collection("books")
        .select(Field.of("price").subtract(store_credit).as_("totacute()
    )firestore_pipelines.py

##### Java

    int storeCredit = 7;
    Pipeline.Snapshot result =
        firestore
            .pipeline()
            .collection("books")
            .select(subtract(field("price"), storeCredit).as("totalCost"))
          .get();PipelineSnippets.java

### MULTIPLY

**Syntax:**

    multiply[N <: INT32 | INT64 | FLOAT64](x: N, y: N) -> N

**Description:**

Returns the value of `x * y` .

**Examples:**

| x           | y           | `multiply(x, y)` |
| :---------- | :---------- | :--------------- |
| 20          | 3           | 60               |
| 10.0        | 1           | 10.0             |
| 22.5        | 2.0         | 45.0             |
| INT64.MAX   | 2           | `[error]`        |
| INT64.MIN   | 2           | `[error]`        |
| FLOAT64.MAX | FLOAT64.MAX | `+inf`           |

##### Node.js

    const result = await db.pipeline()
      .collection("books")
      .select(field("price").multiply(field("soldBooks")e"))
      .execute();test.firestore.js

### Web

    const result = await execute(db.pipeline()
      .collection("books")
      .select(field("price").multiply(field("soldBquot;revenue"))
    );test.firestore.js

##### Swift

    let result = try await db.pipeline()
      .collection("books")
      .select([Field("price").multiply(Field("soldBooks")t;)])
      .execute()PipelineSnippets.swift

##### Kotlin  
Android

    val result = db.pipeline()
        .collection("books")
        .select(Expression.multiply(field("price"), field("soldBooks")).alnue"))
        .execute()DocSnippets.kt

##### Java  
Android

``` 
Task<Pipeline.Snapshot> result = db.pipeline()
    .collection("books")
    .select(Expression.multiply(field("price"), field("soldBooks")).ali"))
    .execute();DocSnippets.java
    
```

##### Python

    from google.cloud.firestore_v1.pipeline_expressions import Field
    
    result = (
        client.pipeline()
        .collection("books")
        .select(Field.of("price").multiply(Field.of("soldBooks")).as)
        .execute()
    )firestore_pipelines.py

##### Java

    Pipeline.Snapshot result =
        firestore
            .pipeline()
            .collection("books")
            .select(multiply(field("price"), field("soldBooks")).as("revenue&que()
            .get();PipelineSnippets.java

### DIVIDE

**Syntax:**

    divide[N <: INT32 | INT64 | FLOAT64](x: N, y: N) -> N

**Description:**

Returns the value of `x / y` . Integer division is truncated.

**Examples:**

| x     | y   | `divide(x, y)` |
| :---- | :-- | :------------- |
| 20    | 3   | 6              |
| 10.0  | 3   | 3.333...       |
| 22.5  | 2   | 11.25          |
| 10    | 0   | `[error]`      |
| 1.0   | 0.0 | `+inf`         |
| \-1.0 | 0.0 | `-inf`         |

##### Node.js

    const result = await db.pipeline()
      .collection("books")
      .select(field("ratings").divide(field("soldBooks")).ae"))
      .execute();test.firestore.js

### Web

    const result = await execute(db.pipeline()
      .collection("books")
      .select(field("ratings").divide(field("soldBookt;reviewRate"))
    );test.firestore.js

##### Swift

    let result = try await db.pipeline()
      .collection("books")
      .select([Field("ratings").divide(Field("soldBooks")).at;)])
      .execute()PipelineSnippets.swift

##### Kotlin  
Android

    val result = db.pipeline()
        .collection("books")
        .select(Expression.divide(field("ratings"), field("soldBooks")).aliasate"))
        .execute()DocSnippets.kt

##### Java  
Android

``` 
Task<Pipeline.Snapshot> result = db.pipeline()
    .collection("books")
    .select(Expression.divide(field("ratings"), field("soldBooks")).alias("))
    .execute();DocSnippets.java
    
```

##### Python

    from google.cloud.firestore_v1.pipeline_expressions import Field
    
    result = (
        client.pipeline()
        .collection("books")
        .select(Field.of("ratings").divide(Field.of("soldBooks")).as_(&)
        .execute()
    )firestore_pipelines.py

##### Java

    Pipeline.Snapshot result =
        firestore
            .pipeline()
            .collection("books")
            .select(divide(field("ratings"), field("soldBooks")).as("reviewRate&que()
            .get();PipelineSnippets.java

### MOD

**Syntax:**

    mod[N <: INT32 | INT64 | FLOAT64](x: N, y: N) -> N

**Description:**

Returns the remainder of `x / y` .

  - Throws an `error` when `y` is zero for integer types ( `INT64` ).
  - Returns `NaN` when `y` is zero for float types ( `FLOAT64` ).

**Examples:**

| x    | y   | `mod(x, y)` |
| :--- | :-- | :---------- |
| 20   | 3   | 2           |
| \-10 | 3   | \-1         |
| 10   | \-3 | 1           |
| \-10 | \-3 | \-1         |
| 10   | 1   | 0           |
| 22.5 | 2   | 0.5         |
| 22.5 | 0.0 | `NaN`       |
| 25   | 0   | `[error]`   |

##### Node.js

    const displayCapacity = 1000;
    const result = await db.pipeline()
      .collection("books")
      .select(field("unsoldBooks").mod(constant(displayCapacity)).as("warehou  .execute();test.firestore.js

### Web

    const displayCapacity = 1000;
    const result = await execute(db.pipeline()
      .collection("books")
      .select(field("unsoldBooks").mod(constant(displayCapacity)).as(&qks"))
    );test.firestore.js

##### Swift

    let displayCapacity = 1000
    let result = try await db.pipeline()
      .collection("books")
      .select([Field("unsoldBooks").mod(Constant(displayCapacity)).as("warehouxecute()PipelineSnippets.swift

##### Kotlin  
Android

    val displayCapacity = 1000
    val result = db.pipeline()
        .collection("books")
        .select(Expression.mod(field("unsoldBooks"), displayCapacity).alias("warehous)
        .execute()DocSnippets.kt

##### Java  
Android

``` 
int displayCapacity = 1000;
Task<Pipeline.Snapshot> result = db.pipeline()
    .collection("books")
    .select(Expression.mod(field("unsoldBooks"), displayCapacity).alias("warehouse   .execute();DocSnippets.java
    
```

##### Python

    from google.cloud.firestore_v1.pipeline_expressions import Field
    
    display_capacity = 1000
    result = (
        client.pipeline()
        .collection("books")
        .select(Field.of("unsoldBooks").mod(display_capacity).as_("warehousedcute()
    )firestore_pipelines.py

##### Java

    int displayCapacity = 1000;
    Pipeline.Snapshot result =
        firestore
            .pipeline()
            .collection("books")
            .select(mod(field("unsoldBooks"), displayCapacity).as("warehousedBooks"))
          .get();PipelineSnippets.java

### CEIL

**Syntax:**

    ceil[N <: INT32 | INT64 | FLOAT64](number: N) -> N

**Description:**

Returns the smallest integer value that isn't less than `number` .

**Examples:**

| number | `ceil(number)` |
| :----- | :------------- |
| 20     | 20             |
| 10     | 10             |
| 0      | 0              |
| 24L    | 24L            |
| \-0.4  | \-0.0          |
| 0.4    | 1.0            |
| 22.5   | 23.0           |
| `+inf` | `+inf`         |
| `-inf` | `-inf`         |

##### Node.js

    const booksPerShelf = 100;
    const result = await db.pipeline()
      .collection("books")
      .select(
        field("unsoldBooks").divide(constant(booksPerShelf)).ceil().as("requiredSh  .execute();test.firestore.js

### Web

    const booksPerShelf = 100;
    const result = await execute(db.pipeline()
      .collection("books")
      .select(
        field("unsoldBooks").divide(constant(booksPerShelf)).ceil().as("quot;)
      )
    );test.firestore.js

##### Swift

    let booksPerShelf = 100
    let result = try await db.pipeline()
      .collection("books")
      .select([
        Field("unsoldBooks").divide(Constant(booksPerShelf)).ceil().as("requiredShxecute()PipelineSnippets.swift

##### Kotlin  
Android

    val booksPerShelf = 100
    val result = db.pipeline()
        .collection("books")
        .select(
            Expression.divide(field("unsoldBooks"), booksPerShelf).ceil().alias("requiredShelv)
        .execute()DocSnippets.kt

##### Java  
Android

``` 
int booksPerShelf = 100;
Task<Pipeline.Snapshot> result = db.pipeline()
    .collection("books")
    .select(
        Expression.divide(field("unsoldBooks"), booksPerShelf).ceil().alias("requiredShelve   .execute();DocSnippets.java
    
```

##### Python

    from google.cloud.firestore_v1.pipeline_expressions import Field
    
    books_per_shelf = 100
    result = (
        client.pipeline()
        .collection("books")
        .select(
            Field.of("unsoldBooks")
            .divide(books_per_shelf)
            .ceil()
            .as_("requiredShelvescute()
    )firestore_pipelines.py

##### Java

    int booksPerShelf = 100;
    Pipeline.Snapshot result =
        firestore
            .pipeline()
            .collection("books")
            .select(ceil(divide(field("unsoldBooks"), booksPerShelf)).as("requiredShelves"))
          .get();PipelineSnippets.java

### FLOOR

**Syntax:**

    floor[N <: INT32 | INT64 | FLOAT64](number: N) -> N

**Description:**

Returns the largest integer value that isn't greater than `number` .

**Examples:**

| number     | `floor(number)` |
| :--------- | :-------------- |
| 20         | 20              |
| 10         | 10              |
| 0          | 0               |
| 2147483648 | 2147483648      |
| \-0.4      | \-1.0           |
| 0.4        | 0.0             |
| 22.5       | 22.0            |
| `+inf`     | `+inf`          |
| `-inf`     | `-inf`          |

##### Node.js

    const result = await db.pipeline()
      .collection("books")
      .addFields(
        field("wordCount").divide(field("pages")).floor().as(&quuot;)
      )
      .execute();test.firestore.js

### Web

    const result = await execute(db.pipeline()
      .collection("books")
      .addFields(
        field("wordCount").divide(field("pages")).flodsPerPage")
      )
    );test.firestore.js

##### Swift

    let result = try await db.pipeline()
      .collection("books")
      .addFields([
        Field("wordCount").divide(Field("pages")).floor().as(&qu
      ])
      .execute()PipelineSnippets.swift

##### Kotlin  
Android

    val result = db.pipeline()
        .collection("books")
        .addFields(
            Expression.divide(field("wordCount"), field("pages")).floor().alias("uot;)
        )
        .execute()DocSnippets.kt

##### Java  
Android

``` 
Task<Pipeline.Snapshot> result = db.pipeline()
    .collection("books")
    .addFields(
        Expression.divide(field("wordCount"), field("pages")).floor().alias("w;)
    )
    .execute();DocSnippets.java
    
```

##### Python

    from google.cloud.firestore_v1.pipeline_expressions import Field
    
    result = (
        client.pipeline()
        .collection("books")
        .add_fields(
            Field.of("wordCount").divide(Field.of("pages")).floor().as_("wo)
        .execute()
    )firestore_pipelines.py

##### Java

    Pipeline.Snapshot result =
        firestore
            .pipeline()
            .collection("books")
            .addFields(floor(divide(field("wordCount"), field("pages"))).as("wordsPerPage&que()
            .get();PipelineSnippets.java

### ROUND

**Syntax:**

    round[N <: INT32 | INT64 | FLOAT64 | DECIMAL128](number: N) -> N
    round[N <: INT32 | INT64 | FLOAT64 | DECIMAL128](number: N, places: INT64) -> N

**Description:**

Rounds `places` digits off a `number` . Rounds digits from the right of the decimal point if `places` is positive, and to the left of the decimal point if it is negative.

  - If only `number` is provided, rounds to the nearest whole value.
  - Rounds away from zero in halfway cases.
  - An `error` is thrown if rounding with a negative `places` value results in overflow.

**Examples:**

| number              | places | `round(number, places)` |
| :------------------ | :----- | :---------------------- |
| 15.5                | 0      | 16.0                    |
| \-15.5              | 0      | \-16.0                  |
| 15                  | 1      | 15                      |
| 15                  | 0      | 15                      |
| 15                  | \-1    | 20                      |
| 15                  | \-2    | 0                       |
| 15.48924            | 1      | 15.5                    |
| 2 <sup>31</sup> -1  | \-1    | `[error]`               |
| 2 <sup>63</sup> -1L | \-1    | `[error]`               |

##### Node.js

    const result = await db.pipeline()
      .collection("books")
      .select(field("soldBooks").multiply(field("price")).round().as("partialRevenue"))
      .aggregate(field("partialReveas("totalRevenue"))
      .execute();test.firestore.js

### Web

    const result = await execute(db.pipeline()
      .collection("books")
      .select(field("soldBooks").multiply(field("price")).round().as("partialRevenue"))
      .aggregate(field("pa;).sum().as("totalRevenue"))
      );test.firestore.js

##### Swift

    let result = try await db.pipeline()
      .collection("books")
      .select([Field("soldBooks").multiply(Field("price")).round().as("partialRevenue")])
      .aggregate([Field("partialReveuot;totalRevenue")])
      .execute()PipelineSnippets.swift

##### Kotlin  
Android

    val result = db.pipeline()
        .collection("books")
        .select(Expression.multiply(field("soldBooks"), field("price")).round().alias("partialRevenue"))
        .aggregate(AggregateFunction.sum("partialRelias("totalRevenue"))
        .execute()DocSnippets.kt

##### Java  
Android

``` 
Task<Pipeline.Snapshot> result = db.pipeline()
    .collection("books")
    .select(Expression.multiply(field("soldBooks"), field("price")).round().alias("partialRevenue"))
    .aggregate(AggregateFunction.sum("partialRevs("totalRevenue"))
    .execute();DocSnippets.java
    
```

##### Python

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
        .aggregate(Field.of("partialRevenue&;totalRevenue"))
        .execute()
    )firestore_pipelines.py

##### Java

    Pipeline.Snapshot result =
        firestore
            .pipeline()
            .collection("books")
            .select(round(multiply(field("soldBooks"), field("price"))).as("partialRevenue"))
            .aggregate(sum("partialRevenue").as(&t;))
            .execute()
            .get();PipelineSnippets.java

### TRUNC

**Syntax:**

    trunc[N <: Number](number: N) -> N
    trunc[N <: Number](number:  N, places: INT64) -> N

**Description:**

Truncates a `number` to a specified number of `places` decimal places. Truncates digits from the right of the decimal point if `places` is positive, and to the left of the decimal point if it is negative.

  - If only `number` is provided, truncates to the nearest whole value towards zero.
  - An `error` is thrown if truncating results in overflow.

**Examples:**

| number     | places | `trunc(number, places)` |
| :--------- | :----- | :---------------------- |
| 15.5       | 0      | 15.0                    |
| \-15.5     | 0      | \-15.0                  |
| 15         | 1      | 15                      |
| 15         | 0      | 15                      |
| 15         | \-1    | 10                      |
| 15         | \-2    | 0                       |
| 15.48924   | 1      | 15.4                    |
| \-15.48924 | 2      | \-15.48                 |

### POW

**Syntax:**

    pow(base: FLOAT64, exponent: FLOAT64) -> FLOAT64

**Description:**

Returns the value `base` raised to the power of `exponent` .

  - Throws an error if `base <= 0` and `exponent` is negative.

  - For any `exponent` , `pow(1, exponent)` is 1.

  - For any `base` , `pow(base, 0)` is 1.

**Examples:**

| base   | exponent | `pow(base, exponent)` |
| :----- | :------- | :-------------------- |
| 2      | 3        | 8.0                   |
| 2      | \-3      | 0.125                 |
| `+inf` | 0        | 1.0                   |
| 1      | `+inf`   | 1.0                   |
| \-1    | 0.5      | `[error]`             |
| 0      | \-1      | `[error]`             |

##### Node.js

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
          // Inaccurate for large distances or clo .as("approximateDistanceToGoogle")
      )
      .execute();test.firestore.js

### Web

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
          // Inaccurate for large distapoles
          .as("approximateDistanceToGoogle")
      )
    );test.firestore.js

##### Swift

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
          // Inaccurate for large distances or clo"approximateDistanceToGoogle")
      ])
      .execute()PipelineSnippets.swift

##### Kotlin  
Android

    val googleplex = GeoPoint(37.4221, -122.0853)
    val result = db.pipeline()
        .collection("cities")
        .addFields(
            field("lat").subtract(googleplex.latitude)
                .multiply(111) // km per degree
                .pow(2)
                .alias("latitudeDifference"),
            field("lng").subtract(googleplex.longitude)
                .multiply(111) // km per degree
                .pow(2)
                .alias("longitudeDifference")
        )
        .select(
            field("latitudeDifference").add(field("longitudeDifference")).sqrt()
                // Inaccurate for large distances or close to poles
    lias("approximateDistanceToGoogle")
        )
        .execute()DocSnippets.kt

##### Java  
Android

``` 
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
 s("approximateDistanceToGoogle")
    )
    .execute();DocSnippets.java
    
```

##### Python

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
            # Inaccurate for large distances or close to po;approximateDistanceToGoogle")
        )
        .execute()
    )firestore_pipelines.py

##### Java

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
                    DistanceToGoogle"))
            .execute()
            .get();PipelineSnippets.java

### SQRT

**Syntax:**

    sqrt[N <: FLOAT64 | DECIMAL128](number: N) -> N

**Description:**

Returns the square root of a `number` .

  - Throws an `error` if `number` is negative.

**Examples:**

| number  | `sqrt(number)` |
| :------ | :------------- |
| 25      | 5.0            |
| 12.002  | 3.464...       |
| 0.0     | 0.0            |
| `NaN`   | `NaN`          |
| `+inf`  | `+inf`         |
| `-inf`  | `[error]`      |
| `x < 0` | `[error]`      |

##### Node.js

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
          // Inaccurate for large distances or clo .as("approximateDistanceToGoogle")
      )
      .execute();test.firestore.js

### Web

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
          // Inaccurate for large distapoles
          .as("approximateDistanceToGoogle")
      )
    );test.firestore.js

##### Swift

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
          // Inaccurate for large distances or clo"approximateDistanceToGoogle")
      ])
      .execute()PipelineSnippets.swift

##### Kotlin  
Android

    val googleplex = GeoPoint(37.4221, -122.0853)
    val result = db.pipeline()
        .collection("cities")
        .addFields(
            field("lat").subtract(googleplex.latitude)
                .multiply(111) // km per degree
                .pow(2)
                .alias("latitudeDifference"),
            field("lng").subtract(googleplex.longitude)
                .multiply(111) // km per degree
                .pow(2)
                .alias("longitudeDifference")
        )
        .select(
            field("latitudeDifference").add(field("longitudeDifference")).sqrt()
                // Inaccurate for large distances or close to poles
    lias("approximateDistanceToGoogle")
        )
        .execute()DocSnippets.kt

##### Java  
Android

``` 
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
 s("approximateDistanceToGoogle")
    )
    .execute();DocSnippets.java
    
```

##### Python

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
            # Inaccurate for large distances or close to po;approximateDistanceToGoogle")
        )
        .execute()
    )firestore_pipelines.py

##### Java

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
                    DistanceToGoogle"))
            .execute()
            .get();PipelineSnippets.java

### EXP

**Syntax:**

    exp(exponent: FLOAT64) -> FLOAT64

**Description:**

Returns the value of Euler's number raised to the power of `exponent` , also called the natural exponential function.

**Examples:**

| exponent | `exp(exponent)`      |
| :------- | :------------------- |
| 0.0      | 1.0                  |
| 10       | `e^10` ( `FLOAT64` ) |
| `+inf`   | `+inf`               |
| `-inf`   | 0                    |

##### Node.js

    const result = await db.pipeline()
      .collection("books")
      .select(field("rating").exp().as("e  .execute();test.firestore.js

### Web

    const result = await execute(db.pipeline()
      .collection("books")
      .select(field("rating").exp()ng"))
    );test.firestore.js

##### Swift

    let result = try await db.pipeline()
      .collection("books")
      .select([Field("rating").exp().as("execute()PipelineSnippets.swift

##### Kotlin  
Android

    val result = db.pipeline()
        .collection("books")
        .select(field("rating").exp().alias("ex)
        .execute()DocSnippets.kt

##### Java  
Android

``` 
Task<Pipeline.Snapshot> result = db.pipeline()
    .collection("books")
    .select(field("rating").exp().alias("exp   .execute();DocSnippets.java
    
```

##### Python

    from google.cloud.firestore_v1.pipeline_expressions import Field
    
    result = (
        client.pipeline()
        .collection("books")
        .select(Field.of("rating").exp().as_("expRcute()
    )firestore_pipelines.py

##### Java

    Pipeline.Snapshot result =
        firestore
            .pipeline()
            .collection("books")
            .select(exp(field("rating")).as("expRating"))
          .get();PipelineSnippets.java

### LN

**Syntax:**

    ln(number: FLOAT64) -> FLOAT64

**Description:**

Returns the natural logarithm of `number` . This function is equivalent to `log(number)` .

**Examples:**

| number            | `ln(number)` |
| :---------------- | :----------- |
| 1                 | 0.0          |
| 2L                | 0.693...     |
| 1.0               | 0.0          |
| `e` ( `FLOAT64` ) | 1.0          |
| `-inf`            | `NaN`        |
| `+inf`            | `+inf`       |
| `x <= 0`          | `[error]`    |

##### Node.js

    const result = await db.pipeline()
      .collection("books")
      .select(field("rating").ln().as("  .execute();test.firestore.js

### Web

    const result = await execute(db.pipeline()
      .collection("books")
      .select(field("rating").ln(ng"))
    );test.firestore.js

##### Swift

    let result = try await db.pipeline()
      .collection("books")
      .select([Field("rating").ln().as("xecute()PipelineSnippets.swift

##### Kotlin  
Android

    val result = db.pipeline()
        .collection("books")
        .select(field("rating").ln().alias("l)
        .execute()DocSnippets.kt

##### Java  
Android

``` 
Task<Pipeline.Snapshot> result = db.pipeline()
    .collection("books")
    .select(field("rating").ln().alias("ln   .execute();DocSnippets.java
    
```

##### Python

    from google.cloud.firestore_v1.pipeline_expressions import Field
    
    result = (
        client.pipeline()
        .collection("books")
        .select(Field.of("rating").ln().as_("lnRcute()
    )firestore_pipelines.py

##### Java

    Pipeline.Snapshot result =
        firestore
            .pipeline()
            .collection("books")
            .select(ln(field("rating")).as("lnRating"))
          .get();PipelineSnippets.java

### LOG

**Syntax:**

    log(number: FLOAT64, base: FLOAT64) -> FLOAT64
    log(number: FLOAT64) -> FLOAT64

**Description:**

Returns the logarithm of a `number` to `base` .

  - If only `number` is provided, returns the logarithm of `number` to `base` (synonymous to `ln(number)` ).

**Examples:**

| number        | base        | `log(number, base)` |
| :------------ | :---------- | :------------------ |
| 100           | 10          | 2.0                 |
| `-inf`        | `Numeric`   | `NaN`               |
| `Numeric` .   | `+inf`      | `NaN`               |
| `number <= 0` | `Numeric`   | `[error]`           |
| `Numeric`     | `base <= 0` | `[error]`           |
| `Numeric`     | 1.0         | `[error]`           |

### LOG10

**Syntax:**

    log10(x: FLOAT64) -> FLOAT64

**Description:**

Returns the logarithm of a `number` to base `10` .

**Examples:**

| number   | `log10(number)` |
| :------- | :-------------- |
| 100      | 2.0             |
| `-inf`   | `NaN`           |
| `+inf`   | `+inf`          |
| `x <= 0` | `[error]`       |

### RAND

**Syntax:**

    rand() -> FLOAT64

**Description:**

Return a pseudo-random floating point number, chosen uniformly between `0.0` (inclusive) and `1.0` (exclusive).

## What's next

  - See the [Pipeline Queries overview](https://docs.cloud.google.com/firestore/docs/pipeline/overview)
