# Secure data access for users and groups

Many collaborative apps allow users to read and write different pieces of data based on a set of permissions. In a document editing app, for example, users may want to allow a few users to read and write their documents while blocking unwanted access.

**Note:** The server client libraries bypass all Firestore Security Rules and instead authenticate through [Google Application Default Credentials](https://cloud.google.com/docs/authentication/production) . If you're using the server client libraries or the REST or RPC APIs, make sure to set up [Identity and Access Management (IAM) for Firestore](https://cloud.google.com/firestore/docs/security/iam) .

## Solution: Role-Based Access Control

You can take advantage of Cloud Firestore's data model as well as custom [security rules](../security/get-started) to implement role-based access control in your app.

Suppose you are building a collaborative writing application in which users can create "stories" and "comments" with the following security requirements:

  - Each story has one owner and can be shared with "writers", "commenters", and "readers".
  - *Readers* can only see stories and comments. They cannot edit anything.
  - *Commenters* have all the access of readers, and they can also add comments to a story.
  - *Writers* have all the access of commenters, and they can also edit story content.
  - *Owners* can edit any part of a story as well as control the access of other users.

### Data Structure

Assume your app has a `  stories  ` collection where each document represents a story. Each story also has a `  comments  ` subcollection where each document is a comment on that story.

To keep track of access roles, add a `  roles  ` field which is a map of user IDs to roles:

**/stories/{storyid}**

``` text
{
  title: "A Great Story",
  content: "Once upon a time ...",
  roles: {
    alice: "owner",
    bob: "reader",
    david: "writer",
    jane: "commenter"
    // ...
  }
}
```

Comments contain only two fields, the author's user ID and some content:

**/stories/{storyid}/comments/{commentid}**

``` text
{
  user: "alice",
  content: "I think this is a great story!"
}
```

### Rules

Now that you have users' roles recorded in the database, you need to write Security Rules to validate them. These rules assume the app uses [Firebase Auth](https://firebase.google.com/docs/auth/) so that the `  request.auth.uid  ` variable is the user's ID.

**Step 1** : Start with a basic rules file, which includes empty rules for stories and comments:

``` text
service cloud.firestore {
   match /databases/{database}/documents {
     match /stories/{story} {
         // TODO: Story rules go here...

         match /comments/{comment} {
            // TODO: Comment rules go here...
         }
     }
   }
}step1-invalid.rules
```

**Step 2** : Add a simple `  write  ` rule that gives owners complete control over stories. The functions defined help determine a user's roles and if new documents are valid:

``` text
service cloud.firestore {
   match /databases/{database}/documents {
     match /stories/{story} {
        function isSignedIn() {
          return request.auth != null;
        }

        function getRole(rsc) {
          // Read from the "roles" map in the resource (rsc).
          return rsc.data.roles[request.auth.uid];
        }

        function isOneOfRoles(rsc, array) {
          // Determine if the user is one of an array of roles
          return isSignedIn() && (getRole(rsc) in array);
        }

        function isValidNewStory() {
          // Valid if story does not exist and the new story has the correct owner.
          return resource == null && isOneOfRoles(request.resource, ['owner']);
        }

        // Owners can read, write, and delete stories
        allow write: if isValidNewStory() || isOneOfRoles(resource, ['owner']);

         match /comments/{comment} {
            // ...
         }
     }
   }
}step2.rules
```

**Step 3** : Write rules that allow a user of any role to read stories and comments. Using the functions defined in the previous step keeps the rules concise and readable:

``` text
service cloud.firestore {
   match /databases/{database}/documents {
     match /stories/{story} {
        function isSignedIn() {
          return request.auth != null;
        }

        function getRole(rsc) {
          return rsc.data.roles[request.auth.uid];
        }

        function isOneOfRoles(rsc, array) {
          return isSignedIn() && (getRole(rsc) in array);
        }

        function isValidNewStory() {
          return resource == null
            && request.resource.data.roles[request.auth.uid] == 'owner';
        }

        allow write: if isValidNewStory() || isOneOfRoles(resource, ['owner']);

        // Any role can read stories.
        allow read: if isOneOfRoles(resource, ['owner', 'writer', 'commenter', 'reader']);

        match /comments/{comment} {
          // Any role can read comments.
          allow read: if isOneOfRoles(get(/databases/$(database)/documents/stories/$(story)),
                                      ['owner', 'writer', 'commenter', 'reader']);
        }
     }
   }
}step3.rules
```

**Step 4** : Allow story writers, commenters, and owners to post comments. Note that this rule also validates that the `  owner  ` of the comment matches the requesting user, which prevents users from writing over each other's comments:

``` text
service cloud.firestore {
   match /databases/{database}/documents {
     match /stories/{story} {
        function isSignedIn() {
          return request.auth != null;
        }

        function getRole(rsc) {
          return rsc.data.roles[request.auth.uid];
        }

        function isOneOfRoles(rsc, array) {
          return isSignedIn() && (getRole(rsc) in array);
        }

        function isValidNewStory() {
          return resource == null
            && request.resource.data.roles[request.auth.uid] == 'owner';
        }

        allow write: if isValidNewStory() || isOneOfRoles(resource, ['owner'])
        allow read: if isOneOfRoles(resource, ['owner', 'writer', 'commenter', 'reader']);

        match /comments/{comment} {
          allow read: if isOneOfRoles(get(/databases/$(database)/documents/stories/$(story)),
                                      ['owner', 'writer', 'commenter', 'reader']);

          // Owners, writers, and commenters can create comments. The
          // user id in the comment document must match the requesting
          // user's id.
          //
          // Note: we have to use get() here to retrieve the story
          // document so that we can check the user's role.
          allow create: if isOneOfRoles(get(/databases/$(database)/documents/stories/$(story)),
                                        ['owner', 'writer', 'commenter'])
                        && request.resource.data.user == request.auth.uid;
        }
     }
   }
}
step4.rules
```

**Step 5** : Give writers the ability to edit story content, but not to edit story roles or change any other properties of the document. This requires splitting the stories `  write  ` rule into separate rules for `  create  ` , `  update  ` , and `  delete  ` since writers can only update stories:

``` text
service cloud.firestore {
   match /databases/{database}/documents {
     match /stories/{story} {
        function isSignedIn() {
          return request.auth != null;
        }

        function getRole(rsc) {
          return rsc.data.roles[request.auth.uid];
        }

        function isOneOfRoles(rsc, array) {
          return isSignedIn() && (getRole(rsc) in array);
        }

        function isValidNewStory() {
          return request.resource.data.roles[request.auth.uid] == 'owner';
        }

        function onlyContentChanged() {
          // Ensure that title and roles are unchanged and that no new
          // fields are added to the document.
          return request.resource.data.title == resource.data.title
            && request.resource.data.roles == resource.data.roles
            && request.resource.data.keys() == resource.data.keys();
        }

        // Split writing into creation, deletion, and updating. Only an
        // owner can create or delete a story but a writer can update
        // story content.
        allow create: if isValidNewStory();
        allow delete: if isOneOfRoles(resource, ['owner']);
        allow update: if isOneOfRoles(resource, ['owner'])
                      || (isOneOfRoles(resource, ['writer']) && onlyContentChanged());
        allow read: if isOneOfRoles(resource, ['owner', 'writer', 'commenter', 'reader']);

        match /comments/{comment} {
          allow read: if isOneOfRoles(get(/databases/$(database)/documents/stories/$(story)),
                                      ['owner', 'writer', 'commenter', 'reader']);
          allow create: if isOneOfRoles(get(/databases/$(database)/documents/stories/$(story)),
                                        ['owner', 'writer', 'commenter'])
                        && request.resource.data.user == request.auth.uid;
        }
     }
   }
}
step5.rules
```

## Limitations

The solution shown above demonstrates securing user data using Security Rules, but you should be aware of the following limitations:

  - **Granularity** : In the example above, multiple roles (writer and owner) have write access to the same document but with different limitations. This can become hard to manage with more complex documents and it may be better to split single documents into multiple documents each owned by a single role.
  - **Large Groups** : If you need to share with very large or complex groups, consider a system where roles are stored in their own collection rather than as a field on the target document.
