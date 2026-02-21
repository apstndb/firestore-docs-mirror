# Test security rules

As you're building your app, you might want to lock down access to your Firestore in Native Mode database. However, before you launch, you'll need more nuanced Firestore Security Rules. With the Firestore in Native Mode emulator, in addition to prototyping and testing your app's [general features and behavior](//firebase.google.com/docs/emulator-suite/connect_and_prototype) , you can write unit tests that check the behavior of your Firestore Security Rules.

**Note:** The server client libraries bypass all Firestore Security Rules and instead authenticate through [Google Application Default Credentials](https://cloud.google.com/docs/authentication/production) . If you're using the server client libraries or the REST or RPC APIs, make sure to set up [Identity and Access Management (IAM) for Firestore](https://cloud.google.com/firestore/docs/security/iam) .

## Quickstart

For a few basic test cases with simple rules, try out the [quickstart sample](https://github.com/firebase/quickstart-testing) .

## Understand Firestore Security Rules

Implement [Firebase Authentication](https://firebase.google.com/docs/auth/) and [Firestore Security Rules](/firestore/native/docs/security/get-started) for serverless authentication, authorization, and data validation when you use the mobile and web client libraries.

Firestore Security Rules include two pieces:

1.  A `  match  ` statement that identifies documents in your database.
2.  An `  allow  ` expression that controls access to those documents.

Firebase Authentication verifies users' credentials and provides the foundation for user-based and role-based access systems.

Every database request from a Firestore mobile/web client library is evaluated against your security rules before reading or writing any data. If the rules deny access to any of the specified document paths, the entire request fails.

Learn more about Firestore Security Rules in [Get started with Firestore Security Rules](/firestore/native/docs/security/get-started) .

## Install the emulator

To install the Firestore in Native Mode emulator, use the [Firebase CLI](//firebase.google.com/docs/cli/) and run the command below:

``` text
firebase setup:emulators:firestore
```

## Run the emulator

Begin by initializing a Firebase project in your working directory. This is a common first step when [using the Firebase CLI](//firebase.google.com/docs/cli#initialize_a_firebase_project) .

``` text
firebase init
```

Start the emulator using the following command. The emulator will run until you kill the process:

``` text
firebase emulators:start --only firestore
```

In many cases you want to start the emulator, run a test suite, and then shut down the emulator after the tests run. You can do this easily using the `  emulators:exec  ` command:

``` text
firebase emulators:exec --only firestore "./my-test-script.sh"
```

When started the emulator will attempt to run on a default port (8080). You can change the emulator port by modifying the `  "emulators"  ` section of your `  firebase.json  ` file:

``` text
{
  // ...
  "emulators": {
    "firestore": {
      "port": "YOUR_PORT"
    }
  }
}
```

## Before you run the emulator

Before you start using the emulator, keep in mind the following:

  - The emulator will initially load the rules specified in the `  firestore.rules  ` field of your `  firebase.json  ` file. It expects the name of a local file containing your Firestore Security Rules and applies those rules to all projects. If you don't provide the local file path or use the `  loadFirestoreRules  ` method as described below, the emulator treats all projects as having open rules.
  - While [most Firebase SDKs](https://firebase.google.com/docs/emulator-suite#which_firebase_features_and_platforms_are_supported) work with the emulators directly, only the `  @firebase/rules-unit-testing  ` library supports mocking `  auth  ` in Security Rules, making unit tests much easier. In addition, the library supports a few emulator-specific features like clearing all data, as listed below.
  - The emulators will also accept production Firebase Auth tokens provided through Client SDKs and evaluate rules accordingly, which allows connecting your application directly to the emulators in integration and manual tests.

## Run local unit tests

### Run local unit tests with the v9 JavaScript SDK

Firebase distributes a Security Rules unit testing library with both its version 9 JavaScript SDK and its version 8 SDK. The library APIs are significantly different. We recommend the v9 testing library, which is more streamlined and requires less setup to connect to emulators and thus safely avoid accidental use of production resources. For backwards compatibility, we continue to make the [v8 testing library available](//firebase.google.com/docs/rules/unit-tests#rut-v1-testing) .

  - [Common test methods and utility functions in the v9 SDK](#rut-v2-common-methods)
  - [Emulator-specific test methods in the v9 SDK](#rut-v2-specific-methods)

Use the `  @firebase/rules-unit-testing  ` module to interact with the emulator that runs locally. If you get timeouts or `  ECONNREFUSED  ` errors, double-check that the emulator is actually running.

We strongly recommend using a recent version of Node.js so you can use `  async/await  ` notation. Almost all of the behavior you might want to test involves asynchronous functions, and the testing module is designed to work with Promise-based code.

The v9 Rules Unit Testing library is always aware of the emulators and never touches your production resources.

You import the library using v9 modular import statements. For example:

``` text
import {
  assertFails,
  assertSucceeds,
  initializeTestEnvironment
} from "@firebase/rules-unit-testing"

// Use `const { … } = require("@firebase/rules-unit-testing")` if imports are not supported
// Or we suggest `const testing = require("@firebase/rules-unit-testing")` if necessary.
```

Once imported, implementing unit tests involves:

  - Creating and configuring a `  RulesTestEnvironment  ` with a call to `  initializeTestEnvironment  ` .
  - Setting up test data without triggering Rules, using a convenience method that allows you to temporarily bypass them, `  RulesTestEnvironment.withSecurityRulesDisabled  ` .
  - Setting up test suite and per-test before/after hooks with calls to clean up test data and environment, like `  RulesTestEnvironment.cleanup()  ` or `  RulesTestEnvironment.clearFirestore()  ` .
  - Implementing test cases that mimic authentication states using `  RulesTestEnvironment.authenticatedContext  ` and `  RulesTestEnvironment.unauthenticatedContext  ` .

**Note:** A summary of the API for the Rules unit testing library is provided below. You can also review the [full API reference documentation](//firebase.google.com/docs/reference/emulator-suite/rules-unit-testing/rules-unit-testing) .

### Common methods and utility functions

Also see [emulator-specific test methods in the v9 SDK](#rut-v2-specific-methods) .

**`  initializeTestEnvironment() => RulesTestEnvironment  `**

This function initializes a test environment for rules unit testing. Call this function first for test setup. Successful execution requires emulators to be running.

The function accepts an optional object defining a `  TestEnvironmentConfig  ` , which can consist of a project ID and emulator configuration settings.

``` text
let testEnv = await initializeTestEnvironment({
  projectId: "demo-project-1234",
  firestore: {
    rules: fs.readFileSync("firestore.rules", "utf8"),
  },
});
```

Note: The emulators persist data between test invocations on a single emulator run. This might impact your results. To clear data between each test run, call the applicable clear emulator data method, e.g. `  clearFirestoreData  ` , between tests.

**`  RulesTestEnvironment.authenticatedContext({ user_id: string, tokenOptions?: TokenOptions }) => RulesTestContext  `**

This method creates a `  RulesTestContext  ` , which behaves like an authenticated Authentication user. Requests created via the returned context will have a mock Authentication token attached. Optionally, pass an object defining custom claims or overrides for Authentication token payloads.

Use the returned test context object in your tests to access any emulator instances configured, including those configured with `  initializeTestEnvironment  ` .

``` text
// Assuming a Firestore app and the Firestore emulator for this example
import { setDoc } from "firebase/firestore";

const alice = testEnv.authenticatedContext("alice", { … });
// Use the Firestore instance associated with this context
await assertSucceeds(setDoc(alice.firestore().doc('/users/alice'), { ... });
```

**`  RulesTestEnvironment.unauthenticatedContext() => RulesTestContext  `**

This method creates a `  RulesTestContext  ` , which behaves like a client that is not logged in via Authentication. Requests created via the returned context will not have Firebase Auth tokens attached.

Use the returned test context object in your tests to access any emulator instances configured, including those configured with `  initializeTestEnvironment  ` .

``` text
// Assuming a Cloud Storage app and the Storage emulator for this example
import { getStorage, ref, deleteObject } from "firebase/storage";

const alice = testEnv.unauthenticatedContext();

// Use the Cloud Storage instance associated with this context
const desertRef = ref(alice.storage(), 'images/desert.jpg');
await assertSucceeds(deleteObject(desertRef));
```

**`  RulesTestEnvironment.withSecurityRulesDisabled()  `**

Run a test setup function with a context that behaves as if Security Rules were disabled.

This method takes a callback function, which takes the Security-Rules-bypassing context and returns a promise. The context will be destroyed once the promise resolves / rejects.

**`  RulesTestEnvironment.cleanup()  `**

This method destroys all `  RulesTestContexts  ` created in the test environment and cleans up the underlying resources, allowing a clean exit.

This method does not change the state of emulators in any way. To reset data between tests, use the application emulator-specific clear data method.

**`  assertSucceeds(pr: Promise<any>)) => Promise<any>  `**

This is a test case utility function.

The function asserts that the supplied Promise wrapping an emulator operation will be resolved with no Security Rules violations.

``` text
await assertSucceeds(setDoc(alice.firestore(), '/users/alice'), { ... });
```

**`  assertFails(pr: Promise<any>)) => Promise<any>  `**

This is a test case utility function.

The function asserts that the supplied Promise wrapping an emulator operation will be rejected with a Security Rules violation.

``` text
await assertFails(setDoc(alice.firestore(), '/users/bob'), { ... });
```

### Emulator-specific methods

Also see [common test methods and utility functions in the v9 SDK](#rut-v2-common-methods) .

**`  RulesTestEnvironment.clearFirestore() => Promise<void>  `**

This method clears data in the Firestore database that belongs to the `  projectId  ` configured for the Firestore emulator.

**`  RulesTestContext.firestore(settings?: Firestore.FirestoreSettings) => Firestore;  `**

This method gets a Firestore instance for this test context. The returned Firebase JS Client SDK instance can be used with the client SDK APIs (v9 modular or v9 compat).

## Visualize rules evaluations

The Firestore in Native Mode emulator lets you visualize client requests in the Emulator Suite UI, including evaluation tracing for Firebase Security Rules.

Open the *Firestore \> Requests* tab to view the detailed evaluation sequence for each request.

## Generate test reports

After running a suite of tests, you can access test coverage reports that show how each of your security rules was evaluated.

To get the reports, query an exposed endpoint on the emulator while it's running. For a browser-friendly version, use the following URL:

`  http://localhost:8080/emulator/v1/projects/<project_id>:ruleCoverage.html  `

This breaks your rules into expressions and subexpressions that you can mouseover for more information, including number of evaluations and values returned. For the raw JSON version of this data, include the following URL in your query:

`  http://localhost:8080/emulator/v1/projects/<project_id>:ruleCoverage  `

## Differences between the emulator and production

1.  You do not have to explicitly create a Firestore in Native Mode project. The emulator automatically creates any instance that is accessed.
2.  The Firestore in Native Mode emulator does not work with the normal Firebase Authentication flow. Instead, in the Firebase Test SDK, we have provided the `  initializeTestApp()  ` method in the `  rules-unit-testing  ` library, which takes an `  auth  ` field. The Firebase handle created using this method will behave as though it has successfully authenticated as whatever entity you provide. If you pass in `  null  ` , it will behave as an unauthenticated user ( `  auth != null  ` rules will fail, for example).

## Troubleshoot known issues

As you use the Firestore in Native Mode emulator, you might run into the following known issues. Follow the guidance below to troubleshoot any irregular behavior you're experiencing. These notes are written with the Security Rules unit testing library in mind, but the general approaches are applicable to any Firebase SDK.

### Test behavior is inconsistent

If your tests are occasionally passing and failing, even without any changes to the tests themselves, you might need to verify that they're properly sequenced. Most interactions with the emulator are asynchronous, so double-check that all the async code is properly sequenced. You can fix the sequencing by either chaining promises, or using `  await  ` notation liberally.

In particular, review the following async operations:

  - Setting security rules, with, for example, `  initializeTestEnvironment  ` .
  - Reading and writing data, with, for example, `  db.collection("users").doc("alice").get()  ` .
  - Operational assertions, including `  assertSucceeds  ` and `  assertFails  ` .

### Tests only pass the first time you load the emulator

The emulator is stateful. It stores all the data written to it in memory, so any data is lost whenever the emulator shuts down. If you're running multiple tests against the same project id, each test can produce data that might influence subsequent tests. You can use any of the following methods to bypass this behavior:

  - Use unique project IDs for each test. Note that if you choose to do this you will need to call `  initializeTestEnvironment  ` as part of each test; rules are only automatically loaded for the default project ID.
  - Restructure your tests so they don't interact with previously written data (for example, use a different collection for each test).
  - Delete all the data written during a test.

### Test setup is very complicated

When setting up your test, you may want to modify data in a way that your Firestore Security Rules don't actually allow. If your rules are making test setup complex, try using `  RulesTestEnvironment.withSecurityRulesDisabled  ` in your setup steps, so reads and writes won't trigger `  PERMISSION_DENIED  ` errors.

After that, your test can perform operations as an authenticated or unauthenticated user using `  RulesTestEnvironment.authenticatedContext  ` and `  unauthenticatedContext  ` respectively. This allows you to validate that your Firestore Security Rules allows / denies different cases correctly.
