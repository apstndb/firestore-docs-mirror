# Create event-driven architectures with Eventarc

You can use [Eventarc](/eventarc/docs/overview) and Firestore with MongoDB compatibility to build [event-driven architectures](/eventarc/docs/event-driven-architectures) . Firestore with MongoDB compatibility triggers for Eventarc generate events from changes to a particular documents in your database. The trigger can route events to a [supported destination](/eventarc/docs/event-providers-targets) :

  - Cloud Run functions (2nd gen) which supports the [Cloud Client Libraries](/firestore/docs/extend-with-functions-2nd-gen) and the [Firebase SDK](https://firebase.google.com/docs/firestore/extend-with-functions-2nd-gen)
  - [Cloud Run](/eventarc/docs/run/route-trigger-cloud-firestore)
  - [Google Kubernetes Engine](/eventarc/docs/gke/route-trigger-cloud-firestore)
  - [Workflows](/eventarc/docs/workflows/route-trigger-cloud-firestore)

Eventarc offers a standardized solution to manage the flow of state changes, called *events* , between decoupled microservices. When triggered, Eventarc routes these events to various destinations while managing delivery, security, authorization, observability, and error-handling for you.

**Note:** Eventarc events use the [`  CloudEvents  `](https://cloudevents.io/) specification.

## Limitations

Note the following limitations for Firestore with MongoDB compatibility triggers for Eventarc:

  - Ordering is not guaranteed. Rapid changes can trigger events in an unexpected order.

  - Events are delivered *at least* once.
    
    Make sure your event handler is idempotent and avoid producing unexpected results or side effects when an event is delivered more than once. Refer to [Building idempotent functions](https://cloud.google.com/blog/products/serverless/cloud-functions-pro-tips-building-idempotent-functions) to learn more.

  - A trigger is associated with a single database. You cannot create a trigger that matches multiple databases.

  - Deleting a database does not automatically delete any triggers for that database. The trigger stops delivering events but continues to exist until you [delete the trigger](/eventarc/docs/managing-triggers#trigger-delete) . If the database is recreated, any associated triggers will also need to be deleted and recreated to restore event delivery.

  - Firestore with MongoDB compatibility supports Cloud Run functions (2nd gen) and doesn't support Cloud Run functions (1st gen).

  - Firestore Enterprise edition databases do not support Datastore entity event types.

## What's next

  - Learn about [event-driven architectures](/eventarc/docs/event-driven-architectures) .
