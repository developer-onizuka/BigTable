# BigTable

| | | |
|:---|:---|:---|
| Row key | The data within BigTable undergoes an assembling process with the use of a row key. The indexing of the map is then arranged as per the timestamps, row key, and column key. | |
| Requests| Pass through the front-end server pool before they can reach the specific BigTable node | |
| Nodes | The nodes are organized in the form of a BigTable cluster that belongs to a specific BigTable instance | |
| Tablets | As soon as BigTable identifies the data, each node directs its pointers to a certain set of tablets. These tablets are then stored over the Colossus. The rebalancing of tablets from one node to the other is seamless and fast. It is because the actual data is not at all copied. Instead, BigTable just updates its node pointers to respective tablets. | |

<br>

# 2. Treat column qualifiers as data
You can save space by naming the column with a value, if you store a column qualifier for every column.<br>
As an example, consider a table that stores data about friendships, in which each row represents a person and all their friendships.<br>
Each column qualifier can be the name of a friend. Then the value for each column in that row can be the social circle the friend is in. In this example, rows might look like this:<br>

| | Fred | Gabriel | Hiroshi | Bob | Jakob |
|:---|:---|:---|:---|:---|:---|
| Jose | book-club | work | tennis | | |
| Sofia | | | work | school | chess-club |


| | Friend | Circle |
|:---|:---|:---|
| Jose#1| Fred | book-club |
| Jose#2| Gabriel | work |
| Jose#3| Hiroshi | tennis |
| Sofia#1| Hiroshi | work |
| Sofia#2| Bob | school |
| Sofia#3| Jakob | chess-club |

<br><br>

![cloumnQualifiers.png](https://github.com/developer-onizuka/BigTable/blob/main/columnQualifiers.png)

![Bigtable-architecture.png](https://github.com/developer-onizuka/BigTable/blob/main/Bigtable-architecture.png)
