Conditionally updating a Firestore document in a transaction (async).

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Transactions and batched writes](/firestore/native/docs/manage-data/transactions)
  - [Transactions and batched writes](https://firebase.google.com/docs/firestore/manage-data/transactions)

## Code sample

### Python

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
transaction = db.transaction()
city_ref = db.collection("cities").document("SF")

@firestore.async_transactional
async def update_in_transaction(transaction, city_ref):
    snapshot = await city_ref.get(transaction=transaction)
    new_population = snapshot.get("population") + 1

    if new_population < 1000000:
        transaction.update(city_ref, {"population": new_population})
        return True
    else:
        return False

result = await update_in_transaction(transaction, city_ref)
if result:
    print("Population updated")
else:
    print("Sorry! Population is too big.")
```

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](/docs/samples?product=firestore) .
