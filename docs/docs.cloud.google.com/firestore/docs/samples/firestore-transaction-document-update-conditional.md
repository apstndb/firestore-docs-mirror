Conditionally updating a Firestore document in a transaction

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Transactions and batched writes](/firestore/native/docs/manage-data/transactions)
  - [Transactions and batched writes](https://firebase.google.com/docs/firestore/manage-data/transactions)

## Code sample

### C\#

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
DocumentReference cityRef = db.Collection("cities").Document("SF");
bool transactionResult = await db.RunTransactionAsync(async transaction =>
{
    DocumentSnapshot snapshot = await transaction.GetSnapshotAsync(cityRef);
    long newPopulation = snapshot.GetValue<long>("Population") + 1;
    if (newPopulation <= 1000000)
    {
        Dictionary<string, object> updates = new Dictionary<string, object>
        {
            { "Population", newPopulation}
        };
        transaction.Update(cityRef, updates);
        return true;
    }
    else
    {
        return false;
    }
});

if (transactionResult)
{
    Console.WriteLine("Population updated successfully.");
}
else
{
    Console.WriteLine("Sorry! Population is too big.");
}
```

### Go

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` go
import (
 "context"
 "errors"
 "log"

 "cloud.google.com/go/firestore"
)

func infoTransaction(ctx context.Context, client *firestore.Client) (int64, error) {
 var updatedPop int64
 ref := client.Collection("cities").Doc("SF")
 err := client.RunTransaction(ctx, func(ctx context.Context, tx *firestore.Transaction) error {
     doc, err := tx.Get(ref)
     if err != nil {
         return err
     }
     pop, err := doc.DataAt("population")
     if err != nil {
         return err
     }
     newpop := pop.(int64) + 1
     if newpop <= 1000000 {
         err := tx.Set(ref, map[string]interface{}{
             "population": newpop,
         }, firestore.MergeAll)
         if err == nil {
             updatedPop = newpop
         }
         return err
     }
     return errors.New("population is too big")
 })
 if err != nil {
     // Handle any errors in an appropriate way, such as returning them.
     log.Printf("An error has occurred: %s", err)
 }
 return updatedPop, err
}
```

### Java

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
final DocumentReference docRef = db.collection("cities").document("SF");
ApiFuture<String> futureTransaction =
    db.runTransaction(
        transaction -> {
          DocumentSnapshot snapshot = transaction.get(docRef).get();
          Long newPopulation = snapshot.getLong("population") + 1;
          // conditionally update based on current population
          if (newPopulation <= 1000000L) {
            transaction.update(docRef, "population", newPopulation);
            return "Population increased to " + newPopulation;
          } else {
            throw new Exception("Sorry! Population is too big.");
          }
        });
// Print information retrieved from transaction
System.out.println(futureTransaction.get());
```

### Node.js

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` javascript
const cityRef = db.collection('cities').doc('SF');
try {
  const res = await db.runTransaction(async t => {
    const doc = await t.get(cityRef);
    const newPopulation = doc.data().population + 1;
    if (newPopulation <= 1000000) {
      await t.update(cityRef, { population: newPopulation });
      return `Population increased to ${newPopulation}`;
    } else {
      throw 'Sorry! Population is too big.';
    }
  });
  console.log('Transaction success', res);
} catch (e) {
  console.log('Transaction failure:', e);
}
```

### PHP

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
$cityRef = $db->collection('samples/php/cities')->document('SF');
$transactionResult = $db->runTransaction(function (Transaction $transaction) use ($cityRef) {
    $snapshot = $transaction->snapshot($cityRef);
    $newPopulation = $snapshot['population'] + 1;
    if ($newPopulation <= 1000000) {
        $transaction->update($cityRef, [
            ['path' => 'population', 'value' => $newPopulation]
        ]);
        return true;
    } else {
        return false;
    }
});

if ($transactionResult) {
    printf('Population updated successfully.' . PHP_EOL);
} else {
    printf('Sorry! Population is too big.' . PHP_EOL);
}
```

### Python

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
transaction = db.transaction()
city_ref = db.collection("cities").document("SF")

@firestore.transactional
def update_in_transaction(transaction, city_ref):
    snapshot = city_ref.get(transaction=transaction)
    new_population = snapshot.get("population") + 1

    if new_population < 1000000:
        transaction.update(city_ref, {"population": new_population})
        return True
    else:
        return False

result = update_in_transaction(transaction, city_ref)
if result:
    print("Population updated")
else:
    print("Sorry! Population is too big.")
```

### Ruby

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
city_ref = firestore.doc "#{collection_path}/SF"

updated = firestore.transaction do |tx|
  new_population = tx.get(city_ref).data[:population] + 1
  if new_population < 1_000_000
    tx.update city_ref, { population: new_population }
    true
  end
end

if updated
  puts "Population updated!"
else
  puts "Sorry! Population is too big."
end
```

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](/docs/samples?product=firestore) .
