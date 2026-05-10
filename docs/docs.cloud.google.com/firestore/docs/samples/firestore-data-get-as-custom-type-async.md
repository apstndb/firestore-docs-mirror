---
name: documents/docs.cloud.google.com/firestore/docs/samples/firestore-data-get-as-custom-type-async
uri: https://docs.cloud.google.com/firestore/docs/samples/firestore-data-get-as-custom-type-async
title: Get a Firestore document using custom types (async)
description: Get a Firestore document using custom types (async).
data_source: docs.cloud.google.com
update_time: "2026-05-09T06:59:00Z"
---

Get a Firestore document using custom types (async).

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Getting data](https://docs.cloud.google.com/firestore/native/docs/query-data/get-data)

## Code sample

### Python

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    doc_ref = db.collection("cities").document("BJ")
    
    doc = await doc_ref.get()
    city = City.from_dict(doc.to_dict())
    print(city)

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](https://docs.cloud.google.com/docs/samples?product=firestore) .
