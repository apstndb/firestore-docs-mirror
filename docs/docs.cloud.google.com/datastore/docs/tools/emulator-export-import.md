Using the import and export features of the Datastore emulator, you can export data from your database instance and load it into the emulator. You can also export data from the emulator and load it into your Datastore mode database.

## Before you begin

Before you use the import or export features of the Datastore emulator, complete the following:

  - [Start the Datastore emulator.](/datastore/docs/tools/datastore-emulator)
    
    The import and export features are available for `  cloud-datastore-emulator  ` versions 2.1.0 and greater. You may need to [update your Google Cloud CLI components](/sdk/docs/components#updating_components) .

  - For import operations, make sure your entity export files are on the same machine as the emulator.

## Import entities into the emulator

The emulator's import feature lets you load entities from a set of entity export files into the emulator. The entity export files can come from an export of your Datastore mode database or of an emulator instance.

To import entities into the emulator, send a `  POST  ` import request to the emulator. You can use [curl](https://curl.haxx.se/) or a similar tool. For example, the following request will import all entities from a set of entity export files into the emulator:

### Protocol

``` bash
curl -X POST localhost:8081/v1/projects/[PROJECT_ID]:import \
-H 'Content-Type: application/json' \
-d '{"input_url":"[ENTITY_EXPORT_FILES]"}'
```

Modify `  localhost:8081  ` if the emulator uses a different port.

where:

  - `  [PROJECT_ID]  ` is the ID of your project.

  - `  [ENTITY_EXPORT_FILES]  ` is the path to the `  overall_export_metadata  ` file of your entity export files. For example:
    
    `  {"input_url":"/home/user/myexports/2019-02-04T19:39:33_443/2019-02-04T19:39:33_443.overall_export_metadata"}  `

### Import entities from specific kinds and namespaces

You can specify an entity filter to import entities from only specific kinds or namespaces. You can specify an entity filter only if the export was created using an entity filter.

Specify kinds or namespaces in an entity filter:

### Protocol

``` bash
curl -X POST localhost:8081/v1/projects/[PROJECT_ID]:import \
-H 'Content-Type: application/json' \
-d '{"input_url":"[ENTITY_EXPORT_FILES]",
"entity_filter":{"kinds":[[KIND_NAMES]], "namespace_ids":[[NAMESPACES]]}}'
```

Modify `  localhost:8081  ` if the emulator uses a different port.

where:

  - `  [PROJECT_ID]  ` is the ID of your project.

  - `  [ENTITY_EXPORT_FILES]  ` is the path to the `  overall_export_metadata  ` file of your entity export files. For example:
    
    `  {"input_url":"/home/user/myexports/2019-02-04T19:39:33_443/2019-02-04T19:39:33_443.overall_export_metadata"}  `

  - `  [KIND_NAMES]  ` is a list of kinds: `  "kinds":["KIND_1", "KIND_2"]  `

  - `  [NAMESPACES]  ` is a list of namespace IDs:
    
    `  "namespace_ids":["NAMESPACE_1", "NAMESPACE_2"]  `

## Export entities in the emulator

The emulator's export feature lets you save entities in the emulator into a set of entity export files. You can then use an import operation to load the entities in the entity export files into your Datastore mode database or into an emulator instance.

To export entities in an emulator instance, send a `  POST  ` export request to the emulator. You can use [curl](https://curl.haxx.se/) or a similar tool. For example, the following request will export all entities in the emulator:

### Protocol

``` bash
curl -X POST localhost:8081/v1/projects/[PROJECT_ID]:export \
-H 'Content-Type: application/json' \
-d '{"output_url_prefix":"EXPORT_DIRECTORY"}'
```

Modify `  localhost:8081  ` if the emulator uses a different port.

where:

  - `  [PROJECT_ID]  ` is the ID of your project.

  - `  [EXPORT_DIRECTORY]  ` specifies the directory where the emulator saves the entity export files. This directory must not already contain a set of entity export files. For example:
    
    `  {"output_url_prefix":"/home/user/myexports/2019-02-04/"}  `

**Note:** If you intend to use an entity filter when importing entities from your entity export files, you must [specify an entity filter in your export operation](#export-with-entity-filter) .

<span id="export-with-entity-filter"></span>

### Export entities from specific kinds and namespaces

You can specify an entity filter to export entities from only specific kinds or namespaces.

Specify kinds or namespaces in an entity filter:

### Protocol

``` bash
curl -X POST localhost:8081/v1/projects/[PROJECT_ID]:export \
-H 'Content-Type: application/json' \
-d '{"output_url_prefix":"EXPORT_DIRECTORY",
"entity_filter":{"kinds":[[KIND_NAMES]], "namespace_ids":[[NAMESPACES]]}}'
```

Modify `  localhost:8081  ` if the emulator uses a different port.

where:

  - `  [PROJECT_ID]  ` is the ID of your project.

  - `  [EXPORT_DIRECTORY]  ` specifies the directory where the emulator saves the entity export files. This directory must not already contain a set of entity export files. For example:
    
    {"output\_url\_prefix":"/home/user/myexports/2019-02-04/"}\`\`

  - `  [KIND_NAMES]  ` is a list of kinds: `  "kinds":["KIND_1", "KIND_2"]  `

  - `  [NAMESPACES]  ` is a list of namespace IDs:
    
    `  "namespace_ids":["NAMESPACE_1", "NAMESPACE_2"]  `

### Load emulator data into your database

Entity export files created by the emulator are compatible with the managed import feature for Datastore mode databases.

<span id="export-with-entity-filter">Before you can load entities exported from the emulator into your database, you must</span> [upload your entity export files to a Cloud Storage bucket](/storage/docs/uploading-objects) . The managed import feature reads only from Cloud Storage buckets.

Once your entity export files are available in a Cloud Storage bucket, you can import the data into your database as described in [Exporting and importing entities](/datastore/docs/export-import-entities) .
