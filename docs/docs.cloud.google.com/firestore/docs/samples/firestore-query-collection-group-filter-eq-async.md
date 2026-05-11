---
name: documents/docs.cloud.google.com/firestore/docs/samples/firestore-query-collection-group-filter-eq-async
uri: https://docs.cloud.google.com/firestore/docs/samples/firestore-query-collection-group-filter-eq-async
title: Query a Firestore collection group with an eq filter (async)
description: Query a Firestore collection group with an eq filter (async).
data_source: docs.cloud.google.com
---

Query a Firestore collection group with an eq filter (async).

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Query and filter data](https://docs.cloud.google.com/firestore/native/docs/query-data/queries)

## Code sample

### Python

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    museums = db.collection_group("landmarks").where(
        filter=FieldFilter("type", "==", "museum")
    )
    docs = museums.stream()
    async for doc in docs:
        print(f"{doc.id} => {doc.to_dict()}")

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](https://docs.cloud.google.com/docs/samples?product=firestore) .
