A *transaction* is a set of operations on one or more entities. Each transaction is guaranteed to be atomic, meaning that transactions are never partially applied. Either all of the operations in the transaction are applied, or none of them are applied.

## Using transactions

Transactions expire after 270 seconds or if idle for 60 seconds.

An operation may fail when:

  - Too many concurrent modifications are attempted on the same entity.
  - The transaction exceeds a resource limit.
  - The Datastore mode database encounters an internal error.

In all these cases, the Datastore API returns an error.

**Note:** If your application receives an exception when committing a transaction, it does not always mean that the transaction failed. You can receive errors in cases where transactions have been committed. Whenever possible, make your transactions idempotent so that if you repeat a transaction, the end result will be the same.

Transactions are an optional feature. You're not required to use transactions to perform database operations.

An application can execute a set of statements and operations in a single transaction, such that if any statement or operation raises an exception, none of the database operations in the set are applied. The application defines the actions to perform in the transaction.

The following snippet shows how to perform a transaction. It transfers money from one account to another.

### C\#

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore C\# API reference documentation](https://cloud.google.com/dotnet/docs/reference/Google.Cloud.Datastore.V1/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
private void TransferFunds(Key fromKey, Key toKey, long amount)
{
    using (var transaction = _db.BeginTransaction())
    {
        var entities = transaction.Lookup(fromKey, toKey);
        entities[0]["balance"].IntegerValue -= amount;
        entities[1]["balance"].IntegerValue += amount;
        transaction.Update(entities);
        transaction.Commit();
    }
}
```

### Go

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Go API reference documentation](https://cloud.google.com/go/docs/reference/cloud.google.com/go/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` go
type BankAccount struct {
 Balance int
}

const amount = 50
keys := []*datastore.Key{to, from}
tx, err := client.NewTransaction(ctx)
if err != nil {
 log.Fatalf("client.NewTransaction: %v", err)
}
accs := make([]BankAccount, 2)
if err := tx.GetMulti(keys, accs); err != nil {
 tx.Rollback()
 log.Fatalf("tx.GetMulti: %v", err)
}
accs[0].Balance += amount
accs[1].Balance -= amount
if _, err := tx.PutMulti(keys, accs); err != nil {
 tx.Rollback()
 log.Fatalf("tx.PutMulti: %v", err)
}
if _, err = tx.Commit(); err != nil {
 log.Fatalf("tx.Commit: %v", err)
}
```

### Java

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Java API reference documentation](https://cloud.google.com/java/docs/reference/google-cloud-datastore/latest/history) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
void transferFunds(Key fromKey, Key toKey, long amount) {
  Transaction txn = datastore.newTransaction();
  try {
    List<Entity> entities = txn.fetch(fromKey, toKey);
    Entity from = entities.get(0);
    Entity updatedFrom =
        Entity.newBuilder(from).set("balance", from.getLong("balance") - amount).build();
    Entity to = entities.get(1);
    Entity updatedTo =
        Entity.newBuilder(to).set("balance", to.getLong("balance") + amount).build();
    txn.put(updatedFrom, updatedTo);
    txn.commit();
  } finally {
    if (txn.isActive()) {
      txn.rollback();
    }
  }
}
```

### Node.js

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Node.js API reference documentation](https://cloud.google.com/nodejs/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` javascript
async function transferFunds(fromKey, toKey, amount) {
  const transaction = datastore.transaction();
  await transaction.run();
  const results = await Promise.all([
    transaction.get(fromKey),
    transaction.get(toKey),
  ]);
  const accounts = results.map(result => result[0]);

  accounts[0].balance -= amount;
  accounts[1].balance += amount;

  transaction.save([
    {
      key: fromKey,
      data: accounts[0],
    },
    {
      key: toKey,
      data: accounts[1],
    },
  ]);

  return await transaction.commit();
}
```

### PHP

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore PHP API reference documentation](https://googleapis.github.io/google-cloud-php/#/docs/cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
/**
 * Update two entities in a transaction.
 *
 * @param string $fromKeyId
 * @param string $toKeyId
 * @param int $amount
 * @param string $namespaceId
 */
function transfer_funds(
    string $fromKeyId,
    string $toKeyId,
    int $amount,
    string $namespaceId = null
) {
    $datastore = new DatastoreClient(['namespaceId' => $namespaceId]);
    $transaction = $datastore->transaction();
    $fromKey = $datastore->key('Account', $fromKeyId);
    $toKey = $datastore->key('Account', $toKeyId);
    // The option 'sort' is important here, otherwise the order of the result
    // might be different from the order of the keys.
    $result = $transaction->lookupBatch([$fromKey, $toKey], ['sort' => true]);
    if (count($result['found']) != 2) {
        $transaction->rollback();
    }
    $fromAccount = $result['found'][0];
    $toAccount = $result['found'][1];
    $fromAccount['balance'] -= $amount;
    $toAccount['balance'] += $amount;
    $transaction->updateBatch([$fromAccount, $toAccount]);
    $transaction->commit();
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

def transfer_funds(client, from_key, to_key, amount):
    with client.transaction():
        from_account = client.get(from_key)
        to_account = client.get(to_key)

        from_account["balance"] -= amount
        to_account["balance"] += amount

        client.put_multi([from_account, to_account])
```

### Ruby

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Ruby API reference documentation](/ruby/docs/reference/google-cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
def transfer_funds from_key, to_key, amount
  datastore.transaction do |tx|
    from = tx.find from_key
    from["balance"] -= amount
    to = tx.find to_key
    to["balance"] += amount
    tx.save from, to
  end
end
```

Note that in order to keep our examples more succinct we sometimes omit the `  rollback  ` if the transaction fails. In production code, it is important to ensure that every transaction is either explicitly committed or rolled back.

## What can be done in a transaction

Transactions can query or lookup any number of entities. The maximum size of a transaction is [10 MiB](/datastore/docs/concepts/limits) . You can use a read-write transaction or a read-only transaction.

## Isolation and consistency

Datastore mode databases enforce [serializable isolation](http://en.wikipedia.org/wiki/Serializability) . Data read or modified by a transaction cannot be concurrently modified.

Queries and lookups in a transaction see a consistent snapshot of the state of the database. This snapshot is guaranteed to contain the effect of all transactions and writes that completed prior to the beginning of the transaction.

This consistent snapshot view also extends to reads after writes inside transactions. Unlike with most databases, queries and lookups inside a Datastore mode transaction do *not* see the results of previous writes inside that transaction. Specifically, if an entity is modified or deleted within a transaction, a query or lookup returns the *original* version of the entity as of the beginning of the transaction, or nothing if the entity did not exist then.

Outside of transactions, queries and lookups also have serializable isolation.

## Concurrency modes

Firestore in Datastore mode supports three concurrency modes. The concurrency mode is a database setting that determines how concurrent transactions interact. You can select from one of the following concurrency modes:

  - **Pessimistic**
    
    Read-write transactions use reader/writer locks to enforce isolation and serializability. When two or more concurrent read-write transactions read or write the same data, the lock held by one transaction can delay the other transactions. If your transaction does not require any writes, you can improve performance and avoid contention with other transactions by using a [read-only transaction](#read-only_transactions) . Read-only transaction do not require any locks.
    
    **Firestore in Datastore mode databases use the pessimistic concurrency mode by default.**

  - **Optimistic**
    
    When two or more concurrent read-write transactions read or write the same data, only the first transaction to commit its changes succeeds. Other transactions that perform writes fail on commit.
    
    **Note:** In the past, legacy Cloud Datastore databases were upgraded to Firestore in Datastore mode. Most upgraded databases were initially configured to use the optimistic concurrency mode.

  - **Optimistic With Entity Groups**
    
    Use this concurrency mode only if your app depends on the [entity group transactional semantics of legacy Cloud Datastore](/datastore/docs/concepts/cloud-datastore-transactions#transactions_and_entity_groups) . This concurrency mode places additional limits on transactions:
    
      - Transactions are limited to 25 entity groups.
      - Writes to an entity group are limited to 1 per second.
      - Queries in transactions must be ancestor queries.
    
    **Note:** In the past, legacy Cloud Datastore databases were upgraded to Firestore in Datastore mode. Databases that depended on entity group transactional semantics were initially configured to use the Optimistic With Entity Groups concurrency mode.
    
    To remove `  OPTIMISTIC_WITH_ENTITY_GROUPS  ` query, transaction and write throughput limitations, change your project's concurrency mode to Optimistic. To ensure this change is compatible with your project:
    
    1.  Create a test project in Firestore in Datastore mode.
    
    2.  Change the test project's concurrency mode to `  OPTIMISTIC  ` . Issue an [HTTP PATCH](/firestore/docs/reference/rest/v1/projects.databases/patch) request, as demonstrated below.
    
    3.  Run tests on the test project to ensure that you workload performs as expected without Entity Groups.
    
    4.  [Change your main project's concurrency mode](#change_concurrency_mode) from `  OPTIMISTIC_WITH_ENTITY_GROUPS  ` to `  OPTIMISTIC  ` .
    
    **Note:** The [Remote API](/appengine/docs/standard/python/tools/remoteapi) library requires Entity Groups and will not work in the `  OPTIMISTIC  ` concurrency mode. If you use the Remote API, either migrate off this API, or to continue using this library, keep your project in the `  OPTIMISTIC_WITH_ENTITY_GROUPS  ` mode.

### View concurrency mode

Use the Firestore [projects.databases](https://cloud.google.com/firestore/docs/reference/rest/v1/projects.databases) REST resource to view your database's concurrency mode:

``` text
curl -X GET -H "Authorization: Bearer "$(gcloud auth print-access-token) \
"https://firestore.googleapis.com/v1/projects/PROJECT_ID/databases"
```

### Change concurrency mode

To change your database's concurrency mode, send a `  PATCH  ` request to the Firestore [projects.databases](https://cloud.google.com/firestore/docs/reference/rest/v1/projects.databases) REST resource:

``` text
curl --request PATCH \
--header "Authorization: Bearer "$(gcloud auth print-access-token) \
--header 'Accept: application/json' \
--header 'Content-Type: application/json' \
--data '{"concurrencyMode":"CONCURRENCY_MODE"}' \
"https://firestore.googleapis.com/v1/projects/PROJECT_ID/databases/(default)?updateMask=concurrencyMode"
```

where:

  - CONCURRENCY\_MODE is `  PESSIMISTIC  ` , `  OPTIMISTIC  ` , or `  OPTIMISTIC_WITH_ENTITY_GROUPS  ` .
  - PROJECT\_ID is the ID of your Google Cloud project.

## Uses for transactions

One use of transactions is updating an entity with a new property value relative to its current value. The `  transferFunds  ` example above does that for two entities, by withdrawing money from one account and transferring it to another. The Datastore API does not automatically retry transactions, but you can add your own logic to retry them, for instance to handle conflicts when another request updates the same entity at the same time.

### C\#

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore C\# API reference documentation](https://cloud.google.com/dotnet/docs/reference/Google.Cloud.Datastore.V1/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
/// <summary>
/// Retry the action when a Grpc.Core.RpcException is thrown.
/// </summary>
private T RetryRpc<T>(Func<T> action)
{
    List<Grpc.Core.RpcException> exceptions = null;
    var delayMs = _retryDelayMs;
    for (int tryCount = 0; tryCount < _retryCount; ++tryCount)
    {
        try
        {
            return action();
        }
        catch (Grpc.Core.RpcException e)
        {
            if (exceptions == null)
                exceptions = new List<Grpc.Core.RpcException>();
            exceptions.Add(e);
        }
        System.Threading.Thread.Sleep(delayMs);
        delayMs *= 2;  // Exponential back-off.
    }
    throw new AggregateException(exceptions);
}

private void RetryRpc(Action action)
{
    RetryRpc(() => { action(); return 0; });
}

[Fact]
public void TestTransactionalRetry()
{
    int tryCount = 0;
    var keys = UpsertBalances();
    RetryRpc(() =>
    {
        using (var transaction = _db.BeginTransaction())
        {
            TransferFunds(keys[0], keys[1], 10, transaction);
            // Insert a conflicting transaction on the first try.
            if (tryCount++ == 0)
                TransferFunds(keys[1], keys[0], 5);
            transaction.Commit();
        }
    });
    Assert.Equal(2, tryCount);
}
```

### Go

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Go API reference documentation](https://cloud.google.com/go/docs/reference/cloud.google.com/go/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` go
type BankAccount struct {
 Balance int
}

const amount = 50
_, err := client.RunInTransaction(ctx, func(tx *datastore.Transaction) error {
 keys := []*datastore.Key{to, from}
 accs := make([]BankAccount, 2)
 if err := tx.GetMulti(keys, accs); err != nil {
     return err
 }
 accs[0].Balance += amount
 accs[1].Balance -= amount
 _, err := tx.PutMulti(keys, accs)
 return err
})
```

### Java

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Java API reference documentation](https://cloud.google.com/java/docs/reference/google-cloud-datastore/latest/history) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
int retries = 5;
while (true) {
  try {
    transferFunds(fromKey, toKey, 10);
    break;
  } catch (DatastoreException e) {
    if (retries == 0) {
      throw e;
    }
    --retries;
  }
}
// Retry handling can also be configured and automatically applied using google-cloud-java.
```

### Node.js

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Node.js API reference documentation](https://cloud.google.com/nodejs/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` javascript
async function transferFundsWithRetry() {
  const maxTries = 5;

  async function tryRequest(currentAttempt, delay) {
    try {
      await transferFunds(fromKey, toKey, 10);
    } catch (err) {
      if (currentAttempt <= maxTries) {
        // Use exponential backoff
        setTimeout(async () => {
          await tryRequest(currentAttempt + 1, delay * 2);
        }, delay);
      }
      throw err;
    }
  }

  await tryRequest(1, 100);
}
```

### PHP

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore PHP API reference documentation](https://googleapis.github.io/google-cloud-php/#/docs/cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
$retries = 5;
for ($i = 0; $i < $retries; $i++) {
    try {
        require_once __DIR__ . '/transfer_funds.php';
        transfer_funds($fromKeyId, $toKeyId, 10, $namespaceId);
    } catch (\Google\Cloud\Core\Exception\ConflictException $e) {
        // if $i >= $retries, the failure is final
        continue;
    }
    // Succeeded!
    break;
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

import google.cloud.exceptions

for _ in range(5):
    try:
        transfer_funds(client, account1.key, account2.key, 50)
        break
    except google.cloud.exceptions.Conflict:
        continue
else:
    print("Transaction failed.")
```

### Ruby

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Ruby API reference documentation](/ruby/docs/reference/google-cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
(1..5).each do |i|
  begin
    return transfer_funds from_key, to_key, amount
  rescue Google::Cloud::Error => e
    raise e if i == 5
  end
end
```

This requires a transaction because the value of `  balance  ` in an entity may be updated by another user after this code fetches the object, but before it saves the modified object. Without a transaction, the user's request uses the value of `  balance  ` prior to the other user's update, and the save overwrites the new value. With a transaction, the application is told about the other user's update.

Another common use for transactions is to fetch an entity with a named key, or create it if it doesn't yet exist (this example builds on the TaskList example from [creating an entity](/datastore/docs/concepts/entities#creating_an_entity) ):

### C\#

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore C\# API reference documentation](https://cloud.google.com/dotnet/docs/reference/Google.Cloud.Datastore.V1/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

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

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Go API reference documentation](https://cloud.google.com/go/docs/reference/cloud.google.com/go/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

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

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Java API reference documentation](https://cloud.google.com/java/docs/reference/google-cloud-datastore/latest/history) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

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

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Node.js API reference documentation](https://cloud.google.com/nodejs/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

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

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore PHP API reference documentation](https://googleapis.github.io/google-cloud-php/#/docs/cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
$transaction = $datastore->transaction();
$entity = $transaction->lookup($task->key());
if ($entity === null) {
    $entity = $transaction->insert($task);
    $transaction->commit();
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

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Ruby API reference documentation](/ruby/docs/reference/google-cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

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

As before, a transaction is necessary to handle the case where another user is attempting to create or update an entity with the same string ID. Without a transaction, if the entity does not exist and two users attempt to create it, the second overwrites the first without knowing that it happened.

When a transaction fails, you can have your app retry the transaction until it succeeds, or you can let your users deal with the error by propagating it to your app's user interface level. You do not have to create a retry loop around every transaction.

**Note:** A transaction should happen as quickly as possible to reduce contention with other transactions. Contention will either delay transactions or cause them to fail. As much as possible, prepare data outside of the transaction, then execute the transaction to perform operations that depend on a consistent state. The application should prepare keys for objects used outside the transaction, then fetch the entities inside the transaction.

### Read-only transactions

Finally, you can use a transaction to read a consistent snapshot of the database. This can be useful when you need multiple reads to render a page or to export data that must be consistent. You can create read-only transaction for these cases.

Read-only transactions cannot modify entities, but in return, they do not contend with any other transactions and do not need to be retried. If you perform only reads in a regular, read-write transaction, then that transaction may contend with transaction that modify the same data.

### C\#

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore C\# API reference documentation](https://cloud.google.com/dotnet/docs/reference/Google.Cloud.Datastore.V1/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

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

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Go API reference documentation](https://cloud.google.com/go/docs/reference/cloud.google.com/go/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

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

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Java API reference documentation](https://cloud.google.com/java/docs/reference/google-cloud-datastore/latest/history) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

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

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Node.js API reference documentation](https://cloud.google.com/nodejs/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

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

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore PHP API reference documentation](https://googleapis.github.io/google-cloud-php/#/docs/cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

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

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Python API reference documentation](https://cloud.google.com/python/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

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

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Ruby API reference documentation](/ruby/docs/reference/google-cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

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

  - Learn about [Queries](/datastore/docs/concepts/queries) .
