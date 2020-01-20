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
* Need no introduction.
### Breath-first search
* Need no introduction.
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

### [A* Search Algorithm]
* What is it
    * Path-finding from one point to another point in graph or grid.
    * It is not exact, it's a fast approximation to the shortest path.
    * Commonly used in games, where movement is usually free.
* How it works:
    * g = the cost to move from the starting point to a given square, following the path generated to get there.
    * h = the estimated movement cost to move from that given square on the grid to the final destination. This is heuristic with various estimation methods (Manhattan, Diagonal and Euclidean).
    * f = the sum of g and h.
    * At each step it picks the node with the lowest f-value as the next step.
* Heuristics to get h (distance to destination):
    * Euclidean: sqrt(delta(x)^2 + delta(y)^2), used when movement is free.
    * Manhattan: abs(delta(x) + abs(delta(y)), used when only traveling L/R/U/D. 
    * Diagnal: max(abs(delta(x)), abs(delta(y)), used when traveling 8 directions.


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

### [Prim’s Minimum Spanning Tree Algorithm]
* How it works:
    * Two sets of vertices: visited and unvisited. 
    * Move any one vertex to visited set. Put all connected edges into a heap based on distance. (O(VlogV))
    * Each round, consider all edges connecting the two sets, and pick the one with lowest weight. And move the unvisited vertex to visited set. (O(logV))
    * Repeat until unvisited set is empty. (O(V))
    * Time complexity: O(VlogV)
* Why it works:
    * This is a greedy algorithm.
    * By only considering the edges connecting to unvisited vertexes, we avoid cycles.

### [Dijkstra’s shortest path algorithm]
* What is it:
    * Dijkstra's algorithm finds the shortest path between two vertices. Edges can be weighted or unweighted (all weights are 1).
    * It can find the shortest paths to _all_ vertices.
    * It's similar to [Prim’s Minimum Spanning Tree Algorithm].
    * Dijkstra is a special case of [A* Search Algorithm], where h = 0 for all nodes.
* How it works:
    * Two sets of vertices: visited and unvisited.
    * Move starting point to visited set. Put all connected vertices into a heap based on distance to start (O(VlogV)).
    * Each round, consider the closes vertex. Add it to visited set. Update heap with its connected vertices and distances to start (O(logE)).
    * Repeat until the end point is found (O(V)).
    * Time complexity: O(VlogE).   
* Why it works:
    * This is a greedy algorithm. 
    * Doesn’t work for graphs with negative weight edges. Need to use [Bellman–Ford negative path algorithm].

### [Bellman–Ford negative path algorithm]
### [Johnson’s algorithm for All-pairs shortest paths]
### [Floyd Warshall Algorithm]


[Minimum spanning tree]: https://www.geeksforgeeks.org/applications-of-minimum-spanning-tree/
[Kruskal’s Minimum Spanning Tree Algorithm]: https://www.geeksforgeeks.org/kruskals-minimum-spanning-tree-algorithm-greedy-algo-2/
[Dijkstra’s shortest path algorithm]: https://www.geeksforgeeks.org/dijkstras-shortest-path-algorithm-greedy-algo-7/
[A* Search Algorithm]: https://www.geeksforgeeks.org/a-search-algorithm/
[Prim’s Minimum Spanning Tree Algorithm]: https://www.geeksforgeeks.org/prims-minimum-spanning-tree-mst-greedy-algo-5/
[Bellman–Ford negative path algorithm]: http://en.wikipedia.org/wiki/Bellman-Ford_algorithm
[Johnson’s algorithm for All-pairs shortest paths]: https://www.geeksforgeeks.org/johnsons-algorithm/
[Floyd Warshall Algorithm]: https://www.geeksforgeeks.org/floyd-warshall-algorithm-dp-16/