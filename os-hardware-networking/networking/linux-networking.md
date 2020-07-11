# Linux kernel networking

## How an inbound packet travel through kernel
1. Network interface controller (NIC, such as an ethernet card) receives a L2 frame, the NIC driver writes it to a buffer by direct memory access (DMA), and sends an interrupt.
1. Kernel finds the buffer, and copy it to a sk_buff (socket buffer), which cotnain
