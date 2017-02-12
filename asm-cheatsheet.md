# Assembly Language Cheatsheet
---

## Syntax

Two main forms of assembly syntax: 

* `AT&T` - used by GNU Assembler; GCC Compiler;

* `Intel` - Netwide Assembler (NASM) most common

Few differences in syntax:

* Source and Destination operands are reversed;  Different symbols used to mark the beginning of a comment
	* `CMD <dest>, <source> <; comment>` - Intel
	* `CMD <source>, <dest> <# comment>` - AT&T
* AT&T format uses a `%` before registers; NASM does not
* AT&T format uses a `$` before literal values; NASM does not

## Intel x86 Processor Register Overview

| Register Category         | Register Name                                                             | Purpose                                                                                     | Size (Bits) |
|---------------------------|---------------------------------------------------------------------------|---------------------------------------------------------------------------------------------|-------------|
| General Purpose Registers | EAX, EBX, ECX, EDX                                                        | Used to manipulate data                                                                     | 32          |
|                           | AX, BX, CX, DX                                                            | 16-bit versions of above                                                                    | 16          |
|                           | AH, BH, CH, DH, AL, BL, CL, DL                                            | 8-bit high and low order bytes of the previous entry                                        | 8           |
| Segment Registers         | CS, SS, DS, ES, FS, GS                                                    | Holds the first part of a memory addr; holds pointers to code stack and extra data segments | 16          |
| Offset Registers          |                                                                           | Indicates an offset related to segment registers                                            |             |
|                           | EBP (Extended Base Pointer)                                               | Points to the beginning of the local environment  for a function                            |             |
|                           | ESI (Extended Source Index)                                               | Holds the data source offset in an operation  using a memory block                          |             |
|                           | EDI (Extended Destination Index)                                          | Holds the destination data offset in an operation  using a memory block                     |             |
|                           | ESP (Extended Stack Pointer)                                              | Points to the top of the stack.                                                             |             |
| Special Registers         |                                                                           | Only used by the CPU                                                                        |             |
|                           | EFLAGS register; ZF = zero flag IF = interrupt enable flag SF = sign flag | Used by the CPU to track results of logic                                                   |             |
|                           | EIP (Extended Instruction Pointer)                                        | Points to the address of the next instruction to be executed                                |             |
|                           |                                                                           |                                                                                             |             |

# Commands
---

##### mov

`mov` - copies data from source to destination;

data cannot be moved directly from memory to a segment register - must use gen-purpose register as intermediate step.

| Intel Syntax           | Intel Example           | AT&T Example               |
|------------------------|-------------------------|----------------------------|
| `mov <dest>, <source>` | `mov eax, 51h ;comment` | `movl $51h, %eax #comment` |

e.g. 
`mov eax, 1234h; store the value of 1234 (hex) into EAX`

`mov cs, ax    ; then copy the value of AX into CS`

---

##### add and sub

`add`, `sub` - adds source to destination/subtracts source from destination and stores result in destination

| Intel Syntax           | Intel Example  | AT&T Example      |
|------------------------|----------------|-------------------|
| `add <dest>, <source>` | `add eax, 51h` | `addl $51h, %eax` |
| `sub <dest>, <source>` | `sub eax, 51h` | `subl $51h, %eax` |

---

##### push and pop

`push`, `pop` - push into stack and pop off of the stack.

| Intel Syntax   | Intel Example  | AT&T Example |
|----------------|----------------|--------------|
| `push <value>` | `push eax`     | `pushl %eax` |
| `pop <dest>`   | `pop eax`      | `popl %eax`  |

---

##### xor - exclusive-OR

`xor` - conducts a bitwise logical exclusive-OR (XOR) function; Use XOR value to zero out or clear a register/memory location.

| Intel Syntax           | Intel Example  | AT&T Example     |
|------------------------|----------------|------------------|
| `xor <dest>, <source>` | `xor eax, eax` | `xor %eax, %eax` |

---

##### jump and branch

Branch the flow of the program to another location based on the value of the eflag ZF (zero flag)

`jne`, `jnz` - jumps if the zero flag is 0
`je`, `jz` - jump if the zero flag is 1
`jmp` - always jumps


| Intel Syntax              | Intel Example  | AT&T Example |
|---------------------------|----------------|--------------|
| `jnz <dest> / jne <dest>` | `jne start`    | `jne start`  |
| `jz <dest> / je <source>` | `jz loop`      | `jz loop`    |
| `jmp <dest>`              | `jmp end`      | `jmp end`    |

---

##### call and return

`call` - calls a procedure
`ret` - used to end a procedure to return the flow to the command after the call.

| Intel Syntax  | Intel Example      | AT&T Example       |
|---------------|--------------------|--------------------|
| `call <dest>` | `call subroutine1` | `call subroutine1` |
| `ret`         | `ret`              | `ret`              |

---

##### increment and decrement

`inc`, `dec` - increment/decrement the destination

| Intel Syntax   | Intel Example  | AT&T Example |
|----------------|----------------|--------------|
| `inc <dest>`   | `inc eax`      | `incl %eax`  |
| `dec <dest>`   | `dec eax`      | `decl %eax`  |

---

##### load effective (memory) address

`lea` - loads effective address of the source into destination

| Intel Syntax           | Intel Example      | AT&T Example         |
|------------------------|--------------------|----------------------|
| `lea <dest>, <source>` | `lea eax, [dsi+4]` | `leal 4(%dsi), %eax` |

---

##### interrupt

`int` - throws a system interrupt signal to the processor; common interrupt is `0x80` - sys call to kernel.

| Intel Syntax | Intel Example  | AT&T Example  |
|--------------|----------------|---------------|
| `int <val>`  | `int 0x80`     | `int $0x80`   |

---