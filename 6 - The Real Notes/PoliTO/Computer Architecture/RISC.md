---
created: 2026-09-29
tags:
  - baby
topics:
  - Architecture 
  - "[[School]]"
author: Danilo Quattrini
---
# RISC
---
The term RISC-V (where V stands for variations and vectors) that stands for (Reduced Instruction Set Computer) is a [computer architecture](https://en.wikipedia.org/wiki/Computer_architecture "Computer architecture") designed to simplify the individual instructions given to the computer to accomplish tasks.

>[!info] 
>RISC-V computer might require more machine code in order to accomplish a task because the individual instructions perform simpler operations. Ci sono tre versioni di istruzioni tra il 32, 64, 128 bit.

E' uno standard che definisce le [[Instruction Set Architecture|ISA]], è interessante il fatto che il RISC ha degli standard open source che può essere utilizzato da ogni sviluppatore.

## Generalità 
Il RISC-V è un'architettura a licenza gratuita per l'utilizzo universitario, è un architettura *load-store* **cioè le uniche istruzioni che possono accedere alla memoria sono load e store**, dove non si possono svolgere altre operazioni se non solo ***load e store***. [[Instruction Set Architecture|ISA]]  a 32bit (cioè ogni istruzione è grande 32bit) che però posso arrivare anche a 16 bit. L'architettura mi permette di creare una serie di estensioni per esempio l'utilizzo dell'architettura in ambito di sicurezza, operazioni su numeri in virgola mobile e operazioni vettoriali.

I modi che andremmo in questa architettura saranno:
- [[Instruction Set Architecture#Displacement|Displacement]]
- [[Instruction Set Architecture#Immediate Mode|Immediate Mode]]
- [[Instruction Set Architecture#Register Mode|Register Mode]]

### Tipi di dato
I tipi dei dati sono i seguenti:
-  **Byte (8 bits)**
-  **Half Words (16 bits)**
- **Words (32 bits)**
- **Double Words (64 bits)**
- **32-bit single precision floating-point**
- **64-bit double precision floating-point.**

### Two's complement
Dato un numero binario $A$ di $N$ bit, il complemento a due (2C) può essere definito come:
$$A = 2^{N}-A = \overline{A} + 1$$
Cioè nega il numero che vogliamo renderlo negativo ed aggiungere $1$![[Screenshot 2026-09-29 at 09.18.30.png]]
Il problema che avremmo con un complemento a due, sarà l'**overflow**, perché se faccio operazioni con lo stesso segno posso rischiare di rappresentare risultati differenti. Tutte le operazioni se non specificate vengono svolte in complemento a due

| Binary | Decimal |
| ------ | ------- |
| 000    | 0       |
| 001    | 1       |
| 010    | 2       |
| 011    | 3       |
| 100    | -4      |
| 101    | -3      |
| 110    | -2      |
| 111    | -1      |

## Rappresentazione del numero nel formate IEEE 754 32-bit
![[Screenshot 2026-09-29 at 09.23.01.png]]
IL NUMERO NON E' 10 COME SULL'IMMAGINE, MA E' 2
Il numero rappresentato in binario seguendo il formato IEEE 754 è rappresentato in formato e diviso nelle seguenti parti:
- **Sign**: il segno occupa solo 1 bit del numero che va da 0 se è positivo 1 se è negativo.
- **Esponente**: occupa solo 8 bit, che è un numero che si deve sottrare alla rappresentazione binaria di 127
- **Mantissa**: occupa a 23bit che rappresenta il valore in binario dopo del valore della virgola 1,\[Mantissa\], come nell'immagine che vediamo i numeri con il colore verde è la mantissa

Per vedere come funziona su RISC-V vedere [qui](https://deepwiki.com/riscv/riscv-isa-manual/3.1.3-f-and-d-extensions-(floating-point))
## Lunghezza dell'istruzione nel RISC-V
Si possono utilizzare diversi tipo di decodifica, che possono essere in blocchi a 16 bit e va in base all'implementazione necessario. La versione base è a 32 bit che hanno i bit meno significative impostate ad 11. L'allineamento può essere rilassato (relaxed). supporta l'assegnamento in memoria in [[Instruction Set Architecture#Little Endian|Little Endian]]

## Organizzazione delle Istruzioni
![[Screenshot 2026-09-29 at 09.38.52.png]]
Il processore che andremmo ad utilizzare sarà RV32G

## Registri
Ci sono due banchi di registri (bank register), i registri avranno 32 o 64 bit di informazione e si dividono in registri interi con la `x`, mentre i registri in virgola mobile sono con il simbolo `f`, il **registro x0 sarà sempre a zero**  ![[Screenshot 2026-09-29 at 09.42.13.png]]
I floating point register, hanno la rappresentazione che abbiamo visto nello standard precedente [[#Rappresentazione del numero nel formate IEEE 754 32-bit|IEEE 754 32-bit]], nella versione con i registri a 32 avremmo la possibilità di utilizzare registri per interi e float.
![[Screenshot 2026-09-29 at 09.45.06.png]]

| **Register Group**      | **Names**              | **ABI Rule & Usage**                                                                                                                                                                                                                         |
| ----------------------- | ---------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Zero Register**       | `x0` / `zero`          | Always hardwired to `0`. Writes to it are ignored. Use `zero` instead of wasting a register like `s0 = 0`!                                                                                                                                   |
| **Temporary Registers** | `t0` – `t6`            | **Caller-saved / Scratchpad.** Used for temporary values and intermediate calculations. Functions can freely overwrite them without restoring their original values.                                                                         |
| **Saved Registers**     | `s0` – `s11`           | **Callee-saved.** Used for long-term variables that must persist across function calls. **Rule:** If you write a function/procedure that modifies an `s` register, you MUST save its old value to the Stack and restore it before returning. |
| **Argument Registers**  | `a0` – `a7`            | Used to pass arguments into functions and return results (`a0`-`a1`). Also used for `ecall` system calls.                                                                                                                                    |
| **Special Registers**   | `sp`, `ra`, `gp`, `tp` | Reserved for Stack Pointer, Return Address, Global Pointer, and Thread Pointer. **Never use these for general arithmetic/loops.**                                                                                                            |
Ci sono degli alias dei registri che raccontano la loro funzionalità. Tali alias seguono lo standard **ABI** che sta per **Application Binary Interface**
## Modi di indirizzamento RISC-V
Uno è quello [[Instruction Set Architecture#Immediate Mode|immediato]], somma con valori immediati, esempio 
```
addi x1, x2, 32 <- x1 = x2 + 32
```
Cambia se utilizzo un registro `x0` perché in questo caso il registro `x0` è sempre 0 quindi è come un'assegnamento
```
addi x1, x0, 32 <- x1 = 32
```

Un'altro sarà quello [[Instruction Set Architecture#Displacement|displacement]]
```
lw x1, 30(x2) <- load word
```
![[Screenshot 2026-09-29 at 10.10.35.png]]
Ma se utilizzo invece del valore immediato > `0`, utilizzassi `0` sarà un [[Instruction Set Architecture|displacement indiretto]]
![[Screenshot 2026-09-29 at 10.11.35.png]]

## Formato dell'istruzione
Istruzione a 32 bit che è composto da 7-bit per l'[[Control Unit (CU)#^eb351c|opcode]] e 12 bit per il piazzamento degli indirizzi, esempio immediato o PC relativi

### Registri (R-Type Instruction)
![[Screenshot 2026-09-29 at 10.13.59.png]]

### Immediate
Possiede il valore immediato che ha 12 bit riservati sull'istruzione![[Screenshot 2026-09-29 at 10.15.02.png]]

### Store![[Screenshot 2026-09-29 at 10.16.06.png]]

### Jump
![[Screenshot 2026-09-29 at 10.16.52.png]]

## Tipi di istruzioni nel RISC-V

### Load & Store
Usato per scrivere e salvare valori in memoria.
>[!quote]
>`lw -> load word` 
>Load a word (Caricare un dato)
>```
>lw x2, 28(x8) # x2 <- MEME[x8 + 28]
>```

>[!quote] Load in Register a Signed Byte
>```
>lb x1, 28(x8) # x1 <- ([MEM[x8 + 28]])
>```
>leggero il byte della posizione in memoria di x8, x1 rappresenta lo stesso valore, estende l'ultimo bite a tutti i bit.

>[!quote] Load in Register unsigned
>```
>lbu x1, 28(x8) # x1 <- 0^24 ## MEM[x8 + 28]
>```
>Deve prendere il byte e non estendere a nulla 

>[!quote] Load a word variable named VAR in a register
>```
>lw x2, VAR # lw is a pseduoinstrucion in this case
>```
>Che viene tradotto in questo caso
>```
>auipc x2, 0x10000 # auipc -> add uperr immediate to pc (program counter)
>lw x2, 0(x2)    # x2 <- PC + 0x10000000, VAR effective address
>```

>[!quote] Load Absolute Address in a Register
>```
>la x5, VECT #la is a psedoinstruction
>```
>Tradotto anche come 
>```
>auipc x5, 0x10000 # x5 <- PC + 0x10000000
>addi x5, x5, -23 # x5 <- x5 – 23 (effective address of VECT)
>```

![[Screenshot 2026-09-29 at 10.30.31.png]]

## ALU Operations
![[Screenshot 2026-09-29 at 10.32.22.png]]
### Shift and slt operation
![[Screenshot 2026-09-29 at 10.32.43.png]]
![[Screenshot 2026-09-29 at 10.32.57.png]]
### Other example
Aggiungere i bit nella parte più altra della memoria
![[Screenshot 2026-09-29 at 10.34.28.png]]

## Istruzioni di salto
![[Screenshot 2026-09-29 at 10.36.31.png]]

`jal` che significa `jump and link`, cioè salta e salve il registro da dove è partito il salto (cioè l'indirizzo di ritorno, solitamente può essere il registro x1 che il registro dove l'operazione `jal` salva il registro dove ritornare quando svolge il jump)
![[Screenshot 2026-09-29 at 10.38.42.png]]
altre istruzioni sulle slide dalla 36 alla 38.

## Branch Instruction
Le branch sono un salto all'"etichetta" (label) se la condizione è vera
Sono del formato **B-Type**![[Screenshot 2026-09-29 at 10.44.28.png]]
l'ultimo bit meno significativo non lo considero, l'offset deve essere un multiplo di due, ogni salto **CONFRONTANO SEMPRE DUE REGISTRI**![[Screenshot 2026-09-29 at 10.46.55.png]]
il primo `beqz` (branch equal zero) confronta se x3 è uguale a zero
il secondo `bnez` (branch not equal zero)  confronta se x3 è uguale a zero
![[Screenshot 2026-09-29 at 10.48.11.png]]
il primo `bltz` (branch less than zero) confronta se x3 è < zero
il secondo `bgtz` (branch greater than zero)  confronta se x3 è > a zero

## ISA per il RV64G
![[Screenshot 2026-09-29 at 10.50.42.png]]

>[!info] Nop Instruction
>Nop (No Operation Instruction) operazione che consuma tempo e non fa niente, in RISC-V è il seguente.
>```
>addi x0, x0, 0 #nop
>```

^504f4e

## Somma dei valori di un array
```arm-asm
.data
numeri:   .word 7, -2, 10, 4, 1
risultato: .word 0

.text
.globl main

main:
    la   x5, numeri       # x5 = indirizzo del primo elemento
    li   x6, 5            # x6 = quanti elementi restano da leggere
    li   x7, 0            # x7 = somma parziale = 0

ciclo:
    beq  x6, x0, fine     # se non restano elementi, esci dal ciclo

    lw   x8, 0(x5)        # x8 = MEM[x5 + 0]: carica un word
    add  x7, x7, x8       # x7 = x7 + x8
    addi x5, x5, 4        # passa al word seguente: 4 byte dopo
    addi x6, x6, -1       # decrementa il contatore
    j    ciclo            # torna a controllare la condizione

fine:
    la   x9, risultato    # x9 = indirizzo della variabile risultato
    sw   x7, 0(x9)        # MEM[x9 + 0] = x7

stop:
    j    stop             # evita di continuare in memoria non valida
```
- `x5` è il registro che contiene l'indirizzo di memoria del vettore numeri e lo incrementiamo di più 4 bite con l'operazione `addi`, per spostarci all'indirizzo di memoria successivo.
- `x6` utilizziamo un registro per contare gli elementi presenti nel vettore `numeri`, dandogli come valore la dimensione del vettore, che in questo case è 5 numeri
- `x7` registro che utilizziamo per salvare i risultati intermedi dell'operazione di somma


# Reference
---

