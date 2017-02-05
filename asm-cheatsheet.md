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

|Register Category        |Register Name     |Purpose                 |
|-------------------------|------------------|------------------------|
|General Purpose Registers|EAX, EBX, ECX, EDX|Used to manipulate data.|
