---
name: documents/docs.cloud.google.com/firestore/docs/samples/firestore-query-order-with-filter-async
uri: https://docs.cloud.google.com/firestore/docs/samples/firestore-query-order-with-filter-async
title: Ordering a Firestore query with a filter (async)
description: Ordering a Firestore query with a filter (async).
data_source: docs.cloud.google.com
update_time: "2026-05-09T06:58:44Z"
---

Ordering a Firestore query with a filter (async).

## Code sample

### Python

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    cities_ref = db.collection("cities")
    query = cities_ref.where(filter=FieldFilter("population", ">", 2500000)).order_by(
        "population"
    )
    results = query.stream()

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](https://docs.cloud.google.com/docs/samples?product=firestore) .
