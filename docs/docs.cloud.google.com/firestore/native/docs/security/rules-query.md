# Securely querying data

This page builds on the concepts in [Structuring Security Rules](./rules-structure) and [Writing Conditions for Security Rules](./rules-conditions) to explain how Firestore Security Rules interact with queries. It takes a closer look at how security rules affect the queries you can write and describes how to ensure your queries use the same constraints as your security rules. This page also describes how to write security rules to allow or deny queries based on query properties like `  limit  ` and `  orderBy  ` .

**Note:** The server client libraries bypass all Firestore Security Rules and instead authenticate through [Google Application Default Credentials](https://cloud.google.com/docs/authentication/production) . If you're using the server client libraries or the REST or RPC APIs, make sure to set up [Identity and Access Management (IAM) for Firestore](https://cloud.google.com/firestore/docs/security/iam) .

### Rules are not filters

When writing queries to retrieve documents, keep in mind that security rules are not filters—queries are all or nothing. To save you time and resources, Firestore evaluates a query against its potential result set instead of the actual field values for all of your documents. If a query could potentially return documents that the client does not have permission to read, the entire request fails.

**Note:** This behavior applies to queries that retrieve one or more documents from a collection and not to individual document retrievals. When you use a document ID to retrieve a single document, Firestore reads the document and evaluates the request using your security rules and the actual document properties.

## Queries and security rules

As the examples below demonstrate, you must write your queries to fit the constraints of your security rules.

**Note:** The same rules apply to both normal queries that return documents and [aggregation queries](../query-data/aggregation-queries) . In other words, security rules control what conditions are allowed, not how data is returned.

### Secure and query documents based on `     auth.uid    `

The following example demonstrates how to write a query to retrieve documents protected by a security rule. Consider a database that contains a collection of `  story  ` documents:

**/stories/{storyid}**

``` text
{
  title: "A Great Story",
  content: "Once upon a time...",
  author: "some_auth_id",
  published: false
}
```

In addition to the `  title  ` and `  content  ` fields, each document stores the `  author  ` and `  published  ` fields to use for access control. These examples assume the app uses [Firebase Authentication](https://firebase.google.com/docs/auth/) to set the `  author  ` field to the UID of the user who created the document. Firebase Authentication also populates the [`  request.auth  `](https://firebase.google.com/docs/reference/rules/rules.firestore.Request) variable in the security rules.

The following security rule uses the [`  request.auth  `](https://firebase.google.com/docs/reference/rules/rules.firestore.Request) and [`  resource.data  `](https://firebase.google.com/docs/reference/rules/rules.firestore.Resource) variables to restrict read and write access for each `  story  ` to its author:

``` text
service cloud.firestore {
  match /databases/{database}/documents {
    match /stories/{storyid} {
      // Only the authenticated user who authored the document can read or write
      allow read, write: if request.auth != null && request.auth.uid == resource.data.author;
    }
  }
}
```

Suppose that your app includes a page that shows the user a list of `  story  ` documents that they authored. You might expect that you could use the following query to populate this page. However, this query will fail, because it does not include the same constraints as your security rules:

Invalid : Query constraints do not match security rules constraints

``` text
// This query will fail
db.collection("stories").get()
```

The query fails ***even if*** the current user actually is the author of every `  story  ` document. The reason for this behavior is that when Firestore applies your security rules, it evaluates the query against its *potential* result set, not against the *actual* properties of documents in your database. If a query could *potentially* include documents that violate your security rules, the query will fail.

In contrast, the following query succeeds, because it includes the same constraint on the `  author  ` field as the security rules:

Valid : Query constraints match security rules constraints

``` text
var user = firebase.auth().currentUser;

db.collection("stories").where("author", "==", user.uid).get()
```

### Secure and query documents based on a field

To further demonstrate the interaction between queries and rules, the security rules below expand read access for the `  stories  ` collection to allow any user to read `  story  ` documents where the `  published  ` field is set to `  true  ` .

``` text
service cloud.firestore {
  match /databases/{database}/documents {
    match /stories/{storyid} {
      // Anyone can read a published story; only story authors can read unpublished stories
      allow read: if resource.data.published == true || (request.auth != null && request.auth.uid == resource.data.author);
      // Only story authors can write
      allow write: if request.auth != null && request.auth.uid == resource.data.author;
    }
  }
}
```

The query for published pages must include the same constraints as the security rules:

``` text
db.collection("stories").where("published", "==", true).get()
```

The query constraint `  .where("published", "==", true)  ` guarantees that `  resource.data.published  ` is `  true  ` for any result. Therefore, this query satisfies the security rules and is allowed to read data.

### `     OR    ` queries

When evaluating a logical `  OR  ` query ( `  or  ` , `  in  ` , or `  array-contains-any  ` ) against a ruleset, Firestore evaluates each comparison value separately. Each comparison value must meet the security rule constraints. For example, for the following rule:

``` text
match /mydocuments/{doc} {
  allow read: if resource.data.x > 5;
}
```

Invalid : Query does not guarantee that `  x > 5  ` for all potential documents

``` text
// These queries will fail
query(db.collection("mydocuments"),
      or(where("x", "==", 1),
         where("x", "==", 6)
      )
    )

query(db.collection("mydocuments"),
      where("x", "in", [1, 3, 6, 42, 99])
    )
```

Valid : Query guarantees that `  x > 5  ` for all potential documents

``` text
query(db.collection("mydocuments"),
      or(where("x", "==", 6),
         where("x", "==", 42)
      )
    )

query(db.collection("mydocuments"),
      where("x", "in", [6, 42, 99, 105, 200])
    )
```

### Evaluating constraints on queries

Your security rules can also accept or deny queries based on their constraints. The [`  request.query  `](https://firebase.google.com/docs/reference/rules/rules.firestore.Request) variable contains the `  limit  ` , `  offset  ` , and `  orderBy  ` properties of a query. For example, your security rules can deny any query that doesn't limit the maximum number of documents retrieved to a certain range:

``` text
allow list: if request.query.limit <= 10;
```

**Note:** [You can break `  read  ` rules into `  get  ` and `  list  ` rules](./rules-structure#granular_operations) . Rules for `  get  ` apply to requests for single documents, and rules for `  list  ` apply to queries and requests for collections.

The following ruleset demonstrates how to write security rules that evaluate constraints placed on queries. This example expands the previous `  stories  ` ruleset with the following changes:

  - The ruleset separates the read rule into rules for `  get  ` and `  list  ` .
  - The `  get  ` rule restricts retrieval of single documents to public documents or documents the user authored.
  - The `  list  ` rule applies the same restrictions as `  get  ` but for queries. It also checks the query limit, then denies any query without a limit or with a limit greater than 10.
  - The ruleset defines an `  authorOrPublished()  ` function to avoid code duplication.

<!-- end list -->

``` text
service cloud.firestore {

  match /databases/{database}/documents {

    match /stories/{storyid} {

      // Returns `true` if the requested story is 'published'
      // or the user authored the story
      function authorOrPublished() {
        return resource.data.published == true || request.auth.uid == resource.data.author;
      }

      // Deny any query not limited to 10 or fewer documents
      // Anyone can query published stories
      // Authors can query their unpublished stories
      allow list: if request.query.limit <= 10 &&
                     authorOrPublished();

      // Anyone can retrieve a published story
      // Only a story's author can retrieve an unpublished story
      allow get: if authorOrPublished();

      // Only a story's author can write to a story
      allow write: if request.auth.uid == resource.data.author;
    }

  }
}
```

## Collection group queries and security rules

By default, queries are scoped to a single collection and they retrieve results only from that collection. With [collection group queries](../query-data/queries#collection-group-query) , you can retrieve results from a collection group consisting of all collections with the same ID. This section describes how to secure your collection group queries using security rules.

### Secure and query documents based on collection groups

In your security rules, you must explicitly allow collection group queries by writing a rule for the collection group:

1.  Make sure `  rules_version = '2';  ` is the first line of your ruleset. Collection group queries require the [new recursive wildcard `  {name=**}  `](./rules-structure#recursive_wildcards) behavior of security rules version 2.
2.  Write a rule for your collection group using `  match /{path=**}/ [COLLECTION_ID] /{doc}  ` .

For example, consider a forum organized into `  forum  ` documents containing `  posts  ` subcollections:

**/forums/{forumid}/posts/{postid}**

``` text
{
  author: "some_auth_id",
  authorname: "some_username",
  content: "I just read a great story.",
}
```

In this application, we make posts editable by their owners and readable by authenticated users:

``` text
service cloud.firestore {
  match /databases/{database}/documents {
    match /forums/{forumid}/posts/{post} {
      // Only authenticated users can read
      allow read: if request.auth != null;
      // Only the post author can write
      allow write: if request.auth != null && request.auth.uid == resource.data.author;
    }
  }
}
```

Any authenticated user can retrieve the posts of any single forum:

``` text
db.collection("forums/technology/posts").get()
```

But what if you want to show the current user their posts across all forums? You can use a [collection group query](../query-data/queries#collection-group-query) to retrieve results from all `  posts  ` collections:

``` text
var user = firebase.auth().currentUser;

db.collectionGroup("posts").where("author", "==", user.uid).get()
```

**Note:** This query requires an index on the `  posts  ` collection for field `  author  ` and with collection group scope. If you haven't enabled this index, the query will return an error link you can follow to create the required index.

In your security rules, you must allow this query by writing a read or list rule for the `  posts  ` collection group:

``` text
rules_version = '2';
service cloud.firestore {

  match /databases/{database}/documents {
    // Authenticated users can query the posts collection group
    // Applies to collection queries, collection group queries, and
    // single document retrievals
    match /{path=**}/posts/{post} {
      allow read: if request.auth != null;
    }
    match /forums/{forumid}/posts/{postid} {
      // Only a post's author can write to a post
      allow write: if request.auth != null && request.auth.uid == resource.data.author;

    }
  }
}
```

Note, however, that these rules will apply to all collections with ID `  posts  ` , regardless of hierarchy. For example, these rules apply to all of the following `  posts  ` collections:

  - `  /posts/{postid}  `
  - `  /forums/{forumid}/posts/{postid}  `
  - `  /forums/{forumid}/subforum/{subforumid}/posts/{postid}  `

### Secure collection group queries based on a field

Like single-collection queries, collection group queries must also meet the constraints set by your security rules. For example, we can add a `  published  ` field to each forum post like we did in the `  stories  ` example above:

**/forums/{forumid}/posts/{postid}**

``` text
{
  author: "some_auth_id",
  authorname: "some_username",
  content: "I just read a great story.",
  published: false
}
```

We can then write rules for the `  posts  ` collection group based on the `  published  ` status and the post `  author  ` :

``` text
rules_version = '2';
service cloud.firestore {

  match /databases/{database}/documents {

    // Returns `true` if the requested post is 'published'
    // or the user authored the post
    function authorOrPublished() {
      return resource.data.published == true || request.auth.uid == resource.data.author;
    }

    match /{path=**}/posts/{post} {

      // Anyone can query published posts
      // Authors can query their unpublished posts
      allow list: if authorOrPublished();

      // Anyone can retrieve a published post
      // Authors can retrieve an unpublished post
      allow get: if authorOrPublished();
    }

    match /forums/{forumid}/posts/{postid} {
      // Only a post's author can write to a post
      allow write: if request.auth.uid == resource.data.author;
    }
  }
}
```

With these rules, Web, Apple, and Android clients can make the following queries:

  - Anyone can retrieve published posts in a forum:
    
    ``` text
    db.collection("forums/technology/posts").where('published', '==', true).get()
    ```

  - Anyone can retrieve an author's published posts across all forums:
    
    ``` text
    db.collectionGroup("posts").where("author", "==", "some_auth_id").where('published', '==', true).get()
    ```

  - Authors can retrieve all their published and unpublished posts across all forums:
    
    ``` text
    var user = firebase.auth().currentUser;
    
    db.collectionGroup("posts").where("author", "==", user.uid).get()
    ```

### Secure and query documents based on collection group and document path

In some cases, you might want to restrict collection group queries based on document path. To create these restrictions, you can use the same techniques for securing and querying documents based on a field.

Consider an application that keeps track of each user's transactions among several stock and cryptocurrency exchanges:

**/users/{userid}/exchange/{exchangeid}/transactions/{transaction}**

``` text
{
  amount: 100,
  exchange: 'some_exchange_name',
  timestamp: April 1, 2019 at 12:00:00 PM UTC-7,
  user: "some_auth_id",
}
```

Notice the `  user  ` field. Even though we know which user owns a `  transaction  ` document from the document's path, we duplicate this information in each `  transaction  ` document because it allows us to do two things:

  - Write collection group queries that are restricted to documents that include a specific `  /users/{userid}  ` in their document path. For example:
    
    ``` text
    var user = firebase.auth().currentUser;
    // Return current user's last five transactions across all exchanges
    db.collectionGroup("transactions").where("user", "==", user).orderBy('timestamp').limit(5)
    ```

  - Enforce this restriction for all queries on the `  transactions  ` collection group so one user cannot retrieve another user's `  transaction  ` documents.

We enforce this restriction in our security rules and include data validation for the `  user  ` field:

``` text
rules_version = '2';
service cloud.firestore {

  match /databases/{database}/documents {

    match /{path=**}/transactions/{transaction} {
      // Authenticated users can retrieve only their own transactions
      allow read: if resource.data.user == request.auth.uid;
    }

    match /users/{userid}/exchange/{exchangeid}/transactions/{transaction} {
      // Authenticated users can write to their own transactions subcollections
      // Writes must populate the user field with the correct auth id
      allow write: if userid == request.auth.uid && request.data.user == request.auth.uid
    }
  }
}
```

## Next steps

  - For a more detailed example of role-based access control, see [Securing Data Access for Users and Groups](../solutions/role-based-access) .
  - Read the [security rules reference](https://firebase.google.com/docs/reference/rules/rules) .
