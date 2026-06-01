A process is the operating system’s abstraction for a running program. Multiple processes can run concurrently on the same system, and each process appears to have exclusive use of the hardware. By concurrently, we mean that the instructions of one process are interleaved with the instructions of another process. In most systems, there are more processes to run than there are CPUs to run them.

Newer multicore processors can execute several programs simultaneously. In either case, a single CPU can appear to execute multiple processes concurrently by having the processor switch among them. The operating system performs this interleaving with a mechanism known as *context switching* 

> 	Context switching: the process where a computer's CPU pauses its current task, saves the exact state (the "context"), and switches to a different task. This happens so quickly that it creates the illusion that the computer is running multiple programs simultaneously


When you run a program, the **Operating System** performs a context switch: it pauses the **shell**, saves its current state, and transfers control to the new **"hello" process**.  After hello terminates, the operating system restores the context of the shell process and passes control back to it, where it waits for the next command-line input.

The kernel is the portion of the operating system code that is always resident in memory. When an application program requires some action by the operating system, such as to read or write a file, it executes a special system call instruction, transferring control to the kernel. Then performs the requested operation and returns back to the application program.

> *Note* that the kernel is not a separate process. Instead, it is a collection of code and data structures that the system uses to manage all the processes.

