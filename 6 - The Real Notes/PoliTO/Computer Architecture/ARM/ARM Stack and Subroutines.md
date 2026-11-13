---
created: 2026-02-14T15:43:00
tags:
  - baby
topics:
author: Danilo Quattrini
---
# ARM Stack and Subroutines
---
# Stack
Lo stack  è una coda che funziona in ordine **LIFO** (Last In First Out), dove i dati sono letti (read) utilizzando il **POP**, e scritti (write) all'interno dello stack tramite l'operazione di **PUSH**.

>[!info] Funzionamento
Lo SP (Stack Point), che viene rappresentato in ARM dal registro `R13`, viene sempre decrementato ogni volta si va ad inserire un elemento al suo intero, incrementa invece se leggiamo un elemento dallo stack.

![[IMG-ARM Stack and Subroutines-20261113.png]]

## Tipi di Stack
Ci sono due tipi di stack, che dipendono dal muovimento dello sp, quando facciamo un operazione, e se lo SP punta ad un elemento valido oppure no.

- *descending stack*: per ogni operazione di push, lo **stack pointer diminuisce**

- *ascending stack*: per ogni operazione di push, lo **stack pointer incrementa**

Si può classificare anche in base all'elemento che sta puntando nello stack.
- **empty stack**: punta ad una posizione di memoria vuota.
  
- **full stack**: punta ad un elemento valido, cioè che esiste un valore.

## Esempio di 3 Operazioni Push
![[IMG-ARM Stack and Subroutines-20261113-1.png]]
Si legge dal basso verso l'alto, cioè l'elemento che dovrà essere preso in caso si svolge un operazione di POP si prenderà dal basso.

## Esempio di POP
![[IMG-ARM Stack and Subroutines-20261113-2.png]]

- **empty ascending**: cioè vado ad incrementare quando leggo e incrementare per scrivere, però in questo caso il dato che vogliamo leggere non è present

- **full ascending**

## LDM & STM
Posso leggere e scrivere multipli registri in memoria.
```
LDM{xx}/STM{xx} <Rn>{!}, <regList>
```
- `{xxx}`: condizione da applicare all'istruzione (`EQ`, `LT`, `GT`)
  
- `Rn`: sarebbe il registro che vogliamo 
  
- `!`: cambia `Rn` alla fine della lettura
  
- `<regList>`: lista dei registri da salvare nello stack

L'insieme dei registri che si possono salvare in diversi modi:

- {`r0-r4`}: salvo dal registro `r0` fino al registro `r4`, è come scrivere `{r0,r1,r2,r3,r4}`.

- {`r1,r2,r3`}: si salva la lista dei registri che si vuole caricare nello stack.

>[!warning] N.B
>Non si può salvare lo **SP** (`r13`) nello **stack**

>[!info] IL `PC`?
Inoltre si può anche salvare il `PC` che però **non si può salvare insieme al** `LP` (Link Register).

## Addressing Modes
Ci sono due modalità di modalità di indirizzamento:
- `IA` *Increment After*:  Incrementa dopo che il valore è stato scritto nello stack, dove il processore si accede alla memoria e poi incrementa o decrementa lo SP

- `DB` *Decrement Before*: decremento prima e poi si legge o scrive il valore nello stack.

>[!example] LDMAI
>Leggo il valore dallo stack poi dopo si incrementa la locazione di memoria
![[IMG-ARM Stack and Subroutines-20261113-3.png]]

Ci sono diverse modalità di accesso e lettura dello stack, che abbiamo visto prima, che si può rappresentare in questa tabella.
![[IMG-ARM Stack and Subroutines-20261113-4.png]]

## `PUSH` & `POP`
Si usano semplicemente `PUSH` e `POP`, quindi non è necessario quello che abbiamo prima detto, quindi sarà:
```
PUSH {<regList>}
```
Per la push, mentre per la `POP`
```
POP {<regList>}
```

# Subrutines
Una sottorutine (*sub-rutines*) è una funzione che possiamo richiamare per eseguire delle operazioni separate dal flow principale del programma, questo è possibile tramite l'utilizzo del:
```
BL <label>
```

Oppure si può utilizzare:
```
BLX <Rn>
```
`B`ranch `L`ink and E`X`change, dove scrive il valore del `PC` nel registro `Rn`, però solitamente il registro di ritorno è salvata nel `LR`

## Richiamare una SubRutine
![[IMG-ARM Stack and Subroutines-20261113-5.png]]


![[IMG-ARM Stack and Subroutines-20261113-6.png]]
Se una sotto-rutine, chiama un altra sotto-rutine, bisogna stare attenti che la seconda sub-rutine quando deve uscire punterà alla sub-rutine1

## Passing Values and Result
Ci sono 3 approcci per poter passare i parametri ad una sub-rutine:
1. Tramite i registri.
2. Utilizzando le reference dei registri nella memoria
3. Oppure tramite lo stack.

## Esempio di SubRutine
```asm
MOV r0, #0x34
MOV r1, #0xA3
BL sub1
; r2 contains the result
```

si scrive una sub-rutine in questo modo:
```
sub1 PROC
	PUSH {LR}
	CMP r0, r1
	SUBHS r2, r0, r1
	SUBLO r2, r1, r0
	POP {PC}
	ENDP
```

Si possiedono sempre salti di tipo `THUMB-2`, questo vuol dire che se il programma prima di saltare alla sub-rutine, ha un `PC` di valore `DC`, che quando salterà sarà `DD`, questo perché il bit LSB (Less-Significant-Bit) sarà ad `1` in `THUMB-2`
