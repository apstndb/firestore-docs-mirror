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

> **Preview**
> 
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

For Firestore Enterprise edition databases with MongoDB compatibility, use the MongoDB `drop()` command as the primary way to delete an entire collection.

### Billing for drop operations

A flat rate of 1 write unit is charged for all drop collection operations.
