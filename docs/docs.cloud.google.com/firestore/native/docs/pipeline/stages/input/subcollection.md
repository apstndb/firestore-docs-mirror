# Subcollection (Input Stage)

**Preview — Firestore in Native mode (with Pipeline Operations) for Enterprise Edition**

This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](/terms/service-terms#1) . You can process personal data for this feature as outlined in the [Cloud Data Processing Addendum](/terms/data-processing-addendum) , subject to the obligations and restrictions described in the agreement under which you access Google Cloud. Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

## Description

The `  subcollection(...)  ` input stage makes it easy to perform parent-child joins using the built-in `  __name__  ` field.

Additional stages can be chained onto the `  subcollection(...)  ` stage to perform filtering or aggregation over the nested documents. Note that any field references used in subsequent stages refer to the documents from the nested collection, not the parent document. To refer to fields in the parent scope, first use the `  let  ` stage to define variables, then reference those variables in the local scope.

## Examples

### Node.js

``` text
db.pipeline()
  .collection("/restaurants")
  .add_fields(subcollection("reviews")
    .aggregate(average("rating").as("avg_rating"))
    .toScalarExpression()
    .as("avg_rating"))
```

## Behavior

The `  subcollection(...)  ` stage must be used within the context of a sub-pipeline. It uses the `  __name__  ` (the document reference) of the current document in the parent scope to determine which sub-collection to fetch. For example, if the parent document is `  /restaurants/pizza-place  ` , then `  subcollection("reviews")  ` returns all documents from the `  /restaurants/pizza-place/reviews  ` collection.

If the document reference has been renamed, or it is not possible to define a field with `  __name__  ` then manually writing the join like:

### Node.js

``` text
db.pipeline()
  .collection("/restaurants")
  .let(field("__name__").as("restaurant_name"))
  .add_fields(db.pipeline()
    .collectionGroup("reviews")
    .where(field("__name__").parent().equals(variable("restaurant_name")))
    .aggregate(average("rating").as("avg_rating"))
    .toScalarExpression()
    .as("avg_rating"))
```

is still possible as fundamentally this stage is just syntactic sugar over this more complex join format.

For the following documents:

### Node.js

``` text
const restaurant1 = db.collection("restaurants").document("pizza-place");
const restaurant2 = db.collection("restaurants").document("urban-bite");
const restaurant3 = db.collection("restaurants").document("nacho-house");

await restaurant1.create({ name: "Pizza Place" });
await restaurant2.create({ name: "Urban Bite" });
await restaurant3.create({ name: "Nacho House" });

await restaurant1.collection("reviews").doc("1").create({ rating: 5 });
await restaurant1.collection("reviews").doc("1").create({ rating: 2 });

await restaurant2.collection("reviews").doc("1").create({ rating: 3 });
await restaurant2.collection("reviews").doc("1").create({ rating: 4 });
await restaurant2.collection("reviews").doc("1").create({ rating: 5 });
```

The following query retrieves each restaurant and summarizes its reviews in a new `  review_summary  ` field:

### Node.js

``` text
const results = await db.pipeline()
  .collectionGroup("restaurants")
  .add_fields(subcollection("reviews")
    .aggregate(
      countAll().as("review_count"),
      average("rating").as("avg_rating"))
    .asScalarExpression()
    .as("review_summary"))
  .execute();
```

and produces the following results:

``` text
{ name: "Pizza Place", review_summary: { review_count: 2, avg_rating: 3.5 } },
{ name: "Urban Bite",  review_summary: { review_count: 3, avg_rating: 4.0 } },
{ name: "Nacho House", review_summary: { review_count: 0, avg_rating: null } },
```
