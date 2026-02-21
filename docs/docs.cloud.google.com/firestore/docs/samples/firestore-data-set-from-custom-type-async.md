Add a Firestore document using a custom type (async).

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Add and update data](/firestore/native/docs/manage-data/add-data)
  - [Add data to Cloud Firestore](https://firebase.google.com/docs/firestore/manage-data/add-data)

## Code sample

### Python

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
city = City(name="Los Angeles", state="CA", country="USA")
await db.collection("cities").document("LA").set(city.to_dict())
```

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](/docs/samples?product=firestore) .
