
# assignment 2
## DGraph class

our class represents a directed graph who is made of nodes and edges
every edge has a source node and a destination node, which means this edge creates a path from source to destination
(the opposite path may not exist)
every edge has a weight filed that represents the "cost" of using this edge during a path, 
we would like to think about this cost as the time it takes to get from source node to destination node.
that is why nonsensitive weight is not possible.
DGraph object:
* int id- represents the next available id for a node to be added.
* HashMap <Integer,node_data> idToVertex- a hash that gets an id of a node and connects it to the actual node who has that id.
* HashMap<Integer,HashMap<Integer,edge_data>>- a hashMap that represents the edges in the graph. main key is the id of the source node
values for a specific key is a hashMap where the keys are the id of all the nodes that has a direct edge that starts with this specific key and ends within them  
* int edgeNum- the number of edges in the graph
* int mc- mode counter- counts all the changes in the graph 

DGraph implements graph interface because every directed graph is first of all a graph.

### main methods 

* getNode- return the node_data by the node's id-  O(1)

* getEdge- return the data of the edge (src,dest), null if edge does not exist- O(1)

* addNode- add a deep copy of the node given to the graph with the given node's data. This is why 2 similar nodes are possible -the ID is unique for each node. Adding a node to the graph more than 1 time is possible since every addition gets a unique id O(1)

* connect- connect an edge with the given weight between node src to node dest. (if the edge is already exist the new edge overwriting the old one.) O(1)

* getV- This method return a pointer (shallow copy) for the collection representing all the nodes in the graph. O(1)

* getE(int srcID)- This method return a pointer (shallow copy) for the collection representing all the edges getting out of the given node (all the edges starting at the given node). O(1)

* removeNode (int nodeID)- Delete the node (with the given ID) from the graph -and removes all edges which starts or ends at this node - O(n)

* removeEdge(int src, int dest)- delete the edge from the graph (the one from src to dest) O(1)

* nodeSize- return the number of nodes O(1)

* edgeSize- return the number of edges O(1)

* getMC- return the number of changes of the graph O(1)



## Graph_Algo class

this class goal is to activate some well known algorithms on a graph.

Graph_Algo object:
* graph- a shallow copy of the graph to activate the algorithms on. if the graph changes the Graph_Algo changes as well

*	HashMap<Integer,HashSet<Integer>> vertexToNeighbors- represents the connection between a vertex and his "kids"-(all the vertices that end an edge that starts with the main vertex)

*	HashMap<Integer,HashSet<Integer>> NeighborsToVertex- represents the connection between a vertex and his "dads"- (all the vertices that start an edge that ends with the main vertex)

Integer.MAX_VALUE = infinity.

Graph_Algo implements graph_algorithms interface

### main methods 

* init (graph g)- initiate the graph given into our object, and defines the 2 additional hashMaps  

* init(String file_name)- initiate a graph from a file into graph-algo object, and defines the 2 additional hashMaps  

* save(String file_name)- save the graph field from this graph-algo object to a file

* copy- return a deep copy of this object's graph by saving the graph to a file and initiate it from the file 

* isConnected- Checks whether this graph is connected or not a connected graph means there is a valid path from EVREY node to each other node in this graph returns true if and only if (iff) the graph is connected

* shortPathGraph(int src)- Initiate all the vertices's weight to their distance from src node and all the vertices info to a string represents their path from src. based on Dijkstra's algorithm.

* shortestPathDist(int src, int dest)- Calculate the shortest path distance starting from src and ending with dest

* shortestPath(int src, int dest)- Calculate the shortest path starting from src and ending with dest

* TSP(List<Integer> targets)- computes a relatively short path which visit each node in the targets List- using a greedy algorithm

## Graph_GUI:
we used StdDraw class that Princeton University created.

here is the original class:

https://introcs.cs.princeton.edu/java/stdlib/StdDraw.java.html

we matched StdDraw to support a graph GUI window with several options:

1. save the graph as a photo or as a Serializable file. 

2. load a graph from the file system.

3. run some algorithm on the graph. (isConnected, shortestPath , TSP)

4. add/remove vertex, add/remove edge, create new graph , clear selected vertices

(if the graph to draw is null we refer to it as an empty graph.) 

Every Graph-GUI object is a thread that repaint the graph every 0.5 second if necessary.
the tread checkes if there is a need to repaint the graph by chacking the mc field within the graph.

