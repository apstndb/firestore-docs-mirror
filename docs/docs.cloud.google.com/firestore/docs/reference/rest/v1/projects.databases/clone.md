Creates a new database by cloning an existing one.

The new database must be in the same cloud region or multi-region location as the existing database. This behaves similar to `  FirestoreAdmin.CreateDatabase  ` except instead of creating a new empty database, a new database is created with the database type, index configuration, and documents from an existing database.

The `  long-running operation  ` can be used to track the progress of the clone, with the Operation's `  metadata  ` field type being the `  CloneDatabaseMetadata  ` . The `  response  ` type is the `  Database  ` if the clone was successful. The new database is not readable or writeable until the LRO has completed.

### HTTP request

Choose a location:

global

africa-south1

asia-east1

asia-east2

asia-northeast1

asia-northeast2

asia-northeast3

asia-south1

asia-south2

asia-southeast1

asia-southeast2

asia-southeast3

australia-southeast1

australia-southeast2

europe-central2

europe-north1

europe-north2

europe-southwest1

europe-west1

europe-west10

europe-west12

europe-west2

europe-west3

europe-west4

europe-west6

europe-west8

europe-west9

me-central1

me-central2

me-west1

northamerica-northeast1

northamerica-northeast2

northamerica-south1

southamerica-east1

southamerica-west1

us-central1

us-east1

us-east4

us-east5

us-south1

us-west1

us-west2

us-west3

us-west4

eu

us

  
`  POST https://firestore.googleapis.com/v1/{parent=projects/*}/databases:clone  `

The URLs use [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`  parent  `

`  string  `

Required. The project to clone the database in. Format is `  projects/{projectId}  ` .

### Request body

The request body contains data with the following structure:

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;databaseId&quot;: string,
  &quot;pitrSnapshot&quot;: {
    object (PitrSnapshot)
  },
  &quot;encryptionConfig&quot;: {
    object (EncryptionConfig)
  },
  &quot;tags&quot;: {
    string: string,
    ...
  }
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  databaseId  `

`  string  `

Required. The ID to use for the database, which will become the final component of the database's resource name. This database ID must not be associated with an existing database.

This value should be 4-63 characters. Valid characters are /\[a-z\]\[0-9\]-/ with first character a letter and the last a letter or a number. Must not be UUID-like /\[0-9a-f\]{8}(-\[0-9a-f\]{4}){3}-\[0-9a-f\]{12}/.

"(default)" database ID is also valid if the database is Standard edition.

`  pitrSnapshot  `

`  object ( PitrSnapshot  ` )

Required. Specification of the PITR data to clone from. The source database must exist.

The cloned database will be created in the same location as the source database.

`  encryptionConfig  `

`  object ( EncryptionConfig  ` )

Optional. Encryption configuration for the cloned database.

If this field is not specified, the cloned database will use the same encryption configuration as the source database, namely `  useSourceEncryption  ` .

`  tags  `

`  map (key: string, value: string)  `

Optional. Immutable. Tags to be bound to the cloned database.

The tags should be provided in the format of `  tagKeys/{tag_key_id} -> tagValues/{tag_value_id}  ` .

An object containing a list of `  "key": value  ` pairs. Example: `  { "name": "wrench", "mass": "1.3kg", "count": "3" }  ` .

### Response body

If successful, the response body contains an instance of `  Operation  ` .

### Authorization scopes

Requires one of the following OAuth scopes:

  - `  https://www.googleapis.com/auth/datastore  `
  - `  https://www.googleapis.com/auth/cloud-platform  `

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .
