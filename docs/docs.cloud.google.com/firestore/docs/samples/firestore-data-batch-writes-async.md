Performs a batch update on a Firestore document (async).

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Transactions and batched writes](https://docs.cloud.google.com/firestore/native/docs/manage-data/transactions)
  - [Transactions and batched writes](https://firebase.google.com/docs/firestore/manage-data/transactions)

## Code sample

### Python

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    batch = db.batch()
    
    # Set the data for NYC
    nyc_ref = db.collection("cities").document("NYC")
    batch.set(nyc_ref, {"name": "New York City"})
    
    # Update the population for SF
    sf_ref = db.collection("cities").document("SF")
    batch.update(sf_ref, {"population": 1000000})
    
    # Delete DEN
    den_ref = db.collection("cities").document("DEN")
    batch.delete(den_ref)
    
    # Commit the batch
    await batch.commit()

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](https://docs.cloud.google.com/docs/samples?product=firestore) .
