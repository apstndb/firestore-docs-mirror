# Structure data

Remember, when you structure your data in Firestore, you have a few different options:

  - Documents
  - Multiple collections
  - Subcollections within documents

Consider the advantages of each option as they relate to your use case. A few example structures for hierarchical data are outlined in this guide.

### Nested data in documents

You can nest complex objects like arrays or maps within documents.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><ul>
<li><strong>Advantages:</strong> If you have simple, fixed lists of data that you want to keep within your documents, this is easy to set up and streamlines your data structure.</li>
<li><strong>Limitations:</strong> This isn't as scalable as other options, especially if your data expands over time. With larger or growing lists, the document also grows, which can lead to slower document retrieval times.</li>
<li><strong>What's a possible use case?</strong> In a chat app, for example, you might store a user's 3 most recently visited chat rooms as a nested list in their profile.</li>
</ul></td>
<td><ul>
<li>class alovelace<br />

<ul>
<li>name :<br />
first : "Ada"<br />
last : "Lovelace"<br />
born : 1815<br />
rooms :<br />
0 : "Software Chat"<br />
1 : "Famous Figures"<br />
2 : "Famous SWEs"<br />
</li>
</ul></li>
</ul></td>
</tr>
</tbody>
</table>

### Subcollections

You can create collections within documents when you have data that might expand over time.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><ul>
<li><strong>Advantages:</strong> As your lists grow, the size of the parent document doesn't change. You also get full query capabilities on subcollections, and you can issue <a href="../query-data/queries">collection group queries</a> across subcollections.</li>
<li><strong>Limitations:</strong> You can't easily delete subcollections.</li>
<li><strong>What's a possible use case?</strong> In the same chat app, for example, you might create collections of users or messages within chat room documents.</li>
</ul></td>
<td><ul>
<li>collections_bookmark science
<ul>
<li>class software<br />
name : "software chat"
<ul>
<li>collections_bookmark users
<ul>
<li>class alovelace<br />
first : "Ada"<br />
last : "Lovelace"<br />
</li>
<li>class sride<br />
first : "Sally"<br />
last : "Ride"`</li>
</ul></li>
</ul>
<br />
<br />
</li>
<li>class astrophysics
<ul>
<li>...<br />
</li>
</ul></li>
</ul></li>
</ul></td>
</tr>
</tbody>
</table>

### Root-level collections

Create collections at the root level of your database to organize disparate data sets.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><ul>
<li><strong>Advantages:</strong> Root-level collections are good for many-to-many relationships and provide powerful querying within each collection.</li>
<li><strong>Limitations:</strong> Getting data that is naturally hierarchical might become increasingly complex as your database grows.</li>
<li><strong>What's a possible use case?</strong> In the same chat app, for example, you might create one collection for users and another for rooms and messages.</li>
</ul></td>
<td><ul>
<li>collections_bookmark users
<ul>
<li>class alovelace<br />
first : "Ada"<br />
last : "Lovelace"<br />
born : 1815<br />
</li>
<li>class sride<br />
first : "Sally"<br />
last : "Ride"<br />
born : 1951<br />
</li>
</ul></li>
<li>collections_bookmark rooms
<ul>
<li>class software
<ul>
<li>collections_bookmark messages
<ul>
<li>class message1<br />
from : "alovelace"<br />
content : "..."<br />
</li>
<li>class message2<br />
from : "sride"<br />
content : "..."<br />
</li>
</ul></li>
</ul></li>
</ul></li>
</ul></td>
</tr>
</tbody>
</table>

## Videos

To learn more, see the following videos:
