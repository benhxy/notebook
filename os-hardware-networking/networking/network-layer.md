# Network layer (IP layer, L3)

## IP header
* Important fields: TTL (decrement every second), Protocol (for L4), Source/Destinaion address.

## ARP (Address resolution protocol)
* To find out the mapping between an IP address and a MAC address.
* ARP mapping is stored in an ARP table on device/switch.
* If mapping is not found, broadcast ARP request to resolve IP address.
* A host with the ARP mapping sends back response by unicast.
* ARP is a L2 protocol.

## DNS (Domain name service)
* To find out the mapping between a domain name and IP address.
* Device uses a DNS server to resolve domain names.
* DNS is a L7 protocol on UDP/IP.

## DHCP (Dynamic host configuration protocol)
* Host creates an IP broadcast to request DHCP information (discovery).
* DHCP servers offer information in unicast response (lease offer).
* Host choose a DHCP server response and request for more information (lease request).
* DHCP server acknowledge the request and assign IP address and other things (acknowledge).
* DHCP is a L7 protocol on UDP/IP.

## ICMP (Internet control message protocol)
* Used for diagnostics.
* ICMP is a L4 protocol.

## IP Address
* IP address has two portions: network + host.
* Classful addressing
   * Network has different classes (A, B, C). Each class has different bit length of network and host portion. Class is decided by the first octet.
   * 127.*.*.* is for local loopback.
   * All host bits set to 0: network address.
   * All host bits set to 1: broadcast address.
* Classless addressing
   * Use a subnet mask to specifically call out the bit length of host portion.
   * Subnets still belong to the classful networks. The class of original network can be still decided by the first octet.
   * Subnets add to the number of possible networks, because we can use the same IP address to represent different hosts (e.g. 4.4.0.2/8 represents network=4.0.0.0 and host 4.0.2, but 4.4.0.2/16 represents network=4.4.0.0, and host=0.2).