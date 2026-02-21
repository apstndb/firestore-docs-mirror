This page documents production updates to Firestore with MongoDB compatibility. You can periodically check this page for announcements about new or updated features, bug fixes, known issues, and deprecated functionality.

You can see the latest product updates for all of Google Cloud on the [Google Cloud](/release-notes) page, browse and filter all release notes in the [Google Cloud console](https://console.cloud.google.com/release-notes) , or programmatically access release notes in [BigQuery](https://console.cloud.google.com/bigquery?p=bigquery-public-data&d=google_cloud_release_notes&t=release_notes&page=table) .

To get the latest product updates delivered to you, add the URL of this page to your [feed reader](https://wikipedia.org/wiki/Comparison_of_feed_aggregators) , or add the [feed URL](https://docs.cloud.google.com/feeds/firestore-with-mongodb-compatibility-release-notes.xml) directly.

## February 02, 2026

Feature

The Firestore databases page in the Google Cloud console now includes a status column. Possible statuses include:

  - Ready
  - Cloning is in progress
  - Restoring from backup is in progress
  - Deleted
  - Failed

For the cloning and restore statuses, the status column updates upon completion.

## November 21, 2025

Feature

Support for Object as document `  _id  ` identifier.

## October 27, 2025

Feature

The [database clone feature](https://docs.cloud.google.com/firestore/mongodb-compatibility/docs/create-databases#clone-database) is now supported at the General Availability ( [GA](https://cloud.google.com/products#product-launch-stages) ) level.

## October 08, 2025

Feature

You can [create, save, and manage queries](https://cloud.google.com/firestore/mongodb-compatibility/docs/create-manage-saved-queries) in Firestore Studio. This feature is available in [Preview](https://cloud.google.com/products#product-launch-stages) .

## September 17, 2025

Feature

The `  $lookup  ` operator now supports the following fields:

  - `  from  `
  - `  localField  `
  - `  foreignField  `
  - `  as  `

For the full list of supported operators see [Supported features](/firestore/mongodb-compatibility/docs/supported-features-80) .

## September 05, 2025

Feature

Support for the following query features. For the full list of supported operators see [Supported features](https://cloud.google.com/firestore/mongodb-compatibility/docs/supported-features-80) .

  - `  $facet  `
  - `  $unionWith  `
  - `  $minN  `
  - `  $firstN  `
  - `  $lastN  `
  - `  $toString  `
  - `  $median  `
  - `  $percentile  `

## September 02, 2025

Feature

Use [Query insights](/firestore/mongodb-compatibility/docs/query-insights) to view query performance metrics for your database. This feature is now generally available ( [GA](https://cloud.google.com/products#product-launch-stages) ).

## August 26, 2025

Feature

New JSON results viewer and JSON export tool in the Google Cloud console.

Feature

Usage dashboard in the Google Cloud console.

Feature

You can [clone an existing database](https://cloud.google.com/firestore/mongodb-compatibility/docs/create-databases#clone-database) at a selected timestamp into a new database. This feature is available in [Preview](https://cloud.google.com/products#product-launch-stages) .

Feature

Support for the following query features. For the full list of supported operators see [Supported features](https://cloud.google.com/firestore/mongodb-compatibility/docs/supported-features-80) .

  - `  $  ` projection operator
  - Update array operators:
      - `  $  `
      - `  $[]  `
      - `  $[<identifier>]  `
      - `  $addToSet  `
      - `  $pop  `
      - `  $pullAll  `
  - Update modifiers:
      - `  $each  `
      - `  $position  `
      - `  $slice  `
      - `  $sort  `
  - `  $addToSet  ` aggregation pipeline accumulator expression
  - Aggregation pipeline arithmetic operators:
      - `  $exp  `
      - `  $ln  `
      - `  $log  `
      - `  $log10  `
      - `  $pow  `
      - `  $sqrt  `
      - `  $trunc  `
  - Aggregation pipeline array operators
      - `  $filter  `
      - `  $firstN  `
      - `  $in  `
      - `  $indexOfArray  `
      - `  $lastN  `
      - `  $maxN  `
      - `  $minN  `
      - `  $objectToArray  `
      - `  $range  `
      - `  $reduce  `
      - `  $sortArray  `
      - `  $zip  `
  - `  $binarySize  ` and `  $bsonSize  ` aggregation pipeline data size operators
  - `  $dateTrunc  ` aggregation pipeline date operator
  - Aggregation pipeline operators:
      - `  $mergeObjects  `
      - `  $natural  ` (ascending)
  - Aggregation pipeline set operators:
      - `  $allElementsTrue  `
      - `  $anyElementsTrue  `
      - `  $anyElementTrue  `
      - `  $setDifference  `
      - `  $setEquals  `
      - `  $setIntersection  `
      - `  $setIsSubset  `
      - `  $setIntersection  `
      - `  $setIsSubset  `
      - `  $setUnion  `
  - `  $bucket  ` aggregation pipeline stage operator
  - Aggregation pipeline type conversion operators:
      - `  $convert  `
      - `  $toDate  `
      - `  $toDecimal  `
      - `  $toDouble  `
      - `  $toInt  `
      - `  $toLong  `
      - `  $toObjectId  `
      - `  $toString  `
      - `  $type  `
  - `  $let  ` and `  $map  ` aggregation pipeline variable operators
  - `  $lookup  ` aggregation pipeline stage operator, limited to `  _id  ` in the `  foreignField  `

Feature

A range of performance improvements to support more performant queries on arrays and larger bulk operations with fewer transient errors.

Feature

Support for [managed bulk delete](https://cloud.google.com/firestore/mongodb-compatibility/docs/bulk-delete) and [import and export](https://cloud.google.com/firestore/mongodb-compatibility/docs/export-import) .

Feature

New [billing metrics](https://cloud.google.com/firestore/mongodb-compatibility/docs/use-monitoring-dashboard#billing_metrics) which allow customers to easily attribute Firestore Enterprise costs to database and RPC methods in Cloud Monitoring.

Feature

Support for [unique indexes](https://cloud.google.com/firestore/mongodb-compatibility/docs/index-overview#unique_indexes) .

Feature

Support for [Point-In-Time-Recovery](https://cloud.google.com/firestore/mongodb-compatibility/docs/pitr) features, including reading data at a specific snapshot through the MongoDB APIs.

Feature

Support for `  int32  ` , binary, and double types as document `  _id  ` identifier.

Feature

Support for [explaining queries](https://cloud.google.com/firestore/mongodb-compatibility/docs/query-explain#use_query_explain) and [managing indexes](https://cloud.google.com/firestore/mongodb-compatibility/docs/indexing#create_an_index) in the MongoDB API.

Feature

Support for [Firestore Triggers (Events)](https://cloud.google.com/firestore/mongodb-compatibility/docs/eventarc) with Firestore with MongoDB compatibility databases.

Feature

Support for Firebase interfaces, including console, CLIs, and documentation.

Feature

General Availability (GA) release of [Firestore with MongoDB compatibility](https://cloud.google.com/firestore/mongodb-compatibility/docs/overview) .

Feature

Support for [Private Google Access](https://cloud.google.com/firestore/mongodb-compatibility/docs/configure-private-google-access) .

## August 01, 2025

Feature

You can [clone an existing database](https://cloud.google.com/firestore/mongodb-compatibility/docs/create-databases#clone-database) at a selected timestamp into a new database. This feature is available in [Preview](https://cloud.google.com/products#product-launch-stages) .

## July 31, 2025

Feature

Support for [`  explain()  `](/firestore/mongodb-compatibility/docs/query-explain#use_query_explain) in the Firestore with MongoDB compatibility API is now available in [Preview](https://cloud.google.com/products#product-launch-stages) . You can now use `  explain()  ` in tools such as MongoDB Shell and Compass.

## July 21, 2025

Feature

[Bulk delete](/firestore/mongodb-compatibility/docs/bulk-delete) for Firestore with MongoDB compatibility is now available in [Preview](https://cloud.google.com/products#product-launch-stages) .

Feature

[Point-in-time recovery](/firestore/mongodb-compatibility/docs/pitr) and snapshot reads for Firestore with MongoDB compatibility are now available in [Preview](https://cloud.google.com/products#product-launch-stages) .

Feature

[Cloud Monitoring billing metrics for Firestore with MongoDB compatibility](/firestore/mongodb-compatibility/docs/use-monitoring-dashboard#billing_metrics) databases are now available in [Preview](https://cloud.google.com/products#product-launch-stages) . Limitations: These metrics don't reflect admin operations like import, export, bulk delete, indexing, and restore.

Feature

[Managed import and export](/firestore/mongodb-compatibility/docs/export-import) for Firestore with MongoDB compatibility is now available in [Preview](https://cloud.google.com/products#product-launch-stages) .

## July 10, 2025

Feature

Performance improvements:

  - Performance improvements on disjunction `  $in  ` queries and keys only index scans due to query optimizer tuning is now available in Preview.
  - Performance improvements on bulk insertions is now available in Preview.
  - Performance improvements on `  $elemMatch  ` queries with indexes due to query optimizer tuning is now available in Preview.

Feature

Array update operators `  $push  ` and `  $pull  ` are now available in Preview.

## April 09, 2025

Feature

Preview release of [Firestore with MongoDB compatibility](/firestore/mongodb-compatibility/docs/overview) .
