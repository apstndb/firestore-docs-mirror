**Note:** This page describes system behavior for Datastore databases that have not yet upgraded to Firestore in Datastore mode.

[Firestore](/firestore) is the new version of Datastore and [removes several Datastore limitations](/datastore/docs/firestore-or-datastore#in_datastore_mode) .

Datastore provides high availability, scalability and durability by distributing data over many machines and using masterless, synchronous replication over a wide geographic area. However, a tradeoff in this design is the write throughput for any single [entity group](/datastore/docs/concepts/entities#entity_groups) is limited to about one commit per second. There are also limitations on queries or transactions that span multiple entity groups. This page describes these limitations in more detail and discusses best practices for structuring your data to support strong consistency while still meeting your application's write throughput requirements.

## Consistency levels

Datastore queries can deliver their results at either of two consistency levels:

  - [*Strongly consistent*](https://en.wikipedia.org/wiki/Strong_consistency) queries guarantee the most up-to-date results, but may take longer to complete or may not be supported in certain cases.
  - [*Eventually consistent*](https://en.wikipedia.org/wiki/Eventual_consistency) queries generally run faster, but may occasionally return stale results.

In an eventually consistent query, the indexes used to gather the results are also accessed with eventual consistency. Consequently, such queries may sometimes return entities that no longer match the query criteria, and may also omit entities that match the query criteria. Strongly consistent queries are transactionally consistent, meaning the results are based on a single, consistent snapshot of the data.

## Consistency guarantees

Queries return their results with different levels of consistency guarantee, depending on the nature of the query:

  - [Ancestor queries](/datastore/docs/concepts/queries#ancestor_queries) (those that execute against an [entity group](/datastore/docs/concepts/entities#entity_groups) ) are strongly consistent by default, but can be made eventually consistent by setting the Datastore read policy (discussed below).
  - Global queries (those that do not execute against an entity group) are always eventually consistent.

In many applications, it is acceptable to use eventual consistency (i.e., a global query spanning multiple entity groups, which may at times return slightly stale data) when obtaining a broad view of unrelated data, and then to use strong consistency (an ancestor query, or a lookup of a single entity) when viewing or editing a single set of highly related data. In such applications, it is usually a good approach to place highly related data in entity groups. A higher number of entity groups increases throughput, while a lower number of entity groups increases the volume of entities that can be read in a single ancestor query. An application needs to take this into account to determine the right balance of throughput and consistency.

## Datastore read policy

To improve performance, you can set a query's *read policy* so that the results are eventually consistent. (The Datastore API also allows you to explicitly set a strong consistency policy, but this setting has no practical effect, since global queries are always eventually consistent regardless of policy.)

You can enable eventually consistent reads via the read options of the query object:

### C\#

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore C\# API reference documentation](https://cloud.google.com/dotnet/docs/reference/Google.Cloud.Datastore.V1/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
Query query = new Query("Task")
{
    Filter = Filter.HasAncestor(_db.CreateKeyFactory("TaskList")
        .CreateKey(keyName))
};
var results = _db.RunQuery(query,
    ReadOptions.Types.ReadConsistency.Eventual);
```

### Go

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Go API reference documentation](https://cloud.google.com/go/docs/reference/cloud.google.com/go/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` go
ancestor := datastore.NameKey("TaskList", "default", nil)
query := datastore.NewQuery("Task").Ancestor(ancestor).EventualConsistency()
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
datastore.run(query, ReadOption.eventualConsistency());
```

### Node.js

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Node.js API reference documentation](https://cloud.google.com/nodejs/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` javascript
const ancestorKey = datastore.key(['TaskList', 'default']);
const query = datastore.createQuery('Task').hasAncestor(ancestorKey);

query.run({consistency: 'eventual'});
```

### PHP

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore PHP API reference documentation](https://googleapis.github.io/google-cloud-php/#/docs/cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
$query = $datastore->query()
    ->kind('Task')
    ->hasAncestor($datastore->key('TaskList', 'default'));
$result = $datastore->runQuery($query, ['readConsistency' => 'EVENTUAL']);
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
query.fetch(eventual=True)
```

### Ruby

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Ruby API reference documentation](/ruby/docs/reference/google-cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
# task_list_name = "default"
ancestor_key = datastore.key "TaskList", task_list_name

query = datastore.query("Task")
                 .ancestor(ancestor_key)

tasks = datastore.run query, consistency: :eventual
```

## Transactions and consistency considerations

Datastore commits are either *transactional* , meaning they take place in the context of a [transaction](/datastore/docs/concepts/transactions) and the transaction’s set of mutations are either all applied or none are applied, or *non-transactional* , meaning the set of mutations may not apply as all or none.

A single transaction can include any number of create, update, or delete mutations. To maintain the consistency of the data, the transaction ensures that all of the mutations it contains are applied to Datastore as a unit or, if any of the mutations fail, that none of them are applied. Furthermore, all strongly consistent reads (ancestor queries or `  lookup  ` operations) performed within the same transaction rely on a single, consistent snapshot of the data. Strongly consistent queries must specify an ancestor filter. Queries that participate in a transaction are always strongly consistent. Transactions can involve at most 25 entity groups. Eventually consistent reads do not have those limitations, and are adequate in many cases. Using eventually consistent reads may allow you to distribute your data among a larger number of entity groups, enabling you to obtain greater write throughput by executing commits in parallel on the different entity groups. But, you need to understand the characteristics of eventually consistent reads in order to determine whether they are suitable for your application:

  - The results from these reads may not reflect the latest transactions. This can occur because these reads do not ensure that the replica they are running on is up-to-date. Instead, they use whatever data is available on that replica at the time of query execution.
  - A committed transaction that spanned multiple entity groups may appear to have been applied to some of the entities and not others. Note, though, that a transaction will never appear to have been partially applied within a single entity.
  - The query results may include entities that should not have been included according to the filter criteria, and may exclude entities that should have been included. This can occur because the snapshot version used to read indexes may differ from the snapshot version used to read the entity.

## Structuring your data for consistency

To understand how to structure your data for strong consistency, compare two different approaches for a simple task list application. The first approach creates each entity in its own new entity group (i.e., each entity is a root entity):

### C\#

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore C\# API reference documentation](https://cloud.google.com/dotnet/docs/reference/Google.Cloud.Datastore.V1/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
Entity task = new Entity()
{
    Key = _db.CreateKeyFactory("Task").CreateKey("sampleTask"),
    ["category"] = "Personal",
    ["done"] = false,
    ["priority"] = 4,
    ["description"] = "Learn Cloud Datastore"
};
```

### Go

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Go API reference documentation](https://cloud.google.com/go/docs/reference/cloud.google.com/go/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` go
type Task struct {
 Category        string
 Done            bool
 Priority        float64
 Description     string `datastore:",noindex"`
 PercentComplete float64
 Created         time.Time
}
task := &Task{
 Category:        "Personal",
 Done:            false,
 Priority:        4,
 Description:     "Learn Cloud Datastore",
 PercentComplete: 10.0,
 Created:         time.Now(),
}
```

### Java

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Java API reference documentation](https://cloud.google.com/java/docs/reference/google-cloud-datastore/latest/history) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
Key taskKey = datastore.newKeyFactory().setKind("Task").newKey("sampleTask");
Entity task =
    Entity.newBuilder(taskKey)
        .set("category", "Personal")
        .set("done", false)
        .set("priority", 4)
        .set("description", "Learn Cloud Datastore")
        .build();
```

### Node.js

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Node.js API reference documentation](https://cloud.google.com/nodejs/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` javascript
const task = {
  category: 'Personal',
  done: false,
  priority: 4,
  description: 'Learn Cloud Datastore',
};
```

### PHP

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore PHP API reference documentation](https://googleapis.github.io/google-cloud-php/#/docs/cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
$task = $datastore->entity('Task', [
    'category' => 'Personal',
    'done' => false,
    'priority' => 4,
    'description' => 'Learn Cloud Datastore'
]);
```

### Python

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Python API reference documentation](https://cloud.google.com/python/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
from google.cloud import datastore

# For help authenticating your client, visit
# https://cloud.google.com/docs/authentication/getting-started
client = datastore.Client()

task = datastore.Entity(client.key("Task"))
task.update(
    {
        "category": "Personal",
        "done": False,
        "priority": 4,
        "description": "Learn Cloud Datastore",
    }
)
```

### Ruby

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Ruby API reference documentation](/ruby/docs/reference/google-cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
task = datastore.entity "Task" do |t|
  t["category"] = "Personal"
  t["done"] = false
  t["priority"] = 4
  t["description"] = "Learn Cloud Datastore"
end
```

It then queries on the entity kind `  Task  ` for the tasks that are not yet done with priorities greater than or equal to 4, sorted in descending order by priority:

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

However, because we are using an eventually consistent query (rather than an ancestor query), the query results may not contain the new entity. Nonetheless, nearly all writes will be available for eventually consistent queries shortly after a commit. For many applications, a solution that provides the results of an eventually consistent query in the context of the current user's own changes will usually be sufficient to make such latencies completely acceptable.

To achieve strong consistency, a better approach is to create the entities with an ancestor path. The ancestor path identifies the common root entity in which the created entities are grouped. This example uses an ancestor path of kind `  TaskList  ` named `  default  ` :

### C\#

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore C\# API reference documentation](https://cloud.google.com/dotnet/docs/reference/Google.Cloud.Datastore.V1/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
Key taskListKey = _db.CreateKeyFactory("TaskList").CreateKey(TestUtil.RandomName());
Key taskKey = new KeyFactory(taskListKey, "Task").CreateKey("sampleTask");
Entity task = new Entity()
{
    Key = taskKey,
    ["category"] = "Personal",
    ["done"] = false,
    ["priority"] = 4,
    ["description"] = "Learn Cloud Datastore"
};
```

### Go

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Go API reference documentation](https://cloud.google.com/go/docs/reference/cloud.google.com/go/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` go
parentKey := datastore.NameKey("TaskList", "default", nil)
key := datastore.IncompleteKey("Task", parentKey)

task := Task{
 Category:    "Personal",
 Done:        false,
 Priority:    4,
 Description: "Learn Cloud Datastore",
}

// A complete key is assigned to the entity when it is Put.
var err error
key, err = client.Put(ctx, key, &task)
```

### Java

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Java API reference documentation](https://cloud.google.com/java/docs/reference/google-cloud-datastore/latest/history) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
Key taskKey =
    datastore
        .newKeyFactory()
        .addAncestors(PathElement.of("TaskList", "default"))
        .setKind("Task")
        .newKey("sampleTask");
Entity task =
    Entity.newBuilder(taskKey)
        .set("category", "Personal")
        .set("done", false)
        .set("priority", 4)
        .set("description", "Learn Cloud Datastore")
        .build();
```

### Node.js

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Node.js API reference documentation](https://cloud.google.com/nodejs/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` javascript
const taskKey = datastore.key([
  'TaskList',
  'default',
  'Task',
  'sampleTask',
]);

const task = {
  key: taskKey,
  data: {
    category: 'Personal',
    done: false,
    priority: 4,
    description: 'Learn Cloud Datastore',
  },
};
```

### PHP

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore PHP API reference documentation](https://googleapis.github.io/google-cloud-php/#/docs/cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
$parentKey = $datastore->key('TaskList', 'default');
$key = $datastore->key('Task')->ancestorKey($parentKey);
$task = $datastore->entity(
    $key,
    [
        'Category' => 'Personal',
        'Done' => false,
        'Priority' => 4,
        'Description' => 'Learn Cloud Datastore'
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

key_with_parent = client.key("TaskList", "default", "Task", "sampleTask")

task = datastore.Entity(key=key_with_parent)

task.update(
    {
        "category": "Personal",
        "done": False,
        "priority": 4,
        "description": "Learn Cloud Datastore",
    }
)
```

### Ruby

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Ruby API reference documentation](/ruby/docs/reference/google-cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
# task_list_name = "default"
# task_name = "sampleTask"
task_key = datastore.key [["TaskList", task_list_name], ["Task", task_name]]

task = datastore.entity task_key do |t|
  t["category"] = "Personal"
  t["done"] = false
  t["priority"] = 4
  t["description"] = "Learn Cloud Datastore"
end
```

You will then be able to perform a strongly consistent ancestor query within the entity group identified by the common root entity:

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

This approach achieves strong consistency by writing to a single entity group per task list, but it also limits changes to the task list to no more than 1 write per second (the supported limit for entity groups). If your application is likely to encounter heavier write usage, you may need to consider using other means. For example, if your application is a guestbook that lets users post messages to a public message board, you might put recent posts in memcache with an expiration and display a mix of recent posts from memcache and Datastore, or you might cache them in a cookie, put some state in the URL, or something else entirely. The goal is to find a caching solution that provides the data for the current user during the period of time in which the user is posting to your application. Remember, if you do a `  lookup  ` , an ancestor query (assuming the read policy is not set to eventually consistent), or any operation within a transaction, you will always see the most recently written data.

**Note:** If your application receives an exception when attempting to commit a transaction, it does not necessarily mean that the transaction has failed. It is possible to receive exceptions or errors even when a transaction has been committed. Whenever possible, structure your Datastore transactions so that the end result will be unaffected if your code retry logic applies the same transaction more than once.

For additional examples of how to use transactions, go [here](/datastore/docs/concepts/transactions#using_transactions) .

## Entity group limitations on transactions

The organization of data into entity groups can limit what transactions can be performed:

  - All the data accessed by a transaction must be contained in at most 25 entity groups.
  - If you want to use queries within a transaction, your data must be organized into entity groups in such a way that you can specify ancestor filters that will match the right data.
  - There is a write throughput limit of about one transaction per second for a single entity group. This limitation exists because Datastore performs masterless, synchronous replication of each entity group over a wide geographic area to provide high reliability and fault tolerance.

**Note:** Avoid storing sensitive information in the entity group key. Entity group keys may be retained after the entity group is deleted in order to provide fast and reliable service across Datastore.

For more information on how entities and indexes are updated, see the [Transaction Isolation](/datastore/docs/articles/transaction_isolation) article.
