With GQL, you can write SQL-like queries for Firestore in Datastore mode. GQL maps roughly to SQL: you can think of a GQL `  kind  ` as a SQL table, a GQL `  entity  ` as a SQL row, and a GQL `  property  ` as a SQL column. However, a SQL row-column lookup is limited to a single value, whereas in GQL a property can be a multiple value property.

The following Cloud Client Libraries for Firestore in Datastore mode support GQL:

  - [C\#](/dotnet/docs/reference/Google.Cloud.Datastore.V1/latest/Google.Cloud.Datastore.V1.GqlQuery)
  - [Java](/java/docs/reference/google-cloud-datastore/latest/com.google.cloud.datastore.GqlQuery)
  - [PHP](https://googleapis.github.io/google-cloud-php/#/docs/google-cloud/latest/datastore/query/gqlquery)
  - [Ruby](/ruby/docs/reference/google-cloud-datastore/latest/Google-Cloud-Datastore-GqlQuery)

## GQL Versions

You need different versions of GQL depending on where you run queries. There are two GQL references:

  - GQL Reference, for the GQL grammar used in the v1 and v1beta3 versions of the Datastore API and in the [Google Cloud console Datastore Viewer](https://console.cloud.google.com/project/_/datastore/entities/query?queryType=gql) (use the reference on this page).

  - [GQL for the Python NDB and DB client libraries](/appengine/docs/python/datastore/gqlreference) , for the GQL grammar used in the NDB and DB client libraries.

## Grammar

The GQL grammar is summarized as follows:

``` text
<aggregation_query> := 
(
    SELECT ( <aggregation>+, )
    [ FROM <kind> ]
    [ WHERE <compound-condition> ]
|
    AGGREGATE ( <aggregation>+, )
    OVER 
      "("
        <query> 
      ")"
)

<aggregation> := ( COUNT "(" "*" ")"
                 | COUNT_UP_TO "(" <integer-literal> ")"
                 | SUM "(" <property-name> ")"
                 | AVG "(" <property-name> ")" )
                 [ AS <alias> ]

<alias> := <name>

<query> :=
SELECT ( "*"
       | <property-name>+,
       | DISTINCT <property-name>+,
       | DISTINCT ON "(" <property-name>+, ")" "*"
       | DISTINCT ON "(" <property-name>+, ")" <property-name>+, )

[ FROM <kind> ]
[ WHERE <compound-condition> ]
[ ORDER BY ( <property-name> [ ASC | DESC ] )+,  ]
[ LIMIT ( <result-position> |
          FIRST "(" <result-position> ,
                    <result-position> ")" ) ]
[ OFFSET <result-position> [ "+" <result-position> ] ]

<compound-condition> :=
  <condition> AND <compound-condition>
| <condition> OR <compound-condition>
| "(" <compound-condition> ")"
| <condition>

<condition> :=
  <property-name> IS NULL
| <property-name> <forward-comparator> <value>
| <value> <backward-comparator> <property-name>

<forward-comparator> :=
  <either-comparator>
| CONTAINS
| HAS ANCESTOR
| IN
| NOT IN

<backward-comparator> :=
  <either-comparator>
| IN
| HAS DESCENDANT

<either-comparator> :=
  =
| <
| <=
| >
| >=
| !=

<result-position> := <binding-site> | <integer-literal>

<value> :=
  <binding-site>
| <synthetic-literal>
| <string-literal>
| <integer-literal>
| <double-literal>
| <boolean-literal>
| <null-literal>

<synthetic-literal> :=
  KEY "("
    [ "PROJECT" "(" <string-literal> ")" "," ]
    [ "NAMESPACE" "(" <string-literal> ")" "," ]
    <key-path-element>+, ")"
| ARRAY "(" <value>+, ")"
| BLOB "(" <string-literal> ")"
| DATETIME "(" <string-literal> ")"

<key-path-element> :=
  <kind> "," ( <integer-literal> | <string-literal> )

<kind> := <name>

<property-name> := <name>+.
```

In the above grammar list, note that:

  - The symbol `  +,  ` after an expression indicates that it can be repeated, with repeated expressions separated by a comma.
  - The boolean `  AND  ` operator has higher precedence than the `  OR  ` operator. For example, a clause like `  a OR b AND c  ` parses to `  a OR (b AND c)  ` , and parenthesis would need to be used to achieve `  (a OR b) AND c  ` .

The following are some examples that return entire entities:

``` text
    SELECT * FROM myKind WHERE myProp >= 100 AND myProp < 200
    SELECT * FROM myKind LIMIT 50 OFFSET @startCursor
    SELECT * FROM myKind ORDER BY myProp DESC
```

Every GQL query string always begins with `  SELECT <something>  ` , where `  <something>  ` is one of the following:

  - `  *  `
  - `  <property-list>  ` , a comma delimited list of properties to be returned from the query.
  - `  __key__  ` , which returns keys only.

Similar to SQL, GQL keywords are case insensitive. Kind and property names are case sensitive.

**Note:** When a query string consists of `  SELECT <property-list>  ` , the query is a [projection query](/datastore/docs/concepts/queries#projection_queries) .

A GQL query returns zero or more entity results of the requested kind, with each result consisting of an entire entity or some subset of the properties of the entity, or even just the entity [key](/datastore/docs/concepts/entities) . For example,

  - `  SELECT * FROM myKind  `
  - `  SELECT __key__ FROM myKind  `
  - `  SELECT title, year FROM Song WHERE composer = 'Lennon, John'  `

A result list produced by `  SELECT *  ` or `  SELECT __key__  ` never contains duplicates. A result list produced by `  SELECT <property-list>  ` may contain multiple results from one entity, typically when any of those properties are multiple value properties.

You can also use fully-qualified property names, in the form of `  <kind>.<property>  ` . This statement:

``` text
SELECT Person.name FROM Person
```

is identical to:

``` text
SELECT name FROM Person
```

If a property name begins with the name of its kind followed by a ".", you must fully qualify the property name in GQL. For example, given a kind named `  Product  ` that has a property named `  Product.Name  ` , you can retrieve matching results using:

``` text
SELECT Product.Product.Name FROM Product
```

But this would not match any results:

``` text
SELECT Product.Name FROM Product
```

**Tip:** `  SELECT __key__  ` or `  SELECT <property-list>  ` queries are faster than `  SELECT *  ` queries, and are cheaper, because they are charged at the less expensive [small operations](/datastore/docs/pricing) rates, rather than at the read rates. See also [projection queries](/datastore/docs/concepts/queries#projection_queries) .

Only `  SELECT  ` is supported by GQL, you must use a [client library](/datastore/docs/reference/libraries) or the [API](/datastore/docs/reference/data/rest) for mutation operations.

## Clauses

The following optional `  SELECT  ` clauses are recognized:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Clause</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       DISTINCT      </code></td>
<td>Specifies that only completely unique results will be returned. Normally used only with <a href="/datastore/docs/concepts/queries#projection_queries">projection queries</a> because non-projection queries return unique results. If you use <code dir="ltr" translate="no">       DISTINCT      </code> in a projection query where more than one entity has the same values in the properties being projected, only the first result is returned.
<p>Note that a query string can use either <code dir="ltr" translate="no">        DISTINCT       </code> or <code dir="ltr" translate="no">        DISTINCT ON       </code> , but not both.</p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       DISTINCT ON      </code></td>
<td>Specifies that only the first result for each distinct combination of values for the specified properties will be returned. Used only with <a href="/datastore/docs/concepts/queries#projection_queries">projection queries</a> . The properties specified in the <code dir="ltr" translate="no">       DISTINCT ON      </code> clause must be a subset of the properties specified for the projection. <code dir="ltr" translate="no">       DISTINCT ON      </code> allows you to specify that only part of the projection is required to be distinct.
<code dir="ltr" translate="no">       SELECT DISTINCT a, b, c      </code> is identical to <code dir="ltr" translate="no">       SELECT DISTINCT ON (a, b, c) a, b, c      </code>
<p>Note that a query string can use either <code dir="ltr" translate="no">        DISTINCT       </code> or <code dir="ltr" translate="no">        DISTINCT ON       </code> , but not both.</p></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       FROM      </code></td>
<td>Limits the result set to those entities of the given kind. A query string without a <code dir="ltr" translate="no">       FROM      </code> clause is called a <em>kindless query</em> and the only condition allowed in the <code dir="ltr" translate="no">       WHERE      </code> clause is one that specifies a <code dir="ltr" translate="no">       __key__      </code> property.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       WHERE      </code></td>
<td>Limits the result set to those entities that meet one or more conditions. Each condition compares a property of the entity with a value using a comparison operator. If multiple conditions are combined with the <code dir="ltr" translate="no">       AND      </code> keyword, then an entity must meet all of the conditions to be returned by the query. GQL does not have an <code dir="ltr" translate="no">       OR      </code> operator.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       ORDER BY      </code></td>
<td>Causes results to be sorted by the specified properties. The <code dir="ltr" translate="no">       ORDER BY      </code> clause can specify multiple sort orders as a comma-delimited list, evaluated from left to right. Specify <code dir="ltr" translate="no">       ASC      </code> for ascending or <code dir="ltr" translate="no">       DESC      </code> for descending order. Note that the order is applied to each property. If the direction is not specified, it defaults to <code dir="ltr" translate="no">       ASC      </code> . If no <code dir="ltr" translate="no">       ORDER BY      </code> clause is specified, the order of the results is undefined and may change over time.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       LIMIT      </code></td>
<td>Limits query results to a count, to results preceding a cursor, or both. Often used to page through results of a query. If LIMIT has two <code dir="ltr" translate="no">       &lt;result-position&gt;      </code> s, one must be a cursor and the other must be an integer. (Note that <code dir="ltr" translate="no">       OFFSET      </code> and <code dir="ltr" translate="no">       LIMIT      </code> are independent.)</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       OFFSET      </code></td>
<td>Specifies offsets into the result set: either a cursor, or a count, or both. If <code dir="ltr" translate="no">       OFFSET      </code> has two <code dir="ltr" translate="no">       &lt;result-position&gt;      </code> s, the left one must be a cursor and the right one must be an integer. Note that an <code dir="ltr" translate="no">       OFFSET      </code> with an integer starts at the beginning or at the cursor, then discards the specified number of entities, and so you still incur the cost of reading those entities. (Note also that <code dir="ltr" translate="no">       OFFSET      </code> and <code dir="ltr" translate="no">       LIMIT      </code> are independent.)</td>
</tr>
</tbody>
</table>

## How to form entity and property names

Kind and property names are formed as follows:

  - With any sequence of letters, digits, underscores, dollar signs, or unicode characters in the range from `  U+0080  ` to `  U+FFFF  ` (inclusive), so long as the name does not begin with a digit. For example, `  foo  ` , `  bar17  ` , `  x_y  ` , `  big$bux  ` , `  __qux__  ` .

  - You can also use a non-empty backquoted string: ``  `fig-bash`  `` or ``  `x.y`  `` . A backquote character can be represented in a backquoted name by doubling it, for example, ```  `silly``putty`  ``` . A backquoted name can contain [escaped characters](#how_to_escape_characters) .

  - An unquoted name can match a predefined name, but must not match a keyword. A backquoted name can contain any character except a newline. (It can contain a newline via `  \n  ` , but not as a raw newline.)

  - Names are case-sensitive.

## How to form literals

You can use the following literals in a comparison:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Literal Type</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       string      </code></td>
<td>Formed following these rules:
<ul>
<li>Can be a single-quoted or double-quoted string, such as <code dir="ltr" translate="no">         'foo'        </code> or <code dir="ltr" translate="no">         "foo"        </code> .</li>
<li>A <code dir="ltr" translate="no">         '        </code> character may be represented in a single-quoted string and a <code dir="ltr" translate="no">         "        </code> character may be represented in a double-quoted string by doubling it: <code dir="ltr" translate="no">         'Joe''s Diner'        </code> or <code dir="ltr" translate="no">         "Expected ""."        </code> .</li>
<li>Can contain <code dir="ltr" translate="no">         \        </code> -escaped characters.</li>
<li>Can contain any character except a newline.</li>
</ul></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       integer      </code></td>
<td>A sequence of decimal digits with the following options or characteristics:
<ul>
<li>An optional initial plus or minus character.</li>
<li>Must be representable as a signed 64 bit integer.</li>
<li>Examples: <code dir="ltr" translate="no">         0        </code> , <code dir="ltr" translate="no">         11        </code> , <code dir="ltr" translate="no">         +5831        </code> , <code dir="ltr" translate="no">         -37        </code> , or <code dir="ltr" translate="no">         3827438927        </code> .</li>
</ul></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       double      </code></td>
<td>A sequence of decimal digits with the following options or characteristics:
<ul>
<li>An optional initial plus or minus character.</li>
<li>Contains either a decimal point or an exponent consisting of the letter <code dir="ltr" translate="no">         E        </code> (or <code dir="ltr" translate="no">         e        </code> ) with an optional plus or minus character.</li>
<li>Must be representable as an IEEE 64 bit floating point number.</li>
<li>Examples: <code dir="ltr" translate="no">         0.0        </code> , <code dir="ltr" translate="no">         +58.31        </code> , <code dir="ltr" translate="no">         -37.0        </code> , <code dir="ltr" translate="no">         3827438927.0        </code> , <code dir="ltr" translate="no">         -3.        </code> , <code dir="ltr" translate="no">         +.1        </code> , <code dir="ltr" translate="no">         314159e-5        </code> , or <code dir="ltr" translate="no">         6.022E23        </code> .</li>
</ul></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       boolean      </code></td>
<td>Can be the values <code dir="ltr" translate="no">       TRUE      </code> or <code dir="ltr" translate="no">       FALSE      </code> , case-insensitive.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       null      </code></td>
<td>Represents <code dir="ltr" translate="no">       NULL      </code> . Case insensitive.</td>
</tr>
</tbody>
</table>

## Synthetic literals

A synthetic literal is a value that is constructed by a function. The following table lists the supported synthetic literals:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Literal Name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>KEY</td>
<td><code dir="ltr" translate="no">       KEY([PROJECT(&lt;project&gt;),] [NAMESPACE(&lt;namespace&gt;),] &lt;key-path-element&gt;*,)      </code> represents a key.<br />
<br />
If <code dir="ltr" translate="no">       &lt;project&gt;      </code> and <code dir="ltr" translate="no">       &lt;namespace&gt;      </code> are not supplied, defaults from the current query context are used. Entities are partitioned into various subsets, each used by different projects and different namespaces within a project and so forth, with an ID (partition ID) assigned to each entity subset. The <code dir="ltr" translate="no">       &lt;key-path-element&gt;      </code> is an <a href="/datastore/docs/concepts/entities#ancestor_paths">entity path</a> , which is an even-length comma-separated list of kinds alternating with either integer ids or string names. The integers must be greater than <code dir="ltr" translate="no">       0      </code> and the strings must not be empty.</td>
</tr>
<tr class="even">
<td>BLOB</td>
<td><code dir="ltr" translate="no">       BLOB(&lt;string&gt;)      </code> represents a blob encoded as <code dir="ltr" translate="no">       &lt;string&gt;      </code> via base-64 encoding with character set <code dir="ltr" translate="no">       [A-Za-z0-9-_]      </code> and no padding.</td>
</tr>
<tr class="odd">
<td>DATETIME</td>
<td><code dir="ltr" translate="no">       DATETIME(&lt;string&gt;)      </code> represents a timestamp. <code dir="ltr" translate="no">       &lt;string&gt;      </code> must be in the time format specified in <a href="http://tools.ietf.org/html/rfc3339">RFC 3339 section 5.6</a> . (However, the second precision is limited to microseconds and leap seconds are omitted.) This standard format is: <code dir="ltr" translate="no">       YYYY-MM-DDThh:mm:ss.SSSSSS+zz:ZZ      </code> where:
<ul>
<li>Year <code dir="ltr" translate="no">         YYYY        </code> is a four digit value between <code dir="ltr" translate="no">         0001        </code> and <code dir="ltr" translate="no">         9999        </code> , inclusive. For example, <code dir="ltr" translate="no">         2013-09-29T09:30:20.00002-08:00        </code></li>
<li>Month <code dir="ltr" translate="no">         MM        </code> must be two digits consisting of values between <code dir="ltr" translate="no">         01        </code> and <code dir="ltr" translate="no">         12        </code> , inclusive. For example, <code dir="ltr" translate="no">         09        </code> .</li>
<li>Day <code dir="ltr" translate="no">         DD        </code> must be two digits consisting of values between <code dir="ltr" translate="no">         01        </code> and <code dir="ltr" translate="no">         31        </code> , inclusive. For example, <code dir="ltr" translate="no">         29        </code> .</li>
<li>Date <code dir="ltr" translate="no">         YYYY-MM-DD        </code> must be a valid date in the Gregorian calendar. For example, <code dir="ltr" translate="no">         February 29, 2013        </code> would be invalid.</li>
<li>Delimiter <code dir="ltr" translate="no">         T        </code> must be <code dir="ltr" translate="no">         T        </code> or <code dir="ltr" translate="no">         t        </code> .</li>
<li>Hour <code dir="ltr" translate="no">         hh        </code> must be two digits consisting of values between <code dir="ltr" translate="no">         0        </code> and <code dir="ltr" translate="no">         23        </code> , inclusive. For example, <code dir="ltr" translate="no">         09        </code> .</li>
<li>Minute <code dir="ltr" translate="no">         mm        </code> and second <code dir="ltr" translate="no">         ss        </code> both must be two digits consisting of values between <code dir="ltr" translate="no">         0        </code> and <code dir="ltr" translate="no">         59        </code> , inclusive.</li>
<li><code dir="ltr" translate="no">         SSSSSS        </code> represents a fraction of a second:
<ul>
<li>It may be omitted, in which case <code dir="ltr" translate="no">           .          </code> must also be omitted. Otherwise...</li>
<li>The value must consist of one to six digits.</li>
</ul></li>
<li><code dir="ltr" translate="no">         +zz:ZZ        </code> represents an offset (or time zone). For example, the Pacific time zone has an offset of <code dir="ltr" translate="no">         -08:00        </code> .
<ul>
<li>It may be entirely replaced by <code dir="ltr" translate="no">           Z          </code> or <code dir="ltr" translate="no">           z          </code> to represent offset <code dir="ltr" translate="no">           0          </code> . Otherwise…</li>
<li>Offset sign <code dir="ltr" translate="no">           +          </code> must be <code dir="ltr" translate="no">           +          </code> or <code dir="ltr" translate="no">           -          </code> .</li>
<li>Offset hour <code dir="ltr" translate="no">           zz          </code> has the same limitations as hour <code dir="ltr" translate="no">           hh          </code> .</li>
<li>Offset minute <code dir="ltr" translate="no">           ZZ          </code> has the same limitations as minute <code dir="ltr" translate="no">           mm          </code> .</li>
<li>Neither <code dir="ltr" translate="no">           +00:00          </code> nor <code dir="ltr" translate="no">           -00:00          </code> are valid offsets.</li>
</ul></li>
</ul></td>
</tr>
</tbody>
</table>

## How to escape characters

You can escape certain characters in string literals and backquoted names. The escaped characters are case sensitive: for example `  \r  ` is valid while `  \R  ` is not.

The following is a list of all the characters that can be escaped in GQL:

<table>
<thead>
<tr class="header">
<th>Character</th>
<th>Escaped</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>backslash character</td>
<td><code dir="ltr" translate="no">       \\      </code></td>
</tr>
<tr class="even">
<td>null character</td>
<td><code dir="ltr" translate="no">       \0      </code></td>
</tr>
<tr class="odd">
<td>backspace character</td>
<td><code dir="ltr" translate="no">       \b      </code></td>
</tr>
<tr class="even">
<td>newline character</td>
<td><code dir="ltr" translate="no">       \n      </code></td>
</tr>
<tr class="odd">
<td>return character</td>
<td><code dir="ltr" translate="no">       \r      </code></td>
</tr>
<tr class="even">
<td>tab character</td>
<td><code dir="ltr" translate="no">       \t      </code></td>
</tr>
<tr class="odd">
<td>the character with decimal code 26</td>
<td><code dir="ltr" translate="no">       \Z      </code></td>
</tr>
<tr class="even">
<td>single quotation mark</td>
<td><code dir="ltr" translate="no">       \'      </code></td>
</tr>
<tr class="odd">
<td>double quotation mark</td>
<td><code dir="ltr" translate="no">       "      </code></td>
</tr>
<tr class="even">
<td>backquote character</td>
<td><code dir="ltr" translate="no">       \`      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       \%      </code> (2 characters, retaining the backslash, per MySQL)</td>
<td><code dir="ltr" translate="no">       \%      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       \_      </code> (2 characters, retaining the backslash, per MySQL)</td>
<td><code dir="ltr" translate="no">       \_      </code></td>
</tr>
</tbody>
</table>

## Operators and comparisons

Comparators are either equivalence comparators: `  =  ` , `  IN  ` , `  CONTAINS  ` , `  = NULL  ` , `  HAS ANCESTOR  ` , and `  HAS DESCENDANT  ` , or inequality comparators: `  <  ` , `  <=  ` , `  >  ` , `  >=  ` , `  !=  ` , `  NOT IN  ` .

Notice that the operator `  =  ` is another name for the `  IN  ` and `  CONTAINS  ` operators. For example, `  <value> = <property-name>  ` is the same as `  <value> IN <property-name>  ` , and `  <property-name> = <value>  ` is the same as `  <property-name> CONTAINS <value>  ` . Also `  <property-name> IS NULL  ` is the same as `  <property-name> = NULL  ` .

A condition can also test whether one entity has another entity as an ancestor, using the `  HAS ANCESTOR  ` or `  HAS DESCENDANT  ` operators. These operators test ancestor relationships between keys. For `  HAS ANCESTOR  ` , the left operand must be `  __key__  ` and the right operand must be a key value. For `  HAS DESCENDANT  ` , the left operand must be a key value and the right operand must be `  __key__  ` . For more information on ancestor relationships, see [ancestor paths](/datastore/docs/concepts/entities#ancestor_paths) .

Only one property may be compared with inequality operators. When a query with an `  ORDER BY  ` clause applies an inequality operator to a property, that property must be the first property in the `  ORDER BY  ` clause.

A typical property name consists of alphanumeric characters optionally mixed with underscore ( `  _  ` ) and dollar sign ( `  $  ` ). In other words, they match the regular expression `  [a-zA-Z0-9_$]+(.[0-9_$]+)*  ` . Property names containing other printable characters must be quoted with backquotes, for example: ``  `first-name`  `` .

### Restrictions

Comparisons must be between a property name and a literal, but these can be on either side of the operator. For example, `  A < 7  ` or `  7 > A  ` . Note, however, that there is no inverse operator for IS NULL, so while you can have `  <property-name> IS NULL  ` , you cannot have `  NULL IS <property-name>  ` .

There is no way to determine whether an entity lacks a value for a property (that is, whether the property has no value). If you use a condition of the form `  property = NULL  ` , what will occur is a check whether a null value is explicitly stored for that property. Datastore queries that refer to a property will never return entities that don't have a value for that property.

## Aggregations

Firestore in Datastore mode supports the following aggregations:

`  COUNT(*)  `

`  COUNT_UP_TO()  `

`  SUM()  `

`  AVG()  `

In GQL, you can write aggregations in either a pipelined form or a simplified form. Each aggregate can have an optional alias.

The simplified form is a shortcut and supports only `  FROM  ` and `  WHERE  ` clauses. To use aggregations over a query with `  ORDER BY  ` , `  LIMIT  ` , or `  OFFSET  ` clauses, you must use the pipelined form.

### `     COUNT(*)    ` and `     COUNT_UP_TO()    `

Use the `  COUNT(*)  ` aggregation to return the total number of entities that match a given query. `  COUNT_UP_TO(n)  ` is a mutation of `  COUNT(*)  ` where the counting stops after it reaches `  n  ` .

#### Pipelined form

Use the `  AGGREGATE  ` keyword over a regular entity query.

``` text
AGGREGATE COUNT(*) OVER ( SELECT * FROM tasks WHERE is_done = false AND tag = 'house' )
AGGREGATE COUNT_UP_TO(5) OVER ( SELECT * FROM tasks WHERE is_done = false AND tag = 'house' )
```

Or over a more complicated base query:

``` text
AGGREGATE COUNT(*) AS total
OVER (
    SELECT * FROM tasks WHERE is_done = true
    LIMIT 5 OFFSET 10
)

AGGREGATE COUNT_UP_TO(5) AS total
OVER (
    SELECT * FROM tasks WHERE is_done = true
    LIMIT 5 OFFSET 10
)
```

#### Simplified form

``` text
SELECT COUNT(*) AS total
FROM tasks
WHERE is_done = false AND tag = 'house'

SELECT COUNT_UP_TO(5) AS total
FROM tasks
WHERE is_done = false AND tag = 'house'
```

### `     SUM()    ` and `     AVG()    `

Use the `  SUM()  ` aggregation to return the sum of the values of the requested property. Use the `  AVG()  ` aggregation to return the average of the values of the requested property.

#### Pipelined form

Use the `  AGGREGATE  ` keyword over a regular entity query.

``` text
AGGREGATE SUM(hours) OVER ( SELECT * FROM tasks WHERE is_done = false AND tag = 'house' )
AGGREGATE AVG(hours) OVER ( SELECT * FROM tasks WHERE is_done = false AND tag = 'house' )
```

Or over a more complicated base query:

``` text
AGGREGATE SUM(hours) AS total_hours
    OVER (
    SELECT * FROM tasks WHERE is_done = true
    LIMIT 5 OFFSET 10
)

AGGREGATE AVG(hours) AS average_hours
OVER (
    SELECT * FROM tasks WHERE is_done = true
    LIMIT 5 OFFSET 10
)
```

#### Simplified form

``` text
SELECT SUM(hours) AS total_hours
FROM tasks
WHERE is_done = false AND tag = 'house'

SELECT AVG(hours) AS average_hours
FROM tasks
WHERE is_done = false AND tag = 'house'
```

### Multiple Aggregations

Multiple aggregations can be combined. For example:

``` text
AGGREGATE
    SUM(hours) AS total_hours,
    AVG(hours) AS average_hours,
    COUNT(*) AS total_tasks
OVER (
    SELECT *
    FROM tasks
    WHERE is_done = false AND tag = 'house'
)
```

## Tips about GQL behavior

The following table highlights some important aspects of GQL literal values and operators:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Behavior</th>
<th>Example</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>An integer value is not equal to the <em>equivalent</em> double: for example <code dir="ltr" translate="no">       4      </code> is not equal to <code dir="ltr" translate="no">       4.0      </code></td>
<td><code dir="ltr" translate="no">       SELECT * FROM Task WHERE priority = 4.0      </code> will never yield a <code dir="ltr" translate="no">       Task      </code> with <code dir="ltr" translate="no">       priority      </code> set to a value of <code dir="ltr" translate="no">       4      </code> ; <code dir="ltr" translate="no">       SELECT * WHERE percent_complete = 50      </code> will never yield a <code dir="ltr" translate="no">       Task      </code> with <code dir="ltr" translate="no">       percent_complete      </code> set to a value of <code dir="ltr" translate="no">       50.0      </code> .</td>
</tr>
<tr class="even">
<td>Null is a value, not the absence of a value.</td>
<td>There is no way to determine whether an entity lacks a value for a property (that is, whether the property has no value). If you use a condition of the form <code dir="ltr" translate="no">       nonexistent = NULL      </code> , what will occur is a check whether a null value is explicitly stored for that property. For example, <code dir="ltr" translate="no">       SELECT * FROM Task WHERE nonexistent = NULL      </code> will never yield an entity with no value set for property <code dir="ltr" translate="no">       nonexistent      </code> .</td>
</tr>
<tr class="odd">
<td>A <code dir="ltr" translate="no">       +      </code> immediately followed by an integer literal without a sign, for example <code dir="ltr" translate="no">       +17      </code> , is always interpreted as an explicitly positive integer, and never as a <code dir="ltr" translate="no">       +      </code> and an implicitly positive integer. When the latter interpretation is desired, include whitespace between the <code dir="ltr" translate="no">       +      </code> and the integer literal.</td>
<td><ul>
<li><code dir="ltr" translate="no">         OFFSET @cursor + 17        </code> is valid</li>
<li><code dir="ltr" translate="no">         OFFSET @cursor + +17        </code> is valid</li>
<li><code dir="ltr" translate="no">         OFFSET @cursor +17        </code> is invalid</li>
</ul></td>
</tr>
<tr class="even">
<td>The operator <code dir="ltr" translate="no">       =      </code> functions like the <a href="#operators_and_comparisons">IN or CONTAINS</a> operators, which can yield some surprising results, especially when used with multi-valued properties.</td>
<td><code dir="ltr" translate="no">       SELECT * FROM Task WHERE tags = 'fun' AND tags = 'programming'      </code> might be expected never to yield any entities, but it is interpreted as <code dir="ltr" translate="no">       SELECT * FROM Task WHERE tags CONTAINS 'fun' AND tags CONTAINS 'programming'      </code> which may certainly yield entities.</td>
</tr>
</tbody>
</table>

## Examples

To find all of the entities of kind `  Person  ` whose ages are between 18 and 35, use this query string:

``` text
SELECT * FROM Person WHERE age >= 18 AND age <= 35
```

To find the three entities of kind `  Person  ` whose ages are the greatest, use this query string:

``` text
SELECT * FROM Person ORDER BY age DESC LIMIT 3
```

To return only the `  name  ` property for each `  Person  ` , use this query string:

``` text
SELECT name FROM Person
```

To return only the `  name  ` property for each `  Person  ` , ordered by `  age  ` , use this query string:

``` text
SELECT name FROM Person ORDER BY age
```

To find the keys of the entities of kind `  Person  ` that have an age of `  NULL  ` , use this query string:

``` text
SELECT __key__ FROM Person WHERE age = NULL
```

To find all the entities, regardless of kind, that are in Amy's [entity group](/datastore/docs/concepts/entities#entity_groups) (i.e. Amy and Fred), use this strongly consistent ancestor query:

``` text
SELECT * WHERE __key__ HAS ANCESTOR KEY(Person, 5629499534213120)
```

In the example above, 5629499534213120 is an auto-generated numeric ID for the `  Person  ` entity that represents Amy. It would return all descendants and the root entity. If you created an entity with a custom name such as 'Amy' for the ID instead of using an auto-generated numeric value, use this strongly consistent query:

``` text
SELECT * WHERE __key__ HAS ANCESTOR KEY(Person, 'Amy')
```

## Unsupported features and behavior differences from MySQL/Python GQL

If you are familiar with MySQL or the Python GQL provided by Google App Engine, you might want to take a look at the following lists, which highlight the main differences between those products and the Datastore GQL behavior.

### MySQL Differences

  - MySQL supports only `  LIMIT  ` / `  OFFSET  ` *counts* . Datastore GQL also supports `  LIMIT  ` / `  OFFSET  ` *cursors* .
  - Datastore GQL supports an `  OFFSET  ` without a `  LIMIT  ` , MySQL does not.
  - MySQL supports an offset count via keyword `  LIMIT  ` , Datastore GQL does not.
  - A MySQL literal string can contain a raw newline. A Datastore GQL literal string cannot.
  - A MySQL literal string can `  \  ` -escape any character. A Datastore GQL literal string can only `  \  ` -escape a specified list of [characters](#how_to_escape_characters) .
  - A MySQL name can begin with a digit. A Datastore GQL name cannot.
  - A Datastore GQL name can contain null characters. A MySQL name cannot.
  - A quoted Datastore GQL name can contain `  \  ` -escaped characters. A quoted MySQL name interprets a `  \  ` as an ordinary character.
  - MySQL has different operators, keywords, and predefined names than Datastore GQL.

### Python GQL for App Engine Differences

The Python NDB and DB App Engine client libraries use a different GQL grammar, see the [GQL Reference for Python NDB/DB](/appengine/docs/standard/python/datastore/gqlreference) . Note the following differences:

  - Python GQL supports operators `  !=  ` and `  OR  ` . Those operators are not supported by Datastore GQL.
  - Datastore GQL supports the `  IN  ` operator [differently](#operators_and_comparisons) .
  - Python GQL supports functions `  DATETIME  ` , `  DATE  ` , `  TIME  ` , `  KEY  ` , `  USER  ` , and `  GEOPT  ` . Datastore GQL supports function `  DATETIME  ` and `  KEY  ` , but with different arguments. Datastore GQL supports function `  BLOB  ` . Datastore GQL does not support `  GEOPT  ` .
  - Python GQL expression `  ANCESTOR IS <entity-or-key-value>  ` is represented in Datastore GQL as the more general expression `  __key__ HAS ANCESTOR <key-value>  ` .
  - Datastore GQL supports the expression `  <property-name> IS NULL  ` . Python GQL does not.
      - Python GQL literal strings are quoted with `  '  ` . Datastore GQL literal strings are quoted with either `  '  ` or `  "  ` .
      - Python GQL names are quoted with `  "  ` . Datastore GQL names are quoted with ``  `  `` .
      - Datastore GQL literal strings and quoted names can contain spaces, return characters, backslashed characters, and the enclosing quote character (doubled). Python GQL literal strings and quoted names cannot have these.
      - Python GQL names may contain `  .  ` without quoting. Datastore GQL reserves `  .  ` for future use.
      - Datastore GQL names may contain `  $  ` and `  U+0080  ` to `  U+FFFF  ` without quoting. Python GQL names may not.
      - Python GQL has different keywords and operators than Datastore GQL.
      - Python GQL supports queries using a URL-safe (base64-encoded) key. Datastore GQL does not.

## When not to use GQL

While GQL provides a convenient way of executing queries in a familiar SQL-like dialect, it does not support `  lookup()  ` of entities. For this capability, use a client library's `  lookup()  ` interface.

## Keywords and predefined names

Keywords and predefined names are case-insensitive.

The following keywords are recognized, although not all of these are currently used in GQL. The unused keywords are marked with an asterisk. To refer to a property name that has the same name as a keyword, surround it with backticks (\`).

<table>
<thead>
<tr class="header">
<th>Keyword</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>AGGREGATE</td>
<td>HAS</td>
</tr>
<tr class="even">
<td>ALL*</td>
<td>HAVING*</td>
</tr>
<tr class="odd">
<td>ANCESTOR</td>
<td>IN</td>
</tr>
<tr class="even">
<td>AND</td>
<td>IS</td>
</tr>
<tr class="odd">
<td>ANY*</td>
<td>JOIN*</td>
</tr>
<tr class="even">
<td>AS*</td>
<td>LIKE*</td>
</tr>
<tr class="odd">
<td>ASC</td>
<td>LIMIT</td>
</tr>
<tr class="even">
<td>AVG</td>
<td>MOD*</td>
</tr>
<tr class="odd">
<td>BETWEEN*</td>
<td>NOT*</td>
</tr>
<tr class="even">
<td>BINARY*</td>
<td>NULL</td>
</tr>
<tr class="odd">
<td>BY</td>
<td>OFFSET</td>
</tr>
<tr class="even">
<td>CHILD*</td>
<td>ON</td>
</tr>
<tr class="odd">
<td>CONTAINS</td>
<td>OR*</td>
</tr>
<tr class="even">
<td>COUNT</td>
<td>ORDER</td>
</tr>
<tr class="odd">
<td>COUNT_UP_TO</td>
<td>PARENT*</td>
</tr>
<tr class="even">
<td>CURSOR*</td>
<td>REGEXP*</td>
</tr>
<tr class="odd">
<td>DESC</td>
<td>RLIKE*</td>
</tr>
<tr class="even">
<td>DESCENDANT</td>
<td>SELECT</td>
</tr>
<tr class="odd">
<td>DISTINCT</td>
<td>SUBSET*</td>
</tr>
<tr class="even">
<td>DIV*</td>
<td>SUM</td>
</tr>
<tr class="odd">
<td>EXISTS*</td>
<td>SUPERSET</td>
</tr>
<tr class="even">
<td>FALSE</td>
<td>TRUE</td>
</tr>
<tr class="odd">
<td>FROM</td>
<td>WHERE</td>
</tr>
<tr class="even">
<td>GROUP</td>
<td>XOR*</td>
</tr>
</tbody>
</table>

The following predefined names are recognized:

<table>
<thead>
<tr class="header">
<th>Predefined Name</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>BLOB</td>
<td>FIRST</td>
</tr>
<tr class="even">
<td>DATETIME</td>
<td>KEY</td>
</tr>
</tbody>
</table>
