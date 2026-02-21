# Billing example

Use this real-world example of a basic chat app to gauge your Firestore in Native Mode usage and costs. This is not an exact estimate, but it can help you better understand how your Firestore in Native Mode usage is billed.

#### Brief review of Firestore in Native Mode billing

Firestore in Native Mode includes a no-cost tier to help you get started at no cost. After you exceed the usage and storage quotas for the no-cost tier, you're charged for the database operations you perform, the data you store, and the network bandwidth you use.

Charges for Firestore in Native Mode usage fall under the following categories:

  - **Operations:** All reads, writes, and deletes have a cost associated with them. Reads include queries, simple fetches, and updates through realtime listeners. You're also charged for any reads required to evaluate Firestore Security Rules you've added to your database. Learn more about [charges for operations in Firestore in Native Mode](/firestore/native/docs/pricing#operations) .
  - **Storage:** You're charged for the data you store in Firestore in Native Mode, including metadata and indexes. Examples of metadata include document names, collection IDs, and field names. Index entries typically include the collection ID, the field values indexed, and the document name. Learn more about [storage costs in Firestore in Native Mode](/firestore/native/docs/pricing#storage) .
  - **Network bandwidth:** Outgoing network bandwidth (or network egress, respectively) costs include connection overhead for your Firestore in Native Mode requests. Incoming network bandwidth (network ingress) is no-cost. Review the [network bandwidth costs](/firestore/native/docs/pricing#network) and monitor your usage to properly plan for bandwidth costs.

For a full, detailed explanation of Firestore in Native Mode costs, see [Firestore in Native Mode Pricing](/firestore/native/docs/pricing) .

## Overview: Costs by usage level

To illustrate typical costs, consider an example chat app, where users can initiate chats with two or more participants. Users can see their active chats in a list, read messages, and send messages. For this example, we're using pricing for the North America multi-region (specifically `  nam5  ` ).

### Assumptions

Consider the following assumptions about usage and data storage:

  - **Daily Active Users (DAUs) are 10% of total app installations.** You can estimate your daily costs using a rough estimate of your Daily Active Users (DAUs). These are the users that actively open and use your app on a given day, which is typically a small subset of your total app installations. For the calculations below, we estimated DAUs as 10% of the total number of app installations.
  - **Document sizes are relatively small.** See the [table below](#document-sizes) for a breakdown of document size by type.
  - **Data is only stored for three months.** The messages in the example chat app are only stored for a three-month period. To account for the delete operations, the calculations below show a daily delete for every daily write.
  - **These cost estimates reflect the bulk of the example app's costs, but not all of them.** We've accounted for the bulk of an app's costs by calculating operations, user and message storage, and egress for the most frequent user tasks outlined in this guide. However, you might need to take into account additional costs, depending on your app's structure and data needs. Use this example to guide your calculations, but refer to the [pricing page](/firestore/pricing) for more thorough explanations of Firestore in Native Mode costs.

For a breakdown of operations by user task, see the [Breakdown: Billed usage by user task](#costs-breakdown) section.

#### Small  
(50k installs)

#### For 50,000 app installs (5,000 Daily Active Users): $12.14/month

Read/Write Costs

**Total monthly cost = $11.10/month**

400K total daily reads

\=

50K No-cost reads + (350K reads at $0.06/100K)

\=

3.5 \* $0.06

**$0.21 / day \* 30 = $6.30**

100K total daily writes

\=

20K No-cost writes + (80K writes at $0.18/100K)

\=

.8 \* $0.18

**$0.14 / day \* 30 = $4.20**

100K total daily deletes

\=

20K No-cost deletes + (80K deletes at $0.02/100K)

\=

.8 \* $0.02

**$0.02 / day \* 30 = $0.60**

Storage/Networking Costs

**Total monthly cost = $1.04/month**

20KB / DAU of daily egress \* 5K DAUs

\=

100MB of daily egress \* 30

\=

3GB monthly network egress

**3 GB No-cost egress = No-cost <sup>1</sup>**

15KB daily message storage / DAU + 3KB storage / install <sup>2</sup>

\=

45KB of storage / DAU \* 5K DAUs

\=

225MB of daily storage / DAU \* 30

\=

6.75GB monthly storage usage

**1GB No-cost storage + (5.75 \* $0.18) = $1.04 / month**

**

<sup>1</sup> 10GB of monthly network egress are no-cost for Firestore in Native Mode.  
<sup>2</sup> Since our assumption is that DAUs are 10% of total app installs, this number accounts for the total number of users that have installed your app.

#### Medium  
(1M installs)

#### For 1,000,000 app installs (100,000 Daily Active Users): $292.02/month

Read/Write Costs

**Total monthly cost = $261.90/month**

8M total daily reads

\=

50K No-cost reads + (7.95M reads at $0.06/100K)

\=

79.5 \* $0.06

**$4.77 / day \* 30 = $143.10**

2M total daily writes

\=

20K No-cost writes + (1.98M writes at $0.18/100K)

\=

19.8 \* $0.18

**$3.56 / day \* 30 = $106.80**

2M total daily deletes

\=

20K No-cost deletes + (1.98M deletes at $0.02/100K)

\=

19.8 \* $0.02

**$0.40 / day \* 30 = $12.00**

Storage/Networking Costs

**Total monthly cost = $30.12/month**

20KB / DAU of daily egress \* 100K DAUs

\=

2GB of daily egress \* 30

\=

60GB monthly network egress

**10 GB No-cost egress + (50GB egress \* $0.12/GB) = $6.00 / month**

15KB daily message storage / DAU + 3KB storage / install <sup>1</sup>

\=

45KB of storage / DAU \* 100K DAUs

\=

4.5GB of daily storage / DAU \* 30

\=

135GB monthly storage usage

**1GB No-cost storage + (134GB \* $0.18/GB) = $24.12 / month**

**

<sup>1</sup> Since our assumption is that DAUs are 10% of total app installs, this number accounts for the total number of users that have installed your app.

#### Large  
(10M installs)

#### For 10,000,000 app installs (1,000,000 Daily Active Users): $2951.52

Read/Write Costs

**Total monthly cost = Total: $2637.90/month**

80M total daily reads

\=

50K No-cost reads + (79.95M reads at $0.06/100K)

\=

799.5 \* $0.06

**$47.97 / day \* 30 = $1439.10**

20M total daily writes

\=

20K No-cost writes + (19.98M writes at $0.18/100K)

\=

199.8 \* $0.18

**$35.96 / day \* 30 = $1078.80**

20M total daily deletes

\=

20K No-cost deletes + (19.98M deletes at $0.02/100K)

\=

199.8 \* $0.02

**$4.00 / day \* 30 = $120.00**

Storage/Networking Costs

**Total monthly cost = $313.62/month**

20KB / DAU of daily egress \* 1M DAUs

\=

20GB of daily egress \* 30

\=

600GB monthly network egress

**10 GB No-cost egress + (590GB egress \* $0.12/GB) = $70.80 / month**

15KB daily message storage / DAU + 3KB storage / install <sup>1</sup>

\=

45KB of storage / DAU \* 1M DAUs

\=

45GB of daily storage / DAU \* 30

\=

1350GB monthly storage usage

**(1GB No-cost storage) + (1349GB \* $0.18/GB) = $242.82 / month**

**

<sup>1</sup> Since our assumption is that DAUs are 10% of total app installs, this number accounts for the total number of users that have installed your app.

A benefit of the Firestore in Native Mode billing model worth considering is that you only pay for what you use. As a result, your bill may grow and shrink with your DAU count.

## Breakdown: Billed usage by user task

For our example chat app, the data structure is as follows:

  - `  users/{userId}  ` — User records
  - `  groups/{groupId}  ` — Chats between 2 or more users
      - `  messages/{messageId}  ` — Each message in a chat.
    
      - 
### Data storage

To calculate the storage costs for storing the app's data, apply the following assumptions about document sizes:

<table>
<thead>
<tr class="header">
<th>Collection</th>
<th>Document Size (in transit)</th>
<th>Document Size (on disk)*</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>users</td>
<td>1KB</td>
<td>3KB</td>
</tr>
<tr class="even">
<td>groups</td>
<td>0.5KB</td>
<td>1.5KB</td>
</tr>
<tr class="odd">
<td>messages</td>
<td>0.25KB</td>
<td>0.75KB</td>
</tr>
</tbody>
</table>

*\*This size calculation includes indexes for the message fields, but assumes indexing is disabled for message content.*

The app also only stores messages that are up to three months old, to lower storage costs.

For more information on calculating storage costs, see [Understanding storage size calculations](/firestore/docs/storage-size) .

### Operations

Users typically complete the following common tasks in the app:

  - [**See the list of chats:**](#see-chats) Users open the home screen of the app and see a list of chats (group and direct) ordered by the most recent message posted.
  - [**Read messages in a chat:**](#read-chats) Users select chats from the home screen and read recent messages from chats.
  - [**Send a message to a chat:**](#send-chats) Users send messages to chats (group or direct).

The example app's total estimated operations in Firestore in Native Mode for the three typical user tasks are as follows:

  - **Reads:** (5 \* 10) + (30) = 80 reads / user / day
  - **Writes:** (10 \* 2) = 20 writes / user / day
  - **Network Egress** : (50 \* 0.25KB) + (30 \* 0.25KB) = 20KB / user / day
  - **Storage** : (20 \* 0.75KB) = 15 KB / user / day

### Total usage by user task

Select each user task to see a full description and breakdown of the operations, storage, and networking costs in the app.

#### See the list of chats

The home screen of the app loads the 25 most recent chats, incurring charges for 25 document reads. Assume that an active user opens the app 5 times per day, totaling 125 reads per user each day. However, more efficient queries, like the one in the following example, can reduce this load.

In the example below, we limit the query to new chats using a timestamp of each successful fetch, stored by the app:

``` text
db.collection('groups')
  .where('participants', 'array-contains', 'user123')
  .where('lastUpdated', '>', lastFetchTimestamp)
  .orderBy('lastUpdated', 'desc')
  .limit(25)
```

Assume there are an average of 10 updated chats each time the user checks the app. This query only incurs 10 document reads.

#### Billed usage: Check chat list

  - Operations: 50 reads / user / day
  - Storage: None
  - Networking: 25KB / user / day

#### Read messages in a chat

Users click into chat threads from the home screen to see recent messages, loading the 50 most recent messages in the initial load.

Assume the typical user performs this action 5 times daily (once for every time they open the home screen), leading to a total of 250 reads per user each day. We can also limit our query to new messages since the last fetch time:

``` text
db.collection('groups')
  .doc('group234')
  .collection('messages')
  .where('sentTime', '>', lastFetchTimestamp)
  .orderBy('sentTime', 'desc')
  .limit(50)
```

Assume that a user gets about 30 messages a day across all chats. Since you've limited the query to fetch new messages, this translates to just 30 retrieved messages/day.

#### Billed usage: Read messages

  - Operations: 30 reads / user / day
  - Storage: None
  - Networking: 7.5KB / user / day

#### Send a message to a chat

Users can send messages to other participants once they're in a chat. Assume that an active user sends about 10 messages per day.

Each sent message will cause two document writes: one write to the `  messages  ` subcollection of the chat and one write to the chat parent document to update the `  lastUpdated  ` timestamp and other metadata.

Note that the cost of reading these messages has been accounted for in the other journeys, so the totals below only consider this write cost.

#### Billed usage: Sending messages

  - Operations: 20 writes / user / day
  - Storage: 15KB / user / day
  - Networking: No-cost (ingress)

## Billed usage for administrator tasks

As an app owner or administrator you probably want to generate reports from your app's data. For example, you might want to keep a daily count of the number of messages sent by your users. You can accomplish this with a [`  count()  `](/firestore/native/docs/query-data/aggregation-queries) aggregation of the `  messages  ` collection group.

For aggregation queries such as `  count()  ` , you are charged one document read for each batch of up to 1,000 index entries matched by the query. Running this daily aggregation adds the following monthly charges:

#### Small  
(50k installs)

#### For 50,000 app installs (5,000 DAUs): $0.0009/month

5,000 active users \* 10 new messages per user = 50,000 new message documents per day

50,000 documents counted / 1,000 index matches per read charge = 50 reads

50 reads per day \* 30 days = 1,500 reads per month

1,500 reads per month \* .06/100,000 read price = $0.0009 per month

#### Medium  
(1M installs)

#### For 1,000,000 app installs (100,000 Daily Active Users): $0.018/month

100,000 active users \* 10 new messages per user = 1,000,000 new message documents per day

1,000,000 documents counted / 1,000 index matches per read charge = 1,000 reads

1,000 reads per day \* 30 day = 30,000 reads per month

30,000 reads per month \* .06/100,000 read price = $0.018 per month

#### Large  
(10M installs)

#### For 10,000,000 app installs (1,000,000 Daily Active Users): $0.18

1,000,000 active users \* 10 new messages per user = 10,000,000 new message documents per day

10,000,000 documents counted / 1,000 index matches per read charge = 10,000 reads

10,000 reads per day \* 30 days = 300,000 reads per month

300,000 reads per month \* .06/100000 read price = $ 0.18 per month
