---
created: 2026-02-14T15:43:00
tags:
  - baby
topics:
  - Architecture 
  - "[[School]]"
  - Microprocessors
author: Danilo Quattrini
---
# Instruction Set Architecture (ISA)
---
## ISA Outline
- [[#Memory Addressing|Memory Access]]
- [[#Operations in the Instruction Set|Operation in the Instruction Set]]
- Type and Size of Operands
- Instruction Encoding

## Definition
The language that the CPU can understand it's a list of instruction that tells to the CPU what operation it should perform. such as adding numbers, loading data, or jumping to another instruction. It **defines how software communicates with hardware through specific instruction** rules and formats.

All machines today are general purpose machines (GPR), that's because register are faster than memory and they are easier for a compiler to use. The quantity of register are usually more than 16, where 32 register are for user.

An ISA may be classified in a number of different ways. A common classification is by architectural _complexity_. 

A [complex instruction set computer](https://en.wikipedia.org/wiki/Complex_instruction_set_computer "Complex instruction set computer") (CISC) has many specialized instructions, some of which may only be rarely used in practical programs.

A [reduced instruction set computer](https://en.wikipedia.org/wiki/Reduced_instruction_set_computer "Reduced instruction set computer") (RISC) simplifies the processor by efficiently implementing only the instructions that are frequently used in programs, while the less common operations are implemented as subroutines, having their resulting additional processor execution time offset by infrequent use

 It includes: 

- Instruction types (ADD, LOAD, JUMP), registers, data types, and memory access
- Interrupt handling and system-level communication

>[!info] 
>Some Popular ISAs are x86 (PCs), ARM (phones), MIPS (education), RISC-V (open source).

For the complete list check the [link here](https://thebestcpu.com/list-of-cpu-instruction-sets/) where there are all the instruction sets that a CPU can understand, these are different depending of the type of the CPU we are working on.

## Load-Store
Architecture Load-Store or also called Register to Register, it means that to access into memory it's only possible to access with load an store operation. All machines today use this architecture and the *data memory* is only accessed through *Load* and *Store* instruction.

The CPUs can be classified according to:
- Typical number of operands per ALU instruction (2 or 3)
- Typical number of memory operands per ALU (from 0 to 3), there are no real cases use 3 memory accesses during one computation. To be cheap we are going to use only 2 operands
ARM and RISC-V they are Load-Store architecture

## Memory Addressing
There are data saved in memory saved in bytes and they are represented as hexadecimal values, there are two ways of organize the data inside the memory:
- **Little Endian vs. Big Endian**
- **Aligned vs. misaligned accesses**
### Little Endian vs Big Endian
In memory if we use the Little Endian the value it's in the highest value of the memory, where the MSB it's in the higher part of the memory where the LSB it's in the lowest.
![[Screenshot 2026-09-25 at 10.22.24.png]]
### Big Endian
The start address it's always 100, but in 100 there's the MSB value of 7 in the image we are going to see below, the LSB it's going to be in the highest part of the memory.
![[Screenshot 2026-09-25 at 10.24.41.png]]
### Aligned
If the memory it's aligned the address, the value that I'm going to save will be saved in the odd position. The address of the memory should be the result of the operation module % 4, for instance if the memory address % 4 it's 0 then it will be saved in memory.![[Screenshot 2026-09-25 at 10.27.38.png]]
### Misaligned
![[Screenshot 2026-09-25 at 10.28.00.png]]

## Addressing Mode
In GPR machines an addressing mode specifies a constant, a register, or a memory location (through its effective address). We should know of the process calculate the location of the data that we are going to save.
- Register Mode
- Immediate Mode
- Displaced Mode
- Register Deferred
- Indexed Mode
- Direct
- Memory Indirect
- (Post )Autoincrement Mode
- (Pre) Autodecrement Mode
- Scaled Mode
### Register Mode
![[Screenshot 2026-09-25 at 10.31.02.png]]
R4 it's an operand and a source, it's a register that it's possible to access its value and use it to save its result.
### Immediate Mode
![[Screenshot 2026-09-25 at 10.33.54.png]]
When I need to save a constant into a register or use the constant for an operation as operand. The *immediate value it's limited*, means that the value should be reasonable big, the value `#3` it came from outside
### Displacement
![[Screenshot 2026-09-25 at 10.35.57.png]]
We are creating a vector, where the first element of the vector it's saved in memory, where each vector position it's a size of 4 bytes, The register R1 is used for vector. The element inside a memory it's a dimension of 32 bits and the size represented in Gb it's 4. so in end the displacement access it's the fixed memory position + the register.
### Register Deferred
![[Screenshot 2026-09-25 at 10.41.45.png]]
We are saying that inside the register there's the memory address of the value we want to access. The `R1` there's the memory address of the value we want to use for the operation.

### Absolute Mode
![[Screenshot 2026-09-25 at 10.44.23.png]]
I'm using the specific index of the memory address

### Memory Indirect![[Screenshot 2026-09-25 at 10.46.08.png]]
We are representing a pointer, that's point the memory location of the value, we read the index of the pointer and the value of the index we are going to read the value.

## Choosing the Memory Addressing Mode
To choose the best memory addressing mode we should consider these facts:
- **Reduce the number of instruction**
- Avoid to Increase the CPU architecture complexity
- Avoid to Increase the Average Cycle Per Instruction (CPI)
![[Screenshot 2026-09-25 at 10.50.48.png]]

The issue we should consider it's how many bits should be devoted to it in the instruction code? Means how large can be the **immediate value**

## Operations in the Instruction Set![[Screenshot 2026-09-25 at 10.56.12.png]]
All arithmetics operation, operations to move data from one register to another, comparision within values and more operation that we can see from the image above. They can be operation to make the system secure, for instance read and decrypt a key.,
# Reference
---

