# Getting started with security rules

With Firestore Security Rules, you can focus on building a great user experience without having to manage infrastructure or write server-side authentication and authorization code.

Security rules provide access control and data validation in a simple yet expressive format. To build user-based and role-based access systems that keep your users' data safe, you need to use [Firebase Authentication](https://firebase.google.com/docs/auth/) with Firestore Security Rules.

**Note:** The server client libraries bypass all Firestore Security Rules and instead authenticate through [Google Application Default Credentials](https://cloud.google.com/docs/authentication/production) . If you're using the server client libraries or the REST or RPC APIs, make sure to set up [Identity and Access Management (IAM) for Firestore](https://cloud.google.com/firestore/docs/security/iam) .

## Security rules version 2

As of May 2019, version 2 of the Firestore security rules is now available. Version 2 of the rules changes the behavior of [recursive wildcards](/firestore/native/docs/security/rules-structure#recursive_wildcards) `  {name=**}  ` . You must use version 2 if you plan to use [collection group queries](../query-data/queries#collection-group-query) . You must opt-in to version 2 by making `  rules_version = '2';  ` the first line in your security rules:

``` text
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
```

## Writing rules

You will write and manage Firestore Security Rules tailored to the data model you create for the default database and each additional database in your project.

All Firestore Security Rules consist of `  match  ` statements, which identify documents in your database, and `  allow  ` expressions, which control access to those documents:

``` text
service cloud.firestore {
  match /databases/{database}/documents {
    match /<some_path>/ {
      allow read, write: if <some_condition>;
    }
  }
}
```

Every database request from a Firestore mobile/web client library is evaluated against your security rules before reading or writing any data. If the rules deny access to any of the specified document paths, the entire request fails.

Below are some examples of basic rule sets. While these rules are valid, they are not recommended for production applications:

### Auth required

``` text
// Allow read/write access on all documents to any user signed in to the application
service cloud.firestore {
  match /databases/{database}/documents {
    match /{document=**} {
      allow read, write: if request.auth != null;
    }
  }
}
```

### Deny all

``` text
// Deny read/write access to all users under any conditions
service cloud.firestore {
  match /databases/{database}/documents {
    match /{document=**} {
      allow read, write: if false;
    }
  }
}
```

### Allow all

``` text
// Allow read/write access to all users under any conditions
// Warning: **NEVER** use this rule set in production; it allows
// anyone to overwrite your entire database.
service cloud.firestore {
  match /databases/{database}/documents {
    match /{document=**} {
      allow read, write: if true;
    }
  }
}
```

The `  {document=**}  ` path used in the examples above matches any document in the entire database. Continue on to the guide for [structuring security rules](/firestore/native/docs/security/rules-structure) to learn how to match specific data paths and work with hierarchical data.

## Testing rules

Firestore provides a rules simulator that you can use to test your ruleset. You can access the simulator from the [**Rules** tab](https://console.firebase.google.com/project/_/firestore/rules) in the Firestore section of the Firebase console.

The rules simulator lets you simulate authenticated and unauthenticated reads, writes, and deletes. When you simulate an authenticated request, you can build and preview authentication tokens from various providers. Simulated requests run against the ruleset in your editor, not your currently deployed ruleset.

## Deploying rules

Before you can start using Firestore from your mobile app, you will need to deploy security rules. You can deploy rules in the Firebase console, using the Firebase CLI, or with the Firestore management REST API.

Updates to Firestore Security Rules can take up to a minute to affect new queries and listeners. However, it can take up to 10 minutes to fully propagate the changes and affect any active listeners.

**Note:** **When you [deploy security rules using the Firebase CLI](https://firebase.google.com/docs/cli/#deployment) , the rules defined in your project directory overwrite any existing rules in the Firebase console.** So, if you choose to define or edit your security rules using the Firebase console, make sure that you also update the rules defined in your project directory.

### Use the Firebase console

To set up and deploy your first set of rules, for the default database in your project, open the [**Rules** tab](https://console.firebase.google.com/project/_/firestore/rules) in the Firestore section of the Firebase console.

Write your rules in the online editor, then click **Publish** .

**Note:** The Firebase console currently supports deployment of Firestore Security Rules to your project's default database. Future updates will allow you to deploy Rules to additional databases in your project. You can use the [Firebase CLI](#use_the_cli) to work with Rules in your multi-database projects.

### Use the Firebase CLI

You can also deploy rules using the [Firebase CLI](https://firebase.google.com/docs/cli) . Using the CLI allows you to keep your rules under version control with your application code and deploy rules as part of your existing deployment process.

``` text
// Set up Firestore in your project directory, creates a .rules file
firebase init firestore

// Edit the generated .rules file to your desired security rules
// ...

// Deploy rules for all configured databases
firebase deploy --only firestore
```

## Next steps

  - Learn how to [structure security rules](/firestore/native/docs/security/rules-structure) .
  - Write [custom security rules conditions](/firestore/native/docs/security/rules-conditions) .
  - Read the [security rules reference](https://firebase.google.com/docs/reference/rules/rules) .
