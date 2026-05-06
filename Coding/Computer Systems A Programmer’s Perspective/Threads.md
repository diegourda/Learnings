A process can actually consist of multiple execution units, called *threads*, each running in the context of the process and sharing the same code and global data.
Threads are an increasingly important programming model because of the requirement for concurrency in network servers, because it is easier to share data between multiple threads than between multiple processes, and because threads are typically more efficient than processes.

> Threads are more efficient because they **share the same memory space** and resources within a single process, whereas each process has its own private, isolated memory.

