# Write-time aggregations

**Tip:** This page applies to the Core operations interface. To aggregate data in the Pipeline operations interface for Enterprise edition, see [Pipeline operation `  aggregate  ` stage](/firestore/native/docs/pipeline/overview#aggregate_distinct) .

Queries in Firestore let you find documents in large collections. To gain insight into properties of the collection as a whole, you can aggregate data over a collection.

You can aggregate data either at read-time or at write time:

  - **Read-time aggregations** calculate a result at the time of the request. Firestore supports the `  count()  ` , `  sum()  ` , and `  average()  ` aggregation queries at read-time. Read-time aggregation queries are are easier to add to your app than write-time aggregations. For more on aggregation queries, see [Summarize data with aggregation queries](../query-data/aggregation-queries) .

  - **Write-time aggregations** calculate a result each time the app performs a relevant write operation. Write-time aggregations are more work to implement, but you might use them instead of read-time aggregations for one of the following reasons:
    
      - You want to listen to the aggregation result for real-time updates. The `  count()  ` , `  sum()  ` , and `  average()  ` aggregation queries do not support real-time updates.
      - You want to store the aggregation result in a client-side cache. The `  count()  ` , `  sum()  ` , and `  average()  ` aggregation queries do not support caching.
      - You are aggregating data from tens of thousands of documents for each of your users and consider costs. At a lower number of documents, read-time aggregations cost less. For a large number of documents in an aggregations, write-time aggregations might cost less.

You can implement a write-time aggregation using either a client-side transaction or with Cloud Run functions. The following sections describe how to implement write-time aggregations.

## Solution: Write-time aggregation with a client-side transaction

Consider a local recommendations app that helps users find great restaurants. The following query retrieves all the ratings for a given restaurant:

### Web

``` javascript
db.collection("restaurants")
  .doc("arinell-pizza")
  .collection("ratings")
  .get();test.solution-aggregation.js
```

### Swift

**Note:** This product is not available on watchOS and App Clip targets.

``` swift
do {
  let snapshot = try await db.collection("restaurants")
    .document("arinell-pizza")
    .collection("ratings")
    .getDocuments()
  print(snapshot)
} catch {
  print(error)
}SolutionAggregationViewController.swift
```

### Objective-C

**Note:** This product is not available on watchOS and App Clip targets.

``` objective-c
FIRQuery *query = [[[self.db collectionWithPath:@"restaurants"]
    documentWithPath:@"arinell-pizza"] collectionWithPath:@"ratings"];
[query getDocumentsWithCompletion:^(FIRQuerySnapshot * _Nullable snapshot,
                                    NSError * _Nullable error) {
  // ...
}];FIRSolutionAggregationViewController.m
```

### Kotlin  
Android

``` kotlin
db.collection("restaurants")
    .document("arinell-pizza")
    .collection("ratings")
    .get()SolutionAggregation.kt
```

### Java  
Android

``` java
db.collection("restaurants")
        .document("arinell-pizza")
        .collection("ratings")
        .get();SolutionAggregation.java
```

Rather than fetching all ratings and then computing aggregate information, we can store this information on the restaurant document itself:

### Web

``` javascript
var arinellDoc = {
  name: 'Arinell Pizza',
  avgRating: 4.65,
  numRatings: 683
};test.solution-aggregation.js
```

### Swift

**Note:** This product is not available on watchOS and App Clip targets.

``` swift
struct Restaurant {

  let name: String
  let avgRating: Float
  let numRatings: Int

}

let arinell = Restaurant(name: "Arinell Pizza", avgRating: 4.65, numRatings: 683)SolutionAggregationViewController.swift
```

### Objective-C

**Note:** This product is not available on watchOS and App Clip targets.

``` objective-c
@interface FIRRestaurant : NSObject

@property (nonatomic, readonly) NSString *name;
@property (nonatomic, readonly) float averageRating;
@property (nonatomic, readonly) NSInteger ratingCount;

- (instancetype)initWithName:(NSString *)name
               averageRating:(float)averageRating
                 ratingCount:(NSInteger)ratingCount;

@end

@implementation FIRRestaurant

- (instancetype)initWithName:(NSString *)name
               averageRating:(float)averageRating
                 ratingCount:(NSInteger)ratingCount {
  self = [super init];
  if (self != nil) {
    _name = name;
    _averageRating = averageRating;
    _ratingCount = ratingCount;
  }
  return self;
}

@endFIRSolutionAggregationViewController.m
```

### Kotlin  
Android

``` kotlin
data class Restaurant(
    // default values required for use with "toObject"
    internal var name: String = "",
    internal var avgRating: Double = 0.0,
    internal var numRatings: Int = 0,
)
```

``` kotlin
val arinell = Restaurant("Arinell Pizza", 4.65, 683)SolutionAggregation.kt
```

### Java  
Android

``` java
public class Restaurant {
    String name;
    double avgRating;
    int numRatings;

    public Restaurant(String name, double avgRating, int numRatings) {
        this.name = name;
        this.avgRating = avgRating;
        this.numRatings = numRatings;
    }
}
```

``` java
Restaurant arinell = new Restaurant("Arinell Pizza", 4.65, 683);SolutionAggregation.java
```

In order to keep these aggregations consistent, they must be updated each time a new rating is added to the subcollection. One way to achieve consistency is to perform the add and the update in a single transaction:

### Web

``` javascript
function addRating(restaurantRef, rating) {
    // Create a reference for a new rating, for use inside the transaction
    var ratingRef = restaurantRef.collection('ratings').doc();

    // In a transaction, add the new rating and update the aggregate totals
    return db.runTransaction((transaction) => {
        return transaction.get(restaurantRef).then((res) => {
            if (!res.exists) {
                throw "Document does not exist!";
            }

            // Compute new number of ratings
            var newNumRatings = res.data().numRatings + 1;

            // Compute new average rating
            var oldRatingTotal = res.data().avgRating * res.data().numRatings;
            var newAvgRating = (oldRatingTotal + rating) / newNumRatings;

            // Commit to Firestore
            transaction.update(restaurantRef, {
                numRatings: newNumRatings,
                avgRating: newAvgRating
            });
            transaction.set(ratingRef, { rating: rating });
        });
    });
}test.firestore.js
```

### Swift

**Note:** This product is not available on watchOS and App Clip targets.

``` swift
func addRatingTransaction(restaurantRef: DocumentReference, rating: Float) async {
  let ratingRef: DocumentReference = restaurantRef.collection("ratings").document()

  do {
    let _ = try await db.runTransaction({ (transaction, errorPointer) -> Any? in
      do {
        let restaurantDocument = try transaction.getDocument(restaurantRef).data()
        guard var restaurantData = restaurantDocument else { return nil }

        // Compute new number of ratings
        let numRatings = restaurantData["numRatings"] as! Int
        let newNumRatings = numRatings + 1

        // Compute new average rating
        let avgRating = restaurantData["avgRating"] as! Float
        let oldRatingTotal = avgRating * Float(numRatings)
        let newAvgRating = (oldRatingTotal + rating) / Float(newNumRatings)

        // Set new restaurant info
        restaurantData["numRatings"] = newNumRatings
        restaurantData["avgRating"] = newAvgRating

        // Commit to Firestore
        transaction.setData(restaurantData, forDocument: restaurantRef)
        transaction.setData(["rating": rating], forDocument: ratingRef)
      } catch {
        // Error getting restaurant data
        // ...
      }

      return nil
    })
  } catch {
    // ...
  }
}SolutionAggregationViewController.swift
```

### Objective-C

**Note:** This product is not available on watchOS and App Clip targets.

``` objective-c
- (void)addRatingTransactionWithRestaurantReference:(FIRDocumentReference *)restaurant
                                             rating:(float)rating {
  FIRDocumentReference *ratingReference =
      [[restaurant collectionWithPath:@"ratings"] documentWithAutoID];

  [self.db runTransactionWithBlock:^id (FIRTransaction *transaction,
                                        NSError **errorPointer) {
    FIRDocumentSnapshot *restaurantSnapshot =
        [transaction getDocument:restaurant error:errorPointer];

    if (restaurantSnapshot == nil) {
      return nil;
    }

    NSMutableDictionary *restaurantData = [restaurantSnapshot.data mutableCopy];
    if (restaurantData == nil) {
      return nil;
    }

    // Compute new number of ratings
    NSInteger ratingCount = [restaurantData[@"numRatings"] integerValue];
    NSInteger newRatingCount = ratingCount + 1;

    // Compute new average rating
    float averageRating = [restaurantData[@"avgRating"] floatValue];
    float newAverageRating = (averageRating * ratingCount + rating) / newRatingCount;

    // Set new restaurant info

    restaurantData[@"numRatings"] = @(newRatingCount);
    restaurantData[@"avgRating"] = @(newAverageRating);

    // Commit to Firestore
    [transaction setData:restaurantData forDocument:restaurant];
    [transaction setData:@{@"rating": @(rating)} forDocument:ratingReference];
    return nil;
  } completion:^(id  _Nullable result, NSError * _Nullable error) {
    // ...
  }];
}FIRSolutionAggregationViewController.m
```

### Kotlin  
Android

``` kotlin
private fun addRating(restaurantRef: DocumentReference, rating: Float): Task<Void> {
    // Create reference for new rating, for use inside the transaction
    val ratingRef = restaurantRef.collection("ratings").document()

    // In a transaction, add the new rating and update the aggregate totals
    return db.runTransaction { transaction ->
        val restaurant = transaction.get(restaurantRef).toObject<Restaurant>()!!

        // Compute new number of ratings
        val newNumRatings = restaurant.numRatings + 1

        // Compute new average rating
        val oldRatingTotal = restaurant.avgRating * restaurant.numRatings
        val newAvgRating = (oldRatingTotal + rating) / newNumRatings

        // Set new restaurant info
        restaurant.numRatings = newNumRatings
        restaurant.avgRating = newAvgRating

        // Update restaurant
        transaction.set(restaurantRef, restaurant)

        // Update rating
        val data = hashMapOf<String, Any>(
            "rating" to rating,
        )
        transaction.set(ratingRef, data, SetOptions.merge())

        null
    }
}SolutionAggregation.kt
```

### Java  
Android

``` java
private Task<Void> addRating(final DocumentReference restaurantRef, final float rating) {
    // Create reference for new rating, for use inside the transaction
    final DocumentReference ratingRef = restaurantRef.collection("ratings").document();

    // In a transaction, add the new rating and update the aggregate totals
    return db.runTransaction(new Transaction.Function<Void>() {
        @Override
        public Void apply(@NonNull Transaction transaction) throws FirebaseFirestoreException {
            Restaurant restaurant = transaction.get(restaurantRef).toObject(Restaurant.class);

            // Compute new number of ratings
            int newNumRatings = restaurant.numRatings + 1;

            // Compute new average rating
            double oldRatingTotal = restaurant.avgRating * restaurant.numRatings;
            double newAvgRating = (oldRatingTotal + rating) / newNumRatings;

            // Set new restaurant info
            restaurant.numRatings = newNumRatings;
            restaurant.avgRating = newAvgRating;

            // Update restaurant
            transaction.set(restaurantRef, restaurant);

            // Update rating
            Map<String, Object> data = new HashMap<>();
            data.put("rating", rating);
            transaction.set(ratingRef, data, SetOptions.merge());

            return null;
        }
    });
}SolutionAggregation.java
```

Using a transaction keeps your aggregate data consistent with the underlying collection. To read more about transactions in Firestore, see [Transactions and Batched Writes](../manage-data/transactions) .

## Limitations

The solution shown above demonstrates aggregating data using the Firestore client library, but you should be aware of the following limitations:

  - **Security** - Client-side transactions require giving clients permission to update the aggregate data in your database. While you can reduce the risks of this approach by writing advanced security rules, this may not be appropriate in all situations.
  - **Offline support** - Client-side transactions will fail when the user's device is offline, which means you need to handle this case in your app and retry at the appropriate time.
  - **Performance** - If your transaction contains multiple read, write, and update operations, it could require multiple requests to the Firestore backend. On a mobile device, this could take significant time.
  - **Write rates** - this solution may not work for frequently updated aggregations because Cloud Firestore documents can only be updated at most once per second. Additionally, If a transaction reads a document that was modified outside of the transaction, it [retries a finite number of times](https://firebase.google.com/docs/firestore/manage-data/transactions#transactions) and then fails. Check out [distributed counters](https://firebase.google.com/docs/firestore/solutions/counters) for a relevant workaround for aggregations which need more frequent updates.

## Solution: Write-time aggregation with Cloud Functions

If client-side transactions are not suitable for your application, you can use a [Cloud Function](../extend-with-functions) to update the aggregate information each time a new rating is added to a restaurant:

### Node.js

``` javascript
exports.aggregateRatings = functions.firestore
    .document('restaurants/{restId}/ratings/{ratingId}')
    .onWrite(async (change, context) => {
      // Get value of the newly added rating
      const ratingVal = change.after.data().rating;

      // Get a reference to the restaurant
      const restRef = db.collection('restaurants').doc(context.params.restId);

      // Update aggregations in a transaction
      await db.runTransaction(async (transaction) => {
        const restDoc = await transaction.get(restRef);

        // Compute new number of ratings
        const newNumRatings = restDoc.data().numRatings + 1;

        // Compute new average rating
        const oldRatingTotal = restDoc.data().avgRating * restDoc.data().numRatings;
        const newAvgRating = (oldRatingTotal + ratingVal) / newNumRatings;

        // Update restaurant info
        transaction.update(restRef, {
          avgRating: newAvgRating,
          numRatings: newNumRatings
        });
      });
    });index.js
```

This solution offloads the work from the client to a hosted function, which means your mobile app can add ratings without waiting for a transaction to complete. Code executed in a Cloud Function is not bound by security rules, which means you no longer need to give clients write access to the aggregate data.

## Limitations

Using a Cloud Function for aggregations avoids some of the issues with client-side transactions, but comes with a different set of limitations:

  - **Cost** - Each rating added will cause a Cloud Function invocation, which may increase your costs. For more information, see the Cloud Functions [pricing page](https://cloud.google.com/functions/pricing) .
  - **Latency** - By offloading the aggregation work to a Cloud Function, your app will not see updated data until the Cloud Function has finished executing and the client has been notified of the new data. Depending on the speed of your Cloud Function, this could take longer than executing the transaction locally.
  - **Write rates** - this solution may not work for frequently updated aggregations because Cloud Firestore documents can only be updated at most once per second. Additionally, If a transaction reads a document that was modified outside of the transaction, it [retries a finite number of times](https://firebase.google.com/docs/firestore/manage-data/transactions#transactions) and then fails. Check out [distributed counters](https://firebase.google.com/docs/firestore/solutions/counters) for a relevant workaround for aggregations which need more frequent updates.
