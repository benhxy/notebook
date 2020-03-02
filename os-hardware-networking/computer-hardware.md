# Computer hardware
Collection of notes of computer harware parts.

---
## Memory
### L1, L2 cache

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

### Port-mapped I/O

### Direct memory access
* Direct memory access (DMA) is a feature of computer systems that allows certain hardware subsystems to access main system memory (random-access memory), independent of the central processing unit (CPU).
* With DMA, the CPU first initiates the transfer, then it does other operations while the transfer is in progress, and it finally receives an interrupt from the DMA controller (DMAC) when the operation is done.

### PCI Express
