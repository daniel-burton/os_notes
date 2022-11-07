# **Operating Systems: *Three Easy Pieces* **
## Chapter 1: A Dialogue on the Book

The "three easy pieces" are
- *Virtualization*
- *Concurrency*
- *Persistence*

## Chapter 2: Introduction to Operating Systems

We already know, as students of computer science, that running a program consists of loading instructions from memory, decoding them into the actions needed, and executing those actions. But how does the computer "know" how to do those things?

Operating systems allow, in layman's terms:
- Running progams -- even many at once
- Sharing memory
- Interacting with devices
- Etc!

This is accomplished by *virtualization*. Virtualization refers to taking a physical resource (a stick of RAM, a hard drive, etc) and presents it as a *virtual* form. Your program does not need to know whether you have a Solid State Drive or a Hard Disc in order to write to it. It only needs to send the "write to memory" *system call* to the operating system, which handles the implementation. For this reason, every *OS* can be called a *virtual machine*.

Because of its management of processor time, hard drive space, RAM, etc, an OS is sometimes called a *resource manager*.

### 2.1 Virtualizing the CPU
### Example C program, demonstrating virtualizing the CPU.
See pages 5 and 6.

The C program prints out a given character once every second.
The point is: you can run several instances of this C program at once, and they will interleave with each other. How does this work? The OS is managing all of the resources to allow them to run at the same time.

### 2.2 Virtualizing Memory
### Example C program that accesses memory with malloc(). It allocates a byte, prints the address of the byte, sets it to "0", then prints the value after incrementing it each loop.
See page 7.

Due to virtualization of RAM, memory is presented as a simple series of bytes with contiguous addresses.

You can see this by running the example program twice at once. The program prints the same byte address for both instances! This is because the address is not an absolute address. It just refers to the address **within** the private memory allocated to the running process-- its *virtual address space*. This prevents processes from interfering with each other or reading memory they shouldn't have access to.

### 2.3 Concurrency

### Example C program to demonstrate the difficulties of concurrency.
See page 9.

When running the above program, you do not always get the results expected. This is due to multiple threads running at the same time. We'll delve into this deeper later.

### 2.4 Persistence

This section has a bunch of examples of why a program might need to save data, or read data written by another program. Long story short: the OS lets you write to persistent memory. The OS provides a *standard library* of system calls that allow a process to write to the disk. These system calls rely on *drivers* to carry out their instructions. Because of the abstraction/virtualization of this process, the OS is free to do a variety of things to optimize access, like delaying writes, sequencing where data are stored for optimum efficiency, retrying if the write fails, etc-- all without the process needing to take notice.
