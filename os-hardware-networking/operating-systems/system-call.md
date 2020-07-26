# System call

* System calls are interface command made by user space to ask kernel space to do some high-privilege operations.
* To make a system call is to execute a CPU instruction. The system call itself does not have a call stack or rely on any language runtime.
   * For instance, on modern Linux on amd64 making a syscall requires filling a set of CPU registers with certain values, doing some other arrangements and then issuing the SYSENTER CPU instruction. 
* Most other lanaguages use C library to implement system calls because of its portability. When using a C standard library function such as in `stdlib.h` or `sys/file.h`, we are actually calling a wrapper function to the system call. The wrapper function helps keep track of call stack and arguments, creating integration between applications and system calls. 
   * For example, malloc() wraps around the platform-dependend system calls to allocate heap memory, instead of doing the real memory allocation itself.
* Technically any language implementation with native interface or assembly interface can also implement its own system call wrappers. 
   * For example, Go's `syscall` standard package directly uses assembly code to do Linux system call instead of using C library.

## Reference
* https://softwareengineering.stackexchange.com/questions/343783/why-system-calls-are-limited-to-c-language-as-far-as-i-see
* https://stackoverflow.com/questions/55735864/how-does-go-make-system-calls
* https://en.wikipedia.org/wiki/System_call