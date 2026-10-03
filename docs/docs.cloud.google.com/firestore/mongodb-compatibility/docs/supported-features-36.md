---
name: documents/docs.cloud.google.com/firestore/mongodb-compatibility/docs/supported-features-36
uri: https://docs.cloud.google.com/firestore/mongodb-compatibility/docs/supported-features-36
title: 'Supported features: 3.6'
description: Explore the MongoDB 3.6 features supported by Firestore with MongoDB compatibility, including query and projection operators, update operators, aggregation pipeline operators, and database commands.
data_source: docs.cloud.google.com
---

# Supported features: 3.6

The following tables include a breakdown of MongoDB 3.6 features supported by Firestore with MongoDB compatibility. For differences in behavior, see [Behavior differences](https://docs.cloud.google.com/firestore/mongodb-compatibility/docs/behavior-differences) .

## Query and projection operators

Firestore with MongoDB compatibility supports the following query and projection operators:

### Array operators

| **Operator** | **Supported** |
|--------------|---------------|
| `$all`       | Yes           |
| `$elemMatch` | Yes           |
| `$size`      | Yes           |

### Bitwise operators

| **Operator**    | **Supported** |
|-----------------|---------------|
| `$bitsAllClear` | No            |
| `$bitsAllSet`   | No            |
| `$bitsAnyClear` | No            |
| `$bitsAnySet`   | No            |

### Comment operator

| **Operator** | **Supported** |
|--------------|---------------|
| `$comment`   | No            |

### Comparison operators

| **Operator** | **Supported** |
|--------------|---------------|
| `$eq`        | Yes           |
| `$gt`        | Yes           |
| `$gte`       | Yes           |
| `$in`        | Yes           |
| `$lt`        | Yes           |
| `$lte`       | Yes           |
| `$ne`        | Yes           |
| `$nin`       | Yes           |

### Element operators

| **Operator** | **Supported** |
|--------------|---------------|
| `$exists`    | Yes           |
| `$type`      | Yes           |

### Evaluation query operators

| **Operator**  | **Supported** |
|---------------|---------------|
| `$expr`       | Yes           |
| `$jsonSchema` | No            |
| `$mod`        | Yes           |
| `$regex`      | Yes           |
| `$text`       | Yes           |
| `$where`      | No            |

### Logical operators

| **Operator** | **Supported** |
|--------------|---------------|
| `$and`       | Yes           |
| `$nor`       | Yes           |
| `$not`       | Yes           |
| `$or`        | Yes           |

### Projection operators

| **Operator** | **Supported**                    |
|--------------|----------------------------------|
| `$`          | Yes                              |
| `$elemMatch` | Yes                              |
| `$meta`      | Partial (supports \`textScore\`) |
| `$slice`     | Yes                              |

## Update operators

Firestore with MongoDB compatibility supports the following update operators.

### Array operators

| **Operator**      | **Supported** |
|-------------------|---------------|
| `$`               | Yes           |
| `$[]`             | Yes           |
| `$[<identifier>]` | Yes           |
| `$addToSet`       | Yes           |
| `$pop`            | Yes           |
| `$pull`           | Yes           |
| `$pullAll`        | Yes           |
| `$push`           | Yes           |

### Bitwise operators

| **Operator** | **Supported** |
|--------------|---------------|
| `$bit`       | Yes           |

### Field operators

| **Operator**   | **Supported** |
|----------------|---------------|
| `$currentDate` | Yes           |
| `$inc`         | Yes           |
| `$max`         | Yes           |
| `$min`         | Yes           |
| `$mul`         | Yes           |
| `$rename`      | Yes           |
| `$setOnInsert` | Yes           |

### Update modifiers

| **Modifier** | **Supported** |
|--------------|---------------|
| `$each`      | Yes           |
| `$position`  | Yes           |
| `$slice`     | Yes           |
| `$sort`      | Yes           |

## Aggregation pipeline operators

Firestore with MongoDB compatibility supports the following aggregation pipeline operators.

### Accumulators

| **Expression**  | **Supported** |
|-----------------|---------------|
| `$addToSet`     | Yes           |
| `$avg`          | Yes           |
| `$first`        | Yes           |
| `$last`         | Yes           |
| `$max`          | Yes           |
| `$mergeObjects` | Yes           |
| `$min`          | Yes           |
| `$push`         | Yes           |
| `$stdDevPop`    | No            |
| `$stdDevSamp`   | No            |
| `$sum`          | Yes           |

### Accumulator expressions

| **Expression** | **Supported** |
|----------------|---------------|
| `$avg`         | Yes           |
| `$first`       | Yes           |
| `$last`        | Yes           |
| `$max`         | Yes           |
| `$min`         | Yes           |
| `$stdDevPop`   | No            |
| `$stdDevSamp`  | No            |
| `$sum`         | Yes           |

### Arithmetic operators

**Limitations** : Arithmetic operators don't support `decimal128` values.

| **Operator** | **Supported** |
|--------------|---------------|
| `$abs`       | Yes           |
| `$add`       | Yes           |
| `$ceil`      | Yes           |
| `$divide`    | Yes           |
| `$exp`       | Yes           |
| `$floor`     | Yes           |
| `$ln`        | Yes           |
| `$log`       | Yes           |
| `$log10`     | Yes           |
| `$mod`       | Yes           |
| `$multiply`  | Yes           |
| `$pow`       | Yes           |
| `$sqrt`      | Yes           |
| `$subtract`  | Yes           |
| `$trunc`     | Yes           |

### Array operators

| **Operator**     | **Supported** |
|------------------|---------------|
| `$arrayElemAt`   | Yes           |
| `$arrayToObject` | Yes           |
| `$concatArrays`  | Yes           |
| `$filter`        | Yes           |
| `$firstN`        | Yes           |
| `$in`            | Yes           |
| `$indexOfArray`  | Yes           |
| `$isArray`       | Yes           |
| `$map`           | Yes           |
| `$objectToArray` | Yes           |
| `$range`         | Yes           |
| `$reduce`        | Yes           |
| `$reverseArray`  | Yes           |
| `$size`          | Yes           |
| `$slice`         | Yes           |
| `$zip`           | Yes           |

### Boolean operators

| **Operator** | **Supported** |
|--------------|---------------|
| `$and`       | Yes           |
| `$not`       | Yes           |
| `$or`        | Yes           |

### Comparison operators

| **Operator** | **Supported** |
|--------------|---------------|
| `$cmp`       | Yes           |
| `$eq`        | Yes           |
| `$gt`        | Yes           |
| `$gte`       | Yes           |
| `$lt`        | Yes           |
| `$lte`       | Yes           |
| `$ne`        | Yes           |

### Conditional expression operators

| **Operator** | **Supported** |
|--------------|---------------|
| `$cond`      | Yes           |
| `$ifNull`    | Yes           |
| `$switch`    | Yes           |

### Date operators

| **Operator**      | **Supported** |
|-------------------|---------------|
| `$dateFromParts`  | Yes           |
| `$dateFromString` | Yes           |
| `$dateToParts`    | Yes           |
| `$dateToString`   | Yes           |
| `$dayOfMonth`     | Yes           |
| `$dayOfWeek`      | Yes           |
| `$dayOfYear`      | Yes           |
| `$hour`           | Yes           |
| `$isoDayOfWeek`   | Yes           |
| `$isoWeek`        | Yes           |
| `$isoWeekYear`    | Yes           |
| `$millisecond`    | Yes           |
| `$minute`         | Yes           |
| `$month`          | Yes           |
| `$second`         | Yes           |
| `$week`           | Yes           |
| `$year`           | Yes           |

### Miscellaneous operators

| **Operator**        | **Supported**   |
|---------------------|-----------------|
| `$natural`          | Yes (ascending) |
| `$toHashedIndexKey` | No              |

### Literal expression operators

| **Operator** | **Supported** |
|--------------|---------------|
| `$literal`   | Yes           |

### Object operators

| **Operator**     | **Supported** |
|------------------|---------------|
| `$mergeObjects`  | Yes           |
| `$objectToArray` | Yes           |

### Set operators

| **Operator**       | **Supported** |
|--------------------|---------------|
| `$allElementsTrue` | Yes           |
| `$anyElementTrue`  | Yes           |
| `$setDifference`   | Yes           |
| `$setEquals`       | Yes           |
| `$setIntersection` | Yes           |
| `$setIsSubset`     | Yes           |
| `$setUnion`        | Yes           |

### Stage operators

| **Operator**         | **Supported** |
|----------------------|---------------|
| `$addFields`         | Yes           |
| `$bucket`            | Yes           |
| `$bucketAuto`        | No            |
| `$collStats`         | Yes           |
| `$count`             | Yes           |
| `$currentOp`         | No            |
| `$facet`             | Yes           |
| `$geoNear`           | No            |
| `$graphLookup`       | No            |
| `$group`             | Yes           |
| `$indexStats`        | No            |
| `$limit`             | Yes           |
| `$listLocalSessions` | No            |
| `$listSessions`      | No            |
| `$lookup`            | Yes           |
| `$match`             | Yes           |
| `$out`               | No            |
| `$project`           | Yes           |
| `$redact`            | No            |
| `$replaceRoot`       | Yes           |
| `$sample`            | Yes           |
| `$set`               | Yes           |
| `$skip`              | Yes           |
| `$sort`              | Yes           |
| `$sortByCount`       | Yes           |
| `$unset`             | Yes           |
| `$unwind`            | Yes           |

### String operators

| **Operator**      | **Supported** |
|-------------------|---------------|
| `$concat`         | Yes           |
| `$dateFromString` | Yes           |
| `$dateToString`   | Yes           |
| `$indexOfBytes`   | Yes           |
| `$indexOfCP`      | Yes           |
| `$split`          | Yes           |
| `$strcasecmp`     | Yes           |
| `$strLenBytes`    | Yes           |
| `$strLenCP`       | Yes           |
| `$substr`         | Yes           |
| `$substrBytes`    | Yes           |
| `$substrCP`       | Yes           |
| `$toLower`        | Yes           |
| `$toString`       | Yes           |
| `$toUpper`        | Yes           |

### System variables

| **Variable** | **Supported** |
|--------------|---------------|
| `$$CURRENT`  | No            |
| `$$DESCEND`  | No            |
| `$$KEEP`     | No            |
| `$$PRUNE`    | No            |
| `$$REMOVE`   | Yes           |
| `$$ROOT`     | Yes           |

### Text operators

| **Operator** | **Supported** |
|--------------|---------------|
| `$meta`      | Yes           |

### Type operators

| **Operator** | **Supported** |
|--------------|---------------|
| `$type`      | Yes           |

### Variable operators

| **Operator** | **Supported** |
|--------------|---------------|
| `$let`       | Yes           |

## Geospatial

Firestore with MongoDB compatibility supports the following Geospatial operators.

### Geometry specifiers

| **Specifier**   | **Supported** |
|-----------------|---------------|
| `$box`          | No            |
| `$center`       | No            |
| `$centerSphere` | No            |
| `$geometry`     | No            |
| `$maxDistance`  | No            |
| `$minDistance`  | No            |
| `$polygon`      | No            |
| `$uniqueDocs`   | No            |

### Query selectors

| **Selector**     | **Supported** |
|------------------|---------------|
| `$geoIntersects` | No            |
| `$geoWithin`     | No            |
| `$near`          | Yes           |
| `$nearSphere`    | No            |
| `$nearSphere`    | No            |
| `$uniqueDocs`    | No            |

## Indexes and index properties

Firestore with MongoDB compatibility supports the following indexes and index operators.

### Indexes

| **Index type** | **Supported** |
|----------------|---------------|
| 2d             | No            |
| 2dsphere       | Yes           |
| Compound       | Yes           |
| Hashed         | No            |
| Multikey       | Yes           |
| Single Field   | Yes           |
| Text           | Yes           |

### Index properties

| **Property**     | **Supported** |
|------------------|---------------|
| Background       | Yes           |
| Case Insensitive | No            |
| Partial          | No            |
| Non-Sparse       | Yes           |
| Sparse           | Yes           |
| Text             | Yes           |
| TTL              | Yes           |
| Unique           | Yes           |

## Database commands

Firestore with MongoDB compatibility supports the following database commands.

### Aggregation

| **Command** | **Supported**                                                                       |
|-------------|-------------------------------------------------------------------------------------|
| `aggregate` | Yes                                                                                 |
| `count`     | Yes                                                                                 |
| `distinct`  | Yes                                                                                 |
| `group`     | No The `$group` stage in aggregations is supported whereas the group command isn't. |
| `mapReduce` | No                                                                                  |

### Authentication

| **Command**    | **Supported** |
|----------------|---------------|
| `authenticate` | No            |
| `getnonce`     | No            |
| `logout`       | No            |

### Query and write operations

| **Command**              | **Supported**                                                             |
|--------------------------|---------------------------------------------------------------------------|
| `delete`                 | Yes                                                                       |
| `eval`                   | No                                                                        |
| `find`                   | Yes                                                                       |
| `findAndModify`          | Yes                                                                       |
| `getLastError`           | Yes                                                                       |
| `getMore`                | Yes                                                                       |
| `getPrevError`           | No                                                                        |
| `GridFS`                 | No                                                                        |
| `insert`                 | Yes                                                                       |
| `parallelCollectionScan` | No                                                                        |
| `replaceOne`             | No The `replaceOne` driver method is supported with the `update` command. |
| `resetError`             | No                                                                        |
| `update`                 | Yes                                                                       |

### Session commands

| **Command**                | **Supported**                                                   |
|----------------------------|-----------------------------------------------------------------|
| `endSessions`              | Yes                                                             |
| `killAllSessions`          | No                                                              |
| `killAllSessionsByPattern` | No                                                              |
| `killSessions`             | No                                                              |
| `refreshSessions`          | No                                                              |
| `startSession`             | Sessions can be started using the `startSession` driver method. |

## Administrative commands

Firestore with MongoDB compatibility supports the following administrative commands.

| **Command**                   | **Supported**                                                                                                                                           |
|-------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------|
| `cloneCollectionAsCapped`     | No                                                                                                                                                      |
| `collMod`                     | No                                                                                                                                                      |
| `collMod: expireAfterSeconds` | No                                                                                                                                                      |
| `convertToCapped`             | No                                                                                                                                                      |
| `copydb`                      | No                                                                                                                                                      |
| `create`                      | Yes                                                                                                                                                     |
| `createIndex`                 | Yes                                                                                                                                                     |
| `createIndexes`               | Yes                                                                                                                                                     |
| `createView`                  | No                                                                                                                                                      |
| `currentOp`                   | No                                                                                                                                                      |
| `drop`                        | Yes                                                                                                                                                     |
| `dropDatabase`                | No To delete a database, see [Delete a database](https://docs.cloud.google.com/firestore/mongodb-compatibility/docs/create-databases#delete-database) . |
| `dropIndex`                   | Yes To delete indexes, see [Manage indexes](https://docs.cloud.google.com/firestore/mongodb-compatibility/docs/indexing) .                              |
| `dropIndexes`                 | No                                                                                                                                                      |
| `filemd5`                     | No                                                                                                                                                      |
| `killCursors`                 | Yes                                                                                                                                                     |
| `killOp`                      | No                                                                                                                                                      |
| `listCollections`             | Yes                                                                                                                                                     |
| `listDatabases`               | Yes                                                                                                                                                     |
| `listIndexes`                 | Yes                                                                                                                                                     |
| `reIndex`                     | No                                                                                                                                                      |
| `renameCollection`            | No                                                                                                                                                      |
| `setAuditConfig`              | No                                                                                                                                                      |

### Diagnostic commands

| **Command**        | **Supported**                                                                                                                                                       |
|--------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `buildInfo`        | Yes                                                                                                                                                                 |
| `collStats`        | Yes                                                                                                                                                                 |
| `connectionStatus` | Yes                                                                                                                                                                 |
| `connPoolStats`    | No                                                                                                                                                                  |
| `dataSize`         | No                                                                                                                                                                  |
| `dbHash`           | No                                                                                                                                                                  |
| `dbStats`          | No                                                                                                                                                                  |
| `explain`          | Yes For behavior differences and limitations, see [Query Explain](https://docs.cloud.google.com/firestore/mongodb-compatibility/docs/query-explain#explain-command) |
| `features`         | No                                                                                                                                                                  |
| `hostInfo`         | Yes                                                                                                                                                                 |
| `listCommands`     | No                                                                                                                                                                  |
| `profiler`         | No                                                                                                                                                                  |
| `serverStatus`     | No                                                                                                                                                                  |
| `top`              | No                                                                                                                                                                  |
| `whatsmyuri`       | No                                                                                                                                                                  |

### User management commands

To manage database access, see the following:

- [Authenticate and connect to a database](https://docs.cloud.google.com/firestore/mongodb-compatibility/docs/connect) .
- [Manage users](https://docs.cloud.google.com/firestore/mongodb-compatibility/docs/security/iam) .

| **Command**                | **Supported** |
|----------------------------|---------------|
| `createUser`               | No            |
| `dropAllUsersFromDatabase` | No            |
| `dropUser`                 | No            |
| `grantRolesToUser`         | No            |
| `revokeRolesFromUser`      | No            |
| `updateUser`               | No            |
| `usersInfo`                | No            |

### Role management commands

To manage database access, see the following:

- [Authenticate and connect to a database](https://docs.cloud.google.com/firestore/mongodb-compatibility/docs/connect) .
- [Manage users](https://docs.cloud.google.com/firestore/mongodb-compatibility/docs/security/iam) .

| **Command**                | **Supported** |
|----------------------------|---------------|
| `createRole`               | No            |
| `dropRole`                 | No            |
| `dropAllRolesFromDatabase` | No            |
| `grantPrivilegesToRole`    | No            |
| `grantRolesToRole`         | No            |
| `invalidateUserCache`      | No            |
| `revokePrivilegesFromRole` | No            |
| `revokeRolesFromRole`      | No            |
| `rolesInfo`                | No            |
| `updateRole`               | No            |

## What's next

- Run the [Quickstart: Create a database and connect to it](https://docs.cloud.google.com/firestore/mongodb-compatibility/docs/create-and-query-database) .
- Learn about [Behavior differences](https://docs.cloud.google.com/firestore/mongodb-compatibility/docs/behavior-differences) .
