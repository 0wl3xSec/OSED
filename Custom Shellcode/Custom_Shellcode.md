## System Call Problem
Kernel-level functions are typically identified by system call numbers that are used to call the
corresponding functions. 

However, Windows system call numbers tend to change between major and minor version releases. We thus avoid direct system calls to write universal and reliable shellcode for Windows.

Without system calls, we can only use Windows API, exported by dynamic-link libraries (DLLs) that are mapped into process memory space at runtime.

## kernel32.dll

kernel32.dll exposes functions that can load DLLs into process space, locate the functions and invoke them.

- **_LoadLibraryA_** - load DLLs
- **_GetModuleHandleA_** - get base address of already-loaded DLL
- **_GetProcAddress_** - resolve symbols

## Position-Independent Shellcode (PIC)
In shellcode/exploits, we often don't know the absolute memory address where the code/data will be. To overcome this, we can use `CALL` instruction to push current address onto the stack. Thereafter, `POP` it into a register.

The `CALL` instruction pushes the **return address** (_address of next instruction_) onto the stack. When we `POP` that into the register, we now have a known, reliable runtime address. From there, we can calculate the absolute address of anything else nearby, using **relative offsets**.

