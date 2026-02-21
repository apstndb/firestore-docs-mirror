An aggregation query processes the data from multiple indexed entities to return a single summary value. Firestore in Datastore mode supports the following aggregation queries:

  - `  count()  `
  - `  sum()  `
  - `  avg()  `

Aggregation queries simplify your application code and cost less than fetching each entity for processing. Read this page to learn how to use aggregation queries.

## `     count()    ` aggregation

Use the `  count()  ` aggregation to return the total number of indexed entities that match a given query. For example, this `  count()  ` aggregation returns the total number of entities in a kind.

##### Java

``` java
import static com.google.cloud.datastore.aggregation.Aggregation.count;

import com.google.cloud.datastore.AggregationQuery;
import com.google.cloud.datastore.AggregationResult;
import com.google.cloud.datastore.Datastore;
import com.google.cloud.datastore.DatastoreOptions;
import com.google.cloud.datastore.Entity;
import com.google.cloud.datastore.EntityQuery;
import com.google.cloud.datastore.Key;
import com.google.cloud.datastore.Query;
import com.google.common.collect.Iterables;

public class CountAggregationOnKind {
  // Instantiates a client.
  private static final Datastore datastore = DatastoreOptions.getDefaultInstance().getService();

  // The kind for the new entity.
  private static final String kind = "Task";

  // Setting up Tasks in database
  private static void setUpTasks() {
    Key task1Key = datastore.newKeyFactory().setKind(kind).newKey("task1");
    Key task2Key = datastore.newKeyFactory().setKind(kind).newKey("task2");
    Key task3Key = datastore.newKeyFactory().setKind(kind).newKey("task3");

    // Save all the tasks.
    datastore.put(
        Entity.newBuilder(task1Key).set("done", true).build(),
        Entity.newBuilder(task2Key).set("done", false).build(),
        Entity.newBuilder(task3Key).set("done", true).build());
  }

  // Accessing aggregation result by the generated alias.
  private static void usageWithGeneratedAlias() {
    EntityQuery selectAllTasks = Query.newEntityQueryBuilder().setKind(kind).build();
    // Creating an aggregation query to get the count of all tasks.
    AggregationQuery allTasksCountQuery =
        Query.newAggregationQueryBuilder().over(selectAllTasks).addAggregation(count()).build();
    // Executing aggregation query.
    AggregationResult aggregationResult =
        Iterables.getOnlyElement(datastore.runAggregation(allTasksCountQuery));

    System.out.printf(
        "Total tasks (accessible from default alias) is %d",
        aggregationResult.get("property_1")); // 3
  }

  // Accessing aggregation result by the provided custom alias.
  private static void usageWithCustomAlias() {
    EntityQuery selectAllTasks = Query.newEntityQueryBuilder().setKind(kind).build();
    // Creating an aggregation query to get the count of all tasks.
    AggregationQuery allTasksCountQuery =
        Query.newAggregationQueryBuilder()
            .over(selectAllTasks)
            // passing 'total_count' as alias in the aggregation query.
            .addAggregation(count().as("total_count"))
            .build();
    // Executing aggregation query.
    AggregationResult aggregationResult =
        Iterables.getOnlyElement(datastore.runAggregation(allTasksCountQuery));

    System.out.printf("Total tasks count is %d", aggregationResult.get("total_count")); // 3
  }

  public static void invoke() {
    setUpTasks();
    usageWithGeneratedAlias();
    usageWithCustomAlias();
  }
}
```

##### Python

``` python
task1 = datastore.Entity(client.key("Task", "task1"))
task2 = datastore.Entity(client.key("Task", "task2"))

tasks = [task1, task2]
client.put_multi(tasks)
all_tasks_query = client.query(kind="Task")
all_tasks_count_query = client.aggregation_query(all_tasks_query).count()
query_result = all_tasks_count_query.fetch()
for aggregation_results in query_result:
    for aggregation in aggregation_results:
        print(f"Total tasks (accessible from default alias) is {aggregation.value}")
```

##### Go

``` text
aggregationCountQuery := datastore.NewQuery("Task").
  NewAggregationQuery().
  WithCount("total_tasks")

countResults, err := client.RunAggregationQuery(ctx, aggregationCountQuery)

count := countResults["total_tasks"]
countValue := count.(*datastorepb.Value)
fmt.Printf("Number of results from query: %d\n", countValue.GetIntegerValue())
```

##### GQL

``` text
AGGREGATE COUNT(*) AS total OVER ( SELECT * AS total FROM tasks )
```

GQL supports a simplified form of `  count()  ` queries:

``` text
SELECT COUNT(*) AS total FROM tasks
```

This example uses an optional alias of `  total  ` .

The simplified form supports only `  FROM  ` and `  WHERE  ` clauses. See the [GQL reference](/datastore/docs/reference/gql_reference#aggregationss) for more information.

The `  count()  ` aggregation takes into account any filters on the query and any `  limit  ` clauses. For example, the following aggregation returns a count of the number of entities that match the given filters.

##### Java

``` java
import static com.google.cloud.datastore.aggregation.Aggregation.count;

import com.google.cloud.datastore.AggregationQuery;
import com.google.cloud.datastore.AggregationResult;
import com.google.cloud.datastore.Datastore;
import com.google.cloud.datastore.DatastoreOptions;
import com.google.cloud.datastore.Entity;
import com.google.cloud.datastore.EntityQuery;
import com.google.cloud.datastore.Key;
import com.google.cloud.datastore.Query;
import com.google.cloud.datastore.StructuredQuery.PropertyFilter;
import com.google.common.collect.Iterables;

public class CountAggregationWithPropertyFilter {

  public static void invoke() {
    // Instantiates a client.
    Datastore datastore = DatastoreOptions.getDefaultInstance().getService();

    // The kind for the new entity.
    String kind = "Task";

    Key task1Key = datastore.newKeyFactory().setKind(kind).newKey("task1");
    Key task2Key = datastore.newKeyFactory().setKind(kind).newKey("task2");
    Key task3Key = datastore.newKeyFactory().setKind(kind).newKey("task3");

    // Save all the tasks.
    datastore.put(
        Entity.newBuilder(task1Key).set("done", true).build(),
        Entity.newBuilder(task2Key).set("done", false).build(),
        Entity.newBuilder(task3Key).set("done", true).build());

    EntityQuery completedTasks =
        Query.newEntityQueryBuilder()
            .setKind(kind)
            .setFilter(PropertyFilter.eq("done", true))
            .build();
    EntityQuery remainingTasks =
        Query.newEntityQueryBuilder()
            .setKind(kind)
            .setFilter(PropertyFilter.eq("done", false))
            .build();
    // Creating an aggregation query to get the count of all completed tasks.
    AggregationQuery completedTasksCountQuery =
        Query.newAggregationQueryBuilder()
            .over(completedTasks)
            .addAggregation(count().as("total_completed_count"))
            .build();
    // Creating an aggregation query to get the count of all remaining tasks.
    AggregationQuery remainingTasksCountQuery =
        Query.newAggregationQueryBuilder()
            .over(remainingTasks)
            .addAggregation(count().as("total_remaining_count"))
            .build();

    // Executing aggregation query.
    AggregationResult completedTasksCountQueryResult =
        Iterables.getOnlyElement(datastore.runAggregation(completedTasksCountQuery));
    AggregationResult remainingTasksCountQueryResult =
        Iterables.getOnlyElement(datastore.runAggregation(remainingTasksCountQuery));

    System.out.printf(
        "Total completed tasks count is %d",
        completedTasksCountQueryResult.get("total_completed_count")); // 2
    System.out.printf(
        "Total remaining tasks count is %d",
        remainingTasksCountQueryResult.get("total_remaining_count")); // 1
  }
}
```

##### Python

``` python
task1 = datastore.Entity(client.key("Task", "task1"))
task2 = datastore.Entity(client.key("Task", "task2"))
task3 = datastore.Entity(client.key("Task", "task3"))

task1["done"] = True
task2["done"] = False
task3["done"] = True

tasks = [task1, task2, task3]
client.put_multi(tasks)
completed_tasks = client.query(kind="Task").add_filter("done", "=", True)
remaining_tasks = client.query(kind="Task").add_filter("done", "=", False)

completed_tasks_query = client.aggregation_query(query=completed_tasks).count(
    alias="total_completed_count"
)
remaining_tasks_query = client.aggregation_query(query=remaining_tasks).count(
    alias="total_remaining_count"
)

completed_query_result = completed_tasks_query.fetch()
for aggregation_results in completed_query_result:
    for aggregation_result in aggregation_results:
        if aggregation_result.alias == "total_completed_count":
            print(f"Total completed tasks count is {aggregation_result.value}")

remaining_query_result = remaining_tasks_query.fetch()
for aggregation_results in remaining_query_result:
    for aggregation_result in aggregation_results:
        if aggregation_result.alias == "total_remaining_count":
            print(f"Total remaining tasks count is {aggregation_result.value}")
```

##### Go

``` text
aggregationCountQuery := datastore.NewQuery("Task").
  FilterField("done", "=", true).
  NewAggregationQuery().
  WithCount("total_tasks_done")

countResults, err := client.RunAggregationQuery(ctx, aggregationCountQuery)

count := countResults["total_tasks_done"]
countValue := count.(*datastorepb.Value)
fmt.Printf("Number of results from query: %d\n", countValue.GetIntegerValue())
```

##### GQL

``` text
AGGREGATE COUNT(*) OVER ( SELECT * FROM tasks WHERE is_done = false AND tag = 'house')
```

GQL supports a simplified form of `  count()  ` queries:

``` text
SELECT COUNT(*) AS total
FROM tasks
WHERE is_done = false AND tag = 'house'
```

This example uses an optional alias of `  total  ` .

The simplified form supports only `  FROM  ` and `  WHERE  ` clauses. See the [GQL reference](/datastore/docs/reference/gql_reference#aggregationss) for more information.

This example shows how to count up to a certain value. You can use this to, for example, stop counting at a certain number and inform users that they exceeded that number.

##### Java

``` java
import static com.google.cloud.datastore.aggregation.Aggregation.count;

import com.google.cloud.datastore.AggregationQuery;
import com.google.cloud.datastore.AggregationResult;
import com.google.cloud.datastore.Datastore;
import com.google.cloud.datastore.DatastoreOptions;
import com.google.cloud.datastore.Entity;
import com.google.cloud.datastore.EntityQuery;
import com.google.cloud.datastore.Key;
import com.google.cloud.datastore.Query;
import com.google.common.collect.Iterables;

public class CountAggregationWithLimit {
  public static void invoke() {
    // Instantiates a client.
    Datastore datastore = DatastoreOptions.getDefaultInstance().getService();

    // The kind for the new entity.
    String kind = "Task";

    Key task1Key = datastore.newKeyFactory().setKind(kind).newKey("task1");
    Key task2Key = datastore.newKeyFactory().setKind(kind).newKey("task2");
    Key task3Key = datastore.newKeyFactory().setKind(kind).newKey("task3");

    // Save all the tasks.
    datastore.put(
        Entity.newBuilder(task1Key).set("done", true).build(),
        Entity.newBuilder(task2Key).set("done", false).build(),
        Entity.newBuilder(task3Key).set("done", true).build());

    EntityQuery selectAllTasks = Query.newEntityQueryBuilder().setKind(kind).setLimit(2).build();
    // Creating an aggregation query to get the count of all tasks.
    AggregationQuery allTasksCountQuery =
        Query.newAggregationQueryBuilder()
            .over(selectAllTasks)
            .addAggregation(count().as("at_least"))
            .build();
    // Executing aggregation query.
    AggregationResult limitQueryResult =
        Iterables.getOnlyElement(datastore.runAggregation(allTasksCountQuery));

    System.out.printf("We have at least %d tasks", limitQueryResult.get("at_least")); // 2
  }
}
```

##### Python

``` python
task1 = datastore.Entity(client.key("Task", "task1"))
task2 = datastore.Entity(client.key("Task", "task2"))
task3 = datastore.Entity(client.key("Task", "task3"))

tasks = [task1, task2, task3]
client.put_multi(tasks)
all_tasks_query = client.query(kind="Task")
all_tasks_count_query = client.aggregation_query(all_tasks_query).count()
query_result = all_tasks_count_query.fetch(limit=2)
for aggregation_results in query_result:
    for aggregation in aggregation_results:
        print(f"We have at least {aggregation.value} tasks")
```

##### Go

``` text
aggregationCountQuery := datastore.NewQuery("Task").
  Limit(2).
  NewAggregationQuery().
  WithCount("at_least")

countResults, err := client.RunAggregationQuery(ctx, aggregationCountQuery)

count := countResults["at_least"]
countValue := count.(*datastorepb.Value)
fmt.Printf("We have at least %d tasks\n", countValue.GetIntegerValue())
```

##### GQL

``` text
AGGREGATE COUNT_UP_TO(1000) OVER ( SELECT * FROM tasks WHERE is_done = false)
```

GQL supports a simplified form of `  count_up_to()  ` queries:

``` text
SELECT COUNT_UP_TO(1000) AS total
FROM tasks
WHERE is_done = false AND tag = 'house'
```

This example uses an optional alias of `  total  ` .

The simplified form supports only `  FROM  ` and `  WHERE  ` clauses. See the [GQL reference](/datastore/docs/reference/gql_reference#aggregationss) for more information.

## `     sum()    ` aggregation

Use the `  sum()  ` aggregation to return the total sum of numeric values that match a given query. For example, the following `  sum()  ` aggregation returns the total sum of numeric values of the given property from entities of the given kind:

##### Java

``` java
import static com.google.cloud.datastore.aggregation.Aggregation.sum;

import com.google.cloud.datastore.AggregationQuery;
import com.google.cloud.datastore.AggregationResult;
import com.google.cloud.datastore.Datastore;
import com.google.cloud.datastore.DatastoreOptions;
import com.google.cloud.datastore.Entity;
import com.google.cloud.datastore.EntityQuery;
import com.google.cloud.datastore.Key;
import com.google.cloud.datastore.Query;
import com.google.common.collect.Iterables;

public class SumAggregationOnKind {

  // Instantiates a client.
  private static final Datastore datastore = DatastoreOptions.getDefaultInstance().getService();

  // The kind for the new entity.
  private static final String kind = "Sales";

  // Setting up Sales in database
  private static void setUpSales() {
    Key sales1Key = datastore.newKeyFactory().setKind(kind).newKey("sales1");
    Key sales2Key = datastore.newKeyFactory().setKind(kind).newKey("sales2");
    Key sales3Key = datastore.newKeyFactory().setKind(kind).newKey("sales3");

    // Save all the sales.
    datastore.put(
        Entity.newBuilder(sales1Key).set("amount", 89).build(),
        Entity.newBuilder(sales2Key).set("amount", 95).build(),
        Entity.newBuilder(sales3Key).set("amount", 55).build());
  }

  // Accessing aggregation result by the provided custom alias.
  private static void usageWithCustomAlias() {
    EntityQuery selectAllSales = Query.newEntityQueryBuilder().setKind(kind).build();
    // Creating an aggregation query to get the sum of all sales.
    AggregationQuery sumOfSalesQuery =
        Query.newAggregationQueryBuilder()
            .over(selectAllSales)
            // passing 'total_sales_amount' as alias in the aggregation query.
            .addAggregation(sum("amount").as("total_sales_amount"))
            .build();
    // Executing aggregation query.
    AggregationResult aggregationResult =
        Iterables.getOnlyElement(datastore.runAggregation(sumOfSalesQuery));

    System.out.printf("Total sales is %d", aggregationResult.getLong("total_sales_amount")); // 239
  }

  public static void invoke() {
    setUpSales();
    usageWithCustomAlias();
  }
}
```

##### Python

``` python
# Set up sample entities
# Use incomplete key to auto-generate ID
task1 = datastore.Entity(client.key("Task"))
task2 = datastore.Entity(client.key("Task"))
task3 = datastore.Entity(client.key("Task"))

task1["hours"] = 5
task2["hours"] = 3
task3["hours"] = 1

tasks = [task1, task2, task3]
client.put_multi(tasks)

# Execute sum aggregation query
all_tasks_query = client.query(kind="Task")
all_tasks_sum_query = client.aggregation_query(all_tasks_query).sum("hours")
query_result = all_tasks_sum_query.fetch()
for aggregation_results in query_result:
    for aggregation in aggregation_results:
        print(f"Total sum of hours in tasks is {aggregation.value}")
```

##### Go

``` text
aggregationSumQuery := datastore.NewQuery("Task").
  NewAggregationQuery().
  WithSum("hours", "total_hours")
sumResults, err := client.RunAggregationQuery(ctx, aggregationSumQuery)

sum := sumResults["total_hours"]
sumValue := sum.(*datastorepb.Value)
fmt.Printf("Sum of results from query: %d\n", sumValue.GetIntegerValue())
```

##### GQL

``` text
AGGREGATE
  SUM(hours) AS total_hours
OVER (
  SELECT *
  FROM tasks
)
```

GQL supports a simplified form of `  sum()  ` queries:

``` text
SELECT SUM(hours) AS total_hours FROM tasks
```

This example uses an optional alias of `  total_hours  ` .

The simplified form supports only `  FROM  ` and `  WHERE  ` clauses. See the [GQL reference](/datastore/docs/reference/gql_reference#aggregationss) for more information.

The `  sum()  ` aggregation takes into account any filters on the query and any `  limit  ` clauses. For example, the following aggregation returns a sum of the specified property with a numeric value in entities that match the given filters.

##### Java

``` java
import static com.google.cloud.datastore.aggregation.Aggregation.sum;

import com.google.cloud.datastore.AggregationQuery;
import com.google.cloud.datastore.AggregationResult;
import com.google.cloud.datastore.Datastore;
import com.google.cloud.datastore.DatastoreOptions;
import com.google.cloud.datastore.Entity;
import com.google.cloud.datastore.EntityQuery;
import com.google.cloud.datastore.Key;
import com.google.cloud.datastore.Query;
import com.google.cloud.datastore.StructuredQuery.PropertyFilter;
import com.google.common.collect.Iterables;

public class SumAggregationWithPropertyFilter {

  public static void invoke() {
    // Instantiates a client.
    Datastore datastore = DatastoreOptions.getDefaultInstance().getService();

    // The kind for the new entity.
    String kind = "Sales";

    Key sales1Key = datastore.newKeyFactory().setKind(kind).newKey("sales1");
    Key sales2Key = datastore.newKeyFactory().setKind(kind).newKey("sales2");
    Key sales3Key = datastore.newKeyFactory().setKind(kind).newKey("sales3");

    // Save all the tasks.
    datastore.put(
        Entity.newBuilder(sales1Key).set("amount", 89).set("customerId", 1).build(),
        Entity.newBuilder(sales2Key).set("amount", 95).set("customerId", 1).build(),
        Entity.newBuilder(sales3Key).set("amount", 55).set("customerId", 2).build());

    EntityQuery customer1Sales =
        Query.newEntityQueryBuilder()
            .setKind(kind)
            .setFilter(PropertyFilter.eq("customerId", 1))
            .build();

    // Creating an aggregation query to get the sum of all sales for customerId 1.
    AggregationQuery customer1SalesSum =
        Query.newAggregationQueryBuilder()
            .over(customer1Sales)
            .addAggregation(sum("amount").as("total_sales"))
            .build();

    // Executing aggregation query.
    AggregationResult customer1SalesSumQueryResult =
        Iterables.getOnlyElement(datastore.runAggregation(customer1SalesSum));

    System.out.printf(
        "Customer 1 sales sum is %d", customer1SalesSumQueryResult.getLong("total_sales")); // 184
  }
}
```

##### Python

``` python
# Set up sample entities
# Use incomplete key to auto-generate ID
task1 = datastore.Entity(client.key("Task"))
task2 = datastore.Entity(client.key("Task"))
task3 = datastore.Entity(client.key("Task"))

task1["hours"] = 5
task2["hours"] = 3
task3["hours"] = 1

task1["done"] = True
task2["done"] = True
task3["done"] = False

tasks = [task1, task2, task3]
client.put_multi(tasks)

# Execute sum aggregation query with filters
completed_tasks = client.query(kind="Task").add_filter("done", "=", True)
completed_tasks_query = client.aggregation_query(query=completed_tasks).sum(
    property_ref="hours", alias="total_completed_sum_hours"
)

completed_query_result = completed_tasks_query.fetch()
for aggregation_results in completed_query_result:
    for aggregation_result in aggregation_results:
        if aggregation_result.alias == "total_completed_sum_hours":
            print(
                f"Total sum of hours in completed tasks is {aggregation_result.value}"
            )
```

This query requires an index such as:

``` text
- kind: Task
  properties:
  - name: done
  - name: hours
```

##### Go

``` text
aggregationSumQuery := datastore.NewQuery("Task").
  FilterField("done", "=", false).
  FilterField("tag", "=", "house").
  NewAggregationQuery().
  WithSum("hours", "total_hours")
sumResults, err := client.RunAggregationQuery(ctx, aggregationSumQuery)

sum := sumResults["total_hours"]
sumValue := sum.(*datastorepb.Value)
fmt.Printf("Sum of results from query: %d\n", sumValue.GetIntegerValue())
```

##### GQL

``` text
AGGREGATE
  SUM(hours) AS total_hours
OVER (
  SELECT *
  FROM tasks
  WHERE is_done = false AND tag = 'house'
)
```

GQL supports a simplified form of `  sum()  ` queries:

``` text
SELECT
  SUM(hours) AS total_hours
FROM tasks
WHERE is_done = false AND tag = 'house'
```

This example uses an optional alias of `  total_hours  ` .

The simplified form supports only `  FROM  ` and `  WHERE  ` clauses. See the [GQL reference](/datastore/docs/reference/gql_reference#aggregationss) for more information.

## `     avg()    ` aggregation

Use the `  avg()  ` aggregation to return the average of numeric values that match a given query. For example, the following `  avg()  ` aggregation returns the arithmetic mean of the specified property from the numeric property values of entities that match the query:

##### Java

``` java
import static com.google.cloud.datastore.aggregation.Aggregation.avg;

import com.google.cloud.datastore.AggregationQuery;
import com.google.cloud.datastore.AggregationResult;
import com.google.cloud.datastore.Datastore;
import com.google.cloud.datastore.DatastoreOptions;
import com.google.cloud.datastore.Entity;
import com.google.cloud.datastore.EntityQuery;
import com.google.cloud.datastore.Key;
import com.google.cloud.datastore.Query;
import com.google.common.collect.Iterables;

public class AvgAggregationOnKind {

  // Instantiates a client.
  private static final Datastore datastore = DatastoreOptions.getDefaultInstance().getService();

  // The kind for the new entity.
  private static final String kind = "Sales";

  // Setting up Sales in database
  private static void setUpSales() {
    Key sales1Key = datastore.newKeyFactory().setKind(kind).newKey("sales1");
    Key sales2Key = datastore.newKeyFactory().setKind(kind).newKey("sales2");
    Key sales3Key = datastore.newKeyFactory().setKind(kind).newKey("sales3");

    // Save all the sales.
    datastore.put(
        Entity.newBuilder(sales1Key).set("amount", 89).build(),
        Entity.newBuilder(sales2Key).set("amount", 95).build(),
        Entity.newBuilder(sales3Key).set("amount", 55).build());
  }

  // Accessing aggregation result by the provided custom alias.
  private static void usageWithCustomAlias() {
    EntityQuery selectAllSales = Query.newEntityQueryBuilder().setKind(kind).build();
    // Creating an aggregation query to get the avg of all sales.
    AggregationQuery avgOfSalesQuery =
        Query.newAggregationQueryBuilder()
            .over(selectAllSales)
            // passing 'avg_sales_amount' as alias in the aggregation query.
            .addAggregation(avg("amount").as("avg_sales_amount"))
            .build();
    // Executing aggregation query.
    AggregationResult aggregationResult =
        Iterables.getOnlyElement(datastore.runAggregation(avgOfSalesQuery));

    System.out.printf(
        "Average sales is %.8f", aggregationResult.getDouble("avg_sales_amount")); // 79.66666667
  }

  public static void invoke() {
    setUpSales();
    usageWithCustomAlias();
  }
}
```

##### Python

``` python
# Set up sample entities
# Use incomplete key to auto-generate ID
task1 = datastore.Entity(client.key("Task"))
task2 = datastore.Entity(client.key("Task"))
task3 = datastore.Entity(client.key("Task"))

task1["hours"] = 5
task2["hours"] = 3
task3["hours"] = 1

tasks = [task1, task2, task3]
client.put_multi(tasks)

# Execute average aggregation query
all_tasks_query = client.query(kind="Task")
all_tasks_avg_query = client.aggregation_query(all_tasks_query).avg("hours")
query_result = all_tasks_avg_query.fetch()
for aggregation_results in query_result:
    for aggregation in aggregation_results:
        print(f"Total average of hours in tasks is {aggregation.value}")
```

##### Go

``` text
aggregationAvgQuery := datastore.NewQuery("Task").
  NewAggregationQuery().
  WithAvg("hours", "avg_hours")
avgResults, err := client.RunAggregationQuery(ctx, aggregationAvgQuery)

avg := avgResults["avg_hours"]
avgValue := avg.(*datastorepb.Value)
fmt.Printf("average hours: %f\n", avgValue.GetDoubleValue())
```

##### GQL

``` text
AGGREGATE
  AVG(hours) as avg_hours
OVER (
  SELECT *
  FROM tasks
)
```

GQL supports a simplified form of `  avg()  ` queries:

``` text
SELECT AVG(hours) as avg_hours
```

This example uses an optional alias of `  avg_hours  ` .

The simplified form supports only `  FROM  ` and `  WHERE  ` clauses. See the [GQL reference](/datastore/docs/reference/gql_reference#aggregationss) for more information.

The `  avg()  ` aggregation takes into account any filters on the query and any `  limit  ` clauses. For example, the following aggregation returns the arithmetic mean of the specified property from the numeric property values of entities that match the query filters.

##### Java

``` java
import static com.google.cloud.datastore.aggregation.Aggregation.avg;

import com.google.cloud.datastore.AggregationQuery;
import com.google.cloud.datastore.AggregationResult;
import com.google.cloud.datastore.Datastore;
import com.google.cloud.datastore.DatastoreOptions;
import com.google.cloud.datastore.Entity;
import com.google.cloud.datastore.EntityQuery;
import com.google.cloud.datastore.Key;
import com.google.cloud.datastore.Query;
import com.google.cloud.datastore.StructuredQuery.PropertyFilter;
import com.google.common.collect.Iterables;

public class AvgAggregationWithPropertyFilter {

  public static void invoke() {
    // Instantiates a client.
    Datastore datastore = DatastoreOptions.getDefaultInstance().getService();

    // The kind for the new entity.
    String kind = "Sales";

    Key sales1Key = datastore.newKeyFactory().setKind(kind).newKey("sales1");
    Key sales2Key = datastore.newKeyFactory().setKind(kind).newKey("sales2");
    Key sales3Key = datastore.newKeyFactory().setKind(kind).newKey("sales3");

    // Save all the tasks.
    datastore.put(
        Entity.newBuilder(sales1Key).set("amount", 89).set("customerId", 1).build(),
        Entity.newBuilder(sales2Key).set("amount", 95).set("customerId", 1).build(),
        Entity.newBuilder(sales3Key).set("amount", 55).set("customerId", 2).build());

    EntityQuery customer1Sales =
        Query.newEntityQueryBuilder()
            .setKind(kind)
            .setFilter(PropertyFilter.eq("customerId", 1))
            .build();

    // Creating an aggregation query to get the avg of all sales for customerId 1.
    AggregationQuery customer1SalesAvg =
        Query.newAggregationQueryBuilder()
            .over(customer1Sales)
            .addAggregation(avg("amount").as("total_sales"))
            .build();

    // Executing aggregation query.
    AggregationResult customer1SalesAvgQueryResult =
        Iterables.getOnlyElement(datastore.runAggregation(customer1SalesAvg));

    System.out.printf(
        "Customer 1 sales avg is %d", customer1SalesAvgQueryResult.getLong("total_sales")); // 92
  }
}
```

##### Python

``` python
# Set up sample entities
# Use incomplete key to auto-generate ID
task1 = datastore.Entity(client.key("Task"))
task2 = datastore.Entity(client.key("Task"))
task3 = datastore.Entity(client.key("Task"))

task1["hours"] = 5
task2["hours"] = 3
task3["hours"] = 1

task1["done"] = True
task2["done"] = True
task3["done"] = False

tasks = [task1, task2, task3]
client.put_multi(tasks)

# Execute average aggregation query with filters
completed_tasks = client.query(kind="Task").add_filter("done", "=", True)
completed_tasks_query = client.aggregation_query(query=completed_tasks).avg(
    property_ref="hours", alias="total_completed_avg_hours"
)

completed_query_result = completed_tasks_query.fetch()
for aggregation_results in completed_query_result:
    for aggregation_result in aggregation_results:
        if aggregation_result.alias == "total_completed_avg_hours":
            print(
                f"Total average of hours in completed tasks is {aggregation_result.value}"
            )
```

This query requires an index such as:

``` text
- kind: Task
  properties:
  - name: done
  - name: hours
```

##### Go

``` text
aggregationAvgQuery := datastore.NewQuery("Task").
  FilterField("done", "=", false).
  FilterField("tag", "=", "house").
  NewAggregationQuery().
  WithAvg("hours", "avg_hours")
avgResults, err := client.RunAggregationQuery(ctx, aggregationAvgQuery)

avg := avgResults["avg_hours"]
avgValue := avg.(*datastorepb.Value)
fmt.Printf("average hours: %f\n", avgValue.GetDoubleValue())
```

##### GQL

``` text
AGGREGATE
  AVG(hours) as avg_hours
OVER (
  SELECT *
  FROM tasks
  WHERE is_done = false AND tag = 'house'
)
```

GQL supports a simplified form of `  avg()  ` queries:

``` text
SELECT
  AVG(hours) as avg_hours
FROM tasks
WHERE is_done = false AND tag = 'house'
```

This example uses an optional alias of `  avg_hours  ` .

The simplified form supports only `  FROM  ` and `  WHERE  ` clauses. See the [GQL reference](/datastore/docs/reference/gql_reference#aggregationss) for more information.

## Calculate multiple aggregations in a query

You can combine multiple aggregations in a single aggregation pipeline. This can reduce the number of index reads required. If the query includes aggregations on multiple fields, the query requires a composite index, and each aggregation calculation includes only those entities that contain all the fields used by each aggregation.

The following example performs multiple aggregations in a single aggregation query:

##### Java

``` java
import static com.google.cloud.datastore.aggregation.Aggregation.avg;
import static com.google.cloud.datastore.aggregation.Aggregation.count;
import static com.google.cloud.datastore.aggregation.Aggregation.sum;

import com.google.cloud.datastore.AggregationQuery;
import com.google.cloud.datastore.AggregationResult;
import com.google.cloud.datastore.Datastore;
import com.google.cloud.datastore.DatastoreOptions;
import com.google.cloud.datastore.Entity;
import com.google.cloud.datastore.EntityQuery;
import com.google.cloud.datastore.Key;
import com.google.cloud.datastore.Query;
import com.google.common.collect.Iterables;

public class MultipleAggregationsInStructuredQuery {

  public static void invoke() {
    // Instantiates a client.
    Datastore datastore = DatastoreOptions.getDefaultInstance().getService();

    // The kind for the new entity.
    String kind = "Sales";

    Key sales1Key = datastore.newKeyFactory().setKind(kind).newKey("sales1");
    Key sales2Key = datastore.newKeyFactory().setKind(kind).newKey("sales2");
    Key sales3Key = datastore.newKeyFactory().setKind(kind).newKey("sales3");

    // Save all the sales.
    datastore.put(
        Entity.newBuilder(sales1Key).set("amount", 89).set("customerId", 1).build(),
        Entity.newBuilder(sales2Key).set("amount", 95).set("customerId", 1).build(),
        Entity.newBuilder(sales3Key).set("amount", 55).set("customerId", 2).build());

    EntityQuery baseQuery = Query.newEntityQueryBuilder().setKind(kind).build();

    // Creating an aggregation query with COUNT, SUM and AVG aggregations.
    AggregationQuery aggregationQuery =
        Query.newAggregationQueryBuilder()
            .over(baseQuery)
            .addAggregation(count().as("total_count"))
            .addAggregation(sum("amount").as("sales_sum"))
            .addAggregation(avg("amount").as("sales_avg"))
            .build();

    // Executing aggregation query.
    AggregationResult aggregationResult =
        Iterables.getOnlyElement(datastore.runAggregation(aggregationQuery));

    System.out.printf("Total sales count: %d", aggregationResult.getLong("total_count")); // 3
    System.out.printf("Sum of sales: %d", aggregationResult.getLong("sales_sum")); // 239
    System.out.printf(
        "Avg of sales: %.8f", aggregationResult.getDouble("sales_avg")); // 79.66666667
  }
}
```

##### Python

``` python
# Set up sample entities
# Use incomplete key to auto-generate ID
task1 = datastore.Entity(client.key("Task"))
task2 = datastore.Entity(client.key("Task"))
task3 = datastore.Entity(client.key("Task"))

task1["hours"] = 5
task2["hours"] = 3
task3["hours"] = 1

tasks = [task1, task2, task3]
client.put_multi(tasks)

# Execute query with multiple aggregations
all_tasks_query = client.query(kind="Task")
aggregation_query = client.aggregation_query(all_tasks_query)
# Add aggregations
aggregation_query.add_aggregations(
    [
        datastore.aggregation.CountAggregation(alias="count_aggregation"),
        datastore.aggregation.SumAggregation(
            property_ref="hours", alias="sum_aggregation"
        ),
        datastore.aggregation.AvgAggregation(
            property_ref="hours", alias="avg_aggregation"
        ),
    ]
)

query_result = aggregation_query.fetch()
for aggregation_results in query_result:
    for aggregation in aggregation_results:
        print(f"{aggregation.alias} value is {aggregation.value}")
```

##### Go

``` text
aggregationQuery := datastore.NewQuery("Task").
  NewAggregationQuery().
  WithCount("total_tasks").
  WithSum("hours", "total_hours").
  WithAvg("hours", "avg_hours")
Results, err := client.RunAggregationQuery(ctx, aggregationQuery)

fmt.Printf("Number of results from query: %d\n", Results["total_tasks"].(*datastorepb.Value).GetIntegerValue())
fmt.Printf("Sum of results from query: %d\n", Results["total_hours"].(*datastorepb.Value).GetIntegerValue())
fmt.Printf("Avg of results from query: %f\n", Results["avg_hours"].(*datastorepb.Value).GetDoubleValue())
```

##### GQL

``` text
AGGREGATE 
  SUM(hours) AS total_hours, 
  COUNT(*) AS total_tasks
OVER (
  SELECT *
  FROM tasks
  WHERE is_done = false AND tag = 'house'
)
```

GQL supports a simplified form for aggregation queries:

``` text
SELECT
  SUM(hours) AS total_hours,
  COUNT(*) AS total_tasks
FROM tasks
WHERE is_done = false AND tag = 'house'
```

This example uses the optional aliases of `  total_hours  ` and `  total_tasks  ` .

The simplified form supports only `  FROM  ` and `  WHERE  ` clauses. See the [GQL reference](/datastore/docs/reference/gql_reference#aggregationss) for more information.

Queries with multiple aggregation include only the entities that contain all the properties in each aggregation. This might lead to different results from performing each aggregation separately.

## Behavior and limitations

As you work with aggregation queries, note the following behavior and limitations:

  - The query you provide to the aggregation must meet the [restrictions on queries](/datastore/docs/concepts/queries#restrictions_on_queries) .

  - If an aggregation query cannot resolve within 60 seconds, it returns a `  DEADLINE_EXCEEDED  ` error. Performance depends on your index configuration and on the size of the dataset.
    
    **Note:** Most queries scale based on the on the size of the result set, not the dataset. However, aggregation queries scale based on the size of the dataset and the number of index entries scanned.
    
    If the operation cannot be completed within the 60 second deadline, a possible workaround is to use [cursors](/datastore/docs/concepts/queries#cursors_limits_and_offsets) to merge multiple aggregations.

  - Aggregation queries read from index entries and include only indexed properties in the calculation.

  - Adding an `  OrderBy  ` clause to the query limits the aggregation to the entities where the sorting property exists.

  - In GQL, the [simplified form](/datastore/docs/reference/gql_reference#aggregationss) does not support `  ORDER BY  ` , `  LIMIT  ` , or `  OFFSET  ` clauses.

  - In a projection query, you can aggregate data only from the properties in the projection. For example, in the GQL query `  SELECT a, b FROM k WHERE c = 1  ` , you can aggregate data only from among `  a  ` or `  b  ` .

  - A `  count()  ` aggregation does not de-duplicate entities with array properties. Each array value that matches the query adds one to the count.

  - For `  sum()  ` and `  avg()  ` aggregations, Non-numeric values are ignored. `  sum()  ` and `  avg()  ` aggregation take into account only integer values, floating-point number values, and timestamps. Timestamps are converted to microsecond integer values for `  sum()  ` , `  avg()  ` , and [projections](/datastore/docs/concepts/queries#limitations_on_projections) .

  - When combining multiple aggregations in a single query, note that `  sum()  ` and `  avg()  ` ignore non-numeric values while `  count()  ` includes non-numeric values.

  - If you combine aggregations that are on different properties, the calculation includes only the entities that contain all those properties. This might lead to different results from performing each aggregation separately.

## Pricing

Pricing for the `  count()  ` , `  sum()  ` , and `  avg()  ` aggregation queries depends on the number of index entries scanned during the operation. You are billed one entity read for up to 1,000 index entries matched. Subsequent index entries matched cost additional read units. There is a minimum cost of one read unit for every query. For pricing information, see [Firestore in Datastore mode pricing](https://cloud.google.com/datastore/pricing#entity_reads) .

If you combine multiple aggregation in a single query, the query uses the same index for each aggregation and performs a single scan over the data. This can help reduce the number of index scans and reads billed when compared to performing each aggregation separately. However, queries with multiple aggregations include only the entities that contain all those properties. This might lead to different results from performing each aggregation separately.

## What's next

  - Learn about [queries](/datastore/docs/concepts/queries) .
  - Learn about [best practices for Firestore in Datastore mode](/datastore/docs/best-practices) .
