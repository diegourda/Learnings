Computers execute *machine code*, sequences of bytes encoding the low-level operations that manipulate data, manage memory, read and write data on storage devices, and communicate over networks. A compiler generates machine code through a series of stages, based on the rules of the programming language, the instruction set of the target machine, and the conventions followed by the operating system.

The *GCC* C compiler generates its output in the form of assembly code, a textual representation of the machine code giving the individual instructions in the program. Gcc then invokes both an assembler and a linker to generate the executable machine code from the assembly code.

When writing programs in assembly code (as was done in the early days of computing) a programmer must specify the low-level instructions the program uses to carry out a computation

Many attacks involve exploiting weaknesses in system programs to overwrite information and thereby take control of the system. Understanding how these vulnerabilities arise and how to guard against them requires a knowledge of the machine-level representation of programs.

A 32-bit machine can only make use of around 4 gigabytes (232 bytes) of random access memory, With memory prices dropping at dramatic rates, and our computational demands and data sizes increasing, it has become both economically feasible and technically desirable to go beyond this limitation. Current 64-bit machines can use up to 256 terabytes (248 bytes) of memory, and could readily be extended to use up to 16 exabytes (264 bytes).

##### Condition Codes 
In addition to the integer registers, the CPU maintains a set of single-bit condition code registers describing attributes of the most recent arithmetic or logical operation. These registers can then be tested to perform conditional branches. These condition codes are the most useful: 
- CF: Carry flag. The most recent operation generated a carry out of the most significant bit. Used to detect overflow for unsigned operations. 
- ZF: Zero flag. The most recent operation yielded zero. 
- SF: Sign flag. The most recent operation yielded a negative value. 
- OF: Overflow flag. The most recent operation caused a two’s-complement overflow—either negative or positive

```
For example, suppose we used one of the add instructions to perform the equivalent of the C assignment t = a+b, where variables a, b, and t are integers. Then the condition codes would be set according to the following C expressions: 
CF (unsigned) t < (unsigned) a Unsigned overflow 
ZF (t == 0) Zero 
SF (t < 0) Negative 
OF (a < 0 == b < 0) && (t < 0 != a < 0) Signed overflow
```

###### Procedures 
Procedures are a key abstraction in software. They provide a way to package code that implements some functionality with a designated set of arguments and an optional return value. This function can then be invoked from different points in a program.

- Passing control. The program counter must be set to the starting address of the code for Q upon entry and then set to the instruction in P following the call to Q upon return. 
- Passing data. P must be able to provide one or more parameters to Q, and Q must be able to return a value back to P. 
- Allocating and deallocating memory. Q may need to allocate space for local variables when it begins and then free that storage before it returns.

###### Control Transfer 
Passing control from function P to function Q involves simply setting the program counter (PC) to the starting address of the code for Q. However, when it later comes time for Q to return, the processor must have some record of the code location where it should resume the execution of P. This information is recorded in x86-64 machines by invoking procedure Q with the instruction call Q. This instruction pushes an address A onto the stack and sets the PC to the beginning of Q. The pushed address A is referred to as the return address and is computed as the address of the instruction immediately following the call instruction. The counterpart instruction ret pops an address A off the stack and sets the PC to A.

###### Data Transfer 
In addition to passing control to a procedure when called, and then back again when the procedure returns, procedure calls may involve passing data as arguments, and returning from a procedure may also involve returning a value. With x86-64, most of these data passing to and from procedures take place via registers

###### Local Storage on the Stack
Most of the procedure examples we have seen so far did not require any local storage beyond what could be held in registers. At times, however, local data must be stored in memory. Common cases of this include these: 
- There are not enough registers to hold all of the local data. 
- The address operator ‘&’ is applied to a local variable, and hence we must be able to generate an address for it. 
- Some of the local variables are arrays or structures and hence must be accessed by array or structure references. We will discuss this possibility when we describe how arrays and structures are allocated. 
Typically, a procedure allocates space on the stack frame by decrementing the stack pointer

###### Local Storage in Registers 
The set of program registers acts as a single resource shared by all of the procedures. Although only one procedure can be active at a given time, we must make sure that when one procedure (the caller) calls another (the callee), the callee does not overwrite some register value that the caller planned to use later. For this reason, x86-64 adopts a uniform set of conventions for register usage that must be respected by all procedures, including those in program libraries.

###### Recursive Procedures 
The conventions we have described for using the registers and the stack allow x86-64 procedures to call themselves recursively. Each procedure call has its own private space on the stack, and so the local variables of the multiple outstanding calls do not interfere with one another. Furthermore, the stack discipline naturally provides the proper policy for allocating local storage when the procedure is called and deallocating it before returning.

###### Data Alignment
Many computer systems place restrictions on the allowable addresses for the primitive data types, requiring that the address for some objects must be a multiple of some value *K* (typically 2, 4, or 8). Such *alignment restrictions* simplify the design of the hardware forming the interface between the processor and the memory system. 
For example, suppose a processor always fetches 8 bytes from memory with an address that must be a multiple of 8. If we can guarantee that any double will be aligned to have its address be a multiple of 8, then the value can be read or written with a single memory operation. Otherwise, we may need to perform two memory accesses, since the object might be split across two 8-byte memory blocks. 
The x86-64 hardware will work correctly regardless of the alignment of data. However, Intel recommends that data be aligned to improve memory system performance. Their alignment rule is based on the principle that any primitive object of K bytes must have an address that is a multiple of K. We can see that this rule leads to the following alignments:

| K   | Types                |
| --- | -------------------- |
| 1   | chat                 |
| 2   | short                |
| 4   | int                  |
| 8   | long, double, char * |

Alignment is enforced by making sure that every data type is organized and allocated in such a way that every object within the type satisfies its alignment restrictions. The compiler places directives in the assembly code indicating the desired alignment for global data.

###### Understanding Pointers 
Pointers are a central feature of the C programming language. They serve as a uniform way to generate references to elements within different data structures. Pointers are a source of confusion for novice programmers, but the underlying concepts are fairly simple.
- Every pointer has an associated type. This type indicates what kind of object the pointer points to. Using the following pointer declarations as illustrations 
> int one *ip; 
  char double **cpp;

Variable ip is a pointer to an object of type int, while cpp is a pointer to an object that itself is a pointer to an object of type char. In general, if the object has type T , then the pointer has type *T . The special void * type represents a generic pointer.

Pointer types are not part of machine code; they are an abstraction provided by C to help programmers avoid addressing errors. 
- Every pointer has a value. This value is an address of some object of the designated type. The special NULL (0) value indicates that the pointer does not point anywhere. 
- Pointers are created with the ‘&’ operator. This operator can be applied to any C expression that is categorized as an lvalue, meaning an expression that can appear on the left side of an assignment. Examples include variables and the elements of structures, unions, and arrays. We have seen that the machine code realization of the ‘&’ operator often uses the leaq instruction to compute the expression value, since this instruction is designed to compute the address of a memory reference. 
- Pointers are dereferenced with the ‘*’ operator. The result is a value having the type associated with the pointer. Dereferencing is implemented by a memory reference, either storing to or retrieving from the specified address. 
- Arrays and pointers are closely related. The name of an array can be referenced (but not updated) as if it were a pointer variable. Array referencing (e.g., a [3]) has the exact same effect as pointer arithmetic and dereferencing (e.g., *(a+3)). Both array referencing and pointer arithmetic require scaling the offsets by the object size. When we write an expression p+i for pointer p with value p, the resulting address is computed as p + L . i, where L is the size of the data type associated with p. 
- Casting from one type of pointer to another changes its type but not its value. One effect of casting is to change any scaling of pointer arithmetic. So, for example, if p is a pointer of type char * having value p, then the expression (int *) p+7 computes p + 28, while (int *) (p+7) computes p + 7. (Recall that casting has higher precedence than addition.) 
- Pointers can also point to functions. This provides a powerful capability for storing and passing references to code, which can be invoked in some other part of the program. For example, if we have a function defined by the prototype 
	- int fun(int x, int *p);
	then we can declare and assign a pointer fp to this function by the following code sequence: 
	int (*fp)(int, int *); fp = fun; 
	We can then invoke the function using this pointer: int y = 1; int result = fp(3, &y); 
	The value of a function pointer is the address of the first instruction in the machine-code representation of the function.