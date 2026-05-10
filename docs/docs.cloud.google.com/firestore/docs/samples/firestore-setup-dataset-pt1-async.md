---
name: documents/docs.cloud.google.com/firestore/docs/samples/firestore-setup-dataset-pt1-async
uri: https://docs.cloud.google.com/firestore/docs/samples/firestore-setup-dataset-pt1-async
title: Add data to Firestore (async)
description: Add data to Firestore (async).
data_source: docs.cloud.google.com
update_time: "2026-05-09T06:58:44Z"
---

Add data to Firestore (async).

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Quickstart: Create a Firestore database by using a server client library](https://docs.cloud.google.com/firestore/native/docs/create-database-server-client-library)

## Code sample

### Python

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    doc_ref = db.collection("users").document("alovelace")
    await doc_ref.set({"first": "Ada", "last": "Lovelace", "born": 1815})

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](https://docs.cloud.google.com/docs/samples?product=firestore) .
