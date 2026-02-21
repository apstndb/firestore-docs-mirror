# Supported features: 7.0

The following tables include a breakdown of MongoDB 7.0 features supported by Firestore with MongoDB compatibility. For differences in behavior, see [Behavior differences](/firestore/mongodb-compatibility/docs/behavior-differences) .

## Query and projection operators

Firestore with MongoDB compatibility supports the following query and projection operators:

### Array operators

<table>
<thead>
<tr class="header">
<th><strong>Operator</strong></th>
<th><strong>Supported</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       $all      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $elemMatch      </code></td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $size      </code></td>
<td>Yes</td>
</tr>
</tbody>
</table>

### Bitwise operators

<table>
<thead>
<tr class="header">
<th><strong>Operator</strong></th>
<th><strong>Supported</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       $bitsAllClear      </code></td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $bitsAllSet      </code></td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $bitsAnyClear      </code></td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $bitsAnySet      </code></td>
<td>No</td>
</tr>
</tbody>
</table>

### Comment operator

<table>
<thead>
<tr class="header">
<th><strong>Operator</strong></th>
<th><strong>Supported</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       $comment      </code></td>
<td>No</td>
</tr>
</tbody>
</table>

### Comparison operators

<table>
<thead>
<tr class="header">
<th><strong>Operator</strong></th>
<th><strong>Supported</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       $eq      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $gt      </code></td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $gte      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $in      </code></td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $lt      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $lte      </code></td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $ne      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $nin      </code></td>
<td>Yes</td>
</tr>
</tbody>
</table>

### Element operators

<table>
<thead>
<tr class="header">
<th><strong>Operator</strong></th>
<th><strong>Supported</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       $exists      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $type      </code></td>
<td>Yes</td>
</tr>
</tbody>
</table>

### Evaluation query operators

<table>
<thead>
<tr class="header">
<th><strong>Operator</strong></th>
<th><strong>Supported</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       $expr      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $jsonSchema      </code></td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $mod      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $regex      </code></td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $text      </code></td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $where      </code></td>
<td>No</td>
</tr>
</tbody>
</table>

### Logical operators

<table>
<thead>
<tr class="header">
<th><strong>Operator</strong></th>
<th><strong>Supported</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       $and      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $nor      </code></td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $not      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $or      </code></td>
<td>Yes</td>
</tr>
</tbody>
</table>

### Projection operators

<table>
<thead>
<tr class="header">
<th><strong>Operator</strong></th>
<th><strong>Supported</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       $      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $elemMatch      </code></td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $meta      </code></td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $slice      </code></td>
<td>Yes</td>
</tr>
</tbody>
</table>

## Update operators

Firestore with MongoDB compatibility supports the following update operators.

### Array operators

<table>
<thead>
<tr class="header">
<th><strong>Operator</strong></th>
<th><strong>Supported</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       $      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $[]      </code></td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $[&lt;identifier&gt;]      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $addToSet      </code></td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $percentile      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $pop      </code></td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $pull      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $pullAll      </code></td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $push      </code></td>
<td>Yes</td>
</tr>
</tbody>
</table>

### Bitwise operators

<table>
<thead>
<tr class="header">
<th><strong>Operator</strong></th>
<th><strong>Supported</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       $bit      </code></td>
<td>Yes</td>
</tr>
</tbody>
</table>

### Field operators

<table>
<thead>
<tr class="header">
<th><strong>Operator</strong></th>
<th><strong>Supported</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       $currentDate      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $inc      </code></td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $max      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $min      </code></td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $mul      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $rename      </code></td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $set      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $setOnInsert      </code></td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $unset      </code></td>
<td>Yes</td>
</tr>
</tbody>
</table>

### Update modifiers

<table>
<thead>
<tr class="header">
<th><strong>Modifier</strong></th>
<th><strong>Supported</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       $each      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $position      </code></td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $slice      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $sort      </code></td>
<td>Yes</td>
</tr>
</tbody>
</table>

## Aggregation pipeline operators

Firestore with MongoDB compatibility supports the following aggregation pipeline operators.

### Accumulators

<table>
<thead>
<tr class="header">
<th><strong>Expression</strong></th>
<th><strong>Supported</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       $accumulator      </code></td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $addToSet      </code></td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $avg      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $bottom      </code></td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $bottomN      </code></td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $count      </code></td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $first      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $firstN      </code></td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $last      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $lastN      </code></td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $max      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $maxN      </code></td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $median      </code></td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $mergeObjects      </code></td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $min      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $minN      </code></td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $percentile      </code></td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $push      </code></td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $stdDevPop      </code></td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $stdDevSamp      </code></td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $sum      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $top      </code></td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $topN      </code></td>
<td>No</td>
</tr>
</tbody>
</table>

### Accumulator expressions

<table>
<thead>
<tr class="header">
<th><strong>Expression</strong></th>
<th><strong>Supported</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       $avg      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $first      </code></td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $last      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $max      </code></td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $median      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $min      </code></td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $percentile      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $stdDevPop      </code></td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $stdDevSamp      </code></td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $sum      </code></td>
<td>Yes</td>
</tr>
</tbody>
</table>

### Arithmetic operators

**Limitations** : Arithmetic operators don't support `  decimal128  ` values.

<table>
<thead>
<tr class="header">
<th><strong>Operator</strong></th>
<th><strong>Supported</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       $abs      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $add      </code></td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $ceil      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $divide      </code></td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $exp      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $floor      </code></td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $ln      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $log      </code></td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $log10      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $mod      </code></td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $multiply      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $pow      </code></td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $round      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $sqrt      </code></td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $subtract      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $trunc      </code></td>
<td>Yes</td>
</tr>
</tbody>
</table>

### Array operators

<table>
<thead>
<tr class="header">
<th><strong>Operator</strong></th>
<th><strong>Supported</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       $arrayElemAt      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $arrayToObject      </code></td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $concatArrays      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $filter      </code></td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $firstN      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $in      </code></td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $indexOfArray      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $isArray      </code></td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $lastN      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $map      </code></td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $maxN      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $minN      </code></td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $objectToArray      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $range      </code></td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $reduce      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $reverseArray      </code></td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $size      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $slice      </code></td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $sortArray      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $zip      </code></td>
<td>Yes</td>
</tr>
</tbody>
</table>

### Boolean operators

<table>
<thead>
<tr class="header">
<th><strong>Operator</strong></th>
<th><strong>Supported</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       $and      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $not      </code></td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $or      </code></td>
<td>Yes</td>
</tr>
</tbody>
</table>

### Comparison operators

<table>
<thead>
<tr class="header">
<th><strong>Operator</strong></th>
<th><strong>Supported</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       $cmp      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $eq      </code></td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $gt      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $gte      </code></td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $lt      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $lte      </code></td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $ne      </code></td>
<td>Yes</td>
</tr>
</tbody>
</table>

### Conditional expression operators

<table>
<thead>
<tr class="header">
<th><strong>Operator</strong></th>
<th><strong>Supported</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       $cond      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $ifNull      </code></td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $switch      </code></td>
<td>Yes</td>
</tr>
</tbody>
</table>

### Data size operators

<table>
<thead>
<tr class="header">
<th><strong>Operator</strong></th>
<th><strong>Supported</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       $binarySize      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $bsonSize      </code></td>
<td>Yes</td>
</tr>
</tbody>
</table>

### Date operators

<table>
<thead>
<tr class="header">
<th><strong>Operator</strong></th>
<th><strong>Supported</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       $dateAdd      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $dateDiff      </code></td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $dateFromParts      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $dateFromString      </code></td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $dateSubtract      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $dateToParts      </code></td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $dateToString      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $dateTrunc      </code></td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $dayOfMonth      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $dayOfWeek      </code></td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $dayOfYear      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $hour      </code></td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $isoDayOfWeek      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $isoWeek      </code></td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $isoWeekYear      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $millisecond      </code></td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $minute      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $month      </code></td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $second      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $toDate      </code></td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $week      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $year      </code></td>
<td>Yes</td>
</tr>
</tbody>
</table>

### Timestamp operators

<table>
<thead>
<tr class="header">
<th><strong>Operator</strong></th>
<th><strong>Supported</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       $tsIncrement      </code></td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $tsSecond      </code></td>
<td>No</td>
</tr>
</tbody>
</table>

### Miscellaneous operators

<table>
<thead>
<tr class="header">
<th><strong>Operator</strong></th>
<th><strong>Supported</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       $getField      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $natural      </code></td>
<td>Yes (ascending)</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $rand      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $sampleRate      </code></td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $toHashedIndexKey      </code></td>
<td>No</td>
</tr>
</tbody>
</table>

### Literal expression operators

<table>
<thead>
<tr class="header">
<th><strong>Operator</strong></th>
<th><strong>Supported</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       $literal      </code></td>
<td>Yes</td>
</tr>
</tbody>
</table>

### Object operators

<table>
<thead>
<tr class="header">
<th><strong>Operator</strong></th>
<th><strong>Supported</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       $mergeObjects      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $objectToArray      </code></td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $setField      </code></td>
<td>No</td>
</tr>
</tbody>
</table>

### Set operators

<table>
<thead>
<tr class="header">
<th><strong>Operator</strong></th>
<th><strong>Supported</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       $allElementsTrue      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $anyElementTrue      </code></td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $setDifference      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $setEquals      </code></td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $setIntersection      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $setIsSubset      </code></td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $setUnion      </code></td>
<td>Yes</td>
</tr>
</tbody>
</table>

### Stage operators

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Operator</strong></th>
<th><strong>Supported</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       $addFields      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $bucket      </code></td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $bucketAuto      </code></td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $changeStreams      </code></td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $collStats      </code></td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $count      </code></td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $currentOp      </code></td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $documents      </code></td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $facet      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $geoNear      </code></td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $graphLookup      </code></td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $group      </code></td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $indexStats      </code></td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $limit      </code></td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $listLocalSessions      </code></td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $listSessions      </code></td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $lookup      </code></td>
<td><p>Yes</p>
<p>Doesn't support the <code dir="ltr" translate="no">        let       </code> and <code dir="ltr" translate="no">        pipeline       </code> fields.</p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $match      </code></td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $merge      </code></td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $out      </code></td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $planCacheStats      </code></td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $project      </code></td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $redact      </code></td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $replaceRoot      </code></td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $replaceWith      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $sample      </code></td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $set      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $search      </code></td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $setWindowFields      </code></td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $skip      </code></td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $sort      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $sortByCount      </code></td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $unionWith      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $unset      </code></td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $unwind      </code></td>
<td>Yes</td>
</tr>
</tbody>
</table>

### String operators

<table>
<thead>
<tr class="header">
<th><strong>Operator</strong></th>
<th><strong>Supported</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       $concat      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $dateFromString      </code></td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $dateToString      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $indexOfBytes      </code></td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $indexOfCP      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $ltrim      </code></td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $regexFind      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $regexFindAll      </code></td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $regexMatch      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $replaceAll      </code></td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $replaceOne      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $rtrim      </code></td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $split      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $strcasecmp      </code></td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $strLenBytes      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $strLenCP      </code></td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $substr      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $substrBytes      </code></td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $substrCP      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $toLower      </code></td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $toString      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $toUpper      </code></td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $trim      </code></td>
<td>Yes</td>
</tr>
</tbody>
</table>

### System variables

<table>
<thead>
<tr class="header">
<th><strong>Variable</strong></th>
<th><strong>Supported</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       $$CLUSTERTIME      </code></td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $$CURRENT      </code></td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $$DESCEND      </code></td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $$KEEP      </code></td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $$NOW      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $$PRUNE      </code></td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $$REMOVE      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $$ROOT      </code></td>
<td>Yes</td>
</tr>
</tbody>
</table>

### Text operators

<table>
<thead>
<tr class="header">
<th><strong>Operator</strong></th>
<th><strong>Supported</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       $meta      </code></td>
<td>No</td>
</tr>
</tbody>
</table>

### Trigonometry operators

<table>
<thead>
<tr class="header">
<th><strong>Operator</strong></th>
<th><strong>Supported</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       $acos      </code></td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $acosh      </code></td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $asin      </code></td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $asinh      </code></td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $atan      </code></td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $atan2      </code></td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $atanh      </code></td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $cos      </code></td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $cosh      </code></td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $degreesToRadians      </code></td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $radiansToDegrees      </code></td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $sin      </code></td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $sinh      </code></td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $tan      </code></td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $tanh      </code></td>
<td>No</td>
</tr>
</tbody>
</table>

### Type operators

<table>
<thead>
<tr class="header">
<th><strong>Operator</strong></th>
<th><strong>Supported</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       $convert      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $isNumber      </code></td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $toBool      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $toDate      </code></td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $toDecimal      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $toDouble      </code></td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $toInt      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $toLong      </code></td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $toObjectId      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $toString      </code></td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $type      </code></td>
<td>Yes</td>
</tr>
</tbody>
</table>

### Variable operators

<table>
<thead>
<tr class="header">
<th><strong>Operator</strong></th>
<th><strong>Supported</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       $let      </code></td>
<td>Yes</td>
</tr>
</tbody>
</table>

## Geospatial

Firestore with MongoDB compatibility supports the following Geospatial operators.

### Geometry specifiers

<table>
<thead>
<tr class="header">
<th><strong>Specifier</strong></th>
<th><strong>Supported</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       $box      </code></td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $center      </code></td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $centerSphere      </code></td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $geometry      </code></td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $maxDistance      </code></td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $minDistance      </code></td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $polygon      </code></td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $uniqueDocs      </code></td>
<td>No</td>
</tr>
</tbody>
</table>

### Query selectors

<table>
<thead>
<tr class="header">
<th><strong>Selector</strong></th>
<th><strong>Supported</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       $geoIntersects      </code></td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $geoWithin      </code></td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $near      </code></td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $nearSphere      </code></td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       $nearSphere      </code></td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       $uniqueDocs      </code></td>
<td>No</td>
</tr>
</tbody>
</table>

## Indexes and index properties

Firestore with MongoDB compatibility supports the following indexes and index operators.

### Indexes

<table>
<thead>
<tr class="header">
<th><strong>Index type</strong></th>
<th><strong>Supported</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>2d</td>
<td>No</td>
</tr>
<tr class="even">
<td>2dsphere</td>
<td>No</td>
</tr>
<tr class="odd">
<td>Compound</td>
<td>Yes</td>
</tr>
<tr class="even">
<td>Hashed</td>
<td>No</td>
</tr>
<tr class="odd">
<td>Multikey</td>
<td>Yes</td>
</tr>
<tr class="even">
<td>Single Field</td>
<td>Yes</td>
</tr>
<tr class="odd">
<td>Text</td>
<td>No</td>
</tr>
</tbody>
</table>

### Index properties

<table>
<thead>
<tr class="header">
<th><strong>Property</strong></th>
<th><strong>Supported</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Background</td>
<td>Yes</td>
</tr>
<tr class="even">
<td>Case Insensitive</td>
<td>No</td>
</tr>
<tr class="odd">
<td>Hidden</td>
<td>No</td>
</tr>
<tr class="even">
<td>Partial</td>
<td>No</td>
</tr>
<tr class="odd">
<td>Non-Sparse</td>
<td>Yes</td>
</tr>
<tr class="even">
<td>Sparse</td>
<td>Yes</td>
</tr>
<tr class="odd">
<td>Text</td>
<td>No</td>
</tr>
<tr class="even">
<td>TTL</td>
<td>No</td>
</tr>
<tr class="odd">
<td>Unique</td>
<td>Yes</td>
</tr>
<tr class="even">
<td>Wildcard</td>
<td>No</td>
</tr>
<tr class="odd">
<td>Vector</td>
<td>No</td>
</tr>
</tbody>
</table>

## Database commands

Firestore with MongoDB compatibility supports the following database commands.

### Aggregation

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Command</strong></th>
<th><strong>Supported</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       aggregate      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       count      </code></td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       distinct      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       group      </code></td>
<td><p>No</p>
<p>The <code dir="ltr" translate="no">        $group       </code> stage in aggregations is supported whereas the group command isn't.</p></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       mapReduce      </code></td>
<td>No</td>
</tr>
</tbody>
</table>

### Authentication

<table>
<thead>
<tr class="header">
<th><strong>Command</strong></th>
<th><strong>Supported</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       authenticate      </code></td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       getnonce      </code></td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       logout      </code></td>
<td>No</td>
</tr>
</tbody>
</table>

### Query and write operations

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Command</strong></th>
<th><strong>Supported</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       watch      </code> (Change Streams)</td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       delete      </code></td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       eval      </code></td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       find      </code></td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       findAndModify      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       getLastError      </code></td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       getMore      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       getPrevError      </code></td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       GridFS      </code></td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       insert      </code></td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       parallelCollectionScan      </code></td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       replaceOne      </code></td>
<td><p>No</p>
<p>The <code dir="ltr" translate="no">        replaceOne       </code> driver method is supported with the <code dir="ltr" translate="no">        update       </code> command.</p></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       resetError      </code></td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       update      </code></td>
<td>Yes</td>
</tr>
</tbody>
</table>

### Session commands

<table>
<thead>
<tr class="header">
<th><strong>Command</strong></th>
<th><strong>Supported</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       abortTransaction      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       commitTransaction      </code></td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       endSessions      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       killAllSessions      </code></td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       killAllSessionsByPattern      </code></td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       killSessions      </code></td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       refreshSessions      </code></td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       startSession      </code></td>
<td><p>Sessions can be started using the <code dir="ltr" translate="no">        startSession       </code> driver method.</p></td>
</tr>
</tbody>
</table>

## Administrative commands

Firestore with MongoDB compatibility supports the following administrative commands.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Command</strong></th>
<th><strong>Supported</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       cloneCollectionAsCapped      </code></td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       collMod      </code></td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       collMod: expireAfterSeconds      </code></td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       convertToCapped      </code></td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       copydb      </code></td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       create      </code></td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       createIndex      </code></td>
<td><p>Yes</p>
<p>To create indexes, see <a href="/firestore/mongodb-compatibility/docs/indexing">Manage indexes</a> .</p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       createIndexes      </code></td>
<td><p>Yes</p>
<p>To create indexes, see <a href="/firestore/mongodb-compatibility/docs/indexing">Manage indexes</a> .</p></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       createView      </code></td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       currentOp      </code></td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       drop      </code></td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       dropDatabase      </code></td>
<td><p>No</p>
<p>To delete a database, see <a href="/firestore/mongodb-compatibility/docs/create-databases#delete-database">Delete a database</a> .</p></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       dropIndex      </code></td>
<td><p>Yes</p>
<p>To delete indexes, see <a href="/firestore/mongodb-compatibility/docs/indexing">Manage indexes</a> .</p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       dropIndexes      </code></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       filemd5      </code></td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       getAuditConfig      </code></td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       killCursors      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       killOp      </code></td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       listCollections      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       listDatabases      </code></td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       listIndexes      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       reIndex      </code></td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       renameCollection      </code></td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       setAuditConfig      </code></td>
<td>No</td>
</tr>
</tbody>
</table>

### Diagnostic commands

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Command</strong></th>
<th><strong>Supported</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       buildInfo      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       collStats      </code></td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       connectionStatus      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       connPoolStats      </code></td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       dataSize      </code></td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       dbHash      </code></td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       dbStats      </code></td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       explain      </code></td>
<td><p>Yes</p>
<p>For behavior differences and limitations, see <a href="/firestore/mongodb-compatibility/docs/query-explain#explain-command">Query Explain</a></p></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       features      </code></td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       hello      </code></td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       hostInfo      </code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       listCommands      </code></td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       profiler      </code></td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       serverStatus      </code></td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       top      </code></td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       whatsmyuri      </code></td>
<td>No</td>
</tr>
</tbody>
</table>

### Role management commands

To manage database access, Firestore with MongoDB compatibility supports [Identity and Access Management roles and permissions](/firestore/mongodb-compatibility/docs/security/iam) .

<table>
<thead>
<tr class="header">
<th><strong>Command</strong></th>
<th><strong>Supported</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       createRole      </code></td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       dropAllRolesFromDatabase      </code></td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       dropRole      </code></td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       grantRolesToRole      </code></td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       revokePrivilegesFromRole      </code></td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       revokeRolesFromRole      </code></td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       rolesInfo      </code></td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       updateRole      </code></td>
<td>No</td>
</tr>
</tbody>
</table>

## What's next

  - Run the [Quickstart: Create a database and connect to it](/firestore/mongodb-compatibility/docs/create-and-query-database) .
  - Learn about [Behavior differences](/firestore/mongodb-compatibility/docs/behavior-differences) .
