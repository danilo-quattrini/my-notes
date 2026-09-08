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
# ALU
---
The part of the processor that handle all the operation like multiplication, addition, subtraction and so on it's the *Arithmetic Logic Unit* (ALU). This is the core of the processor calculation, it perform operation by fetching data from the register and return the result of the operation into a new location inside the register. It can also return an *overflow flag* as result of one of its operations, like if a number it's over the size of the register, means reach the max size of the register then the flag would be 1, means the result of the operation it's bigger than the size capable from the register.

The Control Unit (CU) its responsible of giving signal to the ALU of the operation it should perform and also control the data in input and output of the ALU.

![[Pasted image 20260903095022.png|793]]

## Operation with Integers

### Adder
An **adder**, or **summer**,[[1]](https://en.wikipedia.org/wiki/Adder_\(electronics\)#cite_note-1) is a [digital circuit](https://en.wikipedia.org/wiki/Digital_circuit "Digital circuit") that performs [addition](https://en.wikipedia.org/wiki/Addition "Addition") of numbers. In many [computers](https://en.wikipedia.org/wiki/Computer "Computer") and other kinds of [processors](https://en.wikipedia.org/wiki/Microprocessor "Microprocessor"), adders are used in the [arithmetic logic units](https://en.wikipedia.org/wiki/Arithmetic_logic_units "Arithmetic logic units") (ALUs). They are also used in other parts of the processor, where they are used to calculate [addresses](https://en.wikipedia.org/wiki/Address_space "Address space"), [table indices](https://en.wikipedia.org/wiki/Database_index "Database index"), [increment and decrement operators](https://en.wikipedia.org/wiki/Increment_and_decrement_operators "Increment and decrement operators") and similar operations.

There are different kind of adder, but in this example we are going to see the half adder.
#### Half Adder
The **half adder** adds two single binary digits $A$ and $B$ . It has two outputs, sum ( $S$ ) and carry ( $C$ ). The carry signal represents an [overflow](https://en.wikipedia.org/wiki/Integer_overflow "Integer overflow") into the next digit of a multi-digit addition. The value of the sum is $2C + S$. The simplest half-adder design incorporates an [XOR gate](https://en.wikipedia.org/wiki/XOR_gate "XOR gate") for $S$ and an [AND gate](https://en.wikipedia.org/wiki/AND_gate "AND gate") for $C$. The Boolean logic for the sum (in this case $S$ ) will be $A \oplus B$ whereas for the carry ( $C$) will be $A ⋅ B$. With the addition of an [OR gate](https://en.wikipedia.org/wiki/OR_gate "OR gate") to combine their carry outputs, two half adders can be combined to make a full adder.

The truth table for the adder  (1 it's true and 0 is false) is

| Inputs |     | Outputs |     |
| ------ | --- | ------- | --- |
| $A$    | $B$ | $C$     | $S$ |
| 0      | 0   | 0       | 0   |
| 0      | 1   | 0       | 1   |
| 1      | 0   | 0       | 1   |
| 1      | 1   | 1       | 0   |
|        |     |         |     |
The logic schema with the XOR
![[Pasted image 20260903122946.png|500]]
[Schematic](https://en.wikipedia.org/wiki/Schematic "Schematic") of half adder implemented with one [XOR gate](https://en.wikipedia.org/wiki/XOR_gate "XOR gate") and one [AND gate](https://en.wikipedia.org/wiki/AND_gate "AND gate").
### Addition
To perform an addition the ALU need to use integers that are converted in binary format, in this case we cannot perform an operation with decimal value, but we should use binary value. 

For instance let's sum $2 + 5$, in this case the value $2$ in binary format, represented with 8 bit it's $0000 \ 0010$, and $5$ in binary it's the following number $0000 \ 0101$, to see how convert a number into a binary format [click here](https://www.geeksforgeeks.org/utilities/decimal-to-binary/)

$$
\begin{array}{rl} \phantom{+}0000\ 000^{1}1 & (2) \\ +\ 0000\ 0101 & (5) \\ \hline (1)\ 0000\ 0111 & (7) \end{array}
$$
It's just like the addition with two number the only difference it's that we should follow this rules:
- $1 + 1 = 0$ with the rest of  operation on top of the next number, like in operation before
- $1 + 0 = 1$
- $0 + 0 = 0$

### Subtraction

With the subtraction instead if we have two numbers $A$ and $B$ and we would like to subtract  $B$ from $A$, we should be converte $B$ into the Two's Complement format (Complemento a Due) and then perform the addition operation, what does it means? Why we are doing this conversion without simply use the subtraction operand?

Well the ALU to perform a subtraction need to add more area for transistor to do that, and a dedicate hardware for its operation. With Two's complement eliminates the need for separate subtraction hardware by converting subtraction into addition:
$$A - B = A + (-B)$$
- **Single Circuit:** The ALU uses the exact same addition hardware (Adder) for both addition and subtraction.
    
- **No "Double Zero":** Alternative methods (like Sign-Magnitude) result in two representations for zero ($+0$ and $-0$). Two's complement yields exactly one zero (`0000 0000`).
    
- **Unambiguous Sign:** The Most Significant Bit (MSB—the leftmost bit) acts as the sign bit: `0` for positive, `1` for negative.
## Two's Complement

To represent a negative number in binary (e.g., $-5$ using 8 bits):

**1. Write the positive binary value:**  Standard binary representation.

Convert $5$ into 8-bit **unsigned** binary:

`0000 0101`

**2. Invert all bits (One's Complement):** Flip every 0 to 1 and 1 to 0.

Flip each bit across the byte:

`1111 1010`

**3. Add 1 to the result:** Final step to complete Two's Complement.

Add $1$ to the inverted value:

`1111 1010` + `0000 0001` = `1111 1011`

### Multiplication
Binary multiplication uses the exact same "shift and add" method taught in grade-school decimal arithmetic, but simplified because binary digits are only `0` or `1`.

- Multiplying by `1` copies the multiplicand.    
- Multiplying by `0` produces all zeros.

**Step-by-Step Example: $6 \times 5 = 30$**

- $6_{10} = 0110_2$ (Multiplicand)
    
- $5_{10} = 0101_2$ (Multiplier)

$$\begin{array}{rl} \phantom{\times 00}0110 & (\text{Multiplicand } = 6) \\ \times\phantom{00}0101 & (\text{Multiplier } = 5) \\ \hline 0110 & (\text{LSB is } 1 \rightarrow \text{copy } 0110) \\ 0000\phantom{0} & (\text{Bit 1 is } 0 \rightarrow \text{shift left, add zeros}) \\ 0110\phantom{00} & (\text{Bit 2 is } 1 \rightarrow \text{shift left twice, copy } 0110) \\ +\ 0000\phantom{000} & (\text{Bit 3 is } 0 \rightarrow \text{shift left 3 times}) \\ \hline 0001\ 1110 & (\text{Sum } = 16 + 8 + 4 + 2 = 30) \end{array}$$
# Reference
---

