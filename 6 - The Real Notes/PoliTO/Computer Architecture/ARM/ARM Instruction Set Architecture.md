---
created: 2026-11-03
tags:
  - baby
topics:
  - ARM
  - Architecture 
  - Microprocessors
author: Danilo Quattrini
---
# ARM Instruction Set Architecture
---

## `r15` Program Counter
E' un registro che usiamo per il [[CPU Components#PC (Program Counter)|Program Counter]], lunghezza di 32 bit, che devono essere allineate Quando il processore è eseguito in ARM state tutte le istruzioni sono lunghe 32 bit e sono allineate a word. Per questo motivo, il PC value è salvato nei bit \[`31:2`\] con i bit \[`1:0`\] pari a 0.
## `r14` Link Register
Registro usato per il ritorno di una branch o di una jump per ritornare ad una specifica posizione / istruzione
![[IMG-ARM Instruction Set Architecture-20261103-1.png]]
## `r13` Stack Pointer
![[IMG-ARM Instruction Set Architecture-20261103.png]]

Gli indirizzi di questi elementi sono salvati correttamente dal sistema che andiamo ad utilizzare. Questo registro viene aggiornato in modo automatico al boot che viene recuperato nell'Interrupt Vector Table

## System Register
**BASEPRI**: considerato come il Base Priority Mask register
PRIMASK: Primary Mask... 
FAULTMASK: 
CONTROL: 

### CONTROL Register

## Il Conditional Field
![[IMG-ARM Instruction Set Architecture-20261103-2.png]]

Che ritornano dei flag in base al risultato della condizione, dove i 4 bit della **parte alta del registro delle condizione**, che può assumere ben $2^{4}= 16$ stati differenti che sono i seguenti che vediamo in figura sotto:
![[IMG-ARM Instruction Set Architecture-20261103-3.png]]

>[!example] Esempio
>Per eseguire / attivare una condizione, si può fare in questo modo:
>```asm
ADDEQ r0, r1, r2 ; If zero flag is set then perform r0 = r1 + r2```

Per le operazioni che vanno ad interagire con i dati non vanno ad attivare la *condition flags*.