---
name: documents/docs.cloud.google.com/firestore/mongodb-compatibility/docs/supported-data-types-drivers
uri: https://docs.cloud.google.com/firestore/mongodb-compatibility/docs/supported-data-types-drivers
title: Supported MongoDB data types and drivers
description: Learn about supported MongoDB data types and drivers for Firestore with MongoDB compatibility.
data_source: docs.cloud.google.com
---

# Supported MongoDB data types and drivers

The following tables list supported MongoDB data types, drivers, and third-party tools for Firestore with MongoDB compatibility.

## Data types

| **BSON Type**           | **Supported** |
|-------------------------|---------------|
| 32-bit Integer          | Yes           |
| 64-bit Integer          | Yes           |
| Array                   | Yes           |
| Binary Data             | Yes           |
| Boolean                 | Yes           |
| Date                    | Yes           |
| DBPointer               | No            |
| Decimal128              | Yes           |
| Double                  | Yes           |
| JavaScript              | No            |
| JavaScript (with scope) | No            |
| MaxKey                  | Yes           |
| MinKey                  | Yes           |
| Null                    | Yes           |
| Object                  | Yes           |
| ObjectId                | Yes           |
| Regular Expression      | Yes           |
| String                  | Yes           |
| Symbol                  | No            |
| Timestamp               | Yes           |
| Undefined               | No            |

## Document `_id`

The top-level `_id` field in a document must be one of the following types:

- ObjectId
- String
- 64-bit Integer
- 32-bit Integer
- Double
- Binary
- Object
- Boolean

The total size of the `_id` must not exceed 1500 bytes.

Each values within an Object-typed ID must also be of a supported ID type or an Array of values, each of which is of a supported ID type.

Other BSON types are not supported.

## Languages and MongoDB drivers

Firestore with MongoDB compatibility supports the following driver versions:

| **Language** | **Driver versions** |
|--------------|---------------------|
| Java         | 5.x                 |
| Node.js      | 6.x 5.x             |
| Python       | 4.x 3.x (x ≥ 12)    |
| Go           | 2.x                 |
| C#           | 3.x                 |
| Ruby         | 2.x (x ≥ 16)        |

### OIDC authentication support

The Go, C#, and Ruby drivers support OpenID Connect (OIDC) authentication from Google Cloud for all supported driver versions.

The Java, Node.js, and Python drivers support OIDC authentication from Google Cloud starting with the following driver versions:

- Java: 4.10
- Node.js: 6.7
- Python: 4.7

## Third-party tools

Firestore with MongoDB compatibility supports third-party tools described in this section.

| **Tool**                                                                  | **Description**               | **Notes**                                                                                                                  |
|---------------------------------------------------------------------------|-------------------------------|----------------------------------------------------------------------------------------------------------------------------|
| [mongoimport](https://www.mongodb.com/docs/database-tools/mongoimport/)   | MongoDB Database Tools        | See [Bulk data loading](https://docs.cloud.google.com/firestore/mongodb-compatibility/docs/bulk-data-loading#mongoimport)  |
| [mongoexport](https://www.mongodb.com/docs/database-tools/mongoexport/)   | MongoDB Database Tools        |                                                                                                                            |
| [mongodump](https://www.mongodb.com/docs/database-tools/mongodump/)       | MongoDB Database Tools        |                                                                                                                            |
| [mongorestore](https://www.mongodb.com/docs/database-tools/mongorestore/) | MongoDB Database Tools        | See [Bulk data loading](https://docs.cloud.google.com/firestore/mongodb-compatibility/docs/bulk-data-loading#mongorestore) |
| [mongosh](https://www.mongodb.com/docs/mongodb-shell/)                    | MongoDB Shell                 |                                                                                                                            |
| [Mongoose](https://mongoosejs.com/)                                       | MongoDB object modeling tool  |                                                                                                                            |
| [MongoDB Compass](https://www.mongodb.com/products/tools/compass)         | GUI tool for data exploration |                                                                                                                            |

> **Note:** Some third-party tools require a connection string. To obtain a connection string for your Firestore with MongoDB compatibility database, you can run the [`firestore databases connection-string` command](https://cloud.google.com/sdk/gcloud/reference/firestore/databases/connection-string) using Google Cloud CLI.

## What's next

- Run the [Quickstart: Create a database and connect to it](https://docs.cloud.google.com/firestore/mongodb-compatibility/docs/create-and-query-database) .
- Learn about [Behavior differences](https://docs.cloud.google.com/firestore/mongodb-compatibility/docs/behavior-differences) .
- For a breakdown of supported features depending on MongoDB version, see
  - [Supported features: 8.0](https://docs.cloud.google.com/firestore/mongodb-compatibility/docs/supported-features-80)
  - [Supported features: 7.0](https://docs.cloud.google.com/firestore/mongodb-compatibility/docs/supported-features-70)
  - [Supported features: 6.0](https://docs.cloud.google.com/firestore/mongodb-compatibility/docs/supported-features-60)
  - [Supported features: 5.0](https://docs.cloud.google.com/firestore/mongodb-compatibility/docs/supported-features-50)
  - [Supported features: 4.0](https://docs.cloud.google.com/firestore/mongodb-compatibility/docs/supported-features-40)
  - [Supported features: 3.6](https://docs.cloud.google.com/firestore/mongodb-compatibility/docs/supported-features-36)
