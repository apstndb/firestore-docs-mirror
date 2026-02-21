Get Firestore Documents created from custom classes

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Get data with Cloud Firestore](https://firebase.google.com/docs/firestore/query-data/get-data)
  - [Getting data](/firestore/native/docs/query-data/get-data)
  - [Perform simple and compound queries in Cloud Firestore](https://firebase.google.com/docs/firestore/query-data/queries)
  - [Query and filter data](/firestore/native/docs/query-data/queries)

## Code sample

### C\#

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
CollectionReference citiesRef = db.Collection("cities");
await citiesRef.Document("SF").SetAsync(new Dictionary<string, object>(){
    { "Name", "San Francisco" },
    { "State", "CA" },
    { "Country", "USA" },
    { "Capital", false },
    { "Population", 860000 }
});
await citiesRef.Document("LA").SetAsync(new Dictionary<string, object>(){
    { "Name", "Los Angeles" },
    { "State", "CA" },
    { "Country", "USA" },
    { "Capital", false },
    { "Population", 3900000 }
});
await citiesRef.Document("DC").SetAsync(new Dictionary<string, object>(){
    { "Name", "Washington D.C." },
    { "State", null },
    { "Country", "USA" },
    { "Capital", true },
    { "Population", 680000 }
});
await citiesRef.Document("TOK").SetAsync(new Dictionary<string, object>(){
    { "Name", "Tokyo" },
    { "State", null },
    { "Country", "Japan" },
    { "Capital", true },
    { "Population", 9000000 }
});
await citiesRef.Document("BJ").SetAsync(new Dictionary<string, object>(){
    { "Name", "Beijing" },
    { "State", null },
    { "Country", "China" },
    { "Capital", true },
    { "Population", 21500000 }
});
Console.WriteLine("Added example cities data to the cities collection.");
```

### Go

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` go
import (
 "context"

 "cloud.google.com/go/firestore"
)

func prepareRetrieve(ctx context.Context, client *firestore.Client) error {
 cities := []struct {
     id string
     c  City
 }{
     {id: "SF", c: City{Name: "San Francisco", State: "CA", Country: "USA", Capital: false, Population: 860000}},
     {id: "LA", c: City{Name: "Los Angeles", State: "CA", Country: "USA", Capital: false, Population: 3900000}},
     {id: "DC", c: City{Name: "Washington D.C.", Country: "USA", Capital: true, Population: 680000}},
     {id: "TOK", c: City{Name: "Tokyo", Country: "Japan", Capital: true, Population: 9000000}},
     {id: "BJ", c: City{Name: "Beijing", Country: "China", Capital: true, Population: 21500000}},
 }
 for _, c := range cities {
     _, err := client.Collection("cities").Doc(c.id).Set(ctx, c.c)
     if err != nil {
         return err
     }
 }
 return nil
}
```

### Java

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
CollectionReference cities = db.collection("cities");
List<ApiFuture<WriteResult>> futures = new ArrayList<>();
futures.add(
    cities
        .document("SF")
        .set(
            new City(
                "San Francisco",
                "CA",
                "USA",
                false,
                860000L,
                Arrays.asList("west_coast", "norcal"))));
futures.add(
    cities
        .document("LA")
        .set(
            new City(
                "Los Angeles",
                "CA",
                "USA",
                false,
                3900000L,
                Arrays.asList("west_coast", "socal"))));
futures.add(
    cities
        .document("DC")
        .set(
            new City(
                "Washington D.C.", null, "USA", true, 680000L, Arrays.asList("east_coast"))));
futures.add(
    cities
        .document("TOK")
        .set(
            new City(
                "Tokyo", null, "Japan", true, 9000000L, Arrays.asList("kanto", "honshu"))));
futures.add(
    cities
        .document("BJ")
        .set(
            new City(
                "Beijing",
                null,
                "China",
                true,
                21500000L,
                Arrays.asList("jingjinji", "hebei"))));
// (optional) block on operation
ApiFutures.allAsList(futures).get();
```

### Node.js

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` javascript
const citiesRef = db.collection('cities');

await citiesRef.doc('SF').set({
  name: 'San Francisco', state: 'CA', country: 'USA',
  capital: false, population: 860000
});
await citiesRef.doc('LA').set({
  name: 'Los Angeles', state: 'CA', country: 'USA',
  capital: false, population: 3900000
});
await citiesRef.doc('DC').set({
  name: 'Washington, D.C.', state: null, country: 'USA',
  capital: true, population: 680000
});
await citiesRef.doc('TOK').set({
  name: 'Tokyo', state: null, country: 'Japan',
  capital: true, population: 9000000
});
await citiesRef.doc('BJ').set({
  name: 'Beijing', state: null, country: 'China',
  capital: true, population: 21500000
});
```

### PHP

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
$citiesRef = $db->collection('samples/php/cities');
$citiesRef->document('SF')->set([
    'name' => 'San Francisco',
    'state' => 'CA',
    'country' => 'USA',
    'capital' => false,
    'population' => 860000,
    'density' => 18000,
]);
$citiesRef->document('LA')->set([
    'name' => 'Los Angeles',
    'state' => 'CA',
    'country' => 'USA',
    'capital' => false,
    'population' => 3900000,
    'density' => 8000,
]);
$citiesRef->document('DC')->set([
    'name' => 'Washington D.C.',
    'state' => null,
    'country' => 'USA',
    'capital' => true,
    'population' => 680000,
    'density' => 11000,
]);
$citiesRef->document('TOK')->set([
    'name' => 'Tokyo',
    'state' => null,
    'country' => 'Japan',
    'capital' => true,
    'population' => 9000000,
    'density' => 16000,

]);
$citiesRef->document('BJ')->set([
    'name' => 'Beijing',
    'state' => null,
    'country' => 'China',
    'capital' => true,
    'population' => 21500000,
    'density' => 3500,
]);
printf('Added example cities data to the cities collection.' . PHP_EOL);
```

### Python

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
cities_ref = db.collection("cities")
cities_ref.document("BJ").set(
    City("Beijing", None, "China", True, 21500000, ["hebei"]).to_dict()
)
cities_ref.document("SF").set(
    City(
        "San Francisco", "CA", "USA", False, 860000, ["west_coast", "norcal"]
    ).to_dict()
)
cities_ref.document("LA").set(
    City(
        "Los Angeles", "CA", "USA", False, 3900000, ["west_coast", "socal"]
    ).to_dict()
)
cities_ref.document("DC").set(
    City("Washington D.C.", None, "USA", True, 680000, ["east_coast"]).to_dict()
)
cities_ref.document("TOK").set(
    City("Tokyo", None, "Japan", True, 9000000, ["kanto", "honshu"]).to_dict()
)
```

### Ruby

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
cities_ref = firestore.col collection_path
cities_ref.doc("SF").set(
  {
    name:       "San Francisco",
    state:      "CA",
    country:    "USA",
    capital:    false,
    population: 860_000
  }
)
cities_ref.doc("LA").set(
  {
    name:       "Los Angeles",
    state:      "CA",
    country:    "USA",
    capital:    false,
    population: 3_900_000
  }
)
cities_ref.doc("DC").set(
  {
    name:       "Washington D.C.",
    state:      nil,
    country:    "USA",
    capital:    true,
    population: 680_000
  }
)
cities_ref.doc("TOK").set(
  {
    name:       "Tokyo",
    state:      nil,
    country:    "Japan",
    capital:    true,
    population: 9_000_000
  }
)
cities_ref.doc("BJ").set(
  {
    name:       "Beijing",
    state:      nil,
    country:    "China",
    capital:    true,
    population: 21_500_000
  }
)
```

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](/docs/samples?product=firestore) .
