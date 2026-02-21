Firestore in Datastore mode supports using range and inequality filters on multiple properties in a single query. This feature gives you range and inequality conditions on multiple properties and simplifies your application development by delegating implementation of post-filtering logic to Firestore in Datastore mode.

## Range and inequality filters on multiple properties

The following query uses range filters on priority and days to return all tasks with priority greater than four and with less than three days to complete.

### Go

``` text
query := datastore.NewQuery("Task").
   FilterField("priority", ">", 4).
   FilterField("days", "<", 3).
```

### GQL

``` text
SELECT * FROM /tasks WHERE priority > 4 AND days < 3;
```

### Java

``` text
Query<Entity> query =
    Query.newEntityQueryBuilder()
      .setKind("Task")
      .setFilter(
        CompositeFilter.and(
            PropertyFilter.gt("priority", 4), PropertyFilter.lt("days", 3)))
    .build();
```

### Node.js

``` text
const query = datastore
  .createQuery('Task')
  .filter(
    and([
      new PropertyFilter('priority', '>', 4),
      new PropertyFilter('days', '<', 3),
    ])
  );
```

### Python

``` text
from google.cloud import datastore
client = datastore.Client()
query = client.query(kind="Task")
query.add_filter(filter=PropertyFilter("priority", ">", 4))
query.add_filter(filter=PropertyFilter("days", "<", 3))
```

### PHP

``` text
$query = $datastore->query()
    ->kind('Task')
    ->filter('priority', '>', 4)
    ->filter('days', '<', 3)
```

### C\#

``` text
Query query = new Query("Task")
{
  Filter = Filter.And(Filter.GreaterThan("priority", 4),
    Filter.LessThan("days", 3))
};
```

### Ruby

``` text
query = datastore.query("Task")
                 .where("priority", ">", 4)
                 .where("days", "<", 3)
```

## Indexing considerations

Before you start running queries, make sure you have read about [queries](/datastore/docs/concepts/queries) .

If an `  ORDER BY  ` clause isn't specified, Firestore in Datastore mode uses any index that can satisfy the query's filter condition to serve the query. This approach produces a result set that is ordered according to the index definition.

To optimize the performance and cost of Firestore in Datastore mode queries, optimize the order of properties in the index. To do this, ensure that your index is ordered from left to right so that the query distills to a dataset that prevents scanning of extraneous index entries.

For example, suppose you want to search through a collection of employees to find United States employees whose salary is more than $100,000 and whose number of years of experience is greater than 0. Based on your understanding of the dataset, you know that the salary constraint is more selective than the experience constraint. An index that reduces the number of index scans is the `  (salary [...], experience [...])  ` index. As a result, a fast and cost-efficient query orders `  salary  ` before `  experience  ` , as shown in the following example:

### GQL

``` text
SELECT *
FROM /employees
WHERE salary > 100000 AND experience > 0
ORDER BY salary, experience
```

### Java

``` text
Query<Entity> query =
  Query.newEntityQueryBuilder()
    .setKind("employees")
    .setFilter(
        CompositeFilter.and(
            PropertyFilter.gt("salary", 100000), PropertyFilter.gt("experience", 0)))
    .setOrderBy(OrderBy("salary"), OrderBy("experience"))
    .build();
```

### Node.js

``` text
const query = datastore
  .createQuery("employees")
  .filter(
    and([
      new PropertyFilter("salary", ">", 100000),
      new PropertyFilter("experience", ">", 0),
       ])
    )
  .order("salary")
  .order("experience");
```

### Python

``` text
query = client.query(kind="employees")
query.add_filter("salary", ">", 100000)
query.add_filter("experience", ">", 0)
query.order = ["-salary", "-experience"]
```

## Best practices for optimizing indexes

When optimizing indexes, note the following best practices.

#### Order queries by equalities followed by most selective range or inequality field

Firestore in Datastore mode uses the leftmost properties of a composite index to satisfy the equality constraints and the range and inequality constraint, if any, on the first field of the `  orderBy()  ` query. These constraints can reduce the number of index entries that Firestore in Datastore mode scans. Firestore in Datastore mode uses the remaining properties of the index to satisfy other range and inequality constraints of the query. These constraints don't reduce the number of index entries that Firestore in Datastore mode scans, but they filter out unmatched entities so that the number of entities that are returned to the clients are reduced.

For more information about creating efficient indexes, see [index structure and definition](/datastore/docs/concepts/indexes) and [optimizing indexes](/datastore/docs/concepts/optimize-indexes) .

#### Order properties in decreasing order of query constraint selectivity

To ensure that Firestore in Datastore mode selects the optimal index for your query, specify an `  orderBy()  ` clause that orders range and inequality properties based on how selective their constraints are in your query, starting from the most selective. Higher selectivity matches fewer entities, while lower selectivity matches more entities. In your index ordering, put range and inequality properties with higher selectivity before properties with lower selectivity.

To minimize the number of entities that Firestore in Datastore mode scans and returns over the network, you should always order properties in the decreasing order of query constraint selectivity. If the result set is not in the required order and the result set is expected to be small, you can implement client-side logic to reorder it as per your ordering expectation.

For example, if you want to search through a collection of employees to find United States employees whose salary is more than $100,000 and order the results by the year of experience of the employee. If you expect that only a small number of employees will have salary higher than $100,000, then an efficient way to write the query is as follows:

### Java

``` text
Query<Entity> query =
  Query.newEntityQueryBuilder()
    .setKind("employees")
    .setFilter(PropertyFilter.gt("salary", 100000))
    .setOrderBy(OrderBy("salary"))
    .build();
QueryResults<Entity> results = datastore.run(query);
// Order results by `experience`
```

### Node.js

``` text
const query = datastore
  .createQuery("employees")
  .filter(new PropertyFilter("salary", ">", 100000))
  .order("salary");
const [entities] = await datastore.runQuery(query);
// Order results by `experience`
```

### Python

``` text
query = client.query(kind="employees")
query.add_filter("salary", ">", 100000)
query.order = ["salary"]
results = query.fetch()
// Order results by `experience`
```

While adding an ordering on `  experience  ` to the query will yield the same set of entities and obviate re-ordering the results on the clients, the query may read many more extraneous index entries than the earlier query. This is because Firestore in Datastore mode always prefers an index whose index properties prefix match the order by clause of the query. If `  experience  ` were added to the order by clause, then Firestore in Datastore mode will select the `  (experience [...], salary [...])  ` index for computing query results. Since there are no other constraints on `  experience  ` , Firestore in Datastore mode will read **all** index entries of the `  employees  ` collection before applying the `  salary  ` filter to find the final result set. This means that index entries which don't satisfy the `  salary  ` filter are still read, thus increasing the latency and cost of the query.

## Pricing

Queries with range and inequality filters on multiple properties are billed based on entities read and index entries read.

For detailed information, see the [Pricing](/datastore/docs/pricing) page.

## Limitations

Apart from the [query limitations](/datastore/docs/concepts/queries#limitations_2) , note the following limitations before using queries with range and inequality filters on multiple properties:

  - To prevent queries from becoming too expensive to run, Firestore in Datastore mode limits the number of range or inequality operators to 10.

## What's Next

  - Learn about [optimizing your queries](/datastore/docs/multiple-range-optimize-indexes) .
  - Learn more about [performing simple and compound queries](/datastore/docs/concepts/queries) .
  - Understand how [Firestore in Datastore mode uses indexes](/datastore/docs/concepts/indexes) .
