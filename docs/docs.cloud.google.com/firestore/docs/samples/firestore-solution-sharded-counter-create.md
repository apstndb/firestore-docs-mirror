Create a Firestore sharded counter

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Distributed counters](https://firebase.google.com/docs/firestore/solutions/counters)
  - [Support frequent and distributed counters](/firestore/native/docs/solutions/counters)

## Code sample

### C\#

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
/// <summary>
/// Create a given number of shards as a
/// subcollection of specified document.
/// </summary>
/// <param name="docRef">The document reference <see cref="DocumentReference"/></param>
private static async Task CreateCounterAsync(DocumentReference docRef, int numOfShards)
{
    CollectionReference colRef = docRef.Collection("shards");
    var tasks = new List<Task>();
    // Initialize each shard with Count=0
    for (var i = 0; i < numOfShards; i++)
    {
        tasks.Add(colRef.Document(i.ToString()).SetAsync(new Shard() { Count = 0 }));
    }
    await Task.WhenAll(tasks);
}
```

### Go

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` go
// initCounter creates a given number of shards as
// subcollection of specified document.
func (c *Counter) initCounter(ctx context.Context, docRef *firestore.DocumentRef) error {
 colRef := docRef.Collection("shards")

 // Initialize each shard with count=0
 for num := 0; num < c.numShards; num++ {
     shard := Shard{0}

     if _, err := colRef.Doc(strconv.Itoa(num)).Set(ctx, shard); err != nil {
         return fmt.Errorf("Set: %w", err)
     }
 }
 return nil
}
```

### PHP

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
$numShards = 10;
$ref = $db->collection('samples/php/distributedCounters');
for ($i = 0; $i < $numShards; $i++) {
    $doc = $ref->document((string) $i);
    $doc->set(['Cnt' => 0]);
}
```

### Python

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
def init_counter(self, doc_ref):
    """
    Create a given number of shards as
    subcollection of specified document.
    """
    col_ref = doc_ref.collection("shards")

    # Initialize each shard with count=0
    for num in range(self._num_shards):
        shard = Shard()
        col_ref.document(str(num)).set(shard.to_dict())
```

### Ruby

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
# project_id = "Your Google Cloud Project ID"
# num_shards = "Number of shards for distributed counter"
# collection_path = "shards"

require "google/cloud/firestore"

firestore = Google::Cloud::Firestore.new project_id: project_id

shards_ref = firestore.col collection_path

# Initialize each shard with count=0
num_shards.times do |i|
  shards_ref.doc(i).set({ count: 0 })
end

puts "Distributed counter shards collection created."
```

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](/docs/samples?product=firestore) .
