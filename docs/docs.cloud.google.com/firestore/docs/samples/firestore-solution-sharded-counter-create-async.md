Create a Firestore sharded counter (async).

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Distributed counters](https://firebase.google.com/docs/firestore/solutions/counters)
  - [Support frequent and distributed counters](/firestore/native/docs/solutions/counters)

## Code sample

### Python

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
async def init_counter(self, doc_ref):
    """
    Create a given number of shards as
    subcollection of specified document.
    """
    col_ref = doc_ref.collection("shards")

    # Initialize each shard with count=0
    for num in range(self._num_shards):
        shard = Shard()
        await col_ref.document(str(num)).set(shard.to_dict())
```

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](/docs/samples?product=firestore) .
