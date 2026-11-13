---
created: 2026-02-14T15:43:00
tags:
  - baby
topics:
author: Danilo Quattrini
---
# Accessing Memory
---
## Memory Map
Il processore vede gli elementi di memoria e le periferiche collegate al sistema completo.![[IMG-Accessing Memory-20261110.png]]

La parte del `Code` non sarà sempre 0.5Gb perché dipende fortemente dal micro-controllore che si prende. Nel programma si può anche cambiare la dimensione della memoria 
## Memory Access Attributes
Ci sono diverse regioni della memoria, che si possono accedere in diversi modo o salvare in alcune locazioni specifiche, come il buffer o la cache
![[IMG-Accessing Memory-20261110-1.png]]

## Load and Store Pseudo Instruction
Per accedere alla memoria, dobbiamo utilizzare operazioni *load-store*![[IMG-Accessing Memory-20261110-2.png]]

- `LDR` e `STR`: legge o scrive in memoria una parola a 32 bit
- `LDRB` e `STRB`: legge o scrive in memoria una parola di 8 bit meno significativi (LSB)
- `LDRSB`: legge parole che sono con il segno a 8 bit 
- `LDRSH`: legge parole che sono con il segno a 16 bit 
- `LDRD` e `STRD`: legge due word 64bit di parole
- `LDM` e `STM`:  legge parole multiple

### Commands Examples
Se prendiamo `r0=0x00008004`
![[IMG-Accessing Memory-20261110-3.png]]

```
r1= 0x796C628D
r2= 0x0000008D
r3= 0x0000628D
r4 = 0xFFFFFF8D
r5 = 0x0000628D
```

Se invece usassimo l'operazione con due registri `LDRD`, con `r0 = 0x00008000` avremmo la necessità di due registri in modo da poter rappresentare i 64 bit che sono necessari.
```
LDRD <Rd1>, <Rd2>,<addressing_mode>
```

![[IMG-Accessing Memory-20261110-4.png]]

## Addressing Mode
ARM possiede diversi modi di indirizzamento, che sono:
- **Pre-index, prima della lettura o scrittura**:
	- **con writeback**: **non salvo** il valore del registro
	- **senza writeback**: salvo il valore del registro
	  Utile per gestire dei valori che sono salvati dentro ad un vettore.
- **Post-Index dopo la lettura e scrittura**
  
- Offset

### Pre-index addressing
```
load / store <Rd>, [<Rn>, <offset>]{!}
```

Se c'è il `!` punto esclamativo allora si cambia il valore del registro `Rn`, altrimenti no.

>[!example]
>Prendiamo il valore di `r0 = 0x00008000`  e volessimo leggere 4 valori nella memoria e salvarli nei registri `r2-r5` allora possiamo utilizzare l'offset che ci aiuta a muoverci in memoria, senza dover modificare il valore di `r0`, questo perché non mettiamo il punto esclamativo `!`:
>```
>LDR r2, [r0]
>LDR r3, [r0, #4]
>LDR r4, [r0, #8]
>LDR r5, [r0, #12]
>```
>Alla fine avremmo che `r0` sarà `0x00008000`, se avessimo messo il punto esclamativo, `r0` sarebbe stato invece `0x0000800C`
>
>Inoltre è possibile utilizzare i registri come offset, invece di utilizzare le costanti:
>```
>LDR r2, [r0]
>MOV r1, #4
>LDR r3, [r0, r1]
>MOV r1, #8
>LDR r4, [r0, r1]
>MOV r1, #12
>LDR r5, [r0, r1]
>```

### Post-Index
```
load / store <Rd>, [<Rn>], <offset>
```

Nel post-index il registro `Rn`, **viene sempre aggiornato**, senza dover inserire il punto esclamativo `!`