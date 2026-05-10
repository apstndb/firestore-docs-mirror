---
name: documents/docs.cloud.google.com/firestore/docs/samples/firestore-solution-sharded-counter-increment-async
uri: https://docs.cloud.google.com/firestore/docs/samples/firestore-solution-sharded-counter-increment-async
title: Incrementing a Firestore document field while using shards (async)
description: Incrementing a Firestore document field while using shards (async).
data_source: docs.cloud.google.com
update_time: "2026-05-09T06:58:44Z"
---

Incrementing a Firestore document field while using shards (async).

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Support frequent and distributed counters](https://docs.cloud.google.com/firestore/native/docs/solutions/counters)

## Code sample

### Python

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    async def increment_counter(self, doc_ref):
        """Increment a randomly picked shard."""
        doc_id = random.randint(0, self._num_shards - 1)
    
        shard_ref = doc_ref.collection("shards").document(str(doc_id))
        return await shard_ref.update({"count": firestore.Increment(1)})

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](https://docs.cloud.google.com/docs/samples?product=firestore) .
