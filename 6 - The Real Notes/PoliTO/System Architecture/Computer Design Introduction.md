---
created: 2026-09-22
tags:
  - baby
topics:
author: Danilo Quattrini
---
# Computer Design Introduction
---
Il calcolatore di oggi ha una capacità gigantesca per quando riguarda la sua evoluzione nel tempo, questo perché ci sono stati degli sviluppi sulla tecnologia dei semiconduttori e degli sviluppi nel [[Computer Architecture#Computer Organization|computer design]].

Siamo passati da una quantità di transistor negli anni '70 di ben $2000$ di numero, fino a più di $10^{9}$ milioni di transistor, utilizzati oggi per sistemi per Intelligenza Artificiale.
![[Screenshot 2026-09-22 at 10.10.44.png]]

Oggi la quantità di dati sta crescendo in modo esponenzialmente, ci sono dispositivi che vanno a generare dati ed informazione ogni secondo,  fino ad arrivare alla quantità di $10^{21}$ zettaByte (ZB) di data.

Lo sviluppo dei processori hanno comportato ad un miglioramento dei dispositivi che utilizziamo oggi giorno, nel periodo dagli anni 78 fino all'86 non c'è stato un grande sviluppo tecnologico. Però con l'arrivo dei MIPS, delle architetture RISC e dei processori ARM hanno portato a sistemi che possono computare più istruzioni al secondo.
![[Screenshot 2026-09-22 at 10.21.14.png]]

Vediamo la differenza che negli anni 78 si eseguivano ben 1 milioni di istruzioni al secondo fino ad arrivare ad eseguire ben più di 11 milioni di istruzioni al secondo nel periodo del 2004. Però nel periodo dopo il 2004 c'è stata una saturazione delle prestazioni del calcolatore perché non si riusciva più a creare un calcolatore più potente, ma è stato introdotto il concetto del parallelismo (cioè eseguire più operazioni in parallelo). 

Oltre al parallelismo è stato introdotto il concetto di architetture a microprocessori, dove esistono istruzioni semplici e facili da comprendere, ma si necessitano di più istruzioni alla volta per eseguire operazioni complesse.

## Microprocessor Performance
![[Screenshot 2026-09-22 at 10.26.49.png]]
L'immagine sopra fa vedere un'esempio della struttura architetturale di un processore 8086, che eseguivano istruzioni in modo sequenziale.
![[Screenshot 2026-09-22 at 10.27.14.png]]
Il processore fa come vuole, non si eseguono istruzioni sempre in sequenziale, ed è stato l'elemento chiave dei processori che hanno portato allo sviluppo di quest'ultimi. 

## Mercato dei computer
I dispositivi che si vanno ad utilizzare ed acquistare dipendono principalmente dalle necessità che l'utente ha bisogno. Nel mercato di oggi si tende ad utilizzare i **microprocessori**, cioè processori che vanno a gestire più processi allo stesso tempo. Cioè singoli chip che però gestiscono più processi al secondo.
![[Screenshot 2026-09-22 at 10.35.55.png]]

### Personal Mobile Device (PMD)
In quest'area ci sono telefono, tablet che devono reagire in modo prontato alle esigenze dell'utente.
### Desktop Computer 
In quest'area ci sono Computer e PC Workstation, il target è ottimizzare le performance e il prezzo.
### Server 
Qui il sistema deve eseguire tutti gli esperimenti che vogliamo eseguire su reti neurali o altre necessità che dobbiamo soddisfare, questi sistemi devono essere affidabili, sicuri e veloci.
### Cluster / Warehouse-Scale (WAS)
I [^1]cluster danno importanza alla disponibilità al prezzo e al consumo di energia, perché tali sistemi consumano tanta energia, molti di questi cluster infatti vengono creati in paesi molto freddi per ridurre il consumo energetico.
![[Screenshot 2026-09-22 at 10.43.30.png]]
I cluster vengono costruiti con una serie di processori e una serie di acceleratori, che sono sistemi multicore (4 o 16 core), avvolte possono esserci degl'acceleratori, che permettono di fare operazioni velocemente.

I nodi vengono collegati tra di loro da un Global Interconnection Network.

### Embedded System
I dispositivi sono economici, cioè il costo del sistema è molto alto ma il processore può costare tra $0.01 a $100, anche le pennette USB sono considerati come sistemi embedded system. I target dei computer embedded sono:
- Risposte in real-time
- minimizzare la memoria
- ridurre il consumo di energia
Questi sistemi possono essere di tue tipologie:
- Processore Standard 

## Classi di Parallelismo
Parallelizzare le operazioni da svolgere sui dati e le task da completare, questi sono definiti in tutti i dispositivi che si sono citati precedentemente e sono di due macro-famiglie e variano in base all'applicazione che ne viene fatta:

**DLP** (Data-level Parallelism):  eseguire il parallelismo sui dati di diverso tipo, cioè eseguire la stessa operazione su dati di diversa natura. ^07e7ee
>[!example]
>Hai un vettore di 1000 numeri e devi fare `y[i] = a * x[i] + b` per tutti gli `i`.  
Ogni elemento del vettore è indipendente dagli altri → puoi elaborare molti dati **contemporaneamente**

**TLP** (Task-Level Parallelism), ogni task lavora in modo indipendente e parallelo.
>[!example]
>un server web che gestisce richieste HTTP diverse, o un gioco che ha:
>- un thread per la fisica
>- un thread per il rendering
>- un thread per l’audio
>
Ogni “task” può andare avanti da solo, senza dover aspettare gli altri (o quasi).
Caratteristica chiave: **lavori diversi, potenzialmente indipendenti**.

Ci sono ben quattro modi in cui l'hardware del computer gestisce tale parallelismo e sono i seguenti:
1. **Instruction-Level Parallelism**: L’hardware (con aiuto del compilatore) cerca di eseguire **più istruzioni contemporaneamente** su uno stesso flusso di esecuzione. Questa tipologia di parallelismo utilizza il **DLP**, con tante operazioni simili su dati vicini (es. operazioni in un ciclo)
2. **Vector Architectures e GPU**: qui il parallelismo esiste al livello di istruzione, cioè viene eseguita un'unica operazione su un'insieme di dati. Le GPU sono l’esempio più estremo: migliaia di core che applicano la stessa istruzione a grandi collezioni di dati.
3. **Thread-Level Parallelism** (TLP): qui il parallelismo avviene sia nell'ambito del **DLP** che nel **TLP**, dove vari thread condividono la stessa memoria, cache e spesso la stessa socket per dividere il lavoro che devono svolgere.
>[!example]
>Esempio se devono svolgere un'operazione su un'array, i thread possono dividersi porzioni di array fra di loro (DLP), oppure possono eseguire task diverse come per esempio un'operazione per il calcolo ed un'altra per interagire con le periferiche (TLP) Questo è il classico modello **multicore / multiprocessore** che vedi nei PC, server, smartphone moderni.
4. **Request-Level Parallelism (RLP)**: Sono varie task che sono separate tra di loro e che non sono collegate in nessun modo, cioè ogni macchina esegue una semplice task.

I concetti che si sono visti si possono categorizzare in questo modo

| Parallelismo nell’applicazione  | Come lo sfrutta l’hardware                                                                                                                           |
| ------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------- |
| **DLP** (stessa op, tanti dati) | - ILP (dentro un core, su istruzioni vicine)  <br>- Architetture vettoriali / GPU (istruzioni SIMD su vettori)  <br>- TLP (dividi i dati tra thread) |
| **TLP** (task indipendenti)     | - TLP (thread diversi su core diversi)  <br>- RLP (task/job su nodi diversi, data center)                                                            |

## Affidabilità 
E' la qualità del sistema di inviare correttamente i servizi in modo sicuro e corretto. L'affidabilità può essere influenzata da dei bug dei sistemi hardware, bug nei software, difetti nell'hardware e ci possono essere inoltre problemi che avvengono durante la produzione del sistema.

L'affidabilità viene misurata tramite diverse unità di misure probabilistiche:
- il *Mean Time to Failure* (MTTF, tempo medio di un guasto), che è considerato come 1 FIT = inteso come 1 Failure in One Bilion Times, cioè succede un guasto in un miliardo di ore.
- Il *Mean Time Between Failures* (MTBF), tempo medio dei i vari fallimenti tra i dispositivi.
- Il *Mean Time To Repair* (MTTR) (Tempo medio per riparare)

La formula per calcolare il MTBF è la seguente: 
$$MTBF = MTTR + MTTF$$
## Performance di un Computer
Le performance di un computer viene intesa come il tempo di un computer di eseguire una serie di operazione in un determinato tempo. Dal punto di vista di un utente le performance sono viste come il tempo di risposta di un computer (tempo di inizio e fine di completamento di un'operazione), invece dal sistemista le performance di un computer sono considerate com il totale di lavoro compiuto dal computer in uno specifico tempo. Questo perché il sistemista deve garantire che le operazioni devono essere eseguite in un determinato secondo.
### Tempo di Esecuzione
Il tempo che viene considerato per calcolare le performance di una computer sono il:
- **Elapsed Time**
- **CPU Time**
	- User CPU Time
	- System CPU Time
Queste unità di misura si possono vedere tramite terminale con il comando `time`
```
shell  0.10s user 0.06s system 6% cpu 2.354 total
```
Cioè la durata dell'applicazione, il tempo passato che è passato nell'applicazione

### Valutazioni Delle Performance
Si valutano le prestazioni di un computer andando ad eseguire delle applicazioni o condizioni e vedere il comportamento del computer. Questo è possibile tramite l'utilizzo dei *Benchmark*
### Benchmarks
Programma che utilizzano al massimo le caratteristiche dei dispositivi (componenti di un computer come CPU, RAM o GPU) per fornire delle valutazioni sui dispositivi che vengono stressati e vedere se resistono ai test.

Sono fondamentali perché ci permettono di scegliere i diversi kernel o programmi che sono supportati.

I benchmark più utilizzati sono gli ***SPECS*** (Standard Performance Evaluation Corporation)![[Screenshot 2026-09-25 at 09.10.57.png]]
Sopra ci sono degli esempi di benchmark che alcuni sono utilizzati oggi giorno per valutare il comportamento di un computer sotto stress.

### Riproducibilità
I benchmark che si eseguono devono essere *riproducibili*, cioè far si che si vanno a definire i dettagli riguardo all'hardware, software e i programmi in input.

### Calcolo Tempo Totale Esecuzione
Il calcolo è il seguente:
$$\sum^{n}_{i=1}Time_{i}$$
Cioè la somma di tutti i tempi di esecuzione dei vai programmi, questo come abbiamo visto prima lo si può fare tramite il comando `time`. Oppure ancora meglio sarebbe calcolare la media:
$$\frac{1}{n}\sum^{n}_{i=1}Time_{i}$$
Si può anche decidere di assegnare dei pesi a dei programmi, cioè dare delle priorità a dei programmi che invece di altri.
$$\sum^{n}_{i=1}Weight_{i}*Time_{i}$$
>[!example] Esempio
>![[Screenshot 2026-09-25 at 09.20.55.png]]
>Prendiamo i tempi di esecuzioni di tre processori, $A$, $B$, $C$, con i vari programmi che vanno ad essere eseguiti sui vari processori. I tre calcolatori li posso scegliere in base alla mia importanza

## Linee Guida e Principi per il Computer Design
Le linee guida per la misurazione della performance si basano su due principi:
- [[#Amdahl|Amdahl]]
-  CPU performance equation
### Amdahl
Misura lo speedup di due diverse implementazioni, che ci permette di capire se tra due implementazioni, la seconda implementazione è migliore alla prima oppure non è cambiato di nulla.

$speedup$ = $\frac{perfomance \ with \ enhancement}{perfomance \ without \ enhancement}$

Se lo speed up è uguale ad 1 allora non è cambiato niente, se invece è maggiore di 1 allora ci sono miglioramenti 

Il tempo di esecuzione del nuovo processore sarà la seguente formula:

$execution \ time_{new}$ = $execution \ time_{old}$ ∗ ((1 − $fraction_{enhanced}$) + $\frac{fraction_{enhanced}}{speedup_{enhanced}}$

Il calcolo per lo l'overall dello speedup sarà il seguente:

$speedup_{overall}$ = $\frac{1}{(1-fraction \ enhanced) + \frac{fraction_{enhanced}}{speedup_{enhanced}}}$

### CPU performance equation
$$CPU_{time}=(\sum^{n}_{i=1}CPI_{i}*IC_{i})*Clock \ cycle \ time$$
In few words there are 3 metrics to measure the CPU speed, 
1. the first it's the number of instruction that the CPU should perform, called ****IC** *(Instruction Counter)
2. ***CPI*** (Cycle Per Instruction) average number of clock cycles each instruction requires to complete. CPI depends on the microarchitecture of the processor. Simple instructions may take one cycle, while more complex instructions can take multiple cycles.
3. ***Clock Cycle Time***: is the duration of a single cycle. It is the reciprocal of the clock frequency. A 2 GHz processor has a cycle time of 0.500 nanoseconds (the calculus it's  $\frac{1}{2*10^{9}}$), while a 3 GHz processor has a cycle time of about 0.333 nanoseconds.
To understand performance, computer architects use a fundamental equation that breaks down CPU execution time into three factors:

$$ CPU \ time= Instruction \ Count * CPI * Clock \ Cycle \ Time$$
# Reference
---

[^1]: **Computer cluster**, o più semplicemente un **cluster** (dall'[inglese](https://it.wikipedia.org/wiki/Lingua_inglese "Lingua inglese") _grappolo_), è un insieme di [computer](https://it.wikipedia.org/wiki/Computer "Computer") connessi tra loro tramite una [rete telematica](https://it.wikipedia.org/wiki/Rete_telematica "Rete telematica")
