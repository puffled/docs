# x86/x86-64 assembly

an x86-64 instruction may be at most 15 bytes in length once
encoded.

the following table is a list of components in order of 
how they appear in an encoded instruction.

| component            | size (in bytes) | importance  |
|----------------------|-----------------|-------------|
| legacy prefix        | 1 to 4          | optional    |
| opcodes and prefixes | 1 to 4          | required    |
| mod r/m              | 1               | if required |
| sib                  | 1               | if required |
| displacement         | 1, 2, 4 or 8    | if required |
| immediate            | 1, 2, 4 or 8    | if required |


### names

| short | long           |
|-------|----------------|
| `gp`  | general purpose| 
| `sp`  | stack pointer  |
| `bp`  | base pointer   |

### registers

| binary | decimal | hexidecimal | 8-bit gp    | 16-bit gp | 32-bit gp | 64-bit gp |
|--------|---------|-------------|-------------|-----------|-----------|-----------|
| `0000` | `0`     | `0`         | `al`        | `ax`      | `eax`     | `rax`     |
| `0001` | `1`     | `1`         | `cl`        | `cx`      | `ecx`     | `rcx`     |
| `0010` | `2`     | `2`         | `dl`        | `dx`      | `edx`     | `rdx`     |
| `0011` | `3`     | `3`         | `bl`        | `bx`      | `ebx`     | `rbx`     |
| `0100` | `4`     | `4`         | `ah`, `spl` | `sp`      | `esp`     | `rsp`     |
| `0101` | `5`     | `5`         | `ch`, `bpl` | `bp`      | `ebp`     | `rbp`     |
| `0110` | `6`     | `6`         | `dh`, `sil` | `si`      | `esi`     | `rsi`     |
| `0111` | `7`     | `7`         | `bh`, `dil` | `di`      | `edi`     | `rdi`     |
| `1000` | `8`     | `8`         | `r8l`       | `r8w`     | `r8d`     | `r8`      |
| `1001` | `9`     | `9`         | `r9l`       | `r9w`     | `r9d`     | `r9`      |
| `1010` | `10`    | `A`         | `r10l`      | `r10w`    | `r10d`    | `r10`     |
| `1011` | `11`    | `B`         | `r11l`      | `r11w`    | `r11d`    | `r11`     |
| `1100` | `12`    | `C`         | `r12l`      | `r12w`    | `r12d`    | `r12`     |
| `1101` | `13`    | `D`         | `r13l`      | `r13w`    | `r13d`    | `r13`     |
| `1110` | `14`    | `E`         | `r14l`      | `r14w`    | `r14d`    | `r14`     |
| `1111` | `15`    | `F`         | `r15l`      | `r15w`    | `r15d`    | `r15`     |

### sources

 - [compas/gentle introduction to x86-64 assembly](https://compas.cs.stonybrook.edu/~nhonarmand/courses/sp17/cse506/ref/assembly.html)
 - [felixcloutier/x86 and x86-64 instruction reference](https://www.felixcloutier.com/x86/index.html)
 - [osdev/stack](https://wiki.osdev.org/Stack)
 - [osdev/x86-64 instruction encoding](https://wiki.osdev.org/X86-64_Instruction_Encoding)
 - [uni of virgina/guide to x86 assembly](https://www.cs.virginia.edu/~evans/cs216/guides/x86.html)
 - [wikibooks/functions and stack frames](https://en.wikibooks.org/wiki/X86_Disassembly/Functions_and_Stack_Frames)
