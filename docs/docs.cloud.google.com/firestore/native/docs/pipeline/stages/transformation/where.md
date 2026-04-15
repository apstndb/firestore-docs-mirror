# Where (Transformation Stage)

> **Preview — Firestore in Native mode (with Pipeline Operations) for Enterprise Edition**
> 
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . You can process personal data for this feature as outlined in the [Cloud Data Processing Addendum](https://docs.cloud.google.com/terms/data-processing-addendum) , subject to the obligations and restrictions described in the agreement under which you access Google Cloud. Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

## Description

Filters the documents from the previous stage, returning only the documents where the condition evaluates to `true` .

## Examples

### Web

    let results;
    
    results = await execute(db.pipeline().collection("books")
      .where(field("rating").equal(5))
      .where(field("published").lessThan(1900))
    );
    
    results = await execute(db.pipeline().collection("books")
      .where(and(field("rating").equal(5), field("published").lessThan(1900)))
    );test.firestore.js

##### Swift

    var results: Pipeline.Snapshot
    
    results = try await db.pipeline().collection("books")
      .where(Field("rating").equal(5))
      .where(Field("published").lessThan(1900))
      .execute()
    
    results = try await db.pipeline().collection("books")
      .where(Field("rating").equal(5) && Field("published").lessThan(1900))
      .execute()PipelineSnippets.swift

##### Kotlin  
Android

    var results: Task<Pipeline.Snapshot>
    
    results = db.pipeline().collection("books")
        .where(field("rating").equal(5))
        .where(field("published").lessThan(1900))
        .execute()
    
    results = db.pipeline().collection("books")
        .where(Expression.and(field("rating").equal(5),
          field("published").lessThan(1900)))
        .execute()DocSnippets.kt

##### Java  
Android

    Task<Pipeline.Snapshot> results;
    
    results = db.pipeline().collection("books")
        .where(field("rating").equal(5))
        .where(field("published").lessThan(1900))
        .execute();
    
    results = db.pipeline().collection("books")
        .where(Expression.and(
            field("rating").equal(5),
            field("published").lessThan(1900)
        ))
        .execute();DocSnippets.java

##### Python

    from google.cloud.firestore_v1.pipeline_expressions import And, Field
    
    results = (
        client.pipeline()
        .collection("books")
        .where(Field.of("rating").equal(5))
        .where(Field.of("published").less_than(1900))
        .execute()
    )
    
    results = (
        client.pipeline()
        .collection("books")
        .where(And(Field.of("rating").equal(5), Field.of("published").less_than(1900)))
        .execute()
    )firestore_pipelines.py

##### Java

    Pipeline.Snapshot results1 =
        firestore
            .pipeline()
            .collection("books")
            .where(field("rating").equal(5))
            .where(field("published").lessThan(1900))
            .execute()
            .get();
    
    Pipeline.Snapshot results2 =
        firestore
            .pipeline()
            .collection("books")
            .where(and(field("rating").equal(5), field("published").lessThan(1900)))
            .execute()
            .get();PipelineSnippets.java

## Behavior

### Multiple Stages

Multiple `where(...)` stages can be chained together, acting as an `and(...)` expression across each condition.

### Node.js

    const cities = await db.pipeline()
      .collection("/cities")
      .where(field("location.country").equals("USA"))
      .where(field("population").greaterThan(500000))
      .execute();

Filtering based on a logical `or` of two conditions though need to be done as a single `where(...)` stage though.

### Node.js

    const cities = await db.pipeline()
      .collection("/cities")
      .where(field("location.state").equals("NY").or(field("location.state").equals("CA")))
      .execute();

### Complex Expressions

The filter condition can contain complex filter conditions containing deeply nested expressions and logical operators. For example:

### Node.js

    const cities = await db.pipeline()
      .collection("/cities")
      .where(
        field("name").like("San%")
        .or(
          field("location.state").charLength().greaterThan(7)
          .and(field("location.country").equals("USA"))))

filters `/cities` based on a regular expression, or if the city is in the `USA` with a long enough state name. Any expression can be given as the condition, but will only match those which evaluate to `true` .

### Stage Ordering

The order of stages is important as it can change the query evaluation order. For example the query:

### Node.js

    const cities = await db.pipeline()
      .collection("/cities")
      .limit(10)
      .where(field("location.country").equals("USA"))
      .execute();

will only filter on `location.country` for a (potentially random) set of 10 documents as the prior `limit(...)` stage is restricting the documents that are ever provided to the `where(...)` stage. Given this, the rule of thumb is to put the `where(...)` stages as early in the query as possible.

**`HAVING` -Like Functionality:**

The `where(...)` stage can come after any stage that changes the schema of the documents, like `select(...)` or `aggregate(...)` and will refer to the fields produced from those stages. Importantly for `aggregate(...)` , a following `where(...)` clause that refers to the accumulated fields acts like a `HAVING` clause in a typical SQL system. For example:

### Node.js

    const cities = await db.pipeline()
      .collection("/cities")
      .aggregate({
        accumulators: [field("population").sum().as("total_population")],
        groups: ["location.state"]
      })
      .where(field("total_population").greaterThan(10000000))

allows returning the states which have cities over a total population size.
