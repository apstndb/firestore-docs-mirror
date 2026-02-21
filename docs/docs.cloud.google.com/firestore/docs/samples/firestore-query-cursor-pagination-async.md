Use start cursors and limits to paginate Firestore collections (async).

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Paginate data with query cursors](/firestore/native/docs/query-data/query-cursors)
  - [Paginate data with query cursors](https://firebase.google.com/docs/firestore/query-data/query-cursors)

## Code sample

### Python

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
cities_ref = db.collection("cities")
first_query = cities_ref.order_by("population").limit(3)

# Get the last document from the results
docs = [d async for d in first_query.stream()]
last_doc = list(docs)[-1]

# Construct a new query starting at this document
# Note: this will not have the desired effect if
# multiple cities have the exact same population value
last_pop = last_doc.to_dict()["population"]

next_query = (
    cities_ref.order_by("population").start_after({"population": last_pop}).limit(3)
)
# Use the query for pagination
# ...
```

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](/docs/samples?product=firestore) .
