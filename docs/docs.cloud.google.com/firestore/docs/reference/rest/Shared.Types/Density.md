The density configuration for the index.

Enums

`  DENSITY_UNSPECIFIED  `

Unspecified. It will use database default setting. This value is input only.

`  SPARSE_ALL  `

An index entry will only exist if ALL fields are present in the document.

This is both the default and only allowed value for Standard Edition databases (for both Cloud Firestore `  ANY_API  ` and Cloud Datastore `  DATASTORE_MODE_API  ` ).

Take for example the following document:

``` text
{
  "__name__": "...",
  "a": 1,
  "b": 2,
  "c": 3
}
```

an index on `  (a ASC, b ASC, c ASC, __name__ ASC)  ` will generate an index entry for this document since `  a  ` , 'b', `  c  ` , and `  __name__  ` are all present but an index of `  (a ASC, d ASC, __name__ ASC)  ` will not generate an index entry for this document since `  d  ` is missing.

This means that such indexes can only be used to serve a query when the query has either implicit or explicit requirements that all fields from the index are present.

`  SPARSE_ANY  `

An index entry will exist if ANY field are present in the document.

This is used as the definition of a sparse index for Enterprise Edition databases.

Take for example the following document:

``` text
{
  "__name__": "...",
  "a": 1,
  "b": 2,
  "c": 3
}
```

an index on `  (a ASC, d ASC)  ` will generate an index entry for this document since `  a  ` is present, and will fill in an `  unset  ` value for `  d  ` . An index on `  (d ASC, e ASC)  ` will not generate any index entry as neither `  d  ` nor `  e  ` are present.

An index that contains `  __name__  ` will generate an index entry for all documents since Firestore guarantees that all documents have a `  __name__  ` field.

`  DENSE  `

An index entry will exist regardless of if the fields are present or not.

This is the default density for an Enterprise Edition database.

The index will store `  unset  ` values for fields that are not present in the document.
