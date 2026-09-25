---
created: 2026-09-18
tags:
  - baby
topics:
  - Architecture 
  - Bus
author: Danilo Quattrini
---
# Address Bus
---
The address bus it's the one dedicate to send the location or the address of the component that the CPU or other components wants to comunicate with, either if it's to write or read data from a memory location.

## Communication Method
There is a **one-way** connection from the processor to the address bus and a **one-way** connection from the address bus to the main memory and to the I/O controllers. This is because the address bus is a **unidirectional** bus, which allows the processor to establish a connection with an addressable 'unit', whether it's a memory location or an I/O controller.

## Bus Width
The **width** of the address bus refers to its number of parallel lines, which determines **the number of bits that can be used to form an address** of a memory location. It is typically a multiple of a byte (e.g. 8, 16, 32, or 64 bits).

The formula it's the following one
$$2^n$$
where $n$ refers to the number of bits that can be used to form a bus
- If the width of the address bus is 8 bits, then there are $2^8=256$ numbers that can be used to address memory locations
- If the width of the address bus is 16 bits, then there are $2^{16}=65.536$ numbers that can be used to address memory locations

In general, if the width of the address bus is expressed as n bits, then there are 2n numbers that can be used to address memory locations.

# Reference
---

	