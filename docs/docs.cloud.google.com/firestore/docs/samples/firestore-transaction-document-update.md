Updating a Firestore document in a transaction

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Transactions and batched writes](/firestore/native/docs/manage-data/transactions)
  - [Transactions and batched writes](https://firebase.google.com/docs/firestore/manage-data/transactions)

## Code sample

### C\#

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
DocumentReference cityRef = db.Collection("cities").Document("SF");
await db.RunTransactionAsync(async transaction =>
{
    DocumentSnapshot snapshot = await transaction.GetSnapshotAsync(cityRef);
    long newPopulation = snapshot.GetValue<long>("Population") + 1;
    Dictionary<string, object> updates = new Dictionary<string, object>
    {
        { "Population", newPopulation}
    };
    transaction.Update(cityRef, updates);
});
```

### Go

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` go
import (
 "context"
 "log"

 "cloud.google.com/go/firestore"
)

func runSimpleTransaction(ctx context.Context, client *firestore.Client) error {
 // ...

 ref := client.Collection("cities").Doc("SF")
 err := client.RunTransaction(ctx, func(ctx context.Context, tx *firestore.Transaction) error {
     doc, err := tx.Get(ref) // tx.Get, NOT ref.Get!
     if err != nil {
         return err
     }
     pop, err := doc.DataAt("population")
     if err != nil {
         return err
     }
     return tx.Set(ref, map[string]interface{}{
         "population": pop.(int64) + 1,
     }, firestore.MergeAll)
 })
 if err != nil {
     // Handle any errors appropriately in this section.
     log.Printf("An error has occurred: %s", err)
 }

 return err
}
```

### Java

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
// Initialize doc
final DocumentReference docRef = db.collection("cities").document("SF");
City city = new City("SF");
city.setCountry("USA");
city.setPopulation(860000L);
docRef.set(city).get();

// run an asynchronous transaction
ApiFuture<Void> futureTransaction =
    db.runTransaction(
        transaction -> {
          // retrieve document and increment population field
          DocumentSnapshot snapshot = transaction.get(docRef).get();
          long oldPopulation = snapshot.getLong("population");
          transaction.update(docRef, "population", oldPopulation + 1);
          return null;
        });
// block on transaction operation using transaction.get()
```

### Node.js

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` javascript
// Initialize document
const cityRef = db.collection('cities').doc('SF');
await cityRef.set({
  name: 'San Francisco',
  state: 'CA',
  country: 'USA',
  capital: false,
  population: 860000
});

try {
  await db.runTransaction(async (t) => {
    const doc = await t.get(cityRef);

    // Add one person to the city population.
    // Note: this could be done without a transaction
    //       by updating the population using FieldValue.increment()
    const newPopulation = doc.data().population + 1;
    t.update(cityRef, {population: newPopulation});
  });

  console.log('Transaction success!');
} catch (e) {
  console.log('Transaction failure:', e);
}
```

### PHP

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
$cityRef = $db->collection('samples/php/cities')->document('SF');
$db->runTransaction(function (Transaction $transaction) use ($cityRef) {
    $snapshot = $transaction->snapshot($cityRef);
    $newPopulation = $snapshot['population'] + 1;
    $transaction->update($cityRef, [
        ['path' => 'population', 'value' => $newPopulation]
    ]);
});
```

### Python

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
transaction = db.transaction()
city_ref = db.collection("cities").document("SF")

@firestore.transactional
def update_in_transaction(transaction, city_ref):
    snapshot = city_ref.get(transaction=transaction)
    transaction.update(city_ref, {"population": snapshot.get("population") + 1})

update_in_transaction(transaction, city_ref)
```

### Ruby

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
city_ref = firestore.doc "#{collection_path}/SF"

firestore.transaction do |tx|
  new_population = tx.get(city_ref).data[:population] + 1
  puts "New population is #{new_population}."
  tx.update city_ref, { population: new_population }
end
```

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](/docs/samples?product=firestore) .
