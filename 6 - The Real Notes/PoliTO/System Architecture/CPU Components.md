---
created: 2026-02-14T15:43:00
tags:
  - baby
topics:
  - Architecture 
  - "[[School]]"
author: Danilo Quattrini
---
# CPU Components
---
![[Pasted image 20260918100554.png|836]]

From the image we can see how the CPU it's internally made with different internal components that interact with each other in order to send data or instructions. All these components are connected to each other with buses. For now we just see how they work each of them.

## MAR (Memory Address Register)
it's the register of the CPU that saves the memory address of the instruction or data fetch from the main memory

## MBR (Memory Data Register or Memory Buffer Reader )
It's the register who saves the current instruction or data that it's performed or read from the CPU, it saves the data it self

## PC (Program Counter)
It's the register who saves the next instruction to be performed by the CPU, in this case the PC copy the memory address from the MAR and increments it. The PC increment the memory address after the instruction has immediately fetch from the memory

## CIR or IR (Current Instruction Register or Instruction Register)
it's the register who saved the memory address of the current operation performed by the CPU, more details in this part [[Control Unit (CU)#Instruction Register (IR)|Instruction Register]]
## CU (Control Unit)
The Control Unit it's the part of the CPU that deals with instructions, it fetch instruction from the memory, decode them and execute. The CU generate timing signals and direct other component inside the computer and the CPU like ALU, memory, I/O components and so on, it's like a director that deals with other orchestrants and give orders to them.

The operation performed by the CU are the following one:
- Coordinate and control internal component of the CPU.
- Manage the flow of the instruction to other components inside the CPU.
- Accept instruction from the memory.
- Decode (translate or interpretate) instruction to be executed by the ALU
- Store the result or data back to the memory.

## ALU (Arithmetic Logic Unit)

The Arithmetic Logic Unit it's an internal component of the CPU that deals with calculations and operations like addition, subtraction, multiplication and so on, it takes data in input and return results of the operation in output.

## Status Flag
There is a register internally in the CPU that is task is to check the result of the last operation made from the ALU, the name of the register could be something like (**FLAGS**, **PSW**, **SR**) and these are some example of these flags:
- **Z (Zero flag)**:
    - Z = 1 if the result of the operation it's 0
    - Z = 0 of it's different from 0
- **N (Negative flag)**:
    - N = 1 if the result of the operation it's negative  ([[Calculator Arithmetic#Two's Complement|Two Complement]])
- **C (Carry flag)**:
    - indica se c’è stato un riporto/“carry” in un’addizione o un borrow in una sottrazione 
- **V (Overflow flag)**:
    - The result of an operation it's overflow, that means the operation reach the maximum number of bits available
>[!example]
> Let's take an instruction of this form `CMP R1, R2` we are comparing two registers with different values, the operation of the `CMP` it's performed by the ALU just subtracting `R1-R2` without saving the result, if the result of the subtraction it's ZERO, then the zero flag Z will be 1 and it will be used into another instruction. 
> 
> For instance if the instruction `JE label` (Jump if equal) it will look up at the Z flag and if it's 1 that's true then it will jump to `label` otherwise none.

>[!info] Summarize
>the flag it's a bit that explain and identify the result of an operation. they are used for decisions and jumps.

## Accumulators VS General Pupose Registers
In old machine or old CPU (8086, 6502) or some didacticals machines there are these accumulators (ACC) that's a special register used for save the result of the operation, for instance the operation to add a specific value into the accumulator it's the following one:
```
ADD X -> ACC = ACC + [X]
```

Where the `[]` square brackets means that the value of `X` it's a memory address and we access to the value of it through the square brackets (like arrays with indexes), but the part we are interested it's that the accumulator here **the accumulator act as operand and destination of every operation**.

In moderns architectures there are ([[RISC|RISC]], x86 a 32/64 bit, ecc.) there are instead these **general purpose registers** (R0–R15, EAX/EBX/ECX/EDX, ecc), these register are as the name said for every type of operation, because they are general purpose. General purpose registers are a set of registers that can be used flexibly by many different instructions; the instruction explicitly says which registers to use.

>[!quote] Summarize
>**Instruction dictate which register use for different operations** 
# Reference
---

