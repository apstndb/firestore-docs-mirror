Updating a Firestore document in a transaction (async).

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Transactions and batched writes](https://docs.cloud.google.com/firestore/native/docs/manage-data/transactions)
  - [Transactions and batched writes](https://firebase.google.com/docs/firestore/manage-data/transactions)

## Code sample

### Python

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    transaction = db.transaction()
    city_ref = db.collection("cities").document("SF")
    
    @firestore.async_transactional
    async def update_in_transaction(transaction, city_ref):
        snapshot = await city_ref.get(transaction=transaction)
        transaction.update(city_ref, {"population": snapshot.get("population") + 1})
    
    await update_in_transaction(transaction, city_ref)

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](https://docs.cloud.google.com/docs/samples?product=firestore) .
