Firestore in Datastore mode point-in-time recovery (PITR) provides protection against accidental deletion or writes. PITR maintains versions of your entities from past timestamps. For example, in the case of a developer pushing the incorrect data, accidental deletes or writes, PITR can recover the data to a point in time in the past (up to a maximum of 7 days) seamlessly.

For any live database that follows [Best practices](./best-practices) , use of PITR doesn't affect the performance of reads or writes.

## PITR window

After you enable PITR, Datastore mode starts retaining PITR data. PITR data is retained for 7 days in the PITR window.

You can read data for a timestamp based on when PITR was enabled:

<table>
<thead>
<tr class="header">
<th>PITR enablement status</th>
<th>Earliest PITR data available</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Disabled</td>
<td>1 hour before the time of read request</td>
<td></td>
</tr>
<tr class="even">
<td>enabled within 7 days</td>
<td>1 hour before PITR was enabled</td>
<td></td>
</tr>
<tr class="odd">
<td>enabled more than 7 days ago</td>
<td>7 days before the time of read request</td>
<td></td>
</tr>
</tbody>
</table>

**Note:** You can't start reading from seven days in the past immediately after you enable PITR.

A single version per minute is retained in the PITR window. You can read documents at minute granularity using a whole minute timestamp. Only one version of a document is retained in case of multiple writes. For example, if a document had multiple writes ranging from `  v1, v2, ... vk  ` between `  2023-05-30 09:00:00AM  ` (exclusive) and `  2023-05-30 09:01:00AM  ` (inclusive) timestamp, a read request at timestamp `  2023-05-30 09:01:00AM  ` returns the `  vk  ` version of the document.

You can read from the data created during the PITR window. The data is stored at a minute granularity and you can recover data at the same granularity. Datastore mode PITR feature is disabled by default.

The [earliestVersionTime](/firestore/docs/reference/rest/v1/projects.databases#resource:-database) field of your database specifies the earliest permissible read time for your data.

Regardless of whether PITR is enabled or not, you can read (but not export) documents at any microsecond-granularity timestamp within the past hour, but not before the earliestVersionTime.

## Ways to recover data

There are two ways to recover data:

  - To **recover a portion of the database** , perform a [stale read](/firestore/docs/understand-reads-writes-scale#stale_reads) specifying a query-condition or using direct key lookup along with a timestamp in the past, and then write the results back into the live database. This is typically used for surgical operations on a live database. For example, if you accidentally delete a particular entity or incorrectly update a subset of data, you can recover it with this method. For instructions, see [recovering a portion of your database](/datastore/docs/use-pitr#read-pitr) .

  - To **recover the entire database** , use one of the following options:
    
      - [Clone the database](/datastore/docs/manage-databases#clone-database) to create a copy of the database at a specific timestamp.
    
      - [Export](/datastore/docs/use-pitr#export-import) the database and specify a timestamp in the past and then import it to a new database. The PITR export operation supports all filters, including export of all entities and export of specific kinds and namespaces.
    
    You can clone or export PITR data where the timestamp is a whole minute timestamp within the past seven days, but not earlier than the `  earliestVersionTime  ` .

## Pricing

Consider the following pricing information before you enable PITR for your database:

  - Storage: Datastore mode measures the database size daily. Over the period of a month, these sample points are averaged to calculate the database storage size. This average value is multiplied by the unit price of PITR (GB-month). See the [storage pricing](/firestore/pricing) for more information.
    
    PITR storage doesn't have a free tier and you must have billing enabled if you want to use PITR.

  - Compute billing: Any queries that you make during the PITR window of 7 days, either through stale reads or exports, incur read operation costs based on the number of documents read. See [pricing](/firestore/pricing) for more information.

  - Minimum billing: You may be charged up to 1 day of PITR storage cost even if you disable PITR within a day after enablement.

## What's next

  - Learn more about how to [recover data with PITR](/datastore/docs/use-pitr) .
