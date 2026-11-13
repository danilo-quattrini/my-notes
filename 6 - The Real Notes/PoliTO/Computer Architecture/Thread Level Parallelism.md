---
created: 2026-10-30
tags:
  - baby
topics:
  - Architecture 
author: Danilo Quattrini
---
# Thread Level Parallelism
---
## Introduzione
Si cerca di far girare in parallelo istruzioni in parallelo tra di loro, tramite l'utilizzo del **Thread-Level Parellelism**, questo grazie alla quantità delle unità funzionali.

## Che cos'è un Thread
Il **Thread** è un processo separato che possiede le proprie istruzioni e dei dati. Ci sono elementi separati che non condividono risorse tra di loro. 

Ci sono diversi utilizzi del Thread Level Parallelism, dove ci sono anche programmi che usano livelli di parallelismo molto alto.

## Multithreading
L'idea è quello di mettere l'ILP e il TLP, per sfruttare al massimo un processore superscalare, in modo che le istruzioni vengono da diversi thread. Grazie al multithreading è possibile condividere le unità funzionali di un singolo processore.

Per implementare tale strategia, dobbiamo avere un sistema privato dove salviamo le informazioni, dove abbiamo:
- Un accesso indipendente alla memoria
- Un accesso indipendente alla storage
- Il processore deve poter fare un context switch tra un thread ad un altro.

### Tipologie

Ci sono diverse tipologie di multithreading:
#### Fine-grained multithreading
Ad ogni colpo di clock si fa un context switch

### Coarse-grained Multithreading

### Simultaneous Multithreading
