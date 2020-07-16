# Datalink layer (L2)

## Hubs
* All devices connected to a hub are considered being connected by a single wire loop.
* All devices share the same physical transmission (TX) and reception (RX) channel.
* Frames might collide. Collision detection is required. Badnwidth is not well utilized.
* All frames are broadcasted.
* All devices connected to a hub form a Collection Domain.

## Switches
* Frames only travels between switch and the connected device, allowing duplex between them.
* Switch keeps a MAC address table to forward frames to specific network interface, instead of broadcasting everything. Because of this, a switched network is most efficient when the network is in stable topology, so all the MAC addresses are registered.
* Switch also allow a frame to be broadcasted or multicasted.
* All devices connected to a switch form a Broadcast Domain.

## Routers
* Routers connect multiple networks and move packets bewteen networks.
* A router has multiple network interfaces, each with a different IP address.
* Routers contain routing tables, which determines to which interface a packet destined for an IP should be routed to.

## ARP (Address resolution protocol)
* To find out the mapping between an IP address and a MAC address.
* ARP mapping is stored in an ARP table on device/switch.
* If mapping is not found, broadcast ARP request to resolve IP address.
* A host with the ARP mapping sends back response by unicast.
* ARP is a L2 protocol.

## VLAN (virtual LAN)
* VLAN segments a broadcast domain into multiple broadcast domains. It allows multiple LANs on a single switch.
* A VLAN can also span several switches by trunk ports and VLAN tagging.
* VLAN information is stored in a VLAN database file on switches.
* VLAN tag is a field in ethernet header, which contains VLAN informationvfor that frame.
* VTP (VLAN trunking protocal) allows a switch to push VLAN information to surrounding switches in a client/server manner.

## Spanning tree protocol (STP)
* It constructs a spanning tree from a network topology.
* It eliminates loops when broadcasting a frame and prevent broadcast storm.

## VXLAN (Virtual eXtensible Local Area Network)
* One of the network overlay standards to create multi-tenant virtual LANs in datacenters.
* VXLAN is a tunneling protocol that encapsulates Layer 2 Ethernet frames in Layer 4 UDP packets, enabling you to create virtualized Layer 2 subnets.
* Packets start (encapsulated) and terminate (decapsulated) at VXLAN Tunnel End Point, a proxy on host.

## References
* [CSMD/CD and switching](https://www.youtube.com/watch?v=fxbhqxmWE4o)
* [VLAN and VTP](https://www.youtube.com/watch?v=L6SKYEm1S2c)
* [Ethernet frame sample](https://www.cs.miami.edu/home/burt/learning/Csc524.092/notes/ip_example.html)
* [VXLAN](https://www.juniper.net/us/en/products-services/what-is/vxlan/)