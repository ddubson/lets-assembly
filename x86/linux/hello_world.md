# Hello World Assembly for x86 Linux

> The following assembly file will only work on Linux-based systems (linux kernel) since it links
> the Linux kernel lib to execute the command for printing Hello World

### Linking and Executing

> You must have Netwide Assembler (NASM) installed on your system. (use yum or apt to fetch the assembler)

##### Linking/Executing for x86 (32-bit)

```bash
nasm -f elf32 hello_world.asm
ld -m elf_i386 -s -o hello_world_32 hello_world.o
./hello_world_32
```

##### Linking/Executing for x86_64 (64-bit)

```bash
nasm -f elf64 hello_world.asm
ld -m elf_x86_64 -s -o hello_world_64 hello_world.o
./hello_world_64
```
