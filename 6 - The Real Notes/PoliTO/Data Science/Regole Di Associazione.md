---
created: 2026-02-14T15:43:00
tags:
  - baby
topics:
  - Data
  - BigData
  - "[[School]]"
  - Data Mining
author: Danilo Quattrini
---
# Regole Di Associazione
---
# Questions
- Che cosa sono le regole di associazione?
- A che cosa servono?
- Quali sono le formule importanti?
- Spiega la legge di Apriori?
 - Spiega come funziona l'algoritmo di Apriori
 - Spiega il funzionamento di FP-growth?
 - Perché FP-growth è meglio di Apriori?
 - Fai un esempio di Apriori
 - Fai un esempoi di FP-growth?
---
>[!quote] Definizione
>Tecnica del Data Science che consiste nell'individuare pattern e correlazione tra i dati di diversa natura all'intero di un database tradizionale.

Le regole di associazione servono a individuare correlazioni e pattern frequenti all'interno di database transazionali (es. gli acquisti in un supermercato, la cosiddetta _Market Basket Analysis_).

Una regola si esprime nella forma:
$$
X \implies Y
$$
Dove preso un'insieme di *item* $I=\{i_{1}, i_{2}, \dots, i_{n}\}$ con $n\in N$ (che possono essere per esempio latte, burro, pasta, ecc), si prende un suo sotto insieme (una porzione / parte dell'insieme degli item ad esempio il pane e il burro) e questo sotto-insieme sarà $X$ e $Y$.

In parole più formali:
$$
X, Y \subseteq I
$$
Abbiamo $X$ ed $Y$ che sono sotto-insiemi di $I$ che nella formula sono chiamati:
- $X$ **Antecedente**: L'insieme o il singolo elemento acquistato o presente
- $Y$ **Conseguente**: l'oggetto a cui associamo $X$

Cioè se un record contiene $X$, allora è probabile che contenga anche $Y$

## Formula Matematica

Nella formula dobbiamo quindi considerare i seguenti elementi:

- $N$: sono il numero delle transizioni / record presenti nel database.
- $count(X)$: conta il **numero delle volte in cui $X$ è presente all'interno del database** con le transizioni
- $count(X \cup Y)$: conta il **numero dell volte in cui sia X che Y siano presenti all'interno del database**:

### Supporto (Support)
Calcola la percentuale di quante volte un'insieme di elementi si presente nel database (insieme di transizioni), cioè in percentuale quante volte un'elemento si ripete.
$$
\text{Supporto}(X \implies Y) = P(X \cap Y) = \frac{\text{count}(X \cup Y)}{N} • 100
$$
>[!info]
>**Significato:** È la percentuale (o frazione) di transazioni totali che contengono sia $X$ che $Y$

### Confidenza (Confidence)
Misura la forza dell'implicazione, cioè la probabilità condizionata che si verifichi $Y$ dato che si è verificato $X$
$$\text{Confidence}(X \implies Y) = P(Y \mid X) = \frac{\text{Supporto}(X \implies Y)}{\text{Supporto}(X)} = \frac{\text{count}(X \cup Y)}{\text{count}(X)}$$
>[!info]
>Tra tutti i record che contengono $X$, qual è la percentuale di quelli che contengono anche $Y$?

Entrambi questi due calcoli devono soddisfare un *minsup* e un *minconf* per far si che siano considerati valori validi per l'analisi. Dove si possono avere due diversi risultati per le regole di associazione.

- **Completo** se e solo se sia il *minsup* che il *minconf* vengono soddisfatti
- **Corretto** se una delle due metriche (threshold) imposti vengono soddisfatti.
### Lift (Incremento)
Misura quanto la presenza di $X$ aumenti la probabilità che si verifichi $Y$, rispetto al caso in cui $X$ e $Y$ fossero del tutto indipendenti.

$$\text{Lift}(X \implies Y) = \frac{\text{Confidenza}(X \implies Y)}{\text{Supporto}(Y)} = \frac{P(X \cap Y)}{P(X) \cdot P(Y)}$$

- $\text{Lift} = 1$: $X$ e $Y$ sono indipendenti (nessuna associazione).
- $\text{Lift} > 1$: Associazione positiva ($X$ invoglia/aumenta l'acquisto di $Y$).
- $\text{Lift} < 1$: Associazione negativa (la presenza di $X$ rende meno probabile $Y$).
## Quale tipo di regola è più interessante?

In generale, le regole con **lift significativamente > 1** sono più interessanti, perché indicano una **vera associazione** oltre la semplice frequenza

Regole con lift ≈ 1 o < 1 possono comunque essere utili se:
- la confidenza è molto alta,
- e l’item Y ha un margine di guadagno elevato.

>[!warning] EXAM
>In esame bisogna sapere come funzionano gli algoritmi di Apriori e FP-growth
## Apriori
Principio di Apriori che dice:
>[!quote] definizione
>Se un Itemset è frequente allora tutti i suoi sotto-insiemi sono frequenti

In questo principio si deve considerare che il **supporto di un itemset non deve superare il supporto dei suoi sotto-insiemi**. Nella definizione vale anche se un itemset è infrequente allora tutti i sotto-insieme di tale itemset saranno infrequenti pure loro.

Questo approccio viene applicato dentro all'algoritmo Arg94 **utilizzando un approccio a livelli**. 

>[!info] Note
>Dato un insieme di $n$ items, ci possono essere ben $2^{n}$ combinazioni possibili, che possono essere rappresentate graficamente in questo modo.
>![[IMG-Regole Di Associazione-20261102.png]]
>Cioè dato l'insieme di items $I=\{A,B,C,D,E\}$ si possono generare ben $2^5=32$ combinazioni differenti.

### Complessità
La complessità di questo algoritmo è la seguente:
$$O(|T|2^{d}w)$$
Dove:
- $T$: numero delle transizioni presenti
- $d$: numero degli item presenti nell'insieme (come nell'esempio sopra sono ben $6$)
- $w$: sono la lunghezza delle transizioni ($1$ per le candidate {$A$, $B$, $C$}, $2$ per le coppie $AB$, $BA$, ecc...)

### Funzionamento
In ogni livello si vengono a generare dei sotto-insieme di una lunghezza che definiamo come per esempio $k$ e si eseguono in due fasi:
1. **Generazione dei Candidati**: cioè si vanno a generare dalla tabella delle transizioni, **quante volte appare il singolo elemento all'interno della tabella di transizioni**
   >[!example] Esempio
   >![[Screenshot 2026-10-27 at 17.59.17.png]]
   >Come vediamo dall'immagine dalla prima tabella che sarebbe il nostro database andremmo a vedere quante volte ogni singola lettera appare all'interno della tabella di desta, in questo caso abbiamo che A appare 7 volte B 8 volte e così via.
   >
   >Sarebbe fare una inner join fra la tabella di sinistra con la tabella di destra contando quante volte  appare una lettera.
   >

La fase descritta precedentemente viene chiamata **join**, che si vanno a creare le transizioni frequenti, la fase successiva si chiama **prune**.

Nella fase di **prune** si vanno ad eliminare le transizioni che non superano un determinato *minsup*, imposto da noi. Prendiamo per esempio come valore di *minsup* > $1$, cioè tutte le transizioni che si ripetono almeno più di una volta.

>[!example]
>Dall'immagine sotto vediamo che la lista degli item che non superano il valore di 1 vengono scartati.
![[IMG-Regole Di Associazione-20261102-1.png]]


Questo tipo di algoritmo può essere molto efficiente quando vogliamo individuare solo gli itemset frequenti di una certa lunghezza $k$ fissa

### Criticità e Miglioramenti
>[!danger] Parte critica computazionale dell'algoritmo
>La generazione dei candidati in un itemset è la parte più critica, inoltre gli scan multipli sul database possono essere problematici in tempi di costi e analisi.

I fattori che comportano una limitazione delle performance dell'algoritmo sono:
-  il valore del *minsup*, che in base alla sua grandezza può:
	- Se **aumenta troveremo solo correlazioni ovvie**, ma non quelle più rare e interessanti
	  
	- **Se diminuisce troveremo troppe correlazion**i e avremo un costo computazionale elevato

-  Il numero di items del dataset

-  Il numero di transazioni nel database

-  La lunghezza media di ogni transazione

Per **limitare il costo computazionale viene utilizzato un [hash-tree](https://en.wikipedia.org/wiki/Merkle_tree)** che consente di limitare i costi di lettura della base dati.

### Altri Algoritmi che migliorano ARG64
- **Yu95**:  Basa la selezione degli itemset frequenti sul conteggio degli itemset presenti nel bucket di hashing per aumentarne la velocità

- Riduce l’impatto dello scan riducendo il numero di transazioni

- **Sav96**: consiste in una soluzione distribuita che lavora su un itemset partizionato

- **Toi96:** conteggio mediante sampling

- **Motw98:** conteggio dinamico

## FP-growth
L'algoritmo **FP-Growth**(Han00) migliora le performance dell'algoritmo Apriori in alcuni parti. Questo perché la base di dati viene utilizzata solamente all'inizio per capire la struttura che possiede i dati, poi **dopo viene salvata nella memoria**. 

Questo perché la memoria è più veloce del disco rigido e si riducono i tempi di esecuzioni delle operazioni, inoltre **si vanno solo a considerare porzioni di memoria che sono di interesse**.

### Funzionamento
L'albero deve essere una porzione dati di interesse, prendiamo una *minsup* $> 1$, facciamo prima l'estrazione degli item per prendere la loro frequenza.
![[Screenshot 2026-10-27 at 18.25.57.png]]Ora andiamo a considerare solo gli item che superano il *minsup* (operazioni di **prune**).

Per ogni item si viene a generare una nuova tabella, chiamata **header table** che contiene l'ordine dei supporti di ogni item in ordine **decrescente dal più grande al più piccolo** (serve per me al fine di non dimenticarmi la differenza tra crescente e decrescente :'>).

Creare una struttura ad albero prefissata, chiamata FP-tree, il cui ordine degli item all'interno delle **transizioni devono rispettare l'ordine della header table**. Si prende ogni transizione e si va ad ordinare la transizione in base alla **header table**![[Screenshot 2026-10-27 at 18.29.31.png]]

Come vediamo sull'immagine viene ordinato in modo che prima ci sia l'item che ha il supporto più grande  fino a quello più piccolo, con affianco il numero delle volte che appare la lettera in ogni transazione.

![[Screenshot 2026-10-27 at 18.31.04.png]]

Nella transazione 2 abbiamo che il valore di B appare ancora, che è in comune per le lettere {C,D}, quindi si andrà ad incrementare il valore di B, questo perché è già presente come nodo-radice della FP-tree quindi lo incremento di 1 e B diventerà 2.

![[Screenshot 2026-10-27 at 18.34.01.png]]

Stessa cosa nella terza transazione, prima ordiniamo le transazioni in base all'ordine della header table, in questo caso A è più grande di {C,D,E},  anche se A e C hanno lo stesso supporto, si ordina in base ad una regola che si decide all'inizio, in questo caso l'ordine alfabetico.

Stessa cosa valgono per le altre transazioni, però vediamo il caso in cui se c'è un valore non frequente nella transazione.

![[Screenshot 2026-10-27 at 18.37.27.png]]

Sopra se avessimo avuto una lettera `H`  che non è frequente, **la transazione non viene esclusa ma si esclude solo l'item non frequente**, infatti nell'albero non viene considerato la lettera `H` 

Il risultato finale sarà un albero del genere, che servirà all'algoritmo di FP-growth per operare sopra, questo albero per verificare la sua correttezza si va a svolgere un operazione chiamata **node link-chain**, che è come si vede nella figura
![[Screenshot 2026-10-27 at 18.42.52.png]]

L'algoritmo funziona che si prende l'ultimo nodo presente nell'albero che si è appena creato, con l'ordine della header table con il supporto più basso (nell'immagine la lettera `E`).

Questo processo lo faccio per l'elemento $i$ ed i suoi precedenti.

Se leggi dall'ultima foglia dell'albero, in questo caso la nostra $i$ sarà il nodo`D`e  leggendo dal basso verso all'alto, quindi (`BAC`, togliendo D sapendo che è presente in tutte le transazioni), si va a creare il **Conditional Pattern Base** dell'elemento $i$ ($i-$CPB).

Questo processo poi comporterà quello di creare un altro albero dagli elementi che si sono presi dal nodo $D$ e si itererà sullo stesso albero.
![[IMG-Regole Di Associazione-20261102-2.png]]

####  Esempio del CPB su DC-CPB
![[IMG-Regole Di Associazione-20261102-3.png]]

Prendiamo i candidati della precedente iterazione e vediamo quante volte si ripetono all'interno delle varie transazioni. Vediamo che partendo da C si possono creare le seguenti transizioni:

| Items | Supporto |
| ----- | -------- |
| {A,B} | 1        |
| {A}   | 1        |
| {B}   | 1        |

Abbiamo create il **Conditional Pattern Base** sull'item `C` dell'albero.

>[!example] Esempio
>Prendiamo queste transizioni
>
>>|**ID Paziente / Transazione**|**Prestazioni Mediche Richieste**|
|---|---|
|**T1**|Elettrocardiogramma, Esami del Sangue, Visita Cardiologica, Ecografia Addominale|
|**T2**|Esami del Sangue, Visita Cardiologica, Risonanza Magnetica|
|**T3**|Elettrocardiogramma, Esami del Sangue, Visita Cardiologica|
|**T4**|Esami del Sangue, Ecografia Addominale, Risonanza Magnetica|
|**T5**|Elettrocardiogramma, Visita Cardiologica, Ecografia Addominale|
|**T6**|Elettrocardiogramma, Esami del Sangue, Visita Cardiologica, Risonanza Magnetica|
>
>Da queste transizioni estraiamo la Header Table che sarà la seguente:
>- VC: Visita Cardiologica
>- ECD: Elettro Cardio Gramma
>- ES: Esami del Sangue
>- RM: Risonanza Magnetica
>- EA: Ecografia Addominale:
>
>|  Items   |   Support  |
| --- | --- |
|   ES  |  5   |
|   VC |   5  |
>|   ECD  |  4   |
>|   RM  |  3  |
>|   EA  |  3   |
>
>*minsup* > 50%, cioè 3 $\geq$ transazioni su 6 devono essere presenti.
>_(Nota: a parità di supporto tra ES e VC, e tra RM e EA, si rispetta l'ordine alfabetico o l'ordine di prima comparsa)._

Per Ordinare le transizioni facciamo in questo modo


| **ID Paziente / Transazione** | **Prestazioni Mediche Richieste** |
| ----------------------------- | --------------------------------- |
| **T1**                        | VC, ES, ECD,  EA                  |
| **T2**                        | VC, ES, RM                        |
| **T3**                        | VC, ES, ECD                       |
| **T4**                        | ES, EA, RM                        |
| **T5**                        | VC, ECD, EA                       |
| **T6**                        | VC, ES, ECD,  RM                  |
>
![[IMG-Regole Di Associazione-20261102-4.png]]

Ora da questo albero andremmo a creare il il CPB di EA, che sarebbe il seguente:

**EA-CPB**:

| Items         | Support |
| ------------- | ------- |
| {VC, ECD}     | 1       |
| {VC, ES, ECD} | 1       |
| {ES, RM}      | 1       |
Rivediamo nuovamente quante volte si ripetono le transizioni dalla tabella principale a questa del E-CPB, cioè facciamo prima la lista dei candidati:

| Item | Support |
| ---- | ------- |
| VC   | 2       |
| ECD  | 2       |
| ES   | 2       |
| RM   | 1       |
Siccome vogliamo un minsup > 50% allora **nessuna delle transizioni sono valide** allora avremmo un albero vuoto e si passa alla seguente, vedendo per le *Risonanze Magnetice* (RM)

**RM-CPB**:

| Items         | Support |
| ------------- | ------- |
| {VC, ES, ECD} | 1       |
| {VC, ES}      | 1       |
| {ES}          | 1       |

Andiamo sempre a generare il supporto per i singoli elementi delle transizioni e vediamo che solo `ES`  supera ha il supporto di 3 elementi:

| Items | Support |
| ----- | ------- |
| ES    | 3       |
| VC    | 2       |
| ECD   | 1       |

### Conclusioni
Se vogliamo item lunghi $k$ usiamo Apriori mentre  FP-growth quando vogliamo specifici itemset che contengono uno o più items.

Per dataset molti sparsi si possono utilizzare altri approcci come la rappresentazione verticale.
![[Screenshot 2026-10-28 at 11.51.18.png]]
**Inverted matrix** (Zak00) rappresenta per ogni item, la lista delle transazioni a cui appartiene.
### Rappresentazione Compatta
![[Screenshot 2026-10-28 at 11.51.38.png]]

Rappresentazione compatta della conoscenza, invece di estrarre tutti gli itemset frequenti, si estraggono i massimali.

### Itemset frequenti massimali e Itemset closed
>[!quote] Definizione di Itemset massimale
>Un itemset è considerato massimale se e solamente se l'itemset che consideriamo massimale **non possiede nessun superset frequente**.

![[Screenshot 2026-10-28 at 11.56.38.png]]

Dall'immagine vediamo che la coppia `AD` e considerato **itemset massimale** perché non esiste un sovra-insieme di `AD`,  ma ci sono (`ABD`, `ACD`, `ADE`)

>[!quote] Itemset closed
>Un itemset è considerato closed, se e solamente se **tutti gli itemset di analisi che consideriamo closed, non possiede nessuno dei suoi itemset adiacienti  superiori(cioè vicini a lui in alto nella gerarchia) che possieda lo stesso supporto.**

![[Screenshot 2026-10-28 at 12.01.34.png]]

Gli itemset massimali discussi prima sono un **sotto-insieme** **degli itemset closed** Essi sono utili per fare delle analisi esplorative quando gli item frequenti sono molto numerosi.
![[Screenshot 2026-10-28 at 12.08.51.png]]

## Lift (Correlazione)
In realtà è stato spiegato prima [[#Lift (Incremento)|qui]], che se vuoi rivedere si trova sopra, dove se si parla della Lift e di come funziona, però vediamo che oltre a quello detto sopra, si **può associare un peso** ad ogni singolo oggetto o ad una transazione se vogliamo considerare oggetti o transazioni più importanti che altre anche nel calcolo della confidenza e del supporto.

Oltre a definire dei pesi si possono definire delle generalizzazioni chiamata **tassonomia**  utilizzando lo stesso **concetto delle gerarchie**. Possiamo quindi avere anche regole cross che contengono in A un oggetto e in B una generalizzazione. In questo caso l’estrazione degli itemset frequenti ci restituisce regole a diverse granularità.