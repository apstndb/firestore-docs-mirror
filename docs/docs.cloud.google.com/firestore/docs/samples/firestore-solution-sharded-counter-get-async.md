Getting a Firestore document while using shards (async).

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Distributed counters](https://firebase.google.com/docs/firestore/solutions/counters)
  - [Support frequent and distributed counters](/firestore/native/docs/solutions/counters)

## Code sample

### Python

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
async def get_count(self, doc_ref):
    """Return a total count across all shards."""
    total = 0
    shards = doc_ref.collection("shards").list_documents()
    async for shard in shards:
        total += (await shard.get()).to_dict().get("count", 0)
    return total
```

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](/docs/samples?product=firestore) .
