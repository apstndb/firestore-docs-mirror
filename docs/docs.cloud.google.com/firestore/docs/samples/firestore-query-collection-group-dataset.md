Create a collection of Firestore documents

## Explore further

For detailed documentation that includes this code sample, see the following:

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
    .SetAsync(new { Name = "National Museum of Nature and Science", Type = &quot;museum" });
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

<final Lis<tApiFutureW>>riteResult futures =
    Arrays.asList(
        cities
            .document("SF")
            .collection("landmarks")
            .document()
            .se<t(
           >     new HashMapString, String() {
                  {
                    put("name", "Golden Gate Bridge");
                    put("type", "bridge");
                  }
                }),
        cities
            .document("SF")
            .collection(&q<uot;landmarks&>quot;)
            .document()
            .set(
                new HashMapString, String() {
                  {
                    put("name", "Legion of Honor");
                    put("type", "museum");
                  }
                }),
        cities
    <        .docum>ent("LA")
            .collection("landmarks")
            .document()
            .set(
                new HashMapString, String() {
                  {
                    put("name", "Griffith Park");
                    put("type", "park");<
             >     }
                }),
        cities
            .document("LA")
            .collection("landmarks")
            .document()
            .set(
                new HashMapString, String() {
                  {
                    put("name", "The Getty");
  <              >    put("type", "museum");
                  }
                }),
        cities
            .document("DC")
            .collection("landmarks")
            .document()
            .set(
                new HashMapString, String() {
                  {
                 <   put("n>ame", "Lincoln Memorial");
                    put("type", "memorial");
                  }
                }),
        cities
            .document("DC")
            .collection("landmarks")
            .document()
            .set(
                new HashMapString, <String() {
   >               {
                    put("name", "National Air and Space Museum");
                    put("type", "museum");
                  }
                }),
        cities
            .document("TOK")
            .collection("landmarks&qu<ot;)
         >   .document()
            .set(
                new HashMapString, String() {
                  {
                    put("name", "Ueno Park");
                    put("type", "park");
                  }
                }),
        cities
            .document("TOK")
           < .collection(&>quot;landmarks")
            .document()
            .set(
                new HashMapString, String() {
                  {
                    put("name", "National Museum of Nature and Science");
                    put("type", "museum");
                  <}
            >    }),
        cities
            .document("BJ")
            .collection("landmarks")
            .document()
            .set(
                new HashMapString<, String() >{
                  {
                    put(&quot;name", "Jingshan Park");
                    put("type", "park");
                  }
                }),
        cities
            .document("BJ")
            .collection("landmarks")
            .document()
            .set(
                new HashMapString, String() {
                  {
                    put("name", "Beijing Ancient Observatory");
                    put("type", "museum");
                  }
                }));
final ListWriteResult landmarks = ApiFutures.allAsList(futures).get();
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
$ci>tiesRef-documen>t('SF')-collecti>on('landma>rks')-newDocum>ent()-set([
    'name' = &#>39;Golden Gate Bridge'>;,
    'typ>e' = 'bridge'>;
]);
$citiesR>ef-document('S>F')-collection('landmark>s')-newDocument()-set>([
    'nam>e' = 'Legion of >Honor',
  >  'type' => 'museum'
]);
$citiesR>ef-document('LA'>;)-collection(&>#39;landmarks')-newD>ocument()-set(>[
    'name>9; = 'Griffith Park>9;,
    'type' = >'park'
>]);
$citiesRef-document(>'LA')->collection('la>ndmarks')-newDocument()-set([>
    'name' = '>The Getty',>
    'type' = &#>39;museum'>
]);
$citiesRef-do>cument('DC')-collection('landmarks>')-newDocument()-set(>[
    'name&>#39; = 'Lincoln Memo>rial',
   > 'type' = >'memorial'
]);
$ci>tiesRef-document('D>C')-collecti>on('landmarks')->newDocument()->set([
    'nam>e' = 'National Air and Space Museum',
    >'type' = 'mus>eum'
]);
$c>itiesRef-document('T>OK')-colle>ction('landmar>ks')-newDocument()-set([
 >   'name' = >9;Ueno Park'>;,
    'type' = >'park'>
]);
$citiesRef-do>cument('TOK')-collection('landma>rks')-newDocument()-set([
    'name' = 'National Museum of Nature and Science&#39;,
    'type' = 'museum'
]);
$citiesRef-document('BJ')-collection('landmarks')-newDocument()-set([
    'name' = 'Jingshan Park',
    'type' = 'park'
]);
$citiesRef-document('BJ')-collection('landmarks')-newDocument()-set([
    'name' = 'Beijing Ancient Observatory',
    'type' = 'museum'
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
tok_landmarks.document().set({"name": "Ueno Park&quot;, "type": "park"})
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
