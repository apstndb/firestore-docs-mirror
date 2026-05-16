---
name: documents/docs.cloud.google.com/datastore/docs/samples/datastore-admin-entities-export
uri: https://docs.cloud.google.com/datastore/docs/samples/datastore-admin-entities-export
title: Export a copy of all or a subset of entities
description: Exports a copy of all or a subset of entities from Datastore to another storage system, such as Cloud Storage.
data_source: docs.cloud.google.com
---

Exports a copy of all or a subset of entities from Datastore to another storage system, such as Cloud Storage.

## Code sample

### C\#

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](https://docs.cloud.google.com/datastore/docs/reference/libraries) . For more information, see the [Datastore mode C\# API reference documentation](https://cloud.google.com/dotnet/docs/reference/Google.Cloud.Datastore.V1/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    using Google.Cloud.Datastore.Admin.V1;
    using System;
    using System.Collections.Generic;
    
    public class ExportEntitiesSample
    {
        public string ExportEntities(
            string projectId = "your-project-id",
            string outputUrlPrefix = "gs://your-bucket-name",
            string kind = "Task",
            string namespaceId = "default")
        {
            // Create client
            DatastoreAdminClient datastoreAdminClient = DatastoreAdminClient.Create();
    
            IDictionary<string, string> labels = new Dictionary<string, string> { { "cloud_datastore_samples", "true" }, };
            EntityFilter entityFilter = new EntityFilter
            {
                Kinds = { kind },
                NamespaceIds = { namespaceId }
            };
    
            var response = datastoreAdminClient.ExportEntities(projectId, labels, entityFilter, outputUrlPrefix);
    
            // Poll until the returned long-running operation is complete
            var completedResponse = response.PollUntilCompleted();
    
            if (completedResponse.IsFaulted)
            {
                Console.WriteLine($"Error while Exporting Entities: {completedResponse.Exception}");
                throw completedResponse.Exception;
            }
    
            Console.WriteLine($"Entities exported successfully.");
    
            ExportEntitiesResponse result = completedResponse.Result;
    
            return result.OutputUrl;
        }
    }

### Go

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](https://docs.cloud.google.com/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Go API reference documentation](https://cloud.google.com/go/docs/reference/cloud.google.com/go/datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    import (
     "context"
     "fmt"
     "io"
    
     admin "cloud.google.com/go/datastore/admin/apiv1"
     "cloud.google.com/go/datastore/admin/apiv1/adminpb"
    )
    
    // entitiesExport exports a copy of all or a subset of entities from
    // Datastore to another storage system, such as Cloud Storage.
    func entitiesExport(w io.Writer, projectID, outputURLPrefix string) (*adminpb.ExportEntitiesResponse, error) {
     // projectID := "project-id"
     // outputURLPrefix := "gs://bucket-name"
     ctx := context.Background()
     client, err := admin.NewDatastoreAdminClient(ctx)
     if err != nil {
         return nil, fmt.Errorf("admin.NewDatastoreAdminClient: %w", err)
     }
     defer client.Close()
    
     req := &adminpb.ExportEntitiesRequest{
         ProjectId:       projectID,
         OutputUrlPrefix: outputURLPrefix,
     }
     op, err := client.ExportEntities(ctx, req)
     if err != nil {
         return nil, fmt.Errorf("ExportEntities: %w", err)
     }
     resp, err := op.Wait(ctx)
     if err != nil {
         return nil, fmt.Errorf("Wait: %w", err)
     }
     fmt.Fprintln(w, "Entities were exported")
     return resp, nil
    }

### Python

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](https://docs.cloud.google.com/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Python API reference documentation](https://cloud.google.com/python/docs/reference/datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    def export_entities(project_id, output_url_prefix):
        """
        Exports a copy of all or a subset of entities from
        Datastore to another storage system, such as Cloud Storage.
        """
        # project_id = "project-id"
        # output_url_prefix = "gs://bucket-name"
        client = DatastoreAdminClient()
    
        op = client.export_entities(
            {"project_id": project_id, "output_url_prefix": output_url_prefix}
        )
        response = op.result(timeout=300)
    
        print("Entities were exported\n")
        return response

### Ruby

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](https://docs.cloud.google.com/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Ruby API reference documentation](https://docs.cloud.google.com/ruby/docs/reference/google-cloud-datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    # project_id = "project-id"
    # output_url_prefix = "gs://bucket-name"
    op = client.export_entities project_id: project_id, output_url_prefix: output_url_prefix
    
    op.wait_until_done!
    raise op.error.message if op.error?
    
    response = op.response
    # Process the response.
    
    metadata = op.metadata
    # Process the metadata.
    
    puts "Entities were exported"

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](https://docs.cloud.google.com/docs/samples?product=datastore) .
