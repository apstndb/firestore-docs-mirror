Query a collection group using a partitioned query

## Code sample

### Go

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` go
cities := client.CollectionGroup("cities")

// Get a partioned query for the cities collection group, with a maximum
// partition count of 10
partitionedQueries, err := cities.GetPartitionedQueries(ctx, 10)
if err != nil {
 return fmt.Errorf("GetPartitionedQueries: %w", err)
}

fmt.Printf("Collection Group query partitioned to %d queries\n", len(partitionedQueries))

// Retrieve the first query and iterate over the documents contained.
query := partitionedQueries[0]
iter := query.Documents(ctx)
for {
 doc, err := iter.Next()
 if err == iterator.Done {
     break
 }
 if err != nil {
     return fmt.Errorf("documents iterator: %w", err)
 }
 fmt.Println(doc.Data())
}
```

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](/docs/samples?product=firestore) .
