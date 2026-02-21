# Control access to specific fields

This page builds on the concepts in [Structuring Security Rules](./rules-structure) and [Writing Conditions for Security Rules](./rules-conditions) to explain how you can use Firestore Security Rules to create rules that allow clients to perform operations on some fields in a document but not others.

**Note:** The server client libraries bypass all Firestore Security Rules and instead authenticate through [Google Application Default Credentials](https://cloud.google.com/docs/authentication/production) . If you're using the server client libraries or the REST or RPC APIs, make sure to set up [Identity and Access Management (IAM) for Firestore](https://cloud.google.com/firestore/docs/security/iam) .

There may be times when you want to control changes to a document not at the document level but at the field level.

For instance, you might want to allow a client to create or change a document, but not allow them to edit certain fields in that document. Or you may wish to enforce that any document that a client always creates contains a certain set of fields. This guide covers how you can accomplish some of these tasks using Firestore Security Rules.

## Allowing read access only for specific fields

Reads in Firestore are performed at the document level. You either retrieve the full document, or you retrieve nothing. There is no way to retrieve a partial document. It is impossible using security rules alone to prevent users from reading specific fields within a document.

If there are certain fields within a document that you want to keep hidden from some users, the best way would be to put them in a separate document. For instance, you might consider creating a document in a `  private  ` subcollection like so:

**/employees/{emp\_id}**

``` text
  name: "Alice Hamilton",
  department: 461,
  start_date: <timestamp>
```

**/employees/{emp\_id}/private/finances**

``` text
    salary: 80000,
    bonus_mult: 1.25,
    perf_review: 4.2
```

Then you can add security rules that have different levels of access for the two collections. In this example, we're using [custom auth claims](https://firebase.google.com/docs/auth/admin/custom-claims) to say that only users with the custom auth claim `  role  ` equal to `  Finance  ` can view an employee's financial information.

``` text
service cloud.firestore {
  match /databases/{database}/documents {
    // Allow any logged in user to view the public employee data
    match /employees/{emp_id} {
      allow read: if request.resource.auth != null
      // Allow only users with the custom auth claim of "Finance" to view
      // the employee's financial data
      match /private/finances {
        allow read: if request.resource.auth &&
          request.resource.auth.token.role == 'Finance'
      }
    }
  }
}
```

## Restricting fields on document creation

Firestore is schemaless, meaning that there are no restrictions at the database level for what fields a document contains. While this flexibility can make development easier, there will be times when you want to ensure that clients can only create documents that contain specific fields, or don't contain other fields.

You can create these rules by examining the `  keys  ` method of the [`  request.resource.data  `](https://firebase.google.com/docs/reference/rules/rules.firestore.Resource#data) object. This is a list of all fields that the client is attempting to write in this new document. By combining this set of fields with functions like [`  hasOnly()  `](https://firebase.google.com/docs/reference/rules/rules.List#hasOnly) or [`  hasAny()  `](https://firebase.google.com/docs/reference/rules/rules.List#hasAny) , you can add in logic that restricts the types of documents a user can add to Firestore.

### Requiring specific fields in new documents

Let's say you wanted to make sure that all documents created in a `  restaurant  ` collection contained at least a `  name  ` , `  location  ` , and `  city  ` field. You could do that by calling [`  hasAll()  `](https://firebase.google.com/docs/reference/rules/rules.List#hasAll) on the list of keys in the new document.

``` text
service cloud.firestore {
  match /databases/{database}/documents {
    // Allow the user to create a document only if that document contains a name
    // location, and city field
    match /restaurant/{restId} {
      allow create: if request.resource.data.keys().hasAll(['name', 'location', 'city']);
    }
  }
}
```

This allows restaurants to be created with other fields as well, but it ensures that all documents created by a client contain at least these three fields.

### Forbidding specific fields in new documents

Similarly, you can prevent clients from creating documents that contain specific fields by using [`  hasAny()  `](https://firebase.google.com/docs/reference/rules/rules.List#hasAny) against a list of forbidden fields. This method evaluates to true if a document contains any of these fields, so you probably want to negate the result in order to forbid certain fields.

For instance, in the following example, clients are not allowed to create a document that contains an `  average_score  ` or `  rating_count  ` field since these fields will be added by a server call at a later point.

``` text
service cloud.firestore {
  match /databases/{database}/documents {
    // Allow the user to create a document only if that document does *not*
    // contain an average_score or rating_count field.
    match /restaurant/{restId} {
      allow create: if (!request.resource.data.keys().hasAny(
        ['average_score', 'rating_count']));
    }
  }
}
```

### Creating an allowlist of fields for new documents

Instead of forbidding certain fields in new documents, you might want to create a list of only those fields that are explicitly allowed in new documents. Then you can use the [`  hasOnly()  `](https://firebase.google.com/docs/reference/rules/rules.List#hasOnly) function to make sure that any new documents created contain just these fields (or a subset of these fields) and no other.

``` text
service cloud.firestore {
  match /databases/{database}/documents {
    // Allow the user to create a document only if that document doesn't contain
    // any fields besides the ones listed below.
    match /restaurant/{restId} {
      allow create: if (request.resource.data.keys().hasOnly(
        ['name', 'location', 'city', 'address', 'hours', 'cuisine']));
    }
  }
}
```

### Combining required and optional fields

You can combine `  hasAll  ` and `  hasOnly  ` operations together in your security rules to require some fields and allow others. For instance, this example requires that all new documents contain the `  name  ` , `  location  ` , and `  city  ` fields, and optionally allows the `  address  ` , `  hours  ` , and `  cuisine  ` fields.

``` text
service cloud.firestore {
  match /databases/{database}/documents {
    // Allow the user to create a document only if that document has a name,
    // location, and city field, and optionally address, hours, or cuisine field
    match /restaurant/{restId} {
      allow create: if (request.resource.data.keys().hasAll(['name', 'location', 'city'])) &&
       (request.resource.data.keys().hasOnly(
           ['name', 'location', 'city', 'address', 'hours', 'cuisine']));
    }
  }
}
```

In a real-world scenario, you may wish to move this logic into a helper function to avoid duplicating your code and to more easily combine the optional and required fields into a single list, like so:

``` text
service cloud.firestore {
  match /databases/{database}/documents {
    function verifyFields(required, optional) {
      let allAllowedFields = required.concat(optional);
      return request.resource.data.keys().hasAll(required) &&
        request.resource.data.keys().hasOnly(allAllowedFields);
    }
    match /restaurant/{restId} {
      allow create: if verifyFields(['name', 'location', 'city'],
        ['address', 'hours', 'cuisine']);
    }
  }
}
```

## Restricting fields on update

A common security practice is to only allow clients to edit some fields and not others. You cannot accomplish this solely by looking at the `  request.resource.data.keys()  ` list described in the previous section, since this list represents the complete document as it would look after the update, and would therefore include fields that the client did not change.

However, if you were to use the [`  diff()  `](https://firebase.google.com/docs/reference/rules/rules.Map#diff) function, you could compare `  request.resource.data  ` with the `  resource.data  ` object, which represents the document in the database before the update. This creates a [`  mapDiff  `](https://firebase.google.com/docs/reference/rules/rules.MapDiff) object, which is an object containing all of the changes between two different maps.

By calling the [`  affectedKeys()  `](https://firebase.google.com/docs/reference/rules/rules.MapDiff#affectedKeys) method on this mapDiff, you can come up with a set of fields that were changed in an edit. Then you can use functions like [`  hasOnly()  `](https://firebase.google.com/docs/reference/rules/rules.Set#hasOnly) or [`  hasAny()  `](https://firebase.google.com/docs/reference/rules/rules.Set#hasAny) to ensure that this set does (or doesn't) contain certain items.

### Preventing some fields from being changed

By using the [`  hasAny()  `](https://firebase.google.com/docs/reference/rules/rules.Set#hasAny) method on the set generated by [`  affectedKeys()  `](https://firebase.google.com/docs/reference/rules/rules.MapDiff#affectedKeys) and then negating the result, you can reject any client request that attempts to change fields that you don't want changed.

For instance, you might want to allow clients to update information about a restaurant but not change their average score or number of reviews.

``` text
service cloud.firestore {
  match /databases/{database}/documents {
    match /restaurant/{restId} {
      // Allow the client to update a document only if that document doesn't
      // change the average_score or rating_count fields
      allow update: if (!request.resource.data.diff(resource.data).affectedKeys()
        .hasAny(['average_score', 'rating_count']));
    }
  }
}
```

### Allowing only certain fields to be changed

Rather than specifying fields that you don't want changed, you can also use the [`  hasOnly()  `](https://firebase.google.com/docs/reference/rules/rules.Set#hasOnly) function to specify a list of fields that you do want changed. This is generally considered more secure because writes to any new document fields are disallowed by default until you explicitly allow them in your security rules.

For instance, rather than disallowing the `  average_score  ` and `  rating_count  ` field, you could create security rules that allow clients to only change the `  name  ` , `  location  ` , `  city  ` , `  address  ` , `  hours  ` , and `  cuisine  ` fields.

``` text
service cloud.firestore {
  match /databases/{database}/documents {
    match /restaurant/{restId} {
    // Allow a client to update only these 6 fields in a document
      allow update: if (request.resource.data.diff(resource.data).affectedKeys()
        .hasOnly(['name', 'location', 'city', 'address', 'hours', 'cuisine']));
    }
  }
}
```

This means that if, in some future iteration of your app, restaurant documents include a `  telephone  ` field, attempts to edit that field would fail until you go back and add that field to the `  hasOnly()  ` list in your security rules.

## Enforcing field types

Another effect of Firestore being schemaless is that there is no enforcement at the database level for what types of data can be stored in specific fields. This is something you can enforce in security rules, however, with the `  is  ` operator.

For example, the following security rule enforces that a review's `  score  ` field has to be an integer, the `  headline  ` , `  content  ` , and `  author_name  ` fields are strings, and the `  review_date  ` is a timestamp.

``` text
service cloud.firestore {
  match /databases/{database}/documents {
    match /restaurant/{restId} {
      // Restaurant rules go here...
      match /review/{reviewId} {
        allow create: if (request.resource.data.score is int &&
          request.resource.data.headline is string &&
          request.resource.data.content is string &&
          request.resource.data.author_name is string &&
          request.resource.data.review_date is timestamp
        );
      }
    }
  }
}
```

Valid data types for the `  is  ` operator are `  bool  ` , `  bytes  ` , `  float  ` , `  int  ` , `  list  ` , `  latlng  ` , `  number  ` , `  path  ` , `  map  ` , `  string  ` , and `  timestamp  ` . The `  is  ` operator also supports `  constraint  ` , `  duration  ` , `  set  ` , and `  map_diff  ` data types, but since these are generated by the security rules language itself and not generated by clients, you rarely use them in most practical applications.

`  list  ` and `  map  ` data types do not have support for generics, or type arguments. In other words, you can use security rules to enforce that a certain field contains a list or a map, but you can not enforce that a field contains a list of all integers or all strings.

Similarly, you can use security rules to enforce type values for specific entries in a list or a map (using brakets notation or key names respectively), but there is no shortcut to enforce the data types of all members in a map or a list at once.

For example, the following rules ensure that a `  tags  ` field in a document contains a list and that the first entry is a string. It also ensures that the `  product  ` field contains a map that in turn contains a product name that is a string and a quantity that is an integer.

``` text
service cloud.firestore {
  match /databases/{database}/documents {
  match /orders/{orderId} {
    allow create: if request.resource.data.tags is list &&
      request.resource.data.tags[0] is string &&
      request.resource.data.product is map &&
      request.resource.data.product.name is string &&
      request.resource.data.product.quantity is int
      }
    }
  }
}
```

Field types need to be enforced when both creating and updating a document. Therefore, you might want to consider creating a helper function that you can call in both the create and update sections of your security rules.

``` text
service cloud.firestore {
  match /databases/{database}/documents {

  function reviewFieldsAreValidTypes(docData) {
     return docData.score is int &&
          docData.headline is string &&
          docData.content is string &&
          docData.author_name is string &&
          docData.review_date is timestamp;
  }

   match /restaurant/{restId} {
      // Restaurant rules go here...
      match /review/{reviewId} {
        allow create: if reviewFieldsAreValidTypes(request.resource.data) &&
          // Other rules may go here
        allow update: if reviewFieldsAreValidTypes(request.resource.data) &&
          // Other rules may go here
      }
    }
  }
}
```

### Enforcing types for optional fields

It's important to remember that calling `  request.resource.data.foo  ` on a document where `  foo  ` doesn't exist results in an error, and therefore any security rule making that call will deny the request. You can handle this situation by using the [`  get  `](https://firebase.google.com/docs/reference/rules/rules.Map#get) method on `  request.resource.data  ` . The `  get  ` method allows you to provide a default argument for the field you're retrieving from a map if that field doesn't exist.

For example, if review documents also contain an optional `  photo_url  ` field and an optional `  tags  ` field that you want to verify are strings and lists respectively, you can accomplish this by rewriting the `  reviewFieldsAreValidTypes  ` function to something like the following:

``` text
  function reviewFieldsAreValidTypes(docData) {
     return docData.score is int &&
          docData.headline is string &&
          docData.content is string &&
          docData.author_name is string &&
          docData.review_date is timestamp &&
          docData.get('photo_url', '') is string &&
          docData.get('tags', []) is list;
  }
```

This rejects documents where `  tags  ` exists, but isn't a list, while still permitting documents that don't contain a `  tags  ` (or `  photo_url  ` ) field.

## Partial writes are never allowed

One final note about Firestore Security Rules is that they either allow the client to make a change to a document, or they reject the entire edit. You cannot create security rules that accept writes to some fields in your document while rejecting others in the same operation.
