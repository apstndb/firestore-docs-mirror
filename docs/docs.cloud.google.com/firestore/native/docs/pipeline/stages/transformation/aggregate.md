# Aggregate (Transformation Stage)

**Preview — Firestore in Native mode (with Pipeline Operations) for Enterprise Edition**

This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](/terms/service-terms#1) . You can process personal data for this feature as outlined in the [Cloud Data Processing Addendum](/terms/data-processing-addendum) , subject to the obligations and restrictions described in the agreement under which you access Google Cloud. Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

## Description

The `  aggregate  ` stage computes aggregated results (e.g. count, sum) from the documents returned by the previous stage.

Optionally, when a grouping expression is provided, it groups documents based on the provided expressions and then applies accumulator functions to each group.

## Syntax

For aggregations without group-by, the `  aggregate  ` stage takes one or more aliased aggregator expressions:

### Node.js

``` text
const cities = await db.pipeline()
  .collection("/cities")
  .aggregate(
      countAll().as("total"),
      average("population").as("avg_population")
  )
  .execute();
```

For aggregations with grouping, it takes additional groups besides the aggregators:

### Node.js

``` text
const result = await db.pipeline()
  .collectionGroup('citites')
  .aggregate({
    accumulators: [
      countAll().as('cities'),
      field('population').sum().as('total_popoluation')
    ],
    groups: [field('location.state').as('state')]
  })
  .execute();
```

## Behavior

### Aggregations Without Grouping

Create a cities collection with the following documents:

### Node.js

``` text
await db.collection('cities').doc('SF').set({name: 'San Francisco', state: 'CA', country: 'USA', population: 870000});
await db.collection('cities').doc('LA').set({name: 'Los Angeles', state: 'CA', country: 'USA', population: 3970000});
await db.collection('cities').doc('NY').set({name: 'New York', state: 'NY', country: 'USA', population: 8530000});
await db.collection('cities').doc('TOR').set({name: 'Toronto', state: null, country: 'Canada', population: 2930000});
await db.collection('cities').doc('MEX').set({name: 'Mexico City', state: null, country: 'Mexico', population: 9200000});
```

To find out the total number of cities and the average population of them:

### Node.js

``` text
const cities = await db.pipeline()
  .collection("/cities")
  .aggregate(
      countAll().as("total"),
      average("population").as("avg_population")
  )
  .execute();
```

which produces:

``` text
{avg_population: 5100000, total: 5}
```

### Perform Aggregations on Groups

By supplying a `  groups  ` argument, you can perform aggregations on each distinct group.

For example, to find the city with the largest population in each country and each state:

### Node.js

``` text
const cities = await db.pipeline()
  .collection("/cities")
  .aggregate({
      accumulators: [
          countAll().as("number_of_cities"),
          maximum("population").as("max_population")
      ],
      groups: ["country", "state"]
  })
  .execute();
```

which gives:

``` text
{country: "USA", state: "CA", max_population: 3970000, number_of_cities: 2},
{country: "USA", state: "NY", max_population: 8530000, number_of_cities: 1},
{country: "Canada", state: null, max_population: 2930000, number_of_cities: 1},
{country: "Mexico", state: null,  max_population: 9200000, number_of_cities: 1}
```

### Complex Expressions on Grouping

Beyond grouping by only field values, the `  aggregate  ` stage supports grouping by results of complex expressions. Any expression that is valid in a `  select  ` stage can be used as a grouping key. This allows for flexible grouping based on calculated values or conditions.

For example, to group by whether the state field is null, and find out the total population in each group:

### Node.js

``` text
const cities = await db.pipeline()
  .collection("/cities")
  .aggregate({
      accumulators: [
         sum("population").as("total_population")
      ],
      groups: [equal(field("state"), null).as("state_is_null")]
  })
  .execute();
```

will return:

``` text
{state_is_null: true, total_population: 12130000}
{state_is_null: false, total_population: 13370000}
```

### Aggregator Behaviors

The aggregation behavior of each supported function (e.g. `  count  ` , `  sum  ` , `  avg  ` ) can be found in the dedicated page for [Aggregate Functions](../../functions/aggregate_functions) .

### Group Key Behaviors

When grouping documents, Firestore uses equality semantics to determine if values belong to the same group.

This means that equivalent values, for example mathematically equivalent numeric values, regardless of original type (32-bit integer, 64-bit integer, floating point numbers, decimal128, etc), are all grouped together.

As an example, in a collection `  numerics  ` with different documents containing `  foo  ` values of 32-bit integer `  1  ` , 64-bit integer `  1L  ` and floating-point number `  1.0  ` respectively, they will all be accumulated into the same group. Running a count grouping by `  foo  ` will return:

``` text
{foo: 1.0, count: 3}
```

In such cases of having different equivalent values present in the dataset, the output value of the group can be **any** of these equivalent values. In this example, `  foo  ` could be `  1  ` , `  1L  ` , or `  1.0  ` .

Even if it appears to be deterministic, you should **not** attempt to rely on the behavior of one specific value being selected.

### Memory Usage

How the aggregation will be executed depends on the available indexes. When there is not an appropriate index chosen by the query optimizer, the aggregate needs to buffer all groups in the memory.

In the event of having a very large number of groups, or each group being very large (e.g. grouping by huge values), this stage may run out of memory.

In such cases, you should apply filters to limit the dataset to aggregate on, grouping on smaller/fewer fields, or create indexes as recommended to avoid large memory usages. Query Explain will provide information on the actual query execution plan and profiling data to help with debugging.
