## The Stack

- Each thread in a running program has its own stack, used for short-term data like function calls, local variables, and control info.
- The stack operates as a **Last-In, First-Out (LIFO)** structure.
- In x86 architecture, the CPU uses **PUSH** and **POP** instructions to add and remove data from the top of the stack.
- This design allows independent execution of multiple threads by isolating their stacks.

## Function Return Mechanics
- When a function is called, the **return address** (_where execution should resume afterwards_) is saved on the stack, along with parameters and local variables to form the stack frame.
- Once the function finishes, the CPU retrieves the **return address** from the stack to resume execution in the calling function.

## CPU Registers
- 32-bit CPU uses **nine** 32-bit registers.

### General & Special Purpose Registers
| Register | Name               | Description                                                                 |
|----------|--------------------|-----------------------------------------------------------------------------|
| EAX      | Accumulator        | General-purpose; used for math, data, and function return values            |
| EBX      | Base               | Typically base address within `ds`                                          |
| ECX      | Counter            | Used for loops and repeated instructions; also general-purpose              |
| EDX      | Data               | General-purpose; used for math and I/O operations                           |
| ESI      | Source Index       | Points to source data (within `ds`) for memory/string operations            |
| EDI      | Destination Index  | Points to destination (within `es`) for memory/string operations            |
| EBP      | Base Pointer       | Used to reference stack frames (within `ss`)                                |
| ESP      | Stack Pointer      | Always points to the current bottom of the stack (within `ss`)              |
| EIP      | Instruction Pointer| Points to the next instruction to execute                                   |
| EFLAGS   | Flags Register     | Holds status flags (zero, carry, overflow, etc.) from arithmetic operations |


### Segment Registers
| Register | Name           | Description                                                                  |
|----------|----------------|------------------------------------------------------------------------------|
| CS       | Code Segment   | `EIP` points within this segment                                             |
| SS       | Stack Segment  | `ESP` and `EBP` point within this segment                                    |
| DS       | Data Segment   | `EBX` and `ESI` point within this segment                                    |
| ES       | Extra Segment  | `EDI` points within this segment                                             |
| FS       | Extra Segment  | Points to the Thread Information Block (TIB)                                 |
| GS       | Extra Segment  | Generally unused on 32-bit Windows                                           |


### Register Aliases
| Full Register | 16-bit Alias | 8-bit Low | 8-bit High | Description                            |
|---------------|--------------|------------|------------|----------------------------------------|
| EAX           | AX           | AL         | AH         | Low and high halves of AX              |
| EBX           | BX           | BL         | BH         | Low and high halves of BX              |
| ECX           | CX           | CL         | CH         | Low and high halves of CX              |
| EDX           | DX           | DL         | DH         | Low and high halves of DX              |
