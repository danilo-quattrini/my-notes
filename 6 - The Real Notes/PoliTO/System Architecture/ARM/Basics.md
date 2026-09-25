---
created: 2026-09-18
tags:
  - baby
topics:
  - "[[School]]"
  - Architecture 
  - ARM
author: Danilo Quattrini
---
# Registers
---
We are going to simulate an ARM cpu with register dimension of 32 bits for each register, each of them they are represent as hexadecimals, where each bit number it's 4 bit.

 I use the website [CPUlator](https://cpulator.01xz.net/?sys=arm) to follow along to the tutorial, now let's dive in into the website.
![[Screenshot 2026-09-18 at 21.31.48.png|850]]

From register 1 to 6 these are considered general purpose registers, the register we saw in the theory when we talk about [[CPU Components#Accumulators VS General Pupose Registers|Accumulator VS General Purpose Registers]], for any kind of operation.

The r7 it's a special register for software interrupt call, this register will keep the system call number, for all the list of system call we have al link [here](https://chromium.googlesource.com/chromiumos/docs/+/master/constants/syscalls.md)

![[Screenshot 2026-09-18 at 21.36.24.png|880]]

Another important register it's the **Stack Pointer** (sp in the figure above), that's pointing to the next location available in the Stack, this is used if there's not enough space to store values into the general purpose registers and we want to store more data.

The **Program Counter** that we already know what it's doing check [[CPU Components#PC (Program Counter)|here]]

Then there's the **cpsr** that stands for **Current Program Status Register**, these register it's reserved for special flags that can be turned on if we make some operations, for a list of all flags and how they are active, see there also [here](https://arm.jonpalmisc.com/latest_sysreg/AArch32-cpsr).

For instance if we subtract two register with the same number
```assembly
mov r1, #3
mov r0, #3
subs r2, r0, r1 // we are subtract r1 from r0 and save the result on r2
```
the operation above involves the flag **Z** (Zero Flag) to turn on, from the image we see that there are different types of flags, most of them we saw in here [[CPU Components#Status Flag|Status Flag]]
>[!warning] Warning
>To activate the Current Program Status Register we need to add the S flag in front of the operand, like {subs, adds, mults, ecc}
## .global
The global it's a [^1]directive that specify that a label it's available outside the file and accessible to other modules, in the example above we use the label `_start` because it's the entry point of the program. 

## Why use the `_start` label?
Because the Linux linker (`ld`) and OS loader (which loads executables into memory) default to looking for a symbol named `_start` as the entry point.

>[!info]
>You _can_ use a different name (e.g., `my_entry`), but you’d have to explicitly tell the linker with the `-e` flag (e.g., `ld -e my_entry -o program program.o`). Using `_start` avoids this extra step.

# Reference
---
The video course about ARM: [here](https://www.youtube.com/watch?v=kKtWsuuJEDs&list=PLn_It163He32Ujm-l_czgEBhbJjOUgFhg)
Linux System Call Table: [here](https://chromium.googlesource.com/chromiumos/docs/+/master/constants/syscalls.md)

[^1]: **directives**: are the commands or instructions that control the operation of the assembler, they are the instruction provided to the assembler. 
