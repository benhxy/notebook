# Algorithms in distributed systems

### Consistent hashing

### Rendezvous hashing
* What is it
    * Rendezvous hashing solves the distributed hash table problem: how do let all nodes agree on the hashcode (location of the resource) of an object?
* How it works
    * All nodes agree on the same hash function h(O, i), where i is the identifier of a node.
    * Each node calculate the hash value for all nodes given the object: h(O, 0), h(O, 1), h(O, 2) ...
    * The node with highest hash value is the host/location of the object.
    * When nodes join/leave the network, only the objects assign to that host is re-located remapped.
    * To reflect different capacities of a node, we can add weight to the hash function, such as h(O, i, W(i)).
* Pros/ cons
    * Less flexible then consistent hashing (the hash function needs to be agreed upon up front).
    * Maybe less global uniformity of placement with large data (if the hash function is not uniform).
    * Simpler in concept and implementation than consistent hasing.

### Geo hashing

### Bloom filter


[1]: https://en.wikipedia.org/wiki/Rendezvous_hashing