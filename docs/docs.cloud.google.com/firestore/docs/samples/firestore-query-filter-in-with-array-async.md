---
name: documents/docs.cloud.google.com/firestore/docs/samples/firestore-query-filter-in-with-array-async
uri: https://docs.cloud.google.com/firestore/docs/samples/firestore-query-filter-in-with-array-async
title: Query a Firestore collection with an in array filter (async)
description: Query a Firestore collection with an in array filter (async).
data_source: docs.cloud.google.com
update_time: "2026-05-09T06:58:44Z"
---

Query a Firestore collection with an in array filter (async).

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Query and filter data](https://docs.cloud.google.com/firestore/native/docs/query-data/queries)

## Code sample

### Python

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    cities_ref = db.collection("cities")
    
    query = cities_ref.where(
        filter=FieldFilter("regions", "in", [["west_coast"], ["east_coast"]])
    )
    return query

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](https://docs.cloud.google.com/docs/samples?product=firestore) .
