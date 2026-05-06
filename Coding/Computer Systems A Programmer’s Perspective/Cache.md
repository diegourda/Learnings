To deal with the CPU-memory gap, there is cache memories that serve as temporary staging areas for information that the processor is likely to need in the near future. Types of cache:

- L1 cache: on the processor chip holds tens of thousands of bytes and can be accessed nearly as fast as the register file
- L2 cache: larger, and slower. It has hundreds of thousands to millions of bytes is connected to the processor by a special bus
- L3 cache: large, high-speed memory bank integrated directly onto the CPU chip, shared across all processor cores to speed up data access. Acts as crucial intermediate storage for data that is frequently reused but not as immediately necessary as L1/L2 data

The core idea of **caching** is to trick a system into feeling like it has both the **speed** of high-end hardware and the **capacity** of a massive storage drive.

It achieves this by exploiting **locality**, which is the predictable way software behaves:

> **The Principle:** Programs don't jump around randomly; they tend to stay in the same "neighborhood" of data for a while.
>  **The Strategy:** By keeping a copy of that "neighborhood" in a small, ultra-fast memory bank, the system can fulfill most requests instantly without having to wait on the slower, larger main memory.

![[Pasted image 20260503164737.png]]


