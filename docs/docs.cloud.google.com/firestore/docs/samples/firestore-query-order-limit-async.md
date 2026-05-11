---
name: documents/docs.cloud.google.com/firestore/docs/samples/firestore-query-order-limit-async
uri: https://docs.cloud.google.com/firestore/docs/samples/firestore-query-order-limit-async
title: Ordering and limiting Firestore queries (async)
description: Ordering and limiting Firestore queries (async).
data_source: docs.cloud.google.com
---

Ordering and limiting Firestore queries (async).

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Order and limit data](https://docs.cloud.google.com/firestore/native/docs/query-data/order-limit-data)

## Code sample

### Python

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    cities_ref = db.collection("cities")
    query = cities_ref.order_by("name").limit_to_last(2)
    results = await query.get()

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](https://docs.cloud.google.com/docs/samples?product=firestore) .
