Incrementing a Firestore document field while using shards

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Distributed counters](https://firebase.google.com/docs/firestore/solutions/counters)
  - [Support frequent and distributed counters](/firestore/native/docs/solutions/counters)

## Code sample

### C\#

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
/// <summary>
/// Increment a randomly picked shard by 1.
/// </summary>
/// <param name="docRef">The document reference <see cref="DocumentReference"/></param>
/// <returns>The <see cref="Task"/></returns>
private static async Task IncrementCounterAsync(DocumentReference docRef, int numOfShards)
{
    int documentId;
    lock (s_randLock)
    {
        documentId = s_rand.Next(numOfShards);
    }
    var shardRef = docRef.Collection("shards").Document(documentId.ToString());
    await shardRef.UpdateAsync("count", FieldValue.Increment(1));
}
```

### Go

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` go
// incrementCounter increments a randomly picked shard.
func (c *Counter) incrementCounter(ctx context.Context, docRef *firestore.DocumentRef) (*firestore.WriteResult, error) {
 docID := strconv.Itoa(rand.Intn(c.numShards))

 shardRef := docRef.Collection("shards").Doc(docID)
 return shardRef.Update(ctx, []firestore.Update{
     {Path: "Count", Value: firestore.Increment(1)},
 })
}
```

### Node.js

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` javascript
function incrementCounter(docRef, numShards) {
  const shardId = Math.floor(Math.random() * numShards);
  const shardRef = docRef.collection('shards').doc(shardId.toString());
  return shardRef.set({count: FieldValue.increment(1)}, {merge: true});
}
```

### PHP

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
$ref = $db->collection('samples/php/distributedCounters');
$numShards = 0;
$docCollection = $ref->documents();
foreach ($docCollection as $doc) {
    $numShards++;
}
$shardIdx = random_int(0, max(1, $numShards) - 1);
$doc = $ref->document((string) $shardIdx);
$doc->update([
    ['path' => 'Cnt', 'value' => FieldValue::increment(1)]
]);
```

### Python

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
def increment_counter(self, doc_ref):
    """Increment a randomly picked shard."""
    doc_id = random.randint(0, self._num_shards - 1)

    shard_ref = doc_ref.collection("shards").document(str(doc_id))
    return shard_ref.update({"count": firestore.Increment(1)})
```

### Ruby

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
# project_id = "Your Google Cloud Project ID"
# num_shards = "Number of shards for distributed counter"
# collection_path = "shards"

require "google/cloud/firestore"

firestore = Google::Cloud::Firestore.new project_id: project_id

# Select a shard of the counter at random
shard_id = rand 0...num_shards
shard_ref = firestore.doc "#{collection_path}/#{shard_id}"

# increment counter
shard_ref.update({ count: firestore.field_increment(1) })

puts "Counter incremented."
```

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](/docs/samples?product=firestore) .
