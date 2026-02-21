# Firestore client libraries

This page describes the SDKs and client libraries available for the Firestore API. While you can make direct HTTP and RPC calls to the Firestore API, the Firestore client libraries implement best practices for you and make it easier to access your database.

Firestore supports mobile or web SDKs and server client libraries.

## Server client libraries

Firestore supports server client libraries for C\#, Go, Java, Node.js, PHP, Python, and Ruby. Use these client libraries to set up privileged server environments.

Server client libraries create a privileged Firestore environment with full access to your database. In this environment, requests are not evaluated against your Firestore security rules. Privileged Firestore servers are secured using Identity and Access Management (IAM), see [Security for server client libraries](../security/iam) .

Use the server client libraries for administrative database tasks or if you prefer an architecture with an intermediary server between your users and your Firestore database.

Firestore server client libraries are available as [Firebase Admin SDKs](https://firebase.google.com/docs/admin/setup) and as Google Cloud client libraries. Both sets of libraries provide the same Firestore features. The Firebase Admin SDKs bundle access to Firestore and several other Firebase products, like Firebase Auth and Firebase Cloud Messaging, in a single library.

### Google Cloud client libraries

The Google Cloud client libraries support Firestore access in Java, Python, Node.js, Go, PHP, C\#, and Ruby. To get started with one of the Google Cloud client libraries, see the [Quickstart using a Server Client Library](https://cloud.google.com/firestore/docs/quickstart-servers) .

#### References and resources

For more information about Google Cloud client libraries for Firestore, see the following resources:

##### Java

  - [API Reference Documentation](https://cloud.google.com/java/docs/reference/google-cloud-firestore/latest/overview.html)
  - [Source Code](https://github.com/googleapis/java-firestore)
  - [GitHub Issue Tracker](https://github.com/googleapis/java-firestore/issues)
  - [Stack Overflow](https://stackoverflow.com/questions/tagged/google-cloud-firestore+java)

##### Python

  - [API Reference Documentation](https://cloud.google.com/python/docs/reference/firestore/latest/index.html)
  - [Source Code](https://github.com/googleapis/python-firestore)
  - [GitHub Issue Tracker](https://github.com/googleapis/python-firestore/issues)
  - [Stack Overflow](https://stackoverflow.com/questions/tagged/google-cloud-firestore+python)

##### Node.js

  - [API Reference Documentation](https://googleapis.dev/nodejs/firestore/latest/)
  - [Source Code](https://github.com/googleapis/nodejs-firestore/)
  - [GitHub Issue Tracker](https://github.com/googleapis/nodejs-firestore/issues)
  - [Stack Overflow](https://stackoverflow.com/questions/tagged/node.js+google-cloud-firestore)

##### Go

  - [API Reference Documentation](https://godoc.org/cloud.google.com/go/firestore)
  - [Source Code](https://github.com/googleapis/google-cloud-go/tree/master/firestore)
  - [GitHub Issue Tracker](https://github.com/googleapis/google-cloud-go/labels/api%3A%20firestore)
  - [Stack Overflow](https://stackoverflow.com/questions/tagged/google-cloud-firestore+go)

##### PHP

  - [API Reference Documentation](https://googleapis.github.io/google-cloud-php/#/docs/cloud-firestore/latest)
  - [Source Code](https://github.com/googleapis/google-cloud-php/tree/master/Firestore)
  - [GitHub Issue Tracker](https://github.com/googleapis/google-cloud-php/labels/api%3A%20firestore)
  - [Stack Overflow](https://stackoverflow.com/questions/tagged/google-cloud-firestore+php)

##### C\#

  - [API Reference Documentation](https://googleapis.github.io/google-cloud-dotnet/docs/Google.Cloud.Firestore/)
  - [Source Code](https://github.com/googleapis/google-cloud-dotnet)
  - [GitHub Issue Tracker](https://github.com/googleapis/google-cloud-dotnet/labels/api%3A%20firestore)
  - [Stack Overflow](https://stackoverflow.com/questions/tagged/google-cloud-firestore+c%23)

##### Ruby

  - [API Reference Documentation](https://googleapis.dev/ruby/google-cloud-firestore/latest)
  - [Source Code](https://github.com/googleapis/google-cloud-ruby/tree/master/google-cloud-firestore)
  - [GitHub Issue Tracker](https://github.com/googleapis/google-cloud-ruby/labels/api%3A%20firestore)
  - [Stack Overflow](https://stackoverflow.com/questions/tagged/google-cloud-firestore+ruby)

### Firebase Admin SDKs

The [Firebase Admin SDKs](https://firebase.google.com/docs/admin/setup) bundle the Google Cloud client libraries for Firestore alongside client libraries and SDKs for several other Firebase features. Using one of the Admin SDKs, you can initialize access to Firestore and several other services from a single SDK. The Firebase Admin SDKs support Firestore access in Java, Python, Node.js, and Go.

To get started with a Firebase Admin SDK, see [Add the Firebase Admin SDK to Your Server](https://firebase.google.com/docs/admin/setup) .

#### References and resources

For more information about Firebase Admin SDKs, see the following resources:

##### Java

  - [API Reference Documentation](https://firebase.google.com/docs/reference/admin/java/reference/com/google/firebase/package-summary)
  - [Source Code](https://github.com/firebase/firebase-admin-java)
  - [GitHub Issue Tracker](https://github.com/firebase/firebase-admin-java/labels/api%3A%20firestore)
  - [Stack Overflow](https://stackoverflow.com/questions/tagged/firebase-admin+java)

##### Python

  - [API Reference Documentation](https://firebase.google.com/docs/reference/admin/python/)
  - [Source Code](https://github.com/firebase/firebase-admin-python)
  - [GitHub Issue Tracker](https://github.com/firebase/firebase-admin-python/labels/api%3A%20firestore)
  - [Stack Overflow](https://stackoverflow.com/questions/tagged/firebase-admin+python)

##### Node.js

  - [API Reference Documentation](https://firebase.google.com/docs/reference/admin/node/)
  - [Source Code](https://github.com/firebase/firebase-admin-node)
  - [GitHub Issue Tracker](https://github.com/firebase/firebase-admin-node/labels/api%3A%20firestore)
  - [Stack Overflow](https://stackoverflow.com/questions/tagged/node.js+firebase-admin)

##### Go

  - [API Reference Documentation](https://godoc.org/firebase.google.com/go)
  - [Source Code](https://github.com/firebase/firebase-admin-go)
  - [GitHub Issue Tracker](https://github.com/firebase/firebase-admin-go/labels/api%3A%20firestore)
  - [Stack Overflow](https://stackoverflow.com/questions/tagged/firebase-admin+go)

## Mobile and web SDKs

Firestore supports SDKs for Android, iOS, and web. Combined with [Firestore security rules](https://cloud.google.com/firestore/docs/security/get-started) and [Firebase Auth](https://firebase.google.com/docs/auth/) , the mobile and web SDKs support serverless app architectures where clients connect directly to your Firestore database. With a serverless architecture, you don't need to maintain an intermediary server between your clients and your Firestore database.

The mobile and web SDKs also support [realtime updates](https://cloud.google.com/firestore/docs/query-data/listen) and [offline data persistence](https://firebase.google.com/docs/firestore/manage-data/enable-offline) .

To get started with the Android or Apple platforms, or Web SDK, see [Create a Firestore database by using a web or mobile client library](/firestore/native/docs/reference/firestore/docs/create-database-web-mobile-client-library) .

### References and resources

For more information about each SDK, see the following resources:

##### Web

  - [API Reference Documentation](https://firebase.google.com/docs/reference/js/firebase.firestore)
  - [Source Code](https://github.com/firebase/firebase-js-sdk/tree/master/packages/firestore)
  - [GitHub Issue Tracker](https://github.com/firebase/firebase-js-sdk/labels/api%3A%20firestore)
  - [Stack Overflow](https://stackoverflow.com/questions/tagged/google-cloud-firestore+javascript)

In addition to the standard client SDK, Firebase offers Firestore Lite, a lightweight, REST-only SDK.

  - [Firestore Lite Solutions Guide](https://firebase.google.com/docs/firestore/solutions/firestore-lite)
  - [Firestore Lite API Reference Documentation](https://firebase.google.com/docs/reference/js/firestore_lite.md)
  - [Firestore Lite Source Code](https://github.com/firebase/firebase-js-sdk/tree/master/packages/firestore/lite)
  - [Firestore Lite GitHub Issue Tracker](https://github.com/firebase/firebase-js-sdk/labels/api%3A%20firestore)

##### iOS+

  - [API Reference Documentation](https://firebase.google.com/docs/reference/swift/firebasefirestore/api/reference/Classes)
  - [Source Code](https://github.com/firebase/firebase-ios-sdk/tree/master/Firestore)
  - [GitHub Issue Tracker](https://github.com/firebase/firebase-ios-sdk/labels/api%3A%20firestore)
  - [Stack Overflow](https://stackoverflow.com/questions/tagged/google-cloud-firestore+ios)

##### Android

  - [API Reference Documentation](https://firebase.google.com/docs/reference/android/com/google/firebase/firestore/package-summary)
  - [Source Code](https://github.com/firebase/firebase-android-sdk/tree/master/firebase-firestore)
  - [GitHub Issue Tracker](https://github.com/firebase/firebase-android-sdk/labels/api%3A%20firestore)
  - [Stack Overflow](https://stackoverflow.com/questions/tagged/google-cloud-firestore+android)

##### Flutter

  - [API Reference Documentation](https://pub.dev/documentation/cloud_firestore/latest/)
  - [Source Code](https://github.com/firebase/flutterfire/)
  - [GitHub Issue Tracker](https://github.com/firebase/flutterfire/issues)
  - [Stack Overflow](https://stackoverflow.com/questions/tagged/google-cloud-firestore+flutter)

## Third-party library integrations

In addition to the mobile or web SDKs and server client libraries, Firestore offers a number of integrations with open-source libraries. For more information, see [Library and framework integrations](https://firebase.google.com/docs/firestore/library-integrations) .

## What's next

  - Learn about [authentication](/firestore/docs/authentication) .
  - Learn about [security rules](/firestore/docs/security/get-started) for client libraries.
