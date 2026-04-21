# Use geo queries

> **Preview**
> 
> This product or feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA products and features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

Use geospatial queries in MongoDB compatible operations to query documents that exist within a certain range from a specific longitude and latitude.

## Before you begin

1.  Ensure that you have access to an existing MongoDB compatible operations database, or [Create a database and connect to it](https://firebase.google.com/docs/firestore/enterprise/create-and-query-database) .

2.  Ensure that you have at least one 2dsphere index, or [Create a 2dsphere index](https://docs.cloud.google.com/firestore/mongodb-compatibility/docs/indexing#create-2dsphere-index) .

### GeoJSON objects

To run a geospatial query against fields in your collection, the fields you query must be [GeoJSON objects](https://geojson.org/) or [GeoPoints](https://docs.cloud.google.com/java/docs/reference/google-cloud-firestore/latest/com.google.cloud.firestore.GeoPoint) .

## Run a geospatial query

You can perform a geospatial query using the `$near` operator, which calculates the distance of a geo point relative to geo points within documents. These documents are then sorted from nearest to farthest distance in the query results. You can also override this sort order by defining a secondary sort, other than `$natural` , in your query. The `$near` operator must exist in a document field in the query filter, and must contain a `$geometry` GeoJSON field.

In the following example, the `$near` operator is used to calculate the distance between the geo point `(-122.084, 37.4221)` and the geo points located in the `location` field of all documents in `myCollection.` The documents are returned and ordered by nearest to farthest distance between the two points.

``` 
  db.myCollection.find({
    location: {
      $near: {
        $geometry: {
          type: 'Point',
          coordinates: [ -122.084, 37.4221 ]
        }
      }
    }
  }
  )
```

You can also use the optional `$maxDistance` and `$minDistance` fields to control the distance in meters from the point of your query. The following example shows a query where returned documents must be at least 500 meters and at most 2000 meters from the point `(-122.084, 37.4221)` :

``` 
  db.myCollection.find({
    location: {
      $near: {
        $geometry: {
          type: 'Point',
          coordinates: [ -122.084, 37.4221 ]
        },
        $maxDistance: 2000,
        $minDistance: 500
      }
    }
  }
```

If your index is partitioned, then you can filter based on the partition by including the partition in an "and" equality filter within your query. For example, if you had a `region` partition and wanted to filter your query results by the `midwest` region, you could do the following:

``` 
  db.myCollection.find( { $and: [
    { location:
      { $near: {
        $geometry: {
          type: 'Point',
          coordinates: [ -122.084, 37.4221 ]
        },
      }
    },
    { "region": "midwest" }
  ] } )
```

The value of your partition must be a string. Your partition filter must be joined to your search query by an `$and` operator.

## Limitations

  - `$near` operators and `$text` operators can't be used in the same the query.
  - `$near` can't be nested in a multi-clause `$or` statement unless `$near` is the only expression in the `$or` clause.
  - `$near` can't be used with the `$not` or `$nor` operators in a query.
  - `$near` isn't supported in aggregation queries.
