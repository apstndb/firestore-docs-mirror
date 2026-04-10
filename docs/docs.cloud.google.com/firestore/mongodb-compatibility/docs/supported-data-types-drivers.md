# Supported MongoDB data types and drivers

The following tables list supported MongoDB data types, drivers, and third-party tools for Firestore with MongoDB compatibility.

## Data types

| **BSON Type**           | **Supported** |
| ----------------------- | ------------- |
| 32-bit Integer (int)    | Yes           |
| 64-bit Integer (long)   | Yes           |
| Array                   | Yes           |
| Binary Data             | Yes           |
| Boolean                 | Yes           |
| Date                    | Yes           |
| DBPointer               | No            |
| DBRef                   | No            |
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

## Document `     _id    `

The top-level `  _id  ` field in a document must be one of the following types:

  - ObjectId
  - String
  - 64-bit Integer (long)
  - 32-bit Integer (int)
  - Double
  - Binary
  - Object

The total size of the `  _id  ` must not exceed 1500 bytes.

Each values within an Object-typed ID must also be of a supported ID type or an Array of values, each of which is of a supported ID type.

Other BSON types are not supported.

## Languages and MongoDB drivers

Firestore with MongoDB compatibility supports the following driver versions:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Language</strong></th>
<th><strong>Driver versions</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Java</td>
<td>5.x</td>
</tr>
<tr class="even">
<td>Node.js</td>
<td>6.x<br />
5.x</td>
</tr>
<tr class="odd">
<td>Python</td>
<td>4.x<br />
3.x (x ≥ 12)</td>
</tr>
<tr class="even">
<td>Go</td>
<td>2.x</td>
</tr>
<tr class="odd">
<td>C#</td>
<td>3.x</td>
</tr>
<tr class="even">
<td>Ruby</td>
<td>2.x (x ≥ 16)</td>
</tr>
</tbody>
</table>

### OIDC authentication support

The Go, C\#, and Ruby drivers support OpenID Connect (OIDC) authentication from Google Cloud for all supported driver versions.

The Java, Node.js, and Python drivers support OIDC authentication from Google Cloud starting with the following driver versions:

  - Java: 4.10
  - Node.js: 6.7
  - Python: 4.7

## Third-party tools

Firestore with MongoDB compatibility supports third-party tools described in this section.

| **Tool**                                                                  | **Description**               |
| ------------------------------------------------------------------------- | ----------------------------- |
| [mongoimport](https://www.mongodb.com/docs/database-tools/mongoimport/)   | MongoDB Database Tools        |
| [mongoexport](https://www.mongodb.com/docs/database-tools/mongoexport/)   | MongoDB Database Tools        |
| [mongodump](https://www.mongodb.com/docs/database-tools/mongodump/)       | MongoDB Database Tools        |
| [mongorestore](https://www.mongodb.com/docs/database-tools/mongorestore/) | MongoDB Database Tools        |
| [mongosh](https://www.mongodb.com/docs/mongodb-shell/)                    | MongoDB Shell                 |
| [Mongoose](https://mongoosejs.com/)                                       | MongoDB object modeling tool  |
| [MongoDB Compass](https://www.mongodb.com/products/tools/compass)         | GUI tool for data exploration |

**Note:** Some third-party tools require a connection string. To obtain a connection string for your Firestore with MongoDB compatibility database, you can run the [`  firestore databases connection-string  ` command](https://cloud.google.com/sdk/gcloud/reference/firestore/databases/connection-string) using Google Cloud CLI.

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
