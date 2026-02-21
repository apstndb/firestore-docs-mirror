Query a Firestore collection with a cursor start at field (multiple) filter

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Paginate data with query cursors](/firestore/native/docs/query-data/query-cursors)
  - [Paginate data with query cursors](https://firebase.google.com/docs/firestore/query-data/query-cursors)

## Code sample

### C\#

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
Query query1 = db.Collection("cities").OrderBy("Name").OrderBy("State").StartAt("Springfield");
Query query2 = db.Collection("cities").OrderBy("Name").OrderBy("State").StartAt("Springfield", "Missouri");
```

### Go

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` go
// Will return all Springfields.
client.Collection("cities").
 OrderBy("name", firestore.Asc).
 OrderBy("state", firestore.Asc).
 StartAt("Springfield")

// Will return Springfields where state comes after Wisconsin.
client.Collection("cities").
 OrderBy("name", firestore.Asc).
 OrderBy("state", firestore.Asc).
 StartAt("Springfield", "Wisconsin")
```

### Java

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
// Will return all Springfields
Query query1 = db.collection("cities").orderBy("name").orderBy("state").startAt("Springfield");

// Will return "Springfield, Missouri" and "Springfield, Wisconsin"
Query query2 =
    db.collection("cities").orderBy("name").orderBy("state").startAt("Springfield", "Missouri");
```

### Node.js

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` javascript
// Will return all Springfields
const startAtNameRes = await db.collection('cities')
  .orderBy('name')
  .orderBy('state')
  .startAt('Springfield')
  .get();

// Will return 'Springfield, Missouri' and 'Springfield, Wisconsin'
const startAtNameAndStateRes = await db.collection('cities')
  .orderBy('name')
  .orderBy('state')
  .startAt('Springfield', 'Missouri')
  .get();
```

### PHP

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
// Will return all Springfields
$query1 = $db
    ->collection('samples/php/cities')
    ->orderBy('name')
    ->orderBy('state')
    ->startAt(['Springfield']);

// Will return "Springfield, Missouri" and "Springfield, Wisconsin"
$query2 = $db
    ->collection('samples/php/cities')
    ->orderBy('name')
    ->orderBy('state')
    ->startAt(['Springfield', 'Missouri']);
```

### Python

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
start_at_name = (
    db.collection("cities").order_by("name").start_at({"name": "Springfield"})
)

start_at_name_and_state = (
    db.collection("cities")
    .order_by("name")
    .order_by("state")
    .start_at({"name": "Springfield", "state": "Missouri"})
)
```

### Ruby

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
# Will return all Springfields
query1 = firestore.col(collection_path).order("name").order("state").start_at("Springfield")

# Will return "Springfield, Missouri" and "Springfield, Wisconsin"
query2 = firestore.col(collection_path).order("name").order("state").start_at(["Springfield", "Missouri"])
```

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](/docs/samples?product=firestore) .
