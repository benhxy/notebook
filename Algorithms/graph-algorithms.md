# Graph algorithms

## Concepts
### [Minimum spanning tree]
* A graph's sub-graph.
* From one root vertex, all vertices can be reached.
* Such paths and vertices form a tree.
* The tree with the lowest sum of paths' wedight is a minimum spanning tree.
* A minimum spanning tree has (V – 1) edges where V is the number of vertices in the given graph.

## Basic algorithms
### Depth-first search
### Breath-first search
### Topological sorting
* Only in directed graph.
* Useful for finding cycle.
* Useful for sequencing vertices.

### Union-find
* How it works:
    * Iterate through all edges of a graph.
    * Join two sets of the same edge.
    * If any edge has two vertices already joint, there is cycle in graph.
    * If at the end there are more than 1 set, the graph is not connected.

###

## Advanced algorithms
### [Kruskal’s Minimum Spanning Tree Algorithm]
* How it works:
    * Sort all edges based on wedight from lowest to highest. (O(ElogE))
    * Pick the smallest edge. Check if it forms a cycle with the spanning tree formed so far. If cycle is not formed, include this edge. Else, discard it. (O(logV), cost of find)
    * Repeat step#2 until there are (V-1) edges in the spanning tree. (O(V))
    * Time complexity: O(VlogE) or O(VlogV). (E can be as bad as V^2 so logE is the same as logV)
* Why it works:
    * It uses union-find concept to join vertices.
    * For an edge, if the two vertices are already in the same union, then the edge creates a cycle. It should be discarded.
    * This is a greedy algorithm.

### [Prim’s Minimum Spanning Tree]
* How it works:
    * Two sets of vertices: visited and unvisited. 
    * Move any one vertex to visited set. Put all connected edges into a heap. (O(VlogV))
    * Each round, consider all edges connecting the two sets, and pick the one with lowest weight. And move the unvisited vertex to visited set. (O(logV))
    * Repeat until unvisited set is empty. (O(V))
    * Time complexity: O(VlogV)
* Why it works:
    * This is a greedy algorithm.
    * By only considering the edges connecting to unvisited vertexes, we avoid cycles.

### [Dijkstra’s shortest path algorithm]


### [A* Search Algorithm]

[Minimum spanning tree]: https://www.geeksforgeeks.org/applications-of-minimum-spanning-tree/
[Kruskal’s Minimum Spanning Tree Algorithm]: https://www.geeksforgeeks.org/kruskals-minimum-spanning-tree-algorithm-greedy-algo-2/
[Dijkstra’s shortest path algorithm]: https://www.geeksforgeeks.org/dijkstras-shortest-path-algorithm-greedy-algo-7/
[A* Search Algorithm]: https://www.geeksforgeeks.org/a-search-algorithm/
[Prim’s Minimum Spanning Tree]: https://www.geeksforgeeks.org/prims-minimum-spanning-tree-mst-greedy-algo-5/