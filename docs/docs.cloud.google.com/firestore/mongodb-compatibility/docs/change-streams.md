# Read real-time data with Change Streams

> **Preview**
> 
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

Change Streams for Firestore with MongoDB compatibility let applications access real-time changes (inserts, updates, and deletes) made to a collection or to an entire database. A change stream orders updates by modification time.

Change Streams are accessible through the MongoDB compatible APIs and traditional MongoDB Drivers. The Firestore with MongoDB compatibility implementation of Change Streams can handle any throughput of writes and reads through a unique implementation of automatic partitioning on writes and read parallelism. This lets you build high-throughput workloads. You can also improve migration and data synchronization infrastructure between Firestore and other storage solutions.

In addition to compatibility with the MongoDB drivers, you can use Firestore to read Change Streams in parallel. This lets you build parallel, high-throughput read workloads. Each stream represents a well-distributed partition of results.

Change Streams support the following features:

  - Configurable change streams with database or collection scope.
  - A retention duration for a change stream that's specified at creation. The default retention is 7 days and the minimum retention is 1 day. The retention must be a multiple of 1 day, up to a maximum of 7 days. The retention duration cannot be changed after creation. To change the retention period, you must drop and re-create the change stream.
  - `delete` , `insert` , `update` , and `drop` change events that are observable using `db.collection.watch()` and `db.watch()` .
  - `updateDescription.updatedFields` contains update diffs.
  - All `fullDocument` and `fullDocumentBeforeChange` options.
      - Looking up full document for updates.
      - Pre-image of the document before it was replaced, updated, or deleted.
      - Post-image of the document after it was replaced or updated.
      - Pre and post images older than one hour require enablement of point-in-time recovery (PITR).
  - All resume options including `resumeAfter` and `startAfter` .
  - When using `watch()` to observe changes, you can chain aggregation stages like `$addFields` , `$match` , `$project` , `$replaceRoot` , `$replaceWith` , `$set` , and `$unset` .

## Configure Change Streams

To create, drop, or view existing Change Streams for a database, use the Google Cloud console.

### Roles and permissions

To create, delete, and list Change Streams, a principal requires the `datastore.schemas.create` , `datastore.schemas.delete` , and `datastore.schemas.list` Identity and Access Management (IAM) permissions, respectively.

The **Datastore Index Admin** ( `roles/datastore.indexAdmin` ) role, for example, grants these permissions.

### Create a change stream

Before you can open a corresponding change stream cursor, you must create a change stream. Automatic change stream enablement at collection or database creation is not supported.

To create a change stream, use the Google Cloud console.

1.  In the Google Cloud console, go to the **Databases** page.

2.  From the list, select a Firestore with MongoDB compatibility database. The **Firestore Studio** panel opens.

3.  In the **Explorer** panel, find the **Change streams** node, click more\_vert **More actions** , and then select **Create change stream** .

4.  Enter a unique change stream name, scope, and retention period, and then click **Save**

### View Change Streams

You can view details about Change Streams in the Google Cloud console.

1.  In the Google Cloud console, go to the **Databases** page.

2.  From the list, select a Firestore with MongoDB compatibility database. The **Firestore Studio** panel opens.

3.  In the **Explorer** panel, find the **Change streams** node.

4.  To open or close the node, click arrow\_drop\_down **Toggle node** .

### Delete a change stream

To delete a change stream, use the Google Cloud console.

1.  In the Google Cloud console, go to the **Databases** page.

2.  From the list, select a Firestore with MongoDB compatibility database. The **Firestore Studio** panel opens.

3.  In the **Explorer** panel, find the **Change streams** node.

4.  To open or close the node, click arrow\_drop\_down **Toggle node** .

5.  In the **Explorer** , locate the change stream that you want to delete.

6.  Click more\_vert **More actions** and then select **Delete change stream** .

7.  In the dialog, enter the change stream name to confirm deletion, and then click **Delete** .

## Open or resume a change stream cursor

The following examples demonstrate how to create, resume, and configure a change stream cursor.

Before you create a change stream cursor, you must explicitly [create a change stream](https://docs.cloud.google.com/firestore/mongodb-compatibility/docs/change-streams#create) for the database or collection.

### Create a change stream cursor

To create a new change stream cursor, use the `watch` method in the MongoDB drivers. To listen to all changes on a database, create a database-scoped change stream and call the `watch` method on the `db` object.

    let cursor = db.watch()

To create a cursor scoped to a collection, you must first create a change stream for that collection. Then, call the `watch` method on the corresponding collection.

> **Note:** You can apply a post-filter on `ns.coll` to a database level change stream to only match changes for a given collection. However, explicitly creating and reading Change Streams on the collection can be more cost efficient and performant.

    let cursor = db.my_collection.watch()

Now that you created a change stream cursor, you can begin streaming. For example, if you insert a document and call `tryNext` on the cursor, you see the change appear on the change stream.

    let doc = db.my_collection.insertOne({value: "hello world"})
    console.log(cursor.tryNext())

If you update and delete the document, then you see those changes appear on the change stream:

    db.my_collection.updateOne({"_id": doc.insertedId}, {$set: {value: "hello world!"}})
    db.my_collection.deleteOne({"_id": doc.insertedId}})
    
    // Prints the update event
    console.log(cursor.tryNext())
    
    // Prints the delete event
    console.log(cursor.tryNext())

### Resume a change stream

To resume a change stream, use the `resumeAfter` or `startAfter` options. To determine where in the change log to resume from `resumeAfter` and `startAfter` , use a resume token.

    // Create a cursor and add one event to the change stream.
    let cursor = db.my_collection.watch();
    db.my_collection.insertOne({value: "hello world"});
    let event = cursor.tryNext();
    
    // Get the resume token from the event.
    let resumeToken = event._id;
    
    // Add a new event to the change stream.
    db.my_collection.insertOne({value: "foobar"});
    
    // Create a new cursor by using the resume token as a starting point.
    let newCursor = db.my_collection.watch({resumeAfter: resumeToken})
    
    // Log the change event containing the "foobar" value.
    console.log(newCursor.tryNext())

To use `startAfter` :

    // Start after the resume token.
    let startAfterCursor = db.my_collection.watch({startAfter: resumeToken})

### Include pre and post images in updates and delete

If required, you can include pre and post images of documents in update and delete change events. Image availability is subject to the [point-in-time recovery (PITR) window](https://docs.cloud.google.com/firestore/mongodb-compatibility/docs/pitr#pitr_window) , and to read document images older than one hour, you must enable PITR.

Change Streams take advantage of the PITR window to provide a view of the document before and after the given change event. By default, update events contain an `updateDescription` field which is the delta of the fields modified by the update operation.

To include the pre and post images in a change event, you must specify `fullDocumentBeforeChange` and `fullDocument` options in the change stream query.

    let cursor = db.my_collection.watch({
      "fullDocument": "required",
      "fullDocumentBeforeChange": "required"
    })

If the query attempts to read a document outside of the PITR retention window or if PITR isn't enabled, then the `required` value throws a server-side error message.

As an alternative to throwing an error, you can use the `whenAvailable` value to return a `null` value if the images are no longer available.

    let cursor = db.my_collection.watch({
      "fullDocument": "whenAvailable",
      "fullDocumentBeforeChange": "whenAvailable"
    })

### Include the current image in updates

By default, update events contain an `updateDescription` field which is the delta of the fields modified by the update operation. To instead lookup the most current version of the entire document, use the `updateLookup` value in the `fullDocument` option.

This feature does not require PITR and performs a lookup for the document.

    let cursor = db.my_collection.watch({
      "fullDocument": "updateLookup",
    })

## Parallel Reads

To increase throughput, you can use the `firestoreWorkerConfig` option to split a change stream query across multiple workers. Each worker is responsible for serving the changes for a distinct set of documents. You must create a parallel cursor through a `runCommand` or `aggregate` query.

For example, you can distribute a change stream across 3 workers like so:

    let cursor1 = db.my_collection.aggregate([{
        "$changeStream": {
            "firestoreWorkerConfig": {numWorkers: 3, workerId: 0 }}
      }]);
    
    let cursor2 = db.my_collection.aggregate([{
        "$changeStream": {
            "firestoreWorkerConfig": {numWorkers: 3, workerId: 1 }}
      }]);
    
    let cursor3 = db.my_collection.aggregate([{
        "$changeStream": {
            "firestoreWorkerConfig": {numWorkers: 3, workerId: 2 }}
      }]);

## Change Streams and backups

Neither the change stream configuration nor the change stream data is available in backup restore operations. If you restore a database with Change Streams, you must recreate those changes streams in the destination database to open cursors to that database.

## Billing

  - Change Streams incur read units and storage costs. See [change stream pricing](https://cloud.google.com/firestore/enterprise/pricing#change-streams) .
  - To [include pre and post images older than 1hr at the read request time](https://docs.cloud.google.com/firestore/mongodb-compatibility/docs/change-streams#include-images) , you must enable PITR which incurs [PITR costs](https://cloud.google.com/firestore/enterprise/pricing#pitr-data) .

## Behaviour differences

The following section describes differences in Change Streams between Firestore with MongoDB compatibility and MongoDB.

### `updateDescription`

`updateDescription` is a document in an `update` event that describes the fields that were updated or removed by the update operation. In Firestore, the notable differences are that:

  - In `updateDescription` , the fields `truncatedArrays` and `disambiguatedPaths` are not populated.
  - `updateDescription.updatedFields` represent a canonical diff between the pre and post images of a document before and after a mutation is applied.

Consider the following initial state of a document:

    db.my_collection.insertOne({
      _id: 1,
      root: {
        array: [{a: 1}, {b: 2}, {c: 3}]
      }
    })

#### Scenario 1: mutate only the first element of the array.

In this scenario, Firestore behavior matches MongoDB.

    db.my_collection.updateOne(
      {_id: 1},
      {'$set': {"root.array.0.a": 100}}
    )
    
    {
      updatedFields: {"root.array.0.a": 100},
      removedFields: []
    }

#### Scenario 2: overwrite with a whole array

In this scenario, the operation updates only the first array field but overwrites the whole array.

The Firestore update diff does not differentiate between these two scenarios and returns the same `updateDescription.updatedFields` for both:

    db.my_collection.updateOne(
      {_id: 1},
      {'$set': {"root.array": [{a: 100}, {b: 2}, {c: 3}]}}
    )
    
    // In other implementations, updatedFields reflects the mutation itself
    {
      updatedFields: {
        "root.array": [{a: 100}, {b: 2}, {c: 3}]
      },
      removedFields: []
    }
    
    // Firestore updatedFields is the diff between the before and after versions of the document
    {
      updatedFields: {"root.array.0.a": 100},
      removedFields: []
    }
