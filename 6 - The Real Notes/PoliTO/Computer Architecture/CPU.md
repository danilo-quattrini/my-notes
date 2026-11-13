---
created: 2026-02-14T15:43:00
tags:
  - baby
topics:
author: Danilo Quattrini
---
# CPU
---
Let's start by saying that the microprocessor / processor —also known as the CPU—is the brain of all electronic devices in the world. Many differ from one another in terms of their internal architecture or the arrangement of their various components, but for all of them they follow the same concept.

Let's have a general view of the CPU
![[Pasted image 20260911115826.png|754]]

As we can see above there are several component inside the CPU that are notice to work with the first we are going to see it's the:
## Functions of the CPU 
The functions of the CPU involve processing instructions from programs and controlling all operations within the computer. This is carried out through a sequence known as the Fetch-Decode-Execute-Store cycle:

- **Fetch:*** The CPU retrieves the instruction from main memory, through a coordinate process from the CU and a bus that send this data (RAM).
- ***Decode:*** The Control Unit interprets the fetched instruction to determine the required operation.
- **Execute:** The CPU performs the operation using the appropriate hardware components such as the ALU.
- **Store:*** The result of the executed instruction is written back to memory or a register.

## Instruction Cycle
In the process of the fetch decode and execute, it starts with  fetching the instruction from the memory, the instruction memory address it's saved in the PC and the value of that instruction in the MBR or MDR, the PC increment its value to 1 and  send the value of the memory address to the MAR . The instruction to be execute by the CPU it's saved in the IR and decode from the CU . The instruction has a *Opcode* that define the operation to perform the *Operand* that's the value or the instruction contained in the Instruction. The CU after decode the instruction, it decide which of their internal or external component send the "order" to perform the instruction requested. For instance if the instrunction it's and addition, then it will send the data to the ALU and the ALU will perform the operation and send back the result.

The concept we are going to see about the CPU are the following:
- [[CPU Components]]
- [[Calculator Arithmetic]]
- [[Base Architecture of a Microprocessore]]
# Reference
---

