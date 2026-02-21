# Structure security rules

Firestore Security Rules allow you to control access to documents and collections in your database. The flexible rules syntax allows you to create rules that match anything, from all writes to the entire database to operations on a specific document.

This guide describes the basic syntax and structure of security rules. Combine this syntax with [security rules conditions](/firestore/native/docs/security/rules-conditions) to create complete rulesets.

**Note:** The server client libraries bypass all Firestore Security Rules and instead authenticate through [Google Application Default Credentials](https://cloud.google.com/docs/authentication/production) . If you're using the server client libraries or the REST or RPC APIs, make sure to set up [Identity and Access Management (IAM) for Firestore](https://cloud.google.com/firestore/docs/security/iam) .

## Service and database declaration

Firestore Security Rules always begin with the following declaration:

``` text
service cloud.firestore {
  // The {database} wildcard allows the rules to reference any database,
  // but these rules are only active on databases where they are explicitly deployed.
  match /databases/{database}/documents {
    // ...
  }
}
```

The `  service cloud.firestore  ` declaration scopes the rules to Firestore, preventing conflicts between Firestore Security Rules and rules for other products such as Cloud Storage.

The `  match /databases/{database}/documents  ` declaration specifies that rules should match any Firestore database in the project. While a project can contain up to 100 databases, only the first database created is designated as the default.

Firestore Security Rules are applied separately for each named database in your project. This means that if you create multiple databases, you must manage and deploy rules for each one individually. For detailed instructions on deploying your updates, see [Deploy your updates](https://firebase.google.com/docs/rules/manage-deploy#deploy_your_updates) .

## Basic read/write rules

Basic rules consist of a `  match  ` statement specifying a document path and an `  allow  ` expression detailing when reading the specified data is allowed:

``` text
service cloud.firestore {
  match /databases/{database}/documents {

    // Match any document in the 'cities' collection
    match /cities/{city} {
      allow read: if <condition>;
      allow write: if <condition>;
    }
  }
}
```

All match statements should point to documents, not collections. A match statement can point to a specific document, as in `  match /cities/SF  ` or use wildcards to point to any document in the specified path, as in `  match /cities/{city}  ` .

In the example above, the match statement uses the `  {city}  ` wildcard syntax. This means the rule applies to any document in the `  cities  ` collection, such as `  /cities/SF  ` or `  /cities/NYC  ` . When the `  allow  ` expressions in the match statement are evaluated, the `  city  ` variable will resolve to the city document name, such as `  SF  ` or `  NYC  ` .

**Note:** You can only access documents that your security rules specifically allow you to access. For example, the rules shown above allow access only to documents in the `  cities  ` collection; as a result, they also deny access to documents in all other collections.

## Granular operations

In some situations, it's useful to break down `  read  ` and `  write  ` into more granular operations. For example, your app may want to enforce different conditions on document creation than on document deletion. Or you may want to allow single document reads but deny large queries.

A `  read  ` rule can be broken into `  get  ` and `  list  ` , while a `  write  ` rule can be broken into `  create  ` , `  update  ` , and `  delete  ` :

``` text
service cloud.firestore {
  match /databases/{database}/documents {
    // A read rule can be divided into get and list rules

    match /cities/{city} {
      // Applies to single document read requests
      allow get: if <condition>;

      // Applies to queries and collection read requests
      allow list: if <condition>;
    }
    // A write rule can be divided into create, update, and delete rules
    match /cities/{city} {
      // Applies to writes to nonexistent documents
      allow create: if <condition>;

      // Applies to writes to existing documents
      allow update: if <condition>;

      // Applies to delete operations
      allow delete: if <condition>;
    }
  }
}
```

## Hierarchical data

Data in Firestore is organized into collections of documents, and each document may extend the hierarchy through subcollections. It is important to understand how security rules interact with hierarchical data.

Consider the situation where each document in the `  cities  ` collection contains a `  landmarks  ` subcollection. Security rules apply only at the matched path, so the access controls defined on the `  cities  ` collection do not apply to the `  landmarks  ` subcollection. Instead, write explicit rules to control access to subcollections:

``` text
service cloud.firestore {
  match /databases/{database}/documents {
    match /cities/{city} {
      allow read, write: if <condition>;

        // Explicitly define rules for the 'landmarks' subcollection
        match /landmarks/{landmark} {
          allow read, write: if <condition>;
        }
    }
  }
}
```

When nesting `  match  ` statements, the path of the inner `  match  ` statement is always relative to the path of the outer `  match  ` statement. The following rulesets are therefore equivalent:

``` text
service cloud.firestore {
  match /databases/{database}/documents {
    match /cities/{city} {
      match /landmarks/{landmark} {
        allow read, write: if <condition>;
      }
    }
  }
}
```

``` text
service cloud.firestore {
  match /databases/{database}/documents {
    match /cities/{city}/landmarks/{landmark} {
      allow read, write: if <condition>;
    }
  }
}
```

### Recursive wildcards

If you want rules to apply to an arbitrarily deep hierarchy, use the recursive wildcard syntax, `  {name=**}  ` . For example:

``` text
service cloud.firestore {
  match /databases/{database}/documents {
    // Matches any document in the cities collection as well as any document
    // in a subcollection.
    match /cities/{document=**} {
      allow read, write: if <condition>;
    }
  }
}
```

When using the recursive wildcard syntax, the wildcard variable will contain the entire matching path segment, even if the document is located in a deeply nested subcollection. For example, the rules listed above would match a document located at `  /cities/SF/landmarks/coit_tower  ` , and the value of the `  document  ` variable would be `  SF/landmarks/coit_tower  ` .

Note, however, that the behavior of recursive wildcards depends on the rules version.

### Version 1

Security rules use version 1 by default. In version 1, recursive wildcards match one or more path items. They do not match an empty path, so `  match /cities/{city}/{document=**}  ` matches documents in subcollections but not in the `  cities  ` collection, whereas `  match /cities/{document=**}  ` matches both documents in the `  cities  ` collection and subcollections.

Recursive wildcards must come at the end of a match statement.

### Version 2

In version 2 of the security rules, recursive wildcards match zero or more path items. `  match/cities/{city}/{document=**}  ` matches documents in any subcollections as well as documents in the `  cities  ` collection.

You must opt-in to version 2 by adding `  rules_version = '2';  ` at the top of your security rules:

``` text
rules_version = '2';
service cloud.firestore {
 match /databases/{database}/documents {
   // Matches any document in the cities collection as well as any document
   // in a subcollection.
   match /cities/{city}/{document=**} {
     allow read, write: if <condition>;
   }
 }
}
```

You can have at most one recursive wildcard per match statement, but in version 2, you can place this wildcard anywhere in the match statement. For example:

``` text
rules_version = '2';
service cloud.firestore {
 match /databases/{database}/documents {
   // Matches any document in the songs collection group
   match /{path=**}/songs/{song} {
     allow read, write: if <condition>;
   }
 }
}
```

If you use [collection group queries](../query-data/queries#collection-group-query) , you must use version 2, see [securing collection group queries](/firestore/native/docs/security/rules-query#secure_and_query_documents_based_on_collection_groups) .

## Overlapping match statements

It's possible for a document to match more than one `  match  ` statement. In the case where multiple `  allow  ` expressions match a request, the access is allowed if **any** of the conditions is `  true  ` :

``` text
service cloud.firestore {
  match /databases/{database}/documents {
    // Matches any document in the 'cities' collection.
    match /cities/{city} {
      allow read, write: if false;
    }

    // Matches any document in the 'cities' collection or subcollections.
    match /cities/{document=**} {
      allow read, write: if true;
    }
  }
}
```

In the example above, all reads and writes to the `  cities  ` collection will be allowed because the second rule is always `  true  ` , even though the first rule is always `  false  ` .

## Security rule limits

As you work with security rules, note the following limits:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Limit</th>
<th>Details</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Maximum number of <code dir="ltr" translate="no">       exists()      </code> , <code dir="ltr" translate="no">       get()      </code> , and <code dir="ltr" translate="no">       getAfter()      </code> calls per request</td>
<td><ul>
<li>10 for single-document requests and query requests.</li>
<li><p>20 for multi-document reads, transactions, and batched writes. The previous limit of 10 also applies to each operation.</p>
<p>For example, imagine you create a batched write request with 3 write operations and that your security rules use 2 document access calls to validate each write. In this case, each write uses 2 of its 10 access calls and the batched write request uses 6 of its 20 access calls.</p></li>
</ul>
<p>Exceeding either limit results in a permission denied error.</p>
<p>Some document access calls may be cached, and cached calls do not count towards the limits.</p></td>
</tr>
<tr class="even">
<td>Maximum nested <code dir="ltr" translate="no">       match      </code> statement depth</td>
<td>10</td>
</tr>
<tr class="odd">
<td>Maximum path length, in path segments, allowed within a set of nested <code dir="ltr" translate="no">       match      </code> statements</td>
<td>100</td>
</tr>
<tr class="even">
<td>Maximum number of path capture variables allowed within a set of nested <code dir="ltr" translate="no">       match      </code> statements</td>
<td>20</td>
</tr>
<tr class="odd">
<td>Maximum function call depth</td>
<td>20</td>
</tr>
<tr class="even">
<td>Maximum number of function arguments</td>
<td>7</td>
</tr>
<tr class="odd">
<td>Maximum number of <code dir="ltr" translate="no">       let      </code> variable bindings per function</td>
<td>10</td>
</tr>
<tr class="even">
<td>Maximum number of recursive or cyclical function calls</td>
<td>0 (not permitted)</td>
</tr>
<tr class="odd">
<td>Maximum number of expressions evaluated per request</td>
<td>1,000</td>
</tr>
<tr class="even">
<td>Maximum size of a ruleset</td>
<td>Rulesets must obey two size limits:
<ul>
<li>a 256 KB limit on the size of the ruleset text source published from the Firebase console or from the CLI using <code dir="ltr" translate="no">         firebase deploy        </code> .</li>
<li>a 250 KB limit on the size of the compiled ruleset that results when Firebase processes the source and makes it active on the back-end.</li>
</ul></td>
</tr>
</tbody>
</table>

## Next steps

  - Write [custom security rules conditions](/firestore/native/docs/security/rules-conditions) .
  - Read the [security rules reference](https://firebase.google.com/docs/reference/rules/rules) .
