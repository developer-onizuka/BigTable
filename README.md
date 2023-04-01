# BigTable

Row key : The data within BigTable undergoes an assembling process with the use of a row key. The indexing of the map is then arranged as per the timestamps, row key, and column key. <br>
Requests : pass through the front-end server pool before they can reach the specific BigTable node <br>
Nodes : The nodes are organized in the form of a BigTable cluster that belongs to a specific BigTable instance <br>
Tablets : As soon as BigTable identifies the data, each node directs its pointers to a certain set of tablets.

| | | |
|:---|:---|:---|
| | | |

![cloumnQualifiers.png](https://github.com/developer-onizuka/BigTable/blob/main/columnQualifiers.png)

![Bigtable-architecture.png](https://github.com/developer-onizuka/BigTable/blob/main/Bigtable-architecture.png)
