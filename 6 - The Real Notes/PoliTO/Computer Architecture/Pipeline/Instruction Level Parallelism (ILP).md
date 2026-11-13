---
created: 2026-10-16
tags:
  - baby
topics:
  - Architecture 
  - "[[School]]"
author: Danilo Quattrini
---
# Instruction Level Parallelism (ILP)
---
## Questions
### Loop Unrolling
- Che cos'è?
- Come funziona?
- Che cosa serve?
- Che benefici comporta utilizzarlo?
---
## Introduzione
Tutte i processori fin dal 1985 eseguono le istruzioni in parallelo, cioè si avrà una pipeline dove le istruzione sono uno sopra ad un'altra, **questo è utile per far si che si possano migliorare le performance del processore**, come nell'esempio di questa immagine sotto.
![[Pasted image 20261018172251.png]]
Questo sovrapporsi delle istruzioni una sopra ad un'altra viene chiamata *Instruction-Level Parallelism* (ILP). 

Vengono definiti due approcci **principali per sfruttare (exploit) l'ILP**, sono definiti come:
- **Statico**: Quando si viene ad utilizzare software per poter utilizzare il parallelismo a tempo di compilazione in modo statico.

- **Dinamico**: Si utilizza l'hardware per poter trovare e sfruttare il parallelismo dinamicamente.

Il valore della CPI (clock per instruction) in una pipeline è diverso dal calcolo del CPI ideale ed è la seguente formula:
![[Screenshot 2026-10-18 at 17.31.34.png]]
La CPI Pipelined è la somma tra la CPI ideale + gli [[Pipeline#Rischi Di Tipi Strutturali|stalli strutturali]] + stalli dovuti ad un [[Pipeline#Rischio Di Dati|data hazard]] e gli stalli dovuti ad [[Pipeline#Rischi Di Controllo|hazard di controllo]].

Tutte le tecniche che vedremmo in questo capitolo andranno a sfruttare il parallelismo delle istruzioni, ma prima dobbiamo definire il concetto di:
## Basic Block

>[!quote]
>Il **basic block** sono una serie di istruzioni, racchiuse in blocco che hanno la caratteristica di:
>- NON AVERE BRANCH IN ENTRATA eccetto quello che server per entrare nel blocco
>- NON AVERE BRANC IN USCITA eccetto la branch di exit che serve per uscire la blocco
>  ![[Screenshot 2026-10-18 at 17.45.08.png]]

Prendiamo degli esempi di codice:
![[Screenshot 2026-10-18 at 17.46.29.png]]
Per migliorare le performance del programma, si dovrebbe sfruttare l'ILP tra i vari *basic-blocks*(blocchi di codice) ed **il modo migliore è quello di lavorare direttamente nelle iterazione di un loop**.

Prendiamo ad esempio questo codice in C:
```c
for(i = 0; i < 1000; i++)
	v[i] = v[i] + y[i]
```
La cosa importante da sapere è che ogni istruzione eseguita da questo ciclo for **è indipendente da quella precedente o quella successiva**, questa vuole dire che l'istruzione $i_{0}  \not= i_{1}$. Avendo istruzioni che sono diverse tra di loro, **queste si sovrappongono tra di loro sicuramente**

Quindi come si fa ad introdurre il parallelismo tra le istruzioni di un loop?
Ci sono due modi per farlo:
- [[#Loop Unrolling|Loop Unrolling]] che può essere statico dal compilatore o dinamico da una componente hardware
- [[#SIMD|SIMD]] che lavora su un numero di dati in parallelo (2 o 8 dati)
### Loop Unrolling 
Il **Loop Unrolling** (o *"srotolamento"* del ciclo) è una **tecnica di ottimizzazione del codice** che consiste nel **replicare esplicitamente il corpo di un ciclo più volte** all'interno dell'iterazione, riducendo di conseguenza il numero totale di iterazioni da eseguire.

'Il passaggio dal codice standard al codice "unrolled" funziona nel dettaglio e persegue precise finalità hardware.

### Come funziona?
Partendo da un codice in C
```c
for (int i = 0; i < N; i++) {
    body; // Es. array[i] = array[i] * 2;
}
```
Il ciclo esegue la `body` **$N$ volte**. Ad ogni singola iterazione, la CPU deve eseguire il controllo della condizione (`i < N`), l'incremento del contatore (`i++`) e un salto condizionale alla fine del ciclo.

Quando facciamo l'`unroll` del ciclo allora andiamo a **ripetere la body del ciclo** per tante volte quante vogliamo.

```c
for (int i = 0; i < N ; i+=4) {
    body; // Elabora elemento i*4 + 0
    body; // Elabora elemento i*4 + 1
    body; // Elabora elemento i*4 + 2
    body; // Elabora elemento i*4 + 3
}
```

>[!done] Vantaggi
>Utilizzare questo approccio comporta a dei vantaggi:
>- Riduce l'[[New Words#^0dbe8f|overhead]] del loop dovuto ad un controllo maggiore sulle operazioni di loop
>- Il corpo del loop viene ingigantito con più operazioni e quindi per il copilatore è più semplice sfruttare il [[#Rescheduling|re-scheduling]] per eliminare gli stalli

>[!bug] Svantaggio
>Incrementa la dimensione del codice.

### SIMD
**Single Instruction Multiple Datastream** (SIMD), ne è stato parlato anche [[Flynns Taxonomy#SIMD (Single Instruction Multiple Data)|qui]] in precedenza, ma come dice anche il nome significa una singola istruzione viene letta dalla CPU e più flussi di dati, dove vengono inviate le operazioni che deve svolgere.

Ne spiega in dettaglio il libro però quì faremmo solo una spiegazione base.

Quando si parla di **lavorare sul dato in modo scalare**, sarebbe l'approccio classico che fa il nostro compilatore, cioè lavorare su un dato alla volta. Prendiamo per esempio l'operazione precedentemente discussa:
```c
for(i = 0; i < 1000; i++)
    x[i] = x[i] + y[i];
```
Qui si vanno a leggere ogni singolo elemento del vettore `x` e del vettore `y` per ogni iterazione, partendo da `i = 0` fino ad `i = 1000`. In assembly questo si traduce in fare la load del vettore `x` e `y` per 1000 volte, l'operazione di addizione `add` per ben mille volte e la store del risultato per altre mille volte.

L'approccio come vediamo non è uno dei migliori, quindi si è pensato di lavorare su gruppi di dati, cioè invece di prendere un singolo elemento all'interno del vettore `x` e `y` se ne prendono un numero arbitrario, per esempio 4 elementi per ogni vettore: `x[0], x[1], x[2], x[3]` e stessa cosa per il vettore `y`. Questi elementi vengono salvati in **registri di vettori molto grandi** che ci permettono di ridurre il numero delle operazioni da eseguire nel ciclo.

L'affermazione _"l'istruzione opera su un insieme di dati"_ significa che:

- **Una sola istruzione di Load vettoriale** legge in un unico colpo dalla memoria un blocco di dati: `[x[0], x[1], x[2], x[3]]`.
    
- **Una sola istruzione di Add vettoriale** attiva contemporaneamente 4 Sommatori (ALU) hardware separati:
    
    - ALU 0 esegue: `x[0] + y[0]`
        
    - ALU 1 esegue: `x[1] + y[1]`
        
    - ALU 2 esegue: `x[2] + y[2]`
        
    - ALU 3 esegue: `x[3] + y[3]`
        
- **Una sola istruzione di Store vettoriale** scrive l'intero blocco risultante in memoria.

Grazie a questo approccio andremmo a ridurre il numero di iterazioni da eseguire all'interno del ciclo loop, passando da (es. da 1000 iterazioni scalari a sole 250 iterazioni se il vettore elabora 4 dati alla volta), azzerando gran parte dell'[[New Words#^0dbe8f|overhead]] dovuto all'incremento degli indici e ai salti condizionali (`bne`/`jump`).

>[!info] Analogia
>Sarebbe come il Loop-unrolling spiegato in precedenza, solo che viene fatto direttamente dall'hardware e non è un'operazione svolta direttamente dentro al codice.
## Rescheduling
L'operazione di re-scheduling, consiste nel riordinare le istruzioni dentro ad un basic-block, in modo che si possano risparmiare dei cicli di clock, che vengono sprecati da degli stalli inutili.

Prendiamo questo codice in C
```c
a = b + c
d = e - f
```

Lo traduciamo in un codice assembly, in questo modo:
```asm
lw x1,0(x10)
lw x2,0(x11)
add x5,x1,x2
sw x5,0(x14)
lw x3,0(x12)
lw x4,0(x13)
add x6,x3,x4 
sw x6,0(x15)
```
e la pipeline che segue sarà come il compilatore andrà ad eseguire ogni singola istruzione all'interno della pipeline:
![[Screenshot 2026-10-19 at 09.46.02.png]]

Come notiamo abbiamo degli stalli dovuti a degli *hazard di dato*, cioè il valore del registro `x2` non è stato ancora caricato dalla memoria, quindi l'operazione successiva dovrà aspettare che il valore di `x2` sia dentro la memoria, prima di poter operare l'addizione.

Per poter risolvere questo problema si opta per il **re-scheduling**, cioè spostare l'ordine  delle istruzioni all'interno del blocco, in modo da poter evitare gli stalli.

![[Screenshot 2026-10-19 at 09.49.03.png]]

Nell'immagine semplicemente sposta l'operazione di load word (`lw`) del registro `x3` prima di performare l'addizione, questo perché andrà a ritardare l'istruzione `add` nella pipeline, facendo in modo che il registro `x2` abbia il tempo necessario per poter arrivare nella fase di memory (MEM).

![[Screenshot 2026-10-19 at 09.51.06.png]]