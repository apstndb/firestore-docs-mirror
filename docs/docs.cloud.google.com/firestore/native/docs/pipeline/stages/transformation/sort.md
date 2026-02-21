# Sort (Transformation Stage)

**Preview — Firestore in Native mode (with Pipeline Operations) for Enterprise Edition**

This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](/terms/service-terms#1) . You can process personal data for this feature as outlined in the [Cloud Data Processing Addendum](/terms/data-processing-addendum) , subject to the obligations and restrictions described in the agreement under which you access Google Cloud. Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

## Description

Sorts the input documents based on one or more specified sort orderings.

## Syntax

The following example sorts the cities collection by population in ascending order:

### Node.js

``` text
const results = await db.pipeline()
  .collection("/cities")
  .sort(Field.of("population").ascending())
  .execute();
```

The following example sorts the cities collection by the length of the city name, in ascending order.

### Node.js

``` text
const results = await db.pipeline()
  .collection("/cities")
  .sort(Field.of("name").charLength().ascending())
  .execute();
```

## Client examples

### Web

``` javascript
const results = await execute(db.pipeline()
  .collection("books")
  .sort(
    field("release_date").descending(), field("author").ascending()
  )
);test.firestore.js
```

##### Swift

``` swift
let results = try await db.pipeline()
  .collection("books")
  .sort([
    Field("release_date").descending(), Field("author").ascending()
  ])
  .execute()PipelineSnippets.swift
```

##### Kotlin  
Android

``` kotlin
val results = db.pipeline()
    .collection("books")
    .sort(
        field("release_date").descending(),
        field("author").ascending()
    )
    .execute()DocSnippets.kt
```

##### Java  
Android

``` text
Task<Pipeline.Snapshot> results = db.pipeline()
    .collection("books")
    .sort(
        field("release_date").descending(),
        field("author").ascending()
    )
    .execute();DocSnippets.java
```

##### Python

``` python
from google.cloud.firestore_v1.pipeline_expressions import Field

results = (
    client.pipeline()
    .collection("books")
    .sort(Field.of("release_date").descending(), Field.of("author").ascending())
    .execute()
)firestore_pipelines.py
```

##### Java

``` java
Pipeline.Snapshot results =
    firestore
        .pipeline()
        .collection("books")
        .sort(descending(field("release_date")), ascending(field("author")))
        .execute()
        .get();PipelineSnippets.java
```

## Behavior

### Sort order

Sort order follows [Firestore's value type order](https://docs.cloud.google.com/firestore/native/docs/concepts/data-types#value_type_ordering)

### Deterministic Order of Results

If there is no `  sort  ` stage in the query, the ordering of the returned results is non-deterministic and may vary between executions. If a `  sort  ` stage is present but the ordering expressions fail to produce a unique ordering among the returned results, the ordering of the returned results may still vary between executions.

For example, sorting cities by the country of the cities, in ascending order against the following dataset

``` text
{name: 'Los Angeles', state: 'CA', country: 'USA', population: 3970000},
{name: 'New York', state: 'NY', country: 'USA', population: 8530000}
{name: 'San Francisco', state: 'CA', country: 'USA', population: 870000},
```

can produce any permutation of the 3 documents in the dataset because they all have the same country attribute. To produce a deterministic ordering of the results, you can append a sort order on **name** to the order:

### Node.js

``` text
const results = await db.pipeline()
  .collection("/cities")
  .sort(Field.of("country").ascending(), Field.of("__name__").ascending())
  .execute();
```

This will use the unique document name as the tiebreaker when multiple documents have the same country value. Note that any other fields which together with the country field form a unique key of the document within the collection can be used to produce a deterministic order of results.

### Sorting Equivalent Values

Equivalent values are sorted together but the order of results within the equivalent class are not deterministic according to the [Deterministic Order of Results discussion](#deterministic-order-of-results) . For example, sorting cities by size , in ascending order against the following dataset

``` text
{name: 'Los Angeles', state: 'CA', country: 'USA', size: 3970000},
{name: 'Mexico City', state: null, country: 'Mexico', size: 3970000.0},
```

can produce any permutation of the 2 documents in the dataset because both documents have the equivalent size value `  3970000  ` .

### Multiple Sort Stages

When the query contains multiple consecutive sort stages, only the last sort stage has an impact on the query results. Note that this is different from the behavior of the `  orderBy  ` clause in the Core API.

### Top-N Sort Optimization

When a `  limit  ` is used after a `  sort  ` , a top-n sort may be used. This optimization bounds the memory use of the sort stage by allowing it to only store `  N  ` documents at a time—as defined by `  limit  ` —making the sort more memory-efficient.

### Null and Absent values

If a field specified in an ordering does not exist in a document, its value is sorted as if the value is `  null  ` . For example, sorting cities by the state of the cities, in ascending order against the following dataset

``` text
{name: 'Los Angeles', state: 'CA', country: 'USA', population: 3970000},
{name: 'Mexico City', state: null, country: 'Mexico', population: 9200000},
{name: 'New York', state: 'NY', country: 'USA', population: 8530000}
{name: 'San Francisco', state: 'CA', country: 'USA', population: 870000},
{name: 'Toronto', country: 'Canada', population: 2930000},
```

produces the following results where the "Toronto" document and the "Mexico City" document are sorted as `  null  ` and before other documents.

``` text
{name: 'Toronto', country: 'Canada', population: 2930000},
{name: 'Mexico City', state: null, country: 'Mexico', population: 9200000},
{name: 'Los Angeles', state: 'CA', country: 'USA', population: 3970000},
{name: 'San Francisco', state: 'CA', country: 'USA', population: 870000},
{name: 'New York', state: 'NY', country: 'USA', population: 8530000}
```
