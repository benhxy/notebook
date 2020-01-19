# Algorithms in distributed systems

### Rendezvous hashing [1]
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

### Consistent hashing [2]
* What is it
    * It's a more specific alrogithm of Rendezvous hashing. It is also used to determine an object's location among many nodes.
* How it works
    * Hash keys are scattered on a circle. All nodes sit on that circle randomly.
    * Each node hosts the keys between the prior node and itself. 
    * After object is hashed, a search is conducted clockwise along the circle until it his a node. The search can be binary search (find the first element >= target).
    * When a node leaves, its keys are handled by the next node clockwise.
    * When a node joins, it takes over the keys prior to it from the next node.
    * To add to randomness, uniformity and leave/join load, we can add multiple points for one node, so that leave/join can be hanlded by multiple nodes.
    * To assign weight, we can arrange nodes so larger nodes handles more keys on the circle.
* Pros/ cons
    * The complexity of algorithm.
    * The cost of traveling the circle for searching.


### Geo hashing

### Bloom filter


[1]: https://en.wikipedia.org/wiki/Rendezvous_hashing
[2]: http://highscalability.com/blog/2018/6/18/how-ably-efficiently-implemented-consistent-hashing.html