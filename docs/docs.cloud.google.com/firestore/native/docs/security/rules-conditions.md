# Write conditions for security rules

This guide builds on the [structuring security rules](/firestore/native/docs/security/rules-structure) guide to show how to add conditions to your Firestore Security Rules. If you are not familiar with the basics of Firestore Security Rules, see the [getting started](/firestore/native/docs/security/get-started) guide.

The primary building block of Firestore Security Rules is the condition. A condition is a boolean expression that determines whether a particular operation should be allowed or denied. Use security rules to write conditions that check user authentication, validate incoming data, or even access other parts of your database.

**Note:** The server client libraries bypass all Firestore Security Rules and instead authenticate through [Google Application Default Credentials](https://cloud.google.com/docs/authentication/production) . If you're using the server client libraries or the REST or RPC APIs, make sure to set up [Identity and Access Management (IAM) for Firestore](https://cloud.google.com/firestore/docs/security/iam) .

## Authentication

One of the most common security rule patterns is controlling access based on the user's authentication state. For example, your app may want to allow only signed-in users to write data:

``` text
service cloud.firestore {
  match /databases/{database}/documents {
    // Allow the user to access documents in the "cities" collection
    // only if they are authenticated.
    match /cities/{city} {
      allow read, write: if request.auth != null;
    }
  }
}
```

Another common pattern is to make sure users can only read and write their own data:

``` text
service cloud.firestore {
  match /databases/{database}/documents {
    // Make sure the uid of the requesting user matches name of the user
    // document. The wildcard expression {userId} makes the userId variable
    // available in rules.
    match /users/{userId} {
      allow read, update, delete: if request.auth != null && request.auth.uid == userId;
      allow create: if request.auth != null;
    }
  }
}
```

If your app uses Firebase Authentication or [Google Cloud Identity Platform](https://cloud.google.com/identity-platform) , the `  request.auth  ` variable contains the authentication information for the client requesting data. For more information about `  request.auth  ` , see [the reference documentation](https://firebase.google.com/docs/reference/rules/rules.firestore.Request#auth) .

## Data validation

Many apps store access control information as fields on documents in the database. Firestore Security Rules can dynamically allow or deny access based on document data:

``` text
service cloud.firestore {
  match /databases/{database}/documents {
    // Allow the user to read data if the document has the 'visibility'
    // field set to 'public'
    match /cities/{city} {
      allow read: if resource.data.visibility == 'public';
    }
  }
}
```

The `  resource  ` variable refers to the requested document, and `  resource.data  ` is a map of all of the fields and values stored in the document. For more information on the `  resource  ` variable, see [the reference documentation](https://firebase.google.com/docs/reference/rules/rules.firestore.Resource) .

When writing data, you may want to compare incoming data to existing data. In this case, if your ruleset allows the pending write, the `  request.resource  ` variable contains the future state of the document. For `  update  ` operations that only modify a subset of the document fields, the `  request.resource  ` variable will contain the pending document state after the operation. You can check the field values in `  request.resource  ` to prevent unwanted or inconsistent data updates:

``` text
service cloud.firestore {
  match /databases/{database}/documents {
    // Make sure all cities have a positive population and
    // the name is not changed
    match /cities/{city} {
      allow update: if request.resource.data.population > 0
                    && request.resource.data.name == resource.data.name;
    }
  }
}
```

## Access other documents

Using the `  get()  ` and `  exists()  ` functions, your security rules can evaluate incoming requests against other documents in the database. The `  get()  ` and `  exists()  ` functions both expect fully specified document paths. When using variables to construct paths for `  get()  ` and `  exists()  ` , you need to explicitly escape variables using the `  $(variable)  ` syntax.

In the example below, the `  database  ` variable is captured by the match statement `  match /databases/{database}/documents  ` and used to form the path:

``` text
service cloud.firestore {
  match /databases/{database}/documents {
    match /cities/{city} {
      // Make sure a 'users' document exists for the requesting user before
      // allowing any writes to the 'cities' collection
      allow create: if request.auth != null && exists(/databases/$(database)/documents/users/$(request.auth.uid));

      // Allow the user to delete cities if their user document has the
      // 'admin' field set to 'true'
      allow delete: if request.auth != null && get(/databases/$(database)/documents/users/$(request.auth.uid)).data.admin == true;
    }
  }
}
```

For writes, you can use the `  getAfter()  ` function to access the state of a document after a transaction or batch of writes completes but before the transaction or batch commits. Like `  get()  ` , the `  getAfter()  ` function takes a fully specified document path. You can use `  getAfter()  ` to define sets of writes that must take place together as a transaction or batch.

### Access call limits

There is a limit on document access calls per rule set evaluation:

  - 10 for single-document requests and query requests.

  - 20 for multi-document reads, transactions, and batched writes. The previous limit of 10 also applies to each operation.
    
    For example, imagine you create a batched write request with 3 write operations and that your security rules use 2 document access calls to validate each write. In this case, each write uses 2 of its 10 access calls and the batched write request uses 6 of its 20 access calls.

Exceeding either limit results in a permission denied error. Some document access calls may be cached, and cached calls do not count towards the limits.

For a detailed explanation of how these limits affect transactions and batched writes, see the guide for [securing atomic operations](../manage-data/transactions#security_rules_limits) .

### Access calls and pricing

Using these functions executes a read operation in your database, which means you will be billed for reading documents even if your rules reject the request. See [Firestore Pricing](../pricing#operations) for more specific billing information.

## Custom functions

As your security rules become more complex, you may want to wrap sets of conditions in functions that you can reuse across your ruleset. Security rules support custom functions. The syntax for custom functions is a bit like JavaScript, but security rules functions are written in a domain-specific language that has some important limitations:

  - Functions can contain only a single `  return  ` statement. They cannot contain any additional logic. For example, they cannot execute loops or call external services.
  - Functions can automatically access functions and variables from the scope in which they are defined. For example, a function defined within the `  service cloud.firestore  ` scope has access to the `  resource  ` variable and built-in functions such as `  get()  ` and `  exists()  ` .
  - Functions may call other functions but may not recurse. The total call stack depth is limited to 10.
  - In rules version `  v2  ` , functions can define variables using the `  let  ` keyword. Functions can have up to 10 let bindings, but must end with a return statement.

A function is defined with the `  function  ` keyword and takes zero or more arguments. For example, you may want to combine the two types of conditions used in the examples above into a single function:

``` text
service cloud.firestore {
  match /databases/{database}/documents {
    // True if the user is signed in or the requested data is 'public'
    function signedInOrPublic() {
      return request.auth.uid != null || resource.data.visibility == 'public';
    }

    match /cities/{city} {
      allow read, write: if signedInOrPublic();
    }

    match /users/{user} {
      allow read, write: if signedInOrPublic();
    }
  }
}
```

Using functions in your security rules makes them more maintainable as the complexity of your rules grows.

## Rules are not filters

Once you secure your data and begin to write queries, keep in mind that security rules are not filters. You cannot write a query for all the documents in a collection and expect Firestore to return only the documents that the current client has permission to access.

For example, take the following security rule:

``` text
service cloud.firestore {
  match /databases/{database}/documents {
    // Allow the user to read data if the document has the 'visibility'
    // field set to 'public'
    match /cities/{city} {
      allow read: if resource.data.visibility == 'public';
    }
  }
}
```

Denied : This rule rejects the following query because the result set can include documents where `  visibility  ` is not `  public  ` :

##### Web

``` text
db.collection("cities").get()
    .then(function(querySnapshot) {
        querySnapshot.forEach(function(doc) {
            console.log(doc.id, " => ", doc.data());
    });
});
```

Allowed : This rule allows the following query because the `  where("visibility", "==", "public")  ` clause guarantees that the result set satisfies the rule's condition:

##### Web

``` text
db.collection("cities").where("visibility", "==", "public").get()
    .then(function(querySnapshot) {
        querySnapshot.forEach(function(doc) {
            console.log(doc.id, " => ", doc.data());
        });
    });
```

Firestore security rules evaluate each query against its potential result and fails the request if it could return a document that the client does not have permission to read. Queries must follow the constraints set by your security rules. For more on security rules and queries, see [securely querying data](/firestore/native/docs/security/rules-query) .

## Next steps

  - Learn how [security rules affect your queries](./rules-query) .
  - Learn how to [structure security rules](/firestore/native/docs/security/rules-structure) .
  - Read the [security rules reference](https://firebase.google.com/docs/reference/rules/rules) .
