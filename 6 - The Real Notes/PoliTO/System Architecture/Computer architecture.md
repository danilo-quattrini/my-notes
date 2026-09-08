---
created: 2026-02-14T15:43:00
tags:
  - baby
topics:
  - Architecture 
  - "[[School]]"
author: Danilo Quattrini
---
# Computer architecture
---
**Computer architecture** is the conceptual design and operational structure of a [computer](https://en.wikipedia.org/wiki/Computer "Computer") system that define how component parts are organized and interact to execute [programs](https://en.wikipedia.org/wiki/Computer_program "Computer program") efficiently.

It has two part:
1. The [[Instruction Set Architecture|Instruction Set Architecture]], that's how the machine language program, interact with the computer.
2. Hardware System Architecture, that's deal wit the hardware component we are going to see below in the image. It also deal with how data / instruction are transfer within components.

It's a general description that avoid to go in more further detail of the concept, but it's relative to [instruction set architecture](https://en.wikipedia.org/wiki/Instruction_set_architecture "Instruction set architecture"), [CPU microarchitecture](https://en.wikipedia.org/wiki/Microarchitecture "Microarchitecture"), [memory](https://en.wikipedia.org/wiki/Computer_memory "Computer memory"), and [input/output systems](https://en.wikipedia.org/wiki/Input/output "Input/output").

![[Pasted image 20260828114901.png|748]]

This above it's an example of **computer architecture**, with a single **CPU**, Black lines indicate the flow of control signals, whereas red lines indicate the flow of processor instructions and data. Arrows indicate the direction of flow.

## Computer Organization
When we are talking about computer organization, we are referring to the structural relationship within the components, where the CPU, Memory, I/O Devices are linked together with a **System Bus**.

>[!info] Architecture VS Design
>The difference from the terminology of **Computer Organization** and **Computer Architecture**, it's how they deal with components it self. The first one it just put the major focus on how the hardware it's layout and organized. In the Architecture manner instead we just cover the **Design Implementation** for the various parts of the computer

The architecture that we saw above, take the name of [Von Neumann](https://en.wikipedia.org/wiki/Von_Neumann_architecture)  that's how the architecture of a computer / how computer it's organized internally. But we are going to see that's not the only one we can describe how internally it's made a PC

## Classification
We can classify a computer architecture in two distinct families:
### Von Neumann Architecture (Princeton Architecture).
![[Pasted image 20260829225729.png|770]]
It has 3 basics hardware sub-system, **CPU, Memory and Input / Output device**s, in order to be a Von Neumann architecture **it should be a store program computer**.

What does it means a store program computer?

It means that the **Main Memory** (Memory Unit) **should store the program that control the computer operation and the computer it self can manipulate this program it self too.** (Cioè le operazioni che il computer dovrà svolgere sono salvate in programma presente nella memoria principale, inoltre tale programma può essere gestito dal computer stesso). 

Also the main memory carry each operation that the CPU should perform **sequentially one operation at time**. The only thing this architecture lack it's the separation of buses for the different operation the CPU should perform.

In the Von Neumann architecture **there is only one System Bus from the CPU to the Main Memory**.

>[!danger] What's the problem ?
> All the data and the operation live in the same hardware memory component, so there's no separation of concern about memory that save data and memory that save operation.

In the end this is a bottleneck and a [CPU](https://en.wikipedia.org/wiki/Central_processing_unit "Central processing unit") cannot simultaneously read an instruction and read or write data from or to the memory, but it should perform each operation one at time.
### Non - Von Neumann Architecture (Harvard and Modified Harvard).
![[Pasted image 20260829231221.png]]

We have separate memory unit one for operations and the other for storing data. This improve processor operation, **introducing a way that the CPU can read instruction and data at same time without waiting for one to finish** (Introduce il concetto del parallelismo, dove la CPU può performare operazioni in parallelo, senza dover aspettare il completamento dell'operazione precedente).
#### Modified Harvad Architecture
![[Screenshot 2026-08-29 at 23.28.17.png]]

The architecture it's visually the same, the only difference it's that the division of Data Memory and Instruction Memory it's less thight and more relaxed (that's because the Processor if it need some Instruction or Data that has been discovered before it can access it through the cache). The Processor (CPU), now has a **Cache** where it saves the operation that has been performed before.

>[!important] Harvard vs Von Neumann
>Harvard architecture introduce a more complex concept that's the parallelism and also this can improve the cost of the PC in term of operations. Where the Von Neumann it's easier to understand and have reduced costs.
# Reference
---

[Harvard Architecture](https://www.geeksforgeeks.org/computer-organization-architecture/harvard-architecture/)