# Query and filter data

Firestore provides powerful query functionality for specifying which documents you want to retrieve from a collection or collection group. These queries can also be used with either `  get()  ` or `  addSnapshotListener()  ` , as described in [Get Data](/firestore/native/docs/query-data/get-data) and [Get Realtime Updates](/firestore/native/docs/query-data/listen) .

**Note:** While the code samples cover multiple languages, the text explaining the samples refers to the Web method names.

## Example data

To get started, write some data about cities so we can look at different ways to read it back:

### Web version 9

``` javascript
import { collection, doc, setDoc } from "firebase/firestore"; 

const citiesRef = collection(db, "cities");

await setDoc(doc(citiesRef, "SF"), {
    name: "San Francisco", state: "CA", country: "USA",
    capital: false, population: 860000,
    regions: ["west_coast", "norcal"] });
await setDoc(doc(citiesRef, "LA"), {
    name: "Los Angeles", state: "CA", country: "USA",
    capital: false, population: 3900000,
    regions: ["west_coast", "socal"] });
await setDoc(doc(citiesRef, "DC"), {
    name: "Washington, D.C.", state: null, country: "USA",
    capital: true, population: 680000,
    regions: ["east_coast"] });
await setDoc(doc(citiesRef, "TOK"), {
    name: "Tokyo", state: null, country: "Japan",
    capital: true, population: 9000000,
    regions: ["kanto", "honshu"] });
await setDoc(doc(citiesRef, "BJ"), {
    name: "Beijing", state: null, country: "China",
    capital: true, population: 21500000,
    regions: ["jingjinji", "hebei"] });example_data.js
```

### Web version 8

[Learn more](//firebase.google.com/docs/web/learn-more#modular-version) about the tree-shakeable modular Web API and its advantages over the namespaced API.

``` javascript
var citiesRef = db.collection("cities");

citiesRef.doc("SF").set({
    name: "San Francisco", state: "CA", country: "USA",
    capital: false, population: 860000,
    regions: ["west_coast", "norcal"] });
citiesRef.doc("LA").set({
    name: "Los Angeles", state: "CA", country: "USA",
    capital: false, population: 3900000,
    regions: ["west_coast", "socal"] });
citiesRef.doc("DC").set({
    name: "Washington, D.C.", state: null, country: "USA",
    capital: true, population: 680000,
    regions: ["east_coast"] });
citiesRef.doc("TOK").set({
    name: "Tokyo", state: null, country: "Japan",
    capital: true, population: 9000000,
    regions: ["kanto", "honshu"] });
citiesRef.doc("BJ").set({
    name: "Beijing", state: null, country: "China",
    capital: true, population: 21500000,
    regions: ["jingjinji", "hebei"] });test.firestore.js
```

##### Swift

**Note:** This product is not available on watchOS and App Clip targets.

``` swift
let citiesRef = db.collection("cities")

citiesRef.document("SF").setData([
  "name": "San Francisco",
  "state": "CA",
  "country": "USA",
  "capital": false,
  "population": 860000,
  "regions": ["west_coast", "norcal"]
])
citiesRef.document("LA").setData([
  "name": "Los Angeles",
  "state": "CA",
  "country": "USA",
  "capital": false,
  "population": 3900000,
  "regions": ["west_coast", "socal"]
])
citiesRef.document("DC").setData([
  "name": "Washington D.C.",
  "country": "USA",
  "capital": true,
  "population": 680000,
  "regions": ["east_coast"]
])
citiesRef.document("TOK").setData([
  "name": "Tokyo",
  "country": "Japan",
  "capital": true,
  "population": 9000000,
  "regions": ["kanto", "honshu"]
])
citiesRef.document("BJ").setData([
  "name": "Beijing",
  "country": "China",
  "capital": true,
  "population": 21500000,
  "regions": ["jingjinji", "hebei"]
])ViewController.swift
```

##### Objective-C

**Note:** This product is not available on watchOS and App Clip targets.

``` objective-c
FIRCollectionReference *citiesRef = [self.db collectionWithPath:@"cities"];
[[citiesRef documentWithPath:@"SF"] setData:@{
  @"name": @"San Francisco",
  @"state": @"CA",
  @"country": @"USA",
  @"capital": @(NO),
  @"population": @860000,
  @"regions": @[@"west_coast", @"norcal"]
}];
[[citiesRef documentWithPath:@"LA"] setData:@{
  @"name": @"Los Angeles",
  @"state": @"CA",
  @"country": @"USA",
  @"capital": @(NO),
  @"population": @3900000,
  @"regions": @[@"west_coast", @"socal"]
}];
[[citiesRef documentWithPath:@"DC"] setData:@{
  @"name": @"Washington D.C.",
  @"country": @"USA",
  @"capital": @(YES),
  @"population": @680000,
  @"regions": @[@"east_coast"]
}];
[[citiesRef documentWithPath:@"TOK"] setData:@{
  @"name": @"Tokyo",
  @"country": @"Japan",
  @"capital": @(YES),
  @"population": @9000000,
  @"regions": @[@"kanto", @"honshu"]
}];
[[citiesRef documentWithPath:@"BJ"] setData:@{
  @"name": @"Beijing",
  @"country": @"China",
  @"capital": @(YES),
  @"population": @21500000,
  @"regions": @[@"jingjinji", @"hebei"]
}];ViewController.m
```

##### Kotlin  
Android

``` kotlin
val cities = db.collection("cities")

val data1 = hashMapOf(
    "name" to "San Francisco",
    "state" to "CA",
    "country" to "USA",
    "capital" to false,
    "population" to 860000,
    "regions" to listOf("west_coast", "norcal"),
)
cities.document("SF").set(data1)

val data2 = hashMapOf(
    "name" to "Los Angeles",
    "state" to "CA",
    "country" to "USA",
    "capital" to false,
    "population" to 3900000,
    "regions" to listOf("west_coast", "socal"),
)
cities.document("LA").set(data2)

val data3 = hashMapOf(
    "name" to "Washington D.C.",
    "state" to null,
    "country" to "USA",
    "capital" to true,
    "population" to 680000,
    "regions" to listOf("east_coast"),
)
cities.document("DC").set(data3)

val data4 = hashMapOf(
    "name" to "Tokyo",
    "state" to null,
    "country" to "Japan",
    "capital" to true,
    "population" to 9000000,
    "regions" to listOf("kanto", "honshu"),
)
cities.document("TOK").set(data4)

val data5 = hashMapOf(
    "name" to "Beijing",
    "state" to null,
    "country" to "China",
    "capital" to true,
    "population" to 21500000,
    "regions" to listOf("jingjinji", "hebei"),
)
cities.document("BJ").set(data5)DocSnippets.kt
```

##### Java  
Android

``` java
CollectionReference cities = db.collection("cities");

Map<String, Object> data1 = new HashMap<>();
data1.put("name", "San Francisco");
data1.put("state", "CA");
data1.put("country", "USA");
data1.put("capital", false);
data1.put("population", 860000);
data1.put("regions", Arrays.asList("west_coast", "norcal"));
cities.document("SF").set(data1);

Map<String, Object> data2 = new HashMap<>();
data2.put("name", "Los Angeles");
data2.put("state", "CA");
data2.put("country", "USA");
data2.put("capital", false);
data2.put("population", 3900000);
data2.put("regions", Arrays.asList("west_coast", "socal"));
cities.document("LA").set(data2);

Map<String, Object> data3 = new HashMap<>();
data3.put("name", "Washington D.C.");
data3.put("state", null);
data3.put("country", "USA");
data3.put("capital", true);
data3.put("population", 680000);
data3.put("regions", Arrays.asList("east_coast"));
cities.document("DC").set(data3);

Map<String, Object> data4 = new HashMap<>();
data4.put("name", "Tokyo");
data4.put("state", null);
data4.put("country", "Japan");
data4.put("capital", true);
data4.put("population", 9000000);
data4.put("regions", Arrays.asList("kanto", "honshu"));
cities.document("TOK").set(data4);

Map<String, Object> data5 = new HashMap<>();
data5.put("name", "Beijing");
data5.put("state", null);
data5.put("country", "China");
data5.put("capital", true);
data5.put("population", 21500000);
data5.put("regions", Arrays.asList("jingjinji", "hebei"));
cities.document("BJ").set(data5);DocSnippets.java
```

### Dart

``` dart
final cities = db.collection("cities");
final data1 = <String, dynamic>{
  "name": "San Francisco",
  "state": "CA",
  "country": "USA",
  "capital": false,
  "population": 860000,
  "regions": ["west_coast", "norcal"]
};
cities.doc("SF").set(data1);

final data2 = <String, dynamic>{
  "name": "Los Angeles",
  "state": "CA",
  "country": "USA",
  "capital": false,
  "population": 3900000,
  "regions": ["west_coast", "socal"],
};
cities.doc("LA").set(data2);

final data3 = <String, dynamic>{
  "name": "Washington D.C.",
  "state": null,
  "country": "USA",
  "capital": true,
  "population": 680000,
  "regions": ["east_coast"]
};
cities.doc("DC").set(data3);

final data4 = <String, dynamic>{
  "name": "Tokyo",
  "state": null,
  "country": "Japan",
  "capital": true,
  "population": 9000000,
  "regions": ["kanto", "honshu"]
};
cities.doc("TOK").set(data4);

final data5 = <String, dynamic>{
  "name": "Beijing",
  "state": null,
  "country": "China",
  "capital": true,
  "population": 21500000,
  "regions": ["jingjinji", "hebei"],
};
cities.doc("BJ").set(data5);firestore.dart
```

##### Java

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
// (optional) block on documents successfully added
ApiFutures.allAsList(futures).get();QueryDataSnippets.java
```

##### Python

``` python
class City:
    def __init__(self, name, state, country, capital=False, population=0, regions=[]):
        self.name = name
        self.state = state
        self.country = country
        self.capital = capital
        self.population = population
        self.regions = regions

    @staticmethod
    def from_dict(source):
        # ...

    def to_dict(self):
        # ...

    def __repr__(self):
        return f"City(\
                name={self.name}, \
                country={self.country}, \
                population={self.population}, \
                capital={self.capital}, \
                regions={self.regions}\
            )"
```

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
)snippets.py
```

##### Python  
(Async)

``` python
class City:
    def __init__(self, name, state, country, capital=False, population=0, regions=[]):
        self.name = name
        self.state = state
        self.country = country
        self.capital = capital
        self.population = population
        self.regions = regions

    @staticmethod
    def from_dict(source):
        # ...

    def to_dict(self):
        # ...

    def __repr__(self):
        return f"City(\
                name={self.name}, \
                country={self.country}, \
                population={self.population}, \
                capital={self.capital}, \
                regions={self.regions}\
            )"
```

``` python
cities_ref = db.collection("cities")
await cities_ref.document("BJ").set(
    City("Beijing", None, "China", True, 21500000, ["hebei"]).to_dict()
)
await cities_ref.document("SF").set(
    City(
        "San Francisco", "CA", "USA", False, 860000, ["west_coast", "norcal"]
    ).to_dict()
)
await cities_ref.document("LA").set(
    City(
        "Los Angeles", "CA", "USA", False, 3900000, ["west_coast", "socal"]
    ).to_dict()
)
await cities_ref.document("DC").set(
    City("Washington D.C.", None, "USA", True, 680000, ["east_coast"]).to_dict()
)
await cities_ref.document("TOK").set(
    City("Tokyo", None, "Japan", True, 9000000, ["kanto", "honshu"]).to_dict()
)snippets.py
```

##### C++

``` cpp
CollectionReference cities = db->Collection("cities");

cities.Document("SF").Set({
    {"name", FieldValue::String("San Francisco")},
    {"state", FieldValue::String("CA")},
    {"country", FieldValue::String("USA")},
    {"capital", FieldValue::Boolean(false)},
    {"population", FieldValue::Integer(860000)},
    {"regions", FieldValue::Array({FieldValue::String("west_coast"),
                                   FieldValue::String("norcal")})},
});

cities.Document("LA").Set({
    {"name", FieldValue::String("Los Angeles")},
    {"state", FieldValue::String("CA")},
    {"country", FieldValue::String("USA")},
    {"capital", FieldValue::Boolean(false)},
    {"population", FieldValue::Integer(3900000)},
    {"regions", FieldValue::Array({FieldValue::String("west_coast"),
                                   FieldValue::String("socal")})},
});

cities.Document("DC").Set({
    {"name", FieldValue::String("Washington D.C.")},
    {"state", FieldValue::Null()},
    {"country", FieldValue::String("USA")},
    {"capital", FieldValue::Boolean(true)},
    {"population", FieldValue::Integer(680000)},
    {"regions",
     FieldValue::Array({FieldValue::String("east_coast")})},
});

cities.Document("TOK").Set({
    {"name", FieldValue::String("Tokyo")},
    {"state", FieldValue::Null()},
    {"country", FieldValue::String("Japan")},
    {"capital", FieldValue::Boolean(true)},
    {"population", FieldValue::Integer(9000000)},
    {"regions", FieldValue::Array({FieldValue::String("kanto"),
                                   FieldValue::String("honshu")})},
});

cities.Document("BJ").Set({
    {"name", FieldValue::String("Beijing")},
    {"state", FieldValue::Null()},
    {"country", FieldValue::String("China")},
    {"capital", FieldValue::Boolean(true)},
    {"population", FieldValue::Integer(21500000)},
    {"regions", FieldValue::Array({FieldValue::String("jingjinji"),
                                   FieldValue::String("hebei")})},
});snippets.cpp
```

##### Node.js

``` javascript
const citiesRef = db.collection('cities');

await citiesRef.doc('SF').set({
  name: 'San Francisco', state: 'CA', country: 'USA',
  capital: false, population: 860000,
  regions: ['west_coast', 'norcal']
});
await citiesRef.doc('LA').set({
  name: 'Los Angeles', state: 'CA', country: 'USA',
  capital: false, population: 3900000,
  regions: ['west_coast', 'socal']
});
await citiesRef.doc('DC').set({
  name: 'Washington, D.C.', state: null, country: 'USA',
  capital: true, population: 680000,
  regions: ['east_coast']
});
await citiesRef.doc('TOK').set({
  name: 'Tokyo', state: null, country: 'Japan',
  capital: true, population: 9000000,
  regions: ['kanto', 'honshu']
});
await citiesRef.doc('BJ').set({
  name: 'Beijing', state: null, country: 'China',
  capital: true, population: 21500000,
  regions: ['jingjinji', 'hebei']
});index.js
```

##### Go

``` go
cities := []struct {
 id string
 c  City
}{
 {
     id: "SF",
     c: City{Name: "San Francisco", State: "CA", Country: "USA",
         Capital: false, Population: 860000,
         Regions: []string{"west_coast", "norcal"}},
 },
 {
     id: "LA",
     c: City{Name: "Los Angeles", State: "CA", Country: "USA",
         Capital: false, Population: 3900000,
         Regions: []string{"west_coast", "socal"}},
 },
 {
     id: "DC",
     c: City{Name: "Washington D.C.", Country: "USA",
         Capital: true, Population: 680000,
         Regions: []string{"east_coast"}},
 },
 {
     id: "TOK",
     c: City{Name: "Tokyo", Country: "Japan",
         Capital: true, Population: 9000000,
         Regions: []string{"kanto", "honshu"}},
 },
 {
     id: "BJ",
     c: City{Name: "Beijing", Country: "China",
         Capital: true, Population: 21500000,
         Regions: []string{"jingjinji", "hebei"}},
 },
}
for _, c := range cities {
 if _, err := client.Collection("cities").Doc(c.id).Set(ctx, c.c); err != nil {
     return err
 }
}query.go
```

##### PHP

``` php
$citiesRef = $db->collection('samples/php/cities');
$citiesRef->document('SF')->set([
    'name' => 'San Francisco',
    'state' => 'CA',
    'country' => 'USA',
    'capital' => false,
    'population' => 860000,
    'density' => 18000,
    'regions' => ['west_coast', 'norcal']
]);
$citiesRef->document('LA')->set([
    'name' => 'Los Angeles',
    'state' => 'CA',
    'country' => 'USA',
    'capital' => false,
    'population' => 3900000,
    'density' => 8000,
    'regions' => ['west_coast', 'socal']
]);
$citiesRef->document('DC')->set([
    'name' => 'Washington D.C.',
    'state' => null,
    'country' => 'USA',
    'capital' => true,
    'population' => 680000,
    'density' => 11000,
    'regions' => ['east_coast']
]);
$citiesRef->document('TOK')->set([
    'name' => 'Tokyo',
    'state' => null,
    'country' => 'Japan',
    'capital' => true,
    'population' => 9000000,
    'density' => 16000,
    'regions' => ['kanto', 'honshu']
]);
$citiesRef->document('BJ')->set([
    'name' => 'Beijing',
    'state' => null,
    'country' => 'China',
    'capital' => true,
    'population' => 21500000,
    'density' => 3500,
    'regions' => ['jingjinji', 'hebei']
]);
printf('Added example cities data to the cities collection.' . PHP_EOL);query_filter_dataset.php
```

##### Unity

``` text
CollectionReference citiesRef = db.Collection("cities");
citiesRef.Document("SF").SetAsync(new Dictionary<string, object>(){
    { "Name", "San Francisco" },
    { "State", "CA" },
    { "Country", "USA" },
    { "Capital", false },
    { "Population", 860000 },
    { "Regions", new ArrayList{"west_coast", "norcal"} }
});
citiesRef.Document("LA").SetAsync(new Dictionary<string, object>(){
    { "Name", "Los Angeles" },
    { "State", "CA" },
    { "Country", "USA" },
    { "Capital", false },
    { "Population", 3900000 },
    { "Regions", new ArrayList{"west_coast", "socal"} }
});
citiesRef.Document("DC").SetAsync(new Dictionary<string, object>(){
    { "Name", "Washington D.C." },
    { "State", null },
    { "Country", "USA" },
    { "Capital", true },
    { "Population", 680000 },
    { "Regions", new ArrayList{"east_coast"} }
});
citiesRef.Document("TOK").SetAsync(new Dictionary<string, object>(){
    { "Name", "Tokyo" },
    { "State", null },
    { "Country", "Japan" },
    { "Capital", true },
    { "Population", 9000000 },
    { "Regions", new ArrayList{"kanto", "honshu"} }
});
citiesRef.Document("BJ").SetAsync(new Dictionary<string, object>(){
    { "Name", "Beijing" },
    { "State", null },
    { "Country", "China" },
    { "Capital", true },
    { "Population", 21500000 },
    { "Regions", new ArrayList{"jingjinji", "hebei"} }
});
```

##### C\#

``` csharp
CollectionReference citiesRef = db.Collection("cities");
await citiesRef.Document("SF").SetAsync(new Dictionary<string, object>
{
    { "Name", "San Francisco" },
    { "State", "CA" },
    { "Country", "USA" },
    { "Capital", false },
    { "Population", 860000 },
    { "Density", 18000 },
    { "Regions", new[] {"west_coast", "norcal"} }
});
await citiesRef.Document("LA").SetAsync(new Dictionary<string, object>
{
    { "Name", "Los Angeles" },
    { "State", "CA" },
    { "Country", "USA" },
    { "Capital", false },
    { "Population", 3900000 },
    { "Density", 8300 },
    { "Regions", new[] {"west_coast", "socal"} }
});
await citiesRef.Document("DC").SetAsync(new Dictionary<string, object>
{
    { "Name", "Washington D.C." },
    { "State", null },
    { "Country", "USA" },
    { "Capital", true },
    { "Population", 680000 },
    { "Density", 11300 },
    { "Regions", new[] {"east_coast"} }
});
await citiesRef.Document("TOK").SetAsync(new Dictionary<string, object>
{
    { "Name", "Tokyo" },
    { "State", null },
    { "Country", "Japan" },
    { "Capital", true },
    { "Population", 9000000 },
    { "Density", 16000 },
    { "Regions", new[] {"kanto", "honshu"} }
});
await citiesRef.Document("BJ").SetAsync(new Dictionary<string, object>
{
    { "Name", "Beijing" },
    { "State", null },
    { "Country", "China" },
    { "Capital", true },
    { "Population", 21500000 },
    { "Density", 3500 },
    { "Regions", new[] {"jingjinji", "hebei"} }
});
Console.WriteLine("Added example cities data to the cities collection.");Program.cs
```

##### Ruby

``` ruby
cities_ref = firestore.col collection_path
cities_ref.doc("SF").set(
  {
    name:       "San Francisco",
    state:      "CA",
    country:    "USA",
    capital:    false,
    density:    18_000,
    population: 860_000,
    regions:    ["west_coast", "norcal"]
  }
)
cities_ref.doc("LA").set(
  {
    name:       "Los Angeles",
    state:      "CA",
    country:    "USA",
    capital:    false,
    density:    8_300,
    population: 3_900_000,
    regions:    ["west_coast", "socal"]
  }
)
cities_ref.doc("DC").set(
  {
    name:       "Washington D.C.",
    state:      nil,
    country:    "USA",
    capital:    true,
    density:    11_300,
    population: 680_000,
    regions:    ["east_coast"]
  }
)
cities_ref.doc("TOK").set(
  {
    name:       "Tokyo",
    state:      nil,
    country:    "Japan",
    capital:    true,
    density:    16_000,
    population: 9_000_000,
    regions:    ["kanto", "honshu"]
  }
)
cities_ref.doc("BJ").set(
  {
    name:       "Beijing",
    state:      nil,
    country:    "China",
    capital:    true,
    density:    3_500,
    population: 21_500_000,
    regions:    ["jingjinji", "hebei"]
  }
)query_data.rb
```

## Simple queries

The following query returns all cities with state `  CA  ` :

### Web version 9

``` javascript
// Create a reference to the cities collection
import { collection, query, where } from "firebase/firestore";
const citiesRef = collection(db, "cities");

// Create a query against the collection.
const q = query(citiesRef, where("state", "==", "CA"));simple_queries.js
```

### Web version 8

[Learn more](//firebase.google.com/docs/web/learn-more#modular-version) about the tree-shakeable modular Web API and its advantages over the namespaced API.

``` javascript
// Create a reference to the cities collection
var citiesRef = db.collection("cities");

// Create a query against the collection.
var query = citiesRef.where("state", "==", "CA");test.firestore.js
```

##### Swift

**Note:** This product is not available on watchOS and App Clip targets.

``` swift
// Create a reference to the cities collection
let citiesRef = db.collection("cities")

// Create a query against the collection.
let query = citiesRef.whereField("state", isEqualTo: "CA")ViewController.swift
```

##### Objective-C

**Note:** This product is not available on watchOS and App Clip targets.

``` objective-c
// Create a reference to the cities collection
FIRCollectionReference *citiesRef = [self.db collectionWithPath:@"cities"];
// Create a query against the collection.
FIRQuery *query = [citiesRef queryWhereField:@"state" isEqualTo:@"CA"];ViewController.m
```

##### Kotlin  
Android

``` kotlin
// Create a reference to the cities collection
val citiesRef = db.collection("cities")

// Create a query against the collection.
val query = citiesRef.whereEqualTo("state", "CA")DocSnippets.kt
```

##### Java  
Android

``` java
// Create a reference to the cities collection
CollectionReference citiesRef = db.collection("cities");

// Create a query against the collection.
Query query = citiesRef.whereEqualTo("state", "CA");DocSnippets.java
```

### Dart

``` dart
// Create a reference to the cities collection
final citiesRef = db.collection("cities");

// Create a query against the collection.
final query = citiesRef.where("state", isEqualTo: "CA");firestore.dart
```

##### Java

``` java
// Create a reference to the cities collection
CollectionReference cities = db.collection("cities");
// Create a query against the collection.
Query query = cities.whereEqualTo("state", "CA");
// retrieve  query results asynchronously using query.get()
ApiFuture<QuerySnapshot> querySnapshot = query.get();

for (DocumentSnapshot document : querySnapshot.get().getDocuments()) {
  System.out.println(document.getId());
}QueryDataSnippets.java
```

##### Python

``` python
# Create a reference to the cities collection
cities_ref = db.collection("cities")

# Create a query against the collection
query_ref = cities_ref.where(filter=FieldFilter("state", "==", "CA"))snippets.py
```

##### Python  
(Async)

``` python
# Create a reference to the cities collection
cities_ref = db.collection("cities")

# Create a query against the collection
query_ref = cities_ref.where(filter=FieldFilter("state", "==", "CA"))snippets.py
```

##### C++

``` cpp
CollectionReference cities_ref = db->Collection("cities");
// Create a query against the collection.
Query query_ca =
    cities_ref.WhereEqualTo("state", FieldValue::String("CA"));snippets.cpp
```

##### Node.js

``` javascript
// Create a reference to the cities collection
const citiesRef = db.collection('cities');

// Create a query against the collection
const queryRef = citiesRef.where('state', '==', 'CA');index.js
```

##### Go

``` go
query := client.Collection("cities").Where("state", "==", "CA")query.go
```

##### PHP

``` php
$citiesRef = $db->collection('samples/php/cities');
$query = $citiesRef->where('state', '=', 'CA');
$snapshot = $query->documents();
foreach ($snapshot as $document) {
    printf('Document %s returned by query state=CA' . PHP_EOL, $document->id());
}query_filter_eq_string.php
```

##### Unity

``` text
CollectionReference citiesRef = db.Collection("cities");
Query query = citiesRef.WhereEqualTo("State", "CA");
query.GetSnapshotAsync().ContinueWithOnMainThread((querySnapshotTask) =>
{
    foreach (DocumentSnapshot documentSnapshot in querySnapshotTask.Result.Documents)
    {
        Debug.Log(String.Format("Document {0} returned by query State=CA", documentSnapshot.Id));
    } 
});
```

##### C\#

``` csharp
CollectionReference citiesRef = db.Collection("cities");
Query query = citiesRef.WhereEqualTo("State", "CA");
QuerySnapshot querySnapshot = await query.GetSnapshotAsync();
foreach (DocumentSnapshot documentSnapshot in querySnapshot.Documents)
{
    Console.WriteLine("Document {0} returned by query State=CA", documentSnapshot.Id);
}Program.cs
```

##### Ruby

``` ruby
cities_ref = firestore.col collection_path

query = cities_ref.where "state", "=", "CA"

query.get do |city|
  puts "Document #{city.document_id} returned by query state=CA."
endquery_data.rb
```

The following query returns all the capital cities:

### Web version 9

``` javascript
import { collection, query, where } from "firebase/firestore";
const citiesRef = collection(db, "cities");

const q = query(citiesRef, where("capital", "==", true));simple_queries_again.js
```

### Web version 8

[Learn more](//firebase.google.com/docs/web/learn-more#modular-version) about the tree-shakeable modular Web API and its advantages over the namespaced API.

``` javascript
var citiesRef = db.collection("cities");

var query = citiesRef.where("capital", "==", true);test.firestore.js
```

##### Swift

**Note:** This product is not available on watchOS and App Clip targets.

``` swift
let capitalCities = db.collection("cities").whereField("capital", isEqualTo: true)ViewController.swift
```

##### Objective-C

**Note:** This product is not available on watchOS and App Clip targets.

``` objective-c
FIRQuery *capitalCities =
    [[self.db collectionWithPath:@"cities"] queryWhereField:@"capital" isEqualTo:@YES];ViewController.m
```

##### Kotlin  
Android

``` kotlin
val capitalCities = db.collection("cities").whereEqualTo("capital", true)DocSnippets.kt
```

##### Java  
Android

``` java
Query capitalCities = db.collection("cities").whereEqualTo("capital", true);DocSnippets.java
```

### Dart

``` dart
final capitalcities =
    db.collection("cities").where("capital", isEqualTo: true);firestore.dart
```

##### Java

``` java
// Create a reference to the cities collection
CollectionReference cities = db.collection("cities");
// Create a query against the collection.
Query query = cities.whereEqualTo("capital", true);
// retrieve  query results asynchronously using query.get()
ApiFuture<QuerySnapshot> querySnapshot = query.get();

for (DocumentSnapshot document : querySnapshot.get().getDocuments()) {
  System.out.println(document.getId());
}QueryDataSnippets.java
```

##### Python

``` python
cities_ref = db.collection("cities")

query = cities_ref.where(filter=FieldFilter("capital", "==", True))snippets.py
```

##### Python  
(Async)

``` python
cities_ref = db.collection("cities")

query = cities_ref.where(filter=FieldFilter("capital", "==", True))snippets.py
```

##### C++

``` cpp
Query capital_cities = db->Collection("cities").WhereEqualTo(
    "capital", FieldValue::Boolean(true));snippets.cpp
```

##### Node.js

``` javascript
// Create a reference to the cities collection
const citiesRef = db.collection('cities');

// Create a query against the collection
const allCapitalsRes = citiesRef.where('capital', '==', true);index.js
```

##### Go

``` go
query := client.Collection("cities").Where("capital", "==", true)query.go
```

##### PHP

``` php
$citiesRef = $db->collection('samples/php/cities');
$query = $citiesRef->where('capital', '=', true);
$snapshot = $query->documents();
foreach ($snapshot as $document) {
    printf('Document %s returned by query capital=true' . PHP_EOL, $document->id());
}query_filter_eq_boolean.php
```

##### Unity

``` text
CollectionReference citiesRef = db.Collection("cities");
Query query = citiesRef.WhereEqualTo("Capital", true);
query.GetSnapshotAsync().ContinueWithOnMainThread((querySnapshotTask) =>
{
    foreach (DocumentSnapshot documentSnapshot in querySnapshotTask.Result.Documents)
    {
        Debug.Log(String.Format("Document {0} returned by query Capital=true", documentSnapshot.Id));
    } 
});
```

##### C\#

``` csharp
CollectionReference citiesRef = db.Collection("cities");
Query query = citiesRef.WhereEqualTo("Capital", true);
QuerySnapshot querySnapshot = await query.GetSnapshotAsync();
foreach (DocumentSnapshot documentSnapshot in querySnapshot.Documents)
{
    Console.WriteLine("Document {0} returned by query Capital=true", documentSnapshot.Id);
}Program.cs
```

##### Ruby

``` ruby
cities_ref = firestore.col collection_path

query = cities_ref.where "capital", "=", true

query.get do |city|
  puts "Document #{city.document_id} returned by query capital=true."
endquery_data.rb
```

### Execute a query

After creating a query object, use the `  get()  ` function to retrieve the results:

### Web version 9

``` javascript
import { collection, query, where, getDocs } from "firebase/firestore";

const q = query(collection(db, "cities"), where("capital", "==", true));

const querySnapshot = await getDocs(q);
querySnapshot.forEach((doc) => {
  // doc.data() is never undefined for query doc snapshots
  console.log(doc.id, " => ", doc.data());
});get_multiple.js
```

### Web version 8

[Learn more](//firebase.google.com/docs/web/learn-more#modular-version) about the tree-shakeable modular Web API and its advantages over the namespaced API.

``` javascript
db.collection("cities").where("capital", "==", true)
    .get()
    .then((querySnapshot) => {
        querySnapshot.forEach((doc) => {
            // doc.data() is never undefined for query doc snapshots
            console.log(doc.id, " => ", doc.data());
        });
    })
    .catch((error) => {
        console.log("Error getting documents: ", error);
    });test.firestore.js
```

##### Swift

**Note:** This product is not available on watchOS and App Clip targets.

``` swift
do {
  let querySnapshot = try await db.collection("cities").whereField("capital", isEqualTo: true)
    .getDocuments()
  for document in querySnapshot.documents {
    print("\(document.documentID) => \(document.data())")
  }
} catch {
  print("Error getting documents: \(error)")
}ViewController.swift
```

##### Objective-C

**Note:** This product is not available on watchOS and App Clip targets.

``` objective-c
[[[self.db collectionWithPath:@"cities"] queryWhereField:@"capital" isEqualTo:@(YES)]
    getDocumentsWithCompletion:^(FIRQuerySnapshot *snapshot, NSError *error) {
      if (error != nil) {
        NSLog(@"Error getting documents: %@", error);
      } else {
        for (FIRDocumentSnapshot *document in snapshot.documents) {
          NSLog(@"%@ => %@", document.documentID, document.data);
        }
      }
    }];ViewController.m
```

##### Kotlin  
Android

``` kotlin
db.collection("cities")
    .whereEqualTo("capital", true)
    .get()
    .addOnSuccessListener { documents ->
        for (document in documents) {
            Log.d(TAG, "${document.id} => ${document.data}")
        }
    }
    .addOnFailureListener { exception ->
        Log.w(TAG, "Error getting documents: ", exception)
    }DocSnippets.kt
```

##### Java  
Android

``` java
db.collection("cities")
        .whereEqualTo("capital", true)
        .get()
        .addOnCompleteListener(new OnCompleteListener<QuerySnapshot>() {
            @Override
            public void onComplete(@NonNull Task<QuerySnapshot> task) {
                if (task.isSuccessful()) {
                    for (QueryDocumentSnapshot document : task.getResult()) {
                        Log.d(TAG, document.getId() + " => " + document.getData());
                    }
                } else {
                    Log.d(TAG, "Error getting documents: ", task.getException());
                }
            }
        });DocSnippets.java
```

### Dart

``` dart
db.collection("cities").where("capital", isEqualTo: true).get().then(
  (querySnapshot) {
    print("Successfully completed");
    for (var docSnapshot in querySnapshot.docs) {
      print('${docSnapshot.id} => ${docSnapshot.data()}');
    }
  },
  onError: (e) => print("Error completing: $e"),
);firestore.dart
```

##### Java

``` java
// asynchronously retrieve multiple documents
ApiFuture<QuerySnapshot> future = db.collection("cities").whereEqualTo("capital", true).get();
// future.get() blocks on response
List<QueryDocumentSnapshot> documents = future.get().getDocuments();
for (DocumentSnapshot document : documents) {
  System.out.println(document.getId() + " => " + document.toObject(City.class));
}RetrieveDataSnippets.java
```

##### Python

``` python
# Note: Use of CollectionRef stream() is prefered to get()
docs = (
    db.collection("cities")
    .where(filter=FieldFilter("capital", "==", True))
    .stream()
)

for doc in docs:
    print(f"{doc.id} => {doc.to_dict()}")snippets.py
```

##### Python  
(Async)

``` python
# Note: Use of CollectionRef stream() is prefered to get()
docs = (
    db.collection("cities")
    .where(filter=FieldFilter("capital", "==", True))
    .stream()
)

async for doc in docs:
    print(f"{doc.id} => {doc.to_dict()}")snippets.py
```

##### C++

``` cpp
db->Collection("cities")
    .WhereEqualTo("capital", FieldValue::Boolean(true))
    .Get()
    .OnCompletion([](const Future<QuerySnapshot>& future) {
      if (future.error() == Error::kErrorOk) {
        for (const DocumentSnapshot& document :
             future.result()->documents()) {
          std::cout << document << std::endl;
        }
      } else {
        std::cout << "Error getting documents: " << future.error_message()
                  << std::endl;
      }
    });snippets.cpp
```

##### Node.js

``` javascript
const citiesRef = db.collection('cities');
const snapshot = await citiesRef.where('capital', '==', true).get();
if (snapshot.empty) {
  console.log('No matching documents.');
  return;
}  

snapshot.forEach(doc => {
  console.log(doc.id, '=>', doc.data());
});index.js
```

##### Go

``` go
import (
 "context"
 "fmt"

 "cloud.google.com/go/firestore"
 "google.golang.org/api/iterator"
)

func multipleDocs(ctx context.Context, client *firestore.Client) error {
 fmt.Println("All capital cities:")
 iter := client.Collection("cities").Where("capital", "==", true).Documents(ctx)
 for {
     doc, err := iter.Next()
     if err == iterator.Done {
         break
     }
     if err != nil {
         return err
     }
     fmt.Println(doc.Data())
 }
 return nil
}
retrieve_data_query.go
```

##### PHP

### PHP

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
$citiesRef = $db->collection('samples/php/cities');
$query = $citiesRef->where('capital', '=', true);
$documents = $query->documents();
foreach ($documents as $document) {
    if ($document->exists()) {
        printf('Document data for document %s:' . PHP_EOL, $document->id());
        print_r($document->data());
        printf(PHP_EOL);
    } else {
        printf('Document %s does not exist!' . PHP_EOL, $document->id());
    }
}
```

##### Unity

``` text
Query capitalQuery = db.Collection("cities").WhereEqualTo("Capital", true);
capitalQuery.GetSnapshotAsync().ContinueWithOnMainThread(task => {
  QuerySnapshot capitalQuerySnapshot = task.Result;
  foreach (DocumentSnapshot documentSnapshot in capitalQuerySnapshot.Documents) {
    Debug.Log(String.Format("Document data for {0} document:", documentSnapshot.Id));
    Dictionary<string, object> city = documentSnapshot.ToDictionary();
    foreach (KeyValuePair<string, object> pair in city) {
      Debug.Log(String.Format("{0}: {1}", pair.Key, pair.Value));
    }

    // Newline to separate entries
    Debug.Log("");
  };
});
```

##### C\#

``` csharp
Query capitalQuery = db.Collection("cities").WhereEqualTo("Capital", true);
QuerySnapshot capitalQuerySnapshot = await capitalQuery.GetSnapshotAsync();
foreach (DocumentSnapshot documentSnapshot in capitalQuerySnapshot.Documents)
{
    Console.WriteLine("Document data for {0} document:", documentSnapshot.Id);
    Dictionary<string, object> city = documentSnapshot.ToDictionary();
    foreach (KeyValuePair<string, object> pair in city)
    {
        Console.WriteLine("{0}: {1}", pair.Key, pair.Value);
    }
    Console.WriteLine("");
}Program.cs
```

##### Ruby

``` ruby
cities_ref = firestore.col collection_path

query = cities_ref.where "capital", "=", true

query.get do |city|
  puts "#{city.document_id} data: #{city.data}."
endget_data.rb
```

See [Get Data](/firestore/native/docs/query-data/get-data) for more information on retrieving query results. You can also [add a listener](/firestore/native/docs/query-data/listen) to a query to get the current results and listen for future updates.

## Query operators

The `  where()  ` method takes three parameters: a field to filter on, a comparison operator, and a value. Core operations support the following comparison operators:

  - `  <  ` less than
  - `  <=  ` less than or equal to
  - `  ==  ` equal to
  - `  >  ` greater than
  - `  >=  ` greater than or equal to
  - [`  !=  ` not equal to](#not_equal)
  - [`  array-contains  `](#array_membership)
  - [`  array-contains-any  `](#in_and_array-contains-any)
  - [`  in  `](#in_and_array-contains-any)
  - [`  not-in  `](#in_and_array-contains-any)

**Note:** For Apple, Android, and Java, the comparison operator is explicitly named in the method.

For example:

### Web version 9

``` javascript
const stateQuery = query(citiesRef, where("state", "==", "CA"));
const populationQuery = query(citiesRef, where("population", "<", 100000));
const nameQuery = query(citiesRef, where("name", ">=", "San Francisco"));example_filters.js
```

### Web version 8

[Learn more](//firebase.google.com/docs/web/learn-more#modular-version) about the tree-shakeable modular Web API and its advantages over the namespaced API.

``` javascript
const stateQuery = citiesRef.where("state", "==", "CA");
const populationQuery = citiesRef.where("population", "<", 100000);
const nameQuery = citiesRef.where("name", ">=", "San Francisco");test.firestore.js
```

##### Swift

**Note:** This product is not available on watchOS and App Clip targets.

``` swift
let stateQuery = citiesRef.whereField("state", isEqualTo: "CA")
let populationQuery = citiesRef.whereField("population", isLessThan: 100000)
let nameQuery = citiesRef.whereField("name", isGreaterThanOrEqualTo: "San Francisco")ViewController.swift
```

##### Objective-C

**Note:** This product is not available on watchOS and App Clip targets.

``` objective-c
FIRQuery *stateQuery = [citiesRef queryWhereField:@"state" isEqualTo:@"CA"];
FIRQuery *populationQuery = [citiesRef queryWhereField:@"population" isLessThan:@100000];
FIRQuery *nameQuery = [citiesRef queryWhereField:@"name" isGreaterThanOrEqualTo:@"San Francisco"];ViewController.m
```

##### Kotlin  
Android

``` kotlin
val stateQuery = citiesRef.whereEqualTo("state", "CA")
val populationQuery = citiesRef.whereLessThan("population", 100000)
val nameQuery = citiesRef.whereGreaterThanOrEqualTo("name", "San Francisco")DocSnippets.kt
```

##### Java  
Android

``` java
Query stateQuery = citiesRef.whereEqualTo("state", "CA");
Query populationQuery = citiesRef.whereLessThan("population", 100000);
Query nameQuery = citiesRef.whereGreaterThanOrEqualTo("name", "San Francisco");DocSnippets.java
```

### Dart

``` dart
final citiesRef = db.collection("cities");
final stateQuery = citiesRef.where("state", isEqualTo: "CA");
final populationQuery = citiesRef.where("population", isLessThan: 100000);
final nameQuery = citiesRef.where("name", isEqualTo: "San Francisco");firestore.dart
```

##### Java

``` java
Query stateQuery = cities.whereEqualTo("state", "CA");
Query populationQuery = cities.whereLessThan("population", 1000000L);
Query nameQuery = cities.whereGreaterThanOrEqualTo("name", "San Francisco");QueryDataSnippets.java
```

##### Python

``` python
cities_ref = db.collection("cities")

cities_ref.where(filter=FieldFilter("state", "==", "CA"))
cities_ref.where(filter=FieldFilter("population", "<", 1000000))
cities_ref.where(filter=FieldFilter("name", ">=", "San Francisco"))snippets.py
```

##### Python  
(Async)

``` python
cities_ref = db.collection("cities")

cities_ref.where(filter=FieldFilter("state", "==", "CA"))
cities_ref.where(filter=FieldFilter("population", "<", 1000000))
cities_ref.where(filter=FieldFilter("name", ">=", "San Francisco"))snippets.py
```

##### C++

``` cpp
cities_ref.WhereEqualTo("state", FieldValue::String("CA"));
cities_ref.WhereLessThan("population", FieldValue::Integer(100000));
cities_ref.WhereGreaterThanOrEqualTo("name",
                                     FieldValue::String("San Francisco"));snippets.cpp
```

##### Node.js

``` javascript
const stateQueryRes = await citiesRef.where('state', '==', 'CA').get();
const populationQueryRes = await citiesRef.where('population', '<', 1000000).get();
const nameQueryRes = await citiesRef.where('name', '>=', 'San Francisco').get();index.js
```

##### Go

``` go
countryQuery := cities.Where("state", "==", "CA")
popQuery := cities.Where("population", "<", 1000000)
cityQuery := cities.Where("name", ">=", "San Francisco")query.go
```

##### PHP

``` php
$stateQuery = $citiesRef->where('state', '=', 'CA');
$populationQuery = $citiesRef->where('population', '>', 1000000);
$nameQuery = $citiesRef->where('name', '>=', 'San Francisco');query_filter_single_examples.php
```

##### Unity

``` text
Query stateQuery = citiesRef.WhereEqualTo("State", "CA");
Query populationQuery = citiesRef.WhereGreaterThan("Population", 1000000);
Query nameQuery = citiesRef.WhereGreaterThanOrEqualTo("Name", "San Francisco");
```

##### C\#

``` csharp
CollectionReference citiesRef = db.Collection("cities");
Query stateQuery = citiesRef.WhereEqualTo("State", "CA");
Query populationQuery = citiesRef.WhereGreaterThan("Population", 1000000);
Query nameQuery = citiesRef.WhereGreaterThanOrEqualTo("Name", "San Francisco");Program.cs
```

##### Ruby

``` ruby
state_query      = cities_ref.where "state", "=", "CA"
population_query = cities_ref.where "population", ">", 1_000_000
name_query       = cities_ref.where "name", ">=", "San Francisco"query_data.rb
```

### Not equal ( `     !=    ` )

Use the not equal ( `  !=  ` ) operator to return documents where the given field exists and does not match the comparison value. For example:

### Web version 9

``` javascript
const notCapitalQuery = query(citiesRef, where("capital", "!=", false));simple_query_not_equal.js
```

### Web version 8

[Learn more](//firebase.google.com/docs/web/learn-more#modular-version) about the tree-shakeable modular Web API and its advantages over the namespaced API.

``` javascript
citiesRef.where("capital", "!=", false);test.firestore.js
```

##### Swift

**Note:** This product is not available on watchOS and App Clip targets.

``` swift
let notEqualQuery = citiesRef.whereField("capital", isNotEqualTo: false)ViewController.swift
```

##### Objective-C

**Note:** This product is not available on watchOS and App Clip targets.

``` objective-c
query = [citiesRef queryWhereField:@"capital" isNotEqualTo:@NO];ViewController.m
```

##### Kotlin  
Android

``` kotlin
val notCapitalQuery = citiesRef.whereNotEqualTo("capital", false)DocSnippets.kt
```

##### Java  
Android

``` java
Query notCapitalQuery = citiesRef.whereNotEqualTo("capital", false);DocSnippets.java
```

### Dart

``` dart
final citiesRef = db.collection("cities");
final notCapitals = citiesRef.where("capital", isNotEqualTo: true);firestore.dart
```

##### Java

``` java
CollectionReference citiesRef = db.collection("cities");

Query query = citiesRef.whereNotEqualTo("capital", false);QueryDataSnippets.java
```

##### Python

``` text
// Snippet not yet available
```

##### C++

``` text
cities_ref.WhereNotEqualTo("capital", FieldValue::Boolean(false));
```

##### Node.js

``` javascript
const capitalNotFalseRes = await citiesRef.where('capital', '!=', false).get();index.js
```

##### Go

``` text
// Snippet not yet available
```

##### PHP

``` php
$stateQuery = $citiesRef->where('capital', '!=', false);query_filter_not_eq.php
```

##### Unity

``` text
Query query = citiesRef.WhereNotEqualTo("capital", false);
Query query = citiesRef.WhereNotEqualTo("capital", false);
```

##### C\#

``` text
// Snippet not yet available
```

##### Ruby

``` ruby
cities_ref = firestore.col collection_path
query = cities_ref.where "capital", "!=", falsequery_data.rb
```

This query returns every `  city  ` document where the `  capital  ` field exists with a value other than `  false  ` or `  null  ` . This includes `  city  ` documents where the `  capital  ` field value equals `  true  ` or any non-boolean value besides `  null  ` .

This query does not return `  city  ` documents where the `  capital  ` field does not exist. **Not-equal ( `  !=  ` ) and `  not-in  ` queries exclude documents where the given field does not exist** .

A field exists when it's set to any value, including an empty string ( `  ""  ` ), `  null  ` , and `  NaN  ` (not a number). Note that `  null  ` field values do not match `  !=  ` clauses, because `  x != null  ` evaluates to `  undefined  ` .

**Warning:** A `  !=  ` query clause might match many documents in a collection. To control the number of results returned, use a [limit clause](/firestore/native/docs/query-data/order-limit-data) or [paginate your query](/firestore/native/docs/query-data/query-cursors#paginate_a_query) .

#### Standard edition limitations

Note the following limitations for `  !=  ` queries. These limitations apply only to Standard edition:

  - Only documents where the given field exists can match the query.
  - You can't combine `  not-in  ` and `  !=  ` in a compound query.

### Array membership

You can use the `  array-contains  ` operator to filter based on array values. For example:

### Web version 9

``` javascript
import { query, where } from "firebase/firestore";  
const q = query(citiesRef, where("regions", "array-contains", "west_coast"));array_contains_filter.js
```

### Web version 8

[Learn more](//firebase.google.com/docs/web/learn-more#modular-version) about the tree-shakeable modular Web API and its advantages over the namespaced API.

``` javascript
citiesRef.where("regions", "array-contains", "west_coast");test.firestore.js
```

##### Swift

**Note:** This product is not available on watchOS and App Clip targets.

``` swift
citiesRef
  .whereField("regions", arrayContains: "west_coast")ViewController.swift
```

##### Objective-C

**Note:** This product is not available on watchOS and App Clip targets.

``` objective-c
[citiesRef queryWhereField:@"state" arrayContains:@"west_coast"];ViewController.m
```

##### Kotlin  
Android

``` kotlin
val citiesRef = db.collection("cities")

citiesRef.whereArrayContains("regions", "west_coast")DocSnippets.kt
```

##### Java  
Android

``` java
CollectionReference citiesRef = db.collection("cities");

citiesRef.whereArrayContains("regions", "west_coast");DocSnippets.java
```

### Dart

``` dart
final citiesRef = db.collection("cities");
final westCoastcities =
    citiesRef.where("regions", arrayContains: "west_coast");firestore.dart
```

##### Java

``` java
CollectionReference citiesRef = db.collection("cities");
Query westCoastQuery = citiesRef.whereArrayContains("regions", "west_coast");QueryDataSnippets.java
```

##### Python

``` python
cities_ref = db.collection("cities")

query = cities_ref.where(
    filter=FieldFilter("regions", "array_contains", "west_coast")
)snippets.py
```

##### Python  
(Async)

``` python
cities_ref = db.collection("cities")

query = cities_ref.where(
    filter=FieldFilter("regions", "array_contains", "west_coast")
)snippets.py
```

##### C++

``` cpp
CollectionReference cities_ref = db->Collection("cities");

cities_ref.WhereArrayContains("region", FieldValue::String("west_coast"));snippets.cpp
```

##### Node.js

``` javascript
const westCoastCities = citiesRef.where('regions', 'array-contains',
  'west_coast').get();index.js
```

##### Go

``` go
query := cities.Where("regions", "array-contains", "west_coast").Documents(ctx)query.go
```

##### PHP

``` php
$containsQuery = $citiesRef->where('regions', 'array-contains', 'west_coast');query_filter_array_contains.php
```

##### Unity

``` text
CollectionReference citiesRef = db.Collection("cities");
Query arrayContainsQuery = citiesRef.WhereArrayContains("region", "west_coast");
```

##### C\#

``` csharp
CollectionReference citiesRef = db.Collection("cities");
Query query = citiesRef.WhereArrayContains("Regions", "west_coast");Program.cs
```

##### Ruby

``` ruby
cities_ref = firestore.col collection_path
cities = cities_ref.where "regions", "array-contains", "west_coast"query_data.rb
```

This query returns every `  city  ` document where the `  regions  ` field is an array that contains `  west_coast  ` . If the array has multiple instances of the value you query on, the document is included in the results only once.

You can use at most one `  array-contains  ` clause per disjunction ( `  or  ` group). You can't combine `  array-contains  ` with `  array-contains-any  ` in the same disjunction.

### `     in    ` , `     not-in    ` , and `     array-contains-any    `

Use the `  in  ` operator to combine [up to 30](#in_not-in_array-contains-any_limits) equality ( `  ==  ` ) clauses on the same field with a logical `  OR  ` . An `  in  ` query returns documents where the given field matches any of the comparison values. For example:

### Web version 9

``` javascript
import { query, where } from "firebase/firestore";

const q = query(citiesRef, where('country', 'in', ['USA', 'Japan']));in_filter.js
```

### Web version 8

[Learn more](//firebase.google.com/docs/web/learn-more#modular-version) about the tree-shakeable modular Web API and its advantages over the namespaced API.

``` javascript
citiesRef.where('country', 'in', ['USA', 'Japan']);test.firestore.js
```

##### Swift

**Note:** This product is not available on watchOS and App Clip targets.

``` swift
let citiesRef = db.collection("cities")

citiesRef.whereField("country", in: ["USA", "Japan"])ViewController.swift
```

##### Objective-C

**Note:** This product is not available on watchOS and App Clip targets.

``` objective-c
FIRCollectionReference *citiesRef = [self.db collectionWithPath:@"cities"];

[citiesRef queryWhereField:@"country" in:@[@"USA", @"Japan"]];ViewController.m
```

##### Kotlin  
Android

``` kotlin
val citiesRef = db.collection("cities")

citiesRef.whereIn("country", listOf("USA", "Japan"))DocSnippets.kt
```

##### Java  
Android

``` java
CollectionReference citiesRef = db.collection("cities");

citiesRef.whereIn("country", Arrays.asList("USA", "Japan"));DocSnippets.java
```

### Dart

``` dart
final citiesRef = db.collection("cities");
final cities = citiesRef.where("country", whereIn: ["USA", "Japan"]);firestore.dart
```

##### Java

``` java
CollectionReference citiesRef = db.collection("cities");

Query query = citiesRef.whereIn("country", Arrays.asList("USA", "Japan"));QueryDataSnippets.java
```

##### Python

``` python
cities_ref = db.collection("cities")

query = cities_ref.where(filter=FieldFilter("country", "in", ["USA", "Japan"]))
return querysnippets.py
```

##### Python  
(Async)

``` python
cities_ref = db.collection("cities")

query = cities_ref.where(filter=FieldFilter("country", "in", ["USA", "Japan"]))
return querysnippets.py
```

##### C++

``` cpp
CollectionReference cities_ref = db->Collection("cities");

cities_ref.WhereIn("country", std::vector<FieldValue> {
  FieldValue::String("USA"),
  FieldValue::String("Japan")
});snippets.cpp
```

##### Node.js

``` javascript
const usaOrJapan = await citiesRef.where('country', 'in', ['USA', 'Japan']).get();index.js
```

##### Go

``` go
cities := client.Collection("cities")
query := cities.Where("country", "in", []string{"USA", "Japan"}).Documents(ctx)query.go
```

##### PHP

``` php
$rangeQuery = $citiesRef->where('country', 'in', ['USA', 'Japan']);query_filter_in.php
```

##### Unity

``` text
CollectionReference citiesRef = db.Collection("cities");
List countriesList = new List<object>() {"USA", "Japan"};

Query whereInQuery = citiesRef.WhereIn("country", countriesList);
```

##### C\#

``` csharp
CollectionReference citiesRef = db.Collection("cities");
Query query = citiesRef.WhereIn("Country", new[] { "USA", "Japan" });Program.cs
```

##### Ruby

``` ruby
cities_ref = firestore.col collection_path
usr_or_japan = cities_ref.where "country", "in", ["USA", "Japan"]query_data.rb
```

This query returns every `  city  ` document where the `  country  ` field is set to `  USA  ` or `  Japan  ` . From the example data, this includes the `  SF  ` , `  LA  ` , `  DC  ` , and `  TOK  ` documents.

#### `     not-in    `

Use the `  not-in  ` operator to combine up to 10 not equal ( `  !=  ` ) clauses on the same field with a logical `  AND  ` . A `  not-in  ` query returns documents where the given field exists, is not `  null  ` , and does not match any of the comparison values. For example:

### Web version 9

``` javascript
import { query, where } from "firebase/firestore";

const q = query(citiesRef, where('country', 'not-in', ['USA', 'Japan']));not_in_filter.js
```

### Web version 8

[Learn more](//firebase.google.com/docs/web/learn-more#modular-version) about the tree-shakeable modular Web API and its advantages over the namespaced API.

``` javascript
citiesRef.where('country', 'not-in', ['USA', 'Japan']);test.firestore.js
```

##### Swift

**Note:** This product is not available on watchOS and App Clip targets.

``` swift
citiesRef.whereField("country", notIn: ["USA", "Japan"])ViewController.swift
```

##### Objective-C

**Note:** This product is not available on watchOS and App Clip targets.

``` objective-c
[citiesRef queryWhereField:@"country" notIn:@[@"USA", @"Japan"]];ViewController.m
```

##### Kotlin  
Android

``` kotlin
citiesRef.whereNotIn("country", listOf("USA", "Japan"))DocSnippets.kt
```

##### Java  
Android

``` java
citiesRef.whereNotIn("country", Arrays.asList("USA", "Japan"));DocSnippets.java
```

### Dart

``` dart
final citiesRef = db.collection("cities");
final cities = citiesRef.where("country", whereNotIn: ["USA", "Japan"]);firestore.dart
```

##### Java

``` java
CollectionReference citiesRef = db.collection("cities");

Query query = citiesRef.whereNotIn("country", Arrays.asList("USA", "Japan"));QueryDataSnippets.java
```

##### Python

``` text
// Snippet not yet available
```

##### C++

``` cpp
cities_ref.WhereNotIn("country", std::vector<FieldValue> {
  FieldValue::String("USA"),
  FieldValue::String("Japan")
});snippets.cpp
```

##### Node.js

``` javascript
const notUsaOrJapan = await citiesRef.where('country', 'not-in', ['USA', 'Japan']).get();index.js
```

##### Go

``` text
// Snippet not yet available
```

##### PHP

``` php
$stateQuery = $citiesRef->where(
    'country',
    \Google\Cloud\Firestore\V1\StructuredQuery\FieldFilter\Operator::NOT_IN,
    ['USA', 'Japan']
);query_filter_not_in.php
```

##### Unity

``` text
Query query = citiesRef.WhereNotIn(new FieldPath("country"), new List<string>{"USA", "Japan"});
Query query = citiesRef.WhereNotIn("country", new List<object>(){"USA", "Japan"});
```

##### C\#

``` text
// Snippet not yet available
```

##### Ruby

``` ruby
cities_ref = firestore.col collection_path
usr_or_japan = cities_ref.where "country", "not_in", ["USA", "Japan"]query_data.rb
```

This query returns every `  city  ` document where the `  country  ` field exists and is not set to `  USA  ` , `  Japan  ` , or `  null  ` . From the example data, this includes the `  London  ` and `  Hong Kong  ` documents.

**`  not-in  ` queries exclude documents where the given field does not exist.** A field exists when it's set to any value, including an empty string ( `  ""  ` ), `  null  ` , and `  NaN  ` (not a number). Note that `  x != null  ` evaluates to `  undefined  ` . A `  not-in  ` query with `  null  ` as one of the comparison values does not match any documents.

**Warning:** A `  not-in  ` query clause might match many documents in a collection. To control the number of results returned, use a [limit clause](/firestore/native/docs/query-data/order-limit-data) or [paginate your query](/firestore/native/docs/query-data/query-cursors#paginate_a_query) .

#### `     array-contains-any    `

Use the `  array-contains-any  ` operator to combine [up to 30](#in_not-in_array-contains-any_limits) `  array-contains  ` clauses on the same field with a logical `  OR  ` . An `  array-contains-any  ` query returns documents where the given field is an array that contains one or more of the comparison values:

### Web version 9

``` javascript
import { query, where } from "firebase/firestore";  

const q = query(citiesRef, 
  where('regions', 'array-contains-any', [['west_coast'], ['east_coast']]));array_contains_any_filter.js
```

### Web version 8

[Learn more](//firebase.google.com/docs/web/learn-more#modular-version) about the tree-shakeable modular Web API and its advantages over the namespaced API.

``` javascript
citiesRef.where('regions', 'array-contains-any',
    [['west_coast'], ['east_coast']]);test.firestore.js
```

##### Swift

**Note:** This product is not available on watchOS and App Clip targets.

``` swift
let citiesRef = db.collection("cities")
citiesRef.whereField("regions", arrayContainsAny: ["west_coast", "east_coast"])ViewController.swift
```

##### Objective-C

**Note:** This product is not available on watchOS and App Clip targets.

``` objective-c
FIRCollectionReference *citiesRef = [self.db collectionWithPath:@"cities"];

[citiesRef queryWhereField:@"regions" arrayContainsAny:@[@"west_coast", @"east_coast"]];ViewController.m
```

##### Kotlin  
Android

``` kotlin
val citiesRef = db.collection("cities")

citiesRef.whereArrayContainsAny("regions", listOf("west_coast", "east_coast"))DocSnippets.kt
```

##### Java  
Android

``` java
CollectionReference citiesRef = db.collection("cities");

citiesRef.whereArrayContainsAny("regions", Arrays.asList("west_coast", "east_coast"));DocSnippets.java
```

### Dart

``` dart
final citiesRef = db.collection("cities");
final cities = citiesRef
    .where("regions", arrayContainsAny: ["west_coast", "east_coast"]);firestore.dart
```

##### Java

``` java
CollectionReference citiesRef = db.collection("cities");

Query query =
    citiesRef.whereArrayContainsAny("regions", Arrays.asList("west_coast", "east_coast"));QueryDataSnippets.java
```

##### Python

``` python
cities_ref = db.collection("cities")

query = cities_ref.where(
    filter=FieldFilter(
        "regions", "array_contains_any", ["west_coast", "east_coast"]
    )
)
return querysnippets.py
```

##### Python  
(Async)

``` python
cities_ref = db.collection("cities")

query = cities_ref.where(
    filter=FieldFilter(
        "regions", "array_contains_any", ["west_coast", "east_coast"]
    )
)
return querysnippets.py
```

##### C++

``` cpp
CollectionReference cities_ref = db->Collection("cities");

cities_ref.WhereArrayContainsAny("region", std::vector<FieldValue> {
  FieldValue::String("west_coast"),
  FieldValue::String("east_coast")
});snippets.cpp
```

##### Node.js

``` javascript
const coastalCities = await citiesRef.where('regions', 'array-contains-any',
    ['west_coast', 'east_coast']).get();index.js
```

##### Go

``` go
cities := client.Collection("cities")
query := cities.Where("regions", "array-contains-any", []string{"west_coast", "east_coast"}).Documents(ctx)query.go
```

##### PHP

``` php
$containsQuery = $citiesRef->where('regions', 'array-contains-any', ['west_coast', 'east_coast']);query_filter_array_contains_any.php
```

##### Unity

``` text
Query query = citiesRef.WhereArrayContainsAny(
                         "regions",
                         new List<object>()
                         {
                            new List<object>(){"west_coast"},
                            new List<object>(){"east_coast"}});
```

##### C\#

``` csharp
CollectionReference citiesRef = db.Collection("cities");
Query query = citiesRef.WhereArrayContainsAny("Regions", new[] { "west_coast", "east_coast" });Program.cs
```

##### Ruby

``` ruby
cities_ref = firestore.col collection_path
costal_cities = cities_ref.where "regions", "array-contains-any", ["west_coast", "east_coast"]query_data.rb
```

This query returns every city document where the `  regions  ` field is an array that contains `  west_coast  ` or `  east_coast  ` . From the example data, this includes the `  SF  ` , `  LA  ` , and `  DC  ` documents.

Results from `  array-contains-any  ` are de-duped. Even if a document's array field matches more than one of the comparison values, the result set includes that document only once.

`  array-contains-any  ` always filters by the array data type. For example, the query above would not return a city document where instead of an array, the `  regions  ` field is the string `  west_coast  ` .

You can use an array value as a comparison value for `  in  ` , but unlike `  array-contains-any  ` , the clause matches for an exact match of array length, order, and values. For example:

### Web version 9

``` javascript
import { query, where } from "firebase/firestore";  

const q = query(citiesRef, where('regions', 'in', [['west_coast'], ['east_coast']]));in_filter_with_array.js
```

### Web version 8

[Learn more](//firebase.google.com/docs/web/learn-more#modular-version) about the tree-shakeable modular Web API and its advantages over the namespaced API.

``` javascript
citiesRef.where('regions', 'in',
    [['west_coast'], ['east_coast']]);test.firestore.js
```

##### Swift

**Note:** This product is not available on watchOS and App Clip targets.

``` swift
citiesRef.whereField("regions", in: [["west_coast"], ["east_coast"]])ViewController.swift
```

##### Objective-C

**Note:** This product is not available on watchOS and App Clip targets.

``` objective-c
[citiesRef queryWhereField:@"regions" in:@[@[@"west_coast"], @[@"east_coast"]]];ViewController.m
```

##### Kotlin  
Android

``` kotlin
citiesRef.whereIn("regions", listOf(arrayOf("west_coast"), arrayOf("east_coast")))DocSnippets.kt
```

##### Java  
Android

``` java
citiesRef.whereIn("regions", Arrays.asList(new String[]{"west_coast"}, new String[]{"east_coast"}));DocSnippets.java
```

### Dart

``` dart
final citiesRef = db.collection("cities");
final cities = citiesRef.where("regions", whereIn: [
  ["west_coast"],
  ["east_coast"]
]);firestore.dart
```

##### Java

``` java
CollectionReference citiesRef = db.collection("cities");

Query query =
    citiesRef.whereIn(
        "regions", Arrays.asList(Arrays.asList("west_coast"), Arrays.asList("east_coast")));QueryDataSnippets.java
```

##### Python

``` python
cities_ref = db.collection("cities")

query = cities_ref.where(
    filter=FieldFilter("regions", "in", [["west_coast"], ["east_coast"]])
)
return querysnippets.py
```

##### Python  
(Async)

``` python
cities_ref = db.collection("cities")

query = cities_ref.where(
    filter=FieldFilter("regions", "in", [["west_coast"], ["east_coast"]])
)
return querysnippets.py
```

##### C++

``` cpp
cities_ref.WhereIn("region", std::vector<FieldValue> {
  FieldValue::String("west_coast"),
  FieldValue::String("east_coast")
});snippets.cpp
```

##### Node.js

``` javascript
const exactlyOneCoast = await citiesRef.where('regions', 'in',
    [['west_coast', 'east_coast']]).get();index.js
```

##### Go

``` go
cities := client.Collection("cities")
query := cities.Where("regions", "in", [][]string{{"west_coast"}, {"east_coast"}}).Documents(ctx)query.go
```

##### PHP

``` php
$rangeQuery = $citiesRef->where('regions', 'in', [['west_coast'], ['east_coast']]);query_filter_in_with_array.php
```

##### Unity

``` text
Query query = citiesRef.WhereIn(new FieldPath("regions"), new List<string>{"west_coast", "east_coast"});
```

##### C\#

``` csharp
CollectionReference citiesRef = db.Collection("cities");
Query query = citiesRef.WhereIn("Regions",
    new[] { new[] { "west_coast" }, new[] { "east_coast" } });Program.cs
```

##### Ruby

``` ruby
cities_ref = firestore.col collection_path
exactly_one_cost = cities_ref.where "regions", "in", [["west_coast"], ["east_coast"]]query_data.rb
```

This query returns every city document where the `  regions  ` field is an array that contains exactly one element of either `  west_coast  ` or `  east_coast  ` . From the example data, only the `  DC  ` document qualifies with its `  regions  ` field of `  ["east_coast"]  ` . The `  SF  ` document, however, does not match because its `  regions  ` field is `  ["west_coast", "norcal"]  ` .

#### Standard edition limitations

Note the following limitations for `  in  ` , `  not-in  ` , and `  array-contains-any  ` . These limitations apply only to Standard edition:

  - Firestore provides support for logical `  OR  ` queries through the `  or  ` , `  in  ` , and `  array-contains-any  ` operators. These queries are limited to [30 disjunctions based on the query's disjunctive normal form](#limits_on_or_queries) . This limit is fixed and cannot be adjusted.
  - You can use at most one `  array-contains  ` clause per disjunction ( `  or  ` group). You can't combine `  array-contains  ` with `  array-contains-any  ` in the same disjunction.
  - You can't combine `  not-in  ` with not equals `  !=  ` .
  - `  not-in  ` supports up to 10 comparison values.

## Compound ( `     AND    ` ) queries

You can combine constraints with a logical `  AND  ` by chaining multiple equality operators ( `  ==  ` or `  array-contains  ` ). However, you must create a [composite index](/firestore/native/docs/query-data/indexing) to combine equality operators with the inequality operators, `  <  ` , `  <=  ` , `  >  ` , and `  !=  ` .

### Web version 9

``` javascript
import { query, where } from "firebase/firestore";  

const q1 = query(citiesRef, where("state", "==", "CO"), where("name", "==", "Denver"));
const q2 = query(citiesRef, where("state", "==", "CA"), where("population", "<", 1000000));chain_filters.js
```

### Web version 8

[Learn more](//firebase.google.com/docs/web/learn-more#modular-version) about the tree-shakeable modular Web API and its advantages over the namespaced API.

``` javascript
const q1 = citiesRef.where("state", "==", "CO").where("name", "==", "Denver");
const q2 = citiesRef.where("state", "==", "CA").where("population", "<", 1000000);test.firestore.js
```

##### Swift

**Note:** This product is not available on watchOS and App Clip targets.

``` swift
citiesRef
  .whereField("state", isEqualTo: "CO")
  .whereField("name", isEqualTo: "Denver")
citiesRef
  .whereField("state", isEqualTo: "CA")
  .whereField("population", isLessThan: 1000000)ViewController.swift
```

##### Objective-C

**Note:** This product is not available on watchOS and App Clip targets.

``` objective-c
[[citiesRef queryWhereField:@"state" isEqualTo:@"CO"]
    queryWhereField:@"name" isGreaterThanOrEqualTo:@"Denver"];
[[citiesRef queryWhereField:@"state" isEqualTo:@"CA"]
    queryWhereField:@"population" isLessThan:@1000000];ViewController.m
```

##### Kotlin  
Android

``` kotlin
citiesRef.whereEqualTo("state", "CO").whereEqualTo("name", "Denver")
citiesRef.whereEqualTo("state", "CA").whereLessThan("population", 1000000)DocSnippets.kt
```

##### Java  
Android

``` java
citiesRef.whereEqualTo("state", "CO").whereEqualTo("name", "Denver");
citiesRef.whereEqualTo("state", "CA").whereLessThan("population", 1000000);DocSnippets.java
```

### Dart

``` dart
final citiesRef = db.collection("cities");
citiesRef
    .where("state", isEqualTo: "CO")
    .where("name", isEqualTo: "Denver");
citiesRef
    .where("state", isEqualTo: "CA")
    .where("population", isLessThan: 1000000);firestore.dart
```

##### Java

``` java
Query chainedQuery1 = cities.whereEqualTo("state", "CO").whereEqualTo("name", "Denver");QueryDataSnippets.java
```

##### Python

``` python
cities_ref = db.collection("cities")

denver_query = cities_ref.where(filter=FieldFilter("state", "==", "CO")).where(
    filter=FieldFilter("name", "==", "Denver")
)
large_us_cities_query = cities_ref.where(
    filter=FieldFilter("state", "==", "CA")
).where(filter=FieldFilter("population", ">", 1000000))snippets.py
```

##### Python  
(Async)

``` python
cities_ref = db.collection("cities")

denver_query = cities_ref.where(filter=FieldFilter("state", "==", "CO")).where(
    filter=FieldFilter("name", "==", "Denver")
)
large_us_cities_query = cities_ref.where(
    filter=FieldFilter("state", "==", "CA")
).where(filter=FieldFilter("population", ">", 1000000))snippets.py
```

##### C++

``` cpp
cities_ref.WhereEqualTo("state", FieldValue::String("CO"))
    .WhereEqualTo("name", FieldValue::String("Denver"));
cities_ref.WhereEqualTo("state", FieldValue::String("CA"))
    .WhereLessThan("population", FieldValue::Integer(1000000));snippets.cpp
```

##### Node.js

``` javascript
citiesRef.where('state', '==', 'CO').where('name', '==', 'Denver');
citiesRef.where('state', '==', 'CA').where('population', '<', 1000000);index.js
```

##### Go

``` go
denverQuery := cities.Where("name", "==", "Denver").Where("state", "==", "CO")
caliQuery := cities.Where("state", "==", "CA").Where("population", "<=", 1000000)
query := cities.Where("country", "==", "USA").Where("population", ">", 5000000)query.go
```

##### PHP

``` php
$chainedQuery = $citiesRef
    ->where('state', '=', 'CA')
    ->where('name', '=', 'San Francisco');query_filter_compound_multi_eq.php
```

##### Unity

``` text
Query chainedQuery = citiesRef
    .WhereEqualTo("State", "CA")
    .WhereEqualTo("Name", "San Francisco");
```

##### C\#

``` csharp
CollectionReference citiesRef = db.Collection("cities");
Query chainedQuery = citiesRef
    .WhereEqualTo("State", "CA")
    .WhereEqualTo("Name", "San Francisco");Program.cs
```

##### Ruby

``` ruby
chained_query = cities_ref.where("state", "=", "CA").where("name", "=", "San Francisco")query_data.rb
```

## `     OR    ` queries

You can combine constraints with a logical `  OR  ` . For example:

### Web version 9

``` text
const q = query(citiesRef,
  or(where('capital', '==', true),
     where('population', '>=', 1000000)
  )
);
  
```

### Web version 8

Not available.

##### Swift

``` text
let query = db.collection("cities").whereFilter(Filter.orFilter([
                Filter.whereField("capital", isEqualTo: true),
                Filter.whereField("population", isGreaterThanOrEqualTo: 1000000);
            ]))
  
```

##### Objective-C

``` text
  FIRCollectionReference *collection = [self.db collectionWithPath:@"cities"];
  FIRQuery *query = [collection queryWhereFilter:[FIRFilter orFilterWithFilters:@[
      [FIRFilter filterWhereField:@"capital" isEqualTo:@YES],
      [FIRFilter filterWhereField:@"population" isGreaterThanOrEqualTo:@1000000]
  ]]];
  
```

##### Kotlin  
Android

``` text
val query = collection.where(Filter.or(
        Filter.equalTo("capital", true),
        Filter.greaterThanOrEqualTo("population", 1000000)
))
  
```

##### Java  
Android

``` text
Query query = collection.where(Filter.or(
        Filter.equalTo("capital", true),
        Filter.greaterThanOrEqualTo("population", 1000000)
));
  
```

### Dart

``` dart
var query = db.collection("cities").where(
      Filter.or(
        Filter("capital", isEqualTo: true),
        Filter("population", isGreaterThan: 1000000),
      ),
    );firestore.dart
```

##### Java

Snippet not available.

##### Python

``` python
from google.cloud.firestore_v1.base_query import FieldFilter, Or

col_ref = client.collection("cities")
# Execute the query
query = col_ref.where(
    filter=Or(
        [
            FieldFilter("capital", "==", True),
            FieldFilter("population", ">", 1_000_000),
        ]
    )
)
docs = query.stream()query_filter_or.py
```

##### Python  
(Async)

Snippet not available.

##### C++

Snippet not available.

##### Node.js

``` javascript
const bigCities = await citiesRef
  .where(
    Filter.or(
      Filter.where('capital', '==', true),
      Filter.where('population', '>=', 1000000)
    )
  )
  .get();index.js
```

##### Go

``` go
import (
 "context"
 "fmt"
 "io"

 firestore "cloud.google.com/go/firestore"
 "google.golang.org/api/iterator"
)

func queryFilterOr(w io.Writer, projectId string) error {
 // Instantiate a client
 ctx := context.Background()
 client, err := firestore.NewClient(ctx, projectId)
 if err != nil {
     return err
 }
 // always be sure to close the client to release resources
 defer client.Close()

 q1 := firestore.PropertyFilter{
     Path:     "birthYear",
     Operator: "==",
     Value:    1906,
 }

 q2 := firestore.PropertyFilter{
     Path:     "birthYear",
     Operator: "==",
     Value:    1815,
 }

 orFilter := firestore.OrFilter{
     Filters: []firestore.EntityFilter{q1, q2},
 }

 orQuery := client.Collection("users").WhereEntity(orFilter)
 it := orQuery.Documents(ctx)
 if err != nil {
     return err
 }

 fmt.Fprint(w, "Individual documents:\n")
 for {
     doc, err := it.Next()
     if err == iterator.Done {
         break
     }
     if err != nil {
         return fmt.Errorf("documents iterator: %w", err)
     }
     fmt.Fprintf(w, "%s: %s", doc.Ref.ID, doc.Data()["birthYear"])
 }

 return nil
}
query_filter_or.go
```

##### PHP

Snippet not available.

##### Unity

``` text
Query query = citiesRef.Where(Filter.Or(
        Filter.EqualTo("State", "CA"),
        Filter.GreaterThanOrEqualTo("population", 1000000)
));
query.GetSnapshotAsync().ContinueWithOnMainThread((querySnapshotTask) =>
{
    foreach (DocumentSnapshot documentSnapshot in querySnapshotTask.Result.Documents)
    {
        Debug.Log(String.Format("Document {0} returned by query State=CA or population >= {1}", documentSnapshot.Id, 1000000));
    } 
});
```

##### C\#

Snippet not available.

##### Ruby

Snippet not available.

Firestore uses your composite indexes to serve `  OR  ` queries. If your indexes do not support the query, Firestore [suggests additional indexes for your database](/firestore/native/docs/query-data/indexing#create_a_missing_index_through_an_error_message) .

You can combine `  OR  ` queries with compound queries to filter on combinations of `  OR  ` and `  AND  ` operations. For example:

### Web version 9

``` javascript
const q = query(collection(db, "cities"), and(
  where('state', '==', 'CA'),   
  or(
    where('capital', '==', true),
    where('population', '>=', 1000000)
  )
));test.firestore.js
```

### Web version 8

Not available.

##### Swift

**Note:** This product is not available on watchOS and App Clip targets.

``` swift
let query = db.collection("cities").whereFilter(Filter.andFilter([
  Filter.whereField("state", isEqualTo: "CA"),
  Filter.orFilter([
    Filter.whereField("capital", isEqualTo: true),
    Filter.whereField("population", isGreaterOrEqualTo: 1000000)
  ])
]))ViewController.swift
```

##### Objective-C

**Note:** This product is not available on watchOS and App Clip targets.

``` objective-c
FIRCollectionReference *collection = [self.db collectionWithPath:@"cities"];
FIRQuery *query = [collection queryWhereFilter:[FIRFilter andFilterWithFilters:@[
  [FIRFilter filterWhereField:@"state" isEqualTo:@"CA"],
  [FIRFilter orFilterWithFilters:@[
    [FIRFilter filterWhereField:@"capital" isEqualTo:@YES],
    [FIRFilter filterWhereField:@"population" isGreaterThanOrEqualTo:@1000000]
  ]]
]]];ViewController.m
```

##### Kotlin  
Android

``` kotlin
val query = collection.where(Filter.and(
    Filter.equalTo("state", "CA"),
    Filter.or(
        Filter.equalTo("capital", true),
        Filter.greaterThanOrEqualTo("population", 1000000)
    )
))DocSnippets.kt
```

##### Java  
Android

``` java
Query query = collection.where(Filter.and(
    Filter.equalTo("state", "CA"),
    Filter.or(
        Filter.equalTo("capital", true),
        Filter.greaterThanOrEqualTo("population", 1000000)
    )
));DocSnippets.java
```

### Dart

``` dart
var query = db.collection("cities").where(
      Filter.and(
        Filter("state", isEqualTo: "CA"),
        Filter.or(
          Filter("capital", isEqualTo: true),
          Filter("population", isGreaterThan: 1000000),
        ),
      ),
    );firestore.dart
```

##### Java

Snippet not available.

##### Python

Snippet not available.

##### Python  
(Async)

Snippet not available.

##### C++

Snippet not available.

##### Node.js

``` javascript
const bigCitiesInCalifornia = await citiesRef
  .where('state', '==', 'CA')
  .where(
    Filter.or(
      Filter.where('capital', '==', true),
      Filter.where('population', '>=', 1000000)
    )
  )
  .get();index.js
```

##### Go

Snippet not available.

##### PHP

Snippet not available.

##### Unity

``` text
Query query = citiesRef.Where(Filter.And(
    Filter.EqualTo("state", "CA"),
    Filter.Or(
        Filter.EqualTo("capital", true),
        Filter.GreaterThanOrEqualTo("population", 1000000)
    )
));
```

##### C\#

Snippet not available.

##### Ruby

Snippet not available.

### Standard edition limitations

Note the following limitations for `  or  ` queries. These limitations apply only to Standard edition:

  - Firestore limits a query to a [maximum of 30 disjunctions based on the query's disjunctive normal form](#limits_on_or_queries) . This limit is fixed and cannot be adjusted. You are more likely to reach this limit when performing an `  AND  ` of multiple `  OR  ` groups.

  - You can't combine `  not-in  ` with `  in  ` , `  array-contains-any  ` , or `  or  ` in the same query.

For a full description of limitations, see [Query limitations](#query_limitations) .

## Collection group queries

A collection group consists of all collections with the same ID. By default, queries retrieve results from a single collection in your database. Use a collection group query to retrieve documents from a collection group instead of from a single collection.

For example, you can create a `  landmarks  ` collection group by adding a landmarks subcollection to each city:

### Web version 9

``` javascript
import { collection, addDoc } from "firebase/firestore";  

const citiesRef = collection(db, 'cities');

await Promise.all([
    addDoc(collection(citiesRef, 'SF', 'landmarks'), {
        name: 'Golden Gate Bridge',
        type: 'bridge'
    }),
    addDoc(collection(citiesRef, 'SF', 'landmarks'), {
        name: 'Legion of Honor',
        type: 'museum'
    }),
    addDoc(collection(citiesRef, 'LA', 'landmarks'), {
        name: 'Griffith Park',
        type: 'park'
    }),
    addDoc(collection(citiesRef, 'LA', 'landmarks'), {
        name: 'The Getty',
        type: 'museum'
    }),
    addDoc(collection(citiesRef, 'DC', 'landmarks'), {
        name: 'Lincoln Memorial',
        type: 'memorial'
    }),
    addDoc(collection(citiesRef, 'DC', 'landmarks'), {
        name: 'National Air and Space Museum',
        type: 'museum'
    }),
    addDoc(collection(citiesRef, 'TOK', 'landmarks'), {
        name: 'Ueno Park',
        type: 'park'
    }),
    addDoc(collection(citiesRef, 'TOK', 'landmarks'), {
        name: 'National Museum of Nature and Science',
        type: 'museum'
    }),
    addDoc(collection(citiesRef, 'BJ', 'landmarks'), {
        name: 'Jingshan Park',
        type: 'park'
    }),
    addDoc(collection(citiesRef, 'BJ', 'landmarks'), {
        name: 'Beijing Ancient Observatory',
        type: 'museum'
    })
]);fs_collection_group_query_data_setup.js
```

### Web version 8

[Learn more](//firebase.google.com/docs/web/learn-more#modular-version) about the tree-shakeable modular Web API and its advantages over the namespaced API.

``` javascript
var citiesRef = db.collection('cities');

var landmarks = Promise.all([
    citiesRef.doc('SF').collection('landmarks').doc().set({
        name: 'Golden Gate Bridge',
        type: 'bridge'
    }),
    citiesRef.doc('SF').collection('landmarks').doc().set({
        name: 'Legion of Honor',
        type: 'museum'
    }),
    citiesRef.doc('LA').collection('landmarks').doc().set({
        name: 'Griffith Park',
        type: 'park'
    }),
    citiesRef.doc('LA').collection('landmarks').doc().set({
        name: 'The Getty',
        type: 'museum'
    }),
    citiesRef.doc('DC').collection('landmarks').doc().set({
        name: 'Lincoln Memorial',
        type: 'memorial'
    }),
    citiesRef.doc('DC').collection('landmarks').doc().set({
        name: 'National Air and Space Museum',
        type: 'museum'
    }),
    citiesRef.doc('TOK').collection('landmarks').doc().set({
        name: 'Ueno Park',
        type: 'park'
    }),
    citiesRef.doc('TOK').collection('landmarks').doc().set({
        name: 'National Museum of Nature and Science',
        type: 'museum'
    }),
    citiesRef.doc('BJ').collection('landmarks').doc().set({
        name: 'Jingshan Park',
        type: 'park'
    }),
    citiesRef.doc('BJ').collection('landmarks').doc().set({
        name: 'Beijing Ancient Observatory',
        type: 'museum'
    })
]);test.firestore.js
```

##### Swift

**Note:** This product is not available on watchOS and App Clip targets.

``` swift
let citiesRef = db.collection("cities")

var data = ["name": "Golden Gate Bridge", "type": "bridge"]
citiesRef.document("SF").collection("landmarks").addDocument(data: data)

data = ["name": "Legion of Honor", "type": "museum"]
citiesRef.document("SF").collection("landmarks").addDocument(data: data)

data = ["name": "Griffith Park", "type": "park"]
citiesRef.document("LA").collection("landmarks").addDocument(data: data)

data = ["name": "The Getty", "type": "museum"]
citiesRef.document("LA").collection("landmarks").addDocument(data: data)

data = ["name": "Lincoln Memorial", "type": "memorial"]
citiesRef.document("DC").collection("landmarks").addDocument(data: data)

data = ["name": "National Air and Space Museum", "type": "museum"]
citiesRef.document("DC").collection("landmarks").addDocument(data: data)

data = ["name": "Ueno Park", "type": "park"]
citiesRef.document("TOK").collection("landmarks").addDocument(data: data)

data = ["name": "National Museum of Nature and Science", "type": "museum"]
citiesRef.document("TOK").collection("landmarks").addDocument(data: data)

data = ["name": "Jingshan Park", "type": "park"]
citiesRef.document("BJ").collection("landmarks").addDocument(data: data)

data = ["name": "Beijing Ancient Observatory", "type": "museum"]
citiesRef.document("BJ").collection("landmarks").addDocument(data: data)ViewController.swift
```

##### Objective-C

**Note:** This product is not available on watchOS and App Clip targets.

``` objective-c
FIRCollectionReference *citiesRef = [self.db collectionWithPath:@"cities"];

NSDictionary *data = @{@"name": @"Golden Gate Bridge", @"type": @"bridge"};
[[[citiesRef documentWithPath:@"SF"] collectionWithPath:@"landmarks"] addDocumentWithData:data];

data = @{@"name": @"Legion of Honor", @"type": @"museum"};
[[[citiesRef documentWithPath:@"SF"] collectionWithPath:@"landmarks"] addDocumentWithData:data];

data = @{@"name": @"Griffith Park", @"type": @"park"};
[[[citiesRef documentWithPath:@"LA"] collectionWithPath:@"landmarks"] addDocumentWithData:data];

data = @{@"name": @"The Getty", @"type": @"museum"};
[[[citiesRef documentWithPath:@"LA"] collectionWithPath:@"landmarks"] addDocumentWithData:data];

data = @{@"name": @"Lincoln Memorial", @"type": @"memorial"};
[[[citiesRef documentWithPath:@"DC"] collectionWithPath:@"landmarks"] addDocumentWithData:data];

data = @{@"name": @"National Air and Space Museum", @"type": @"museum"};
[[[citiesRef documentWithPath:@"DC"] collectionWithPath:@"landmarks"] addDocumentWithData:data];

data = @{@"name": @"Ueno Park", @"type": @"park"};
[[[citiesRef documentWithPath:@"TOK"] collectionWithPath:@"landmarks"] addDocumentWithData:data];

data = @{@"name": @"National Museum of Nature and Science", @"type": @"museum"};
[[[citiesRef documentWithPath:@"TOK"] collectionWithPath:@"landmarks"] addDocumentWithData:data];

data = @{@"name": @"Jingshan Park", @"type": @"park"};
[[[citiesRef documentWithPath:@"BJ"] collectionWithPath:@"landmarks"] addDocumentWithData:data];

data = @{@"name": @"Beijing Ancient Observatory", @"type": @"museum"};
[[[citiesRef documentWithPath:@"BJ"] collectionWithPath:@"landmarks"] addDocumentWithData:data];ViewController.m
```

##### Kotlin  
Android

``` kotlin
val citiesRef = db.collection("cities")

val ggbData = mapOf(
    "name" to "Golden Gate Bridge",
    "type" to "bridge",
)
citiesRef.document("SF").collection("landmarks").add(ggbData)

val lohData = mapOf(
    "name" to "Legion of Honor",
    "type" to "museum",
)
citiesRef.document("SF").collection("landmarks").add(lohData)

val gpData = mapOf(
    "name" to "Griffth Park",
    "type" to "park",
)
citiesRef.document("LA").collection("landmarks").add(gpData)

val tgData = mapOf(
    "name" to "The Getty",
    "type" to "museum",
)
citiesRef.document("LA").collection("landmarks").add(tgData)

val lmData = mapOf(
    "name" to "Lincoln Memorial",
    "type" to "memorial",
)
citiesRef.document("DC").collection("landmarks").add(lmData)

val nasaData = mapOf(
    "name" to "National Air and Space Museum",
    "type" to "museum",
)
citiesRef.document("DC").collection("landmarks").add(nasaData)

val upData = mapOf(
    "name" to "Ueno Park",
    "type" to "park",
)
citiesRef.document("TOK").collection("landmarks").add(upData)

val nmData = mapOf(
    "name" to "National Musuem of Nature and Science",
    "type" to "museum",
)
citiesRef.document("TOK").collection("landmarks").add(nmData)

val jpData = mapOf(
    "name" to "Jingshan Park",
    "type" to "park",
)
citiesRef.document("BJ").collection("landmarks").add(jpData)

val baoData = mapOf(
    "name" to "Beijing Ancient Observatory",
    "type" to "musuem",
)
citiesRef.document("BJ").collection("landmarks").add(baoData)DocSnippets.kt
```

##### Java  
Android

``` java
CollectionReference citiesRef = db.collection("cities");

Map<String, Object> ggbData = new HashMap<>();
ggbData.put("name", "Golden Gate Bridge");
ggbData.put("type", "bridge");
citiesRef.document("SF").collection("landmarks").add(ggbData);

Map<String, Object> lohData = new HashMap<>();
lohData.put("name", "Legion of Honor");
lohData.put("type", "museum");
citiesRef.document("SF").collection("landmarks").add(lohData);

Map<String, Object> gpData = new HashMap<>();
gpData.put("name", "Griffith Park");
gpData.put("type", "park");
citiesRef.document("LA").collection("landmarks").add(gpData);

Map<String, Object> tgData = new HashMap<>();
tgData.put("name", "The Getty");
tgData.put("type", "museum");
citiesRef.document("LA").collection("landmarks").add(tgData);

Map<String, Object> lmData = new HashMap<>();
lmData.put("name", "Lincoln Memorial");
lmData.put("type", "memorial");
citiesRef.document("DC").collection("landmarks").add(lmData);

Map<String, Object> nasaData = new HashMap<>();
nasaData.put("name", "National Air and Space Museum");
nasaData.put("type", "museum");
citiesRef.document("DC").collection("landmarks").add(nasaData);

Map<String, Object> upData = new HashMap<>();
upData.put("name", "Ueno Park");
upData.put("type", "park");
citiesRef.document("TOK").collection("landmarks").add(upData);

Map<String, Object> nmData = new HashMap<>();
nmData.put("name", "National Museum of Nature and Science");
nmData.put("type", "museum");
citiesRef.document("TOK").collection("landmarks").add(nmData);

Map<String, Object> jpData = new HashMap<>();
jpData.put("name", "Jingshan Park");
jpData.put("type", "park");
citiesRef.document("BJ").collection("landmarks").add(jpData);

Map<String, Object> baoData = new HashMap<>();
baoData.put("name", "Beijing Ancient Observatory");
baoData.put("type", "museum");
citiesRef.document("BJ").collection("landmarks").add(baoData);DocSnippets.java
```

### Dart

``` dart
final citiesRef = db.collection("cities");

final ggbData = {"name": "Golden Gate Bridge", "type": "bridge"};
citiesRef.doc("SF").collection("landmarks").add(ggbData);

final lohData = {"name": "Legion of Honor", "type": "museum"};
citiesRef.doc("SF").collection("landmarks").add(lohData);

final gpData = {"name": "Griffth Park", "type": "park"};
citiesRef.doc("LA").collection("landmarks").add(gpData);

final tgData = {"name": "The Getty", "type": "museum"};
citiesRef.doc("LA").collection("landmarks").add(tgData);

final lmData = {"name": "Lincoln Memorial", "type": "memorial"};
citiesRef.doc("DC").collection("landmarks").add(lmData);

final nasaData = {
  "name": "National Air and Space Museum",
  "type": "museum"
};
citiesRef.doc("DC").collection("landmarks").add(nasaData);

final upData = {"name": "Ueno Park", "type": "park"};
citiesRef.doc("TOK").collection("landmarks").add(upData);

final nmData = {
  "name": "National Musuem of Nature and Science",
  "type": "museum"
};
citiesRef.doc("TOK").collection("landmarks").add(nmData);

final jpData = {"name": "Jingshan Park", "type": "park"};
citiesRef.doc("BJ").collection("landmarks").add(jpData);

final baoData = {"name": "Beijing Ancient Observatory", "type": "musuem"};
citiesRef.doc("BJ").collection("landmarks").add(baoData);firestore.dart
```

##### Java

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
final List<WriteResult> landmarks = ApiFutures.allAsList(futures).get();QueryDataSnippets.java
```

##### Python

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
)snippets.py
```

##### Python  
(Async)

``` python
cities = db.collection("cities")

sf_landmarks = cities.document("SF").collection("landmarks")
await sf_landmarks.document().set({"name": "Golden Gate Bridge", "type": "bridge"})
await sf_landmarks.document().set({"name": "Legion of Honor", "type": "museum"})
la_landmarks = cities.document("LA").collection("landmarks")
await la_landmarks.document().set({"name": "Griffith Park", "type": "park"})
await la_landmarks.document().set({"name": "The Getty", "type": "museum"})
dc_landmarks = cities.document("DC").collection("landmarks")
await dc_landmarks.document().set({"name": "Lincoln Memorial", "type": "memorial"})
await dc_landmarks.document().set(
    {"name": "National Air and Space Museum", "type": "museum"}
)
tok_landmarks = cities.document("TOK").collection("landmarks")
await tok_landmarks.document().set({"name": "Ueno Park", "type": "park"})
await tok_landmarks.document().set(
    {"name": "National Museum of Nature and Science", "type": "museum"}
)
bj_landmarks = cities.document("BJ").collection("landmarks")
await bj_landmarks.document().set({"name": "Jingshan Park", "type": "park"})
await bj_landmarks.document().set(
    {"name": "Beijing Ancient Observatory", "type": "museum"}
)snippets.py
```

##### C++

``` text
// Get a new write batch
WriteBatch batch = db->batch();

DocumentReference sf_ref = db->Collection("cities").Document("SF");
batch.Set(sf_ref,{{"name", FieldValue::String("Golden Gate Bridge")}, {"type", FieldValue::String("bridge")}});
batch.Set(sf_ref,{{"name", FieldValue::String("Legion of Honor")}, {"type", FieldValue::String("museum")}});

DocumentReference la_ref = db->Collection("cities").Document("LA");
batch.Set(la_ref,{{"name", FieldValue::String("Griffith Park")}, {"type", FieldValue::String("park")}});
batch.Set(la_ref,{{"name", FieldValue::String("The Getty")}, {"type", FieldValue::String("museum")}});

DocumentReference dc_ref = db->Collection("cities").Document("DC");
batch.Set(dc_ref,{{"name", FieldValue::String("Lincoln Memorial")}, {"type", FieldValue::String("memorial")}});
batch.Set(dc_ref,{{"name", FieldValue::String("National Air and Space Museum")}, {"type", FieldValue::String("museum")}});

DocumentReference tok_ref = db->Collection("cities").Document("TOK");
batch.Set(tok_ref,{{"name", FieldValue::String("Ueno Park")}, {"type", FieldValue::String("park")}});
batch.Set(tok_ref,{{"name", FieldValue::String("National Museum of Nature and Science")}, {"type", FieldValue::String("museum")}});

DocumentReference bj_ref = db->Collection("cities").Document("BJ");
batch.Set(bj_ref,{{"name", FieldValue::String("Jingshan Park")}, {"type", FieldValue::String("park")}});
batch.Set(bj_ref,{{"name", FieldValue::String("Beijing Ancient Observatory")}, {"type", FieldValue::String("museum")}});

// Commit the batch
batch.Commit().OnCompletion([](const Future<void>& future) {
  if (future.error() == Error::kErrorOk) {
    std::cout << "Write batch success!" << std::endl;
  } else {
    std::cout << "Write batch failure: " << future.error_message() << std::endl;
  }
});
```

##### Node.js

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
});index.js
```

##### Go

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
collection_group_setup.go
```

##### PHP

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
print('Added example landmarks collections to the cities collection.' . PHP_EOL);query_collection_group_dataset.php
```

##### Unity

``` text
List<Task<DocumentReference>> futures =
    new List<Task<DocumentReference>>(){
        citiesRef
            .Document("SF")
            .Collection("landmarks")
            .AddAsync(
                new Dictionary<string, object>()
                {
                    {"name", "Golden Gate Bridge"},
                    {"type", "bridge"},
                }
                ),
        citiesRef
            .Document("SF")
            .Collection("landmarks")
            .AddAsync(
                new Dictionary<string, object>()
                {
                    {"name", "Legion of Honor"},
                    {"type", "museum"},
                }
                ),
        citiesRef
            .Document("LA")
            .Collection("landmarks")
            .AddAsync(
                new Dictionary<string, object>() 
                {
                    {"name", "Griffith Park"},
                    {"type", "park"},
                }
                ),
        citiesRef
            .Document("LA")
            .Collection("landmarks")
            .AddAsync(
                new Dictionary<string, object>() 
                {
                    {"name", "The Getty"},
                    {"type", "museum"},
                }
                ),
        citiesRef
            .Document("DC")
            .Collection("landmarks")
            .AddAsync(
                new Dictionary<string, object>() 
                {
                    {"name", "Lincoln Memorial"},
                    {"type", "memorial"},
                }
                ),
        citiesRef
            .Document("DC")
            .Collection("landmarks")
            .AddAsync(
                new Dictionary<string, object>()
                {
                    {"name", "National Air and Space Museum"},
                    {"type", "museum"},
                }
                ),
        citiesRef
            .Document("TOK")
            .Collection("landmarks")
            .AddAsync(
                new Dictionary<string, object>()
                {
                    {"name", "Ueno Park"},
                    {"type", "park"},
                }
                ),
        citiesRef
            .Document("TOK")
            .Collection("landmarks")
            .AddAsync(
                new Dictionary<string, object>()
                {
                    {"name", "National Museum of Nature and Science"},
                    {"type", "museum"},
                }
                ),
        citiesRef
            .Document("BJ")
            .Collection("landmarks")
            .AddAsync(
                new Dictionary<string, object>()
                {
                    {"name", "Jingshan Park"},
                    {"type", "park"},
                }
                ),
        citiesRef
            .Document("BJ")
            .Collection("landmarks")
            .AddAsync(
                new Dictionary<string, object>()
                {
                    {"name", "Beijing Ancient Observatory"},
                    {"type", "museum"},
                }
                )};
DocumentReference[] landmarks = Task.WhenAll(futures).Result;
```

##### C\#

``` csharp
// Copyright(c) 2017 Google Inc.
//
// Licensed under the Apache License, Version 2.0 (the "License"); you may not
// use this file except in compliance with the License. You may obtain a copy of
// the License at
//
// http://www.apache.org/licenses/LICENSE-2.0
//
// Unless required by applicable law or agreed to in writing, software
// distributed under the License is distributed on an "AS IS" BASIS, WITHOUT
// WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. See the
// License for the specific language governing permissions and limitations under
// the License.

using Google.Cloud.Firestore;
using Google.Cloud.Firestore.Admin.V1;
using Google.Protobuf.WellKnownTypes;
using Grpc.Core;
using System;
using System.Collections;
using System.Collections.Generic;
using System.Threading.Tasks;
using static Google.Cloud.Firestore.Admin.V1.Index.Types;

namespace GoogleCloudSamples
{
    public class QueryData
    {
        public static string Usage = @"Usage:
C:\> dotnet run command YOUR_PROJECT_ID

Where command is one of
    query-create-examples
    create-query-state
    create-query-capital
    simple-queries
    array-contains-query
    array-contains-any-query
    in-query
    in-query-array
    collection-group-query
    subcollection-query
    chained-query
    composite-index-chained-query
    range-query
    multiple-inequalities
";
        private static async Task QueryCreateExamples(string project)
        {
            FirestoreDb db = FirestoreDb.Create(project);
            // Note: the extra braces here are just to allow multiple citiesRef local variables.
            {
                CollectionReference citiesRef = db.Collection("cities");
                await citiesRef.Document("SF").SetAsync(new Dictionary<string, object>
                {
                    { "Name", "San Francisco" },
                    { "State", "CA" },
                    { "Country", "USA" },
                    { "Capital", false },
                    { "Population", 860000 },
                    { "Density", 18000 },
                    { "Regions", new[] {"west_coast", "norcal"} }
                });
                await citiesRef.Document("LA").SetAsync(new Dictionary<string, object>
                {
                    { "Name", "Los Angeles" },
                    { "State", "CA" },
                    { "Country", "USA" },
                    { "Capital", false },
                    { "Population", 3900000 },
                    { "Density", 8300 },
                    { "Regions", new[] {"west_coast", "socal"} }
                });
                await citiesRef.Document("DC").SetAsync(new Dictionary<string, object>
                {
                    { "Name", "Washington D.C." },
                    { "State", null },
                    { "Country", "USA" },
                    { "Capital", true },
                    { "Population", 680000 },
                    { "Density", 11300 },
                    { "Regions", new[] {"east_coast"} }
                });
                await citiesRef.Document("TOK").SetAsync(new Dictionary<string, object>
                {
                    { "Name", "Tokyo" },
                    { "State", null },
                    { "Country", "Japan" },
                    { "Capital", true },
                    { "Population", 9000000 },
                    { "Density", 16000 },
                    { "Regions", new[] {"kanto", "honshu"} }
                });
                await citiesRef.Document("BJ").SetAsync(new Dictionary<string, object>
                {
                    { "Name", "Beijing" },
                    { "State", null },
                    { "Country", "China" },
                    { "Capital", true },
                    { "Population", 21500000 },
                    { "Density", 3500 },
                    { "Regions", new[] {"jingjinji", "hebei"} }
                });
                Console.WriteLine("Added example cities data to the cities collection.");
            }

            {
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
            }
        }

        private static async Task CreateQueryState(string project)
        {
            FirestoreDb db = FirestoreDb.Create(project);
            CollectionReference citiesRef = db.Collection("cities");
            Query query = citiesRef.WhereEqualTo("State", "CA");
            QuerySnapshot querySnapshot = await query.GetSnapshotAsync();
            foreach (DocumentSnapshot documentSnapshot in querySnapshot.Documents)
            {
                Console.WriteLine("Document {0} returned by query State=CA", documentSnapshot.Id);
            }
        }

        private static async Task CreateQueryCapital(string project)
        {
            FirestoreDb db = FirestoreDb.Create(project);
            CollectionReference citiesRef = db.Collection("cities");
            Query query = citiesRef.WhereEqualTo("Capital", true);
            QuerySnapshot querySnapshot = await query.GetSnapshotAsync();
            foreach (DocumentSnapshot documentSnapshot in querySnapshot.Documents)
            {
                Console.WriteLine("Document {0} returned by query Capital=true", documentSnapshot.Id);
            }
        }

        private static async Task SimpleQueries(string project)
        {
            FirestoreDb db = FirestoreDb.Create(project);
            CollectionReference citiesRef = db.Collection("cities");
            Query stateQuery = citiesRef.WhereEqualTo("State", "CA");
            Query populationQuery = citiesRef.WhereGreaterThan("Population", 1000000);
            Query nameQuery = citiesRef.WhereGreaterThanOrEqualTo("Name", "San Francisco");
            QuerySnapshot stateQuerySnapshot = await stateQuery.GetSnapshotAsync();
            foreach (DocumentSnapshot documentSnapshot in stateQuerySnapshot.Documents)
            {
                Console.WriteLine("Document {0} returned by query State=CA", documentSnapshot.Id);
            }
            QuerySnapshot populationQuerySnapshot = await populationQuery.GetSnapshotAsync();
            foreach (DocumentSnapshot documentSnapshot in populationQuerySnapshot.Documents)
            {
                Console.WriteLine("Document {0} returned by query Population>1000000", documentSnapshot.Id);
            }
            QuerySnapshot nameQuerySnapshot = await nameQuery.GetSnapshotAsync();
            foreach (DocumentSnapshot documentSnapshot in nameQuerySnapshot.Documents)
            {
                Console.WriteLine("Document {0} returned by query Name>=San Francisco", documentSnapshot.Id);
            }
        }

        private static async Task ArrayContainsQuery(string project)
        {
            FirestoreDb db = FirestoreDb.Create(project);
            CollectionReference citiesRef = db.Collection("cities");
            Query query = citiesRef.WhereArrayContains("Regions", "west_coast");
            QuerySnapshot querySnapshot = await query.GetSnapshotAsync();
            foreach (DocumentSnapshot documentSnapshot in querySnapshot.Documents)
            {
                Console.WriteLine("Document {0} returned by query 'Regions array_contains west_coast'", documentSnapshot.Id);
            }
        }

        private static async Task ArrayContainsAnyQuery(string project)
        {
            FirestoreDb db = FirestoreDb.Create(project);
            CollectionReference citiesRef = db.Collection("cities");
            Query query = citiesRef.WhereArrayContainsAny("Regions", new[] { "west_coast", "east_coast" });
            QuerySnapshot querySnapshot = await query.GetSnapshotAsync();
            foreach (DocumentSnapshot documentSnapshot in querySnapshot.Documents)
            {
                Console.WriteLine("Document {0} returned by query 'Regions array_contains_any {{west_coast, east_coast}}'", documentSnapshot.Id);
            }
        }

        private static async Task InQueryWithoutArray(string project)
        {
            FirestoreDb db = FirestoreDb.Create(project);
            CollectionReference citiesRef = db.Collection("cities");
            Query query = citiesRef.WhereIn("Country", new[] { "USA", "Japan" });
            QuerySnapshot querySnapshot = await query.GetSnapshotAsync();
            foreach (DocumentSnapshot documentSnapshot in querySnapshot.Documents)
            {
                Console.WriteLine("Document {0} returned by query 'Country in {{USA, Japan}}'", documentSnapshot.Id);
            }
        }

        private static async Task InQueryWithArray(string project)
        {
            FirestoreDb db = FirestoreDb.Create(project);
            CollectionReference citiesRef = db.Collection("cities");
            Query query = citiesRef.WhereIn("Regions",
                new[] { new[] { "west_coast" }, new[] { "east_coast" } });
            QuerySnapshot querySnapshot = await query.GetSnapshotAsync();
            foreach (DocumentSnapshot documentSnapshot in querySnapshot.Documents)
            {
                Console.WriteLine("Document {0} returned by query 'Regions in {{west_coast}}, {{east_coast}}'", documentSnapshot.Id);
            }
        }

        private static async Task CollectionGroupQuery(string project)
        {
            FirestoreDb db = FirestoreDb.Create(project);
            Query museums = db.CollectionGroup("landmarks").WhereEqualTo("Type", "museum");
            QuerySnapshot querySnapshot = await museums.GetSnapshotAsync();
            foreach (DocumentSnapshot document in querySnapshot.Documents)
            {
                Console.WriteLine($"{document.Reference.Path}: {document.GetValue<string>("Name")}");
            }
        }

        private static async Task SubcollectionQuery(string project)
        {
            FirestoreDb db = FirestoreDb.Create(project);
            CollectionReference landmarks = db.Collection("cities").Document("SF").Collection("landmarks");
            QuerySnapshot querySnapshot = await landmarks.GetSnapshotAsync();
            foreach (DocumentSnapshot document in querySnapshot.Documents)
            {
                Console.WriteLine($"{document.Reference.Path}: {document.GetValue<string>("Name")}");
            }
        }

        private static async Task ChainedQuery(string project)
        {
            FirestoreDb db = FirestoreDb.Create(project);
            CollectionReference citiesRef = db.Collection("cities");
            Query chainedQuery = citiesRef
                .WhereEqualTo("State", "CA")
                .WhereEqualTo("Name", "San Francisco");
            QuerySnapshot querySnapshot = await chainedQuery.GetSnapshotAsync();
            foreach (DocumentSnapshot documentSnapshot in querySnapshot.Documents)
            {
                Console.WriteLine("Document {0} returned by query State=CA and Name=San Francisco", documentSnapshot.Id);
            }
        }

        private static async Task CompositeIndexChainedQuery(string project)
        {
            FirestoreDb db = FirestoreDb.Create(project);
            CollectionReference citiesRef = db.Collection("cities");
            Query chainedQuery = citiesRef
                .WhereEqualTo("State", "CA")
                .WhereLessThan("Population", 1000000);
            QuerySnapshot querySnapshot = await chainedQuery.GetSnapshotAsync();
            foreach (DocumentSnapshot documentSnapshot in querySnapshot.Documents)
            {
                Console.WriteLine("Document {0} returned by query State=CA and Population<1000000", documentSnapshot.Id);
            }
        }

        private static async Task RangeQuery(string project)
        {
            FirestoreDb db = FirestoreDb.Create(project);
            CollectionReference citiesRef = db.Collection("cities");
            Query rangeQuery = citiesRef
                .WhereGreaterThanOrEqualTo("State", "CA")
                .WhereLessThanOrEqualTo("State", "IN");
            QuerySnapshot querySnapshot = await rangeQuery.GetSnapshotAsync();
            foreach (DocumentSnapshot documentSnapshot in querySnapshot.Documents)
            {
                Console.WriteLine("Document {0} returned by query CA<=State<=IN", documentSnapshot.Id);
            }
        }

        private static async Task MultipleInequalitiesQuery(string project)
        {
            FirestoreDb db = FirestoreDb.Create(project);
            FirestoreAdminClient adminClient = FirestoreAdminClient.Create();
            var index = new Google.Cloud.Firestore.Admin.V1.Index
            {
                Fields =
                {
                    new IndexField { FieldPath = "Density", Order = IndexField.Types.Order.Ascending },
                    new IndexField { FieldPath = "Population", Order = IndexField.Types.Order.Ascending }
                },
                QueryScope = QueryScope.Collection
            };

            // We speculatively try to create the index, and just ignore an error of it already existing.
            try
            {
                var lro = await adminClient.CreateIndexAsync(new CollectionGroupName(db.ProjectId, db.DatabaseId, "cities"), index);
                await lro.PollUntilCompletedAsync();
            }
            catch (RpcException ex) when (ex.StatusCode == StatusCode.AlreadyExists)
            {
                // Assume the index is okay.
            }

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
        }

        public static void Main(string[] args)
        {
            if (args.Length < 2)
            {
                Console.Write(Usage);
                return;
            }
            string command = args[0].ToLower();
            string project = string.Join(" ",
                new ArraySegment<string>(args, 1, args.Length - 1));
            switch (command)
            {
                case "query-create-examples":
                    QueryCreateExamples(project).Wait();
                    break;

                case "create-query-state":
                    CreateQueryState(project).Wait();
                    break;

                case "create-query-capital":
                    CreateQueryCapital(project).Wait();
                    break;

                case "simple-queries":
                    SimpleQueries(project).Wait();
                    break;

                case "array-contains-query":
                    ArrayContainsQuery(project).Wait();
                    break;

                case "array-contains-any-query":
                    ArrayContainsAnyQuery(project).Wait();
                    break;

                case "in-query":
                    InQueryWithoutArray(project).Wait();
                    break;

                case "in-query-array":
                    InQueryWithArray(project).Wait();
                    break;

                case "collection-group-query":
                    CollectionGroupQuery(project).Wait();
                    break;

                case "subcollection-query":
                    SubcollectionQuery(project).Wait();
                    break;

                case "chained-query":
                    ChainedQuery(project).Wait();
                    break;

                case "composite-index-chained-query":
                    CompositeIndexChainedQuery(project).Wait();
                    break;

                case "range-query":
                    RangeQuery(project).Wait();
                    break;

                case "multiple-inequalities":
                    MultipleInequalitiesQuery(project).Wait();
                    break;

                default:
                    Console.Write(Usage);
                    return;
            }
        }
    }
}
Program.cs
```

##### Ruby

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
)query_data.rb
```

We can use the simple and compound query described earlier to query a single city's `  landmarks  ` subcollection, but you might also want to retrieve results from every city's `  landmarks  ` subcollection at once.

The `  landmarks  ` collection group consists of all collections with the ID `  landmarks  ` , and you can query it using a collection group query. For example, this collection group query retrieves all `  museum  ` landmarks across all cities:

### Web version 9

``` javascript
import { collectionGroup, query, where, getDocs } from "firebase/firestore";  

const museums = query(collectionGroup(db, 'landmarks'), where('type', '==', 'museum'));
const querySnapshot = await getDocs(museums);
querySnapshot.forEach((doc) => {
    console.log(doc.id, ' => ', doc.data());
});fs_collection_group_query.js
```

### Web version 8

[Learn more](//firebase.google.com/docs/web/learn-more#modular-version) about the tree-shakeable modular Web API and its advantages over the namespaced API.

``` javascript
var museums = db.collectionGroup('landmarks').where('type', '==', 'museum');
museums.get().then((querySnapshot) => {
    querySnapshot.forEach((doc) => {
        console.log(doc.id, ' => ', doc.data());
    });
});test.firestore.js
```

##### Swift

**Note:** This product is not available on watchOS and App Clip targets.

``` swift
db.collectionGroup("landmarks").whereField("type", isEqualTo: "museum").getDocuments { (snapshot, error) in
  // ...
}ViewController.swift
```

##### Objective-C

**Note:** This product is not available on watchOS and App Clip targets.

``` objective-c
[[[self.db collectionGroupWithID:@"landmarks"] queryWhereField:@"type" isEqualTo:@"museum"]
    getDocumentsWithCompletion:^(FIRQuerySnapshot *snapshot, NSError *error) {
    // ...
}];ViewController.m
```

##### Kotlin  
Android

``` kotlin
db.collectionGroup("landmarks").whereEqualTo("type", "museum").get()
    .addOnSuccessListener { queryDocumentSnapshots ->
        // ...
    }DocSnippets.kt
```

##### Java  
Android

``` java
db.collectionGroup("landmarks").whereEqualTo("type", "museum").get()
        .addOnSuccessListener(new OnSuccessListener<QuerySnapshot>() {
            @Override
            public void onSuccess(QuerySnapshot queryDocumentSnapshots) {
                // ...
            }
        });DocSnippets.java
```

### Dart

``` dart
db
    .collectionGroup("landmarks")
    .where("type", isEqualTo: "museum")
    .get()
    .then(
      (res) => print("Successfully completed"),
      onError: (e) => print("Error completing: $e"),
    );firestore.dart
```

##### Java

``` java
final Query museums = db.collectionGroup("landmarks").whereEqualTo("type", "museum");
final ApiFuture<QuerySnapshot> querySnapshot = museums.get();
for (DocumentSnapshot document : querySnapshot.get().getDocuments()) {
  System.out.println(document.getId());
}QueryDataSnippets.java
```

##### Python

``` python
museums = db.collection_group("landmarks").where(
    filter=FieldFilter("type", "==", "museum")
)
docs = museums.stream()
for doc in docs:
    print(f"{doc.id} => {doc.to_dict()}")snippets.py
```

##### Python  
(Async)

``` python
museums = db.collection_group("landmarks").where(
    filter=FieldFilter("type", "==", "museum")
)
docs = museums.stream()
async for doc in docs:
    print(f"{doc.id} => {doc.to_dict()}")snippets.py
```

##### C++

``` text
db->CollectionGroup("landmarks")
.WhereEqualTo("type", FieldValue::String("museum")).Get()
.OnCompletion([](const firebase::Future<QuerySnapshot>& future) {
  if (future.error() == Error::kErrorOk) {
    for (const DocumentSnapshot& document : future.result()->documents()) {
      std::cout << document << std::endl;
    }
  } else {
    std::cout << "Error getting documents: " << future.error_message()
              << std::endl;
  }
});
```

##### Node.js

``` javascript
const querySnapshot = await db.collectionGroup('landmarks').where('type', '==', 'museum').get();
querySnapshot.forEach((doc) => {
  console.log(doc.id, ' => ', doc.data());
});index.js
```

##### Go

``` go
import (
 "context"
 "fmt"
 "io"

 "cloud.google.com/go/firestore"
 "google.golang.org/api/iterator"
)

// collectionGroupQuery runs a collection group query over the data created by
// collectionGroupSetup.
func collectionGroupQuery(w io.Writer, projectID string) error {
 ctx := context.Background()

 client, err := firestore.NewClient(ctx, projectID)
 if err != nil {
     return fmt.Errorf("firestore.NewClient: %w", err)
 }
 defer client.Close()

 it := client.CollectionGroup("landmarks").Where("type", "==", "museum").Documents(ctx)
 for {
     doc, err := it.Next()
     if err == iterator.Done {
         break
     }
     if err != nil {
         return fmt.Errorf("documents iterator: %w", err)
     }
     fmt.Fprintf(w, "%s: %s", doc.Ref.ID, doc.Data()["name"])
 }

 return nil
}
collection_group_query.go
```

##### PHP

``` php
$museums = $db->collectionGroup('landmarks')->where('type', '==', 'museum');
foreach ($museums->documents() as $document) {
    printf('%s => %s' . PHP_EOL, $document->id(), $document->data()['name']);
}query_collection_group_filter_eq.php
```

##### Unity

``` text
Query museums = db.CollectionGroup("landmarks").WhereEqualTo("type", "museum");
museums.GetSnapshotAsync().ContinueWithOnMainThread((querySnapshotTask) =>
{
    foreach (DocumentSnapshot documentSnapshot in querySnapshotTask.Result.Documents)
    {
        Debug.Log(String.Format("Document {0} returned by query State=CA", documentSnapshot.Id));
    } 
});
```

##### C\#

``` csharp
Query museums = db.CollectionGroup("landmarks").WhereEqualTo("Type", "museum");
QuerySnapshot querySnapshot = await museums.GetSnapshotAsync();
foreach (DocumentSnapshot document in querySnapshot.Documents)
{
    Console.WriteLine($"{document.Reference.Path}: {document.GetValue<string>("Name")}");
}Program.cs
```

##### Ruby

``` ruby
museums = firestore.collection_group("landmarks").where("type", "==", "museum")
museums.get do |museum|
  puts "#{museum[:type]} name is #{museum[:name]}."
endquery_data.rb
```

Before using a collection group query, you must create an index that supports your collection group query. [You can create an index through an error message, the console, or the Firebase CLI](/firestore/native/docs/query-data/indexing) .

For the web and mobile SDKs, you must also [create rules that allow your collection group queries](../security/rules-query#secure_and_query_documents_based_on_collection_groups) .

## Explain your query performance

Firestore in Native Mode allows you to measure performance of your queries on the backend and receive detailed performance statistics on backend query execution in return.

Query Explain results help you understand how your queries are executed, showing you inefficiencies and the location of likely server-side bottlenecks.

For more information, see the [guide for Query Explain](../query-explain) .

## Standard edition query limitations

The following list summarizes Firestore query limitations. These limitations apply only to Standard edition:

  - Firestore provides support for logical `  OR  ` queries through the `  or  ` , `  in  ` , and `  array-contains-any  ` operators. These queries are limited to [30 disjunctions based on the query's disjunctive normal form](#limits_on_or_queries) . This limit is fixed and cannot be adjusted.
  - You can use at most one `  array-contains  ` clause per disjunction ( `  or  ` group). You can't combine `  array-contains  ` with `  array-contains-any  ` in the same disjunction.
  - You can't combine `  not-in  ` with `  in  ` , `  array-contains-any  ` , or `  or  ` in the same query.
  - Only a single `  not-in  ` or `  !=  ` is allowed per query.
  - `  not-in  ` supports up to 10 comparison values.
  - The sum of filters, sort orders, and parent document path (1 for a subcollection, 0 for a root collection) in a query cannot exceed 100. This is calculated based on the [disjunctive normal form of the query](#disjunctive_normal_form) .
  - A query with an inequality filter on a field implies ordering by that field and [filters for existence of that field](#orderby_and_existence) .

### Limits on `     OR    ` queries

To prevent a query from becoming too computationally expensive, Firestore Standard edition limits how many `  AND  ` and `  OR  ` clauses you can combine. To apply this limit, Firestore converts queries that perform logical `  OR  ` operations ( `  or  ` , `  in  ` , and `  array-contains-any  ` ) to [disjunctive normal form](https://en.wikipedia.org/wiki/Disjunctive_normal_form) (also known as an `  OR  ` of `  AND  ` s). **Firestore limits a query to a maximum of 30 disjunctions in disjunctive normal form.** This limit is fixed and cannot be adjusted.

#### Disjunctive normal form

Firestore converts queries to disjunctive normal form by applying two rules:

  - ***Flatten***
    
    Given conditions `  A  ` , `  B  ` , and `  C  ` :
    
    `  A and (B and C) => A and B and C  `

  - [***Distributive Law***](https://en.wikipedia.org/wiki/Distributive_property)
    
    Given conditions `  A  ` , `  B  ` , `  C  ` , and `  D  ` :
    
      - `  A and (B or C) => (A and B) or (A and C)  `
      - `  (A or B) and (C or D) => (A and C) or (A and D) or (B and C) or (B and D)  `

When applying these rules to `  in  ` and `  array-contains-any  ` queries, remember that these operators are shorthands for `  OR  ` . For example, `  a in [1,2]  ` is shorthand for `  a = 1 OR a = 2  ` .

**Warning:** Due to the multiplicative nature of conversions to disjunctive normal form, you are more likely to reach the limit when performing an `  AND  ` of multiple `  OR  ` groups.

The following examples show the number of disjunctions for different queries:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Query</th>
<th>Number of disjunctions</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" data-syntax="Text only" data-syntax-guessed="" translate="no"><code>query(collectionRef, where(&quot;a&quot;, &quot;==&quot;, 1))
      </code></pre></td>
<td>1</td>
</tr>
<tr class="even">
<td><pre class="text" dir="ltr" data-is-upgraded="" data-syntax="Text only" data-syntax-guessed="" translate="no"><code>query(collectionRef, or( where(&quot;a&quot;, &quot;==&quot;, 1), where(&quot;b&quot;, &quot;==&quot;, 2) ))
      </code></pre></td>
<td>2</td>
</tr>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" data-syntax="Text only" data-syntax-guessed="" translate="no"><code>query(collectionRef,
        or( and( where(&quot;a&quot;, &quot;==&quot;, 1), where(&quot;c&quot;, &quot;==&quot;, 3) ),
            and( where(&quot;a&quot;, &quot;==&quot;, 1), where(&quot;d&quot;, &quot;==&quot;, 4) ),
            and( where(&quot;b&quot;, &quot;==&quot;, 2), where(&quot;c&quot;, &quot;==&quot;, 3) ),
            and( where(&quot;b&quot;, &quot;==&quot;, 2), where(&quot;d&quot;, &quot;==&quot;, 4) )
        )
      )
      </code></pre></td>
<td>4</td>
</tr>
<tr class="even">
<td><pre class="text" dir="ltr" data-is-upgraded="" data-syntax="Text only" data-syntax-guessed="" translate="no"><code>query(collectionRef,
        and( or( where(&quot;a&quot;, &quot;==&quot;, 1), where(&quot;b&quot;, &quot;==&quot;, 2) ),
             or( where(&quot;c&quot;, &quot;==&quot;, 3), where(&quot;d&quot;, &quot;==&quot;, 4) )
        )
      )
      </code></pre></td>
<td><p>4</p>
<p>The disjunctive normal form of this query is equal to the query above.</p></td>
</tr>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" data-syntax="Text only" data-syntax-guessed="" translate="no"><code>query(collectionRef, where(&quot;a&quot;, &quot;in&quot;, [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]) )
      </code></pre></td>
<td>10</td>
</tr>
<tr class="even">
<td><pre class="text" dir="ltr" data-is-upgraded="" data-syntax="Text only" data-syntax-guessed="" translate="no"><code>query(collectionRef,
        and( where(&quot;a&quot;, &quot;in&quot;, [1, 2, 3, 4, 5]),
             where(&quot;b&quot;, &quot;in&quot;, [1, 2, 3, 4, 5, 6, 7, 8, 9, 10])
        )
      )
      </code></pre></td>
<td><p>50</p>
<p>This query returns an error, because it surpasses the limit of 30 disjunctions.</p></td>
</tr>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" data-syntax="Text only" data-syntax-guessed="" translate="no"><code>query(collectionRef,
        or( where(&quot;a&quot;, &quot;in&quot;, [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]),
            where(&quot;b&quot;, &quot;in&quot;, [1, 2, 3, 4, 5, 6, 7, 8, 9, 10])
        )
      )
      </code></pre></td>
<td>20</td>
</tr>
<tr class="even">
<td><pre class="text" dir="ltr" data-is-upgraded="" data-syntax="Text only" data-syntax-guessed="" translate="no"><code>query(collectionRef,
        and( where(&quot;a&quot;, &quot;in&quot;, [1, 2, 3, 4, 5]),
             or( where(&quot;b&quot;, &quot;==&quot;, 2),
                 where(&quot;c&quot;, &quot;==&quot;, 3)
             )
        )
      )
      </code></pre></td>
<td>10</td>
</tr>
</tbody>
</table>

## `     orderBy    ` and existence

When you order a query by a given field, the query can return only the documents where the order-by field exists.

For example, the following query would not return any documents where the `  population  ` field is not set, even if they otherwise meet the query filters.

##### Java

``` text
db.collection("cities").whereEqualTo("country", “USA”).orderBy(“population”);
```

A related effect applies to inequalities. A query with an inequality filter on a field also implies ordering by that field. The following query does not return documents without a `  population  ` field even if `  country = USA  ` in that document . As a workaround, you can execute separate queries for each ordering or you can assign a value for all fields that you order by.

##### Java

``` text
db.collection(“cities”).where(or(“country”, USA”), greaterThan(“population”, 250000));
```

The query above includes an implied order-by on the inequality and is equivalent to the following:

##### Java

``` text
db.collection(“cities”).where(or(“country”, USA”), greaterThan(“population”, 250000)).orderBy(“population”);
```

## What's next

  - Learn how to [order and limit data in query results](./order-limit-data) .
  - Save reads when you simply want to [count results](./aggregation-queries) .
