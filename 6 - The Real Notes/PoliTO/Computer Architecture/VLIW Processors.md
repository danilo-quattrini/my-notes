---
created: 2026-10-30
tags:
  - baby
topics:
  - Architecture 
author: Danilo Quattrini
---
# VLIW Processors
---
## Introduzione
Fino ad ora abbiamo cercato di migliorare le prestazioni dei nostri dispositivi, migliorando le caratteristiche del processore. Con i *Very Long Instruction Word* (**VLIW**), i processori per arrivare a migliorare le prestazioni, possiedono delle lunghe operazioni di decodifica.

## Caratteristiche
**Software è molto più complesso**: questo perché sarà il compilatore gestirà tutte le dipendenza, gestire il parallelismo e un unrolling aggressivo nella fase di  decodifica.

**Hardware molto più semplice**: perché non si deve occupare di controllare le dipendenza, queste perché le ha gestite il compilatore.
## Gli Stalli?
Non ci dovrebbero essere stalli, perché sarà il compilatore gestirà tutto, in alcuni casi però ci saranno un minimo di stalli dovuti al dato mancante in memoria cache.
## Example
Ci sono tante unità funzionali (intere, numeri reali, salti e accesso alla memori *load & store*), prendiamo come esempio il processore che per ogni clock cycle abbia:

- due operazioni di floating point
- due accessi alla memoria
- un'operazione di interi o di branch

Abbiamo una porzione di codice:
```asm
loop:
	fld f0, 0(x1)
	fadd.d f4, f0, f2
	fsd f4, 0(x1)
	addi x1, x1, -8
	bne x1, x2, loop
```

L'idea è prendere questo loop, svolgere l'operazione di *unrolling*
![[IMG-20261030085841894.png]]

 Il codice contiene ben 7 iterazioni che vengono eseguite in 9 clock cycle, con 1.29 cicli per vettore, dove vengono eseguite 2.5 operazioni per clock cycle.
 
 Se notiamo però ci sono degli slot liberi, che sono quasi 50% delle operazioni, che sono semplicemente delle `nop`. Inoltre abbiamo bisogno di `15` registri, in confronto ad un processore superscalare che ne usano solitamente solo `3` o `6`
 
### Dimensione dell'istruzione
Passiamo da 64 a 120 bit

>[!done] Vantaggi
>Semplifichiamo l'hardware evitando di chiedere all'hardware di fare il controllo delle dipendeze

>[!bug]
>Ci sono però diverse problematiche:
>- Ci sono delle limitazioni che sono ereditate dall'[[Instruction Level Parallelism (ILP)|ILP]]
>- Non è semplice creare questo hardware, questo perché devono lavorare in modo sincorono

### Limitazioni ereditate dall'ILP
Qui rimane difficile trovare istruzioni che possano eseguire in parallelo.

Per trovare istruzioni indipendenti possiamo 

## Costi Hardware
Aumenta l'accesso alla memoria, complicando l'hardware intorno al processore

## Memory Access
La memoria può diventare un collo di bottiglia, questo perché è richiesta una banda molto elevate e ci sono molti stalli dovuti ai miss causati dalla mancanza dei dati nella cache

### Soluzioni Per l'accesso alla memoria
Le soluzioni possono essere le seguenti:
- memory interleaving
- multiport memories
- multiple access per clock cycle memories

## Dimensione del Codice
Aumenta la dimensione del codice, questo perché stiamo svolgendo operazioni di *unrolling* all'interno di un loop. Ci sono anche i buchi di istruzioni, perché non riusciamo a mettere istruzioni utili negli slot che si creano a causa dall'*unrolling*

## Binary Code Compability
Ogni cambiamento all'interno del processore VLIW richiede di ri-compilare nuovamente tutto il codice