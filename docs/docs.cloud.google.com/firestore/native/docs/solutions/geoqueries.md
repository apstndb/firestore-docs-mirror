# Geo queries

Many apps have documents that are indexed by physical locations. For example, your app might allow users to browse stores near their current location.

## Solution: Geohashes

Geohash is a system for encoding a `  (latitude, longitude)  ` pair into a single Base32 string. In the Geohash system the world is divided into a rectangular grid. Each character of a Geohash string specifies one of 32 subdivisions of the prefix hash. For example the Geohash `  abcd  ` is one of 32 four-character hashes fully contained within the larger Geohash `  abc  ` .

The longer the shared prefix between two hashes, the closer they are to each other. For example `  abcdef  ` is closer to `  abcdeg  ` than `  abcdff  ` . However the converse is not true\! Two areas may be very close to each other while having very different Geohashes:

We can use Geohashes to store and query documents by position in Firestore with reasonable efficiency while only requiring a single indexed field.

### Install helper library

Creating and parsing Geohashes involves some tricky math, so we created helper libraries to abstract the most difficult parts on Android, Apple, and Web:

### Web version 9

``` text
// Install from NPM. If you prefer to use a static .js file visit
// https://github.com/firebase/geofire-js/releases and download
// geofire-common.min.js from the latest version
npm install --save geofire-common
```

### Web version 8

``` text
// Install from NPM. If you prefer to use a static .js file visit
// https://github.com/firebase/geofire-js/releases and download
// geofire-common.min.js from the latest version
npm install --save geofire-common
```

### Swift

**Note:** This product is not available on watchOS and App Clip targets.

// Add this to your Podfile pod 'GeoFire/Utils'

### Kotlin  
Android

``` text
// Add this to your app/build.gradle
implementation 'com.firebase:geofire-android-common:3.2.0'
```

### Java  
Android

``` text
// Add this to your app/build.gradle
implementation 'com.firebase:geofire-android-common:3.1.0'
```

### Store Geohashes

For each document you want to index by location, you will need to store a Geohash field:

### Web version 9

``` javascript
import { doc, updateDoc } from 'firebase/firestore';

// Compute the GeoHash for a lat/lng point
const lat = 51.5074;
const lng = 0.1278;
const hash = geofire.geohashForLocation([lat, lng]);

// Add the hash and the lat/lng to the document. We will use the hash
// for queries and the lat/lng for distance comparisons.
const londonRef = doc(db, 'cities', 'LON');
await updateDoc(londonRef, {
  geohash: hash,
  lat: lat,
  lng: lng
});fs_geo_add_hash.js
```

### Web version 8

``` javascript
// Compute the GeoHash for a lat/lng point
const lat = 51.5074;
const lng = 0.1278;
const hash = geofire.geohashForLocation([lat, lng]);

// Add the hash and the lat/lng to the document. We will use the hash
// for queries and the lat/lng for distance comparisons.
const londonRef = db.collection('cities').doc('LON');
londonRef.update({
  geohash: hash,
  lat: lat,
  lng: lng
}).then(() => {
  // ...
});test.solution-geoqueries.js
```

### Swift

**Note:** This product is not available on watchOS and App Clip targets.

``` swift
// Compute the GeoHash for a lat/lng point
let latitude = 51.5074
let longitude = 0.12780
let location = CLLocationCoordinate2D(latitude: latitude, longitude: longitude)

let hash = GFUtils.geoHash(forLocation: location)

// Add the hash and the lat/lng to the document. We will use the hash
// for queries and the lat/lng for distance comparisons.
let documentData: [String: Any] = [
  "geohash": hash,
  "lat": latitude,
  "lng": longitude
]

let londonRef = db.collection("cities").document("LON")
londonRef.updateData(documentData) { error in
  // ...
}SolutionGeoPointViewController.swift
```

### Kotlin  
Android

``` kotlin
// Compute the GeoHash for a lat/lng point
val lat = 51.5074
val lng = 0.1278
val hash = GeoFireUtils.getGeoHashForLocation(GeoLocation(lat, lng))

// Add the hash and the lat/lng to the document. We will use the hash
// for queries and the lat/lng for distance comparisons.
val updates: MutableMap<String, Any> = mutableMapOf(
    "geohash" to hash,
    "lat" to lat,
    "lng" to lng,
)
val londonRef = db.collection("cities").document("LON")
londonRef.update(updates)
    .addOnCompleteListener {
        // ...
    }SolutionGeoqueries.kt
```

### Java  
Android

``` java
// Compute the GeoHash for a lat/lng point
double lat = 51.5074;
double lng = 0.1278;
String hash = GeoFireUtils.getGeoHashForLocation(new GeoLocation(lat, lng));

// Add the hash and the lat/lng to the document. We will use the hash
// for queries and the lat/lng for distance comparisons.
Map<String, Object> updates = new HashMap<>();
updates.put("geohash", hash);
updates.put("lat", lat);
updates.put("lng", lng);

DocumentReference londonRef = db.collection("cities").document("LON");
londonRef.update(updates)
        .addOnCompleteListener(new OnCompleteListener<Void>() {
            @Override
            public void onComplete(@NonNull Task<Void> task) {
                // ...
            }
        });SolutionGeoqueries.java
```

### Query Geohashes

Geohashes allow us to approximate area queries by joining a set of queries on the Geohash field and then filtering out some false positives:

### Web version 9

``` javascript
import { collection, query, orderBy, startAt, endAt, getDocs } from 'firebase/firestore';

// Find cities within 50km of London
const center = [51.5074, 0.1278];
const radiusInM = 50 * 1000;

// Each item in 'bounds' represents a startAt/endAt pair. We have to issue
// a separate query for each pair. There can be up to 9 pairs of bounds
// depending on overlap, but in most cases there are 4.
// @ts-ignore
const bounds = geofire.geohashQueryBounds(center, radiusInM);
const promises = [];
for (const b of bounds) {
  const q = query(
    collection(db, 'cities'), 
    orderBy('geohash'), 
    startAt(b[0]), 
    endAt(b[1]));

  promises.push(getDocs(q));
}

// Collect all the query results together into a single list
const snapshots = await Promise.all(promises);

const matchingDocs = [];
for (const snap of snapshots) {
  for (const doc of snap.docs) {
    const lat = doc.get('lat');
    const lng = doc.get('lng');

    // We have to filter out a few false positives due to GeoHash
    // accuracy, but most will match
    // @ts-ignore
    const distanceInKm = geofire.distanceBetween([lat, lng], center);
    const distanceInM = distanceInKm * 1000;
    if (distanceInM <= radiusInM) {
      matchingDocs.push(doc);
    }
  }
}fs_geo_query_hashes.js
```

### Web version 8

``` javascript
// Find cities within 50km of London
const center = [51.5074, 0.1278];
const radiusInM = 50 * 1000;

// Each item in 'bounds' represents a startAt/endAt pair. We have to issue
// a separate query for each pair. There can be up to 9 pairs of bounds
// depending on overlap, but in most cases there are 4.
const bounds = geofire.geohashQueryBounds(center, radiusInM);
const promises = [];
for (const b of bounds) {
  const q = db.collection('cities')
    .orderBy('geohash')
    .startAt(b[0])
    .endAt(b[1]);

  promises.push(q.get());
}

// Collect all the query results together into a single list
Promise.all(promises).then((snapshots) => {
  const matchingDocs = [];

  for (const snap of snapshots) {
    for (const doc of snap.docs) {
      const lat = doc.get('lat');
      const lng = doc.get('lng');

      // We have to filter out a few false positives due to GeoHash
      // accuracy, but most will match
      const distanceInKm = geofire.distanceBetween([lat, lng], center);
      const distanceInM = distanceInKm * 1000;
      if (distanceInM <= radiusInM) {
        matchingDocs.push(doc);
      }
    }
  }

  return matchingDocs;
}).then((matchingDocs) => {
  // Process the matching documents
  // ...
});
test.solution-geoqueries.js
```

### Swift

**Note:** This product is not available on watchOS and App Clip targets.

``` swift
// Find cities within 50km of London
let center = CLLocationCoordinate2D(latitude: 51.5074, longitude: 0.1278)
let radiusInM: Double = 50 * 1000

// Each item in 'bounds' represents a startAt/endAt pair. We have to issue
// a separate query for each pair. There can be up to 9 pairs of bounds
// depending on overlap, but in most cases there are 4.
let queryBounds = GFUtils.queryBounds(forLocation: center,
                                      withRadius: radiusInM)
let queries = queryBounds.map { bound -> Query in
  return db.collection("cities")
    .order(by: "geohash")
    .start(at: [bound.startValue])
    .end(at: [bound.endValue])
}

@Sendable func fetchMatchingDocs(from query: Query,
                       center: CLLocationCoordinate2D,
                       radiusInMeters: Double) async throws -> [QueryDocumentSnapshot] {
  let snapshot = try await query.getDocuments()
  // Collect all the query results together into a single list
  return snapshot.documents.filter { document in
    let lat = document.data()["lat"] as? Double ?? 0
    let lng = document.data()["lng"] as? Double ?? 0
    let coordinates = CLLocation(latitude: lat, longitude: lng)
    let centerPoint = CLLocation(latitude: center.latitude, longitude: center.longitude)

    // We have to filter out a few false positives due to GeoHash accuracy, but
    // most will match
    let distance = GFUtils.distance(from: centerPoint, to: coordinates)
    return distance <= radiusInM
  }
}

// After all callbacks have executed, matchingDocs contains the result. Note that this code
// executes all queries serially, which may not be optimal for performance.
do {
  let matchingDocs = try await withThrowingTaskGroup(of: [QueryDocumentSnapshot].self) { group -> [QueryDocumentSnapshot] in
    for query in queries {
      group.addTask {
        try await fetchMatchingDocs(from: query, center: center, radiusInMeters: radiusInM)
      }
    }
    var matchingDocs = [QueryDocumentSnapshot]()
    for try await documents in group {
      matchingDocs.append(contentsOf: documents)
    }
    return matchingDocs
  }

  print("Docs matching geoquery: \(matchingDocs)")
} catch {
  print("Unable to fetch snapshot data. \(error)")
}SolutionGeoPointViewController.swift
```

### Kotlin  
Android

``` kotlin
// Find cities within 50km of London
val center = GeoLocation(51.5074, 0.1278)
val radiusInM = 50.0 * 1000.0

// Each item in 'bounds' represents a startAt/endAt pair. We have to issue
// a separate query for each pair. There can be up to 9 pairs of bounds
// depending on overlap, but in most cases there are 4.
val bounds = GeoFireUtils.getGeoHashQueryBounds(center, radiusInM)
val tasks: MutableList<Task<QuerySnapshot>> = ArrayList()
for (b in bounds) {
    val q = db.collection("cities")
        .orderBy("geohash")
        .startAt(b.startHash)
        .endAt(b.endHash)
    tasks.add(q.get())
}

// Collect all the query results together into a single list
Tasks.whenAllComplete(tasks)
    .addOnCompleteListener {
        val matchingDocs: MutableList<DocumentSnapshot> = ArrayList()
        for (task in tasks) {
            val snap = task.result
            for (doc in snap!!.documents) {
                val lat = doc.getDouble("lat")!!
                val lng = doc.getDouble("lng")!!

                // We have to filter out a few false positives due to GeoHash
                // accuracy, but most will match
                val docLocation = GeoLocation(lat, lng)
                val distanceInM = GeoFireUtils.getDistanceBetween(docLocation, center)
                if (distanceInM <= radiusInM) {
                    matchingDocs.add(doc)
                }
            }
        }

        // matchingDocs contains the results
        // ...
    }SolutionGeoqueries.kt
```

### Java  
Android

``` java
// Find cities within 50km of London
final GeoLocation center = new GeoLocation(51.5074, 0.1278);
final double radiusInM = 50 * 1000;

// Each item in 'bounds' represents a startAt/endAt pair. We have to issue
// a separate query for each pair. There can be up to 9 pairs of bounds
// depending on overlap, but in most cases there are 4.
List<GeoQueryBounds> bounds = GeoFireUtils.getGeoHashQueryBounds(center, radiusInM);
final List<Task<QuerySnapshot>> tasks = new ArrayList<>();
for (GeoQueryBounds b : bounds) {
    Query q = db.collection("cities")
            .orderBy("geohash")
            .startAt(b.startHash)
            .endAt(b.endHash);

    tasks.add(q.get());
}

// Collect all the query results together into a single list
Tasks.whenAllComplete(tasks)
        .addOnCompleteListener(new OnCompleteListener<List<Task<?>>>() {
            @Override
            public void onComplete(@NonNull Task<List<Task<?>>> t) {
                List<DocumentSnapshot> matchingDocs = new ArrayList<>();

                for (Task<QuerySnapshot> task : tasks) {
                    QuerySnapshot snap = task.getResult();
                    for (DocumentSnapshot doc : snap.getDocuments()) {
                        double lat = doc.getDouble("lat");
                        double lng = doc.getDouble("lng");

                        // We have to filter out a few false positives due to GeoHash
                        // accuracy, but most will match
                        GeoLocation docLocation = new GeoLocation(lat, lng);
                        double distanceInM = GeoFireUtils.getDistanceBetween(docLocation, center);
                        if (distanceInM <= radiusInM) {
                            matchingDocs.add(doc);
                        }
                    }
                }

                // matchingDocs contains the results
                // ...
            }
        });SolutionGeoqueries.java
```

## Limitations

Using Geohashes for querying locations gives us new capabilities, but comes with its own set of limitations:

  - **False Positives** - querying by Geohash is not exact, and you have to filter out false-positive results on the client side. These extra reads add cost and latency to your app.
  - **Edge Cases** - this query method relies on estimating the distance between lines of longitude/latitude. The accuracy of this estimate decreases as points get closer to the North or South Pole which means Geohash queries have more false positives at extreme latitudes.
