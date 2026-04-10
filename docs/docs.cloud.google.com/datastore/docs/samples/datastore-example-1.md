Datastore Example showing setup

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Local Unit Testing for Go](https://docs.cloud.google.com/appengine/docs/legacy/standard/go111/tools/localunittesting)
  - [Local Unit Testing for Python 2](https://docs.cloud.google.com/appengine/docs/legacy/standard/python/tools/localunittesting)

## Code sample

### Go

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](https://docs.cloud.google.com/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Go API reference documentation](https://cloud.google.com/go/docs/reference/cloud.google.com/go/datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    func TestWithdrawLowBal(t *testing.T) {
     ctx, done, err := aetest.NewContext()
     if err != nil {
         t.Fatal(err)
     }
     defer done()
     key := datastore.NewKey(ctx, "BankAccount", "", 1, nil)
     if _, err := datastore.Put(ctx, key, &BankAccount{100}); err != nil {
         t.Fatal(err)
     }
    
     err = withdraw(ctx, "myid", 128, 0)
     if err == nil || err.Error() != "insufficient funds" {
         t.Errorf("Error: %v; want insufficient funds error", err)
     }
    
     b := BankAccount{}
     if err := datastore.Get(ctx, key, &b); err != nil {
         t.Fatal(err)
     }
     if bal, want := b.Balance, 100; bal != want {
         t.Errorf("Balance %d, want %d", bal, want)
     }
    }

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](https://docs.cloud.google.com/docs/samples?product=datastore) .
