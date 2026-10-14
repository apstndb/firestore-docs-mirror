---
name: documents/docs.cloud.google.com/firestore/docs/reference/rest/Shared.Types
uri: https://docs.cloud.google.com/firestore/docs/reference/rest/Shared.Types
title: Index
description: A cloud-hosted NoSQL database that's simple enough for rapid prototyping yet scalable and flexible enough to grow to any size.
data_source: docs.cloud.google.com
---

Cloud Firestore indexes enable simple and complex queries against documents in a database.

**JSON representation**

```
{
  "name": string,
  "queryScope": enum (QueryScope),
  "apiScope": enum (ApiScope),
  "fields": [
    {
      object (IndexField)
    }
  ],
  "state": enum (State),
  "density": enum (Density),
  "multikey": boolean,
  "shardCount": integer,
  "unique": boolean,
  "searchIndexOptions": {
    object (SearchIndexOptions)
  }
}
```

| Fields               |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
|----------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name`               | `string` Output only. A server defined name for this index. The form of this name for composite indexes will be: `projects/{projectId}/databases/{databaseId}/collectionGroups/{collectionId}/indexes/{composite_index_id}` For single field indexes, this field will be empty.                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| `queryScope`         | `enum ( `[`QueryScope`](https://docs.cloud.google.com/firestore/docs/reference/rest/Shared.Types/QueryScope)` )` Indexes with a collection query scope specified allow queries against a collection that is the child of a specific document, specified at query time, and that has the same collection ID. Indexes with a collection group query scope specified allow queries against all collections descended from a specific document, specified at query time, and that have the same collection ID as this index.                                                                                                                                                                                                                       |
| `apiScope`           | `enum ( `[`ApiScope`](https://docs.cloud.google.com/firestore/docs/reference/rest/Shared.Types/ApiScope)` )` The API scope supported by this index.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| `fields[]`           | `object ( `[`IndexField`](https://docs.cloud.google.com/firestore/docs/reference/rest/Shared.Types/Index#IndexField)` )` The fields supported by this index. For composite indexes, this requires a minimum of 2 and a maximum of 100 fields. The last field entry is always for the field path `__name__` . If, on creation, `__name__` was not specified as the last field, it will be added automatically with the same direction as that of the last field defined. If the final field in a composite index is not directional, the `__name__` will be ordered ASCENDING (unless explicitly specified). For single field indexes, this will always be exactly one entry with a field path equal to the field path of the associated field. |
| `state`              | `enum ( `[`State`](https://docs.cloud.google.com/firestore/docs/reference/rest/Shared.Types/State)` )` Output only. The serving state of the index.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| `density`            | `enum ( `[`Density`](https://docs.cloud.google.com/firestore/docs/reference/rest/Shared.Types/Density)` )` Immutable. The density configuration of the index.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| `multikey`           | `boolean` Optional. Whether the index is multikey. By default, the index is not multikey. For non-multikey indexes, none of the paths in the index definition reach or traverse an array, except via an explicit array index. For multikey indexes, at most one of the paths in the index definition reach or traverse an array, except via an explicit array index. Violations will result in errors. Note this field only applies to index with MONGODB_COMPATIBLE_API ApiScope.                                                                                                                                                                                                                                                             |
| `shardCount`         | `integer` Optional. The number of shards for the index.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `unique`             | `boolean` Optional. Whether it is an unique index. Unique index ensures all values for the indexed field(s) are unique across documents.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| `searchIndexOptions` | `object ( `[`SearchIndexOptions`](https://docs.cloud.google.com/firestore/docs/reference/rest/Shared.Types/Index#SearchIndexOptions)` )` Optional. Options for search indexes that are at the index definition level.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |

## IndexField

A field in an index. The fieldPath describes which field is indexed, the value_mode describes how the field value is indexed.

**JSON representation**

```
{
  "fieldPath": string,

  // Union field value_mode can be only one of the following:
  "order": enum (Order),
  "arrayConfig": enum (ArrayConfig),
  "vectorConfig": {
    object (VectorConfig)
  },
  "searchConfig": {
    object (SearchConfig)
  }
  // End of list of possible types for union field value_mode.
}
```

| Fields                                                                                                    |                                                                                                                                                                                                                       |
|-----------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `fieldPath`                                                                                               | `string` Can be **name** . For single field indexes, this must match the name of the field or may be omitted.                                                                                                         |
| Union field `value_mode` . How the field value is indexed. `value_mode` can be only one of the following: |                                                                                                                                                                                                                       |
| `order`                                                                                                   | `enum ( `[`Order`](https://docs.cloud.google.com/firestore/docs/reference/rest/Shared.Types/Order)` )` Indicates that this field supports ordering by the specified order or comparing using =, !=, \<, \<=, \>, \>=. |
| `arrayConfig`                                                                                             | `enum ( `[`ArrayConfig`](https://docs.cloud.google.com/firestore/docs/reference/rest/Shared.Types/ArrayConfig)` )` Indicates that this field supports operations on `arrayValue` s.                                   |
| `vectorConfig`                                                                                            | `object ( `[`VectorConfig`](https://docs.cloud.google.com/firestore/docs/reference/rest/Shared.Types/Index#VectorConfig)` )` Indicates that this field supports nearest neighbor and distance operations on vector.   |
| `searchConfig`                                                                                            | `object ( `[`SearchConfig`](https://docs.cloud.google.com/firestore/docs/reference/rest/Shared.Types/Index#SearchConfig)` )` Indicates that this field supports search operations.                                    |

## VectorConfig

The index configuration to support vector search operations

**JSON representation**

```
{
  "dimension": integer,

  // Union field type can be only one of the following:
  "flat": {
    object (FlatIndex)
  }
  // End of list of possible types for union field type.
}
```

| Fields                                                                                |                                                                                                                                                                                                     |
|---------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `dimension`                                                                           | `integer` Required. The vector dimension this configuration applies to. The resulting index will only include vectors of this dimension, and can be used for vector search with the same dimension. |
| Union field `type` . The type of index used. `type` can be only one of the following: |                                                                                                                                                                                                     |
| `flat`                                                                                | `object ( `[`FlatIndex`](https://docs.cloud.google.com/firestore/docs/reference/rest/Shared.Types/Index#FlatIndex)` )` Indicates the vector index is a flat index.                                  |

## FlatIndex

This type has no fields.

An index that stores vectors in a flat data structure, and supports exhaustive search.

## SearchConfig

The configuration for how to index a field for search.

**JSON representation**

```
{
  "textSpec": {
    object (SearchTextSpec)
  },
  "geoSpec": {
    object (SearchGeoSpec)
  }
}
```

| Fields     |                                                                                                                                                                                                            |
|------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `textSpec` | `object ( `[`SearchTextSpec`](https://docs.cloud.google.com/firestore/docs/reference/rest/Shared.Types/Index#SearchTextSpec)` )` Optional. The specification for building a text search index for a field. |
| `geoSpec`  | `object ( `[`SearchGeoSpec`](https://docs.cloud.google.com/firestore/docs/reference/rest/Shared.Types/Index#SearchGeoSpec)` )` Optional. The specification for building a geo search index for a field.    |

## SearchTextSpec

The specification for how to build a text search index for a field.

**JSON representation**

```
{
  "indexSpecs": [
    {
      object (SearchTextIndexSpec)
    }
  ]
}
```

| Fields         |                                                                                                                                                                                                                                                                      |
|----------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `indexSpecs[]` | `object ( `[`SearchTextIndexSpec`](https://docs.cloud.google.com/firestore/docs/reference/rest/Shared.Types/Index#SearchTextIndexSpec)` )` Required. Specifications for how the field should be indexed. Repeated so that the field can be indexed in multiple ways. |

## SearchTextIndexSpec

Specification of how the field should be indexed for search text indexes.

**JSON representation**

```
{
  "indexType": enum (TextIndexType),
  "matchType": enum (TextMatchType)
}
```

| Fields      |                                                                                                                                                                     |
|-------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `indexType` | `enum ( `[`TextIndexType`](https://docs.cloud.google.com/firestore/docs/reference/rest/Shared.Types/TextIndexType)` )` Required. How to index the text field value. |
| `matchType` | `enum ( `[`TextMatchType`](https://docs.cloud.google.com/firestore/docs/reference/rest/Shared.Types/TextMatchType)` )` Required. How to match the text field value. |

## SearchGeoSpec

The specification for how to build a geo search index for a field.

**JSON representation**

```
{
  "geoJsonIndexingDisabled": boolean
}
```

| Fields                    |                                                                                                      |
|---------------------------|------------------------------------------------------------------------------------------------------|
| `geoJsonIndexingDisabled` | `boolean` Optional. Disables geoJSON indexing for the field. By default, geoJSON points are indexed. |

## SearchIndexOptions

Options for search indexes at the definition level.

**JSON representation**

```
{
  "textLanguage": string,
  "textLanguageOverrideFieldPath": string
}
```

| Fields                          |                                                                                                                                                                                                                                                                                                                                                                                                                                          |
|---------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `textLanguage`                  | `string` Optional. The language to use for text search indexes. Used as the default language if not overridden at the document level by specifying the `text_language_override_field` . The language is specified as a BCP 47 language code. For indexes with MONGODB_COMPATIBLE_API ApiScope: If unspecified, the default language is English. For indexes with `ANY_API` ApiScope: If unspecified, the default behavior is autodetect. |
| `textLanguageOverrideFieldPath` | `string` Optional. The field in the document that specifies which language to use for that specific document. For indexes with MONGODB_COMPATIBLE_API ApiScope: if unspecified, the language is taken from the "language" field if it exists or from `textLanguage` if it does not.                                                                                                                                                      |
