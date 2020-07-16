# Network layer (IP layer, L3)

## IP header
* Important fields: TTL (decrement every second), Protocol (for L4), Source/Destinaion address.

## ICMP (Internet control message protocol)
* Used for diagnostics.
* ICMP is a L4 protocol.

## IP Address
* IP address has three portions: network + host + subnet mask.
* Classful addressing
   * Network has different classes (A, B, C). Each class has different bit length of network and host portion. Class is decided by the first octet.
   * 127.*.*.* is for local loopback.
   * All host bits set to 0: network address.
   * All host bits set to 1: broadcast address.
* Classless addressing
   * Use a subnet mask to specifically call out the bit length of host portion.
   * Subnets still belong to the classful networks. The class of original network can be still decided by the first octet.
   * Subnets add to the number of possible networks, because we can use the same IP address to represent different hosts (e.g. 4.4.0.2/8 represents network=4.0.0.0 and host 4.0.2, but 4.4.0.2/16 represents network=4.4.0.0, and host=0.2).
* Classful network design served its purpose in the startup stage of the Internet, but it lacked scalability in the face of the rapid expansion of networking in the 1990s. The class system of the address space was replaced with Classless Inter-Domain Routing (CIDR) in 1993. Today, remnants of classful network concepts function only in a limited scope as the default configuration parameters of some network software and hardware components (e.g. netmask), and in the technical jargon used in network administrators' discussions.

## Private IP address space
* The Internet Assigned Numbers Authority (IANA) has reserved the following three blocks of the IP address space for private internets:
   * 10.0.0.0        -   10.255.255.255  (10/8 prefix)
   * 172.16.0.0      -   172.31.255.255  (172.16/12 prefix)
   * 192.168.0.0     -   192.168.255.255 (192.168/16 prefix)
* An enterprise that decides to use IP addresses out of the address space defined in this document can do so without any coordination with IANA or an Internet registry. The address space can thus be used by many enterprises. Addresses within this private address space will only be unique within the enterprise.


## Routing protocols

## NAT

## Reference
* [Private IP allocation RFC1918](https://tools.ietf.org/html/rfc1918)
* [History of subnet](https://en.wikipedia.org/wiki/IP_address#Subnetting_history)