Create a collection of Firestore documents (async).

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Perform simple and compound queries in Cloud Firestore](https://firebase.google.com/docs/firestore/query-data/queries)
  - [Query and filter data](/firestore/native/docs/query-data/queries)

## Code sample

### Python

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
cities = db.collection("cities")

sf_landmarks = cities.document("SF").collection("landmarks")
await sf_landmarks.document().set({"name": "Golden Gate Bridge", "type": "bridge"})
await sf_landmarks.document().set({"name": "Legion of Honor", "type": "museum"})
la_landmarks = cities.document("LA").collection("landmarks")
await la_landmarks.document().set({"name": "Griffith Park", "type": "park"})
await la_landmarks.document().set({"name": "The Getty", "type": "museum"})
dc_landmarks = cities.document("DC").collection("landmarks")
await dc_landmarks.document().set({"name": "Lincoln Memorial", "type": "memorial"})
await dc_landmarks.document().set(
    {"name": "National Air and Space Museum", "type": "museum"}
)
tok_landmarks = cities.document("TOK").collection("landmarks")
await tok_landmarks.document().set({"name": "Ueno Park", "type": "park"})
await tok_landmarks.document().set(
    {"name": "National Museum of Nature and Science", "type": "museum"}
)
bj_landmarks = cities.document("BJ").collection("landmarks")
await bj_landmarks.document().set({"name": "Jingshan Park", "type": "park"})
await bj_landmarks.document().set(
    {"name": "Beijing Ancient Observatory", "type": "museum"}
)
```

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](/docs/samples?product=firestore) .
