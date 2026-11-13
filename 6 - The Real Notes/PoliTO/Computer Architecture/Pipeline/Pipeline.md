---
created: 2026-10-02
tags:
  - baby
topics:
  - Architecture 
  - "[[School]]"
  - Pipeline
author: Danilo Quattrini
---
# Questions
---
## Concetti base
- Che cos'è una pipeline?
- Come funziona una pipeline?
- Quali sono le principali operazioni che vengono eseguite da una CPU?
- Qual'è la pipeline ideale che si cerca di raggiungere? Come viene misurata?
## From Unpipeline to Pipeline
- Quali sono i 5 cicli di clock che vengono eseguiti per eseguire un'istruzione?
- Quale operazioni vengono svolte durante la fase di **IF**?
- Quale istruzioni vengono svolte durante la fase di **ID**?
- Quale istruzioni vengono svolte durante la fase di **EX**?
- Quale istruzioni vengono svolte durante la fase di **MEM**?
- Quale istruzioni vengono svolte durante la fase di **WB**?
- Quante cicli di clock servono per completare un istruzione? Invece se ci sono dei branc quanti ne servono?
- Come si possono svolgere delle ottimizzazioni?
- Elenca i registri che sono presenti tra i vari cicli di clock e che cosa memorizzano al loro interno?

# Definizione
---
La pipeline è una tecnica che permette di eseguire le istruzioni in parallelo. L'idea è realizzare un'implementazione dell'architettura, dove la maggior quantità di istruzioni vengono eseguite in parallelo, non vengono sempre eseguite le stesse istruzioni, ma si possono eseguire operazioni varie.

l'istruzione è composta da *Fetch*, *Decode*, *Execute*, *Write*, da vedere dentro [[CPU#Functions of the CPU| funzioni della CPU]], in un processore CISC si attendeva l'esecuzione di un istruzione per procedere alla successiva![[Screenshot 2026-10-02 at 08.40.41.png]]
Si cerca di avere una situazione, dove nel mio processore ho 4 istruzioni parallelo, con ognuna uno stadio diverso tra di loro. Prima finivo 4 istruzioni in 8 colpi di clock, invece con le pipeline viene eseguite 4 istruzioni in 7 colpi di clock

Il throughput sarà il numero di istruzioni eseguite per unità di tempo, l'idea della pipeline è dividere le operazioni in stage di pipeline che sono sincronizzate. Per eseguire uno step è chiamato **machine cycle** e normalmente corrisponde ad **1 clock cycle**

*CPI*: clock per instruction
## Ideal Pipeline
Non eseguo l'istruzione completa in 1 colpo di clock, ma si dividono gli stadi della pipeline in $n$ elementi, dove dividiamo l'elaborazione delle istruzioni in $n$ passaggi, quello che avremmo è:
$$throughput_{pipeline} = throughput_{unpipeline}  * n$$
Dove abbiamo $n$ sono il numero degli stage della pipeline.

## Unpipelined Implementation
Partiamo con un'implementazione non-pipeline, che diventerà pipeline, l'idea è far eseguire il processore con le stesse quantità di istruzioni. L'esecuzione di ogni istruzione sarà composti da 5 cicli di clock:
1. **Instruction Fetch Cycle (IF)**:  il *fetch* significa **recuperare**, che in questo caso è un'istruzione nella memoria
2. **Instruction Decode/Register Fetch Cycle (ID)**: si guardano i 7 bit dell'*Opcode* per capire qual'è l'istruzione da eseguire, nella decodifica potrei sapere quali sono i registri che dovrei utilizzare
3. **Execution/effective Address Cycle** (EX)
4. **Memory Access/Branch completion cycle** (MEM)
5. **Write-back cycle**: scriviamo i dati della nostra elaborazione

## Unpipelined Datapath
![[Screenshot 2026-10-02 at 08.55.44.png]]
In ognuna delle fasi ci sono degli elementi che sono coinvolti, dove i rettangoli sono i registri, il **PC** indica qual'è la prossima istruzione da eseguire, da [[CPU Components#PC (Program Counter)|vedere qui]]. Il PC accede alla memoria delle istruzioni e salva le istruzioni nell'IR, ma dopo IL CU va a vedere il valore dell'IR, decidendo quale registri definire come sorgente e operando.

Nel momento dell'elaborazione, vengono eseguite delle operazioni sulla ALU, dove l'output di tale operazione vengono salvate nella memoria
### Instruction Fetch Cycle
![[Screenshot 2026-10-02 at 09.01.46.png]]
Si prender l'istruzione dalla memoria (MUX nell'immagine), che viene salvata nel program counter, La prossima istruzione invece si trova nella posizione +4 byte, ma con i salti tipo `j` o `jre`, cambiano. L'**ADDER** ci permette di fare in automatico l'operazione di aggiunta di +4 per andare alla prossima istruzione **NPC** (Next Program Counter), quindi avremmo **NPC = PC + 4**

### Instruction Decode Register Fetch
![[Screenshot 2026-10-02 at 09.03.14.png]]
Si legge l'istruzione dove si vanno a capire l'operazione che si dovrà svolgere, ma si faranno anche delle scelte speculative, perché nella fase di decode, non so effettivamente se ho un'istruzione che userà 2-3 registri o un'istruzione di salto, in questo momento dove sto capendo se sono dei registri o operazioni di salto.

**Rs1**: (Registro 1): definito dai bit 15 a 19
**Rs2:** (Registro 2) definito dal bit 20 a 24

Le istruzioni anno decodifica fissa precisa.![[Screenshot 2026-10-02 at 09.09.04.png]]
Diciamo che abbiamo un dato immediato, dove lo prendo ed estendo il segno con il **sign extender** per farlo arrivare a 32 bit, dalle 12 bit che sono dedicate vengono aggiunti 10 bit per estendere.![[Screenshot 2026-10-02 at 09.11.16.png]]
### Execute/Effective Address Cycle
![[Screenshot 2026-10-06 at 09.39.31.png]]
So che tipo di elaborazione che devo fare, questa è variegata in base all'operazione che è stata decodifica precedente, esempio se devo accedere alla memoria. Completo le operazioni ad esempio.

**Memory Reference**
`ALUOutput <- A + Imm`
Qui sto aggiungendo il valore immediato nella memoria dando anche un valore di *offset* cioè spostare il registro in una posizione specifica

**Register-Register ALU Instruction**
`ALUOutput <- A funct B`

**Register-Immediate ALU Instruction**
`ALUOutput <- A funct Imm`

**Branch**
`ALUOutput <- NPC + Imm << 2`
`Cond <- ( A == B )`
Il valore immediato può essere shiftato a sinistra, cioè moltiplicato a 4 cioè i bit meno significativi sono 00, e a questo valore sommiamo il `Next Program Counter`.

### Memory Access/Branch Completion Cycle
Accedo alla memoria utlizzando (Load Memory Address), usando il **Memory Reference**
`LMD <- MEM[ALUOutput]` oppure `MEM[ALUOutput] <- B`

In questa fase posso anche completare le operazioni di branch, dove
```c
if (cond) {
	PC <- ALUOutput;
} else {
	PC <- NPC;
}
```

### Write-back Cycle
Fase finale di elaborazione dove salvo il valore di output o l'output della ALUOutput nei registri, che in questo caso è il registro destinazione **Rd** che va dal 7 bit fino all 11 bit dell'istruzione, che prima abbiamo definito come sorgente:
![[Screenshot 2026-10-02 at 09.24.15.png]]
## Ottimizzazioni
Ogni istruzioni hanno bisogno di 5 clock cycle, tranne le istruzioni branch che ne richiedono 4. Le ottimizzazioni che si possono fare è quello di far si che l'ALU scrive direttamente nei registri di destinazione, durante l'accesso alla memoria. Si possono utilizzare risorse hardware che riducono le duplicazioni. I diversi passaggi che devono eseguire una macchina statica non è complicata

## Conversione al Pipeline
Convertiamo il processore definito prima in modo che sia *pipeline*, facendo questi passaggi:
1. Ogni nuova istruzione viene inizializzata in ogni ciclo di clock (clock cycle), ogni colpo di clock devo sapere qual'è la prossima istruzione.
2. Utilizzo diverse risorse per ogni istruzione, cioè dovrei avere instruction register, che si risolve aggiungere dei blocchi di pipeline tra ogni stage.
3. In ogni clock cycle le risorse devono essere utilizzate solo per un singolo scopo, questo significa che:
	1.  Memoria separata per le istruzioni (vengono usate le cache)
	2. Si utilizza il register file, durante la decodifica e la scrittura finale e questo register file deve essere in grado di di eseguire queste due fasi insieme (scrivere nella prima metà del clock e la lettura/decodifica nella seconda metà)
	3. Il PC deve essere modificato
## Pipelined Data Path
![[Screenshot 2026-10-02 at 09.36.22.png]]
Si visualizza quindi la Datapath con ogni fase ci sono dei registri di pipeline che prendono il nome delle fasi della Datapath.
Per risolvere questo problema, vengono aggiunti dei **registri di pipeline** (detti anche _pipeline latches_) posizionati esattamente al confine tra due stadi contigui:

1. **IF/ID**: Memorizza l'istruzione letta dalla memoria delle istruzioni (`IR`) e il Next Program Counter (`NPC`).
2. **ID/EX**: Memorizza i dati letti dal Register File (operandi `A` e `B`), l'estensione del valore immediato (`Imm`) e i segnali per la ALU.
3. **EX/MEM**: Memorizza il risultato calcolato dalla ALU (`ALUOutput`), il dato da scrivere eventualmente in memoria e le condizioni di branch (`Cond`).
4. **MEM/WB**: Memorizza il dato letto dalla memoria dati (`LMD`) o l'output della ALU (`ALUOutput`), oltre all'indirizzo del registro di destinazione (`Rd`).


Avremmo poi un'elaborazione di questo tipo![[Screenshot 2026-10-02 at 09.40.15.png]]
Nella CC (**Colpo Di Clock**) la linea tratteggiata nel registro vuol dire che prima si legge l'istruzione e poi viene scritta nella seconda parte del registro
## Pipeline Performance
La pipeline incrementa il throughput del processore senza rendere ogni singola istruzione veloce. Il processore riesce ad elaborare più istruzioni nella stessa quantità di tempo. 

Prendiamo un esempio per capire che stiamo usando la pipeline in modo efficace
>[!example] Esempio
>Il clock per cycle è di 1ns, le operazioni della ALU e di branc richiedono 4 cycle, le operazioni di memoria invece 5. Le frequenze delle operazioni sono 40%,  20%, 40%
>$$CP * average CPI = 1ns *((0.4 + 0.2) * 4 + 0.4 * 5) = 4.4ns$$
>Supponiamo che 

completare  con slide 23-24 della Pipeline
## Pipeline Hazard 
Rischi della pipeline che sono 3 tipi:
1. **Strutturali**: in base all'hardware
2. **Dato**: relativi alle dipendenze di dati
3. **Controllo**: relativi al cambio di flusso di operazioni che si basano nei salti
### Stalls
Uno stallo come una situazione dove la pipeline è forzata a fermare una cerca quantità di istruzioni per far si che le istruzioni completino i propri stadi, questo potrebbe richiedere di fermare la seconda istruzione così la prima può andare avanti. 

Quando fermo le istruzioni, inserisco delle bolle nella pipeline, che fanno perdere tempo. Esempio il grafico qui sotto![[Screenshot 2026-10-02 at 10.13.31.png]]
Nella istruzione 4 cioè nel Clock Cycle 4 si blocca l'elaborazione, perché due istruzioni non possono accedere alla memoria nello stesso tempo, quindi blocco l'istruzione in entrante e

### Rischi Di Tipi Strutturali
Sono relativi ai componenti hardware, questo perché se non ho due memorie separate.
![[Screenshot 2026-10-02 at 10.17.29.png]]
L'unica soluzione sono i soldi. 

### Rischio Di Dati
Sono relativi alle dipendenze e sono critici e da individuare velocemente. Un problema della pipeline è che siccome le istruzioni sono eseguite in paralello cioè una sopra ad un'altra gli operatori di accesso. Questo può risultare risultati sbagliati e comportamenti non deterministici:

Prendiamo l'esempio:
```
ADD R1,R2,R3
SUB R4,R1,R5 
AND R6,R1,R7
OR R8,R1,R9 
XOR R10,R1,R11
```
Creiamo una dipendenza di dati tra `R1` e i registri dei dati
![[Screenshot 2026-10-02 at 10.26.01.png]]
Succede che con `R1` la prima istruzione calcola la somma tra `R2` e `R3`   e salva l'operazione in `R1`, Nella seconda operazione con il `SUB` il valore di `R1` è cambiato che comporta a valori sbagliati. Solo nell'operazione di `XOR` ha il valore vero di `R1` aggiornato.

Quindi ho dipendenze di dati e non gestirle avrò problemi di determinismo. 

**Risoluzione**: introdurre degli stalli oppure implementare un bypass alle unità che ne hanno bisogno tecnica del **forwoarding**

### Forwarding
Tecnica speciale che mi permette di anticipare i dati alle istruzioni successive anche se il dato non è salvato nei banchi dei registri, serve che il dato sia calcolato, per poterlo utilizzare nelle istruzioni successive.
>[!info] N.B
>Nel programma ASE si può rimuovere il forwarding

Cambia la pipeline in questo, creando dei cammini particolari, dall'output dell'operazione.![[Screenshot 2026-10-02 at 10.34.11.png]]
L'istruzione di sottrazione non prende il valore dal registro, ma lo prende dal registro della  pipeline, senza fermare il processore e far camminare il processore. Mando i dati in avanti senza bloccare il processamento.

>[!info] Info
>Il valore che serve all'istruzione `SUB` viene presa direttamente alla fine della fase di execute dell'`ADD`, senza dove aspettare che l'istruzione `SUB` finisca in fase di `WB` 
#### Generalizzazione della tecnica di forwarding
Se voglio evitare lo stall il forwarding deve essere sempre possible in ogni **pipeline  register** in ogni input register
```arm
ADD R1,R2,R3
LD R4,0(R1)
SD R4,12(R1)
```
![[Screenshot 2026-10-02 at 10.38.14.png]]
Quando abbiamo rischi di dato, quando **abbiamo dipendenze tra i registri e dipendenze di memoria**. Questo succede se scriviamo e leggiamo nella stessa locazione di memoria.

Non tutti i rischi sui dati si possono risolvere con il **forwarding**, prendiamo questo esempio
```
LD  R1, 0(R2)  FDEMW +1
SUB R4,R1,R5    FDSEMW +2
AND R6,R1,R7     FSDEMW + 1
OR R8,R1,R9       SFDEMW + 1
```
La prima istruzione va tranquillamente bene, mentre la seconda deve stare in stallo per poter utilizzare il registro `R1`, perché leggo `R1` prima che sia scritto nel processore (cioè dopo la fase di write-back allora posso utilizzare `R1`), come si vede nell'esempio sopra l'esecuzione della seconda istruzione riparte solo dopo che è stato scritto il valore di `R1` in memoria
![[Screenshot 2026-10-02 at 10.49.51.png]]
Non si può andare indietro nel tempo, quindi non si può usare il forwarding.
In questo caso l'unica soluzione sarebbe lo stallo, che viene propagata nelle istruzioni![[Screenshot 2026-10-02 at 10.51.11.png]]
Questo lo si gestisce in fase di decodifica e lo si può fare anche abiltando il forwarding
![[Screenshot 2026-10-02 at 10.58.14.png]]
```
LD  R1, 0(R2)  FDEMW +1
SUB R4,R6,R5    FDEMW +2
AND R6,R1,R7     FDEMW + 1
OR R8,R1,R9        FDEMW + 1
```
Nel terzo esempio dell'immagine non attivo uno stallo, ma un **forwarding**

#### Introdurre uno Stallo
Per introdurre uno stallo si aggiunge un'istruzione di tipo `nop`, [[RISC#^504f4e|NOP]] nella fase di **Instruction Decode** ed **Execute** oppure si stoppa il **program counter** (PC)

#### Forwarding to the ALU inputs
![[Screenshot 2026-10-02 at 11.04.34.png]]

### Rischi Di Controllo
Quando compaiono i salti, devo o posso saltare in  base ad una condizione, cioè quanti colpi di clock vado a perdere? Ne sono due e vengono fatti nella **fetch dell'istruzione**
#### Soluzione
Cercare di migliore i dispositivi o decidere se un branch deve essere preso oppure no.

### Basic pipelined data path
![[Screenshot 2026-10-02 at 11.08.07.png]]
Questo sotto è il comportamento del processore in questo momento
![[Screenshot 2026-10-02 at 11.08.37.png]]
Vado a perder i colpi di clock sempre
![[Screenshot 2026-10-02 at 11.09.19.png]]
La soluzione è spostare l'hardware nella fase precedente della decodifica, in questo modo spostiamo la parte del controllo e il sommattore prima, in questo caso andiamo a perdere solo un colpo di clock.![[Screenshot 2026-10-02 at 11.10.30.png]]
vedere le slide 68-75

### Tecniche Alternative
Ci sono tecniche alternative che sono relative al migliorare il processo di esecuzione delle fasi di un ciclo di clock e sono:
- Stoppare la pipeline
- Predirre i salti come non presi
- Predirre i salti
- Usare uno slot di tempo chiamato **branch delay slot**
Lo si possono utilizzare nel compilatore.
#### Stoppare la Pipeline
Appena la pipeline si accorge che stiamo lavorando con un salto ferma le istruzioni successive, lo raggiungiamo solo durante lo stage di decodifica,.
#### Predirre i salti come non presi
Immaginiamo che i salti non sono presi, perché di solito l'istruzione successiva non è l'istruzione target del salto, ma l'istruzione salto + 1, cioè PC + 4byte, lo fa in modo automatico. Quindi se non saltiamo andiamo a fare un'elaborazione più efficiente.
![[Screenshot 2026-10-07 at 08.57.20.png]]
Se prendiamo un salto noi ce ne accorgiamo nella fase di execute del salto

#### Predire il salto come preso
Per predire il salto come preso, dobbiamo avere l'indirizzo da dove poter saltare, cioè serve predire dove si sta saltando.

## Compilatore
Integrare il processore con il compilatore, quando si fa questa elaborazione, il compilatore dovrebbe essere in grado di darmi una mano a creare programmi più efficienti, con il tipo di salto che ho preso. Cioè come il compilatore andrà a compilare i cicli o le iterazioni all'interno del nostro programma, quando vengono riportate in assembler.

Se ho un ciclo `for` o `do-while`, dove nel ciclo `for` noi controlliamo la condizione del ciclo di salto (es `i = 0, i < costante, i++`) la condizione viene eseguita prima del corpo del ciclo. Nel `do-while` invece noi eseguiamo prima il processo poi facciamo il confronto e saltiamo.

Conviene fare tutti i cicli come se fossero dei `for`, faccio i controlli prima di eseguire delle operazioni nel corpo. Se mi accorgo che non devo saltare evito di fare altre operazioni aggiuntivi.

## Delayed Branch
Cosa facciamo se il processore perde dei colpi di clock quando, per esempio il salto viene preso (il branch), dipende dalla dimensione della pipeline, se io devo perdere 1 o più colpi di clock. In alcuni processori, ci permettevano di non perdere i colpi di clock delle operazioni successive, ma effettivamente eseguire le istruzioni successive: Nel caso iniziale si perdono due colpi di clock, perché si fà il fetch delle due istruzioni successive![[Screenshot 2026-10-07 at 09.20.49.png]]
A seconda delle configurazioni del processore, si potevano far eseguire sempre due istruzioni, come nell'immagine. Per facilità si usava mettere dopo i salti delle `nop`.

**Esempio di Programma**
```asm
#******** RISCV INITIAL PROGRAM ************
#-------------------------------------------
# AddTwoVectors.s
# this program adds two vectors and stores 
# the result in another vector
#-------------------------------------------
.section .data 
# Vettore con 10 elementi da 4 byte, quindi sarà di dimensione 4 * 10 = 40 byte la dimensione del vettore
V1:	.word 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 
V2:	.word 1, 2, 3, 4, 5, 6, 7, 8, 9, 10
result:	.space 40
	.section .text
# This prologue ensures that vectors are in 
# the cache when we need them, otherwise 
# the pipeline will stall at first access
.globl _start
_start:
      nop
main:
     la x1, V1		FDEMW
					 FDEMW                              6 
     la x2, V2		  FDEMW                             
					   FDEMW						    2
     la x3, result								        2
     addi x4, x0, 10      FDEMW                         1
cycle:                                                  
     lw x5, 0(x1)	       FDEMW					    1
     lw x6, 0(x2)	        FDEMW					    1
     add x7, x5, x6			 FDSEMW						2
     sw x7, 0(x3)	    	  FSDEMW					1
     addi x1, x1, 4				FDEMW					1
     addi x2, x2, 4				 FDEMW					1
     addi x3, x3, 4				  FDEMW					1
     addi x4, x4, -1	           FDEMW				1
     bnez x4, cycle		   			FSDEMW 				2+1  (10*12)
     nop			                  F---- 			
									  FDEMW             -
END_of_PROGRAM:                # Total c.c.           131        			
     li a0, 0  		
     li a7, 93 
     ecall
```

l'operazione di `add x7, x5, x6` cioè somma `x7 = x5 + x6 ` ha un problema di dipendenza (cioè dipendono dalle due istruzioni precedenti `lw x5, 0(x1)`), questo perché utilizza i due registri che stavo caricando in precedenza che devono essere ancora caricati.

**Me ne accorgo in fase di decodifica** ([[#Instruction Decode Register Fetch|ID]]), perché nella fase di fetch ancora non so nulla, ma nella decodifica controllo i miei registri sorgenti con i registri di destinazione delle istruzioni che sono presenti nella pipeline precedenti e osservo che `x5` e `x6` sono stati aggiornati nelle due istruzioni precedenti.

Il problema è `x6` perché quando in decodifica la somma `add x7, x5, x6` e leggo dai banco dei registri `x5` e `x6` vedo che:
1. Si stanno aggiornando le istruzioni all'interno della pipeline
2. `x6` non ha completato il suo aggiornamento, perché è in fase di elaborazione (Execute)

La soluzione è fermare il processore con uno [[#Stalls|stallo]], che tipo di **hazard ho attivato**?
In questo caso ho attivato una [[#Rischio Di Dati|hazard di dato]].

Dopo la fase di [[#Memory Access/Branch Completion Cycle|MEM]] del registro `x6` io posso eseguire l'istruzione di addizione, questo perché ora il dato è presente nei registri.

Se un istruzione è ferma nella pipeline non può passare quella successiva, questo è il caso dell’istruzione store (nella riga 31 `sw` store word), che il processore si dovrà fermare perché la pipeline è occupata dall’istruzione precedente. Dopo la fase di decodifica la store passa alla fase di execute, dove va a calcolare l’indirizzo effettivo (che serve solamente` x3` e `x0`), nella riga `31` del codice della locazione di memoria dove salvare il valore, ma non ho bisogno del valore di `x7` perché lo userò solo nella fase di Memory. Nella memory salvo il dato di `x7` in memoria e write back. Quindi l’istruzione `add`, (riga `29`) contribuisce con 2 colpi di clock e la store di uno solo.

L’istruzione di salto (jump) è particolare perché andiamo a modificare l’hardware. Dove inizia la fase di fetch che prende l’istruzione e nella fase di decodifica confronta il registro `x4` con 0 (cioè se `x4` è diverso da `0`), cercando i capire se sono uguali e per farlo ha bisogno di x4 in fase di decodifica. Ma in questa fase `x4` non è ancora pronto quindi deve stallare rimanendo nello stato FDS, poi dopo quando l’istruzione precedente (che sarebbe `addi x4, x4, -1`) ha passato la fase di execute, solo da allora l’operazione di Jump può andare avanti. Quindi il salto ha 2 cicli di clock per la dipendenza di dati discussa precedentemente.

Nel ciclo quindi avremmo i 12 colpi di clock all’interno del ciclo, per le n volte che ripetiamo il ciclo includendo anche l’ultima istruzione.

>[!warning] Importante per l'esame
>Dobbiamo evitare nel conteggio le operazioni dopo il Label `End`

Importante notare nel codice:
•⁠  ⁠Le dipendenze di dato, che posso bloccare le altre istruzioni, che si osservano quando eseguivamo delle modifiche a dei registri prima che completino le loro operazioni
# Reference
---

