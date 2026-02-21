You can use [Eventarc](/eventarc/docs/overview) and Firestore in Datastore mode to build event-driven architectures. Firestore in Datastore mode provides triggers for Eventarc that generate events from changes to a particular entity in your database. The trigger can route events to a [supported destination](/eventarc/docs/event-providers-targets) :

  - [Cloud Run functions (2nd gen)](/datastore/docs/extend-with-functions-2nd-gen)
  - [Cloud Run](/eventarc/docs/run/route-trigger-cloud-firestore)
  - [Google Kubernetes Engine](/eventarc/docs/gke/route-trigger-cloud-firestore)
  - [Workflows](/eventarc/docs/workflows/route-trigger-cloud-firestore)

Eventarc offers a standardized solution to manage the flow of state changes, called *events* , between decoupled microservices. When triggered, Eventarc routes these events to various destinations while managing delivery, security, authorization, observability, and error-handling for you.

**Note:** Eventarc events use the [`  CloudEvents  `](https://cloudevents.io/) specification.

## Example use cases

An event-driven architecture is a system design pattern where services react to changes in state known as events. You can use this pattern alongside the scalability of Firestore to add more features to your app. For example, you might add the following capabilities:

  - Interoperability between different technology stacks
    
    Replicate your data and transform it before sending it to an analytics system.

  - Parallel processing
    
    Fan out operations for parallel processing. If you have multiple systems that operate based on entity changes, you can use the push-based streams in each consumer and route the event to multiple consumers.

  - Push-based event streams
    
    Build push-based messaging designs. Clients can receive notifications without needing to poll remote services. Without the polling latency, you can better perform on-the-fly data processing and real-time analysis.

  - State monitoring and alerting
    
    Use an event-driven architecture to add custom metrics to your database operations. Monitor and receive alerts on changes and updates. Detect anomalies.

## Limitations

Note the following limitations for Datastore mode triggers for Eventarc:

  - Ordering is not guaranteed. Rapid changes can trigger events in an unexpected order.

  - Events are delivered *at least* once.
    
    Make sure your event handler is idempotent and avoid producing unexpected results or side effects when an event is delivered more than once. Refer to [Building idempotent functions](https://cloud.google.com/blog/products/serverless/cloud-functions-pro-tips-building-idempotent-functions) to learn more.

  - A trigger is associated with a single database. You cannot create a trigger that matches multiple databases.

  - Deleting a database does not automatically delete any triggers for that database. The trigger stops delivering events but continues to exist until you [delete the trigger](/eventarc/docs/managing-triggers#trigger-delete) .

## Eventarc and Firestore in Datastore mode locations

Eventarc does not support multi-regions for Firestore event triggers, but you can still create triggers for Firestore databases in multi-region locations. Eventarc maps Firestore multi-region locations to the following Eventarc regions:

<table>
<thead>
<tr class="header">
<th>Firestore multi-region</th>
<th>Eventarc region</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       nam5      </code></td>
<td><code dir="ltr" translate="no">       us-central1      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       eur3      </code></td>
<td><code dir="ltr" translate="no">       europe-west4      </code></td>
</tr>
</tbody>
</table>

## Datastore mode and Native mode event interoperability

Eventarc supports event triggers for both Datastore mode and Native mode. These event triggers are interoperable with both database types. A Firestore in Native mode database can receive Datastore events, and a Firestore in Datastore mode database can receive Native mode events.

Event interoperability lets you share Eventarc code across Firestore databases of different types.

### Event conversions

If you apply a Native mode event trigger to a Datastore mode database, Eventarc makes the following conversions:

  - The namespace of the entity is stored in the event's `  PartitionId  ` attribute.
  - Embedded entities are converted to Native mode `  map  ` types.

## What's next

  - Learn about [event-driven architectures](/eventarc/docs/event-driven-architectures) .
