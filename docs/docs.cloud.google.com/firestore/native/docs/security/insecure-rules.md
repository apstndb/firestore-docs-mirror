# Fix insecure rules

Use this guide to understand common vulnerabilities in Firestore Security Rules configurations, review and better secure your own rules, and test your changes before deploying them.

**Note:** The server client libraries bypass all Firestore Security Rules and instead authenticate through [Google Application Default Credentials](https://cloud.google.com/docs/authentication/production) . If you're using the server client libraries or the REST or RPC APIs, make sure to set up [Identity and Access Management (IAM) for Firestore](https://cloud.google.com/firestore/docs/security/iam) .

If you receive an alert that your Firestore in Native Mode database isn't properly secured, you can resolve the vulnerabilities by modifying and testing your Firestore Security Rules.

To view your existing Security Rules, go to the [Rules tab](//console.firebase.google.com/project/_/firestore/_/rules) in the Firebase console.

**Note:** If you manage your Security Rules from the Firebase CLI, go to the rules file noted in your [firebase.json file](https://firebase.google.com/docs/cli/#the_firebasejson_file) .

#### For Firestore in Native Mode instances created in the Google Cloud console

If you created your Firestore in Native Mode database in the Google Cloud console, and haven't connected it to a Firebase project, you don't need Firestore Security Rules. Those Firestore in Native Mode instances will only accept and return requests through your application layer. Firestore in Native Mode instances tied to a Firebase project (created in the Firebase console) allow clients to connect directly to the database and employ access control through Firestore Security Rules. To enable direct access for clients, [import your Google Cloud project in the Firebase console](https://firebase.google.com/docs/guides) . If you've already added your Google Cloud project to a Firebase project, it's important that you properly configure your Security Rules.

**The following documentation only applies to Firestore in Native Mode instances that were created with Firebase or have been added to a Firebase project.** All Firestore in Native Mode instances tied to Firebase projects must have properly configured Security Rules to protect your data.

## Understand your Firestore Security Rules

Firestore Security Rules protect your data from malicious users. The default rules for any Firestore in Native Mode instance created in the Firebase console deny access to all users. To develop your app and access your database, you'll need to modify those rules and might consider granting blanket access to all users in a development environment. Before deploying your app to a production environment, however, take the time to properly configure your rules and secure your data.

As you're developing your app and testing different configurations for your rules, use the [Firestore in Native Mode emulator](/firestore/native/docs/security/test-rules-emulator) to run your app in a local development environment.

## Common scenarios with insecure rules

The Firestore Security Rules you might have set up by default or as you initially worked on developing your app with Firestore in Native Mode should be reviewed and updated before you deploy your app. Make sure you properly secure your users' data by avoiding the following common pitfalls.

### Open access

As you set up Firestore in Native Mode, you might have set your rules to allow open access during development. You might think you're the only person using your app, but if you've deployed it, it's available on the internet. If you're not authenticating users and configuring security rules, then anyone who guesses your project ID can steal, modify, or delete the data.

<table>
<tbody>
<tr class="odd">
<td>Not recommended: Read and write access to all users.</td>
</tr>
</tbody>
</table>

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

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td>Solution: Rules that restrict read and write access.
<p>Build rules that make sense for your data hierarchy. One of the common solutions to this insecurity is user-based security with Firebase Authentication. Learn more about <a href="/firestore/native/docs/security/rules-conditions#authentication">authenticating users with rules</a> .</p></td>
</tr>
</tbody>
</table>

#### Content owner only

``` text
service cloud.firestore {
  match /databases/{database}/documents {
    // Allow only authenticated content owners access
    match /some_collection/{document} {
      // Allow reads and deletion if the current user owns the existing document
      allow read, delete: if request.auth.uid == resource.data.author_uid;
      // Allow creation if the current user owns the new document
      allow create: if request.auth.uid == request.resource.data.author_uid;
      // Allow updates by the owner, and prevent change of ownership
      allow update: if request.auth.uid == request.resource.data.author_uid
                    && request.auth.uid == resource.data.author_uid;

    }
  }
}
  
```

#### Mixed public and private access

``` text
service cloud.firestore {
  match /databases/{database}/documents {
    // Allow public read access, but only content owners can write
    match /some_collection/{document} {
      // Allow public reads
      allow read: if true
      // Allow creation if the current user owns the new document
      allow create: if request.auth.uid == request.resource.data.author_uid;
      // Allow updates by the owner, and prevent change of ownership
      allow update: if request.auth.uid == request.resource.data.author_uid
                    && request.auth.uid == resource.data.author_uid;
      // Allow deletion if the current user owns the existing document
      allow delete: if request.auth.uid == resource.data.author_uid;
    }
  }
}
  
```

### Access for any authenticated user

Sometimes, Firestore Security Rules check that a user is logged in, but don't further restrict access based on that authentication. If one of your rules includes `  auth != null  ` , confirm that you want any logged-in user to have access to the data.

<table>
<tbody>
<tr class="odd">
<td>Not recommended: Any logged-in user has read and write access to your entire database.</td>
</tr>
</tbody>
</table>

``` text
service cloud.firestore {
  match /databases/{database}/documents {
    match /some_collection/{document} {
      allow read, write: if request.auth != null;
    }
  }
}
```

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td>Solution: Narrow access using security conditions.
<p>When you're checking for authentication, you might also want to use one of the authentication properties to further restrict access to specific users for specific data sets. Learn more about <a href="/firestore/native/docs/security/rules-conditions">adding security conditions</a> and <a href="../solutions/role-based-access">role-based access</a> .</p></td>
</tr>
</tbody>
</table>

#### Role-based access

``` text
service cloud.firestore {
  match /databases/{database}/documents {
    // Assign roles to all users and refine access based on user roles
    match /some_collection/{document} {
     allow read: if request.auth != null && get(/databases/$(database)/documents/users/$(request.auth.uid)).data.role == "Reader"
     allow write: if request.auth != null && get(/databases/$(database)/documents/users/$(request.auth.uid)).data.role == "Writer"

     // Note: Checking for roles in your database using `get` (as in the code
     // above) or `exists` carry standard charges for read operations.
    }
  }
}
```

#### Attribute-based access

``` text
// Give each user in your database a particular attribute
// and set it to true/false
// Then, use that attribute to grant access to subsets of data
// For example, an "admin" attribute set
// to "true" grants write access to data

service cloud.firestore {
  match /databases/{database}/documents {
    match /collection/{document} {
      allow write: if get(/databases/$(database)/documents/users/$(request.auth.uid)).data.admin == true;
      allow read: true;
    }
  }
}
  
```

#### Mixed public and private access

``` text
service cloud.firestore {
  match /databases/{database}/documents {
    // Allow public read access, but only content owners can write
    match /some_collection/{document} {
      allow read: if true
      allow write: if request.auth.uid == request.resource.data.author_uid
    }
  }
}
  
```

### Access for unverified email addresses

Sometimes, Firestore Security Rules check that a user's email belongs to a particular domain. While this is generally a good practice, emails are not always verified during sign-in until an additional step is performed by the user upon receipt of a verification email. Ensure you are validating that the email does in fact belong to the user.

<table>
<tbody>
<tr class="odd">
<td>Not recommended: Any user can sign in with an arbitrary email address.</td>
</tr>
</tbody>
</table>

``` text
service cloud.firestore {
  match /databases/{database}/documents {
    // Allow access based on email domain
    match /some_collection/{document} {
     allow read: if request.auth != null
                 && request.auth.email.endsWith('@example.com')
    }
  }
}
```

<table>
<tbody>
<tr class="odd">
<td>Solution: Narrow access to verified emails only.</td>
</tr>
</tbody>
</table>

#### Verify emails

``` text
service cloud.firestore {
  match /databases/{database}/documents {
    // Allow access based on email domain
    match /some_collection/{document} {
     allow read: if request.auth != null
                 && request.auth.email_verified
                 && request.auth.email.endsWith('@example.com')
    }
  }
}
```

### Closed access

While you're developing your app, another common approach is to keep your data locked down. Typically, this means you've closed off read and write access to all users, as follows:

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

The Firebase Admin SDKs and Cloud Functions can still access your database. Use these rules when you intend to use Firestore in Native Mode as a server-only backend in conjunction with the Firebase Admin SDK. While it is secure, you should test that your app's clients can properly retrieve data.

Learn more about Firestore Security Rules and how they work in [Get Started with Firestore Security Rules](/firestore/native/docs/security/get-started) .

## Check your Firestore Security Rules

To check your app's behavior and verify your Firestore Security Rules configurations, use the [Firestore in Native Mode emulator](/firestore/native/docs/security/test-rules-emulator) . Use the Firestore in Native Mode emulator to run and automate unit tests in a local environment before you deploy any changes.

To quickly test your updated Firestore Security Rules in the Firebase console, use the Rules Playground tool.

1.  To open the Rules Playground, click **Rules playground** from the [Rules tab](//console.firebase.google.com/project/_/firestore/_/rules) .
2.  In the *Rules playground* settings, select options for your test, including:
      - Testing reads or writes
      - A specific **Location** in your database, as a path
      - Authentication type — unauthenticated, authenticated anonymous user, or a specific user ID
      - Document-specific data that your rules specifically reference (for example, if your rules require the presence of a specific field before allowing a write)
3.  Click **Run** and look for the results in the banner above the rules window.
