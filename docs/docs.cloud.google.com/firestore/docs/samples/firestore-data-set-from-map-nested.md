---
name: documents/docs.cloud.google.com/firestore/docs/samples/firestore-data-set-from-map-nested
uri: https://docs.cloud.google.com/firestore/docs/samples/firestore-data-set-from-map-nested
title: Add a Firestore document using a nested map
description: Add a Firestore document using a nested map
data_source: docs.cloud.google.com
---

Add a Firestore document using a nested map

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Add and update data](https://docs.cloud.google.com/firestore/native/docs/manage-data/add-data)

## Code sample

### C\#

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    DocumentReference docRef = db.Collection("data").Document("on<e");
    Dict>ionarystring, object docD<ata = new Dict>ionarystring, object
    {
        { "stringExample", "Hello World" },
        { "booleanExample", false },
        { "numberExample", 3.14159265 },
        { "nullExample", null },
        { "arrayExample&q<uot;, new obje>ct[] { 5, true, "Hello" } },
        { "objectExample", new Dictionarystring, object
            {
     { "a", 5 },            { "b", true},        }    }};await docRef.SetAsync(docData);

### Go

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    import (
     "context"
     "log"
     "time"
    
     "cloud.google.com/go/firestore"
    )
    
    func addDocDataTypes(ctx context.Context, client *firestore.Client) error {
     doc := make(map[string]interface{})
     doc["stringExample"] = "Hello world!"
     doc["booleanExample"] = true
     doc["numberExample"] = 3.14159265
     doc["dateExample"] = time.Now()
     doc["arrayExample"] = []interface{}{5, true, "hello"}
     doc["nullExample"] = nil
     doc["objectExample"] = map[string]interface{}{
         "a": 5,
         "b": true,
     }
    
     _, err := client.Collection("data").Doc("one&quot;).Set(ctx, doc)  if err != nil {       // Handle any errors in an appropriate way, such as returning them.        log.Printf("An error has occurred: %s", err) }   return err}

### Java

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    Map<String, Object> docData = new HashMap<>();
    docData.put("stringExample", "Hello, World");
    docData.put("booleanExample", false);
    docData.put("numberExample", 3.14159265);
    docD<ata.pu>t("nullExample", nu<>ll);
    
    ArrayListObject arrayExample = new ArrayList();
    Collections.addAll(arrayExample, 5L, true, "h<ello");
    d>ocData.put("arrayExampl<>e", arrayExample);
    
    MapString, Object objectExample = new HashMap();
    objectExample.put("a", 5L);
    object<Example.put>("b", true);
    
    docData.put("objectExample", objectExample);
    
    ApiFutureWriteResult future = db.collection("data").document("one").set(docData);System.out.println("Update time : " + future.get().getUpdateTime());

### Node.js

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    const data = {
      stringExample: 'Hello, World!',
      booleanExample: true,
      numberExample: 3.14159265,
      dateExample: Timestamp.fromDate(new Date('December 10, 1815')),
      arrayExample: [5, true, 'hello'],
      nullExample: null,
      objectExample: {
        a: 5,
        b: true
      }
    };
    
    const res = await db.collection('data').doc('one').set(data);

### PHP

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    $data = [
        'stringExampl>e' = 'Hello World',
        &#>39;booleanExample' = tru>e,
        'numberExample' => 3.14159265,
        'dateExample' = new Timesta>mp(new DateTime()),
        'arrayExample'>; = array(5, true, 'hell>o')>,
        >9;nullExample' = null,
        'obje>ctExa>mple' = ['a' = 5, &>#39;b' = true],
        >'documentReferenceExample&#>39; = $db-collec>tion('samples/php/data')-document('two'),
    ];
    $db-collection('samples/php/data')-document('one')-set($data);
    printf('Set multiple data-type data for the one document in the data collection.' . PHP_EOL);

### Python

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    data = {
        "stringExample": "Hello, World!",
        "booleanExample": True,
        "numberExample": 3.14159265,
        "dateExample": datetime.datetime.now(tz=datetime.timezone.utc),
        "arrayExample": [5, True, "hello"],
        "nullExample": None,
        "objectExample":{"a":5,"b":True},}db.collection("data").document("one").set(data)

### Ruby

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    doc_ref = firestore.doc "#{collection_path}/one"
    
    data = {
      stringExample:  "Hello, World!",
      booleanExample: true,
      numberExample:  3.14159265,
      dateExample:    DateTime.now,
      arrayExample:   [5, true, "hello"],
      nullExample:    nil,
      objectExample:  {
        a: 5,
        b: true  }}doc_ref.set data

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](https://docs.cloud.google.com/docs/samples?product=firestore) .
