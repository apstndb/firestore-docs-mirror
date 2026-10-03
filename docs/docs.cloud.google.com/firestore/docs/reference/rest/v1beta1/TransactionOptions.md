---
name: documents/docs.cloud.google.com/firestore/docs/reference/rest/v1beta1/TransactionOptions
uri: https://docs.cloud.google.com/firestore/docs/reference/rest/v1beta1/TransactionOptions
title: TransactionOptions
description: A cloud-hosted NoSQL database that's simple enough for rapid prototyping yet scalable and flexible enough to grow to any size.
data_source: docs.cloud.google.com
---

Options for creating a new transaction.

**JSON representation**

```
{

  // Union field mode can be only one of the following:
  "readOnly": {
    object (ReadOnly)
  },
  "readWrite": {
    object (ReadWrite)
  }
  // End of list of possible types for union field mode.
}
```

| Fields                                                                                     |                                                                                                                                                                                                |
|--------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `mode` . The mode of the transaction. `mode` can be only one of the following: |                                                                                                                                                                                                |
| `readOnly`                                                                                 | `object ( `[`ReadOnly`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1beta1/TransactionOptions#ReadOnly)` )` The transaction can only be used for read operations.             |
| `readWrite`                                                                                | `object ( `[`ReadWrite`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1beta1/TransactionOptions#ReadWrite)` )` The transaction can be used for both read and write operations. |

## ReadOnly

Options for a transaction that can only be used to read documents.

**JSON representation**

```
{

  // Union field consistency_selector can be only one of the following:
  "readTime": string
  // End of list of possible types for union field consistency_selector.
}
```

| Fields                                                                                                                                                                               |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `consistency_selector` . The consistency mode for this transaction. If not set, defaults to strong consistency. `consistency_selector` can be only one of the following: |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| `readTime`                                                                                                                                                                           | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Reads documents at the given time. This must be a microsecond precision timestamp within the past one hour, or if Point-in-Time Recovery is enabled, can additionally be a whole minute timestamp within the past 7 days. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` . |

## ReadWrite

Options for a transaction that can be used to read and write documents.

Firestore does not allow 3rd party auth requests to create read-write. transactions.

**JSON representation**

```
{
  "retryTransaction": string
}
```

| Fields             |                                                                                                                                                   |
|--------------------|---------------------------------------------------------------------------------------------------------------------------------------------------|
| `retryTransaction` | `string ( `[`bytes`](https://developers.google.com/discovery/v1/type-format)` format)` An optional transaction to retry. A base64-encoded string. |
