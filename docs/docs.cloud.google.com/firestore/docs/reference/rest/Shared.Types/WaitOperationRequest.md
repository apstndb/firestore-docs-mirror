---
name: documents/docs.cloud.google.com/firestore/docs/reference/rest/Shared.Types/WaitOperationRequest
uri: https://docs.cloud.google.com/firestore/docs/reference/rest/Shared.Types/WaitOperationRequest
title: WaitOperationRequest
description: A cloud-hosted NoSQL database that's simple enough for rapid prototyping yet scalable and flexible enough to grow to any size.
data_source: docs.cloud.google.com
---

The request message for `Operations.WaitOperation` .

**JSON representation**

```
{
  "name": string,
  "timeout": string
}
```

| Fields    |                                                                                                                                                                                                                                                                                                                                                                                                                                 |
|-----------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name`    | `string` The name of the operation resource to wait on.                                                                                                                                                                                                                                                                                                                                                                         |
| `timeout` | `string ( `[`Duration`](https://protobuf.dev/reference/protobuf/google.protobuf/#duration)` format)` The maximum duration to wait before timing out. If left blank, the wait will be at most the time permitted by the underlying HTTP/RPC protocol. If RPC context deadline is also specified, the shorter one will be used. A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` . |
