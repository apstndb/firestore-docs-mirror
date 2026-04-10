Getting a Firestore document while using shards

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Distributed counters](https://firebase.google.com/docs/firestore/solutions/counters)
  - [Support frequent and distributed counters](https://docs.cloud.google.com/firestore/native/docs/solutions/counters)

## Code sample

### C\#

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    /// <summary>
    /// Get total count across all shards.
    /// </summary>
    /// <param name="docRef">The document reference <see cref="DocumentReference"/></param>
    /// <returns>The <see cref="int"/></returns>
    private static async Task<int> GetCountAsync(DocumentReference docRef)
    {
        var snapshotList = await docRef.Collection("shards").GetSnapshotAsync();
        return snapshotList.Sum(shard => shard.GetValue<int>("count"));
    }

### Go

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    // getCount returns a total count across all shards.
    func (c *Counter) getCount(ctx context.Context, docRef *firestore.DocumentRef) (int64, error) {
     var total int64
     shards := docRef.Collection("shards").Documents(ctx)
     for {
         doc, err := shards.Next()
         if err == iterator.Done {
             break
         }
         if err != nil {
             return 0, fmt.Errorf("Next: %w", err)
         }
    
         vTotal := doc.Data()["Count"]
         shardCount, ok := vTotal.(int64)
         if !ok {
             return 0, fmt.Errorf("firestore: invalid dataType %T, want int64", vTotal)
         }
         total += shardCount
     }
     return total, nil
    }

### Node.js

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    async function getCount(docRef) {
      const querySnapshot = await docRef.collection('shards').get();
      const documents = querySnapshot.docs;
    
      let count = 0;
      for (const doc of documents) {
        count += doc.get('count');
      }
      return count;
    }

### PHP

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    $result = 0;
    $docCollection = $db->collection('samples/php/distributedCounters')->documents();
    foreach ($docCollection as $doc) {
        $result += $doc->data()['Cnt'];
    }

### Python

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    def get_count(self, doc_ref):
        """Return a total count across all shards."""
        total = 0
        shards = doc_ref.collection("shards").list_documents()
        for shard in shards:
            total += shard.get().to_dict().get("count", 0)
        return total

### Ruby

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    # project_id = "Your Google Cloud Project ID"
    # collection_path = "shards"
    
    require "google/cloud/firestore"
    
    firestore = Google::Cloud::Firestore.new project_id: project_id
    
    shards_ref = firestore.col_group collection_path
    
    count = 0
    shards_ref.get do |doc_ref|
      count += doc_ref[:count]
    end
    
    puts "Count value is #{count}."

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](https://docs.cloud.google.com/docs/samples?product=firestore) .
