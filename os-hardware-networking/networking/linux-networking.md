# Linux kernel networking

## Network interface (aka. network device)

## sk_buff

## How an ingress (aka reception, RX) packet travel through kernel
1. Network interface controller (NIC, such as an ethernet card) receives a L2 frame, the NIC writes it to its own memory (or main memory through DMA), and sends an interrupt to notify kernel.
1. Kernel looks up a driver associated to the interrupt, and invoke its interrupt handler (top half handler). 
1. The top half handler copies frames from NIC memory into kernel memory in the form of sk_buff (socket buffer), and initializes the sk_buff. The top half handler also schedules bottom half handler by enqueuing a softirq (software interrupt) NET_RX_SOFTIRQ. The data structure of the queues is softnet_data, which has a pointer to the sk_buff.
1. The bottom half handler picks and invokes the correct L3 protocol (e.g. IP) handler based on a skb field.
1. L3 (IP) handler moves the skb pointer to L4 header, and picks and invokes the correct L4 protocol (e.g. TCP).
1. L4 (TCP) handler unpack and combine skb segments into a data frame and send it to the application's socket.
1. Application (L7) can now read socket data.


## Network namespace (netns)

## Bridge, virtual network interface pair

## iptables

## DNAT by iptables

## conntrack

## Reference
* Understanding Linux Network Internals by Christian Benvenuti, 2005