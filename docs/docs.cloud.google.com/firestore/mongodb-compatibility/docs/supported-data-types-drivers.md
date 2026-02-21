# Supported MongoDB data types and drivers

The following tables list supported MongoDB data types, drivers, and third-party tools for Firestore with MongoDB compatibility.

## Data types

<table>
<thead>
<tr class="header">
<th><strong>BSON Type</strong></th>
<th><strong>Supported</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>32-bit Integer (int)</td>
<td>Yes</td>
</tr>
<tr class="even">
<td>64-bit Integer (long)</td>
<td>Yes</td>
</tr>
<tr class="odd">
<td>Array</td>
<td>Yes</td>
</tr>
<tr class="even">
<td>Binary Data</td>
<td>Yes</td>
</tr>
<tr class="odd">
<td>Boolean</td>
<td>Yes</td>
</tr>
<tr class="even">
<td>Date</td>
<td>Yes</td>
</tr>
<tr class="odd">
<td>DBPointer</td>
<td>No</td>
</tr>
<tr class="even">
<td>DBRef</td>
<td>No</td>
</tr>
<tr class="odd">
<td>Decimal128</td>
<td>Yes</td>
</tr>
<tr class="even">
<td>Double</td>
<td>Yes</td>
</tr>
<tr class="odd">
<td>JavaScript</td>
<td>No</td>
</tr>
<tr class="even">
<td>JavaScript (with scope)</td>
<td>No</td>
</tr>
<tr class="odd">
<td>MaxKey</td>
<td>Yes</td>
</tr>
<tr class="even">
<td>MinKey</td>
<td>Yes</td>
</tr>
<tr class="odd">
<td>Null</td>
<td>Yes</td>
</tr>
<tr class="even">
<td>Object</td>
<td>Yes</td>
</tr>
<tr class="odd">
<td>ObjectId</td>
<td>Yes</td>
</tr>
<tr class="even">
<td>Regular Expression</td>
<td>Yes</td>
</tr>
<tr class="odd">
<td>String</td>
<td>Yes</td>
</tr>
<tr class="even">
<td>Symbol</td>
<td>No</td>
</tr>
<tr class="odd">
<td>Timestamp</td>
<td>Yes</td>
</tr>
<tr class="even">
<td>Undefined</td>
<td>No</td>
</tr>
</tbody>
</table>

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

<table>
<thead>
<tr class="header">
<th><strong>Tool</strong></th>
<th><strong>Description</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><a href="https://www.mongodb.com/docs/database-tools/mongoimport/">mongoimport</a></td>
<td>MongoDB Database Tools</td>
</tr>
<tr class="even">
<td><a href="https://www.mongodb.com/docs/database-tools/mongoexport/">mongoexport</a></td>
<td>MongoDB Database Tools</td>
</tr>
<tr class="odd">
<td><a href="https://www.mongodb.com/docs/database-tools/mongodump/">mongodump</a></td>
<td>MongoDB Database Tools</td>
</tr>
<tr class="even">
<td><a href="https://www.mongodb.com/docs/database-tools/mongorestore/">mongorestore</a></td>
<td>MongoDB Database Tools</td>
</tr>
<tr class="odd">
<td><a href="https://www.mongodb.com/docs/mongodb-shell/">mongosh</a></td>
<td>MongoDB Shell</td>
</tr>
<tr class="even">
<td><a href="https://mongoosejs.com/">Mongoose</a></td>
<td>MongoDB object modeling tool</td>
</tr>
<tr class="odd">
<td><a href="https://www.mongodb.com/products/tools/compass">MongoDB Compass</a></td>
<td>GUI tool for data exploration</td>
</tr>
</tbody>
</table>

**Note:** Some third-party tools require a connection string. To obtain a connection string for your Firestore with MongoDB compatibility database, you can run the [`  firestore databases connection-string  ` command](https://cloud.google.com/sdk/gcloud/reference/firestore/databases/connection-string) using Google Cloud CLI.

## What's next

  - Run the [Quickstart: Create a database and connect to it](/firestore/mongodb-compatibility/docs/create-and-query-database) .
  - Learn about [Behavior differences](/firestore/mongodb-compatibility/docs/behavior-differences) .
  - For a breakdown of supported features depending on MongoDB version, see
      - [Supported features: 8.0](/firestore/mongodb-compatibility/docs/supported-features-80)
      - [Supported features: 7.0](/firestore/mongodb-compatibility/docs/supported-features-70)
      - [Supported features: 6.0](/firestore/mongodb-compatibility/docs/supported-features-60)
      - [Supported features: 5.0](/firestore/mongodb-compatibility/docs/supported-features-50)
      - [Supported features: 4.0](/firestore/mongodb-compatibility/docs/supported-features-40)
      - [Supported features: 3.6](/firestore/mongodb-compatibility/docs/supported-features-36)
