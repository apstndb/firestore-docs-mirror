Use an update in a transaction.

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Cloud Datastore Transactions](/datastore/docs/concepts/cloud-datastore-transactions)
  - [Transactions](/datastore/docs/concepts/transactions)

## Code sample

### C\#

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode C\# API reference documentation](https://cloud.google.com/dotnet/docs/reference/Google.Cloud.Datastore.V1/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

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

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Go API reference documentation](https://cloud.google.com/go/docs/reference/cloud.google.com/go/datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

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

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Java API reference documentation](https://cloud.google.com/java/docs/reference/google-cloud-datastore/latest/history) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

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

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Node.js API reference documentation](https://cloud.google.com/nodejs/docs/reference/datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

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

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode PHP API reference documentation](https://googleapis.github.io/google-cloud-php/#/docs/cloud-datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

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

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Python API reference documentation](https://cloud.google.com/python/docs/reference/datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

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

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Ruby API reference documentation](/ruby/docs/reference/google-cloud-datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

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

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](/docs/samples?product=datastore) .
