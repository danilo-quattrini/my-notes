---
created: 2026-02-14T15:43:00
tags:
  - baby
topics:
  - Architecture 
  - "[[School]]"
  - Memory
author: Danilo Quattrini
---
# Memory Hierarchy
---
>[!quote] Definition
>The Memory hierarchy it's  defined on how the computer memory are placed into a ranking list, based on the response time. 

Means that different types of memory are placed in this ranking based on their complexity and capacity. We are going to consider two different types of ranking:
1. **Access Time** and **Size**![[Screenshot 2026-09-11 at 10.15.13.png]]
- In term of access time all the registers from the memory are speed to access information into the memory but they are relately small of their size.
- Cache memory (S.R.A.M) is a small, fast memory unit located close to the CPU. It stores frequently used data and instructions that have been recently accessed from the main memory. [Cache memory](https://www.geeksforgeeks.org/computer-organization-architecture/cache-memory-in-computer-organization/) is designed to minimize the time it takes to access data by providing the CPU with quick access to frequently used data.
Then we have the other memory components that follows the same idea, more you go deep into the pyramid then the access time it's slower and the size would be much bigger.

In terms of **Cost** and **Usage** things changes:
2. **Cost** and **Usage**
![[Screenshot 2026-09-11 at 10.20.49.png]]
# Reference
---

[Memory Hierarchy](https://en.wikipedia.org/wiki/Memory_hierarchy)