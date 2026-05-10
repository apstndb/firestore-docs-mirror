---
name: documents/docs.cloud.google.com/firestore/docs/reference/rest/Shared.Types/QueryScope
uri: https://docs.cloud.google.com/firestore/docs/reference/rest/Shared.Types/QueryScope
title: QueryScope
description: A cloud-hosted NoSQL database that's simple enough for rapid prototyping yet scalable and flexible enough to grow to any size.
data_source: docs.cloud.google.com
update_time: "2025-10-17T23:18:41Z"
---

Query Scope defines the scope at which a query is run. This is specified on a StructuredQuery's `from` field.

Enums

`QUERY_SCOPE_UNSPECIFIED`

The query scope is unspecified. Not a valid option.

`COLLECTION`

Indexes with a collection query scope specified allow queries against a collection that is the child of a specific document, specified at query time, and that has the collection ID specified by the index.

`COLLECTION_GROUP`

Indexes with a collection group query scope specified allow queries against all collections that has the collection ID specified by the index.

`COLLECTION_RECURSIVE`

Include all the collections's ancestor in the index. Only available for Datastore Mode databases.
