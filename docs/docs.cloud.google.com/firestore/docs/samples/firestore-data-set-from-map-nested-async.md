Add a Firestore document using a nested map (async).

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Add and update data](https://docs.cloud.google.com/firestore/native/docs/manage-data/add-data)

## Code sample

### Python

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    data = {
        "stringExample": "Hello, World!",
        "booleanExample": True,
        "numberExample": 3.14159265,
        "dateExample": datetime.datetime.now(tz=datetime.timezone.utc),
        "arrayExample": [5, True, "hello"],
        "nullExample": None,
        "objectExample": {"a": 5, "b": True},
    }
    
    await db.collection("data").document("one").set(data)

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](https://docs.cloud.google.com/docs/samples?product=firestore) .
