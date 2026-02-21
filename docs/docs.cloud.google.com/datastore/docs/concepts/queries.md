A *query* retrieves [*entities*](/datastore/docs/concepts/entities) from Firestore in Datastore mode that meet a specified set of conditions.

The query operates on entities of a given [*kind*](/datastore/docs/concepts/entities#kinds_and_identifiers) ; it can specify [*filters*](#filters) on the entities' property values, keys, and ancestors, and can return zero or more entities as *results* . A query can also specify [*sort orders*](#sort_orders) to sequence the results by their property values. The results include all entities that have at least one value for every property named in the filters and sort orders, and whose property values meet all the specified filter criteria. The query can return entire entities, projected entities, or just entity keys.

A typical query includes the following:

  - An [entity kind](/datastore/docs/concepts/entities#kinds_and_identifiers) to which the query applies
  - Zero or more [filters](#filters) based on the entities' property values, keys, and ancestors
  - Zero or more [sort orders](#sort_orders) to sequence the results

When executed, the query retrieves all entities of the given kind that satisfy all of the given filters, sorted in the specified order. Queries execute as read-only.

**Note:** To conserve memory and improve performance, a query should, whenever possible, specify a limit on the number of results returned.

Every query computes its results using one or more [*indexes*](/datastore/docs/concepts/indexes) , which contain entity keys in a sequence specified by the index's properties and, optionally, the entity's ancestors. The indexes are updated incrementally to reflect any changes the application makes to its entities, so that the correct results of all queries are available with no further computation needed.

The index-based query mechanism supports a wide range of queries and is suitable for most applications, except for non-scaling queries, such as join queries. For more information about limitations on Datastore mode queries, see [Restrictions on queries](#restrictions_on_queries) .

## Query interface

You can issue a query against a Datastore mode database. The following example shows how to retrieve all tasks that are not yet done with priorities greater than or equal to 4, sorted in descending order by priority:

### C\#

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore C\# API reference documentation](https://cloud.google.com/dotnet/docs/reference/Google.Cloud.Datastore.V1/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
Query query = new Query("Task")
{
    Filter = Filter.And(Filter.Equal("done", false),
        Filter.GreaterThanOrEqual("priority", 4)),
    Order = { { "priority", PropertyOrder.Types.Direction.Descending } }
};
```

### Go

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Go API reference documentation](https://cloud.google.com/go/docs/reference/cloud.google.com/go/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` go
query := datastore.NewQuery("Task").
 FilterField("Done", "=", false).
 FilterField("Priority", ">=", 4).
 Order("-Priority")
```

### Java

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Java API reference documentation](https://cloud.google.com/java/docs/reference/google-cloud-datastore/latest/history) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
Query<Entity> query =
    Query.newEntityQueryBuilder()
        .setKind("Task")
        .setFilter(
            CompositeFilter.and(
                PropertyFilter.eq("done", false), PropertyFilter.ge("priority", 4)))
        .setOrderBy(OrderBy.desc("priority"))
        .build();
```

### Node.js

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Node.js API reference documentation](https://cloud.google.com/nodejs/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` javascript
const query = datastore
  .createQuery('Task')
  .filter(
    and([
      new PropertyFilter('done', '=', false),
      new PropertyFilter('priority', '>=', 4),
    ]),
  )
  .order('priority', {
    descending: true,
  });
```

### PHP

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore PHP API reference documentation](https://googleapis.github.io/google-cloud-php/#/docs/cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
$query = $datastore->query()
    ->kind('Task')
    ->filter('done', '=', false)
    ->filter('priority', '>=', 4)
    ->order('priority', Query::ORDER_DESCENDING);
```

### Python

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Python API reference documentation](https://cloud.google.com/python/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
from google.cloud import datastore

# For help authenticating your client, visit
# https://cloud.google.com/docs/authentication/getting-started
client = datastore.Client()

query = client.query(kind="Task")
query.add_filter(filter=datastore.query.PropertyFilter("done", "=", False))
query.add_filter(filter=datastore.query.PropertyFilter("priority", ">=", 4))
query.order = ["-priority"]
```

### Ruby

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Ruby API reference documentation](/ruby/docs/reference/google-cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
query = datastore.query("Task")
                 .where("done", "=", false)
                 .where("priority", ">=", 4)
                 .order("priority", :desc)
```

### GQL

``` text
SELECT * FROM Task
WHERE done = FALSE AND priority >= 4
ORDER BY priority DESC
```

**Note:** The properties being filtered on must have a corresponding predefined index which can be defined in your [index configuration file](/datastore/docs/tools/indexconfig) ( `  index.yaml  ` ).

The following example shows how to run a query:

### C\#

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore C\# API reference documentation](https://cloud.google.com/dotnet/docs/reference/Google.Cloud.Datastore.V1/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
Query query = new Query("Task");
DatastoreQueryResults tasks = _db.RunQuery(query);
```

### Go

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Go API reference documentation](https://cloud.google.com/go/docs/reference/cloud.google.com/go/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` go
it := client.Run(ctx, query)
for {
 var task Task
 _, err := it.Next(&task)
 if err == iterator.Done {
     break
 }
 if err != nil {
     log.Fatalf("Error fetching next task: %v", err)
 }
 fmt.Printf("Task %q, Priority %d\n", task.Description, task.Priority)
}
```

### Java

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Java API reference documentation](https://cloud.google.com/java/docs/reference/google-cloud-datastore/latest/history) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
QueryResults<Entity> tasks = datastore.run(query);
```

### Node.js

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Node.js API reference documentation](https://cloud.google.com/nodejs/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` javascript
const [tasks] = await datastore.runQuery(query);
console.log('Tasks:');
tasks.forEach(task => console.log(task));
```

### PHP

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore PHP API reference documentation](https://googleapis.github.io/google-cloud-php/#/docs/cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
$result = $datastore->runQuery($query);
```

### Python

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Python API reference documentation](https://cloud.google.com/python/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
from google.cloud import datastore

# For help authenticating your client, visit
# https://cloud.google.com/docs/authentication/getting-started
client = datastore.Client()

query = client.query()
results = list(query.fetch())
```

### Ruby

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Ruby API reference documentation](/ruby/docs/reference/google-cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
tasks = datastore.run query
```

### GQL

Not Applicable

## Query structure

A query can specify an [entity kind](/datastore/docs/concepts/entities#kinds_and_identifiers) , zero or more [filters](#filters) , and zero or more [sort orders](#sort_orders) .

### Filters

A query's *filters* set constraints on the [properties](#property_filters) , [keys](#key_filters) , and ancestors of the entities to be retrieved.

#### Property filters

A *property filter* specifies the following:

  - A property name
  - A comparison operator
  - A property value

The following example returns task entities that are marked not done:

### C\#

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore C\# API reference documentation](https://cloud.google.com/dotnet/docs/reference/Google.Cloud.Datastore.V1/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
Query query = new Query("Task")
{
    Filter = Filter.Equal("done", false)
};
```

### Go

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Go API reference documentation](https://cloud.google.com/go/docs/reference/cloud.google.com/go/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` go
query := datastore.NewQuery("Task").FilterField("Done", "=", false)
```

### Java

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Java API reference documentation](https://cloud.google.com/java/docs/reference/google-cloud-datastore/latest/history) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
Query<Entity> query =
    Query.newEntityQueryBuilder()
        .setKind("Task")
        .setFilter(PropertyFilter.eq("done", false))
        .build();
```

### Node.js

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Node.js API reference documentation](https://cloud.google.com/nodejs/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` javascript
const query = datastore
  .createQuery('Task')
  .filter(new PropertyFilter('done', '=', false));
```

### PHP

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore PHP API reference documentation](https://googleapis.github.io/google-cloud-php/#/docs/cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
$query = $datastore->query()
    ->kind('Task')
    ->filter('done', '=', false);
```

### Python

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Python API reference documentation](https://cloud.google.com/python/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
from google.cloud import datastore

# For help authenticating your client, visit
# https://cloud.google.com/docs/authentication/getting-started
client = datastore.Client()

query = client.query(kind="Task")
query.add_filter(filter=datastore.query.PropertyFilter("done", "=", False))
```

### Ruby

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Ruby API reference documentation](/ruby/docs/reference/google-cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
query = datastore.query("Task")
                 .where("done", "=", false)
```

### GQL

``` text
SELECT * FROM Task WHERE done = FALSE
```

The property value must be supplied by the application; it cannot refer to or be calculated in terms of other properties. An entity satisfies the filter if it has a property of the given name whose value compares to the value specified in the filter in the manner described by the comparison operator. If the property of the given name is array-valued, the entity satisfies the filter if any of the values compares to the value specified in the filter in the manner described by the comparison operator.

The comparison operator can be any of the following:

<table>
<thead>
<tr class="header">
<th>Operator</th>
<th>Meaning</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       EQUAL      </code></td>
<td>Equal to</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       LESS_THAN      </code></td>
<td>Less than</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       LESS_THAN_OR_EQUAL      </code></td>
<td>Less than or equal to</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       GREATER_THAN      </code></td>
<td>Greater than</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       GREATER_THAN_OR_EQUAL      </code></td>
<td>Greater than or equal to</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       NOT_EQUAL      </code></td>
<td>Not equal to</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       IN      </code></td>
<td>Member of the specified list. Equal to any of the values in a specified list.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       NOT_IN      </code></td>
<td>Not a member of the specified list. Not equal to any of the values in a specified list.</td>
</tr>
</tbody>
</table>

#### Composite filters

A *composite filter* consists of more than one property filter. You can combine filters with `  AND  ` and `  OR  ` . The following example returns `  Task  ` entities that are marked not done and have a priority of 4:

### C\#

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore C\# API reference documentation](https://cloud.google.com/dotnet/docs/reference/Google.Cloud.Datastore.V1/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
Query query = new Query("Task")
{
    Filter = Filter.And(Filter.Equal("done", false),
        Filter.Equal("priority", 4)),
};
```

### Go

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Go API reference documentation](https://cloud.google.com/go/docs/reference/cloud.google.com/go/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` go
query := datastore.NewQuery("Task").
 FilterField("Done", "=", false).
 FilterField("Priority", "=", 4)
```

### Java

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Java API reference documentation](https://cloud.google.com/java/docs/reference/google-cloud-datastore/latest/history) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
Query<Entity> query =
    Query.newEntityQueryBuilder()
        .setKind("Task")
        .setFilter(
            CompositeFilter.and(
                PropertyFilter.eq("done", false), PropertyFilter.eq("priority", 4)))
        .build();
```

### Node.js

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Node.js API reference documentation](https://cloud.google.com/nodejs/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` javascript
const query = datastore
  .createQuery('Task')
  .filter(
    and([
      new PropertyFilter('done', '=', false),
      new PropertyFilter('priority', '=', 4),
    ]),
  );
```

### PHP

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore PHP API reference documentation](https://googleapis.github.io/google-cloud-php/#/docs/cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
$query = $datastore->query()
    ->kind('Task')
    ->filter('done', '=', false)
    ->filter('priority', '=', 4);
```

### Python

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Python API reference documentation](https://cloud.google.com/python/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
from google.cloud import datastore

# For help authenticating your client, visit
# https://cloud.google.com/docs/authentication/getting-started
client = datastore.Client()

query = client.query(kind="Task")
query.add_filter(filter=datastore.query.PropertyFilter("done", "=", False))
query.add_filter(filter=datastore.query.PropertyFilter("priority", "=", 4))
```

### Ruby

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Ruby API reference documentation](/ruby/docs/reference/google-cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
query = datastore.query("Task")
                 .where("done", "=", false)
                 .where("priority", "=", 4)
```

### GQL

``` text
SELECT * FROM Task WHERE done = FALSE AND priority = 4
```

The following example combines filters with a logical `  OR  ` :

##### C\#

Snippet not available.

##### Go

Snippet not available.

### Java

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Java API reference documentation](https://cloud.google.com/java/docs/reference/google-cloud-datastore/latest/history) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
import com.google.cloud.datastore.Datastore;
import com.google.cloud.datastore.DatastoreOptions;
import com.google.cloud.datastore.Entity;
import com.google.cloud.datastore.Query;
import com.google.cloud.datastore.QueryResults;
import com.google.cloud.datastore.StructuredQuery.CompositeFilter;
import com.google.cloud.datastore.StructuredQuery.Filter;
import com.google.cloud.datastore.StructuredQuery.PropertyFilter;

public class OrFilterQuery {
  public static void invoke() throws Exception {

    // Instantiates a client
    Datastore datastore = DatastoreOptions.getDefaultInstance().getService();
    String propertyName = "description";

    // Create the two filters
    Filter orFilter =
        CompositeFilter.or(
            PropertyFilter.eq(propertyName, "Feed cats"),
            PropertyFilter.eq(propertyName, "Buy milk"));

    // Build the query
    Query<Entity> query = Query.newEntityQueryBuilder().setKind("Task").setFilter(orFilter).build();

    // Get the results back from Datastore
    QueryResults<Entity> results = datastore.run(query);

    if (!results.hasNext()) {
      throw new Exception("query yielded no results");
    }

    while (results.hasNext()) {
      Entity entity = results.next();
      System.out.printf("Entity: %s%n", entity);
    }
  }
}
```

### Node.js

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Node.js API reference documentation](https://cloud.google.com/nodejs/docs/reference/datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` javascript
/**
 * TODO(developer): Uncomment these variables before running the sample.
 */
// const projectId = "your Google Cloud project id";

// Imports the Cloud Datastore
const {Datastore, PropertyFilter, or} = require('@google-cloud/datastore');

async function queryFilterOr() {
  // Instantiate the Datastore
  const datastore = new Datastore();
  const query = datastore
    .createQuery('Task')
    .filter(
      or([
        new PropertyFilter('description', '=', 'Buy milk'),
        new PropertyFilter('description', '=', 'Feed cats'),
      ]),
    );

  const [entities] = await datastore.runQuery(query);
  for (const entity of entities) {
    console.log(`Entity found: ${entity['description']}`);
  }
}

queryFilterOr();
```

##### PHP

Snippet not available.

### Python

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Python API reference documentation](https://cloud.google.com/python/docs/reference/datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
from google.cloud import datastore
from google.cloud.datastore import query


def query_filter_or(project_id: str) -> None:
    """Builds a union of two queries (OR) filter.

    Arguments:
        project_id: your Google Cloud Project ID
    """
    client = datastore.Client(project=project_id)

    or_query = client.query(kind="Task")
    or_filter = query.Or(
        [
            query.PropertyFilter("description", "=", "Buy milk"),
            query.PropertyFilter("description", "=", "Feed cats"),
        ]
    )

    or_query.add_filter(filter=or_filter)

    results = list(or_query.fetch())
    for result in results:
        print(result["description"])
```

##### Ruby

Snippet not available.

##### GQL

Snippet not available.

Firestore in Datastore mode supports combining filters with `  AND  ` and `  OR  ` operators. The following example returns `  Task  ` entities that are either starred or that are marked not done and have a priority of 4:

##### C\#

Snippet not available.

##### Go

Snippet not available.

##### Java

``` text
Query<Entity> query =
    Query.newEntityQueryBuilder()
        .setKind("Task")
        .setFilter(CompositeFilter.or(
            PropertyFilter.eq("starred", true)),
            CompositeFilter.and(
                PropertyFilter.eq("done", false),
                PropertyFilter.eq("priority", 4)))
        .build();
```

##### Node.js

Snippet not available.

##### PHP

Snippet not available.

##### Python

``` text
and_or_query = client.query(kind="Task")

query_filter = query.Or(
    [
        query.PropertyFilter("starred", "=", True),
        query.And([query.PropertyFilter("done", "=", False),
                    query.PropertyFilter("priority", "=", 4,),
        ]
        )
    ]
)

and_or_query.add_filter(filter=query_filter)

results = and_or_query.fetch()
for result in results:
    print(result["description"])
```

##### Ruby

Snippet not available.

##### GQL

Snippet not available.

#### Key filters

To filter on the value of an entity's key, use the special property `  __key__  ` :

### C\#

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore C\# API reference documentation](https://cloud.google.com/dotnet/docs/reference/Google.Cloud.Datastore.V1/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
Query query = new Query("Task")
{
    Filter = Filter.GreaterThan("__key__", _keyFactory.CreateKey("aTask"))
};
```

### Go

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Go API reference documentation](https://cloud.google.com/go/docs/reference/cloud.google.com/go/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` go
key := datastore.NameKey("Task", "someTask", nil)
query := datastore.NewQuery("Task").FilterField("__key__", ">", key)
```

### Java

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Java API reference documentation](https://cloud.google.com/java/docs/reference/google-cloud-datastore/latest/history) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
Query<Entity> query =
    Query.newEntityQueryBuilder()
        .setKind("Task")
        .setFilter(PropertyFilter.gt("__key__", keyFactory.newKey("someTask")))
        .build();
```

### Node.js

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Node.js API reference documentation](https://cloud.google.com/nodejs/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` javascript
const query = datastore
  .createQuery('Task')
  .filter(
    new PropertyFilter('__key__', '>', datastore.key(['Task', 'someTask'])),
  );
```

### PHP

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore PHP API reference documentation](https://googleapis.github.io/google-cloud-php/#/docs/cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
$query = $datastore->query()
    ->kind('Task')
    ->filter('__key__', '>', $datastore->key('Task', 'someTask'));
```

### Python

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Python API reference documentation](https://cloud.google.com/python/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
from google.cloud import datastore

# For help authenticating your client, visit
# https://cloud.google.com/docs/authentication/getting-started
client = datastore.Client()

query = client.query(kind="Task")
first_key = client.key("Task", "first_task")
# key_filter(key, op) translates to add_filter('__key__', op, key).
query.key_filter(first_key, ">")
```

### Ruby

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Ruby API reference documentation](/ruby/docs/reference/google-cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
query = datastore.query("Task")
                 .where("__key__", ">", datastore.key("Task", "someTask"))
```

### GQL

``` text
SELECT * FROM Task WHERE __key__ > KEY(Task, 'someTask')
```

When comparing for inequality, keys are ordered by the following criteria, in order:

1.  Ancestor path
2.  Entity kind
3.  Identifier (key name or numeric ID)

Elements of the ancestor path are compared similarly: by kind (string), then by key name or numeric ID. Kinds and key names are strings and are ordered by byte value; numeric IDs are integers and are ordered numerically. If entities with the same parent and kind use a mix of key name strings and numeric IDs, those with numeric IDs precede those with key names.

Queries on keys use indexes just like queries on properties and require custom indexes in the same cases. The following exceptions don't require a custom index:

  - Inequality filters
  - Ascending sort order on the key

A descending sort order on the key requires a custom index. As with all queries, the development server creates appropriate entries in the [index configuration file](/datastore/docs/concepts/indexes#index_configuration) when a query that needs a custom index is used in the development environment.

### Sort orders

A query *sort order* specifies the following:

  - A property name.
  - A sort direction (ascending or descending). By default the sort order is ascending.

This example sorts Task entities by creation time in ascending order:

### C\#

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore C\# API reference documentation](https://cloud.google.com/dotnet/docs/reference/Google.Cloud.Datastore.V1/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
Query query = new Query("Task")
{
    Order = { { "created", PropertyOrder.Types.Direction.Ascending } }
};
```

### Go

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Go API reference documentation](https://cloud.google.com/go/docs/reference/cloud.google.com/go/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` go
query := datastore.NewQuery("Task").Order("created")
```

### Java

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Java API reference documentation](https://cloud.google.com/java/docs/reference/google-cloud-datastore/latest/history) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
Query<Entity> query =
    Query.newEntityQueryBuilder().setKind("Task").setOrderBy(OrderBy.asc("created")).build();
```

### Node.js

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Node.js API reference documentation](https://cloud.google.com/nodejs/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` javascript
const query = datastore.createQuery('Task').order('created');
```

### PHP

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore PHP API reference documentation](https://googleapis.github.io/google-cloud-php/#/docs/cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
$query = $datastore->query()
    ->kind('Task')
    ->order('created');
```

### Python

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Python API reference documentation](https://cloud.google.com/python/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
from google.cloud import datastore

# For help authenticating your client, visit
# https://cloud.google.com/docs/authentication/getting-started
client = datastore.Client()

query = client.query(kind="Task")
query.order = ["created"]
```

### Ruby

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Ruby API reference documentation](/ruby/docs/reference/google-cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
query = datastore.query("Task")
                 .order("created", :asc)
```

### GQL

``` text
SELECT * FROM Task ORDER BY created ASC
```

This example sorts Task entities by creation time in descending order:

### C\#

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore C\# API reference documentation](https://cloud.google.com/dotnet/docs/reference/Google.Cloud.Datastore.V1/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
Query query = new Query("Task")
{
    Order = { { "created", PropertyOrder.Types.Direction.Descending } }
};
```

### Go

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Go API reference documentation](https://cloud.google.com/go/docs/reference/cloud.google.com/go/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` go
query := datastore.NewQuery("Task").Order("-created")
```

### Java

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Java API reference documentation](https://cloud.google.com/java/docs/reference/google-cloud-datastore/latest/history) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
Query<Entity> query =
    Query.newEntityQueryBuilder().setKind("Task").setOrderBy(OrderBy.desc("created")).build();
```

### Node.js

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Node.js API reference documentation](https://cloud.google.com/nodejs/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` javascript
const query = datastore.createQuery('Task').order('created', {
  descending: true,
});
```

### PHP

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore PHP API reference documentation](https://googleapis.github.io/google-cloud-php/#/docs/cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
$query = $datastore->query()
    ->kind('Task')
    ->order('created', Query::ORDER_DESCENDING);
```

### Python

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Python API reference documentation](https://cloud.google.com/python/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
from google.cloud import datastore

# For help authenticating your client, visit
# https://cloud.google.com/docs/authentication/getting-started
client = datastore.Client()

query = client.query(kind="Task")
query.order = ["-created"]
```

### Ruby

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Ruby API reference documentation](/ruby/docs/reference/google-cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
query = datastore.query("Task")
                 .order("created", :desc)
```

### GQL

``` text
SELECT * FROM Task ORDER BY created DESC
```

If a query includes multiple sort orders, they are applied in the sequence specified. The following example sorts first by descending priority and then by ascending creation time:

### C\#

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore C\# API reference documentation](https://cloud.google.com/dotnet/docs/reference/Google.Cloud.Datastore.V1/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
Query query = new Query("Task")
{
    Order = { { "priority", PropertyOrder.Types.Direction.Descending },
        { "created", PropertyOrder.Types.Direction.Ascending } }
};
```

### Go

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Go API reference documentation](https://cloud.google.com/go/docs/reference/cloud.google.com/go/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` go
query := datastore.NewQuery("Task").Order("-priority").Order("created")
```

### Java

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Java API reference documentation](https://cloud.google.com/java/docs/reference/google-cloud-datastore/latest/history) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
Query<Entity> query =
    Query.newEntityQueryBuilder()
        .setKind("Task")
        .setOrderBy(OrderBy.desc("priority"), OrderBy.asc("created"))
        .build();
```

### Node.js

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Node.js API reference documentation](https://cloud.google.com/nodejs/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` javascript
const query = datastore
  .createQuery('Task')
  .order('priority', {
    descending: true,
  })
  .order('created');
```

### PHP

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore PHP API reference documentation](https://googleapis.github.io/google-cloud-php/#/docs/cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
$query = $datastore->query()
    ->kind('Task')
    ->order('priority', Query::ORDER_DESCENDING)
    ->order('created');
```

### Python

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Python API reference documentation](https://cloud.google.com/python/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
from google.cloud import datastore

# For help authenticating your client, visit
# https://cloud.google.com/docs/authentication/getting-started
client = datastore.Client()

query = client.query(kind="Task")
query.order = ["-priority", "created"]
```

### Ruby

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Ruby API reference documentation](/ruby/docs/reference/google-cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
query = datastore.query("Task")
                 .order("priority", :desc)
                 .order("created", :asc)
```

### GQL

``` text
SELECT * FROM Task ORDER BY priority DESC, created ASC
```

If no sort orders are specified, the results are returned in the order they are retrieved from Datastore mode.

#### Restrictions

*Sort orders* have the following restrictions:

  - Because of the way Datastore mode executes queries, if a query specifies inequality filters on a property and *sort orders* on other properties, [the property used in the inequality filters must be ordered before the other properties](#properties_used_in_inequality_filters_must_be_sorted_first) .
  - If ordering is specified, the set of properties specified in the `  distinct on  ` clause must appear before any non- `  distinct on  ` properties in the *sort orders* . For more information, see [grouping queries](#grouping) .
  - [Sort orders on properties with equality filters are all ignored](#sort_orders_are_ignored_on_properties_with_equality_filters) .

## Special query types

Some specific types of query deserve special mention:

### `     != Not equal    `

Use the not-equal ( `  !=  ` ) operator to return entities where the given property exists and doesn't match the comparison value.

### C\#

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore C\# API reference documentation](https://cloud.google.com/dotnet/docs/reference/Google.Cloud.Datastore.V1/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

Not Applicable

### Go

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Go API reference documentation](https://cloud.google.com/go/docs/reference/cloud.google.com/go/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` go
package datastore_snippets

import (
 "context"
 "fmt"
 "io"

 "cloud.google.com/go/datastore"
 "google.golang.org/api/iterator"
)

func queryNotEquals(w io.Writer, projectId string) error {
 ctx := context.Background()
 client, err := datastore.NewClient(ctx, projectId)
 if err != nil {
     return fmt.Errorf("NewClient: %w", err)
 }
 defer client.Close()

 q := datastore.NewQuery("TaskList")
 q.FilterField("Task", "!=", []string{"notASimpleTask"})

 it := client.Run(ctx, q)
 for {
     var dst struct {
         Task string
     }
     key, err := it.Next(&dst)
     if err == iterator.Done {
         break
     }

     if err != nil {
         return err
     }
     fmt.Fprintf(w, "Key retrieved: %v\n", key)
 }

 return nil
}
```

### Java

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Java API reference documentation](https://cloud.google.com/java/docs/reference/google-cloud-datastore/latest/history) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
Query<Entity> query =
    Query.newEntityQueryBuilder()
        .setKind("Task")
        .setFilter(PropertyFilter.neq("category", "Work"))
        .build();
```

### Node.js

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Node.js API reference documentation](https://cloud.google.com/nodejs/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

Not Applicable

### PHP

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore PHP API reference documentation](https://googleapis.github.io/google-cloud-php/#/docs/cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

Not Applicable

### Python

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Python API reference documentation](https://cloud.google.com/python/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
query = client.query(kind="Task")
query.add_filter("category", "!=", "work")
```

### Ruby

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Ruby API reference documentation](/ruby/docs/reference/google-cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

Not Applicable

### GQL

``` text
SELECT * FROM Task WHERE category != 'work'
```

This query returns every `  Task  ` entity where the `  category  ` property exists and is set to any value other than `  Work  ` .

This query doesn't return entities where the `  category  ` property doesn't exist. Not-equal ( `  !=  ` ) and `  NOT_IN  ` queries exclude entities where the given property doesn't exist or where the property is excluded from indexing. A property exists when it's set to any value, including an empty string or `  null  ` .

**Note:** This features is available for Firestore in Datastore mode. It is not available for pre-migration [Datastore databases](/datastore/docs/upgrade-to-firestore) .

#### Limitations

Note the following limitations for `  !=  ` queries:

  - Only entities where the given property exists can match the query.
  - Only a single `  NOT_IN  ` or `  !=  ` is allowed per query.

### `     IN    `

Use the `  IN  ` operator to combine up to 30 equality ( `  ==  ` ) clauses on the same property with a logical `  OR  ` . An `  IN  ` query returns entities where the given property matches any of the comparison values.

### C\#

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore C\# API reference documentation](https://cloud.google.com/dotnet/docs/reference/Google.Cloud.Datastore.V1/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

Not Applicable

### Go

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Go API reference documentation](https://cloud.google.com/go/docs/reference/cloud.google.com/go/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` go
package datastore_snippets

import (
 "context"
 "fmt"
 "io"

 "cloud.google.com/go/datastore"
 "google.golang.org/api/iterator"
)

func queryIn(w io.Writer, projectId string) error {
 ctx := context.Background()
 client, err := datastore.NewClient(ctx, projectId)
 if err != nil {
     return fmt.Errorf("NewClient: %w", err)
 }
 defer client.Close()

 q := datastore.NewQuery("TaskList")
 q.FilterField("Task", "in", []string{"simpleTask", "easyTask"})

 it := client.Run(ctx, q)
 for {
     var dst struct {
         Task string
     }
     key, err := it.Next(&dst)
     if err == iterator.Done {
         break
     }

     if err != nil {
         return err
     }
     fmt.Fprintf(w, "Key retrieved: %v\n", key)
 }

 return nil
}
```

### Java

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Java API reference documentation](https://cloud.google.com/java/docs/reference/google-cloud-datastore/latest/history) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
Query<Entity> query =
    Query.newEntityQueryBuilder()
        .setKind("Task")
        .setFilter(PropertyFilter.in("tag", ListValue.of("learn", "study")))
        .build();
```

### Node.js

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Node.js API reference documentation](https://cloud.google.com/nodejs/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

Not Applicable

### PHP

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore PHP API reference documentation](https://googleapis.github.io/google-cloud-php/#/docs/cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

Not Applicable

### Python

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Python API reference documentation](https://cloud.google.com/python/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
query = client.query(kind="Task")
query.add_filter("tag", "IN", ["learn", "study"])
```

### Ruby

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Ruby API reference documentation](/ruby/docs/reference/google-cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

Not Applicable

### GQL

``` text
SELECT * FROM Task WHERE tag IN ARRAY('learn', 'study')
```

This query returns every `  Task  ` entity where the `  tag  ` property is set to `  learn  ` or `  study  ` . This includes `  Task  ` entities where the `  tag  ` property includes one of these values but not the other.

**Note:** This features is available for Firestore in Datastore mode. It is not available for pre-migration [Datastore databases](/datastore/docs/upgrade-to-firestore) .

### `     NOT_IN    `

Use the `  NOT_IN  ` operator to combine up to 10 not-equal ( `  !=  ` ) clauses on the same property with a logical `  AND  ` . A `  NOT_IN  ` query returns entities where the given property exists and doesn't match any of the comparison values.

### C\#

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore C\# API reference documentation](https://cloud.google.com/dotnet/docs/reference/Google.Cloud.Datastore.V1/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

Not Applicable

### Go

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Go API reference documentation](https://cloud.google.com/go/docs/reference/cloud.google.com/go/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` go
package datastore_snippets

import (
 "context"
 "fmt"
 "io"

 "cloud.google.com/go/datastore"
 "google.golang.org/api/iterator"
)

func queryNotIn(w io.Writer, projectId string) error {
 ctx := context.Background()
 client, err := datastore.NewClient(ctx, projectId)
 if err != nil {
     return fmt.Errorf("NewClient: %w", err)
 }
 defer client.Close()

 q := datastore.NewQuery("TaskList")
 q.FilterField("Task", "not-in", []string{"notASimpleTask", "notAnEasyTask"})

 it := client.Run(ctx, q)
 for {
     var dst struct {
         Task string
     }
     key, err := it.Next(&dst)
     if err == iterator.Done {
         break
     }

     if err != nil {
         return err
     }
     fmt.Fprintf(w, "Key retrieved: %v\n", key)
 }

 return nil
}
```

### Java

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Java API reference documentation](https://cloud.google.com/java/docs/reference/google-cloud-datastore/latest/history) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
Query<Entity> query =
    Query.newEntityQueryBuilder()
        .setKind("Task")
        .setFilter(PropertyFilter.not_in("category", ListValue.of("Work", "Chores", "School")))
        .build();
```

### Node.js

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Node.js API reference documentation](https://cloud.google.com/nodejs/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

Not Applicable

### PHP

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore PHP API reference documentation](https://googleapis.github.io/google-cloud-php/#/docs/cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

Not Applicable

### Python

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Python API reference documentation](https://cloud.google.com/python/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
query = client.query(kind="Task")
query.add_filter("category", "NOT_IN", ["work", "chores", "school"])
```

### Ruby

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Ruby API reference documentation](/ruby/docs/reference/google-cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

Not Applicable

### GQL

``` text
SELECT * FROM Task WHERE category NOT IN ARRAY('work', 'chores', 'school')
```

This query doesn't return entities where the `  category  ` entity doesn't exist. Not-equal ( `  !=  ` ) and `  NOT_IN  ` queries exclude entities where the given property doesn't exist. A property exists when it's set to any value, including an empty string or `  null  ` .

**Note:** This features is available for Firestore in Datastore mode. It is not available for pre-migration [Datastore databases](/datastore/docs/upgrade-to-firestore) .

#### Limitations

Note the following limitations for `  NOT_IN  ` queries:

  - Only entities where the given property exists can match the query.
  - Only a single `  NOT_IN  ` or `  !=  ` is allowed per query.

### Ancestor queries

An ancestor query limits its results to the specified entity and its descendants. This example returns all Task entities that have the specified TaskList entity as an ancestor:

### C\#

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore C\# API reference documentation](https://cloud.google.com/dotnet/docs/reference/Google.Cloud.Datastore.V1/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
Query query = new Query("Task")
{
    Filter = Filter.HasAncestor(_db.CreateKeyFactory("TaskList")
        .CreateKey(keyName))
};
```

### Go

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Go API reference documentation](https://cloud.google.com/go/docs/reference/cloud.google.com/go/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` go
ancestor := datastore.NameKey("TaskList", "default", nil)
query := datastore.NewQuery("Task").Ancestor(ancestor)
```

### Java

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Java API reference documentation](https://cloud.google.com/java/docs/reference/google-cloud-datastore/latest/history) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
Query<Entity> query =
    Query.newEntityQueryBuilder()
        .setKind("Task")
        .setFilter(
            PropertyFilter.hasAncestor(
                datastore.newKeyFactory().setKind("TaskList").newKey("default")))
        .build();
```

### Node.js

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Node.js API reference documentation](https://cloud.google.com/nodejs/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` javascript
const ancestorKey = datastore.key(['TaskList', 'default']);

const query = datastore.createQuery('Task').hasAncestor(ancestorKey);
```

### PHP

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore PHP API reference documentation](https://googleapis.github.io/google-cloud-php/#/docs/cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
$ancestorKey = $datastore->key('TaskList', 'default');
$query = $datastore->query()
    ->kind('Task')
    ->hasAncestor($ancestorKey);
```

### Python

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Python API reference documentation](https://cloud.google.com/python/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
from google.cloud import datastore

# For help authenticating your client, visit
# https://cloud.google.com/docs/authentication/getting-started
client = datastore.Client()

# Query filters are omitted in this example as any ancestor queries with a
# non-key filter require a composite index.
ancestor = client.key("TaskList", "default")
query = client.query(kind="Task", ancestor=ancestor)
```

### Ruby

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Ruby API reference documentation](/ruby/docs/reference/google-cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
# task_list_name = "default"
ancestor_key = datastore.key "TaskList", task_list_name

query = datastore.query("Task")
                 .ancestor(ancestor_key)
```

### GQL

``` text
SELECT * FROM Task WHERE __key__ HAS ANCESTOR KEY(TaskList, 'default')
```

#### Limitations on Ancestor queries

Note the following limitations for `  Ancestor  ` queries:

  - All evaluated disjunctions must have the same ancestor filter.

### Kindless queries

A query with no kind and no ancestor retrieves all of the entities of an application from Datastore mode. Such *kindless queries* cannot include filters or sort orders on property values. They can, however, filter on entity keys and use ancestor filters. Key filters can be used by specifying `  __key__  ` as the property name:

### C\#

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore C\# API reference documentation](https://cloud.google.com/dotnet/docs/reference/Google.Cloud.Datastore.V1/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
Query query = new Query()
{
    Filter = Filter.GreaterThan("__key__",
        _keyFactory.CreateKey("aTask"))
};
```

### Go

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Go API reference documentation](https://cloud.google.com/go/docs/reference/cloud.google.com/go/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` go
query := datastore.NewQuery("").FilterField("__key__", ">", lastSeenKey)
```

### Java

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Java API reference documentation](https://cloud.google.com/java/docs/reference/google-cloud-datastore/latest/history) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
Query<Entity> query =
    Query.newEntityQueryBuilder().setFilter(PropertyFilter.gt("__key__", lastSeenKey)).build();
```

### Node.js

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Node.js API reference documentation](https://cloud.google.com/nodejs/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` javascript
const query = datastore
  .createQuery()
  .filter(new PropertyFilter('__key__', '>', lastSeenKey))
  .limit(1);
```

### PHP

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore PHP API reference documentation](https://googleapis.github.io/google-cloud-php/#/docs/cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
$query = $datastore->query()
    ->filter('__key__', '>', $lastSeenKey);
```

### Python

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Python API reference documentation](https://cloud.google.com/python/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
from google.cloud import datastore

# For help authenticating your client, visit
# https://cloud.google.com/docs/authentication/getting-started
client = datastore.Client()

last_seen_key = client.key("Task", "a")
query = client.query()
query.key_filter(last_seen_key, ">")
```

### Ruby

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Ruby API reference documentation](/ruby/docs/reference/google-cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
query = Google::Cloud::Datastore::Query.new
query.where "__key__", ">", last_seen_key
```

### GQL

``` text
SELECT * WHERE __key__ > KEY(Task, 'someTask')
```

### Projection queries

Most queries return whole entities as their results, but often an application is actually interested in only a few of the entity's properties. *Projection queries* allow you to query for just those specific properties of an entity that you actually need, at lower latency and cost than retrieving the entire entity.

Projection queries require the specified properties to be indexed.

#### Keys-only queries

A *keys-only query* (which is a type of projection query) returns just the keys of the result entities instead of the entities themselves, at lower latency and cost than retrieving entire entities.

It is often more economical to do a keys-only query first, and then fetch a subset of entities from the results, rather than executing a general query which may fetch more entities than you actually need.

Here's how to create a keys-only query:

### C\#

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore C\# API reference documentation](https://cloud.google.com/dotnet/docs/reference/Google.Cloud.Datastore.V1/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
Query query = new Query("Task")
{
    Projection = { "__key__" }
};
```

### Go

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Go API reference documentation](https://cloud.google.com/go/docs/reference/cloud.google.com/go/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` go
query := datastore.NewQuery("Task").KeysOnly()
```

### Java

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Java API reference documentation](https://cloud.google.com/java/docs/reference/google-cloud-datastore/latest/history) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
Query<Key> query = Query.newKeyQueryBuilder().setKind("Task").build();
```

### Node.js

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Node.js API reference documentation](https://cloud.google.com/nodejs/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` javascript
const query = datastore.createQuery().select('__key__').limit(1);
```

### PHP

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore PHP API reference documentation](https://googleapis.github.io/google-cloud-php/#/docs/cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
$query = $datastore->query()
    ->keysOnly();
```

### Python

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Python API reference documentation](https://cloud.google.com/python/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
from google.cloud import datastore

# For help authenticating your client, visit
# https://cloud.google.com/docs/authentication/getting-started
client = datastore.Client()

query = client.query()
query.keys_only()
```

### Ruby

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Ruby API reference documentation](/ruby/docs/reference/google-cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
query = datastore.query("Task")
                 .select("__key__")
```

### GQL

``` text
SELECT __key__ FROM Task
```

A keys-only query is a small operation and counts as only a single entity read for the query itself.

#### Projections

Projection queries are similar to SQL queries of the form:

``` text
SELECT priority, percent_complete FROM Task
```

You can use all of the filtering and sorting features available for standard entity queries, but note [these limitations](#limitations_on_projections) .

The example SQL query returns abridged results with only the specified properties, `  priority  ` and `  percent_complete  ` , populated with values; all other properties are not populated. Here's how you construct this as a projection query:

### C\#

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore C\# API reference documentation](https://cloud.google.com/dotnet/docs/reference/Google.Cloud.Datastore.V1/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
Query query = new Query("Task")
{
    Projection = { "priority", "percent_complete" }
};
```

### Go

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Go API reference documentation](https://cloud.google.com/go/docs/reference/cloud.google.com/go/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` go
query := datastore.NewQuery("Task").Project("Priority", "PercentComplete")
```

### Java

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Java API reference documentation](https://cloud.google.com/java/docs/reference/google-cloud-datastore/latest/history) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
Query<ProjectionEntity> query =
    Query.newProjectionEntityQueryBuilder()
        .setKind("Task")
        .setProjection("priority", "percent_complete")
        .build();
```

### Node.js

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Node.js API reference documentation](https://cloud.google.com/nodejs/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` javascript
const query = datastore
  .createQuery('Task')
  .select(['priority', 'percent_complete']);
```

### PHP

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore PHP API reference documentation](https://googleapis.github.io/google-cloud-php/#/docs/cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
$query = $datastore->query()
    ->kind('Task')
    ->projection(['priority', 'percent_complete']);
```

### Python

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Python API reference documentation](https://cloud.google.com/python/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
from google.cloud import datastore

# For help authenticating your client, visit
# https://cloud.google.com/docs/authentication/getting-started
client = datastore.Client()

query = client.query(kind="Task")
query.projection = ["priority", "percent_complete"]
```

### Ruby

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Ruby API reference documentation](/ruby/docs/reference/google-cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
query = datastore.query("Task")
                 .select("priority", "percent_complete")
```

### GQL

``` text
SELECT priority, percent_complete FROM Task
```

And here's how to run the projection query:

### C\#

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore C\# API reference documentation](https://cloud.google.com/dotnet/docs/reference/Google.Cloud.Datastore.V1/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
Query query = new Query("Task")
{
    Projection = { "priority", "percent_complete" }
};
List<long> priorities = new List<long>();
List<double> percentCompletes = new List<double>();
foreach (var entity in _db.RunQuery(query).Entities)
{
    priorities.Add((long)entity["priority"]);
    percentCompletes.Add((double)entity["percent_complete"]);
}
```

### Go

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Go API reference documentation](https://cloud.google.com/go/docs/reference/cloud.google.com/go/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` go
var priorities []int
var percents []float64
it := client.Run(ctx, query)
for {
 var task Task
 if _, err := it.Next(&task); err == iterator.Done {
     break
 } else if err != nil {
     log.Fatal(err)
 }
 priorities = append(priorities, task.Priority)
 percents = append(percents, task.PercentComplete)
}
```

### Java

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Java API reference documentation](https://cloud.google.com/java/docs/reference/google-cloud-datastore/latest/history) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
List<Long> priorities = new LinkedList<>();
List<Double> percentCompletes = new LinkedList<>();
QueryResults<ProjectionEntity> tasks = datastore.run(query);
while (tasks.hasNext()) {
  ProjectionEntity task = tasks.next();
  priorities.add(task.getLong("priority"));
  percentCompletes.add(task.getDouble("percent_complete"));
}
```

### Node.js

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Node.js API reference documentation](https://cloud.google.com/nodejs/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` javascript
async function runProjectionQuery() {
  const priorities = [];
  const percentCompletes = [];
  const [tasks] = await datastore.runQuery(query);
  tasks.forEach(task => {
    priorities.push(task.priority);
    percentCompletes.push(task.percent_complete);
  });

  return {
    priorities: priorities,
    percentCompletes: percentCompletes,
  };
}
```

### PHP

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore PHP API reference documentation](https://googleapis.github.io/google-cloud-php/#/docs/cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
$priorities = array();
$percentCompletes = array();
$result = $datastore->runQuery($query);
/* @var Entity $task */
foreach ($result as $task) {
    $priorities[] = $task['priority'];
    $percentCompletes[] = $task['percent_complete'];
}
```

### Python

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Python API reference documentation](https://cloud.google.com/python/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
priorities = []
percent_completes = []

for task in query.fetch():
    priorities.append(task["priority"])
    percent_completes.append(task["percent_complete"])
```

### Ruby

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Ruby API reference documentation](/ruby/docs/reference/google-cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
priorities = []
percent_completes = []
datastore.run(query).each do |task|
  priorities << task["priority"]
  percent_completes << task["percent_complete"]
end
```

### GQL

Not Applicable

A projection query that doesn't use the [`  distinct on  `](#grouping) clause is a small operation and counts as only a single entity read for the query itself.

#### Grouping

Projection queries can use the `  distinct on  ` clause to ensure that only the first result for each distinct combination of values for the specified properties will be returned. This will return only the first result for entities which have the same values for the properties that are being projected.

### C\#

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore C\# API reference documentation](https://cloud.google.com/dotnet/docs/reference/Google.Cloud.Datastore.V1/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
Query query = new Query("Task")
{
    Projection = { "category", "priority" },
    DistinctOn = { "category" },
    Order = {
        { "category", PropertyOrder.Types.Direction.Ascending},
        {"priority", PropertyOrder.Types.Direction.Ascending }
    }
};
```

### Go

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Go API reference documentation](https://cloud.google.com/go/docs/reference/cloud.google.com/go/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` go
query := datastore.NewQuery("Task").
 Project("Priority", "Category").
 DistinctOn("Category").
 Order("Category").Order("Priority")
```

### Java

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Java API reference documentation](https://cloud.google.com/java/docs/reference/google-cloud-datastore/latest/history) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
Query<ProjectionEntity> query =
    Query.newProjectionEntityQueryBuilder()
        .setKind("Task")
        .setProjection("category", "priority")
        .setDistinctOn("category")
        .setOrderBy(OrderBy.asc("category"), OrderBy.asc("priority"))
        .build();
```

### Node.js

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Node.js API reference documentation](https://cloud.google.com/nodejs/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` javascript
const query = datastore
  .createQuery('Task')
  .groupBy('category')
  .order('category')
  .order('priority');
```

### PHP

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore PHP API reference documentation](https://googleapis.github.io/google-cloud-php/#/docs/cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
$query = $datastore->query()
    ->kind('Task')
    ->order('category')
    ->order('priority')
    ->projection(['category', 'priority'])
    ->distinctOn('category');
```

### Python

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Python API reference documentation](https://cloud.google.com/python/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
from google.cloud import datastore

# For help authenticating your client, visit
# https://cloud.google.com/docs/authentication/getting-started
client = datastore.Client()

query = client.query(kind="Task")
query.distinct_on = ["category"]
query.order = ["category", "priority"]
```

### Ruby

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Ruby API reference documentation](/ruby/docs/reference/google-cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
query = datastore.query("Task")
                 .select("category", "priority")
                 .distinct_on("category")
                 .order("category")
                 .order("priority")
```

### GQL

``` text
SELECT DISTINCT ON (category) category, priority FROM Task
ORDER BY category, priority
```

The set of properties specified in the `  distinct on  ` clause must appear before any non- `  distinct on  ` properties in the `  order by  ` clause if `  order by  ` is specified.

### Aggregation queries

Firestore in Datastore mode supports the `  count()  ` aggregation query. See [Aggregation queries](/datastore/docs/aggregation-queries) .

### Range and inequality filters on multiple properties

Firestore in Datastore mode supports multiple inequality filters in a compound query. See [Query using range and inequality filters on multiple properties](/datastore/docs/multiple-range-fields) .

## Array values

Datastore mode indexes each unique array property value once per index. Thus to query if an array contains a value use an equality filter.

Consider the following when your query includes properties with array values.

### Inequality Filters

Because of the way they're indexed, entities with multiple values for the same property can sometimes interact with query filters and sort orders in unexpected and surprising ways.

If a query has multiple inequality filters on a given property, an entity will match the query only if at least one of its individual values for the property satisfies *all* of the filters. For example, if an entity of kind `  Task  ` has values `  fun  ` and `  programming  ` for property `  tag  ` , it will *not* match the query:

### C\#

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore C\# API reference documentation](https://cloud.google.com/dotnet/docs/reference/Google.Cloud.Datastore.V1/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
Query query = new Query("Task")
{
    Filter = Filter.And(Filter.GreaterThan("tag", "learn"),
        Filter.LessThan("tag", "math"))
};
```

### Go

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Go API reference documentation](https://cloud.google.com/go/docs/reference/cloud.google.com/go/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` go
query := datastore.NewQuery("Task").
 FilterField("Tag", ">", "learn").
 FilterField("Tag", "<", "math")
```

### Java

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Java API reference documentation](https://cloud.google.com/java/docs/reference/google-cloud-datastore/latest/history) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
Query<Entity> query =
    Query.newEntityQueryBuilder()
        .setKind("Task")
        .setFilter(
            CompositeFilter.and(
                PropertyFilter.gt("tag", "learn"), PropertyFilter.lt("tag", "math")))
        .build();
```

### Node.js

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Node.js API reference documentation](https://cloud.google.com/nodejs/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` javascript
const query = datastore
  .createQuery('Task')
  .filter(
    and([
      new PropertyFilter('tag', '>', 'learn'),
      new PropertyFilter('tag', '<', 'math'),
    ]),
  );
```

### PHP

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore PHP API reference documentation](https://googleapis.github.io/google-cloud-php/#/docs/cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
$query = $datastore->query()
    ->kind('Task')
    ->filter('tag', '>', 'learn')
    ->filter('tag', '<', 'math');
```

### Python

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Python API reference documentation](https://cloud.google.com/python/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
from google.cloud import datastore

# For help authenticating your client, visit
# https://cloud.google.com/docs/authentication/getting-started
client = datastore.Client()

query = client.query(kind="Task")
query.add_filter(filter=datastore.query.PropertyFilter("tag", ">", "learn"))
query.add_filter(filter=datastore.query.PropertyFilter("tag", "<", "math"))
```

### Ruby

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Ruby API reference documentation](/ruby/docs/reference/google-cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
query = datastore.query("Task")
                 .where("tag", ">", "learn")
                 .where("tag", "<", "math")
```

### GQL

``` text
SELECT * FROM Task WHERE tag > 'learn' AND tag < 'math'
```

Each of the entity's `  tag  ` values satisfies one of the filters, but neither single value satisfies both.

### Multiple equality filters

Multiple equality filters can be used to query for entities that contain a set of values. For example, an entity of kind `  Task  ` with values `  fun  ` and `  programming  ` for property `  tag  ` *will* satisfy the query

### C\#

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore C\# API reference documentation](https://cloud.google.com/dotnet/docs/reference/Google.Cloud.Datastore.V1/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
Query query = new Query("Task")
{
    Filter = Filter.And(Filter.Equal("tag", "fun"),
        Filter.Equal("tag", "programming"))
};
```

### Go

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Go API reference documentation](https://cloud.google.com/go/docs/reference/cloud.google.com/go/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` go
query := datastore.NewQuery("Task").
 FilterField("Tag", "=", "fun").
 FilterField("Tag", "=", "programming")
```

### Java

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Java API reference documentation](https://cloud.google.com/java/docs/reference/google-cloud-datastore/latest/history) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
Query<Entity> query =
    Query.newEntityQueryBuilder()
        .setKind("Task")
        .setFilter(
            CompositeFilter.and(
                PropertyFilter.eq("tag", "fun"), PropertyFilter.eq("tag", "programming")))
        .build();
```

### Node.js

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Node.js API reference documentation](https://cloud.google.com/nodejs/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` javascript
const query = datastore
  .createQuery('Task')
  .filter(
    and([
      new PropertyFilter('tag', '=', 'fun'),
      new PropertyFilter('tag', '=', 'programming'),
    ]),
  );
```

### PHP

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore PHP API reference documentation](https://googleapis.github.io/google-cloud-php/#/docs/cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
$query = $datastore->query()
    ->kind('Task')
    ->filter('tag', '=', 'fun')
    ->filter('tag', '=', 'programming');
```

### Python

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Python API reference documentation](https://cloud.google.com/python/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
from google.cloud import datastore

# For help authenticating your client, visit
# https://cloud.google.com/docs/authentication/getting-started
client = datastore.Client()

query = client.query(kind="Task")
query.add_filter(filter=datastore.query.PropertyFilter("tag", "=", "fun"))
query.add_filter(filter=datastore.query.PropertyFilter("tag", "=", "programming"))
```

### Ruby

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Ruby API reference documentation](/ruby/docs/reference/google-cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
query = datastore.query("Task")
                 .where("tag", "=", "fun")
                 .where("tag", "=", "programming")
```

### GQL

``` text
SELECT * FROM Task WHERE tag = 'fun' AND tag = 'programming'
```

even though neither of the entity's individual `  tag  ` values satisfies both filter conditions.

### Sort Order

Similarly, the sort order for multiple-valued properties is unusual. Because such properties appear once in the index for each unique value, the first value seen in the index determines an entity's sort order.

If a multi-valued property is not used in any filter:

  - and the query results are sorted in ascending order by the property, the smallest value of the property is used for ordering.
  - and the query results are sorted in descending order by the property, the greatest value is used for ordering.
  - other values don't affect the sort order, nor does the number of values.

This has the unusual consequence that an entity with property values `  1  ` and `  9  ` precedes an entity with values `  4  ` , `  5  ` , `  6  ` , and `  7  ` in both ascending *and* descending order.

If a multi-valued property is used in an equality filter, [any sort order on that property is ignored](#sort_orders_are_ignored_on_properties_with_equality_filters) .

If a multi-valued property is used in an inequality or an `  NOT_IN  ` filter:

  - and the query results are sorted in ascending order by the property, the smallest value that satisfies all of the query's inequality filters is used for ordering.
  - and the query results are sorted in descending order by the property, the greatest value that satisfies all of the query's inequality filters is used for ordering.

Note that if a set of inequality filters on a property translate into an equality filter, such as

``` text
WHERE tag >= 'math' AND tag <= 'math'
```

any sort order on that property is ignored, as the filters evaluate the same as the equality filter

``` text
WHERE tag = 'math'
```

### Projections and array-valued properties

Projecting a property with array values won't populate all values for that property. Instead, a separate entity will be returned for each unique combination of projected values matching the query. For example, suppose you have an entity of kind `  Task  ` with two multiple-valued properties, `  tag  ` and `  collaborators  ` :

### C\#

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore C\# API reference documentation](https://cloud.google.com/dotnet/docs/reference/Google.Cloud.Datastore.V1/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
Entity task = new Entity()
{
    Key = _db.CreateKeyFactory("Task").CreateKey("sampleTask"),
    ["collaborators"] = new ArrayValue() { Values = { "alice", "bob" } },
    ["tags"] = new ArrayValue() { Values = { "fun", "programming" } }
};
```

### Go

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Go API reference documentation](https://cloud.google.com/go/docs/reference/cloud.google.com/go/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` go
type Task struct {
 Tags          []string
 Collaborators []string
}
task := &Task{
 Tags:          []string{"fun", "programming"},
 Collaborators: []string{"alice", "bob"},
}
```

### Java

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Java API reference documentation](https://cloud.google.com/java/docs/reference/google-cloud-datastore/latest/history) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
Entity task =
    Entity.newBuilder(taskKey)
        .set("tags", "fun", "programming")
        .set("collaborators", ListValue.of("alice", "bob"))
        .build();
```

### Node.js

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Node.js API reference documentation](https://cloud.google.com/nodejs/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` javascript
const task = {
  tags: ['fun', 'programming'],
  collaborators: ['alice', 'bob'],
};
```

### PHP

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore PHP API reference documentation](https://googleapis.github.io/google-cloud-php/#/docs/cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
$task = $datastore->entity(
    $key,
    [
        'tags' => ['fun', 'programming'],
        'collaborators' => ['alice', 'bob']
    ]
);
```

### Python

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Python API reference documentation](https://cloud.google.com/python/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
from google.cloud import datastore

# For help authenticating your client, visit
# https://cloud.google.com/docs/authentication/getting-started
client = datastore.Client()

key = client.key("Task")
task = datastore.Entity(key)
task.update({"tags": ["fun", "programming"], "collaborators": ["alice", "bob"]})
```

### Ruby

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Ruby API reference documentation](/ruby/docs/reference/google-cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
# task_name = "sampleTask"
task = datastore.entity "Task", task_name do |t|
  t["tags"] = ["fun", "programming"]
  t["collaborators"] = ["alice", "bob"]
end
```

### GQL

Not Applicable

Then the projection query

``` text
SELECT tag, collaborators FROM Task WHERE collaborators < 'charlie'
```

will return four entities with the following combinations of values:

`  tag  ` = `  'fun'  ` , `  collaborators  ` = `  'alice'  `  
`  tag  ` = `  'fun'  ` , `  collaborators  ` = `  'bob'  `  
`  tag  ` = `  'programming'  ` , `  collaborators  ` = `  'alice'  `  
`  tag  ` = `  'programming'  ` , `  collaborators  ` = `  'bob'  `

**Warning:** Including more than one array-valued property in a projection will result in an [exploding index](/datastore/docs/concepts/indexes#index_limits) .

## Cursors, limits, and offsets

You can specify a *limit* for your query to control the maximum number of results returned in one batch. The following example retrieves at most five Task entities:

### C\#

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore C\# API reference documentation](https://cloud.google.com/dotnet/docs/reference/Google.Cloud.Datastore.V1/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
Query query = new Query("Task")
{
    Limit = 5,
};
```

### Go

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Go API reference documentation](https://cloud.google.com/go/docs/reference/cloud.google.com/go/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` go
query := datastore.NewQuery("Task").Limit(5)
```

### Java

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Java API reference documentation](https://cloud.google.com/java/docs/reference/google-cloud-datastore/latest/history) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
Query<Entity> query = Query.newEntityQueryBuilder().setKind("Task").setLimit(5).build();
```

### Node.js

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Node.js API reference documentation](https://cloud.google.com/nodejs/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` javascript
const query = datastore.createQuery('Task').limit(5);
```

### PHP

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore PHP API reference documentation](https://googleapis.github.io/google-cloud-php/#/docs/cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
$query = $datastore->query()
    ->kind('Task')
    ->limit(5);
```

### Python

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Python API reference documentation](https://cloud.google.com/python/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
from google.cloud import datastore

# For help authenticating your client, visit
# https://cloud.google.com/docs/authentication/getting-started
client = datastore.Client()

query = client.query()
tasks = list(query.fetch(limit=5))
```

### Ruby

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Ruby API reference documentation](/ruby/docs/reference/google-cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
query = datastore.query("Task")
                 .limit(5)
```

### GQL

``` text
SELECT * FROM Task LIMIT 5
```

*Query cursors* allow an application to retrieve a query's results in convenient batches without incurring the overhead of a query offset. After performing a retrieval operation, the application can obtain a cursor, which is an opaque byte string marking the index position of the last result retrieved. The application can save this string (for instance in your Datastore mode database, a cache, or embedded in a web page as a base-64 encoded HTTP `  GET  ` or `  POST  ` parameter), and can then use the cursor as the starting point for a subsequent retrieval operation to obtain the next batch of results from the point where the previous retrieval ended. A retrieval can also specify an end cursor, to limit the extent of the result set returned.

The following example demonstrates the use of cursors for pagination:

### C\#

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore C\# API reference documentation](https://cloud.google.com/dotnet/docs/reference/Google.Cloud.Datastore.V1/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
Query query = new Query("Task")
{
    Limit = pageSize,
};
if (!string.IsNullOrEmpty(pageCursor))
    query.StartCursor = ByteString.FromBase64(pageCursor);

return _db.RunQuery(query).EndCursor?.ToBase64();
```

### Go

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Go API reference documentation](https://cloud.google.com/go/docs/reference/cloud.google.com/go/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` go
// cursorStr is a cursor to start querying at.
cursorStr := ""

const pageSize = 5
query := datastore.NewQuery("Tasks").Limit(pageSize)
if cursorStr != "" {
 cursor, err := datastore.DecodeCursor(cursorStr)
 if err != nil {
     log.Fatalf("Bad cursor %q: %v", cursorStr, err)
 }
 query = query.Start(cursor)
}

// Read the tasks.
it := client.Run(ctx, query)
var tasks []Task
for {
 var task Task
 _, err := it.Next(&task)
 if err == iterator.Done {
     break
 }
 if err != nil {
     log.Fatalf("Failed fetching results: %v", err)
 }
 tasks = append(tasks, task)
}

// Get the cursor for the next page of results.
// nextCursor.String can be used as the next page's token.
nextCursor, err := it.Cursor()
```

### Java

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Java API reference documentation](https://cloud.google.com/java/docs/reference/google-cloud-datastore/latest/history) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
EntityQuery.Builder queryBuilder =
    Query.newEntityQueryBuilder().setKind("Task").setLimit(pageSize);
if (pageCursor != null) {
  queryBuilder.setStartCursor(pageCursor);
}
QueryResults<Entity> tasks = datastore.run(queryBuilder.build());
while (tasks.hasNext()) {
  Entity task = tasks.next();
  // do something with the task
}
Cursor nextPageCursor = tasks.getCursorAfter();
```

### Node.js

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Node.js API reference documentation](https://cloud.google.com/nodejs/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` javascript
// By default, google-cloud-node will automatically paginate through all of
// the results that match a query. However, this sample implements manual
// pagination using limits and cursor tokens.
async function runPageQuery(pageCursor) {
  let query = datastore.createQuery('Task').limit(pageSize);

  if (pageCursor) {
    query = query.start(pageCursor);
  }
  const results = await datastore.runQuery(query);
  const entities = results[0];
  const info = results[1];

  if (info.moreResults !== Datastore.NO_MORE_RESULTS) {
    // If there are more results to retrieve, the end cursor is
    // automatically set on `info`. To get this value directly, access
    // the `endCursor` property.
    const results = await runPageQuery(info.endCursor);

    // Concatenate entities
    results[0] = entities.concat(results[0]);
    return results;
  }

  return [entities, info];
}
```

### PHP

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore PHP API reference documentation](https://googleapis.github.io/google-cloud-php/#/docs/cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
/**
 * Fetch a query cursor.
 *
 * @param int $pageSize
 * @param string $pageCursor
 * @param string $namespaceId
 */
function cursor_paging(int $pageSize, string $pageCursor = '', string $namespaceId = null)
{
    $datastore = new DatastoreClient(['namespaceId' => $namespaceId]);
    $query = $datastore->query()
        ->kind('Task')
        ->limit($pageSize)
        ->start($pageCursor);
    $result = $datastore->runQuery($query);
    $nextPageCursor = '';
    $entities = [];
    /* @var Entity $entity */
    foreach ($result as $entity) {
        $nextPageCursor = $entity->cursor();
        $entities[] = $entity;
    }

    printf('Found %s entities', count($entities));

    $entities = [];
    if (!empty($nextPageCursor)) {
        $query = $datastore->query()
          ->kind('Task')
          ->limit($pageSize)
          ->start($nextPageCursor);
        $result = $datastore->runQuery($query);

        foreach ($result as $entity) {
            $entities[] = $entity;
        }

        printf('Found %s entities with next page cursor', count($entities));
    }
}
```

### Python

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Python API reference documentation](https://cloud.google.com/python/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
from google.cloud import datastore

# For help authenticating your client, visit
# https://cloud.google.com/docs/authentication/getting-started
client = datastore.Client()


def get_one_page_of_tasks(cursor=None):
    query = client.query(kind="Task")
    query_iter = query.fetch(start_cursor=cursor, limit=5)
    page = next(query_iter.pages)

    tasks = list(page)
    next_cursor = query_iter.next_page_token

    return tasks, next_cursor
```

### Ruby

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Ruby API reference documentation](/ruby/docs/reference/google-cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
page_size = 2
query = datastore.query("Task")
                 .limit(page_size)
tasks = datastore.run query

page_cursor = tasks.cursor

query = datastore.query("Task")
                 .limit(page_size)
                 .start(page_cursor)
```

### GQL

Not Applicable

**Caution:** Be careful when passing a cursor to a client, such as in a web form. Although the client cannot change the cursor value to access results outside of the original query, it is possible for it to decode the cursor to expose information about result entities, such as the project ID, entity kind, key name or numeric ID, ancestor keys, and properties used in the query's filters and sort orders. If you don't want users to have access to that information, you can encrypt the cursor, or store it and provide the user with an opaque key.

**Although Datastore mode databases support integer offsets, you should avoid using them.** Instead, use cursors. Using an offset only avoids returning the skipped entities to your application, but these entities are still retrieved internally. The skipped entities do affect the latency of the query, and your application is billed for the read operations required to retrieve them. Using cursors instead of offsets lets you avoid all these costs.

### Limitations of cursors

Cursors are subject to the following limitations:

  - A cursor can be used only by the same project that performed the original query, and only to continue the same query. It is not possible to retrieve results using a cursor without setting up the same query from which it was originally generated.
  - If any of the following items are changed, a cursor can still be used for subsequent retrievals.
      - start cursor
      - end cursor
      - offset
      - limit
  - If any of the following items are changed, a cursor cannot be used for subsequent retrievals.
      - projection
      - kind
      - ancestor
      - filter
      - distinct on
      - sort order An exception is if the original query's final sort order was on `  __key__  ` . In that case, you can use the cursor in a *reverse query* , which is the original query with each sort order reversed. The reverse query can modify the start cursor, end cursor, offset, and limit.
  - Cursors don't always work as expected with a query that uses an inequality filter or a sort order on a property with multiple values. The de-duplication logic for such multiple-valued properties doesn't persist between retrievals, possibly causing the same result to be returned more than once.
  - New Datastore mode releases may change internal implementation details, invalidating cursors that depend on them. If an application attempts to use a cursor that is no longer valid, Firestore in Datastore mode raises an exception.

### Cursors and data updates

The cursor represents the location in the result list after the last result returned. A cursor is not a relative position in the list (it's not an offset); it's a marker to which a Datastore mode database can jump when starting an index scan for results. If the results for a query change between uses of a cursor, the query notices only changes that occur in results after the cursor. If a new result appears before the cursor's position for the query, it won't be returned when the results after the cursor are fetched. Similarly, if an entity is no longer a result for a query but had appeared before the cursor, the results that appear after the cursor don't change. If the last result returned is removed from the result set, the cursor still knows how to locate the next result.

When retrieving query results, you can use both a start cursor and an end cursor to return a continuous group of results. When using a start and end cursor to retrieve the results, you are not guaranteed that the size of the results will be the same as when you generated the cursors. Entities may be added or deleted from the database between the time the cursors are generated and when they are used in a query.

## Restrictions on queries

The nature of the index query mechanism imposes certain restrictions on what a query can do. Datastore mode queries don't support substring matches, case-insensitive matches, or full-text search. Additionally, the following restrictions apply:

#### Entities lacking a property named in the query are ignored

Entities of the same kind need not have the same properties. To be eligible as a query result, an entity must possess a value (possibly null) for every property named in the query's filters and sort orders. If not, the entity is omitted from the indexes used to execute the query and consequently won't be included in the query's results.

**Note:** It is not possible to query for entities that are specifically *lacking* a given property. One alternative is to add the property with a null value, then filter for entities with null as the value of that property.

#### Filtering on unindexed properties returns no results

A query can't find property values that aren't indexed, nor can it sort on such properties. For more information, see [Unindexed properties](/datastore/docs/concepts/indexes#unindexed_properties) .

#### Limits on inequality filters

To prevent queries from becoming too expensive to run, Firestore in Datastore mode limits the number of range or inequality properties to 10. For more information on queries with inequality filters, see [Query using range and inequality filters on multiple properties](/datastore/docs/multiple-range-fields) .

#### You can't use both `     NOT_EQUAL    ` and `     NOT_IN    ` s

If you use the `  NOT_IN  ` , you can't also add a `  NOT_EQUAL  ` clause.

#### Ordering of query results is undefined when no sort order is specified

When a query doesn't specify a sort order, the results are returned in the order they are retrieved. As the Datastore mode implementation evolves (or if a project's indexes change), this order may change. Therefore, if your application requires its query results in a particular order, be sure to explicitly specify that sort order in the query.

#### Sort orders are ignored on properties with equality filters

Queries that include an equality filter for a given property ignore any sort order specified for that property. This is an optimization to save needless processing for single-valued properties. Since all results have the same value for the property, no further sorting is needed. Multiple-valued properties, however, may have additional values besides the one matched by the equality filter. Because this use case is rare and applying the sort order would be expensive and require extra indexes, the Datastore mode query planner ignores the sort order even in the multiple-valued case. This may cause query results to be returned in a different order than the sort order appears to imply. For example, the sort order is ignored in the following query:

### C\#

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore C\# API reference documentation](https://cloud.google.com/dotnet/docs/reference/Google.Cloud.Datastore.V1/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

Not Applicable

### Go

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Go API reference documentation](https://cloud.google.com/go/docs/reference/cloud.google.com/go/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

Not Applicable

### Java

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Java API reference documentation](https://cloud.google.com/java/docs/reference/google-cloud-datastore/latest/history) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
Query<Entity> query =
    Query.newEntityQueryBuilder()
        .setKind("Task")
        .setFilter(PropertyFilter.eq("tag", "learn"))
        .setOrderBy(OrderBy.asc("tag"))
        .build();
```

### Node.js

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Node.js API reference documentation](https://cloud.google.com/nodejs/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

Not Applicable

### PHP

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore PHP API reference documentation](https://googleapis.github.io/google-cloud-php/#/docs/cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

Not Applicable

### Python

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Python API reference documentation](https://cloud.google.com/python/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

Not Applicable

### Ruby

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Ruby API reference documentation](/ruby/docs/reference/google-cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

Not Applicable

### GQL

``` text
# Sort order on an equality filter is ignored
SELECT * FROM Task WHERE tag = 'learn' ORDER BY tag ASC
```

This doesn't apply to queries that include an `  IN  ` filter. Use the [`  IN  ` operator](/datastore/docs/concepts/queries#in) to combine up to 10 equality ( `  ==  ` ) clauses on the same property with a logical `  OR  ` . If you add a sort order for that property, it's applied to the result set.

### C\#

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore C\# API reference documentation](https://cloud.google.com/dotnet/docs/reference/Google.Cloud.Datastore.V1/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

Not Applicable

### Go

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Go API reference documentation](https://cloud.google.com/go/docs/reference/cloud.google.com/go/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

Not Applicable

### Java

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Java API reference documentation](https://cloud.google.com/java/docs/reference/google-cloud-datastore/latest/history) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
Query<Entity> query =
    Query.newEntityQueryBuilder()
        .setKind("Task")
        .setFilter(PropertyFilter.in("tag", ListValue.of("learn", "study")))
        .setOrderBy(OrderBy.asc("tag"))
        .build();
```

### Node.js

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Node.js API reference documentation](https://cloud.google.com/nodejs/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

Not Applicable

### PHP

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore PHP API reference documentation](https://googleapis.github.io/google-cloud-php/#/docs/cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

Not Applicable

### Python

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Python API reference documentation](https://cloud.google.com/python/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

Not Applicable

### Ruby

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Ruby API reference documentation](/ruby/docs/reference/google-cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

Not Applicable

### GQL

``` text
SELECT * FROM Task WHERE tag IN ARRAY('learn', 'study') ORDER BY tag ASC
```

  - For ascending order, the smallest value that satisfies the filter is used for ordering.
  - For descending order, the greatest value that satisfies the filter is used for ordering.
  - Other values don't affect the sort order and nor does the number of values in the property.

#### Properties used in inequality filters must be sorted first

To retrieve all results that match an inequality filter, a query scans the index for the first row matching the filter, then scans forward until it encounters a non matching row. For the consecutive rows to encompass the complete result set, they must be ordered by the property used in the inequality filter before any other properties. Thus if a query specifies one or more inequality filters along with one or more sort orders, the first sort order must refer to the same property named in the inequality filters. The following is a valid query:

### C\#

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore C\# API reference documentation](https://cloud.google.com/dotnet/docs/reference/Google.Cloud.Datastore.V1/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
Query query = new Query("Task")
{
    Filter = Filter.GreaterThan("priority", 3),
    Order = { { "priority", PropertyOrder.Types.Direction.Ascending},
        {"created", PropertyOrder.Types.Direction.Ascending } }
};
```

### Go

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Go API reference documentation](https://cloud.google.com/go/docs/reference/cloud.google.com/go/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` go
query := datastore.NewQuery("Task").
 FilterField("Priority", ">", 3).
 Order("Priority").
 Order("Created")
```

### Java

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Java API reference documentation](https://cloud.google.com/java/docs/reference/google-cloud-datastore/latest/history) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
Query<Entity> query =
    Query.newEntityQueryBuilder()
        .setKind("Task")
        .setFilter(PropertyFilter.gt("priority", 3))
        .setOrderBy(OrderBy.asc("priority"), OrderBy.asc("created"))
        .build();
```

### Node.js

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Node.js API reference documentation](https://cloud.google.com/nodejs/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` javascript
const query = datastore
  .createQuery('Task')
  .filter(new PropertyFilter('priority', '>', 3))
  .order('priority')
  .order('created');
```

### PHP

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore PHP API reference documentation](https://googleapis.github.io/google-cloud-php/#/docs/cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
$query = $datastore->query()
    ->kind('Task')
    ->filter('priority', '>', 3)
    ->order('priority')
    ->order('created');
```

### Python

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Python API reference documentation](https://cloud.google.com/python/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
from google.cloud import datastore

# For help authenticating your client, visit
# https://cloud.google.com/docs/authentication/getting-started
client = datastore.Client()

query = client.query(kind="Task")
query.add_filter(filter=datastore.query.PropertyFilter("priority", ">", 3))
query.order = ["priority", "created"]
```

### Ruby

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Ruby API reference documentation](/ruby/docs/reference/google-cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
query = datastore.query("Task")
                 .where("priority", ">", 3)
                 .order("priority")
                 .order("created")
```

### GQL

``` text
SELECT * FROM Task WHERE priority > 3 ORDER BY priority, created
```

This query is *not* valid, because it doesn't sort on the property used in the inequality filter:

### C\#

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore C\# API reference documentation](https://cloud.google.com/dotnet/docs/reference/Google.Cloud.Datastore.V1/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
Query query = new Query("Task")
{
    Filter = Filter.GreaterThan("priority", 3),
    Order = { { "created", PropertyOrder.Types.Direction.Ascending } }
};
```

### Go

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Go API reference documentation](https://cloud.google.com/go/docs/reference/cloud.google.com/go/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` go
query := datastore.NewQuery("Task").
 FilterField("Priority", ">", 3).
 Order("Created")
```

### Java

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Java API reference documentation](https://cloud.google.com/java/docs/reference/google-cloud-datastore/latest/history) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
Query<Entity> query =
    Query.newEntityQueryBuilder()
        .setKind("Task")
        .setFilter(PropertyFilter.gt("priority", 3))
        .setOrderBy(OrderBy.asc("created"))
        .build();
```

### Node.js

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Node.js API reference documentation](https://cloud.google.com/nodejs/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` javascript
const query = datastore
  .createQuery('Task')
  .filter(new PropertyFilter('priority', '>', 3))
  .order('created');
```

### PHP

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore PHP API reference documentation](https://googleapis.github.io/google-cloud-php/#/docs/cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
$query = $datastore->query()
    ->kind('Task')
    ->filter('priority', '>', 3)
    ->order('created');
```

### Python

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Python API reference documentation](https://cloud.google.com/python/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
from google.cloud import datastore

# For help authenticating your client, visit
# https://cloud.google.com/docs/authentication/getting-started
client = datastore.Client()

    query = client.query(kind="Task")
    query.add_filter(filter=datastore.query.PropertyFilter("priority", ">", 3))
    query.order = ["created"]
```

### Ruby

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Ruby API reference documentation](/ruby/docs/reference/google-cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
query = datastore.query("Task")
                 .where("priority", ">", 3)
                 .order("created")
```

### GQL

``` text
# Invalid query!
SELECT * FROM Task WHERE priority > 3 ORDER BY created
```

Similarly, this query is not valid because the property used in the inequality filter is not the first one sorted:

### C\#

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore C\# API reference documentation](https://cloud.google.com/dotnet/docs/reference/Google.Cloud.Datastore.V1/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
Query query = new Query("Task")
{
    Filter = Filter.GreaterThan("priority", 3),
    Order = { {"created", PropertyOrder.Types.Direction.Ascending },
        { "priority", PropertyOrder.Types.Direction.Ascending} }
};
```

### Go

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Go API reference documentation](https://cloud.google.com/go/docs/reference/cloud.google.com/go/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` go
query := datastore.NewQuery("Task").
 FilterField("Priority", ">", 3).
 Order("Created").
 Order("Priority")
```

### Java

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Java API reference documentation](https://cloud.google.com/java/docs/reference/google-cloud-datastore/latest/history) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
Query<Entity> query =
    Query.newEntityQueryBuilder()
        .setKind("Task")
        .setFilter(PropertyFilter.gt("priority", 3))
        .setOrderBy(OrderBy.asc("created"), OrderBy.asc("priority"))
        .build();
```

### Node.js

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Node.js API reference documentation](https://cloud.google.com/nodejs/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` javascript
const query = datastore
  .createQuery('Task')
  .filter(new PropertyFilter('priority', '>', 3))
  .order('created')
  .order('priority');
```

### PHP

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore PHP API reference documentation](https://googleapis.github.io/google-cloud-php/#/docs/cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
$query = $datastore->query()
    ->kind('Task')
    ->filter('priority', '>', 3)
    ->order('created')
    ->order('priority');
```

### Python

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Python API reference documentation](https://cloud.google.com/python/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
from google.cloud import datastore

# For help authenticating your client, visit
# https://cloud.google.com/docs/authentication/getting-started
client = datastore.Client()

    query = client.query(kind="Task")
    query.add_filter(filter=datastore.query.PropertyFilter("priority", ">", 3))
    query.order = ["created", "priority"]
```

### Ruby

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Ruby API reference documentation](/ruby/docs/reference/google-cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
query = datastore.query("Task")
                 .where("priority", ">", 3)
                 .order("created")
                 .order("priority")
```

### GQL

``` text
# Invalid query!
SELECT * FROM Task WHERE priority > 3 ORDER BY created, priority
```

#### `     OrderBy    ` and existence

When you order a query by a given property, the query can return only the entities where the order-by property exists.

For example, the following query wouldn't return any entities where the `  priority  ` property is not set, even if they otherwise meet the query filters.

##### Java

``` text
Query<Entity> query =
    Query.newEntityQueryBuilder().setKind("Task")
                                 .setFilter(PropertyFilter.eq("done", false))
                                 .setOrderBy(OrderBy.desc("priority"))
                                 .build();
```

A related effect applies to inequalities. A query with an inequality filter on a property also implies ordering by that property. The following query doesn't return entities without a `  priority  ` property even if `  starred = true  ` in that entity. As a workaround, you can execute separate queries for each ordering or you can assign a value for all properties that you order by.

##### Java

``` text
Query<Entity> query =
    Query.newEntityQueryBuilder()
        .setKind("Task")
        .setFilter(CompositeFilter.or(
            PropertyFilter.eq("starred", true)),
            PropertyFilter.ge("priority", 4))
        .build();
```

The earlier query includes an implied order-by on the inequality such as the following. The direction of the implied order-by depends on available indexes:

##### Java

``` text
Query<Entity> query =
    Query.newEntityQueryBuilder()
        .setKind("Task")
        .setFilter(CompositeFilter.or(
            PropertyFilter.eq("starred", true)),
            PropertyFilter.ge("priority", 4)
        )
        .setOrderBy(OrderBy.asc("priority"))
        .build();
```

#### Limitations on projections

Projection queries are subject to the following limitations:

  - **Only indexed properties can be projected.**
    
    This means that all properties used in a query (projected or filters) must exist in the same index. So, `  select tag from Task where priority = 1  ` requires a composite index on priority then tag.
    
    Projection is not supported for strings that are longer than 1500 bytes, byte arrays that have more than 1500 elements, and other properties explicitly marked as unindexed.

  - **The same property cannot be projected more than once.**

  - **Properties referenced in an equality filter cannot be projected.**
    
    For example,
    
    ``` text
    SELECT tag FROM Task WHERE priority = 1
    ```
    
    is valid (projected property not used in the equality filter), as is
    
    ``` text
    SELECT tag FROM Task WHERE tag > 'fun`
    ```
    
    (not an equality filter), but
    
    ``` text
    SELECT tag FROM Task WHERE tag = 'fun`
    ```
    
    (projected property used in equality filter) is not.

  - **Results returned by a projection query shouldn't be saved back to your Datastore mode database.**
    
    Because the query returns results that are only partially populated, you shouldn't write them back to the Datastore mode database.

  - **Projection queries convert timestamps into integers.**
    
    In the results of a projection query, Datastore mode converts timestamp values to microsecond integer values.

## What's next

Learn about [Transactions](/datastore/docs/concepts/transactions) .
