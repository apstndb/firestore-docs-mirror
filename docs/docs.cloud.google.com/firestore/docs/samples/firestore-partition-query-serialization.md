Serialize a Firestore query for execution elsewhere

## Code sample

### Go

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` go
cities := client.CollectionGroup("cities")

// Get a partioned query for the cities collection group, with a maximum
// partition count of 10
partitionedQueries, err := cities.GetPartitionedQueries(ctx, 10)
if err != nil {
 return err
}

fmt.Printf("Collection Group query partitioned to %d queries\n", len(partitionedQueries))

query := partitionedQueries[0]

// Serialize a query created by GetPartitionedQueries
bytes, err := query.Serialize()
if err != nil {
 return fmt.Errorf("Serialize: %w", err)
}

// Deserialize a query created by Query.Serialize
deserializedQuery, err := client.CollectionGroup("").Deserialize(bytes)
if err != nil {
 return fmt.Errorf("Deserialize: %w", err)
}
```

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](/docs/samples?product=firestore) .
