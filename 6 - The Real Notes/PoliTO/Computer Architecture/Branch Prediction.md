---
created: 2026-10-20
tags:
  - baby
topics:
author: Danilo Quattrini
---

# Branch Prediction
---
## Questions
- Quali sono le due macro famiglie degli approcci che si utilizzano per predire i branch? [[#^f8b720|risposta]]
- Quali sono le 3 tipologie di soluzioni proposte per un approccio di tipo statico? [[#^3b2701|risposta]]
### Approccio Statico
- Come funziona l'approccio always taken (not taken)?
- Come funziona l'approccio di predire il branch in base al salto?
- Quali sono i due casi di salto che possono avvenire in un branch?
- Qual'è il salto che si preferisce prendere spesso?
### Approccio Dinamico
- Come funziona l'approccio dinamico per predire i branch?
- Quali sono i metodi per l'approccio dinamico?
- Spiegami come funziona la Branch History Table?
- Come posso identificare la riga della branch history table?
- Quale problema si può incorrere in una branch history table?
- Quali sono i due approcci usati per identificare un branch come take oppure no?

## 1-Bit 2-Bit N-Bit
- Come funziona l'approccio del branch prediction ad 1 bit?
- Che downgrade possiede l'approccio ad un solo bit?
- In che cosa consiste l'approccio a 2 bit?
- Come mai è più efficace dell approccio ad un solo bit?
- Come si fa a capire che un branch è taken oppure no in un approccio a 2-bit?
- Come funziona l'approccio ad N-bit? Che condizione si deve verificare affinché un branch viene considerato taken oppure no?

---
## Introduzione
I branch possono impattare le performance della pipeline, però ci sono dei modi che si 
possono usare per poter predire i salti.

Ci sono due gruppi  ^f8b720
- **Statici**: gestiti nel compilatore riordinati prima di un analisi dal compilatore
- **Dinamici**: gestiti direttamente dall'hardware

## Statici
Sono utili quando si vanno a combinare con altre tecniche statiche come il **branch delay** e il [[Instruction Level Parallelism (ILP)#Rescheduling|rescheduling]] per evitare gli hazard.

Ci sono predizioni del tipo: ^3b2701
- **Always taken** (not Taken too):  cioè dire che i branch vengono sempre presi (o no presi) di default
- **Predire il comportamento del branch** in base alla direzione
- **Predire in base alle informazioni di profilazione**, cioè ai comportamenti del branch che ha avuto nelle precedenti iterazioni.

### Predire il branch sempre preso
Non usare tale tecnica, perché possiede una percentuale di mis-prediction che è sopra al 34% (dopo vediamo cosa sono le percentuali di mis-prediction).

Questo approccio comporta che l'istruzione successiva viene sempre presa o non presa anche quando la branch fa l'opposto della predizione, si va a perdere un colpo di clock perché la **pipeline dovrà svuotare le istruzioni caricate per errore (_flush_) pagando la penalità del branch**.

### Predire in base alla direzione del salto
In questa tecnica ci si basa sull'osservare che:
- **I branch in forward sono molto spesso non presi**
- **I branch in backward sono spesso presi**

Il comportamento dipende molto dalla struttura del loop, e dall'indirizzo di destinazione della branch, quindi avremmo due tipi di jump:

- **Jump forward**: l'indirizzo di destinazione della **jump è più grande della** **PC** (Program Counter della branch) $\text{Target} > \text{PC}$, quindi è come se facesse nel codice sorgente corrisponde a saltare istruzioni posizionate più in basso (es. i blocchi `if-else`)
  
- **Jump Backward**: se **l'indirizzo di destinazione è più piccolo della PC**, questo spesso succede nei cicli loop, quando il branch deve saltare all'istruzione precedente per poter ricominciare il ciclo loop.

**Viene predisposto più un approccio backward che forward**, questo perché il primo approccio è quello che possiede un miss-rate molto basso, dato che in un ciclo loop l'operazione si ripete per quante volte si deve soddisfare la condizione.

### Predire i salti in base alla profilazione
Invece di usare una regola rigida sull'hardware per tutti i branch, questa tecnica sfrutta le informazioni di **profilazione del programma raccolte dal compilatore durante esecuzioni di prova**:

1. Il compilatore analizza le esecuzioni passate del programma per identificare quali branch tendono a essere presi più spesso.
    
2. Il compilatore inserisce un **hint (bit di suggerimento)** all'interno della codifica dell'istruzione di branch stessa (o dispone il codice per favorire la predizione predefinita dell'hardware).
    
3. Durante l'esecuzione, l'unità di predizione statica legge questo suggerimento incorporato nell'istruzione e decide se predire **Taken** o **Not Taken** rispettando il profilo storico calcolato dal compilatore.
## Predizione Dinamica 
La ==predizione dei salti dinamica avviene tramite l'utilizzo di hardware== e l'utilizzo dell'indirizzo delle istruzione per poter attivare diversi meccanismi di predizione. La predizione dinamica dei branch può avvenire secondo diverse tecniche:
- [[#Branch History Table|Branch History Table]]
	- Schema di predizione [[#One-bit prediction schema|ad uno]] o [[#Two-bit Prediction Schema|due bit]].
- [[#Predizioni a due livelli (two-level predictor)]]
### Branch History Table
La Branch History Table (BHT) è una tabella della storia dei salti che si sono presi, serve a predire se un salto sarà **Taken** oppure **Not-Taken**.  La predizione viene salvata nella tabella utilizzata, e il nuovo program counter viene calcolato in accordo a tale predizione. Quando il risultato di un branch è noto, la tabella viene aggiornata.
![[Screenshot 2026-10-20 at 08.59.41.png]]
Per prendere l'elemento della tabella bisogna prendere la **parte più bassa della indirizzo dell'istruzione branch**, che sull'immagine sopra viene indicato con la lettera **T** (escludendo l'offset che viene rappresentato dalla lettera $d$ nella figura).

Tali bit servono **per trovare la riga giusta all'interno della tabella**, questo tramite la formula:
$$\log_{2}(N)$$
La formula ci aiuta a trovare la riga che svolge la predizione, ma l'**operazione di predizione la fa direttamente il contenuto della riga** (cioè la word)

Quindi il funzionamento della riga avviene in questo modo:
- **Genera il segnale di predizione (Taken / Not Taken):** Un multiplexer (`N to 1 Mux logic`), guidato dagli stessi bit d'indice $T$, seleziona la parola di storia indicata e la converte nel segnale **Taken** o **Not Taken**.
    
- **Aggiorna lo stato (BHT Control):** Quando la fase di _Execute_ del processore stabilisce la reale condizione del branch, la linea di controllo (`BHT control`) riscrive la riga aggiornando i bit di storia in base al risultato reale.

#### Problemi della branch history table
La tecnica è efficace, ma soffre di un problema chiamatosi **aliasing**, cioè vuol dire che una linea della tabella potrebbe far riferimento ad un altro salto invece di quello che sto eseguendo, ma l'efficacia dipende anche dall'accuratezza.

>[!warning] Come mai questo problema?
>Tale problema è dovuto dal fatto che **non esistono dei tag che riescano ad identificare istruzioni branch differenti**.
#### One-bit prediction schema
In una predizione a un bit si avrà solamente due bit che decideranno se il branch è in stato di **Taken** con valore di `1` e con `0` invece lo stato di **Not-Taken**.

>[!danger] Problema
>Il problema che si presenta in questo approccio è il fatto che in un ciclo loop si andrà sempre a svolgere due predizioni sbagliate, una in entrata ed un altra in uscita.
#### Two-bit Prediction Schema
![[Screenshot 2026-10-20 at 09.07.03.png]]

Lo schema a due bit permette di avere una predizione più elevata, questo mantenendo due bit nella branch history table, la **predizione cambia dopo due miss o due take**.

In questo esempio sopra abbiamo che se i bit sono `10` oppure `11` allora il branch viene identificato come **Taken**, nei casi di `01` ed `00` invece sono considerati **Not-Taken**.

>[!info] Benefici
>In questo modo a differenza dell'approccio ad 1 bit, in questo caso se abbiamo considerato un brach **Not-Taken**, c'è bisogno di ben 2 stati prima che il branch sia considerato **Take**, cioè lo stato 00 e poi dopo lo stato 01 e se di nuovo è taken allora passa ad 10 e sarà quindi **Taken**.

#### N-bit Schema
Il contatore predittivo a n-bit è una generalizzazione dello schema precedente. Si ha un **vero e proprio contatore**,  questo contatore aumenta se il branch viene preso, altrimenti decrementa.

>[!info]
>Il branch viene considerato taken, se e solamente se il valore del contatore è >= della metà della sua dimensione in n-bit.

Questa tecnica viene definita anche come **bi-modal**
![[Screenshot 2026-10-20 at 09.13.15.png]]

>[!done]
>Le performance dei branch vengono impattate da alcuni fattori:
>- accuratezza della precisione
>- costo del branch (penalità per predizione errata)
>- branch frequency (minore per programmi in floating point)

### Predizioni a due livelli (two-level predictor)
In questo approccio si va a vedere il risultato del salto precedente, dal salto che sto valutando, per valutare se si dovrà saltare oppure no. 

>[!example] Esempio
>```c
>if (aa==2) aa=0; // branch 1
>if(bb==2) bb=0; // branch 2
> if(aa!==bb){} // branch 3
>```
>Il comportamento dell'ultimo `if` è fortemente dipendente dal risultato delle due precedenti `if`
>Se il Branch 1 è **Taken** (aa diventa 0) e il Branch 2 è **Taken** (bb diventa 0), allora sappiamo con certezza matematica che `aa` e `bb` sono entrambi 0. Di conseguenza, la condizione del Branch 3 (`0 != 0`) sarà falsa, quindi sarà sicuramente **Not Taken**. Un predittore a due livelli "impara" questo schema: _se gli ultimi due salti sono stati presi, il prossimo non lo sarà_.

### (m, n) Prediction
Si vanno ad utilizzare gli $m$ branch precedenti (cioè il numero dei branch precedenti alla condizione che vogliamo valutare come taken o no) per poter scegliere ben **$2^m$ branch predictors,** ciascuno ad *n-bit*, L’hardware necessario per implementare lo schema è molto semplice:
- La storia dei più recenti $m$ branches è registrato in uno shift register ad $m$‑bit, dove ciascun bit registra se un salto è stato preso o meno (`1` salto preso, `0` salto non preso).

- Il branch prediction buffer è indicizzato utilizzando una concatenazione di bit low order del branch address con $m$ low order history bits.

#### (2, 2) Predictor
![[Screenshot 2026-10-20 at 09.26.18.png]]

>[!example] Esempio
Prendiamo come esempio $m = 2$ e $n = 2$, dove avremmo ben 2 bit per il predittore e $2^2 = 4$ **branch predictors** (che sono le colonne dell'immagine) Per ogni salto ho 4 possibilità cioè $2^2$ "storie" passate (`00, 01, 10, 11`). Ogni singola istruzione di branch ora avrà ben 4 stati in cui passare

#### Esempio pratico
![[Screenshot 2026-10-20 at 09.26.18 copy.png]]
Partiamo sempre dalla base di $m=2$  branch precedenti che vogliamo analizzare e i $2^{2}=4$ branch predictors.

1. Si parte prendendo la storia del branch che per semplificare diremmo sarà `01` come nell'immagine Questo valore di storia (`01`) agisce come un selettore (o un indice di colonna). Dirige l'attenzione del processore su **una specifica colonna** tra le 4 disponibili nella tabella. Graficamente, è la freccia che sale dal registro a 2 bit e punta alla base delle colonne per selezionarne una
   
2. **Lettura dell'Indirizzo:** Contemporaneamente, il processore prende i bit meno significativi dell'indirizzo dell'istruzione di branch corrente (`Branch address` che si trova in alto).

	- Dato che ci sono 16 righe, il processore userà $\log_2(16) = \mathbf{4 \text{ bit}}$ dell'indirizzo del branch per selezionare la riga corretta. Graficamente, questo è rappresentato dalla linea "Branch address" con il taglietto "4" che punta lateralmente verso le righe. 
	  
3. **Predizione Finale (L'Incrocio):** All'intersezione tra la riga selezionata dai 4 bit dell'indirizzo e la colonna selezionata dalla storia a 2 bit, il processore trova la cella `XX`. Estrae i 2 bit contenuti in quella cella e li usa per emettere la `XX prediction` (Taken o Not Taken).
## Branch Target Buffer
Il **Branch Target Buffer** è una memoria cache che serve per salvare l'istruzione di salto che è stata presa in precedenza dal processore onde di evitare nuovamente di richiamare la memoria per indicare in quale indirizzo di memoria saltare.


In questo approccio si salva l'indirizzo dell'istruzione di salto, con l'obbiettivo di identificare l'istruzione di salto nella fetch invece che nella fase di decodifica. Salvo anche l'indirizzo dell'**istruzione target**, che verrà poi dopo caricato nel **program counter**.
![[Screenshot 2026-10-20 at 09.37.05.png]]

>[!info] Componenti della Branch Target Buffer
>Sono ben due componenti che possiede la branch target buffer:
>1. L'indirizzo dell'istruzione branch (address)
>2. Target: cioè il branch in cui dovrà saltare

>[!example] Esempio
>1. La CPU sta facendo la fase di **Fetch** all'indirizzo `0x1008`.
>2. Nello stesso istante, controlla nel BTB: _"Ho già visto l'indirizzo 0x1008?"_.
>3. **Hit (Trovato):** Il BTB risponde _"Sì, è un branch, e la volta scorsa è saltato all'indirizzo 0x2000!"_.
>4. Se il predittore (es. la BHT) dice che il salto sarà **Taken**, la CPU non aspetta la fase di Decode o Execute. Nel ciclo di clock immediatamente successivo, imposta il Program Counter a `0x2000` e inizia a caricare le istruzioni giuste senza perdere nemmeno un istante.
### G-select
Predittore correlato

==(da recuperare che non ho seguito)==

## Esercizii
### BHT con 2 bit 
Prendiamo una saturazione a 2-bit con un count BHT di 1K entries e assumiamo che il processore esegue il seguente codice:
```c
for(i = 1; i <= 100; i++){
	read_data();
	if(aa == 2)
		aa = 0;
	if(bb == 2)
		bb = 0
	if(aa == bb)
	{}
}
```
Determinare lo stato finale della BHT e calcolare il mis-prediction ratio del presente caso.
Convertiamo il codice sopra in RISC-V
```
L0: 
	addi x3, x1, -2
	bnez x3, L1 
	add x1, x0, x0 

L1: 
	addi x3, x2, -2 
	bnez x3, L2 
	add x2, x0, x0

L2:
	sub x3, x1, x2
	bnez x3, L3

L3:
	addi x4, x4, -1
	bnez x4, L0
```

Prendiamo il caso 1 dove avremmo `aa` e `bb` che siano sempre diversi da 2, l'esempio sotto abbiamo `aa = 4`, come nella tabella qui sotto:
![[Screenshot 2026-10-20 at 10.43.10.png]]

La predizione alla prima iterazione sono **NT** (Not Taken), nella prima è sempre così (se abbiamo valori che siano diversi dalla condizione) per ora sono Not Taken perché in questo caso non sono stati incrementati da 0 ad 1, la prima condizione l'ho sbagliata  quindi l'aggiungo alla colonna delle **misP.counter**
![[Screenshot 2026-10-20 at 10.48.33.png]]

Dopo le seguenti iterazioni vediamo che il valore di BHT incrementano per le volte che prendo i salti, mentre le miss le incremento quando non si prendono i salti, quando quindi abbiamo i BHT **che superano la dimensione dei bit (che in queso caso sono 2-bit) allora la prediction diventa Taken**.
![[Screenshot 2026-10-20 at 10.51.40.png]]

Dopo le 100 iterazioni però succede che l'ultimo salto non sarà lo stesso valore di prima, questo perché l'ultimo salto, che indica l'indice del loop, non verrà preso il salto, allora vuol dire che abbiamo fatto una predizione sbagliata quindi dobbiamo incrementa la colonna delle **miss prediction counter** e decrementare la colonna della BHT perché il salto non viene preso.
![[Screenshot 2026-10-20 at 10.55.28.png]]

Ora per calcolare la miss prediction rate si usa la formula:
$$Misspredition \ ratio = \frac {n}{b_{tot}} * 100$$
Dove abbiamo:
$n$ = somma di tutte le miss prediction value nella colonna della tabella
$b_{tot}$ = il numero totale dei branch

Avremmo quindi che ci sono $9$ **miss prediction value in totale** e il numero dei branch che in questo caso sono dentro ad un ciclo che si ripete ben $100$ volte saranno ben il numero dei branch nel ciclo per il numero di volte che si ripete, quindi $4 *100$.

Allora avremmo che:
$$Misspredition \ ratio= \frac{9}{400} = 0,00225 * 100 = 2,25\%$$
Avremmo quindi un miss prediction ratio sarà del $2,25\%$

### (2,2) Example DA VEDERE
==(da vedere esempio come funziona con un predittore (n,m))==