# BigTable

| | | |
|:---|:---|:---|
| Row key | The data within BigTable undergoes an assembling process with the use of a row key. The indexing of the map is then arranged as per the timestamps, row key, and column key. | |
| Requests| Pass through the front-end server pool before they can reach the specific BigTable node | |
| Nodes | The nodes are organized in the form of a BigTable cluster that belongs to a specific BigTable instance | |
| Tablets | As soon as BigTable identifies the data, each node directs its pointers to a certain set of tablets. These tablets are then stored over the Colossus. The rebalancing of tablets from one node to the other is seamless and fast. It is because the actual data is not at all copied. Instead, BigTable just updates its node pointers to respective tablets. | |

<br>

# 1. Time buckets or Single-timestamp rows
**Time buckets** : In a time bucket pattern, each row in your table represents a "bucket" of time, such as an hour, day, or month. A row key includes a non-timestamp identifier, such as week49, for the time period recorded in the row, along with other identifying data. <br><br>
**Single-timestamp rows** : In this pattern, you create a row for each new event or measurement instead of adding cells to columns in existing rows. The row key suffix is the timestamp value. Tables that follow this pattern tend to be tall and narrow, and each column in a row contains only one cell. <br>

| | Advantages | Disadvantages |
|:---|:---|:---|
| Time buckets | - You'll see better performance. For example, if you store 100 measurements, Bigtable writes and reads those measurements faster if they are in one row than if they are in 100 rows. <br> - Data stored in this way is compressed more efficiently than data in tall, narrow tables. <br>| Time-bucket schema design patterns are more complicated than single-timestamp patterns and can take more time and effort to develop. |
| Single-timestamp rows | | |

# 2. Adding new columns for new events
Treat column qualifiers as data, so that you can save space by naming the column with a value.<br>
As an example, consider a table that stores data about friendships, in which each row represents a person and all their friendships.<br>
Each column qualifier can be the name of a friend. Then the value for each column in that row can be the social circle the friend is in. In this example, rows might look like this:<br>

| | Fred | Gabriel | Hiroshi | Bob | Jakob |
|:---|:---|:---|:---|:---|:---|
| Jose | book-club | work | tennis | | |
| Sofia | | | work | school | chess-club |
<br>

Contrast this schema with a schema for the same data that doesn't use column qualifiers as data:<br>

| | Friend | Circle |
|:---|:---|:---|
| Jose#1| Fred | book-club |
| Jose#2| Gabriel | work |
| Jose#3| Hiroshi | tennis |
| Sofia#1| Hiroshi | work |
| Sofia#2| Bob | school |
| Sofia#3| Jakob | chess-club |
<br>

If you're using column qualifiers to store data, give column qualifiers short but meaningful names. This approach lets you reduce the amount of data that is transferred for each request. 

# 3. Adding new cells for new events
This pattern lets you take advantage of Bigtable's ability to let you store multiple timestamped cells in a given row and column.<br>
Using the weather balloon data as an example, Every time a balloon sends its measurements, the application writes new values to the row that holds the current week's data for the balloon, writing additional timestamped cells to each column.<br>
Each column in each row holds a measurement for each minute of the week. In this case, after three minutes, the first two columns in a row might look like this:<br>


| Row key |	pressure	| temp |
|:---|:---|:---|
| asia-south2#3698#week1 |	94558 (t2021-03-05-1200)	| 9.5 (t2021-03-05-1200) |
| ^ | 94122 (t2021-03-05-1201)	| 9.4 (t2021-03-05-1201) |
| ^ | 95992 (t2021-03-05-1202)	| 9.2 (t2021-03-05-1202) |

<br><br>

![cloumnQualifiers.png](https://github.com/developer-onizuka/BigTable/blob/main/columnQualifiers.png)

![Bigtable-architecture.png](https://github.com/developer-onizuka/BigTable/blob/main/Bigtable-architecture.png)
