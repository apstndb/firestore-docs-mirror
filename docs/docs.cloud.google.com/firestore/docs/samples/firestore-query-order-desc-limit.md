Ordering and limiting Firestore queries in descending order

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Order and limit data](https://docs.cloud.google.com/firestore/native/docs/query-data/order-limit-data)
  - [Order and limit data with Cloud Firestore](https://firebase.google.com/docs/firestore/query-data/order-limit-data)

## Code sample

### C\#

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    Query query = citiesRef.OrderByDescending("Name").Limit(3);

### Go

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    query := cities.OrderBy("name", firestore.Desc).Limit(3)

### Java

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    Query query = cities.orderBy("name", Direction.DESCENDING).limit(3);

### Node.js

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    const lastThreeRes = await citiesRef.orderBy('name', 'desc').limit(3).get();

### PHP

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    $query = $citiesRef->orderBy('name', 'DESC')->limit(3);

### Python

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    cities_ref = db.collection("cities")
    query = cities_ref.order_by("name", direction=firestore.Query.DESCENDING).limit(3)
    results = query.stream()

### Ruby

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    query = cities_ref.order("name", "desc").limit(3)

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](https://docs.cloud.google.com/docs/samples?product=firestore) .
