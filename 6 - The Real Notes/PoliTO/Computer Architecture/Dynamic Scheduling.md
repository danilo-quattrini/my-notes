---
created: 2026-10-23
tags:
  - baby
topics:
  - Architecture 
  - "[[School]]"
author: Danilo Quattrini
---
# Dynamic Scheduling
---
## Questions
### Introduzione
- Che cosa si vuole evitare di incappare quando si eseguono le istruzioni in-order?
- Qual'è lo scopo del Dynamic Scheduling?
- Perché si preferisce un approccio *out-of-order*?
-  Che problemi si possono riscontrare in un esecuzione *out-of-order*?
### Splitting ID Stage
- Come viene divisa la fase di ID (Instruction Decode)?
- Da dove vengono prese le istruzioni da dover eseguire?
- Che cosa deve si deve aspettare nella execution phase prima di passare all'esecuzione vera e propria delle istruzioni?

### Hardware Schemas
- Quale schema vengono utilizzati per il Dynamic Scheduling?
- Qual'è quello più utilizzato?

### Tomasulo Architecture
- Su che idee principali si basa l'architettura di Tomasulo?
---
## Introduzione
Abbiamo visto solo come paralellizzare la execute però non abbiamo visto come si possono paralellizzare altre fasi del processore (IF, ID, ecc...), dobbiamo quindi capire come paralelizzare le istruzioni in modo dinamico, lasciando al core il compito di eseguire le istruzioni appena possibile.

Meccanismo basato principalmente sull'architettura HARVARD, l'idea è quello di **identificare le dipendenze al più presto possibili**, anche quelle che non si conoscono al tempo di compilazione, inoltre **bisogna anche semplificare il lavoro del compilatore**.

Utilizzando questo schema si riesce anche a tollerare delay troppo lunghi, si può utilizzare lo stesso codice di un RISC-V in un processore super-scalare.

>[!example]
>Diciamo che la divisione not-pipelined ha 10 stadi di latenza, scriviamo la pipeline.
>```asm
>fdiv.s f0, f2, f4  FD//////////MW
>fadd.s f10, f0, f8  FDSSSSSSSSS***MW
>fsub.s f12, f8, f14  FSSSSSSSSSSSSSD---MW
>```
>L'obbiettivo è quello di far si che le operazioni **debbano essere eseguire fuori ordine** ***out-of-order***, invece che *in-order*, questo per far si che si vada ad evitare gli stalli che abbiamo visto nell'esempio sopra.

## Esecuzioni OUT-OF-ORDER
Questa esecuzione però può introdurre rischi che abbiamo già visto, che sono:
- WAR hazard
- WAW hazard
- Gestione delle eccezioni in modo impreciso

### WAR HAZARD
In una esecuzione out-of-order, possono capitare dei WAR (Write After Read) hazard
![[Screenshot 2026-10-23 at 08.52.55.png]]
```
fdiv.d f0, f2, f4 FD//////////MW
fadd.d f6, f0, f8  FSSSSSSSSSSSD+++MW
fsub.s f8, f9, f14             FSSSSD---MW
```
Nell'esempio di sopra abbiamo che l'esecuzione è *out-order* invece che *in-order*, questo possono causare gli hazard di tipo **write after read** (WAR) perché se l'istruzione di sottrazione finisce la sua esecuzione prima dell'addizione allora il risultato di `fadd.d` verrà sbagliato.
### WAW HAZARD
Stessa cosa può avvenire invece anche nel Write after Write (WAW):
![[Screenshot 2026-10-23 at 08.53.33.png]]

### Gestione delle Eccezioni
Se si abilita l'esecuzione del codice *out-of-order*, la gestione delle eccezioni può risultare complicata in questi casi:

1. Se l'istruzione precedente,  lancia un eccezione prima di aver completato la propria esecuzione 

2. Se l'istruzione successiva completa la propria esecuzione, ma poi c'è l'eccezione.

In entrambi i casi è difficile gestire tale eccezione, quindi ci sono dei modi che verranno spiegati [[qui]]
## Splitting the ID (Instruction Decode) Stage
Per garantire una esecuzione del codice *out-of-order* si divide la fase di decodifica in due parti e si creano due sotto-stalli della pipeline:

- **issue**: decodifica l'istruzione e controlla se ci sono degli [[Pipeline#Rischi Di Tipi Strutturali|hazard strutturali]]

- **read operands**: legge gli operandi in un secondo momento, se e solamente se sono pronti, in modo da evitare hazard di tipo dato.

### Elementi dello Splitting
Tutte **le issue delle istruzioni devono essere in ordine**, permettendoci di mantenere dei vincoli con i data-flow del programma e inoltre si cercherà di leggere alcuni dati dei registri che sono consolidati.  Le istruzioni che sono mandate in *issue*, vengono prese da una coda (queue) o da un registro.

Poi dopo si  attenderà che gli operandi che devono essere inviati allo stadio di execute quando saranno pronti.

### Execute Stage
Fase **eseguita fuori ordine** (out-of-order), **perché ci sono degli operandi che devono essere pronti che però vengono eseguite istruzioni**, quando gli operandi sono fuori-ordine si possono eseguire.

## Hardware Schemes for Dynamic Scheduling
Ci sono due tipologie di tecniche:
- *Scoreboarding*![[Screenshot 2026-10-23 at 09.09.25.png]]
Quando gli operandi sono pronti nella sub-sezione della decodifica **read-operands**, allora lo manda avanti in fase di esecuzione.

- *Tomasulo's Alghoritm*
### Tomasulo Approach
Robert Tomasulo propone nel 1967 di creare un unità chiamata **reservation station**, che permette di tracciare la disponibilità degli operandi e ri-nominare i registri del programma.

>[!info] Qual'è l'idea principale?
>L'idea principale di questa architettura è quello di eseguire le istruzioni **out-of-order**, ma utilizzando un emissione delle istruzioni *in-order*, andando ad evitare i falsi hazard di tipo WAR e WAW, tramite il **Register Renaming**.

#### Componenti dell'architettura di Tomasulo
![[Screenshot 2026-10-23 at 09.12.28.png]]

##### Instruction Queue
![[Screenshot 2026-10-23 at 09.12.28 copy.png]]

La coda delle istruzioni come vediamo dall'immagine nel centro in altro viene riempita nella fase di **pre-fetch**, dove si prendono le istruzioni nella memoria e vengono inserite nella **coda** (ricordiamo che la code funzionano in FIFO **First-In-First-Out** cioè il primo elemento ad entrare nella coda sarà l'ultimo ad uscire), per questo motivo l'istruzione che viene inserita per primo nella coda verrà inviata in una dei due percorsi:

1. **Load-Store Operations**: qui vanno le istruzioni come `flw`, `fsw`, `sw`, `lw`, ecc... che sono inviate alla **address unit**
   
2. **Floating Point Operations**: le operazione come `fadd.s`, `fmul.s`, `fdiv.s`, ecc.. vengono inviate in questo BUS che arrivano direttamente alle **Reservation Station**

##### Address Unit
![[Screenshot 2026-10-23 at 09.12.28 copy 2.png]]
In questa fase si vanno a calcolare l'indirizzo effettivo della memoria dove si vuole caricare (con l'operazione di *store*) o scaricare (tramite l'operazione di *load*) il dato interessato. 

Questo calcolo avviene prendendo l'indirizzo che gli è stato passato dalla **instruction queue** e gli si aggiungi l'*offset* se è presente. 

Il risultato del calcolo fatto dalla **address unit** viene poi inviato o agli *Load Buffers* oppure agli *Store Buffers*

- **Load Buffers**: locazione di memoria temporanea che salva le operazioni di `load` con il dato che deve richiedere, ed aspetta che la memoria sia disponibile per eseguire l'operazione

- **Store Buffers**: sempre delle memorie temporanee che servono a mantenere l'operazione e il dato che si vole caricare nella memoria, questo fino a quando la memoria non si libera

Gli _Store Buffers_ monitorano il _Common Data Bus (CDB)_ per catturare il dato da scrivere in memoria se quest'ultimo non era ancora pronto al momento dell'emissione.
##### Memory Unit
![[Screenshot 2026-10-23 at 09.12.28 copy 3.png]]
Abbiamo poi la **Memory Unit** (che possono essere o memorie cache oppure RAM) che si interfaccia direttamente con **CDB** per far si di eseguire effettivamente le operazioni di **Load** e **Store**.

##### FP Registers
![[Screenshot 2026-10-23 at 09.12.28 copy 4.png]]
Sono i registri `f0`, `f1`, `f2`, ecc...,  che possono contenere il valore floating point per svolgere il calcolo, oppure vengono salvati i risultati delle operazioni.

>[!info] 
>In fase di *issue* (vedremmo dopo cos'è), quando l'istruzione di store che deve scrivere in uno dei registri presenti nella lista dei registri (`f0`, `f1`, `f2`, ecc...,) oppure una delle operazioni di moltiplicazione, addizione o divisione vanno a scrivere il risultato in uno dei registri FP. Lo stack dei registri si salva un **TAG** che identifica chi tra lo *Store Buffer* e le *Reservation Station* che hanno cambiato il valore di un registro.

In arancione invece vediamo gli **Operational Buses**, che sono semplicemente dei bus di lettura dove mandano i dati nelle *Reservation Station* 

In qualche modo qui andiamo ad eliminare nella fase di *fetch*, perché avremmo una coda di istruzioni presenti nella parte centrale, questo buffer è stato riempito dalla fase di **pre-fetch**, dove ci sono tutte le istruzioni in ordine.

Le istruzioni che escono dalla coda, saranno distribuite al resto del processore, come abbiamo visto prima e vanno nella fase di *issue* e vede se ci sono degli operandi, e se sono pronti, vanno nella **reservation station**, che **ogni unità funzionale (addizioni, moltiplicazione, divisione, eccc) possiede la propria reservation stations**. Ci sono alcuni processori che hanno tante reservation station a seconda delle unità funzionali che possiede il processore.
##### Reservation Station
![[Pasted image 20261027120715.png]]
Quelli evidenziati in verde, loro ricevono i dati dalla coda di **pre-fetch**  e si comportano come delle **"sale di attesa"**, cioè ci sono le istruzioni (esempio `fadd.s`, `fmul.s`, ecc...) che aspettano il valori degli operandi prima di poterli passare direttamente alle unità funzionali, vedremmo dopo che cosa contengono ogni entry della reservation station [[#Instruction Identifiers|qui]].

##### FP Multipliers & FP adders
Sono le unità di calcolo che effettuano i veri e propri calcoli, **solo e solamente se nelle reservation station i valori degli operandi siano effettivamente pronti**, in tal caso dopo aver svolto il calcolo manderà il risultato verso il.
##### Command Data Bus (CDB)
![[Screenshot 2026-10-23 at 09.12.28 copy 5.png]]
Quello che è evidenziato in blu è il *Common Data Bus*.

Le unità funzionali scriveranno le informazioni sulla **CDB**, che è accessibile dalle reservation station, dalla load e store buffer. La problematica che si presenta però è che se il CDB sono accedute da diverse unità funzionali può diventare un collo di bottiglia (*bottle-neck*). Non è necessario che il CDB va nei buffer di lettura e tutte le istruzioni possono guardare cosa succede nella CDB

>[!example] Funzionamento
>Quando uno delle due unità funzionali finiscono i loro calcoli, queste inviano i risultati delle operazioni verso il CDB, con il risultato dell'operazione + il tag (`TAG Reservation Statio, valore calcolato`) Tutte le stazioni di riserva e i registri in ascolto che stavano aspettando quel preciso Tag catturano il valore direttamente dal bus nello stesso ciclo di clock.

### Instruction Identifiers
Ogni reservation station abbiamo detto che hanno un identificativo, che vanno ad identificare anche gli operandi delle istruzione.

Qui di seguito vediamo le componenti dell'identificativo
- **Op:** Il codice dell'operazione da eseguire.
    
- **$V_j, V_k$:** I **valori** effettivi degli operandi sorgente $j$ e $k$ (compilati se il dato è già disponibile).
    
- **$Q_j, Q_k$:** I **Tag** (identificativi) delle stazioni di riserva o buffer che produrranno gli operandi $j$ e $k$ (se i dati non sono ancora pronti).
    
- **Busy:** Flag (Sì/No) che indica se la stazione è attualmente occupata.
  
![[Screenshot 2026-10-23 at 09.43.13.png]]
#### Register Renaming
>[!example]
>Diciamo che la divisione ha 10 stadi di latenza, scriviamo la pipeline.
>```asm
>fdiv.s f0, f2, f4  FD//////////MW
>fadd.s f10, f0, f8  FDSSSSSSSSS***MW
>fsub.s f12, f8, f14  FSSSSSSSSSSSSS---MW
>```
>Quando la seconda istruzione cerca `f0` non andrà a trovare`f0`. ma andrà invece a ricercare il valore della reservation station.

I rischi WAW e WAR vengono eliminati, il data-flow è lo stesso, ma il registro destinazione di un istruzione verrà sostituito dal valore della **reservation-station**.

#### Distributed Hazard Detection
Controllo più complesso, ma distribuito dove ogni elemento gestirà il controllo a modo suo.
===(vedere se da completare oppure no)===
### The instruction Step
La fase di decodifica viene quindi divisa in:
- Issue dove c'è un (Emissione in-order) delle istruzione dalla coda
- Execute esecuzione delle istruzioni **out-of-order**
- Write Result
#### Issue
Quando prelevo l'istruzione nella coda, **si deve capire se ci sono delle reservation station disponibili**, se le reservation station sono piene allora si stalla finché la reservation station sia disponibile (in un processore ci possono essere 32 o 48 reservation station).

Se i valori degli operandi sono disponibili nei register file, allora vengono messi in $V_{j}$ e $V_{k}$, se invece i dati nei file dei registri non è ancora pronto allora si andrà a mettere il Tag dell'operazione nelle sezioni $Q_{j}$ o $Q_{k}$
#### Execute
Quando l'operando appare nella CDB è letta dalla reservation station, cioè che i tag identificativi siano nulli ($Q_{j}$ e $Q_{k}$ $=$ null), quando gli operando sono disponibili ed inseriti in   $V_{j}$ e $V_{k}$ nella stazione della reservation station allora si eseguono le operazioni sui valori di $V_{j}$ e $V_{k}$. In questo modo i gli hazard reali RAW vengono evitate.

##### Execution Branches
Se c'è un salto non si fa niente con le istruzioni successive e determinare se saltare oppure no

#### Write Result
Quando il risultato dell’istruzione è disponibile, viene immediatamente scritto nel CDB con il formato `TAG Reservation Station, Result`, Tutti i blocchi che attendevano quel Tag salvano il valore e azzerano il campo $Q$ corrispondente. La Stazione di Riserva viene quindi liberata (`Busy = No`). 

### Register File
Ogni elemento in un register file contiene un campo Q_{i}. Questo, contiene il numero della reservation station che contiene l’istruzione il cui risultato dovrebbe essere salvato in un registro. Se il Qi è null, non è attualmente attiva nessuna istruzione che sta calcolando un risultato per quel registro.

In questo modo la hazard detection logic è distribuita e gli stalli per WAW e WAR sono eliminati. Si ha però come contro una alta complessità hardware (includendo un buffer associativo per ogni reservation station) e il CDB potrebbe essere un bottleneck.
## Esempio Tomasulo's 
![[Screenshot 2026-10-23 at 10.33.50.png]]

Partiamo con questa tabella nella quale abbiamo la coda con le istruzioni a sinistra  e i tre stadi dell'algoritmo di Tomasulo:
1. **Issue**: Prende l'istruzione dalla coda della Floating Point, controlla se la resevation station è libera, se lo è allora **incrementa il valore della colonna delle issue**  e manda l'istruzione nella **Reservation Station**.

2. **Execution**: opera sugli operandi di un operazione, cioè **esegue l'operazione dell'istruzione se entrambi gli operandi dell'operazione è disponibile** 