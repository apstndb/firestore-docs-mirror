Create custom shard and counter types for Firestore distributed counters (async).

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Distributed counters](https://firebase.google.com/docs/firestore/solutions/counters)
  - [Support frequent and distributed counters](/firestore/native/docs/solutions/counters)

## Code sample

### Python

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
import random

from google.cloud import firestore


class Shard:
    """
    A shard is a distributed counter. Each shard can support being incremented
    once per second. Multiple shards are needed within a Counter to allow
    more frequent incrementing.
    """

    def __init__(self):
        self._count = 0

    def to_dict(self):
        return {"count": self._count}


class Counter:
    """
    A counter stores a collection of shards which are
    summed to return a total count. This allows for more
    frequent incrementing than a single document.
    """

    def __init__(self, num_shards):
        self._num_shards = num_shards
```

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](/docs/samples?product=firestore) .
