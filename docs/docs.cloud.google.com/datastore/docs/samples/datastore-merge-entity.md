Merge datastore entity

## Code sample

### Node.js

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](https://docs.cloud.google.com/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Node.js API reference documentation](https://cloud.google.com/nodejs/docs/reference/datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    async function merge(taskId, description) {
      const taskKey = datastore.key(['Task', taskId]);
      const task = {
        description,
      };
      try {
        await datastore.merge({
          key: taskKey,
          data: task,
        });
        console.log(`Task ${taskId} description updated successfully.`);
      } catch (err) {
        console.error('ERROR:', err);
      }
    }

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](https://docs.cloud.google.com/docs/samples?product=datastore) .
