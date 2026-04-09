Please provide C\# and Ruby samples that match Firestore and Datastore examples originally requested in the Firestore Doc Plan for Multiple Inequalities to GA and bug 351980346. The request is for turbo/469184.

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Query with range and inequality filters on multiple fields overview](/firestore/native/docs/query-data/multiple-range-fields)
  - [Query with range and inequality filters on multiple fields overview](https://firebase.google.com/docs/firestore/query-data/multiple-range-fields)

## Code sample

### C\#

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
CollectionReference citiesRef = db.Collection("cities");
Query query = citiesRef
    .WhereGreaterThan("Population", 1000000)
    .WhereLessThan("Density", 10000);
QuerySnapshot querySnapshot = await query.GetSnapshotAsync();
foreach (DocumentSnapshot documentSnapshot in querySnapshot)
{
    var name = documentSnapshot.GetValue<string>("Name");
    var population = documentSnapshot.GetValue<int>("Population");
    var density = documentSnapshot.GetValue<int>("Density");
    Console.WriteLine($"City '{name}' returned by query. Population={population}; Density={density}");
}
```

### Go

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` go
import (
 "context"
 "fmt"
 "io"

 "cloud.google.com/go/firestore"
)

func multipleInequalitiesQuery(w io.Writer, projectID string) error {
 ctx := context.Background()

 // Create client
 client, err := firestore.NewClient(ctx, projectID)
 if err != nil {
     return fmt.Errorf("firestore.NewClient: %w", err)
 }
 defer client.Close()

 // Create query
 query := client.Collection("cities").
     Where("population", ">", 1000000).
     Where("density", "<", 10000)

 // Get documents
 docSnapshots, err := query.Documents(ctx).GetAll()
 for _, doc := range docSnapshots {
     fmt.Fprintln(w, doc.Data())
 }
 if err != nil {
     return fmt.Errorf("GetAll: %w", err)
 }

 return nil
}
```

### Java

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
Query query =
    db.collection("cities")
        .whereGreaterThan("population", 1000000)
        .whereLessThan("density", 10000);
```

### PHP

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
$collection = $db->collection('samples/php/cities');
$chainedQuery = $collection
    ->where('population', '>', 1000000)
    ->where('density', '<', 10000);
```

### Python

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
query = (
    db.collection("cities")
    .where(filter=FieldFilter("population", ">", 1_000_000))
    .where(filter=FieldFilter("density", "<", 10_000))
)
```

### Ruby

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
cities_ref = firestore.col collection_path
compound_multi_ineq_query = cities_ref.where("population", ">", 1_000_000).where("density", "<", 5_000)
```

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](/docs/samples?product=firestore) .
