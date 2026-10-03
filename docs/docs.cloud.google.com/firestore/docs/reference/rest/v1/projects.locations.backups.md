---
name: documents/docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.locations.backups
uri: https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.locations.backups
title: 'REST Resource: projects.locations.backups'
description: A cloud-hosted NoSQL database that's simple enough for rapid prototyping yet scalable and flexible enough to grow to any size.
data_source: docs.cloud.google.com
---

## Resource: Backup

A Backup of a Cloud Firestore Database.

The backup contains all documents and index configurations for the given database at a specific point in time.

**JSON representation**

```
{
  "name": string,
  "database": string,
  "databaseUid": string,
  "snapshotTime": string,
  "expireTime": string,
  "state": enum (State)
}
```

| Fields         |                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
|----------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name`         | `string` Output only. The unique resource name of the Backup. Format is `projects/{project}/locations/{location}/backups/{backup}` . The location in the name will be the Standard Managed Multi-Region (SMMR) location (e.g. `us` ) if the backup was created with an SMMR location, or the Google Managed Multi-Region (GMMR) location (e.g. `nam5` ) if the backup was created with a GMMR location.                                                            |
| `database`     | `string` Output only. Name of the Firestore database that the backup is from. Format is `projects/{project}/databases/{database}` .                                                                                                                                                                                                                                                                                                                                |
| `databaseUid`  | `string` Output only. The system-generated UUID4 for the Firestore database that the backup is from.                                                                                                                                                                                                                                                                                                                                                               |
| `snapshotTime` | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Output only. The backup contains an externally consistent copy of the database at this time. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` . |
| `expireTime`   | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Output only. The timestamp at which this backup expires. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .                                     |
| `state`        | `enum ( `[`State`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.locations.backups#State)` )` Output only. The current state of the backup.                                                                                                                                                                                                                                                                                              |

## State

Indicate the current state of the backup.

| Enums               |                                                                                                     |
|---------------------|-----------------------------------------------------------------------------------------------------|
| `STATE_UNSPECIFIED` | The state is unspecified.                                                                           |
| `CREATING`          | The pending backup is still being created. Operations on the backup will be rejected in this state. |
| `READY`             | The backup is complete and ready to use.                                                            |
| `NOT_AVAILABLE`     | The backup is not available at this moment.                                                         |

| Methods                                                                                                      |                                  |
|--------------------------------------------------------------------------------------------------------------|----------------------------------|
| [`delete`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.locations.backups/delete) | Deletes a backup.                |
| [`get`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.locations.backups/get)       | Gets information about a backup. |
| [`list`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.locations.backups/list)     | Lists all the backups.           |
