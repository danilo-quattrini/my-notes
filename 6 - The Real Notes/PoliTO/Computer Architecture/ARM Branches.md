---
created: 2026-02-14T15:43:00
tags:
  - baby
topics:
author: Danilo Quattrini
---
# ARM Branches
---
## Unconditional Branch
Ci sono 4 salti di tipo incondizionali e sono:
- `B <label>`: 
- `BX <Rn>`: salti indiretti
- `BL <label>`: salto e salvo il valore di ritorno nel `r14 (LR)` link register
- `BLX <Rn>`: salto indiretto con il link sempre verso il `r14 (LR)`

Eseguendo un codice Thumb 2 il valore del registro di link, avrà il LSB ad 1, viene fatto in modo automatico dal compilatore. 

Per fermare l'evoluzione del programma si dovrà saltare nello stesso punto, come qui:
```
stop B stop
```

oppure si può utilizzare
```
	LDR r1, =stop
stop BX r1
```

## MOV for unconditional branch
L'operazione di `B` e `BX`, vanno a cambiare il valore del `PC`, che però non è consigliata è meglio utilizzare il `BX`:
```
LDR <Rd>, =<label>
MOV PC, <Rd>
LDR PC, =<label>
```

## Tabelle delle Condizioni
![[IMG-ARM Branches-20261110.png]]