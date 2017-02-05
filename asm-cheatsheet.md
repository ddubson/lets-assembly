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
