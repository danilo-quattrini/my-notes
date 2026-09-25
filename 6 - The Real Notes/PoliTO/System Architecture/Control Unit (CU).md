---
created: 2026-02-14T15:43:00
tags:
  - baby
topics:
  - Architecture 
  - "[[School]]"
author: Danilo Quattrini
---
# Control Unit (CU)
---
>[!quote] Definition
>The Control Unit it's a internal component of the CPU that direct computer components and the one who are inside the CPU. It deals with instruction and generate timing signals and direct CPU components like ALU, memory, I/O components and so on, it's like a director that deals with other orchestrants and give orders to them.

The CU has internally a **Program Instruction Decoder**, it deals with translate / decode instruction that are in the [[#Instruction Register (IR)|Instruction Register]] As we can see from the image below these are all the inner operation / component made from the CU.
![[Screenshot 2026-09-15 at 09.56.54.png]]

## Timing Unit
The timing unit it's the part of the CU that deals with electrical signal, where each signal it's defined as **clock signal**. The timing unit internally consist of quartz oscillating crystal that generates the analog signals. These analog signals are converted into digital sign wave by a analog to digital converter.

![[Screenshot 2026-09-15 at 10.05.28.png]]
This above it's an example of quartz oscillator.

And the operation that the CU perform they are sequence of oscillations of these digital sign.
![[Screenshot 2026-09-15 at 10.13.35.png]]
Where the time period it's the time to complete the specific circle of 1-0, when the 1-0 it's completed that's a time period denominated $T_{1}$, so the time period to fetch an instruction from the image we see above it's $T_{1} + T_{2}$, we can say like 2 Clock Cycle, to execute an instruction instead it's from $T_{3}+T_{4}+T_{5}$ 3 Clock Cycle, there are formulas and more to know about this topic in this [link](https://www.uvm.edu/~cbcafier/cs2210/content/02_basics_of_architecture/basic_performance_metrics.html) that's important to know how measure the CPU speed. 

In few words there are 3 metrics to measure the CPU speed, 
1. the first it's the number of instruction that the CPU should perform, called ****IC** *(Instruction Counter)
2. ***CPI*** (Cycle Per Instruction) average number of clock cycles each instruction requires to complete. CPI depends on the microarchitecture of the processor. Simple instructions may take one cycle, while more complex instructions can take multiple cycles.
3. ***Clock Cycle Time***: is the duration of a single cycle. It is the reciprocal of the clock frequency. A 2 GHz processor has a cycle time of 0.500 nanoseconds, while a 3 GHz processor has a cycle time of about 0.333 nanoseconds.
To understand performance, computer architects use a fundamental equation that breaks down CPU execution time into three factors:

$$ CPU \ time= Instruction \ Count * CPI * Clock \ Cycle \ Time$$

### Clock Speed Calculation
How calculate the speed of a processor with frequency? Like how to know the time of the processor speed. Let's first consider the table below.![[Screenshot 2026-09-07 at 10.07.16.png]]
That it can be translated to $\frac{1}{2} * 10^{-9}$  that's $\frac{1}{2}$ nanoseconds a CPU can perform a task.

## Program Counter
The program counter it's an internal register of the CPU that deals with operation of increasing the memory location to the next instruction to be performed by the CPU . The first time the CPU should perform an operation it has to fetch the location of the instruction for that operation into the memory. 

After the instruction has been fetch and completed by the ALU or other components, the PC (Program Counter) fetch the memory location saved in the register MAR (Memory Address Register), increase its value by one, and then the CPU takes the Memory Address incremented from the PC.
![[Screenshot 2026-09-15 at 11.12.32.png]]


## Instruction Register (IR)
The instruction register[^1] it's an internal register of the CU that deals with saving the current instruction decode and executed from the CPU. It saves the instruction word fetch from the memory temporarily.

There are different types of IR but the basic structure of the it's the following one:
![[Pasted image 20260915112037.png]]

The part of the instruction are these one:
- ***Opcode:*** This field specifies the operation to be performed by the CPU, such as addition, subtraction, or data transfer.
- ***Operands:*** These fields contain the data or references (addresses) to data on which the operation acts.
- ***Addressing Mode:*** This specifies how to interpret or locate the operand, such as direct, indirect, or immediate addressing, there are detailed explanation in this [link](https://medium.com/@prajun_t/addressing-modes-and-instruction-classes-2dc559d19939) 
  
That's another example of how it's interpretate / decode an Instruction
![[Pasted image 20260915120512.png]]
# Reference
---

[^1]: For additional content check here [link](https://www.geeksforgeeks.org/computer-organization-architecture/computer-organization-instruction-formats-zero-one-two-three-address-instruction/).
