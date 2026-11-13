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
# ARM Architettura
---
Sono divise in tre fasi, con fetch, decode ed execute, con la seguente data-path
![[IMG-ARM Architettura-20261103.png]]
Il program counter (PC), sarà uno dei registri, dove però ogni componente sarà collegato tramite diversi [[Data Bus|BUS]], in fase di execute si dovranno utilizzare più colpi di clock in base ai registri. 

Banco di registri che sono 16, dove uno di questi registri è il PC che è il numero `r15`, dove `r0` non è zero come succedeva nel RISC-V, il processore è sempre di tipo *load-store* come prima.

## Istruzioni registro-registro
Chi viene coinvolto nell'operazione sarà sempre due registri, dove si prendono due registri per l'operazione e salvo il risultato in un altro registro, questo è lo stesso funzionamento del processore RISC-V che abbiamo discusso prima.
![[IMG-ARM Architettura-20261103-1.png]]

## Istruzioni Registro-Immediato
## Trasferimento dei dati in Memoria
Le istruzioni di trasferimento dati richiedono due cicli di esecuzione nello stage di esecuzione. Nel primo viene calcolato l’indirizzo utilizzando un registro e un immediato, mentre nel secondo avviene un accesso in memoria nel quale viene trascritto il dato.

## Istruzione di Salto (Branch)
Qui c'è la necessità di svolgere un colpo di clock aggiuntivo per salvare l'indirizzo di ritorno del branch in `r14` (link register)