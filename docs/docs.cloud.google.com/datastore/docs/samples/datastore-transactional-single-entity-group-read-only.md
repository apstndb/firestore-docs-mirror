Use a read-only transaction.

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Cloud Datastore Transactions](/datastore/docs/concepts/cloud-datastore-transactions)
  - [Transactions](/datastore/docs/concepts/transactions)

## Code sample

### C\#

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode C\# API reference documentation](https://cloud.google.com/dotnet/docs/reference/Google.Cloud.Datastore.V1/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
Entity taskList;
IReadOnlyList<Entity> tasks;
using (var transaction = _db.BeginTransaction(TransactionOptions.CreateReadOnly()))
{
    taskList = transaction.Lookup(taskListKey);
    var query = new Query("Task")
    {
        Filter = Filter.HasAncestor(taskListKey)
    };
    tasks = transaction.RunQuery(query).Entities;
    transaction.Commit();
}
```

### Go

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Go API reference documentation](https://cloud.google.com/go/docs/reference/cloud.google.com/go/datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` go
tx, err := client.NewTransaction(ctx, datastore.ReadOnly)
if err != nil {
 log.Fatalf("client.NewTransaction: %v", err)
}
defer tx.Rollback() // Transaction only used for read.

ancestor := datastore.NameKey("TaskList", "default", nil)
query := datastore.NewQuery("Task").Ancestor(ancestor).Transaction(tx)
var tasks []Task
_, err = client.GetAll(ctx, query, &tasks)
```

### Java

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Java API reference documentation](https://cloud.google.com/java/docs/reference/google-cloud-datastore/latest/history) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
Entity taskList;
QueryResults<Entity> tasks;
Transaction txn =
    datastore.newTransaction(
        TransactionOptions.newBuilder().setReadOnly(ReadOnly.newBuilder().build()).build());
try {
  taskList = txn.get(taskListKey);
  Query<Entity> query =
      Query.newEntityQueryBuilder()
          .setKind("Task")
          .setFilter(PropertyFilter.hasAncestor(taskListKey))
          .build();
  tasks = txn.run(query);
  txn.commit();
} finally {
  if (txn.isActive()) {
    txn.rollback();
  }
}
```

### Node.js

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Node.js API reference documentation](https://cloud.google.com/nodejs/docs/reference/datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` javascript
async function getTaskListEntities() {
  const transaction = datastore.transaction({readOnly: true});
  try {
    const taskListKey = datastore.key(['TaskList', 'default']);

    await transaction.run();
    const [taskList] = await transaction.get(taskListKey);
    const query = datastore.createQuery('Task').hasAncestor(taskListKey);
    const [taskListEntities] = await transaction.runQuery(query);
    await transaction.commit();
    return [taskList, taskListEntities];
  } catch (err) {
    await transaction.rollback();
  }
}
```

### PHP

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode PHP API reference documentation](https://googleapis.github.io/google-cloud-php/#/docs/cloud-datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
$transaction = $datastore->readOnlyTransaction();
$taskListKey = $datastore->key('TaskList', 'default');
$query = $datastore->query()
    ->kind('Task')
    ->hasAncestor($taskListKey);
$result = $transaction->runQuery($query);
$taskListEntities = [];
$num = 0;
/* @var Entity $task */
foreach ($result as $task) {
    $taskListEntities[] = $task;
    $num += 1;
}
```

### Python

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Python API reference documentation](https://cloud.google.com/python/docs/reference/datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
from google.cloud import datastore

# For help authenticating your client, visit
# https://cloud.google.com/docs/authentication/getting-started
client = datastore.Client()

with client.transaction(read_only=True):
    task_list_key = client.key("TaskList", "default")

    task_list = client.get(task_list_key)

    query = client.query(kind="Task", ancestor=task_list_key)
    tasks_in_list = list(query.fetch())

    return task_list, tasks_in_list
```

### Ruby

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Ruby API reference documentation](/ruby/docs/reference/google-cloud-datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
# task_list_name = "default"
task_list_key = datastore.key "TaskList", task_list_name
datastore.read_only_transaction do |tx|
  task_list = tx.find task_list_key
  query = datastore.query("Task").ancestor(task_list)
  tasks_in_list = tx.run query
end
```

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](/docs/samples?product=datastore) .
