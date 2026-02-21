Get Firestore Documents created from custom classes (async).

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Get data with Cloud Firestore](https://firebase.google.com/docs/firestore/query-data/get-data)
  - [Getting data](/firestore/native/docs/query-data/get-data)
  - [Perform simple and compound queries in Cloud Firestore](https://firebase.google.com/docs/firestore/query-data/queries)
  - [Query and filter data](/firestore/native/docs/query-data/queries)

## Code sample

### Python

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
cities_ref = db.collection("cities")
await cities_ref.document("BJ").set(
    City("Beijing", None, "China", True, 21500000, ["hebei"]).to_dict()
)
await cities_ref.document("SF").set(
    City(
        "San Francisco", "CA", "USA", False, 860000, ["west_coast", "norcal"]
    ).to_dict()
)
await cities_ref.document("LA").set(
    City(
        "Los Angeles", "CA", "USA", False, 3900000, ["west_coast", "socal"]
    ).to_dict()
)
await cities_ref.document("DC").set(
    City("Washington D.C.", None, "USA", True, 680000, ["east_coast"]).to_dict()
)
await cities_ref.document("TOK").set(
    City("Tokyo", None, "Japan", True, 9000000, ["kanto", "honshu"]).to_dict()
)
```

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](/docs/samples?product=firestore) .
