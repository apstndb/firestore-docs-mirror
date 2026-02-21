# Distinct (Transformation Stage)

**Preview — Firestore in Native mode (with Pipeline Operations) for Enterprise Edition**

This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](/terms/service-terms#1) . You can process personal data for this feature as outlined in the [Cloud Data Processing Addendum](/terms/data-processing-addendum) , subject to the obligations and restrictions described in the agreement under which you access Google Cloud. Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

## Description

Find out the distinct values of a field or an expression from the previous stages.

## Syntax

`  distinct  ` stage has similar syntax as `  select  ` . It takes one or more selectable expressions to select and find distinct values on. Strings can be used when the expression is just a field reference:

### Node.js

``` text
const cities = await db.pipeline()
  .collection('/cities')
  .distinct("country")
  .execute();

const cities = await db.pipeline()
  .collection('/cities')
  .distinct(
    field("state").toLower().as("normalized_state"),
    field("country"))
  .execute();
```

## Client examples

##### Node.js

``` javascript
let cities = await db.pipeline()
  .collection("cities")
  .distinct("country")
  .execute();

cities = await db.pipeline()
  .collection("cities")
  .distinct(
    field("state").toLower().as("normalizedState"),
    field("country"))
  .execute();test.firestore.js
```

### Web

``` javascript
let cities = await execute(db.pipeline()
  .collection("cities")
  .distinct("country"));

cities = await execute(db.pipeline()
  .collection("cities")
  .distinct(
    field("state").toLower().as("normalizedState"),
    field("country")));test.firestore.js
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
var cities = db.pipeline()
    .collection("cities")
    .distinct("country")
    .execute()

cities = db.pipeline()
    .collection("cities")
    .distinct(
        field("state").toLower().alias("normalizedState"),
        field("country")
    )
    .execute()DocSnippets.kt
```

##### Java  
Android

``` text
Task<Pipeline.Snapshot> cities;
cities = db.pipeline()
        .collection("cities")
        .distinct("country")
        .execute();

cities = db.pipeline()
        .collection("cities")
        .distinct(
                field("state").toLower().alias("normalizedState"),
                field("country"))
        .execute();DocSnippets.java
```

##### Python

``` python
from google.cloud.firestore_v1.pipeline_expressions import Field

cities = client.pipeline().collection("cities").distinct("country").execute()

cities = (
    client.pipeline()
    .collection("cities")
    .distinct(Field.of("state").to_lower().as_("normalizedState"), "country")
    .execute()
)firestore_pipelines.py
```

##### Java

``` java
Pipeline.Snapshot cities1 =
    firestore.pipeline().collection("cities").distinct("country").execute().get();

Pipeline.Snapshot cities2 =
    firestore
        .pipeline()
        .collection("cities")
        .distinct(toLower(field("state")).as("normalizedState"), field("country"))
        .execute()
        .get();PipelineSnippets.java
```

## Behavior

In terms of projection behaviors, `  distinct  ` is similar to `  select  ` with deduplication, therefore any selectable expression available to `  select  ` can also be used for `  distinct  ` .

The `  distinct  ` stage works similarly to an aggregate stage without groups.

See also [Aggregate Stage](/firestore/native/docs/pipeline/stages/transformation/aggregate) and [Select Stage](/firestore/native/docs/pipeline/stages/transformation/select) .

### Find Distinct Field Values

For example, to get a list of every country in the following `  cities  ` collection:

### Node.js

``` text
await db.collection('cities').doc('SF').set({name: 'San Francisco', state: 'CA', country: 'USA'});
await db.collection('cities').doc('LA').set({name: 'Los Angeles', state: 'CA', country: 'USA'});
await db.collection('cities').doc('NY').set({name: 'New York', state: 'NY', country: 'USA'});
await db.collection('cities').doc('TOR').set({name: 'Toronto', state: null, country: 'Canada'});
await db.collection('cities').doc('MEX').set({name: 'Mexico City', state: null, country: 'Mexico'});
```

Distinct countries can be found using:

### Node.js

``` text
const cities = await db.pipeline()
  .collection('/cities')
  .distinct("country")
  .execute();
```

which generates the following result:

``` text
{country: "USA"}
{country: "Canada"}
{country: "Mexico"}
```

### Distinct Output of Expressions

You can also find the distinct combinations of multiple fields, or more complicated expressions. For example:

### Node.js

``` text
const cities = await db.pipeline()
  .collection('/cities')
  .distinct(
    field("state").toLower().as("normalized_state"),
    field("country"))
  .execute();
```

to get:

``` text
{country: "USA", normalized_state: "ca"}
{country: "USA", normalized_state: "ny"}
{country: "Canada", normalized_state: null}
{country: "Mexico", normalized_state: null}
```

### Equivalence Behaviors

The equivalence behavior on distinct values follows the same semantics as equalities.

This means that equivalent values, for example mathmatically equivalent numeric values, regardless of original types (32-bit integer, 64-bit integer, floating point numbers, decimal numbers, etc), are considered the same distinct value.

As an example, in a collection `  numerics  ` with different documents containing `  foo  ` values of 32-bit integer `  1  ` , 64-bit integer `  1L  ` and floating point `  1.0  ` respectively, `  distinct  ` will only return 1 result.

In such cases of having different equivalent values present in the dataset, the output value of the group can be **any** of these equivalent values. In this example, this value of `  foo  ` could be returned as `  1  ` , `  1L  ` , or `  1.0  ` .

Even if it appears to be deterministic, you should **not** attempt to rely on the behavior of one specific value getting selected.

### Memory Usage

How the `  distinct  ` stage is executed depends on the available indexes. When there is not an appropriate index chosen by the query optimizer, `  distinct  ` requires buffering all distinct values in the memory.

In the event of having a very large number of distinct values, or values being very large (e.g. distinct on huge values), this stage may run out of memory.

In such cases, you should apply filters to limit the dataset to perform `  distinct  ` on, or create indexes as recommended to avoid large memory usages.

Query Explain will provide information on the actual query execution plan and profiling data to help with the debugging.
