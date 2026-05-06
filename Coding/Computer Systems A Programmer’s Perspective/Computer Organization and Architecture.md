## The Concept

**Out-of-Bounds Memory References** occur when a program writes data outside the memory space specifically reserved for an array. Since the C language doesn't double-check if you’re "staying inside the lines," it will happily let you write data into neighboring memory addresses.

A **Buffer Overflow** is the specific result of this: extra data "overflows" its container and overwrites adjacent data on the **stack**. This is dangerous because the stack also stores critical control info, like **return addresses** (the instructions telling the CPU where to go next). If an attacker overwrites a return address with a pointer to their own malicious code, they can hijack the entire program.
## What is a "Bound"?

In programming, a **bound** is the technical limit or boundary of a data structure.

- **Lower Bound:** The starting index of an array (usually `0`).
- **Upper Bound:** The highest valid index (usually `size - 1`).
### Example: The "Egg Carton" Analogy

Imagine an egg carton designed to hold **12 eggs**.

- **The Bound:** The physical edge of the carton.
- **Out-of-Bounds:** Trying to force a 13th egg into the carton.
- **The Overflow:** Because there is no more room in the "array" (the carton), the 13th egg gets smashed onto the table next to it. If there was a "Return Address" (an important note) sitting on the table right next to the carton, the egg yolk would cover it, corrupting that information.

```
int buffer[10];   // The bounds are 0 to 9
buffer[15] = 1;   // Out-of-bounds! We just smashed an "egg" at index 15.
```

The `gets()` function is one of the most famous examples of "insecure" code in C history. It is so dangerous that modern compilers will often give you a loud warning just for using it.

### Why `gets()` is Dangerous

The core issue is that `gets()` has no parameter to specify the **maximum number of characters** to read. It simply continues reading from the input until it hits a newline character or an end-of-file.

If you have a buffer (an array) that can hold 10 characters, but the user types 100, `gets()` will faithfully write all 100 characters into memory. The first 10 go where they belong, and the remaining 90 overwrite whatever comes next on the stack.
### The Anatomy of the Attack

To understand how this leads to "state corruption," look at how the **Stack Frame** is organized in memory:

1. **Local Variables:** This is where your `char s[]` buffer lives.
2. **Saved Registers:** Data the CPU needs to restore once your function finishes.
3. **Return Address:** The most critical piece—it is the memory address of the next instruction the CPU should execute after `gets()` finishes.

When a buffer overflow occurs, the data "grows" upward from the local variables. A long enough string will eventually reach and overwrite the **Return Address**.
### Example: Hijacking the Flow

Imagine a function that checks a password:

```
void check_password() {
    char buffer[8];
    gets(buffer); // User inputs 24 characters
}
```

- **Normal Execution:** The program runs `gets()`, then looks at the **Return Address** to go back to the main menu.
- **The Overflow:** The user inputs a specifically crafted string. The first 8 characters fill the buffer. The next several characters overwrite saved data. The final characters land exactly where the **Return Address** is stored.
- **The Corruption:** Instead of returning to the main menu, the CPU now reads a **corrupted address** provided by the user. If that address points to malicious code (shellcode), the attacker now has control of the system.

### The Solution
Never use `gets()`. Instead, use `fgets()`, which forces you to define a limit:

`fgets(buffer, sizeof(buffer), stdin);`

This ensures the "bounds" are respected, and no data can spill over into critical stack state.

### Floating-Point Code 

The *floating-point architecture* for a processor consists of the different aspects that affect how programs operating on floating-point data are mapped onto the machine, including 
- How floating-point values are stored and accessed. This is typically via some form of registers. 
- The instructions that operate on floating-point data. 
- The conventions used for passing floating-point values as arguments to functions and for returning them as results. 
- The conventions for how registers are preserved during function calls—for example, with some registers designated as caller saved, and others as callee saved.

