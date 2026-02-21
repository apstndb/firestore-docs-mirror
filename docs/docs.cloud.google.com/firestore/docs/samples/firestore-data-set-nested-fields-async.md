Add a Firestore document with nested fields (async).

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Add and update data](/firestore/native/docs/manage-data/add-data)
  - [Add data to Cloud Firestore](https://firebase.google.com/docs/firestore/manage-data/add-data)

## Code sample

### Python

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
# Create an initial document to update
frank_ref = db.collection("users").document("frank")
await frank_ref.set(
    {
        "name": "Frank",
        "favorites": {"food": "Pizza", "color": "Blue", "subject": "Recess"},
        "age": 12,
    }
)

# Update age and favorite color
await frank_ref.update({"age": 13, "favorites.color": "Red"})
```

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](/docs/samples?product=firestore) .
