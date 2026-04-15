Add a Firestore document using a custom type

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Add and update data](https://docs.cloud.google.com/firestore/native/docs/manage-data/add-data)

## Code sample

### C\#

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    DocumentReference docRef = db.Collection("cities").Document("LA");
    City city = new City
    {
        Name = "Los Angeles",
        State = "CA",
        Country = "USA",
        Capital = false,
        Population = 3900000L
    };
    await docRef.SetAsync(city);

### Go

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    import (
     "context"
     "log"
    
     "cloud.google.com/go/firestore"
    )
    
    func addDocAsEntity(ctx context.Context, client *firestore.Client) error {
     city := City{
         Name:    "Los Angeles",
         Country: "USA",
     }
     _, err := client.Collection("cities").Doc("LA").Set(ctx, city)
     if err != nil {
         // Handle any errors in an appropriate way, such as returning them.
         log.Printf("An error has occurred: %s", err)
     }
    
     return err
    }

### Java

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    City city =
        new City("Los Angeles", "CA", "USA", false, 3900000L, Arrays.asList("west_coast", "socal"));
    ApiFuture<WriteResult> future = db.collection("cities").document("LA").set(city);
    // block on response if required
    System.out.println("Update time : " + future.get().getUpdateTime());

### Python

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    city = City(name="Los Angeles", state="CA", country="USA")
    db.collection("cities").document("LA").set(city.to_dict())

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](https://docs.cloud.google.com/docs/samples?product=firestore) .
