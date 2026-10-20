---
name: documents/docs.cloud.google.com/firestore/mongodb-compatibility/docs/supported-data-types-drivers
uri: https://docs.cloud.google.com/firestore/mongodb-compatibility/docs/supported-data-types-drivers
title: Supported MongoDB data types and drivers
description: Learn about supported MongoDB data types and drivers for Firestore with MongoDB compatibility.
data_source: docs.cloud.google.com
---

# Supported MongoDB data types and drivers

The following tables list supported MongoDB data types, drivers, and third-party tools for Firestore with MongoDB compatibility.

## Data types

| **BSON Type**           | **Supported** |
|-------------------------|---------------|
| 32-bit Integer          | Yes           |
| 64-bit Integer          | Yes           |
| Array                   | Yes           |
| Binary Data             | Yes           |
| Boolean                 | Yes           |
| Date                    | Yes           |
| DBPointer               | No            |
| Decimal128              | Yes           |
| Double                  | Yes           |
| JavaScript              | No            |
| JavaScript (with scope) | No            |
| MaxKey                  | Yes           |
| MinKey                  | Yes           |
| Null                    | Yes           |
| Object                  | Yes           |
| ObjectId                | Yes           |
| Regular Expression      | Yes           |
| String                  | Yes           |
| Symbol                  | No            |
| Timestamp               | Yes           |
| Undefined               | No            |

## Document `_id`

The top-level `_id` field in a document must be one of the following types:

- ObjectId
- String
- 64-bit Integer
- 32-bit Integer
- Double
- Binary
- Object
- Boolean

The total size of the `_id` must not exceed 1500 bytes.

Each values within an Object-typed ID must also be of a supported ID type or an Array of values, each of which is of a supported ID type.

Other BSON types are not supported.

## Languages and MongoDB drivers

Firestore with MongoDB compatibility supports the following driver versions:

| **Language** | **Driver versions** |
|--------------|---------------------|
| Java         | 5.x                 |
| Node.js      | 6.x 5.x             |
| Python       | 4.x 3.x (x ≥ 12)    |
| Go           | 2.x                 |
| C#           | 3.x                 |
| Ruby         | 2.x (x ≥ 16)        |

### OIDC authentication support

The Go, C#, and Ruby drivers support OpenID Connect (OIDC) authentication from Google Cloud for all supported driver versions.

The Java, Node.js, and Python drivers support OIDC authentication from Google Cloud starting with the following driver versions:

- Java: 4.10
- Node.js: 6.7
- Python: 4.7

## Third-party tools

Firestore with MongoDB compatibility supports third-party tools described in this section.

| **Tool**                                                                  | **Description**               | **Notes**                                                                                                                  |
|---------------------------------------------------------------------------|-------------------------------|----------------------------------------------------------------------------------------------------------------------------|
| [mongoimport](https://www.mongodb.com/docs/database-tools/mongoimport/)   | MongoDB Database Tools        | See [Bulk data loading](https://docs.cloud.google.com/firestore/mongodb-compatibility/docs/bulk-data-loading#mongoimport)  |
| [mongoexport](https://www.mongodb.com/docs/database-tools/mongoexport/)   | MongoDB Database Tools        |                                                                                                                            |
| [mongodump](https://www.mongodb.com/docs/database-tools/mongodump/)       | MongoDB Database Tools        |                                                                                                                            |
| [mongorestore](https://www.mongodb.com/docs/database-tools/mongorestore/) | MongoDB Database Tools        | See [Bulk data loading](https://docs.cloud.google.com/firestore/mongodb-compatibility/docs/bulk-data-loading#mongorestore) |
| [mongosh](https://www.mongodb.com/docs/mongodb-shell/)                    | MongoDB Shell                 |                                                                                                                            |
| [Mongoose](https://mongoosejs.com/)                                       | MongoDB object modeling tool  |                                                                                                                            |
| [MongoDB Compass](https://www.mongodb.com/products/tools/compass)         | GUI tool for data exploration |                                                                                                                            |

> **Note:** Some third-party tools require a connection string. To obtain a connection string for your Firestore with MongoDB compatibility database, you can run the [`firestore databases connection-string` command](https://cloud.google.com/sdk/gcloud/reference/firestore/databases/connection-string) using Google Cloud CLI.

## BSON and Firestore type compatibility

This section summarizes the mapping between MongoDB BSON types and Firestore values. Since BSON is a binary format and the Firestore API uses Protocol Buffers, some types map directly, while others require special map representations.

### Mapping overview

The following tables show how BSON data types correspond to Firestore protocol buffer representations.

#### Direct mappings

These types have a direct equivalent in both systems.

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>BSON Type</th>
<th>BSON</th>
<th>Firestore Proto</th>
<th>Notes</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>Double</strong></td>
<td><code>1.23</code></td>
<td><code>double_value: 1.23</code></td>
<td></td>
</tr>
<tr class="even">
<td><strong>String</strong></td>
<td><code>"hello"</code></td>
<td><code>string_value: "hello"</code></td>
<td></td>
</tr>
<tr class="odd">
<td><strong>Object</strong></td>
<td><pre data-fenced=""><code>{
  &quot;a&quot;: 1.23
}</code></pre></td>
<td><pre data-fenced=""><code>map_value {
  fields {
    key: &quot;a&quot;
    value {
      double_value: 1.23
    }
  }
}</code></pre></td>
<td></td>
</tr>
<tr class="even">
<td><strong>Array</strong></td>
<td><pre data-fenced=""><code>[
  1.23,
  &quot;a&quot;
]</code></pre></td>
<td><pre data-fenced=""><code>array_value {
  values {
    double_value: 1.23
  }
  values {
    string_value: &quot;a&quot;
  }
}</code></pre></td>
<td></td>
</tr>
<tr class="odd">
<td><strong>Binary (Subtype Zero)</strong></td>
<td><code>BinData(0, 'SGVsbG8=')</code></td>
<td><code>bytes_value: "Hello"</code></td>
<td></td>
</tr>
<tr class="even">
<td><strong>Boolean</strong></td>
<td><code>true</code></td>
<td><code>boolean_value: true</code></td>
<td></td>
</tr>
<tr class="odd">
<td><strong>Null</strong></td>
<td><code>null</code></td>
<td><code>null_value: NULL_VALUE</code></td>
<td></td>
</tr>
<tr class="even">
<td><strong>64-bit Integer</strong></td>
<td><code>Long('1234567890')</code></td>
<td><code>integer_value: 1234567890</code></td>
<td></td>
</tr>
<tr class="odd">
<td><strong>Date</strong></td>
<td><code>ISODate('2026-05-22T04:00:00Z')</code></td>
<td><pre data-fenced=""><code>timestamp_value {
  seconds: 1779470400
  nanos: 0
}</code></pre></td>
<td>Firestore timestamp values are stored at microsecond precision, but anything beyond millisecond precision is lost when converting to BSON.</td>
</tr>
</tbody>
</table>

#### BSON types represented as maps in Firestore API

These BSON types are wrapped in the Firestore `map_value` with special keys to denote the type.

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>BSON Type</th>
<th>BSON</th>
<th>Firestore Proto</th>
<th>Notes</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>32-bit Integer</strong></td>
<td><code>123</code></td>
<td><pre data-fenced=""><code>map_value {
  fields {
    key: &quot;__int__&quot;
    value {
      integer_value: 123
    }
  }
}</code></pre></td>
<td></td>
</tr>
<tr class="even">
<td><strong>Binary (Non-Zero Subtype)</strong></td>
<td><code>BinData(1, 'AQIDBA==')</code></td>
<td><pre data-fenced=""><code>map_value {
  fields {
    key: &quot;__binary__&quot;
    value {
      bytes_value: &quot;&lt;subtype + data&gt;&quot;
    }
  }
}</code></pre></td>
<td>Subtype byte prepended to data.</td>
</tr>
<tr class="odd">
<td><strong>ObjectId</strong></td>
<td><code>ObjectId('67eea9446dc71ec469e9496a')</code></td>
<td><pre data-fenced=""><code>map_value {
  fields {
    key: &quot;__oid__&quot;
    value {
      string_value:
        &quot;67eea9446dc71ec469e9496a&quot;
    }
  }
}</code></pre></td>
<td>Lowercase hex string.</td>
</tr>
<tr class="even">
<td><strong>Timestamp (Internal)</strong></td>
<td><code>Timestamp(123, 1)</code></td>
<td><pre data-fenced=""><code>map_value {
  fields {
    key: &quot;__request_timestamp__&quot;
    value {
      map_value {
        fields {
          key: &quot;seconds&quot;
          value {
            integer_value: 123
          }
        }
        fields {
          key: &quot;increment&quot;
          value {
            integer_value: 1
          }
        }
      }
    }
  }
}</code></pre></td>
<td>MongoDB internal timestamp.</td>
</tr>
<tr class="odd">
<td><strong>Regular Expression</strong></td>
<td><code>RegExp('.*', 'im')</code></td>
<td><pre data-fenced=""><code>map_value {
  fields {
    key: &quot;__regex__&quot;
    value {
      map_value {
        fields {
          key: &quot;pattern&quot;
          value {
            string_value: &quot;.*&quot;
          }
        }
        fields {
          key: &quot;options&quot;
          value {
            string_value: &quot;im&quot;
          }
        }
      }
    }
  }
}</code></pre></td>
<td></td>
</tr>
<tr class="even">
<td><strong>Min Key</strong></td>
<td><code>MinKey()</code></td>
<td><pre data-fenced=""><code>map_value {
  fields {
    key: &quot;__min__&quot;
    value {
      null_value: NULL_VALUE
    }
  }
}</code></pre></td>
<td></td>
</tr>
<tr class="odd">
<td><strong>Max Key</strong></td>
<td><code>MaxKey()</code></td>
<td><pre data-fenced=""><code>map_value {
  fields {
    key: &quot;__max__&quot;
    value {
      null_value: NULL_VALUE
    }
  }
}</code></pre></td>
<td></td>
</tr>
<tr class="even">
<td><strong>Decimal128</strong></td>
<td><code>Decimal128('4E7')</code></td>
<td><pre data-fenced=""><code>map_value {
  fields {
    key: &quot;__decimal128__&quot;
    value {
      string_value: &quot;4E7&quot;
    }
  }
}</code></pre></td>
<td></td>
</tr>
</tbody>
</table>

#### Firestore types not natively in BSON

These Firestore types are represented as specially structured maps when converted to BSON.

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Firestore Type</th>
<th>BSON</th>
<th>Firestore Proto</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>GeoPoint</strong></td>
<td><pre data-fenced=""><code>{
  &quot;__fs_geopoint__&quot;: {
    &quot;latitude&quot;: 37.42,
    &quot;longitude&quot;: -122.08
  }
}</code></pre></td>
<td><pre data-fenced=""><code>geo_point_value {
  latitude: 37.42
  longitude: -122.08
}</code></pre></td>
</tr>
<tr class="even">
<td><strong>Vector</strong></td>
<td><pre data-fenced=""><code>{
  &quot;__fs_vector__&quot;: [
    1.0,
    2.0
  ]
}</code></pre></td>
<td><pre data-fenced=""><code>map_value {
  fields {
    key: &quot;__type__&quot;
    value {
      string_value: &quot;__vector__&quot;
    }
  }
  fields {
    key: &quot;value&quot;
    value {
      array_value {
        ...
      }
    }
  }
}</code></pre></td>
</tr>
<tr class="odd">
<td><strong>Document Ref</strong></td>
<td><pre data-fenced=""><code>{
  &quot;__fs_ref__&quot;: &quot;projects/.../documents/col/doc&quot;
}</code></pre></td>
<td><code>reference_value: "projects/.../documents/col/doc"</code></td>
</tr>
</tbody>
</table>

### Field names

Field names from MongoDB that match `__.*__` are escaped by incorporating `r:` when stored in Firestore. For example, a BSON field `__foo__` becomes `__r:foo__` in Firestore.

### BSON data types in client SDKs

When using Firestore client SDKs, you can use specialized SDK classes to represent BSON data types like 128-bit decimals, regular expressions, and BSON timestamps.

##### Node.js

```
const { RegexValue, Decimal128Value, BsonTimestamp } = require('@google-cloud/firestore');

// Setting fields with BSON data types
const res = await db.collection('foo').doc('bar').set({
  regex: new RegexValue('myRegexPattern', 'i'),
  decimal: new Decimal128Value('0.73e-7'),
  bsonTimestamp: new BsonTimestamp(1732754912, 500),
});
```

##### Java

```
import com.google.cloud.firestore.BsonTimestamp;
import com.google.cloud.firestore.Decimal128Value;
import com.google.cloud.firestore.RegexValue;
import java.util.HashMap;
import java.util.Map;

Map<String, Object> data = new HashMap<>();
data.put("regex", new RegexValue("myRegexPattern", "i"));
data.put("decimal", new Decimal128Value("0.73e-7"));
data.put("bson_timestamp", new BsonTimestamp(1732754912, 500));

db.collection("foo").doc("bar").set(data);
```

##### Java Android

```
import com.google.firebase.firestore.BsonTimestamp;
import com.google.firebase.firestore.Decimal128Value;
import com.google.firebase.firestore.RegexValue;
import java.util.HashMap;
import java.util.Map;

Map<String, Object> data = new HashMap<>();
data.put("regex", new RegexValue("myRegexPattern", "i"));
data.put("decimal", new Decimal128Value("0.73e-7"));
data.put("bson_timestamp", new BsonTimestamp(1732754912, 500));

db.collection("foo").doc("bar").set(data);
```

##### Go

```
import (
    "context"

    "cloud.google.com/go/firestore"
)

func writeBsonTypes(ctx context.Context, client *firestore.Client) error {
    _, err := client.Collection("foo").Doc("bar").Set(ctx, map[string]interface{}{
        "regex":     firestore.RegexValue{Pattern: "myRegexPattern", Options: "i"},
        "decimal":   firestore.Decimal128Value{Value: "0.73e-7"},
        "bson_timestamp": firestore.BsonTimestamp{Seconds: 1732754912, Increment: 500},
    })
    return err
}
```

## What's next

- Run the [Quickstart: Create a database and connect to it](https://docs.cloud.google.com/firestore/mongodb-compatibility/docs/create-and-query-database) .
- Learn about [Behavior differences](https://docs.cloud.google.com/firestore/mongodb-compatibility/docs/behavior-differences) .
- For a breakdown of supported features depending on MongoDB version, see
  - [Supported features: 8.0](https://docs.cloud.google.com/firestore/mongodb-compatibility/docs/supported-features-80)
  - [Supported features: 7.0](https://docs.cloud.google.com/firestore/mongodb-compatibility/docs/supported-features-70)
  - [Supported features: 6.0](https://docs.cloud.google.com/firestore/mongodb-compatibility/docs/supported-features-60)
  - [Supported features: 5.0](https://docs.cloud.google.com/firestore/mongodb-compatibility/docs/supported-features-50)
  - [Supported features: 4.0](https://docs.cloud.google.com/firestore/mongodb-compatibility/docs/supported-features-40)
  - [Supported features: 3.6](https://docs.cloud.google.com/firestore/mongodb-compatibility/docs/supported-features-36)
