---
created: 2026-09-25
tags:
  - devoleped
topics:
  - Architecture 
  - "[[School]]"
  - Microprocessors
author: Danilo Quattrini
---
# Instruction Set Architecture (ISA)
---
## Questions
### Concetti Fondamentali e Classificazione delle ISA

1. **Cos'è un'ISA?** Qual è il suo ruolo primario nel sistema informatico e perché viene definita come l'interfaccia tra software e hardware?
    
2. **Perché le architetture moderne sono General Purpose Register (GPR)?** Quali sono i tre principali vantaggi dell'uso dei registri rispetto all'accesso diretto alla memoria?
    
3. **CISC vs RISC:** Come differiscono in termini di complessità e frequenza d'uso delle istruzioni? In che modo le operazioni meno frequenti vengono gestite in un'architettura RISC?
    
4. **Qual è la differenza fondamentale** tra un'architettura _Register-Memory_ e un'architettura _Load-Store_ (o Register-to-Register)? A quale categoria appartengono architetture come RISC-V, ARM e MIPS?
### **Organizzazione della Memoria e Indirizzamento**

5. **Little Endian vs. Big Endian:** Come viene posizionato il byte più significativo (MSB) in memoria nei due sistemi?
    
6. **Accesso Allineato vs. Disallineato:** Cosa rende un accesso alla memoria "allineato"? Qual è la condizione aritmetica (con l'operatore modulo `%`) per verificare l'allineamento a 32 bit?
    
7. **Modi di Indirizzamento dell'Operando:** Riesci a spiegare brevemente e fare un esempio del funzionamento dei seguenti modi di indirizzamento?
    
    - **Register Mode** e **Immediate Mode**
        
    - **Displacement Mode** e **Register Deferred**
        
    - **Absolute / Direct Mode** e **Memory Indirect**
        
8. **Selezione dei Modi di Indirizzamento:** Quali fattori chiave bisogna considerare quando si sceglie quali modi di indirizzamento supportare nell'ISA?
### **Operazioni, Controllo di Flusso e Codifica (Encoding)**

9. **Destinazione del Branch:** Perché gli indirizzi di salto/branch vengono solitamente calcolati tramite _displacement_ (offset) rispetto al Program Counter (PC) anziché usando un indirizzo assoluto?
    
10. **Valutazione delle Condizioni di Salto:** Quali sono i tre approcci con cui un processore valuta se prendere o meno un branch? _(Es. Condition Code, Condition Register, Compare and Branch)_
    
11. **Codifica delle Istruzioni (Instruction Encoding):**
    
    - **Decodifica Variabile:** Quali sono i vantaggi (es. dimensione del codice) e gli svantaggi (es. impatto su CPI/clock)?
        
    - **Decodifica Fissa:** Per quale motivo semplifica l'hardware dell'unità di fetch/decode e migliora le prestazioni?
        
    - **Decodifica Ibrida:** Qual è un esempio classico di questa codifica e qual è il suo scopo principale?
---
## ISA Outline
- [[#Memory Addressing|Memory Access]]
- [[#Operations in the Instruction Set|Operation in the Instruction Set]]
- [[#Type and Size of Operands|Type and Size of Operands]]
- [[#Instruction Set Encoding|Instruction Encoding]]
---
## Definition

>[!quote] Instruction Set Architecture (Definition)
>The language that the CPU can understand it's a list of instruction that tells to the CPU what operation it should perform. such as adding numbers, loading data, or jumping to another instruction. It **defines how software communicates with hardware through specific instruction** rules and formats.

## General Purpose Registers
All machines today are general purpose machines (GPR), that's **because register are faster than memory and they are easier for a compiler to use**. The size of register are usually more than 16 bit, where 32 bit register are for user.

Also it's better to use registers instead of the memory directly to store the value of any variable. When variables are allocated to registers, the memory traffic reduces, the program speeds up (since registers are faster than memory), and the code density improves (since a register can be named with fewer bits than can a memory location).

An ISA may be classified in a number of different ways. A common classification is by architectural _complexity_. 

A [complex instruction set computer](https://en.wikipedia.org/wiki/Complex_instruction_set_computer "Complex instruction set computer") (CISC) has many specialized instructions, some of which may only be rarely used in practical programs.

A [reduced instruction set computer](https://en.wikipedia.org/wiki/Reduced_instruction_set_computer "Reduced instruction set computer") (RISC) simplifies the processor by efficiently implementing only the instructions that are frequently used in programs, while the less common operations are implemented as subroutines, having their resulting additional processor execution time offset by infrequent use.

>[!info] 
>Some Popular ISAs are x86 (PCs), ARM (phones), MIPS (education), RISC-V (open source).

For the complete list check the [link here](https://thebestcpu.com/list-of-cpu-instruction-sets/) where there are all the instruction sets that a CPU can understand, these are different depending of the type of the CPU we are working on.

## Classes of Register Computer
There are two classes of register computer that we are going to discuss here:
- **Register to Memory Architecture**: that access into memory for any kind of instruction
- [[#Load-Store|Load-Store]]: It's an architecture that can access into memory with only load and store operations.
### Load-Store
Architecture Load-Store or also called Register to Register, **it means that to access into memory it's only possible to access with load an store operation**. All machines today use this architecture and the *data memory* is only accessed through *Load* and *Store* instruction.

The CPUs can be classified according to:
- **Typical number of operands** per ALU instruction (2 or 3)
- Typical number of memory operands per ALU (from 0 to 3), there are no real cases use 3 memory accesses during one computation. To be cheap we are going to use only 2 operands
**ARM, RISC-V and MIPS they are Load-Store architecture**

## Memory Addressing
We should specify how the memory it's addressed an interpreted in each type of architecture, independently if it's a load-store architecture or a memory-to-memory one.The measurements presented here are largely, but not completely, computer independent. In some cases the measurements are significantly affected by the compiler technology
### Interpreting Memory Addresses
There are data saved in memory saved in bytes and they are represented as hexadecimal values, there are two ways of organize the data inside the memory:
- **Little Endian vs. Big Endian**
- **Aligned vs. misaligned accesses**

All the instruction sets discussed provide access for bytes (8 bits), half words (16 bits), and words (32 bits)
#### Little Endian
In memory if we use the Little Endian, where the MSB (Most Significant Byte) it's in the higher part of the memory where the LSB it's in the lowest. In order first it will start to save the address from the LSB to the MSBOt, if we see the image below.
![[Screenshot 2026-09-25 at 10.22.24.png]]
#### Big Endian
Stores the most significant byte (the "big end") first. This means that the first byte (at the lowest memory address) is the largest, which makes the most sense to people who read left to right.
![[Screenshot 2026-09-25 at 10.24.41.png]]
#### Memory Alignment
##### Aligned
If the memory it's aligned the address, the value that I'm going to save will be saved in the odd position. The address of the memory should be the result of the operation module % 4, for instance if the memory address % 4 it's 0 then it will be saved in memory (that's for the example of the word type that's 4bytes).![[Screenshot 2026-09-25 at 10.27.38.png|1080]]
>[!quote] General Rule
>To access into an object of size $s$ at a byte address of $A$ if $A$ module $s$ is equal to zero:
>$$\text{Accesso allineato} \iff A \bmod s = 0$$
>Then it means it's aligned. 

For instance if the memory:

**Byte ($s = 1$ byte):** every address is aligned.
    
- $A = 7 \implies 7 \bmod 1 = 0$ $\rightarrow$ **Allineato**
        
**Half-word ($s = 2$ byte):** every address must be even to be aligned ($A \bmod 2 = 0$).
    
- $A$ = `0x10000004` $\implies$ `0x100000044`$\bmod$ `2` = `0` $\rightarrow$ **Allineato**
        
- $A = 5 \implies 5 \bmod 2 = 1$ $\rightarrow$ **Non allineato (Misaligned)**
        
**Word ($s = 4$ byte):** L'indirizzo deve finire con numeri divisibili per 4 ($A \bmod 4 = 0$).
    
- $A = 12 \implies 12 \bmod 4 = 0$ $\rightarrow$ **Allineato**
       
  - $A = 14 \implies 14 \bmod 4 = 2$ $\rightarrow$ **Non allineato**
        
**Double-word ($s = 8$ byte):** L'indirizzo deve essere un multiplo di 8 ($A \bmod 8 = 0$).

##### Misaligned
![[Screenshot 2026-09-25 at 10.28.00.png]]
##### Why we metter about alignment
Every modern calculator today read 4 bytes / 8 bytes block into a memory bus, where each block of memory it's divisible by four.
![[Screenshot 2026-10-04 at 19.11.18.png]]
from the image we see above each memory section has an index that's divisible of 4 and each and if the access it's aligned then for instance :
```
[Block 0: Byte 0, 1, 2, 3] | [Block 1: Byte 4, 5, 6, 7]
```
**Aligned**: if we have a word $s$ of 4 bytes  loaded in the **Block 1**  into Byte 4 then it will only perform 1 access to the memory to read the value of word $s$

**Mis-aligned**: If the memory is mis-aligned and the word $s$ is in position `3` (that means it will occupy from position `3` to position `6`) then to read the first part of the word $s$ it should access to Block 0 and later to Block 1 to read position `4` to `6`.

Facciamo una tabella riassuntiva dei concetti di **Allineamento** e **Endianness**, perché è facile confonderli perché riguardano entrambi come la memoria viene interpretata, ma risolvono due problemi totalmente diversi:

| Concetto                          | Risponde alla domanda                                                            | Problema gestito                                                                               |
| --------------------------------- | -------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------- |
| Allineamento (Aligned/Misaligned) | A che indirizzo posso posizionare o leggere un dato di $s$ byte?                 | **Efficienza dell'Hardware e dei Bus** (quanti cicli di memoria servono per caricare il dato). |
| Endianness (Big/Little Endian     | In che ordine sono disposti i byte di un singolo dato all'interno della memoria? | **Rappresentazione e Interpretabilità dei Byte**.                                              |

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

### Memory Indirect
![[Screenshot 2026-09-25 at 10.46.08.png]]
We are representing a pointer, that's point the memory location of the value, we read the index of the pointer and the value of the index we are going to read the value.

## Choosing the Memory Addressing Mode
To choose the best memory addressing mode we should consider these facts:
- **Reduce the number of instruction**
- Avoid to Increase the CPU architecture complexity
- Avoid to Increase the Average Cycle Per Instruction (CPI)
![[Screenshot 2026-09-25 at 10.50.48.png]]

The issue we should consider it's how many bits should be devoted to it in the instruction code? Means how large can be the **immediate value**

## Operations in the Instruction Set
![[Screenshot 2026-09-25 at 10.56.12.png]]
All arithmetics operation, operations to move data from one register to another, comparision within values and more operation that we can see from the image above. They can be operation to make the system secure, for instance read and decrypt a key

### RISC-V Instruction frequency
![[Screenshot 2026-09-25 at 11.01.24.png]]

### Destination Address
It is normally specified as a displacement with respect to the current value of the [[CPU Components#PC (Program Counter)|Program Counter]]. In this way:  we save bits, since the target instruction is often close to the source one and  the code is position-independent.

### Evaluating Branch Condition
I need to change the flow of the program in base of the condition we set. How the processor save these conditions? There are three cases:
![[Screenshot 2026-09-25 at 11.11.28.png]]
We are going to see the first one the **Condition Code** that's is save in ARM into a special register called [[Basics#^270b34|CPSR]].

In MIPS we use the second case where there's a **Condition Register** and in RISC-V we use the **Compare and Branch**

### Procedure
The procedure it's a dedicate section of the program were it will execute some operations, in this case from an instruction we move into a specific dedicated program that execute some code and then returns a result.

## Type and Size of Operands
Per calcolare l'impronta della memoria (**memory footprint**) si **fa semplicemente sommando tutti i dati che si sono dichiarati nella `.data` di un programma in assembly**.

**Byte (`.byte`)**: $1\text{ byte}$
**Single-Precision Float (`.float`)**: $4\text{ bytes}$ ($32\text{ bits}$)
**Word (`.word`)**: $4\text{ bytes}$
 **Double-Precision Float (`.double`)**: $8\text{ bytes}$ ($64\text{ bits}$)

## Instruction Set Characterist
It's a set of one and zero  and it depends on  which instructions compose the Instruction set and which addressing modes are supported. When a high number of addressing modes is supported, an address specifier field is used to specify the addressing mode and the registers which are possibly involved. When the number of addressing modes is low, they can be encoded together with the opcode.

## Instruction Set Encoding
La decodifica dell'istruzione dipende da due fattori:
1. Da che cosa è composta l'istruzione
2. Quale metodo di indirizzamento sono supportati
### Decodifica Variabile
![[Screenshot 2026-09-29 at 08.39.22.png]]
La quantità di istruzioni è variabile, che può variare da 1 fino a 4 byte, esempio l'80x86, servono un quantità ragionevole di Byte. Posso supportare un numero diverso di operandi, l'istruzione è di lunghezza variabile, che vanno da 1 a 2 byte fino a 4 byte, le **performance si diminuiscono** (perché ho bisogno di più colpi di clock per eseguire le stesse istruzioni), e si riducono anche perché bisogna capire la dimensione dell'istruzione dato che è di lunghezza variabile e per capire quanto è lungha l'istruzione difficile. 

La dimensione del **codice è minima** perché avrò meno istruzioni, dato che le istruzioni sono molto compatte
### Decodifica Fissa
![[Screenshot 2026-09-29 at 08.39.58.png]]
Qui si semplifica la decodifica dell'istruzione, cioè si fissano la dimensione di ogni istruzione. Esempio di processori sono il MIPS, [[RISC|RISC]], ARM. 

Ho un numero fisso di operandi 3 destinazione, operandi e sorgenti, l'istruzione definisce anche il modo di indirizzamento. La dimensione dell'istruzione è fissa 32 bit. Migliore prestazione perché sto facilitando il modo in cui il processore decodifica l'istruzione dato che tale istruzione segue uno standard di 4 byte. La dimensione del codice è più grande perché avrò tante istruzioni semplici che rendono complesso il codice creando hover-head.
### Decodifica Ibrida
![[Screenshot 2026-09-29 at 08.43.39.png]]
Sarà l'ARM Thumb2  con cui andiamo a lavorare con le istruzioni variabili.

Ci sono formati differenti che sono specificati nell'*opcode* e tramite questa decodifica si possono fare compromessi tra la dimensione del codice e le performance.

## Problemi Sull Instruction Set
Dobbiamo tener conto della dimensione del codice che andremmo a lavorare sopra, la dimensione delle istruzioni devono essere di una giusta dimensione.

Modifica e complica la fase di fetch e decoding nell'hardware
# Reference
---

