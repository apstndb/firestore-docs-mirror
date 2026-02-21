Getting Firestore documents from a collection

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Create a Firestore database by using a server client library](/firestore/native/docs/create-database-server-client-library)
  - [Get started with Cloud Firestore](https://firebase.google.com/docs/firestore/quickstart)

## Code sample

### C\#

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
CollectionReference usersRef = db.Collection("users");
QuerySnapshot snapshot = await usersRef.GetSnapshotAsync();
foreach (DocumentSnapshot document in snapshot.Documents)
{
    Console.WriteLine("User: {0}", document.Id);
    Dictionary<string, object> documentDictionary = document.ToDictionary();
    Console.WriteLine("First: {0}", documentDictionary["First"]);
    if (documentDictionary.ContainsKey("Middle"))
    {
        Console.WriteLine("Middle: {0}", documentDictionary["Middle"]);
    }
    Console.WriteLine("Last: {0}", documentDictionary["Last"]);
    Console.WriteLine("Born: {0}", documentDictionary["Born"]);
    Console.WriteLine();
}
```

### Go

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` go
iter := client.Collection("users").Documents(ctx)
for {
 doc, err := iter.Next()
 if err == iterator.Done {
     break
 }
 if err != nil {
     log.Fatalf("Failed to iterate: %v", err)
 }
 fmt.Println(doc.Data())
}
```

### Java

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
// asynchronously retrieve all users
ApiFuture<QuerySnapshot> query = db.collection("users").get();
// ...
// query.get() blocks on response
QuerySnapshot querySnapshot = query.get();
List<QueryDocumentSnapshot> documents = querySnapshot.getDocuments();
for (QueryDocumentSnapshot document : documents) {
  System.out.println("User: " + document.getId());
  System.out.println("First: " + document.getString("first"));
  if (document.contains("middle")) {
    System.out.println("Middle: " + document.getString("middle"));
  }
  System.out.println("Last: " + document.getString("last"));
  System.out.println("Born: " + document.getLong("born"));
}
```

### Node.js

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` javascript
const snapshot = await db.collection('users').get();
snapshot.forEach((doc) => {
  console.log(doc.id, '=>', doc.data());
});
```

### PHP

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
$usersRef = $db->collection('samples/php/users');
$snapshot = $usersRef->documents();
foreach ($snapshot as $user) {
    printf('User: %s' . PHP_EOL, $user->id());
    printf('First: %s' . PHP_EOL, $user['first']);
    if (!empty($user['middle'])) {
        printf('Middle: %s' . PHP_EOL, $user['middle']);
    }
    printf('Last: %s' . PHP_EOL, $user['last']);
    printf('Born: %d' . PHP_EOL, $user['born']);
    printf(PHP_EOL);
}
printf('Retrieved and printed out all documents from the users collection.' . PHP_EOL);
```

### Python

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
users_ref = db.collection("users")
docs = users_ref.stream()

for doc in docs:
    print(f"{doc.id} => {doc.to_dict()}")
```

### Ruby

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
users_ref = firestore.col collection_path
users_ref.get do |user|
  puts "#{user.document_id} data: #{user.data}."
end
```

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](/docs/samples?product=firestore) .
