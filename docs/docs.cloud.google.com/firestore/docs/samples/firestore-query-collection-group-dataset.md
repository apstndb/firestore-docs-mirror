Create a collection of Firestore documents

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Perform simple and compound queries in Cloud Firestore](https://firebase.google.com/docs/firestore/query-data/queries)
  - [Query and filter data](/firestore/native/docs/query-data/queries)

## Code sample

### C\#

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
CollectionReference citiesRef = db.Collection("cities");
await citiesRef.Document("SF").Collection("landmarks").Document()
    .SetAsync(new { Name = "Golden Gate Bridge", Type = "bridge" });
await citiesRef.Document("SF").Collection("landmarks").Document()
    .SetAsync(new { Name = "Legion of Honor", Type = "museum" });
await citiesRef.Document("LA").Collection("landmarks").Document()
    .SetAsync(new { Name = "Griffith Park", Type = "park" });
await citiesRef.Document("DC").Collection("landmarks").Document()
    .SetAsync(new { Name = "Lincoln Memorial", Type = "memorial" });
await citiesRef.Document("DC").Collection("landmarks").Document()
    .SetAsync(new { Name = "National Air And Space Museum", Type = "museum" });
await citiesRef.Document("TOK").Collection("landmarks").Document()
    .SetAsync(new { Name = "Ueno Park", Type = "park" });
await citiesRef.Document("TOK").Collection("landmarks").Document()
    .SetAsync(new { Name = "National Museum of Nature and Science", Type = "museum" });
await citiesRef.Document("BJ").Collection("landmarks").Document()
    .SetAsync(new { Name = "Jingshan Park", Type = "park" });
await citiesRef.Document("BJ").Collection("landmarks").Document()
    .SetAsync(new { Name = "Beijing Ancient Observatory", Type = "museum" });
```

### Go

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` go
import (
 "context"
 "fmt"

 "cloud.google.com/go/firestore"
)

// collectionGroupSetup sets up a collection group to query.
func collectionGroupSetup(projectID, cityCollection string) error {
 ctx := context.Background()

 client, err := firestore.NewClient(ctx, projectID)
 if err != nil {
     return fmt.Errorf("firestore.NewClient: %w", err)
 }
 defer client.Close()

 landmarks := []struct {
     city, name, t string
 }{
     {"SF", "Golden Gate Bridge", "bridge"},
     {"SF", "Legion of Honor", "museum"},
     {"LA", "Griffith Park", "park"},
     {"LA", "The Getty", "museum"},
     {"DC", "Lincoln Memorial", "memorial"},
     {"DC", "National Air and Space Museum", "museum"},
     {"TOK", "Ueno Park", "park"},
     {"TOK", "National Museum of Nature and Science", "museum"},
     {"BJ", "Jingshan Park", "park"},
     {"BJ", "Beijing Ancient Observatory", "museum"},
 }

 cities := client.Collection(cityCollection)
 for _, l := range landmarks {
     if _, err := cities.Doc(l.city).Collection("landmarks").NewDoc().Set(ctx, map[string]string{
         "name": l.name,
         "type": l.t,
     }); err != nil {
         return fmt.Errorf("Set: %w", err)
     }
 }

 return nil
}
```

### Java

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
CollectionReference cities = db.collection("cities");

final List<ApiFuture<WriteResult>> futures =
    Arrays.asList(
        cities
            .document("SF")
            .collection("landmarks")
            .document()
            .set(
                new HashMap<String, String>() {
                  {
                    put("name", "Golden Gate Bridge");
                    put("type", "bridge");
                  }
                }),
        cities
            .document("SF")
            .collection("landmarks")
            .document()
            .set(
                new HashMap<String, String>() {
                  {
                    put("name", "Legion of Honor");
                    put("type", "museum");
                  }
                }),
        cities
            .document("LA")
            .collection("landmarks")
            .document()
            .set(
                new HashMap<String, String>() {
                  {
                    put("name", "Griffith Park");
                    put("type", "park");
                  }
                }),
        cities
            .document("LA")
            .collection("landmarks")
            .document()
            .set(
                new HashMap<String, String>() {
                  {
                    put("name", "The Getty");
                    put("type", "museum");
                  }
                }),
        cities
            .document("DC")
            .collection("landmarks")
            .document()
            .set(
                new HashMap<String, String>() {
                  {
                    put("name", "Lincoln Memorial");
                    put("type", "memorial");
                  }
                }),
        cities
            .document("DC")
            .collection("landmarks")
            .document()
            .set(
                new HashMap<String, String>() {
                  {
                    put("name", "National Air and Space Museum");
                    put("type", "museum");
                  }
                }),
        cities
            .document("TOK")
            .collection("landmarks")
            .document()
            .set(
                new HashMap<String, String>() {
                  {
                    put("name", "Ueno Park");
                    put("type", "park");
                  }
                }),
        cities
            .document("TOK")
            .collection("landmarks")
            .document()
            .set(
                new HashMap<String, String>() {
                  {
                    put("name", "National Museum of Nature and Science");
                    put("type", "museum");
                  }
                }),
        cities
            .document("BJ")
            .collection("landmarks")
            .document()
            .set(
                new HashMap<String, String>() {
                  {
                    put("name", "Jingshan Park");
                    put("type", "park");
                  }
                }),
        cities
            .document("BJ")
            .collection("landmarks")
            .document()
            .set(
                new HashMap<String, String>() {
                  {
                    put("name", "Beijing Ancient Observatory");
                    put("type", "museum");
                  }
                }));
final List<WriteResult> landmarks = ApiFutures.allAsList(futures).get();
```

### Node.js

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` javascript
const citiesRef = db.collection('cities');

await citiesRef.doc('SF').collection('landmarks').doc().set({
  name: 'Golden Gate Bridge',
  type: 'bridge'
});
await citiesRef.doc('SF').collection('landmarks').doc().set({
  name: 'Legion of Honor',
  type: 'museum'
});
await citiesRef.doc('LA').collection('landmarks').doc().set({
  name: 'Griffith Park',
  type: 'park'
});
await citiesRef.doc('LA').collection('landmarks').doc().set({
  name: 'The Getty',
  type: 'museum'
});
await citiesRef.doc('DC').collection('landmarks').doc().set({
  name: 'Lincoln Memorial',
  type: 'memorial'
});
await citiesRef.doc('DC').collection('landmarks').doc().set({
  name: 'National Air and Space Museum',
  type: 'museum'
});
await citiesRef.doc('TOK').collection('landmarks').doc().set({
  name: 'Ueno Park',
  type: 'park'
});
await citiesRef.doc('TOK').collection('landmarks').doc().set({
  name: 'National Museum of Nature and Science',
  type: 'museum'
});
await citiesRef.doc('BJ').collection('landmarks').doc().set({
  name: 'Jingshan Park',
  type: 'park'
});
await citiesRef.doc('BJ').collection('landmarks').doc().set({ 
  name: 'Beijing Ancient Observatory',
  type: 'museum'
});
```

### PHP

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
$citiesRef = $db->collection('samples/php/cities');
$citiesRef->document('SF')->collection('landmarks')->newDocument()->set([
    'name' => 'Golden Gate Bridge',
    'type' => 'bridge'
]);
$citiesRef->document('SF')->collection('landmarks')->newDocument()->set([
    'name' => 'Legion of Honor',
    'type' => 'museum'
]);
$citiesRef->document('LA')->collection('landmarks')->newDocument()->set([
    'name' => 'Griffith Park',
    'type' => 'park'
]);
$citiesRef->document('LA')->collection('landmarks')->newDocument()->set([
    'name' => 'The Getty',
    'type' => 'museum'
]);
$citiesRef->document('DC')->collection('landmarks')->newDocument()->set([
    'name' => 'Lincoln Memorial',
    'type' => 'memorial'
]);
$citiesRef->document('DC')->collection('landmarks')->newDocument()->set([
    'name' => 'National Air and Space Museum',
    'type' => 'museum'
]);
$citiesRef->document('TOK')->collection('landmarks')->newDocument()->set([
    'name' => 'Ueno Park',
    'type' => 'park'
]);
$citiesRef->document('TOK')->collection('landmarks')->newDocument()->set([
    'name' => 'National Museum of Nature and Science',
    'type' => 'museum'
]);
$citiesRef->document('BJ')->collection('landmarks')->newDocument()->set([
    'name' => 'Jingshan Park',
    'type' => 'park'
]);
$citiesRef->document('BJ')->collection('landmarks')->newDocument()->set([
    'name' => 'Beijing Ancient Observatory',
    'type' => 'museum'
]);
print('Added example landmarks collections to the cities collection.' . PHP_EOL);
```

### Python

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
cities = db.collection("cities")

sf_landmarks = cities.document("SF").collection("landmarks")
sf_landmarks.document().set({"name": "Golden Gate Bridge", "type": "bridge"})
sf_landmarks.document().set({"name": "Legion of Honor", "type": "museum"})
la_landmarks = cities.document("LA").collection("landmarks")
la_landmarks.document().set({"name": "Griffith Park", "type": "park"})
la_landmarks.document().set({"name": "The Getty", "type": "museum"})
dc_landmarks = cities.document("DC").collection("landmarks")
dc_landmarks.document().set({"name": "Lincoln Memorial", "type": "memorial"})
dc_landmarks.document().set(
    {"name": "National Air and Space Museum", "type": "museum"}
)
tok_landmarks = cities.document("TOK").collection("landmarks")
tok_landmarks.document().set({"name": "Ueno Park", "type": "park"})
tok_landmarks.document().set(
    {"name": "National Museum of Nature and Science", "type": "museum"}
)
bj_landmarks = cities.document("BJ").collection("landmarks")
bj_landmarks.document().set({"name": "Jingshan Park", "type": "park"})
bj_landmarks.document().set(
    {"name": "Beijing Ancient Observatory", "type": "museum"}
)
```

### Ruby

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
cities_ref = firestore.col collection_path

sf_landmarks = cities_ref.document("SF").collection("landmarks")
sf_landmarks.document.set(
  {
    name: "Golden Gate Bridge",
    type: "bridge"
  }
)
sf_landmarks.document.set(
  {
    name: "Legion of Honor",
    type: "museum"
  }
)

la_landmarks = cities_ref.document("LA").collection("landmarks")
la_landmarks.document.set(
  {
    name: "Griffith Park",
    type: "park"
  }
)
la_landmarks.document.set(
  {
    name: "The Getty",
    type: "museum"
  }
)

dc_landmarks = cities_ref.document("DC").collection("landmarks")
dc_landmarks.document.set(
  {
    name: "Lincoln Memorial",
    type: "memorial"
  }
)
dc_landmarks.document.set(
  {
    name: "National Air and Space Museum",
    type: "museum"
  }
)

tok_landmarks = cities_ref.document("TOK").collection("landmarks")
tok_landmarks.document.set(
  {
    name: "Ueno Park",
    type: "park"
  }
)
tok_landmarks.document.set(
  {
    name: "National Museum of Nature and Science",
    type: "museum"
  }
)

bj_landmarks = cities_ref.document("BJ").collection("landmarks")
bj_landmarks.document.set(
  {
    name: "Jingshan Park",
    type: "park"
  }
)
bj_landmarks.document.set(
  {
    name: "Beijing Ancient Observatory",
    type: "museum"
  }
)
```

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](/docs/samples?product=firestore) .
