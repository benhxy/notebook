# Link layer (L2)
* L2 layer protocols are hardware-specific. 
* If the frame is received on an Ethernet interface, the receiver knows it contains an Ethernet header, and a Token Ring interface knows it contains a Token Ring header, and so on.
* For example, ARP is based on MAC address, so its an ethernet protocol.

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

## VXLAN (Virtual eXtensible Local Area Network)
* One of the network overlay standards to create multi-tenant virtual LANs in datacenters.
* VXLAN is a tunneling protocol that encapsulates Layer 2 Ethernet frames in Layer 4 UDP packets, enabling you to create virtualized Layer 2 subnets.
* Packets start (encapsulated) and terminate (decapsulated) at VXLAN Tunnel End Point, a proxy on host.

## References
* [CSMD/CD and switching](https://www.youtube.com/watch?v=fxbhqxmWE4o)
* [Ethernet frame sample](https://www.cs.miami.edu/home/burt/learning/Csc524.092/notes/ip_example.html)
* [VXLAN](https://www.juniper.net/us/en/products-services/what-is/vxlan/)