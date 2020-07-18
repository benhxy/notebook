# Linux kernel networking

## Network interface (aka. network device)

## sk_buff

## How an ingress (aka reception, RX) packet travel through kernel
1. Network interface controller (NIC, such as an ethernet card) receives a L2 frame, the NIC writes it to its own memory (or main memory through DMA), and sends an interrupt to notify kernel.
1. Kernel looks up a driver associated to the interrupt, and invoke its interrupt handler (top half handler). 
1. The top half handler copies frames from NIC memory into kernel memory in the form of sk_buff (socket buffer), and initializes the sk_buff. The top half handler also schedules bottom half handler by enqueuing a softirq (software interrupt) NET_RX_SOFTIRQ. The data structure of the queues is softnet_data, which has a pointer to the sk_buff.
1. 




## Network namespace (netns)

## Bridge, virtual network interface pair

## iptables

## DNAT by iptables

## conntrack

