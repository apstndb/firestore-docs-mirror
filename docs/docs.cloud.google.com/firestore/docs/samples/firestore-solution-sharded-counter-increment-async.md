Incrementing a Firestore document field while using shards (async).

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Distributed counters](https://firebase.google.com/docs/firestore/solutions/counters)
  - [Support frequent and distributed counters](/firestore/native/docs/solutions/counters)

## Code sample

### Python

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
async def increment_counter(self, doc_ref):
    """Increment a randomly picked shard."""
    doc_id = random.randint(0, self._num_shards - 1)

    shard_ref = doc_ref.collection("shards").document(str(doc_id))
    return await shard_ref.update({"count": firestore.Increment(1)})
```

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](/docs/samples?product=firestore) .
