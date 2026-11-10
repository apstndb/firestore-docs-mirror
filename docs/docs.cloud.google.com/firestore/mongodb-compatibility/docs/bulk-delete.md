---
name: documents/docs.cloud.google.com/firestore/mongodb-compatibility/docs/bulk-delete
uri: https://docs.cloud.google.com/firestore/mongodb-compatibility/docs/bulk-delete
title: Bulk delete data
description: Bulk-delete data from Firestore with MongoDB compatibility.
data_source: docs.cloud.google.com
---

# Bulk delete data

To bulk delete data from your database, we recommend that you use the `drop()` command.

## `drop()` command

For Firestore Enterprise edition databases with MongoDB compatibility, use the MongoDB `drop()` command as the primary way to delete an entire collection.

### Billing for drop operations

A flat rate of 1 write unit is charged for all drop collection operations.
