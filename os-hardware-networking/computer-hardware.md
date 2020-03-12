# Computer hardware
Collection of notes of computer harware parts.
---
## CPU

### Interrupt
* An interrupt is an input signal to the processor indicating an event that needs immediate attention. An interrupt signal alerts the processor and serves as a request for the processor to interrupt the currently executing code, so that the event can be processed in a timely manner. If the request is accepted, the processor responds by suspending its current activities, saving its state, and executing a function called an interrupt handler.
* Interrupts are commonly used by hardware devices to indicate electronic or physical state changes that require attention. Interrupts are also commonly used to implement computer multitasking, especially in real-time computing.

---
## Memory
### CPU (L1, L2) cache 
* CPU caches are small pools of memory that store information the CPU is most likely to need next.
* The goal of the cache system is to ensure that the CPU has the next bit of data it will need already loaded into cache by the time it goes looking for it (also called a cache hit).
* https://www.extremetech.com/extreme/188776-how-l1-and-l2-cpu-caches-work-and-why-theyre-an-essential-part-of-modern-chips

### Address space
* An address space defines a range of discrete addresses, each of which may correspond to a network host, peripheral device, disk sector, or a memory cell.
* For software programs to save and retrieve data, each unit of data must have an address where it can be individually located.

### Memory address
* Each memory location has a physical address which is a code. The CPU (or other device) can use the code to access the corresponding memory location.
* A computer program uses logical (or virtual) memory addresses to execute machine code, and to store and retrieve data.
* The computer's memory management unit and operating system maintain the mapping between physical and logical memory.

### Main memory
### Virtual memory
### Memory-mapped I/O
* Memory-mapped I/O uses the same address space to address both memory and I/O devices.
* Each I/O device monitors the CPU's address bus and responds to any CPU access of an address assigned to that device, connecting the data bus to the desired device's hardware register. 
* To accommodate the I/O devices, areas of the addresses used by the CPU must be reserved for I/O and must not be available for normal physical memory.

---
## Bus
* A bus is a communication system that transfers data between components inside a computer, or between computers.
* In most cases, the CPU and memory share signalling characteristics and operate in synchrony. The bus connecting the CPU and memory is one of the defining characteristics of the system, and often referred to simply as the system bus.
* It is possible to allow peripherals to communicate with memory in the same fashion, attaching adaptors in the form of expansion cards directly to the system bus. However, as the performance differences between the CPU and peripherals varies widely, some solution is generally needed to ensure that peripherals do not slow overall system performance. 

### System bus
* A system bus is a single computer bus that connects the major components of a computer system, combining the functions of a data bus to carry information, an address bus to determine where it should be sent, and a control bus to determine its operation.
* Since 2005/2006, considering an architecture in which 4 processors share a chipset, the DIB is composed by two buses, each of them is shared among two CPUs. The theoretical bandwidth is doubled compared to a shared front-side bus up to 12.8 GB/s in the best case.

### Paralle and serial bus
* In data transmission, parallel communication is a method of conveying multiple binary digits (bits) simultaneously. It contrasts with serial communication, which conveys only a single bit at a time; this distinction is one way of characterizing a communications link.
* The basic difference between a parallel and a serial communication channel is the number of electrical conductors used at the physical layer to convey bits. Parallel communication implies more than one such conductor.
* One huge advantage of having fewer wires/pins in a serial cable is the significant reduction in the size, the complexity of the connectors, and the associated costs.

### Port-mapped I/O

### Direct memory access
* Direct memory access (DMA) is a feature of computer systems that allows certain hardware subsystems to access main system memory (random-access memory), independent of the central processing unit (CPU).
* With DMA, the CPU first initiates the transfer, then it does other operations while the transfer is in progress, and it finally receives an interrupt from the DMA controller (DMAC) when the operation is done.

### PCI Express
