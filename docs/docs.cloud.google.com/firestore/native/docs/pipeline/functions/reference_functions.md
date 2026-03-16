# Reference Functions Reference

**Preview — Firestore in Native mode (with Pipeline Operations) for Enterprise Edition**

This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](/terms/service-terms#1) . You can process personal data for this feature as outlined in the [Cloud Data Processing Addendum](/terms/data-processing-addendum) , subject to the obligations and restrictions described in the agreement under which you access Google Cloud. Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

## **Reference Functions**

The `  REFERENCE  ` type acts as a "pointer" to other documents in the database (or even other databases). The following functions allow manipulating this type during query execution.

<table>
<tbody>
<tr class="odd">
<td>Name</td>
<td>Description</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         COLLECTION_ID       </code></td>
<td>Returns the ID of the leaf collection in the given reference</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         DOCUMENT_ID       </code></td>
<td>Returns the ID of the document in the given reference</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         PARENT       </code></td>
<td>Returns the parent reference</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         REFERENCE_SLICE       </code></td>
<td>Returns a subset of segments from the given reference</td>
</tr>
</tbody>
</table>

### COLLECTION\_ID

**Syntax:**

``` text
collection_id(ref: REFERENCE) -> STRING
```

**Description:**

Returns the leaf collection ID of the given `  REFERENCE  ` .

**Examples:**

<table>
<thead>
<tr class="header">
<th style="text-align: left;"><code dir="ltr" translate="no">       ref      </code></th>
<th style="text-align: left;"><code dir="ltr" translate="no">       collection_id(ref)      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;"><code dir="ltr" translate="no">       users/user1      </code></td>
<td style="text-align: left;"><code dir="ltr" translate="no">       "users"      </code></td>
</tr>
<tr class="even">
<td style="text-align: left;"><code dir="ltr" translate="no">       users/user1/posts/post1      </code></td>
<td style="text-align: left;"><code dir="ltr" translate="no">       "posts"      </code></td>
</tr>
</tbody>
</table>

### DOCUMENT\_ID

**Syntax:**

``` text
document_id(ref: REFERENCE) -> ANY
```

**Description:**

Returns the document ID of the given `  REFERENCE  ` .

**Examples:**

<table>
<thead>
<tr class="header">
<th style="text-align: left;"><code dir="ltr" translate="no">       ref      </code></th>
<th style="text-align: left;"><code dir="ltr" translate="no">       document_id(ref)      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;"><code dir="ltr" translate="no">       users/user1      </code></td>
<td style="text-align: left;"><code dir="ltr" translate="no">       "user1"      </code></td>
</tr>
<tr class="even">
<td style="text-align: left;"><code dir="ltr" translate="no">       users/user1/posts/post1      </code></td>
<td style="text-align: left;"><code dir="ltr" translate="no">       "post1"      </code></td>
</tr>
</tbody>
</table>

### PARENT

**Syntax:**

``` text
parent(ref: REFERENCE) -> REFERENCE
```

**Description:**

Returns the parent `  REFERENCE  ` of the given reference, or `  NULL  ` if the ref is a root reference already.

**Examples:**

<table>
<thead>
<tr class="header">
<th style="text-align: left;"><code dir="ltr" translate="no">       ref      </code></th>
<th style="text-align: left;"><code dir="ltr" translate="no">       parent(ref)      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;"><code dir="ltr" translate="no">       /      </code></td>
<td style="text-align: left;"><code dir="ltr" translate="no">       NULL      </code></td>
</tr>
<tr class="even">
<td style="text-align: left;"><code dir="ltr" translate="no">       users/user1      </code></td>
<td style="text-align: left;"><code dir="ltr" translate="no">       /      </code></td>
</tr>
<tr class="odd">
<td style="text-align: left;"><code dir="ltr" translate="no">       users/user1/posts/post1      </code></td>
<td style="text-align: left;"><code dir="ltr" translate="no">       users/user1      </code></td>
</tr>
</tbody>
</table>

### REFERENCE\_SLICE

**Syntax:**

``` text
reference_slice(ref: REFERENCE, offset: INT, length: INT) -> REFERENCE
```

**Description:**

A `  REFERENCE  ` is a list of `  (collection_id, document_id)  ` tuples and this allows getting a view of that list, just like `  array_slice(...)  ` .

Returns a new `  REFERENCE  ` that is a subset of the segments of the given `  ref  ` .

  - `  offset  ` : The starting index (0-based) of the slice. If negative, it is an offset from the end of the reference.
  - `  length  ` : The number of segments to include in the slice.

**Examples:**

<table>
<thead>
<tr class="header">
<th style="text-align: left;"><code dir="ltr" translate="no">       ref      </code></th>
<th style="text-align: left;"><code dir="ltr" translate="no">       offset      </code></th>
<th style="text-align: left;"><code dir="ltr" translate="no">       length      </code></th>
<th style="text-align: left;"><code dir="ltr" translate="no">       reference_slice(ref, offset, length)      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;"><code dir="ltr" translate="no">       a/1/b/2/c/3      </code></td>
<td style="text-align: left;">1L</td>
<td style="text-align: left;">2L</td>
<td style="text-align: left;"><code dir="ltr" translate="no">       b/2/c/3      </code></td>
</tr>
<tr class="even">
<td style="text-align: left;"><code dir="ltr" translate="no">       a/1/b/2/c/3      </code></td>
<td style="text-align: left;">0L</td>
<td style="text-align: left;">2L</td>
<td style="text-align: left;"><code dir="ltr" translate="no">       a/1/b/2      </code></td>
</tr>
<tr class="odd">
<td style="text-align: left;"><code dir="ltr" translate="no">       a/1/b/2/c/3      </code></td>
<td style="text-align: left;">-2L</td>
<td style="text-align: left;">2L</td>
<td style="text-align: left;"><code dir="ltr" translate="no">       c/3      </code></td>
</tr>
</tbody>
</table>

## What's next

  - See the [Pipeline Queries overview](/firestore/docs/pipeline/overview)
