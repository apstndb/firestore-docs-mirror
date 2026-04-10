# Firestore connector for Workflows

[Workflows](https://docs.cloud.google.com/workflows/docs/overview) is a Google Cloud product you can use to create serverless workflows that link series of serverless tasks together in an order you define. Combine functionality from Google Cloud's APIs, serverless products like Cloud Run functions and Cloud Run, and calls to external APIs to create flexible serverless applications.

## Example use case

**Automating low-latency shipment processing**

For example, the architecture below implements a workflow that checks whether a shipment can be executed based on inventory levels. It requests the shipment if the stock levels are sufficient. Otherwise, it requests replenishment from a supplier using their public API. In either case, the workflow immediately responds to the caller about whether the shipment transaction will be accepted.

![low-latency shipment processing diagram](https://cloudx-bricks-prod-bucket.storage.googleapis.com/d73aad6ed6ea3211307c6c72fb5590983959ac52744e9daddd580d5ea386ecf1.svg)

## Firestore connector for Workflows

Workflows supports a connector for Firestore. Use the connector to integrate Firestore into your workflows:

  - [Learn more about connectors.](https://docs.cloud.google.com/workflows/docs/connectors)
  - [See a sample workflow that uses Firestore.](https://docs.cloud.google.com/workflows/docs/reference/googleapis/firestore/Overview)

## What's next

  - [See the Workflows quickstarts.](https://docs.cloud.google.com/workflows/docs/quickstarts)
