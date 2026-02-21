# Get started with Pipeline Queries

**Preview — Firestore in Native mode (with Pipeline Operations) for Enterprise Edition**

This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](/terms/service-terms#1) . You can process personal data for this feature as outlined in the [Cloud Data Processing Addendum](/terms/data-processing-addendum) , subject to the obligations and restrictions described in the agreement under which you access Google Cloud. Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

## Background

Pipeline operations are a new query interface for Firestore. This interface provides advanced query functionality that includes complex expressions. It also adds support for many new functions like `  min, max, substring, regex_match  ` and `  array_contains_all  ` .

With Pipeline operations, index creation is also completely optional, streamlining the process of developing new queries. Pipeline operations also remove many limitations on query shape allowing you to specify large `  in  ` or `  or  ` queries.

## Getting Started

To install and initialize client SDKs, refer to the instructions in the following guides:

  - [Get started with mobile and web SDKs](/firestore/native/docs/create-database-web-mobile-client-library#initialize) .
  - [Get started with server client libraries](/firestore/native/docs/create-database-server-client-library#add_the_server_client_library_to_your_app) .

## Syntax

The following sections give an overview of the syntax for Pipeline operations.

### Concepts

One notable difference with Pipeline operations is the introduction of explicit "stage" ordering. This makes it possible to express more complex queries. However, it is a notable deviation from the existing query interface (Core operations) where the ordering of stages was implied. Consider the following Pipeline operation example:

##### Node.js

``` text
  db.pipeline()
    .collection() // Step 1 (start a query with 'collection' scope)
    .where()      // Step 2 (filter collection)
    .sort()       // Step 3 (order results)
    .limit()      // Step 4 (limit results)

  // Note: Applying a limit before a sort can yield unintended
  // results (as the limit would be applied before sorting).
    
```

### Web

``` javascript
const pipeline = db.pipeline()
  // Step 1: Start a query with collection scope
  .collection("cities")
  // Step 2: Filter the collection
  .where(field("population").greaterThan(100000))
  // Step 3: Sort the remaining documents
  .sort(field("name").ascending())
  // Step 4: Return the top 10. Note applying the limit earlier in the
  // pipeline would have unintentional results.
  .limit(10);test.firestore.js
```

##### Swift

``` swift
let pipeline = db.pipeline()
  // Step 1: Start a query with collection scope
  .collection("cities")
  // Step 2: Filter the collection
  .where(Field("population").greaterThan(100000))
  // Step 3: Sort the remaining documents
  .sort([Field("name").ascending()])
  // Step 4: Return the top 10. Note applying the limit earlier in the pipeline would have
  // unintentional results.
  .limit(10)PipelineSnippets.swift
```

##### Kotlin  
Android

``` kotlin
val pipeline = db.pipeline()
    // Step 1: Start a query with collection scope
    .collection("cities")
    // Step 2: Filter the collection
    .where(field("population").greaterThan(100000))
    // Step 3: Sort the remaining documents
    .sort(field("name").ascending())
    // Step 4: Return the top 10. Note applying the limit earlier in the pipeline would have
    // unintentional results.
    .limit(10)DocSnippets.kt
```

##### Java  
Android

``` text
Pipeline pipeline = db.pipeline()
    // Step 1: Start a query with collection scope
    .collection("cities")
    // Step 2: Filter the collection
    .where(field("population").greaterThan(100000))
    // Step 3: Sort the remaining documents
    .sort(field("name").ascending())
    // Step 4: Return the top 10. Note applying the limit earlier in the pipeline would have
    // unintentional results.
    .limit(10);DocSnippets.java
```

##### Python

``` python
from google.cloud.firestore_v1.pipeline_expressions import Field

pipeline = (
    client.pipeline()
    .collection("cities")
    .where(Field.of("population").greater_than(100_000))
    .sort(Field.of("name").ascending())
    .limit(10)
)firestore_pipelines.py
```

### Initialization

Pipeline operations have a very familiar syntax coming from existing Firestore queries. To get started, you initialize a query by writing the following:

##### Node.js

``` text
  const db = new Firestore({ projectId: '', databaseId: databaseId'})
  db.pipeline()
    
```

##### Java

``` text
  Firestore db = FirestoreOptions.newBuilder().build().getService();
  db.pipeline()
    
```

### Structure

There are a few terms that are important to understand when creating Pipeline operations: stages, expressions, and functions.

**Stages:** A pipeline may consist of one or more stages. Logically, these represent the series of steps (or stages) taken to execute the query. Note: In practice, stages may be executed out of order to improve performance. However, this does not modify the intent or correctness of the query.

**Expressions:** Stages will often accept an expression allowing you to express more complex queries. Expression may be simple and consist of a single function like `  eq("a", 1)  ` . You can also express more complex expressions by nesting expressions like `  and(eq("a", 1), eq("b", 2)).  `

### Field vs. Constant References

Pipeline operations support complex expressions. As such, it may be necessary to differentiate whether a value represents a **field** or a **constant** . Consider the following example:

##### Node.js

``` text
  // Here the two parameters "name" and "toronto" could represent fields or constants.

  db.pipeline()
    .collection("cities")
    .where(eq("name","toronto"))

  // In many cases, it's not necessary to differentiate between the two. In the
  // case of equality, we will implicit treat the first parameter as a field 
  // reference and the second as a constant. However if you need to override you 
  // can always be explicit with the value types
  
  db.pipeline()
    .collection("cities")
    .where(eq(Field.of("name"), Constant.of("toronto")))

  // In some cases, being explicit is always required. However, it should be
  // enough to look at the type signature of the expressions to know what
  //parameters can be used with implicit types, and what should be explicitly specified. 
    
```

### Web

``` javascript
const pipeline = db.pipeline()
  .collection("cities")
  .where(field("name").equal(constant("Toronto")));test.firestore.js
```

##### Swift

``` swift
let pipeline = db.pipeline()
  .collection("cities")
  .where(Field("name").equal(Constant("Toronto")))PipelineSnippets.swift
```

##### Kotlin  
Android

``` kotlin
val pipeline = db.pipeline()
    .collection("cities")
    .where(field("name").equal(constant("Toronto")))DocSnippets.kt
```

##### Java  
Android

``` text
Pipeline pipeline = db.pipeline()
    .collection("cities")
    .where(field("name").equal(constant("Toronto")));DocSnippets.java
```

##### Python

``` python
from google.cloud.firestore_v1.pipeline_expressions import Field, Constant

pipeline = (
    client.pipeline()
    .collection("cities")
    .where(Field.of("name").equal(Constant.of("Toronto")))
)firestore_pipelines.py
```

## Stages

### Input Stages

The input stage represents the first stage of a query. It defines the initial set of documents you are querying over. For Pipeline operations, this largely is similar to existing queries, where most queries start with either a `  collection(...)  ` or `  collection_group(...)  ` stage. Two new input stages are `  database()  ` and `  documents(...)  ` where `  database()  ` allows returning **all** documents in the database, while `  documents(...)  ` acts identical to a batch read.

##### Node.js

``` text
  // Return all restaurants in San Francisco
  const results = await db.pipeline()
    .collection("cities/sf/restaurants")
    .execute();

  // Return all restaurants
  const results = await db.pipeline()
    .collectionGroup("restaurants")
    .execute();

  // Return all documents across all collections in the database (huge result!)
  const results = await db.pipeline()
    .database()
    .execute();

  // Batch read of 3 documents
  const results = await db.pipeline()
    .documents(
      db.collection("cities").doc("SF"),
      db.collection("cities").doc("DC"),
      db.collection("cities").doc("NY"))
    .execute();
    
```

### Web

``` javascript
let results;

// Return all restaurants in San Francisco
results = await execute(db.pipeline().collection("cities/sf/restaurants"));

// Return all restaurants
results = await execute(db.pipeline().collectionGroup("restaurants"));

// Return all documents across all collections in the database (the entire database)
results = await execute(db.pipeline().database());

// Batch read of 3 documents
results = await execute(db.pipeline().documents([
  doc(db, "cities", "SF"),
  doc(db, "cities", "DC"),
  doc(db, "cities", "NY")
]));test.firestore.js
```

##### Swift

``` swift
var results: Pipeline.Snapshot

// Return all restaurants in San Francisco
results = try await db.pipeline().collection("cities/sf/restaurants").execute()

// Return all restaurants
results = try await db.pipeline().collectionGroup("restaurants").execute()

// Return all documents across all collections in the database (the entire database)
results = try await db.pipeline().database().execute()

// Batch read of 3 documents
results = try await db.pipeline().documents([
  db.collection("cities").document("SF"),
  db.collection("cities").document("DC"),
  db.collection("cities").document("NY")
]).execute()PipelineSnippets.swift
```

##### Kotlin  
Android

``` kotlin
var results: Task<Pipeline.Snapshot>

// Return all restaurants in San Francisco
results = db.pipeline().collection("cities/sf/restaurants").execute()

// Return all restaurants
results = db.pipeline().collectionGroup("restaurants").execute()

// Return all documents across all collections in the database (the entire database)
results = db.pipeline().database().execute()

// Batch read of 3 documents
results = db.pipeline().documents(
    db.collection("cities").document("SF"),
    db.collection("cities").document("DC"),
    db.collection("cities").document("NY")
).execute()DocSnippets.kt
```

##### Java  
Android

``` text
Task<Pipeline.Snapshot> results;

// Return all restaurants in San Francisco
results = db.pipeline().collection("cities/sf/restaurants").execute();

// Return all restaurants
results = db.pipeline().collectionGroup("restaurants").execute();

// Return all documents across all collections in the database (the entire database)
results = db.pipeline().database().execute();

// Batch read of 3 documents
results = db.pipeline().documents(
    db.collection("cities").document("SF"),
    db.collection("cities").document("DC"),
    db.collection("cities").document("NY")
).execute();DocSnippets.java
```

##### Python

``` python
# Return all restaurants in San Francisco
results = client.pipeline().collection("cities/sf/restaurants").execute()

# Return all restaurants
results = client.pipeline().collection_group("restaurants").execute()

# Return all documents across all collections in the database (the entire database)
results = client.pipeline().database().execute()

# Batch read of 3 documents
results = (
    client.pipeline()
    .documents(
        client.collection("cities").document("SF"),
        client.collection("cities").document("DC"),
        client.collection("cities").document("NY"),
    )
    .execute()
)firestore_pipelines.py
```

As with all other stages, the order of results from these input stages is not stable. A `  sort(...)  ` operator should always be added if a specific ordering is desired.

### Where

The `  where(...)  ` stage acts as a traditional filter operation over documents generated from the previous stage and mostly mirrors the existing "where" syntax for existing queries. Any document for where a given expression evaluates to a non- `  true  ` value is filtered out from the returned documents.

Multiple `  where(...)  ` statements can be chained together, and act as an `  and(...)  ` expression. For example the following two queries are logically equivalent and can be used interchangeably.

##### Node.js

``` text
  const results = await db.pipeline()
    .collection("books")
    .where(eq("rating", 5.0))
    .where(lt('published', 1900))
    .execute();
  
  const results = await db.pipeline()
    .collection("books")
    .where(and(
      eq("rating", 5.0), 
      lt('published', 1900)))
    .execute();
    
```

### Web

``` javascript
let results;

results = await execute(db.pipeline().collection("books")
  .where(field("rating").equal(5))
  .where(field("published").lessThan(1900))
);

results = await execute(db.pipeline().collection("books")
  .where(and(field("rating").equal(5), field("published").lessThan(1900)))
);test.firestore.js
```

##### Swift

``` swift
var results: Pipeline.Snapshot

results = try await db.pipeline().collection("books")
  .where(Field("rating").equal(5))
  .where(Field("published").lessThan(1900))
  .execute()

results = try await db.pipeline().collection("books")
  .where(Field("rating").equal(5) && Field("published").lessThan(1900))
  .execute()PipelineSnippets.swift
```

##### Kotlin  
Android

``` kotlin
var results: Task<Pipeline.Snapshot>

results = db.pipeline().collection("books")
    .where(field("rating").equal(5))
    .where(field("published").lessThan(1900))
    .execute()

results = db.pipeline().collection("books")
    .where(Expression.and(field("rating").equal(5),
      field("published").lessThan(1900)))
    .execute()DocSnippets.kt
```

##### Java  
Android

``` text
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
```

##### Python

``` python
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
```

### Select / Add & Remove Fields

The `  select(...)  ` , `  add_fields(...)  ` , & `  remove_fields(...)  ` all allow you to modify the fields being returned from a previous stage. These three are generally referred to as projection-style stages.

The `  select(...)  ` and `  add_fields(...)  ` allow you to specify the result of an expression to a user-provided field name. An expression that results in an error will result in a `  null  ` value. The `  select(...)  ` will only return the documents with specified field names while `  add_fields(...)  ` extends the schema of the previous stage (potentially overwriting values with identical field names).

The `  remove_fields(...)  ` allows specifying a set of fields to remove from the previous stage. Specifying field names that do not exist is a no-op.

See the [Restrict the Fields to Return](#restrict_the_fields_to_return) section below but in general using such a stage to restrict the result to only the fields needed in the client is helpful in reducing the cost and latency for most queries.

### Aggregate / Distinct

The `  aggregate(...)  ` stage lets you perform a series of aggregations over the input documents. By default, all documents are aggregated together, but an optional `  grouping  ` argument can be provided, allowing the input documents aggregated into different buckets.

##### Node.js

``` text
  const results = await db.pipeline()
    .collection("books")
    .aggregate({
        accumulators: [avg('rating').as('avg_rating')],
        groups: ['genre'],
      })
    .execute();
    
```

### Web

``` javascript
const results = await execute(db.pipeline()
  .collection("books")
  .aggregate(
    field("rating").average().as("avg_rating")
  )
  .distinct(field("genre"))
);test.firestore.js
```

##### Swift

``` swift
let results = try await db.pipeline()
  .collection("books")
  .aggregate([
    Field("rating").average().as("avg_rating")
  ], groups: [
    Field("genre")
  ])
  .execute()PipelineSnippets.swift
```

##### Kotlin  
Android

``` kotlin
val results = db.pipeline()
    .collection("books")
    .aggregate(
        AggregateStage
            .withAccumulators(AggregateFunction.average("rating").alias("avg_rating"))
            .withGroups(field("genre"))
    )
    .execute()DocSnippets.kt
```

##### Java  
Android

``` text
Task<Pipeline.Snapshot> results = db.pipeline()
    .collection("books")
    .aggregate(AggregateStage
        .withAccumulators(
            AggregateFunction.average("rating").alias("avg_rating"))
        .withGroups(field("genre")))
    .execute();DocSnippets.java
```

##### Python

``` python
from google.cloud.firestore_v1.pipeline_expressions import Field

results = (
    client.pipeline()
    .collection("books")
    .aggregate(
        Field.of("rating").average().as_("avg_rating"), groups=[Field.of("genre")]
    )
    .execute()
)firestore_pipelines.py
```

When `  groupings  ` is not specified, this stage will produce only a single document, otherwise a document will be generated for each unique combination of `  groupings  ` values.

The `  distinct(...)  ` stage is a simplified aggregation operator which allows generating just the unique `  groupings  ` without any accumulators. It behaves identically to that of `  aggregate(...)  ` in all other regards. An example is given below:

##### Node.js

``` text
  const results = await db.pipeline()
    .collection("books")
    .distinct(toUppercase(Field.of("author")).as("author"), Field.of("genre"))
    .execute();
    
```

### Web

``` javascript
const results = await execute(db.pipeline()
  .collection("books")
  .distinct(
    field("author").toUpper().as("author"),
    field("genre")
  )
);test.firestore.js
```

##### Swift

``` swift
let results = try await db.pipeline()
  .collection("books")
  .distinct([
    Field("author").toUpper().as("author"),
    Field("genre")
  ])
  .execute()PipelineSnippets.swift
```

##### Kotlin  
Android

``` kotlin
val results = db.pipeline()
    .collection("books")
    .distinct(
        field("author").toUpper().alias("author"),
        field("genre")
    )
    .execute()DocSnippets.kt
```

##### Java  
Android

``` text
Task<Pipeline.Snapshot> results = db.pipeline()
    .collection("books")
    .distinct(
        field("author").toUpper().alias("author"),
        field("genre")
    )
    .execute();DocSnippets.java
```

##### Python

``` python
from google.cloud.firestore_v1.pipeline_expressions import Field

results = (
    client.pipeline()
    .collection("books")
    .distinct(Field.of("author").to_upper().as_("author"), "genre")
    .execute()
)firestore_pipelines.py
```

## Functions

Functions are a building block for creating expressions and complex queries. For a complete list of functions with examples, refer to the [Functions reference](/firestore/docs/pipeline/functions/all_functions) . As a quick reminder, consider the structure of a typical query:

Many stages accept expressions which contain one or more functions. The most common function usage will be found in the `  where(...)  ` and `  select(...)  ` stages. There are two main types of functions that you should be familiar with:

##### Node.js

``` text
  // Type 1: Scalar (for use in non-aggregation stages)
  // Example: Return the min store price for each book.

  const results = await db.pipeline()
    .collection("books")
    .select(logicalMin(Field.of("current"),Field.of("updated")).as("price_min"))
    .execute();

  // Type 2: Aggregation (for use in aggregate stages)
  // Example: Return the min price of all books.

  const results = await db.pipeline()
    .collection("books")
    .aggregate(min(Field.of("price"))
    .execute();
    
```

### Web

``` javascript
let results;

// Type 1: Scalar (for use in non-aggregation stages)
// Example: Return the min store price for each book.
results = await execute(db.pipeline().collection("books")
  .select(field("current").logicalMinimum(field("updated")).as("price_min"))
);

// Type 2: Aggregation (for use in aggregate stages)
// Example: Return the min price of all books.
results = await execute(db.pipeline().collection("books")
  .aggregate(field("price").minimum().as("min_price"))
);test.firestore.js
```

##### Swift

``` swift
var results: Pipeline.Snapshot

// Type 1: Scalar (for use in non-aggregation stages)
// Example: Return the min store price for each book.
results = try await db.pipeline().collection("books")
  .select([
    Field("current").logicalMinimum(["updated"]).as("price_min")
  ])
  .execute()

// Type 2: Aggregation (for use in aggregate stages)
// Example: Return the min price of all books.
results = try await db.pipeline().collection("books")
  .aggregate([Field("price").minimum().as("min_price")])
  .execute()PipelineSnippets.swift
```

##### Kotlin  
Android

``` kotlin
var results: Task<Pipeline.Snapshot>

// Type 1: Scalar (for use in non-aggregation stages)
// Example: Return the min store price for each book.
results = db.pipeline().collection("books")
    .select(
        field("current").logicalMinimum("updated").alias("price_min")
    )
    .execute()

// Type 2: Aggregation (for use in aggregate stages)
// Example: Return the min price of all books.
results = db.pipeline().collection("books")
    .aggregate(AggregateFunction.minimum("price").alias("min_price"))
    .execute()DocSnippets.kt
```

##### Java  
Android

``` text
Task<Pipeline.Snapshot> results;

// Type 1: Scalar (for use in non-aggregation stages)
// Example: Return the min store price for each book.
results = db.pipeline().collection("books")
    .select(
        field("current").logicalMinimum("updated").alias("price_min")
    )
    .execute();

// Type 2: Aggregation (for use in aggregate stages)
// Example: Return the min price of all books.
results = db.pipeline().collection("books")
    .aggregate(AggregateFunction.minimum("price").alias("min_price"))
    .execute();DocSnippets.java
```

##### Python

``` python
from google.cloud.firestore_v1.pipeline_expressions import Field

# Type 1: Scalar (for use in non-aggregation stages)
# Example: Return the min store price for each book.
results = (
    client.pipeline()
    .collection("books")
    .select(
        Field.of("current").logical_minimum(Field.of("updated")).as_("price_min")
    )
    .execute()
)

# Type 2: Aggregation (for use in aggregate stages)
# Example: Return the min price of all books.
results = (
    client.pipeline()
    .collection("books")
    .aggregate(Field.of("price").minimum().as_("min_price"))
    .execute()
)firestore_pipelines.py
```

## Limits

For the most part Enterprise Edition doesn't impose limits on the shape of the query. In other words, you're not limited to a small number of values in an `  IN  ` or `  OR  ` query. Instead, there are two primary limits you should be aware of:

  - **Deadline:** 60 seconds (identical to Standard Edition).
  - **Memory Usage:** 128 MiB limit on the amount of materialized data during query execution.

## Errors

You may encounter failed queries for a number of reasons. Here is a link to [common errors](/firestore/docs/understand-error-codes) and the associated action you can take:

<table>
<tbody>
<tr class="odd">
<td><strong>Error Code</strong></td>
<td><strong>Action</strong></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       DEADLINE_EXCEEDED      </code></td>
<td>The query you are executing exceeds a 60 second deadline and requires additional optimization. See the performance section for tips. If you are unable to root cause the problem, reach out to the team.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       RESOURCE_EXHAUSTED      </code></td>
<td>The query you are executing exceeds the memory limits and requires additional optimization. See the performance section for tips. If you are unable to root cause the problem, reach out to the team.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       INTERNAL      </code></td>
<td><a href="https://docs.cloud.google.com/support/docs/customer-care-procedures#create_a_support_case">Contact</a> the team for support.</td>
</tr>
</tbody>
</table>

## Performance

Unlike existing queries, Pipeline operations do not require that an index is always present. This means that a query can exhibit higher latency compared to existing queries which would have just failed immediately with a `  FAILED_PRECONDITION  ` missing index error. To improve the performance of Pipeline operations, there are a couple of steps you can take.

### Create Indexes

#### Index Used

Query explain lets you identify if your query is being served by an index or falling back to a less efficient operation like a table scan. If your query is not being fully served from an index, you can create an index by following the instructions.

#### Creating Indexes

You can follow the existing [index management documentation](/firestore/docs/query-data/indexing) to create indexes. Before creating an index, familiarize yourself with [general best practices](/firestore/docs/concepts/index-overview) with indexes in Firestore. To ensure your query can leverage indexes, follow the [best practices](/firestore/docs/concepts/index-overview#index_properties) to create indexes with fields in the following order:

1.  All fields that will be used in equality filters (in any order)
2.  All fields that will be sorted on (in the same order)
3.  Fields that will be used in range or inequality filters in decreasing order of query constraint selectivity

For example, for the following query,

##### Node.js

``` text
const results = await db.pipeline()
  .collection('books')
  .where(lt('published', 1900))
  .where(eq('genre', 'Science Fiction'))
  .where(gt('avg_rating', 4.3))
  .sort(Field.of('published').descending())
  .execute();
    
```

### Web

``` javascript
const results = await execute(db.pipeline()
  .collection("books")
  .where(field("published").lessThan(1900))
  .where(field("genre").equal("Science Fiction"))
  .where(field("rating").greaterThan(4.3))
  .sort(field("published").descending())
);test.firestore.js
```

##### Swift

``` swift
let results = try await db.pipeline()
  .collection("books")
  .where(Field("published").lessThan(1900))
  .where(Field("genre").equal("Science Fiction"))
  .where(Field("rating").greaterThan(4.3))
  .sort([Field("published").descending()])
  .execute()PipelineSnippets.swift
```

##### Kotlin  
Android

``` kotlin
val results = db.pipeline()
    .collection("books")
    .where(field("published").lessThan(1900))
    .where(field("genre").equal("Science Fiction"))
    .where(field("rating").greaterThan(4.3))
    .sort(field("published").descending())
    .execute()DocSnippets.kt
```

##### Java  
Android

``` text
Task<Pipeline.Snapshot> results = db.pipeline()
    .collection("books")
    .where(field("published").lessThan(1900))
    .where(field("genre").equal("Science Fiction"))
    .where(field("rating").greaterThan(4.3))
    .sort(field("published").descending())
    .execute();DocSnippets.java
```

##### Python

``` python
from google.cloud.firestore_v1.pipeline_expressions import Field

results = (
    client.pipeline()
    .collection("books")
    .where(Field.of("published").less_than(1900))
    .where(Field.of("genre").equal("Science Fiction"))
    .where(Field.of("rating").greater_than(4.3))
    .sort(Field.of("published").descending())
    .execute()
)firestore_pipelines.py
```

The recommended index is a collection scope index on `  books  ` for `  (genre [...], published DESC, avg_rating DESC).  `

#### Index density

Firestore supports sparse and non-sparse indexes. For more information, see [Index density](/docs/firestore/pipelines/index-overview#index_density) .

#### Covered Queries + Secondary Indexes

Firestore can skip fetching the full document and just return results from the index if all fields being returned are present in a secondary index. This normally leads to a significant latency (and cost) improvement. Using the sample query below:

##### Node.js

``` text
const results = await db.pipeline()
  .collection("books")
  .where(like(Field.of("category"), "%fantasy%"))
  .where(exists("title"))
  .where(exists("author"))
  .select("title", "author")
  .execute();
    
```

### Web

``` javascript
const results = await execute(db.pipeline()
  .collection("books")
  .where(field("category").like("%fantasy%"))
  .where(field("title").exists())
  .where(field("author").exists())
  .select(field("title"), field("author"))
);test.firestore.js
```

##### Swift

``` swift
let results = try await db.pipeline()
  .collection("books")
  .where(Field("category").like("%fantasy%"))
  .where(Field("title").exists())
  .where(Field("author").exists())
  .select([Field("title"), Field("author")])
  .execute()PipelineSnippets.swift
```

##### Kotlin  
Android

``` kotlin
val results = db.pipeline()
    .collection("books")
    .where(field("category").like("%fantasy%"))
    .where(field("title").exists())
    .where(field("author").exists())
    .select(field("title"), field("author"))
    .execute()DocSnippets.kt
```

##### Java  
Android

``` text
Task<Pipeline.Snapshot> results = db.pipeline()
    .collection("books")
    .where(field("category").like("%fantasy%"))
    .where(field("title").exists())
    .where(field("author").exists())
    .select(field("title"), field("author"))
    .execute();DocSnippets.java
```

##### Python

``` python
from google.cloud.firestore_v1.pipeline_expressions import Field

results = (
    client.pipeline()
    .collection("books")
    .where(Field.of("category").like("%fantasy%"))
    .where(Field.of("title").exists())
    .where(Field.of("author").exists())
    .select("title", "author")
    .execute()
)firestore_pipelines.py
```

If the database already has a collection scope index on `  books  ` for `  (category [...], title [...], author [...])  ` then it can avoid fetching anything from the main documents themselves. In this case the order in the index does not matter, `  [...]  ` is used to signify that.

### Restrict the Fields to Return

By default, a Firestore query returns all fields in a document, analogous to a `  SELECT *  ` in traditional systems. If however your application only needs a subset of the fields, the `  select(...)  ` or `  restrict(...)  ` stages can be used to push this filtering server-side. This will decrease both the response size (decreasing the network egress cost) as well as improving latency.

## Troubleshooting Tools

### Query Explain

Query Explain lets you bring visibility in execution metrics and details about indexes used.

### Metrics

Pipeline operations if fully integrated with existing [Firestore metrics](/monitoring/api/metrics_gcp_d_h#gcp-firestore) .

## Known Issues / Limitations

### Specialized Indexes

Pipeline operations do not yet support existing `  array-contains  ` & `  vector  ` [index types](/firestore/docs/concepts/index-overview#index_modes) . Instead of just rejecting such queries, Firestore will attempt to use other existing `  ascending  ` & `  descending  ` indexes. It is expected that during private preview Pipeline operations with such `  array_contains  ` or `  find_nearest  ` expressions will be slower than their existing equivalents due to this.

### Pagination

Support for easily [paginating](/firestore/docs/query-data/query-cursors) over a result set is not supported during the private preview. This can be worked around by chaining up equivalent `  where(...)  ` & `  sort(...)  ` stages as shown below.

##### Node.js

``` text
  // Existing pagination via 'startAt(...)'.
  db.collection("cities")
    .orderBy("population")
    .startAt(1000000);

  // Near-term work around via Pipeline operations.
  db.pipeline()
    .collection("cities")
    .where(gte("population", 1000000)
    .sort(Field.of("population").descending());
    
```

### Web

``` javascript
// Existing pagination via `startAt()`
const q =
  query(collection(db, "cities"), orderBy("population"), startAt(1000000));

// Private preview workaround using pipelines
const pageSize = 2;
const pipeline = db.pipeline()
  .collection("cities")
  .select("name", "population", "__name__")
  .sort(field("population").descending(), field("__name__").ascending());

// Page 1 results
let snapshot = await execute(pipeline.limit(pageSize));

// End of page marker
const lastDoc = snapshot.results[snapshot.results.length - 1];

// Page 2 results
snapshot = await execute(
  pipeline
    .where(
      or(
        and(
          field("population").equal(lastDoc.get("population")),
          field("__name__").greaterThan(lastDoc.ref)
        ),
        field("population").lessThan(lastDoc.get("population"))
      )
    )
    .limit(pageSize)
);test.firestore.js
```

##### Swift

``` swift
// Existing pagination via `start(at:)`
let query = db.collection("cities").order(by: "population").start(at: [1000000])

// Private preview workaround using pipelines
let pipeline = db.pipeline()
  .collection("cities")
  .where(Field("population").greaterThanOrEqual(1000000))
  .sort([Field("population").descending()])PipelineSnippets.swift
```

##### Kotlin  
Android

``` kotlin
// Existing pagination via `startAt()`
val query = db.collection("cities").orderBy("population").startAt(1000000)

// Private preview workaround using pipelines
val pipeline = db.pipeline()
    .collection("cities")
    .where(field("population").greaterThanOrEqual(1000000))
    .sort(field("population").descending())DocSnippets.kt
```

##### Java  
Android

``` text
// Existing pagination via `startAt()`
Query query = db.collection("cities").orderBy("population").startAt(1000000);

// Private preview workaround using pipelines
Pipeline pipeline = db.pipeline()
    .collection("cities")
    .where(field("population").greaterThanOrEqual(1000000))
    .sort(field("population").descending());DocSnippets.java
```

##### Python

``` python
from google.cloud.firestore_v1.pipeline_expressions import Field

# Existing pagination via `start_at()`
query = (
    client.collection("cities")
    .order_by("population")
    .start_at({"population": 1_000_000})
)

# Private preview workaround using pipelines
pipeline = (
    client.pipeline()
    .collection("cities")
    .where(Field.of("population").greater_than_or_equal(1_000_000))
    .sort(Field.of("population").descending())
)firestore_pipelines.py
```

### Emulator Support

The emulator does not yet support Pipeline operations.

### Realtime and Offline Support

Pipeline operations don't have realtime and offline capabilities yet.

## What's next

  - See the [Functions reference](/firestore/docs/pipeline/functions/all_functions) .
