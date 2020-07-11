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

## VLAN (virtual LAN)
* VLAN segments a broadcast domain into multiple broadcast domains. It allows multiple LANs on a single switch.
* A VLAN can also span several switches by trunk ports and VLAN tagging.
* VLAN information is stored in a VLAN database file on switches.
* VLAN tag is a field in ethernet header, which contains VLAN informationvfor that frame.
* VTP (VLAN trunking protocal) allows a switch to push VLAN information to surrounding switches in a client/server manner.

## Spanning tree protocol (STP)
* It constructs a spanning tree from a network topology.
* It eliminates loops when broadcasting a frame and prevent broadcast storm.

## Routers
* Routers connect multiple networks and move packets bewteen networks.
* A router has multiple interfaces, each with a different IP address.

## References
* [CSMD/CD and switching](https://www.youtube.com/watch?v=fxbhqxmWE4o)
* [VLAN and VTP](https://www.youtube.com/watch?v=L6SKYEm1S2c)
* [Ethernet frame sample](https://www.cs.miami.edu/home/burt/learning/Csc524.092/notes/ip_example.html)