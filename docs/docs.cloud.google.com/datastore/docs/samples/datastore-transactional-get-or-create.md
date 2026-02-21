Get or create in a transaction.

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Cloud Datastore Transactions](/datastore/docs/concepts/cloud-datastore-transactions)
  - [Transactions](/datastore/docs/concepts/transactions)

## Code sample

### C\#

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode C\# API reference documentation](https://cloud.google.com/dotnet/docs/reference/Google.Cloud.Datastore.V1/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
Entity task;
using (var transaction = _db.BeginTransaction())
{
    task = transaction.Lookup(_sampleTask.Key);
    if (task == null)
    {
        transaction.Insert(_sampleTask);
        transaction.Commit();
    }
}
```

### Go

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Go API reference documentation](https://cloud.google.com/go/docs/reference/cloud.google.com/go/datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` go
_, err := client.RunInTransaction(ctx, func(tx *datastore.Transaction) error {
 var task Task
 if err := tx.Get(key, &task); err != datastore.ErrNoSuchEntity {
     return err
 }
 _, err := tx.Put(key, &Task{
     Category:    "Personal",
     Done:        false,
     Priority:    4,
     Description: "Learn Cloud Datastore",
 })
 return err
})
```

### Java

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Java API reference documentation](https://cloud.google.com/java/docs/reference/google-cloud-datastore/latest/history) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
Entity task;
Transaction txn = datastore.newTransaction();
try {
  task = txn.get(taskKey);
  if (task == null) {
    task = Entity.newBuilder(taskKey).build();
    txn.put(task);
    txn.commit();
  }
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
async function getOrCreate(taskKey, taskData) {
  const taskEntity = {
    key: taskKey,
    data: taskData,
  };
  const transaction = datastore.transaction();

  try {
    await transaction.run();
    const [task] = await transaction.get(taskKey);
    if (task) {
      // The task entity already exists.
      await transaction.rollback();
    } else {
      // Create the task entity.
      transaction.save(taskEntity);
      await transaction.commit();
    }
    return taskEntity;
  } catch (err) {
    await transaction.rollback();
  }
}
```

### PHP

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode PHP API reference documentation](https://googleapis.github.io/google-cloud-php/#/docs/cloud-datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
$transaction = $datastore->transaction();
$entity = $transaction->lookup($task->key());
if ($entity === null) {
    $entity = $transaction->insert($task);
    $transaction->commit();
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

import datetime

with client.transaction():
    key = client.key(
        "Task", datetime.datetime.now(tz=datetime.timezone.utc).isoformat()
    )

    task = client.get(key)

    if not task:
        task = datastore.Entity(key)
        task.update({"description": "Example task"})
        client.put(task)

    return task
```

### Ruby

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Ruby API reference documentation](/ruby/docs/reference/google-cloud-datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
task = nil
datastore.transaction do |tx|
  task = tx.find task_key
  if task.nil?
    task = datastore.entity task_key do |t|
      t["category"] = "Personal"
      t["done"] = false
      t["priority"] = 4
      t["description"] = "Learn Cloud Datastore"
    end
    tx.save task
  end
end
```

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](/docs/samples?product=datastore) .
