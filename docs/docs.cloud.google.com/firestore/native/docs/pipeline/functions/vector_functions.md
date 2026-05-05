# Vector Functions Reference

## **Vector Functions**

|                                       |                                                    |
| ------------------------------------- | -------------------------------------------------- |
| Name                                  | Description                                        |
| `         COSINE_DISTANCE        `    | Returns the cosine distance between two vectors    |
| `         DOT_PRODUCT        `        | Returns the dot product between two vectors        |
| `         EUCLIDEAN_DISTANCE        ` | Returns the euclidean distance between two vectors |
| `         MANHATTAN_DISTANCE        ` | Returns the manhattan distance between two vectors |
| `         VECTOR_LENGTH        `      | Returns the number of elements in a vector         |

### COSINE\_DISTANCE

**Syntax:**

    cosine_distance(x: VECTOR, y: VECTOR) -> FLOAT64

**Description:**

Returns the cosine distance between `x` and `y` .

##### Node.js

    const sampleVector = [0.0, 1, 2, 3, 4, 5];
    const result = await db.pipeline()
      .collection("books")
      .select(
        field("embedding").cosineDistance(sampleVector).as("cosineDistance")
      )
      .execute();

### Web

    const sampleVector = [0.0, 1, 2, 3, 4, 5];
    const result = await execute(db.pipeline()
      .collection("books")
      .select(
        field("embedding").cosineDistance(sampleVector).as("cosineDistance")));

##### Swift

    let sampleVector = [0.0, 1, 2, 3, 4, 5]
    let result = try await db.pipeline()
      .collection("books")
      .select([
        Field("embedding").cosineDistance(sampleVector).as("cosineDistance")
      ])
      .execute()

##### Kotlin  
Android

    val sampleVector = doubleArrayOf(0.0, 1.0, 2.0, 3.0, 4.0, 5.0)
    val result = db.pipeline()
        .collection("books")
        .select(
            field("embedding").cosineDistance(sampleVector).alias("cosineDistance")
        )
        .execute()

##### Java  
Android

    double[] sampleVector = {0.0, 1.0, 2.0, 3.0, 4.0, 5.0};
    Task<Pipeline.Snapshot> result = db.pipeline()
        .collection("books")
        .select(
            field("embedding").cosineDistance(sampleVector).alias("cosineDistance")
        )
        .execute();

##### Python

    from google.cloud.firestore_v1.pipeline_expressions import Field
    from google.cloud.firestore_v1.vector import Vector
    
    sample_vector = Vector([0.0, 1.0, 2.0, 3.0, 4.0, 5.0])
    result = (
        client.pipeline()
        .collection("books")
        .select(
            Field.of("embedding").cosine_distance(sample_vector).as_("cosineDistance")
        )
        .execute()
    )

##### Java

    double[] sampleVector = new double[] {0.0, 1.0, 2.0, 3.0, 4.0, 5.0};
    Pipeline.Snapshot result =
        firestore
            .pipeline()
            .collection("books")
            .select(cosineDistance(field("embedding"), sampleVector).as("cosineDistance"))
            .execute()
            .get();

### DOT\_PRODUCT

**Syntax:**

    dot_product(x: VECTOR, y: VECTOR) -> FLOAT64

**Description:**

Returns the dot product of `x` and `y` .

##### Node.js

    const sampleVector = [0.0, 1, 2, 3, 4, 5];
    const result = await db.pipeline()
      .collection("books")
      .select(
        field("embedding").dotProduct(sampleVector).as("dotProduct")
      )
      .execute();

### Web

    const sampleVector = [0.0, 1, 2, 3, 4, 5];
    const result = await execute(db.pipeline()
      .collection("books")
      .select(
        field("embedding").dotProduct(sampleVector).as("dotProduct")
      )
    );

##### Swift

    let sampleVector = [0.0, 1, 2, 3, 4, 5]
    let result = try await db.pipeline()
      .collection("books")
      .select([
        Field("embedding").dotProduct(sampleVector).as("dotProduct")
      ])
      .execute()

##### Kotlin  
Android

    val sampleVector = doubleArrayOf(0.0, 1.0, 2.0, 3.0, 4.0, 5.0)
    val result = db.pipeline()
        .collection("books")
        .select(
            field("embedding").dotProduct(sampleVector).alias("dotProduct")
        )
        .execute()

##### Java  
Android

    double[] sampleVector = {0.0, 1.0, 2.0, 3.0, 4.0, 5.0};
    Task<Pipeline.Snapshot> result = db.pipeline()
        .collection("books")
        .select(
            field("embedding").dotProduct(sampleVector).alias("dotProduct")
        )
        .execute();

##### Python

    from google.cloud.firestore_v1.pipeline_expressions import Field
    from google.cloud.firestore_v1.vector import Vector
    
    sample_vector = Vector([0.0, 1.0, 2.0, 3.0, 4.0, 5.0])
    result = (
        client.pipeline()
        .collection("books")
        .select(Field.of("embedding").dot_product(sample_vector).as_("dotProduct"))
        .execute()
    )

##### Java

    double[] sampleVector = new double[] {0.0, 1.0, 2.0, 3.0, 4.0, 5.0};
    Pipeline.Snapshot result =
        firestore
            .pipeline()
            .collection("books")
            .select(dotProduct(field("embedding"), sampleVector).as("dotProduct"))
            .execute()
            .get();

### EUCLIDEAN\_DISTANCE

**Syntax:**

    euclidean_distance(x: VECTOR, y: VECTOR) -> FLOAT64

**Description:**

Computes the euclidean distance between `x` and `y` .

##### Node.js

    const sampleVector = [0.0, 1, 2, 3, 4, 5];
    const result = await db.pipeline()
      .collection("books")
      .select(
        field("embedding").euclideanDistance(sampleVector).as("euclideanDistance")
      )
      .execute();

### Web

    const sampleVector = [0.0, 1, 2, 3, 4, 5];
    const result = await execute(db.pipeline()
      .collection("books")
      .select(
        field("embedding").euclideanDistance(sampleVector).as("euclideanDistance")
      )
    );

##### Swift

    let sampleVector = [0.0, 1, 2, 3, 4, 5]
    let result = try await db.pipeline()
      .collection("books")
      .select([
        Field("embedding").euclideanDistance(sampleVector).as("euclideanDistance")
      ])
      .execute()

##### Kotlin  
Android

    val sampleVector = doubleArrayOf(0.0, 1.0, 2.0, 3.0, 4.0, 5.0)
    val result = db.pipeline()
        .collection("books")
        .select(
            field("embedding").euclideanDistance(sampleVector).alias("euclideanDistance")
        )
        .execute()

##### Java  
Android

    double[] sampleVector = {0.0, 1.0, 2.0, 3.0, 4.0, 5.0};
    Task<Pipeline.Snapshot> result = db.pipeline()
        .collection("books")
        .select(
            field("embedding").euclideanDistance(sampleVector).alias("euclideanDistance")
        )
        .execute();

##### Python

    from google.cloud.firestore_v1.pipeline_expressions import Field
    from google.cloud.firestore_v1.vector import Vector
    
    sample_vector = Vector([0.0, 1.0, 2.0, 3.0, 4.0, 5.0])
    result = (
        client.pipeline()
        .collection("books")
        .select(
            Field.of("embedding")
            .euclidean_distance(sample_vector)
            .as_("euclideanDistance")
        )
        .execute()
    )

##### Java

    double[] sampleVector = new double[] {0.0, 1.0, 2.0, 3.0, 4.0, 5.0};
    Pipeline.Snapshot result =
        firestore
            .pipeline()
            .collection("books")
            .select(euclideanDistance(field("embedding"), sampleVector).as("euclideanDistance"))
            .execute()
            .get();

### MANHATTAN\_DISTANCE

**Syntax:**

    manhattan_distance(x: VECTOR, y: VECTOR) -> FLOAT64

**Description:**

Computes the manhattan distance between `x` and `y` .

### VECTOR\_LENGTH

**Syntax:**

    vector_length(vector: VECTOR) -> INT64

**Description:**

Returns the number of elements in a `VECTOR` .

##### Node.js

    const result = await db.pipeline()
      .collection("books")
      .select(
        field("embedding").vectorLength().as("vectorLength")
      )
      .execute();

### Web

    const result = await execute(db.pipeline()
      .collection("books")
      .select(
        field("embedding").vectorLength().as("vectorLength")
      )
    );

##### Swift

    let result = try await db.pipeline()
      .collection("books")
      .select([
        Field("embedding").vectorLength().as("vectorLength")
      ])
      .execute()

##### Kotlin  
Android

    val result = db.pipeline()
        .collection("books")
        .select(
            field("embedding").vectorLength().alias("vectorLength")
        )
        .execute()

##### Java  
Android

    Task<Pipeline.Snapshot> result = db.pipeline()
        .collection("books")
        .select(
            field("embedding").vectorLength().alias("vectorLength")
        )
        .execute();

##### Python

    from google.cloud.firestore_v1.pipeline_expressions import Field
    
    result = (
        client.pipeline()
        .collection("books")
        .select(Field.of("embedding").vector_length().as_("vectorLength"))
        .execute()
    )

##### Java

    Pipeline.Snapshot result =
        firestore
            .pipeline()
            .collection("books")
            .select(vectorLength(field("embedding")).as("vectorLength"))
            .execute()
            .get();

## What's next

  - See the [Pipeline Queries overview](https://docs.cloud.google.com/firestore/docs/pipeline/overview)
