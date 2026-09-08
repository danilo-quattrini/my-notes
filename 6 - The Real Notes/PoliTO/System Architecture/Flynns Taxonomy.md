---
created: 2026-02-14T15:43:00
tags:
  - baby
topics:
  - Architecture 
  - "[[School]]"
author: Danilo Quattrini
---
# Flynns Taxonomy
---
This classification was proposed by [Micheal John Flynn](https://en.wikipedia.org/wiki/Michael_J._Flynn) in 1966.

This is another way of classify a computer architecture based on the number of processor, the number of program it execute (instruction it can process) and the memory structure it use.

There are four group of how we can classify computer architecture in this way:

## SISD (Single Instruction Single Data)
This is the category the Von Neumann take parts, this group has a single instruction stream (**stream** in italiano significa flusso, quindi singolo flusso di istruzioni). 

- **One CPU  that execute one instruction at the time**
- One stream / bus where it's possible to fetch and send data to the memory

![[Screenshot 2026-08-30 at 23.10.53.png]]

In the image about there's only one bus / stream where the CPU can retrive data and send the result to the main memory, **they have only one ALU (Arithmetic Logic Unit)**.

## SIMD (Single Instruction Multiple Data)
Processor are falling in this category of computer architecture, the characteristic of this family it's that:

- The CPU it has always **one instruction stream where the memory pass the instruction.**
- It has more than one ALU, so the same instruction passed from the control it's shared with different Operator.
![[Screenshot 2026-08-30 at 23.19.20.png]]

In the example above the ALU's interact with the same memory but they retrive different data and return different results. SIMD model are well suited to scientific computing since they involve lots of vector and matrix operations

## MISD (Multiple Instruction Single Data)
The system performs different operations on the same data set. Machines built using the MISD model are not useful in most of the application, a few machines are built, but none of them are available commercially.

## MIMD (Multiple Instruction Multiple Data)
These are known as multi processor machines where, there are different processor that handle different instruction and has different instruction stream. Also each processor has its own ALU that process data and return results.
![[Screenshot 2026-08-30 at 23.27.11.png]]

MIMD machines are classified into ***shared-memory*** and ***distributed-memory*** models depending on how processors connect to memory. In the example above we are in the scenario of a shared memory, where a change made from one instruction from a CPU it's visible from another CPU too. Where the **distributed memory** every processor has its own local memory were it works on and comunicate with each other through interconnection network.

>[!question] Why that?
>Shared-memory systems are easier to program but harder to scale and more vulnerable to failures, since a fault can affect the whole system. In contrast, distributed-memory systems are more scalable and fault-tolerant, since each processor is independent. For real-world use, distributed-memory MIMD is generally considered ****superior for large-scale and high-performance computing****, due to their scalability, reliability, and ability to handle complex tasks efficiently

# Reference
---
[GeekForGeeks](https://www.geeksforgeeks.org/computer-organization-architecture/computer-architecture-flynns-taxonomy/)
