---
name: documents/docs.cloud.google.com/firestore/docs/samples/firestore-query-order-with-filter
uri: https://docs.cloud.google.com/firestore/docs/samples/firestore-query-order-with-filter
title: Ordering a Firestore query with a filter
description: Ordering a Firestore query with a filter
data_source: docs.cloud.google.com
---

Ordering a Firestore query with a filter

## Code sample

### C#

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

```csharp
Query query = citiesRef
    .WhereGreaterThan("Population", 2500000)
    .OrderBy("Population");
```

### Go

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

```go
query := cities.Where("population", ">", 2500000).OrderBy("population", firestore.Asc)
```

### Java

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

```java
Query query = cities.whereGreaterThan("population", 2500000L).orderBy("population");
```

### Node.js

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

```javascript
citiesRef.where('population', '>', 2500000).orderBy('population');
```

### PHP

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

```php
$query = $citiesRef
    ->where('population', '>', 2500000)
    ->orderBy('population');
```

### Python

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

```python
cities_ref = db.collection("cities")
query = cities_ref.where(filter=FieldFilter("population", ">", 2500000)).order_by(
    "population"
)
results = query.stream()
```

### Ruby

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

```ruby
query = cities_ref.where("population", ">", 2_500_000).order("population")
```

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](https://docs.cloud.google.com/docs/samples?product=firestore) .
