# BigTable

| | | |
|:---|:---|:---|
| Row key | The data within BigTable undergoes an assembling process with the use of a row key. The indexing of the map is then arranged as per the timestamps, row key, and column key. | |
| Requests| Pass through the front-end server pool before they can reach the specific BigTable node | |
| Nodes | The nodes are organized in the form of a BigTable cluster that belongs to a specific BigTable instance | |
| Tablets | As soon as BigTable identifies the data, each node directs its pointers to a certain set of tablets. These tablets are then stored over the Colossus. The rebalancing of tablets from one node to the other is seamless and fast. It is because the actual data is not at all copied. Instead, BigTable just updates its node pointers to respective tablets. | |

![cloumnQualifiers.png](https://github.com/developer-onizuka/BigTable/blob/main/columnQualifiers.png)

![Bigtable-architecture.png](https://github.com/developer-onizuka/BigTable/blob/main/Bigtable-architecture.png)
