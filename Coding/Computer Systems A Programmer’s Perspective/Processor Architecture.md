
Each instruction in a Y86-64 program can read and modify some part of the processor state. This is referred to as the programmer-visible state, where the “programmer” in this case is either someone writing programs in assembly code or a compiler generating machine-level code. We will see in our processor implementations that we do not need to represent and organize this state in exactly the manner implied by the ISA, as long as we can make sure that machine-level programs appear to have access to the programmer-visible state. The state for Y86-64 is similar to that for x86-64.

- The x86-64 movq instruction is split into four different instructions: irmovq, rrmovq, mrmovq, and rmmovq, explicitly indicating the form of the source and destination. The source is either immediate (i), register (r), or memory (m). It is designated by the first character in the instruction name. The destination is either register (r) or memory (m). It is designated by the second character in the instruction name. Explicitly identifying the four types of data transfer will prove helpful when we decide how to implement them. The memory references for the two memory movement instructions have a simple base and displacement format. We do not support the second index register or any scaling of a register’s value in the address computation. As with x86-64, we do not allow direct transfers from one memory location to another. In addition, we do not allow a transfer of immediate data to memory. 

- There are four integer operation instructions, shown in Figure 4.2 as OPq. These are addq, subq, andq, and xorq. They operate only on register data, whereas x86-64 also allows operations on memory data. These instructions set the three condition codes ZF, SF, and OF (zero, sign, and overflow).

![[Pasted image 20260506101255.png]]

Y86-64 instruction set. Instruction encodings range between 1 and 10 bytes. An instruction consists of a 1-byte instruction specifier, possibly a 1-byte register specifier, and possibly an 8-byte constant word. Field fn specifies a particular integer operation (OPq), data movement condition (cmovXX), or branch condition (jXX). All numeric values are shown in hexadecimal.

### Y86-64 Exceptions

In the **Y86-64** architecture, the status code (**Stat**) acts as a diagnostic health check for the processor, signaling whether it can continue execution or must stop due to an error.

### The Status Codes (Stat)

Based on the architecture's design, there are four primary values for the status register:

|**Value**|**Name**|**Meaning**|**Resulting Action**|
|---|---|---|---|
|**1**|**AOK**|Normal operation|The processor continues to the next instruction.|
|**2**|**HLT**|`halt` instruction encountered|The processor stops gracefully (no error).|
|**3**|**ADR**|Invalid address encountered|The processor stops because it tried to read/write a bad memory address.|
|**4**|**INS**|Invalid instruction encountered|The processor stops because it hit a byte sequence it doesn't recognize.|

### Key Principles of Y86-64 Exception Handling

- **The "Halt on Error" Policy:** Unlike modern x86-64 processors, which might trigger an exception handler (like a "Segmentation Fault" message in Linux), a basic Y86-64 processor is designed to **simply stop** whenever the status is anything other than **AOK**.
- **The INS Error:** Looking back at the instruction encoding image, the processor expects the first nibble to be a value between `0` and `B`. If the processor fetches a byte like `0xCF`, it doesn't have a command for `C`, so it sets the status to **INS** and stops.
- **The ADR Error:** This occurs if the processor attempts to access a memory address beyond the physical limit defined for that specific system (e.g., trying to access address `0xFFFFFFFFFFFFFFFF` on a system with only 4GB of memory).
### Practical Example

If you accidentally write a program that "falls off the end" of your code and starts executing random data, it will likely hit a byte that isn't a valid opcode. The status will flip from **AOK** (1) to **INS** (4), and the machine will freeze immediately to prevent further corruption of the state.


### Logic Gates 

Logic gates are the basic computing elements for digital circuits. They generate an output equal to some Boolean function of the bit values at their inputs.
![[Pasted image 20260506101914.png]]

Figure 4.9 shows the standard symbols used for Boolean functions and, or, and not. HCL expressions are shown below the gates for the operators in C (Section 2.1.8): && for and, || for or, and ! for not. We use these instead of the bit-level C operators &, |, and ~, because logic gates operate on single-bit quantities, not entire words

