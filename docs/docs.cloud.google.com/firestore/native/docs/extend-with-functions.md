# Extending Firestore with Cloud Functions

With Cloud Functions, you can deploy Node.js code to handle events triggered by changes in your Firestore database. This allows you to easily add server-side functionality into your app without running your own servers.

**Note:** The examples on this page use [Cloud Functions for Firebase](https://firebase.google.com/docs/functions/) , which has [some differences from Cloud Functions for Google Cloud](/functions/docs/concepts/functions-and-firebase) .

For examples of use cases, see [What Can I Do with Cloud Functions?](//firebase.google.com/docs/functions/use-cases) or the [Functions Samples](https://github.com/firebase/functions-samples) GitHub repository.

### Edition and mode requirements

This document applies to Firestore Standard edition in Native mode.

Firestore Enterprise edition doesn't support Cloud Functions (1st gen). Use [Cloud Run functions (2nd gen)](/firestore/native/docs/eventarc) instead.

## Firestore function triggers

The Cloud Functions for Firebase SDK exports a [`  functions.firestore  `](https://firebase.google.com/docs/reference/functions/firebase-functions.firestore) object that allows you to create handlers tied to specific Firestore events.

<table>
<thead>
<tr class="header">
<th>Event Type</th>
<th style="text-align: center;">Trigger</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><a href="https://firebase.google.com/docs/reference/functions/firebase-functions.firestore.documentbuilder.md#firestoredocumentbuilderoncreate"><code dir="ltr" translate="no">        onCreate       </code></a></td>
<td style="text-align: center;">Triggered when a document is written to for the first time.</td>
</tr>
<tr class="even">
<td><a href="https://firebase.google.com/docs/reference/functions/firebase-functions.firestore.documentbuilder.md#firestoredocumentbuilderonupdate"><code dir="ltr" translate="no">        onUpdate       </code></a></td>
<td style="text-align: center;">Triggered when a document already exists and has any value changed.</td>
</tr>
<tr class="odd">
<td><a href="https://firebase.google.com/docs/reference/functions/firebase-functions.firestore.documentbuilder.md#firestoredocumentbuilderondelete"><code dir="ltr" translate="no">        onDelete       </code></a></td>
<td style="text-align: center;">Triggered when a document with data is deleted.</td>
</tr>
<tr class="even">
<td><a href="https://firebase.google.com/docs/reference/functions/firebase-functions.firestore.documentbuilder.md#firestoredocumentbuilderonwrite"><code dir="ltr" translate="no">        onWrite       </code></a></td>
<td style="text-align: center;">Triggered when <code dir="ltr" translate="no">       onCreate      </code> , <code dir="ltr" translate="no">       onUpdate      </code> or <code dir="ltr" translate="no">       onDelete      </code> is triggered.</td>
</tr>
</tbody>
</table>

**Note:** Firestore events will trigger only on document changes. An update to a Firestore document, where data is unchanged (a no-op write), will not generate an update or write event. It is not possible to add events to specific fields.

If you don't have a project enabled for Cloud Functions for Firebase yet, then read [Get Started: Write and Deploy Your First Functions](//firebase.google.com/docs/functions/get-started) to configure and set up your Cloud Functions for Firebase project.

## Writing Firestore-triggered functions

### Define a function trigger

To define a Firestore trigger, specify a document path and an event type:

### Node.js

``` text
const functions = require('firebase-functions');

exports.myFunction = functions.firestore
  .document('my-collection/{docId}')
  .onWrite((change, context) => { /* ... */ });
```

Document paths can reference either a [specific document](#specific-documents) or a [wildcard pattern](#wildcards-parameters) .

**Important:** Document paths must **not** contain trailing slashes.

### Specify a single document

If you want to trigger an event for *any* change to a specific document then you can use the following function.

### Node.js

``` javascript
// Listen for any change on document `marie` in collection `users`
exports.myFunctionName = functions.firestore
    .document('users/marie').onWrite((change, context) => {
      // ... Your code here
    });index.js
```

### Specify a group of documents using wildcards

If you want to attach a trigger to a group of documents, such as any document in a certain collection, then use a `  {wildcard}  ` in place of the document ID:

### Node.js

``` javascript
// Listen for changes in all documents in the 'users' collection
exports.useWildcard = functions.firestore
    .document('users/{userId}')
    .onWrite((change, context) => {
      // If we set `/users/marie` to {name: "Marie"} then
      // context.params.userId == "marie"
      // ... and ...
      // change.after.data() == {name: "Marie"}
    });index.js
```

In this example, when any field on any document in `  users  ` is changed, it matches a wildcard called `  userId  ` .

If a document in `  users  ` has subcollections, and a field in one of those subcollections' documents is changed, the `  userId  ` wildcard is *not* triggered.

Wildcard matches are extracted from the document path and stored into `  context.params  ` . You may define as many wildcards as you like to substitute explicit collection or document IDs, for example:

### Node.js

``` javascript
// Listen for changes in all documents in the 'users' collection and all subcollections
exports.useMultipleWildcards = functions.firestore
    .document('users/{userId}/{messageCollectionId}/{messageId}')
    .onWrite((change, context) => {
      // If we set `/users/marie/incoming_messages/134` to {body: "Hello"} then
      // context.params.userId == "marie";
      // context.params.messageCollectionId == "incoming_messages";
      // context.params.messageId == "134";
      // ... and ...
      // change.after.data() == {body: "Hello"}
    });index.js
```

**Note:** Your trigger must *always* point to a document, even if you're using a wildcard. For example, `  users/{userId}/{messageCollectionId}  ` is not valid because `  {messageCollectionId}  ` is a collection. However, `  users/{userId}/{messageCollectionId}/{messageId}  ` *is* valid because `  {messageId}  ` will always point to a document.

## Event Triggers

### Trigger a function when a new document is created

You can trigger a function to fire any time a new document is created in a collection by using an `  onCreate()  ` handler with a [wildcard](#wildcards-parameters) . This example function calls `  createUser  ` every time a new user profile is added:

### Node.js

``` javascript
exports.createUser = functions.firestore
    .document('users/{userId}')
    .onCreate((snap, context) => {
      // Get an object representing the document
      // e.g. {'name': 'Marie', 'age': 66}
      const newValue = snap.data();

      // access a particular field as you would any JS property
      const name = newValue.name;

      // perform desired operations ...
    });index.js
```

### Trigger a function when a document is updated

You can also trigger a function to fire when a document is updated using the `  onUpdate()  ` function with a [wildcard](#wildcards-parameters) . This example function calls `  updateUser  ` if a user changes their profile:

### Node.js

``` javascript
exports.updateUser = functions.firestore
    .document('users/{userId}')
    .onUpdate((change, context) => {
      // Get an object representing the document
      // e.g. {'name': 'Marie', 'age': 66}
      const newValue = change.after.data();

      // ...or the previous value before this update
      const previousValue = change.before.data();

      // access a particular field as you would any JS property
      const name = newValue.name;

      // perform desired operations ...
    });index.js
```

### Trigger a function when a document is deleted

You can also trigger a function when a document is deleted using the `  onDelete()  ` function with a [wildcard](#wildcards-parameters) . This example function calls `  deleteUser  ` when a user deletes their user profile:

### Node.js

``` javascript
exports.deleteUser = functions.firestore
    .document('users/{userID}')
    .onDelete((snap, context) => {
      // Get an object representing the document prior to deletion
      // e.g. {'name': 'Marie', 'age': 66}
      const deletedValue = snap.data();

      // perform desired operations ...
    });index.js
```

### Trigger a function for all changes to a document

If you don't care about the type of event being fired, you can listen for all changes in a Firestore document using the `  onWrite()  ` function with a [wildcard](#wildcards-parameters) . This example function calls `  modifyUser  ` if a user is created, updated, or deleted:

### Node.js

``` javascript
exports.modifyUser = functions.firestore
    .document('users/{userID}')
    .onWrite((change, context) => {
      // Get an object with the current document value.
      // If the document does not exist, it has been deleted.
      const document = change.after.exists ? change.after.data() : null;

      // Get an object with the previous document value (for update or delete)
      const oldDocument = change.before.data();

      // perform desired operations ...
    });index.js
```

## Reading and Writing Data

When a function is triggered, it provides a snapshot of the data related to the event. You can use this snapshot to read from or write to the document that triggered the event, or use the Firebase Admin SDK to access other parts of your database.

### Event Data

#### Reading Data

When a function is triggered, you might want to get data from a document that was updated, or get the data prior to update. You can get the prior data by using `  change.before.data()  ` , which contains the document snapshot before the update. Similarly, `  change.after.data()  ` contains the document snapshot state after the update.

### Node.js

``` javascript
exports.updateUser2 = functions.firestore
    .document('users/{userId}')
    .onUpdate((change, context) => {
      // Get an object representing the current document
      const newValue = change.after.data();

      // ...or the previous value before this update
      const previousValue = change.before.data();
    });index.js
```

You can access properties as you would in any other object. Alternatively, you can use the `  get  ` function to access specific fields:

### Node.js

``` javascript
// Fetch data using standard accessors
const age = snap.data().age;
const name = snap.data()['name'];

// Fetch data using built in accessor
const experience = snap.get('experience');index.js
```

#### Writing Data

Each function invocation is associated with a specific document in your Firestore database. You can access that document as a `  DocumentReference  ` in the `  ref  ` property of the snapshot returned to your function.

This `  DocumentReference  ` comes from the [Firestore Node.js SDK](/firestore/native/docs/quickstart) and includes methods like `  update()  ` , `  set()  ` , and `  remove()  ` so you can easily modify the document that triggered the function.

### Node.js

``` javascript
// Listen for updates to any `user` document.
exports.countNameChanges = functions.firestore
    .document('users/{userId}')
    .onUpdate((change, context) => {
      // Retrieve the current and previous value
      const data = change.after.data();
      const previousData = change.before.data();

      // We'll only update if the name has changed.
      // This is crucial to prevent infinite loops.
      if (data.name == previousData.name) {
        return null;
      }

      // Retrieve the current count of name changes
      let count = data.name_change_count;
      if (!count) {
        count = 0;
      }

      // Then return a promise of a set operation to update the count
      return change.after.ref.set({
        name_change_count: count + 1
      }, {merge: true});
    });index.js
```

**Note:** Any time you write to the same document that triggered a function, you are at risk of creating an infinite loop. Use caution and ensure that you safely exit the function when no change is needed.

### Data outside the trigger event

Cloud Functions execute in a trusted environment, which means they are authorized as a service account on your project. You can perform reads and writes using the [Firebase Admin SDK](https://firebase.google.com/docs/reference/admin) :

### Node.js

``` text
const admin = require('firebase-admin');
admin.initializeApp();

const db = admin.firestore();

exports.writeToFirestore = functions.firestore
  .document('some/doc')
  .onWrite((change, context) => {
    db.doc('some/otherdoc').set({ ... });
  });
```

**Note:** Reads and writes performed in Cloud Functions are not controlled by your security rules, they can access any part of your database.

## Limitations

Note the following limitations for Firestore triggers for Cloud Run functions:

  - Cloud Run functions (1st gen) prerequisites an existing "(default)" database in Firestore native mode. It does not support Firestore named databases or Datastore mode. Please use Cloud Run functions (2nd gen) to configure events in such cases.
  - Cross project setup with Cloud Run functions and Firestore trigger is a limitation. To setup Firestore trigger Cloud Run functions must be in the same project.
  - Ordering is not guaranteed. Rapid changes can trigger function invocations in an unexpected order.
  - Events are delivered at least once, but a single event may result in multiple function invocations. Avoid depending on exactly-once mechanics, and write [idempotent functions](https://cloud.google.com/blog/products/serverless/cloud-functions-pro-tips-building-idempotent-functions) .
  - [Firestore in Datastore mode](https://cloud.google.com/firestore/docs/firestore-or-datastore) requires Cloud Run functions (2nd gen). Cloud Run functions (1st gen) does not support Datastore mode.
  - A trigger is associated with a single database. You cannot create a trigger that matches multiple databases.
  - Deleting a database does not automatically delete any triggers for that database. The trigger stops delivering events but continues to exist until you [delete the trigger](https://cloud.google.com/eventarc/docs/managing-triggers#trigger-delete) .
  - If a matched event exceeds the [maximum request size](https://cloud.google.com/functions/quotas#resource_limits) , the event might not be delivered to Cloud Run functions (1st gen).
      - Events not delivered because of request size are logged in [platform logs](https://cloud.google.com/logging/docs/api/platform-logs) and count towards the log usage for the project.
      - You can find these logs in the Logs Explorer with the message "Event cannot deliver to Cloud function due to size exceeding the limit for 1st gen..." of `  error  ` severity. You can find the function name under the `  functionName  ` field. If the `  receiveTimestamp  ` field is still within an hour from now, you can infer the actual event content by reading the document in question with a snapshot before and after the timestamp.
      - To avoid such cadence, you can:
          - Migrate and upgrade to Cloud Run functions (2nd gen)
          - Downsize the document
          - Delete the Cloud Run functions in question
      - You can turn off the logging itself using [exclusions](https://cloud.google.com/logging/docs/routing/overview#exclusions) but note that the offending events will still not be delivered.
