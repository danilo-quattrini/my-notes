---
created: 2026-10-28
tags:
  - baby
topics:
  - Data
  - AI
  - Data Mining
author: Danilo Quattrini
---
# Classificazione
---
# Questions
- Che cos'è la classificazione?
- Come funziona?
- Come si valutano le performance di un algoritmo di classificazione?
- Quali sono gli algoritmi di classificazione?

## Alberi decisionali
- Che cosa sono gli alberi decisionali
- Come funzionano con un dataset?
---
# Introduzione
Il processo di classificazione viene inteso come l'operazione di predire ed assegnare un **etichetta** (su un insieme di etichette definite precedentemente) a degli oggetti o dati, tramite l'utilizzo di modelli interpretabili utilizzando un approccio [[Supervised And Unsupervised#Supervised (Apprendimento Supervisionato)|supervised]].

I modelli interpretabili sono generati e validati in due fasi:
1. Si fornisce un dataset con l'associazione tra etichette e dati già presenti, che verrà utilizzato come base da dare in pasto al modello per apprendere a che dato o valore l'etichetta è associato

2. Il modello poi viene testato, cioè dato un dataset in input, il modello legge i dati del dataset e si vede se svolge l'associazione etichetta -> dato nel modo corretto oppure no, per vedere le suo reale capacità
![[Screenshot 2026-10-28 at 12.29.22.png]]
I dataset di training devono essere arricchiti con dati che siano etichettati in modo da far si che il modello riuscirà in modo autonomo a classificare i dati
## Parametri per valutare l'algoritmo di classificazione
Per poter valutare un algoritmo di classificazione si vengono ad utilizzare queste 6 metriche:

- **Accuratezza (Performance)**: cioè se il modello svolge le predizioni nel modo giusto oppure no

- **Interpretabile**: cioè il risultato generato dal modello sia coerente con il contesto e sia chiaro e comprensibile, cioè come l'umano riesca a capire l'algoritmo usato dal modello per classificare.

- **Incrementabilità**: il modello deve crescere quando riceverà dei nuovi valori/etichette nel dataset usato per il training

- **Efficienza**: le tempistiche che ci si impiegano per creare il modello e le operazioni di svolgere la classificazione.

- **Scalabilità**: cioè la capacità del modello di supportare una grande quantità di dati nel dataset.

- **Robustezza**: la capacità del modello di poter operare nel modo corretto anche in presenza degli outliers o il rumore presente nei dati.

# Tecniche della Classificazione
- [[#Albero Decisionale|Albero Decisionale]]
- Regole di Classificazione
- Regole di Associazione
- Reti Neurali
- k-Nearest Neighbors (k-NN)
- Support Vector Machines (SVM)

## Albero Decisionale
>[!info] Definizione
>L'**albero decisionale** è un struttura che serve per associare delle etichette di classe ai dati in base a delle condizioni che sono presenti nei nodi, condizioni che sono valutate in base al valore dei dati che vengono forniti al nodo.

![[Screenshot 2026-10-29 at 10.28.19.png]]

Sopra abbiamo un dataset di 5 colonne, dove c'è `TransactionID`, poi c'è il `Refund` attributo categorico che può assumere valori `Yes` o `No`, stessa cosa per lo stato matrimoniale `Marital Status` attributo categorico, attributo continuo `Taxable Income` che indicano le tasse che pagano.

Bisogna **tramite questi attributi identificare quali condizioni bisogna soddisfare per arrivare a dei nodi specifici**.

>[!example] Esempio
>Nell'immagine sopra abbiamo come radice dell'albero abbiamo come attributo `Refound`, può assumere valore `Yes` o `No`, dobbiamo leggere la tabella di sinistra e vedere se quando `Refound` è `Yes` allora abbiamo l'attributo `Cheat` che sarà `No`, mentre se `Refound` è `No` allora la `Cheat` sarà in parte `Yes` ed in parte `No`. In questo caso è importante scegliere un attributo di split che possa raffinare il partizionamento, che in questo caso sarà l'attributo `Marital Status`

Si possono generare più alberi, che si può scegliere il miglior albero che è più idoneo in base al dataset di training.

### Applicare il modello in dataset di test
![[Screenshot 2026-10-29 at 10.42.08.png]]

Guardo ogni nodo e vedo se rispettano le condizioni del dataset che ho. Se alla fine rispetta quello che ho nel dataset allora l'albero è giusto

### Algoritmi per generare gli alberi di Decisione

#### Algoritmo di Hunt
L'**algoritmo di Hunt** è uno dei primi algoritmi utilizzati per la creazione di alberi decisionali dall'intero dataset.

>[!question] Come funziona?
 Si fa prendendo un insieme di record $D_{t}$  di un dataset (cioè i 10 record della tabella della training data) che in un preciso momento raggiungono un determinato nodo $t$. Poi abbiamo la condizione $A$  che viene applicata nel nodo per divider il nodo in sotto-insiemi  più piccoli.
 ![[IMG-Classificazione-20261105.png]]

- Se $D_{t}$ contiene record appartenenti a più di una classe selezioniamo l’attributo $A$ migliore per lo split e nominiamo il nodo 𝑡 con $A$, in seguito dividiamo 𝐷𝑡 in subset più piccoli e applichiamo ricorsivamente questa procedura.

- Se 𝐷𝑡 contiene record che appartengono alla stessa classe $y_{t}$ allora 𝑡 diventa un nodo foglia etichettato con $y_{t}$.

-  Se 𝐷𝑡 è vuoto allora 𝑡 è un nodo foglia etichettato con la classe di maggioranza $y_{d}$
##### Esempio pratico Hunt
![[IMG-Classificazione-20261105-1.png]]

#### Scelta della struttura della condizione di test
La scelta della struttura del test va in base al tipo di attributo che abbiamo, che può essere:
- **Nominale**: si può creare un ramo per ogni valor distinto chiamato **split multiplo** oppure si possono creare dei sotto-insieme dei valori in partizionamento ottimale, con uno **split-binario**
  
  Esempio di uno **split binario**![[Screenshot 2026-10-29 at 10.58.23.png]]
  
  Esempio **split multiplo**![[Screenshot 2026-10-29 at 10.59.23.png]]

- **Ordinale**: lo stesso di quello nominale solo che i valori del sotto-insieme in un binario devono essere sempre continui.
  
- **Continuii**: si possono svolgere in due modi, che possono essere:
	- **Discretizzazione**: 
	- **Decisione Binaria**
	  
	  Esempio di discretizzazione e decisione binaria![[Screenshot 2026-10-29 at 11.04.34.png]]

### Selezionare l'attributo migliore per lo split
Per selezionare l'attributo serve sceglierlo uno che possegga delle classi **omogenea**, per far cioè serve calcolare la **purezza** dell'attributi e possiamo farlo in diversi modi:
- **GINI Index**: che sono valori che vanno da 0 ad 1.
  
- Entropy (valori da 0 a $\log_{2}n_{c}$ con $n_{c}$ numero delle classi): la computazione è simile a quella del GINI.
  
- Information gain: misura la riduzione dell’entropia data dallo split. Tende a dare maggiore importanza a split formati da molti gruppi piccoli e puri

- **GainRatio**: aggiustamento dell’information gain per penalizzare gli split multipli e piccoli.

- Misclassification error

Verifichiamo sperimentalmente quale sono le metriche migliori per il nostro dataset.

Si mostra un esempio di come una metrica che viene scelta, si possa valutare quale sia il migliore split.

## Formula di GINI Index
La formula di GINI index serve per calcolare quanto un insieme di dati in un dataset sia diverso tra di loro, serve per **calcolare la divesità** dei dati in un dataset
![[Screenshot 2026-10-29 at 13.08.33.png]]

Prendiamo questa immagine come esempio e vediamo che sul dataset di sinistra abbiamo meno diversità dei dati, questo perché ci sono meno elementi differenti tra di loro.
### Overfitting vs Underfitting
![[Screenshot 2026-10-29 at 11.21.02.png]]

All'aumentare la dimensione dell'albero posso rischiare problematiche di tipo **overfitting**, dove si ha un livello di dettaglio dell'albero (intesa come numero dei nodi presenti) molto elevata, questo è causa principali di errori.

Mentre se ci sono pochi nodi nell'albero si parla di **underfitting**, cioè se la gerarchia è così semplice che non va a specificare abbastanza.

Si possono trovare delle problematiche dovute alla **mancanza dei nodi** nell'albero decisionale:
- Influenzano il calcolo dell'impurità. Le performance dell'albero decisionale tendono a peggiorare.
![[IMG-Classificazione-20261104.png]]

## Valutazione Dell'albero Decisionale

# Random Forest
Si utilizzano una foresta di alberi (cioè diversi alberi decisionale) per svolgere una decisione, che si prendono diversi alberi di decisione, cioè n algoritmi in parallelo che eseguono questo algoritmo si chiama **Random Forest**.  C'è anche una tecnica di learning chiamata ***Ensemble***, che aumenta l'accuratezza e la stabilità dell'algoritmo andando ad evitare l'**overfitting**.

## Funzionamento
Vengono generati n modelli in parallelo, dove ogni modello possiede un etichetta di classe.
![[IMG-Classificazione-20261104-1.png]]

Si vengono come si vede dall'immagine diversi alberi decisionali definiti come $D$, dove però ogni $D$ vanno a definire delle etichette nella quale vanno a valutare i record del dataset. Il criterio di assegnamento della classe di un record avviene tramite  **majority voting**, cioè se più alberi decisionali votano che un determinato record sia $A$ invece che $B$ allora sarà $A$.

Si prende un **dataset**, nella quale si va a **creare dei sotto-gruppi randomici**, dove i record vengono assegnati per rimpiazzamento, per il quale viene selezionato anche un subset di attributi random (solitamente se 𝑝 è il numero di attributi vengono selezionati √𝑝 attributi) e viene generato per ognuno dei subset un albero. Gli alberi ottenuti sono completamente decorrelati. La classe viene assegnata per maggioranza fra tutte le predizioni dei diversi alberi.

## Valutazione
Valutazione del random forest:

-  **Accuratezza**: maggiore rispetto agli alberi decisionali

-  **Interpretabilità**: l’interpretabilià diminuisce all’aumentare del numero di alberi, ma permette di capire l’importanza delle feautures rispetto a tutte le altre

-  **Incrementalità**: non è incrementale

-  **Efficienza**: risulta più veloce rispetto agli alberi decisionali perché una volta selezionati i subset le operazioni di costruzione degli alberi e di classificazione saranno più veloci perché eseguibili contemporaneamente

-  **Scalabilità**: è scalabile in quanto gli alberi vengono creati su una porzione di dati

-  **Robustezza**: è robusto rispetto a rumore e outliers perché abbiamo modelli diversi che lavorano in contemporanea e lavora meglio in presenza di missing values

# Rule Base Classification (Regole di classificazione)
>[!info]
>La ***Rule Based Classification*** è un approccio / algoritmo di classificazione nella quale si definisce una specifica condizione, che un record deve soddisfare se fa parte di una determinata classe / etichetta.
>$$(Condition)\to y$$
>- $Condition$: congiunzione o semplice predicato
>- $y$: l'etichetta che andiamo a dare alla classe.

Dove si ha la condizione che sono un insieme di regole, mentre la $y$ è l'etichetta di classe che viene assegnata se la condizione viene soddisfatta. Ci sono degli algoritmi che presi in input un dataset, con dati strutturati, da questi dati riescono ad estrapolare le condizioni che si possono applicare.

![[IMG-Classificazione-20261104-2.png]]
Vediamo l'immagine sopra, dove c'è la condizione `R1`, che se `(Given Birth = no) AND (Can Fly = yes)`  allora lo associamo all'animale  `Bird`.

>[!info] Definizione
>Una **regola copre un record**, se e solamente se il record soddisfa la condizione della regola

Una determinata condizione può **triggerare** / **inizializzare**, diverse regole, cioè quando un determinato record di una tabella soddisfa più regole / condizioni, queste possono attivare più etichette di classe.
![[IMG-Classificazione-20261105-2.png]]

Nell'immagine sopra abbiamo che tartaruga attiva la condizione `R4` e `R5`, perché nella tabella ci sono tutte e tre le condizioni che fanno avverare la regola. 

>[!info] N.B
>Se **NESSUNA DELLE REGOLE DI VENGONO SODDISFATTE** da un determinato record di un dataset, si deve prevedere un attributo di default.

Ci sono però delle condizioni ideali che sono:
1. **Mutualmente Esclusive**: cioè definite due specifiche condizioni, queste non possono essere entrambe vere, **ogni record deve essere coperto da almeno una regola**.
   $$(Condizione_{1})\to y_{1} \not= (Condizione_{2})\to y_{2}$$
2. **Esaustive**: le condizioni devono soddisfare tutte le combinazioni dei valori degli attributi presenti nei record ed **ogni record deve coprire almeno una regola**

Si possono anche estrarre delle regole dagli alberi decisionali, questo tramite i valori dei nodi che sono delle singole regole specifiche per ogni specifico record, **in questo caso saremmo sempre nel caso ideale**.
![[IMG-Classificazione-20261105-3.png]]

 Se l'albero invece proviene da un operazione di pruning, questo **non definirà delle condizioni ideali**. Questo perché se volessimo ridurre il livello di dettaglio dell'albero ed evitare di andare in [[#Overfitting vs Underfitting|overfitting]] dobbiamo svolgere un operazione di pruning sull'albero.
![[IMG-Classificazione-20261105-4.png]]
Nell'immagine si vede che dalla regola `(Refound = NO And Status = Married) -> No` si è passati direttamente ad `(Status = Married) -> No`. 

>[!warning] Attenzione
>- Questa semplificazione  **deteriora la muta esclusività delle regole** (nella quale un record può triggerare più condizioni) e per risolvere a tale problema si definisce un ordinamento. 
>- **Regole non più esaustive**, cioè un record del dataset non soddisfa nessuna delle regole che abbiamo definito, quindi si deve **definire un etichetta di default**.
## Definire le regole
Le regole delle condizioni si possono estrarre in due modi, che sono:
- **Diretto**: tramite un algoritmo specifico che definisce le regole che si sono estratte dai dati del dataset (algoritmi RIPPER, CN2, Holet's).

- **Indiretto**: Si estraggono le regole tramite altri algoritmi di classificazione (come abbiamo fatto prima con l'albero decisionale)

## Valutazione

- **Accuratezza**: performa meglio dell'albero decisionale (se non si utilizzano metodi di creazioni delle regole indiretti)

- **Interpretabile**: modello interpretabile e di facile comprensione (sono solo delle condizioni grazie al cabbo)

- **Incrementale**: non è incrementale, questo perché quando ci sono nuovi dati che  entrano nel dataset, l'algoritmo deve essere ri-allenato

- **Efficienza:** Crea modelli molto velocemente e svolge classificazioni in modo immediato.

- **Scalabilità**: sono scalabili per il numero degli attributi del training set e la dimensione.

- **Robusto**: Resiste agli outliers.

# K-Nearest Neighbor
>[!info] Definizione
>L'algoritmo di *k-nearest neighbor* KNN utilizza un dataset di training per svolgere una decisione, senza dover utilizzare un modello predittivo. Cioè un classificatore che si basa sulle istanze.

![[IMG-Classificazione-20261105-5.png]]
 
Si prende un dataset che contiene già delle classificazioni fatti in precedenza, quando un nuovo dato (record di un dataset) deve essere classificato, questo si confronterà con il dataset che è presente alla sinistra e **vede quali sono gli attributi che sono in comune**, cioè le caratteristiche che sono in comune tra l'**unseen case record** e il **set of stored cases**
## Classificatori utilizzati
- **Rote-learner** (si utilizzava una volta ora non più): dove si memorizza l'intero dataset e poi faceva il matching se il nuovo record  era esattamente uguale a quello presente nel dataset.
  
- **Nearest neighbor**: usa i $k$ punti che sono più vicini al record che si vuole classificare per definire la classificazione.

![[IMG-Classificazione-20261104-3.png]]

Quando si vuole classificare un oggetto, si vanno a considerare i *k* oggetti che si vogliono utilizzare per la classificazione, che sono vicini all'oggetto che vogliamo classificare. **Per classificare bisogna prima dover normalizzare** i dati in modo da far si che ci siano lo stesso 
peso. 

Dopo aver normalizzato i dati si utilizzano delle distanze, per identificare la [[Similarità e Dissimilarità|similarità]] tra l'oggetto che sto analizzando con il vicino.

Come si vede nell'immagine si possono scegliere 1, 2 o 3 vicini al valore che vogliamo classificare e **dare un'etichetta in base al tipo di classe che possiede il vicino**.

## Come si sceglie *k*?
Per scegliere il valore di *k* si svolgono una serie di tentavi in modo che si possa scegliere un valore che:
- Se **troppo grande**, allora si vanno ad analizzare anche le classe dei vicini dei vicini, andando a prendere una classe sbagliata, creando quindi dei valori sbagliati.
  
- Se **troppo piccolo**: abbiamo una alta sensitività al rumore.

Bisogna scegliere dei valori medii che possono essere 5 o 7 a seconda della casistica e dell'ipotesi

>[!warning] Problemi con le misure sulle distanze
>Con la metrica della distanza, sui dati normalizzati, può subire un problema chiamato **cur
se of dimensionality**, cioè con l'aumentare del numero delle dimensioni, le distribuzioni tendono ad essere sparse. 

Come tecnica di pre-processing si può applicare la **riduzione dimensionale** per risolvere a questo problema.

## Valutazione

Valutazione del random forest:

-  **Accuratezza**: comparabile con le altre tecniche di classificazione.

-  **Interpretabilità**: **modello non interpretabile**, la spiegazione è difficile non è facile se non descrivendo che la predizione avviene in base alle caratteristiche dei vicini.

-  **Incrementalità**: ovvio perché ci sono sempre dei nuovi dati che servono per il training

-  **Efficienza**: non esistono tempi di generazione del modello, ma **aumento i tempi di di classificazione molto maggiori rispetto agli altri modelli**.

-  **Scalabilità**: poco scalabilità

-  **Robustezza**: dipende dalla metrica scelta.

# Classificazione Bayesiana
>[!info] Teorema
>Modello statistico dove si prendono due variabili $X$ e $C$ e si vuole calcolare la probabilità che $X$ andrà a far assegnare l'etichetta di class $C$.

Qui si applica una semplificazione che viene chiamata *Naive Bayesian*, come abbiamo visto dal teorema abbiamo:

- $C$: etichetta di class

- $X$ $<x_{1},\dots,x_{k}>$:  record da classificare o i record del dataset di training.

Per applicare Bayesian bisogna **applicare l'ipotesi che i record i un dataset sono  considerati diversi**, in modo tale da dire che la probabilità di $X$ di calcolare $C$, la possiamo calcolare come il prodotto di tutte le probabilità che caratterizzano $C$.

Cioè si prende ogni singola variabile di $X$ e si calcola la probabilità di quanto ogni singola variable $x_{1},\dots,x_{k}$ sia probabile di appartenere alla determinata classe $C$, si calcola il teorema di **Bayes**:
$$P(C|X)=\frac{P(X|C) * P(C)}{P(X)}$$
- $P(X)$: è una variabile costante per una determinata classe $C$.
- $P(C)$: è dato dal numero di record che appartengono a $C$, che denominiamo $N$ sul numero di record totali $N_{tot}$, che calcoliamo so ogni singola classe.

## Example
![[IMG-Classificazione-20261105-6.png]]

Da questa tabella andiamo a prendere come valore di $X$, la colonna **Outlook**, si vanno a prendere tutte le variabili possibili della colonna, in questo esempio sono (`rain`, `sunny`, `overcast`, diverse tra loro) e le etichette di classi, `Class` che sono due variabili `P` e `N`. 

Di questi valori ora andiamo a calcolare le singole probabilità, che possano appartenere all'etichetta di class `P` e  `N`![[IMG-Classificazione-20261105-7.png]]

Vediamo che per `sunny` insieme a `P` ci sono due volte.
![[IMG-Classificazione-20261105-8.png]]

Mentre il numero delle `P` presenti nella colonna class sono 9, allora si calcola quanto è presente `sunny` su tutte le istanze di `P`
$$P(sunny|P) = \frac 2  9 = 0,222\dots$$
Si fa questo per tutti i casi per tutte le colonne![[IMG-Classificazione-20261105-9.png]]

Poi se prendiamo come esempio un nuovo record da classificare come
```
X = <rain, hot, high, false>
```

Per calcolare se questo record è appartenente all'etichetta `P`o `N`, si calcola la probabilità delle singole colonne e si fa la moltiplicazione di tutte le probabilità $P(X|p)*P(p)$
$$P(rain|p) * P(hot|p) * P(high|p) * P(false|p) * P(p)$$
$$\frac{3}{9} * \frac{2}{9} * \frac{3}{9} * \frac{6}{9}* \frac{9}{14} = 0,010582$$
Se volessimo calcolare la probabilità che sia più correlato all'etichetta `N`, si fa la stessa cosa ma con N
$$\frac{2}{5} * \frac{2}{5} * \frac{4}{5} * \frac{2}{5}* \frac{5}{14} = 0,01826$$
Vediamo infine che il record `X = <rain, hot, high, false>` è più probabile che sia appartenente alla classe `N` che alla `P`

# Supported Vector Machine
Tecnica utilizzata per generare un modello che cerca cerca di identificare un iper-piano lineare che riesce a separare le classi, che si basano sulle funzioni di ottimizzazione.
![[IMG-Classificazione-20261109.png]]

Dalla linea $B_{1}$, ci si chiede quanto dista dal punto verde o dal punto vuoto? Questo si vede dall'immagine tramite il **margine**, che viene generato da quanto distano i punti dalla linea $B_{1}$.

Mentre per $B_{2}$,  si ha un margine molto ridotto tra i due differenti punti, quindi **ci sono più sbagli**. Quindi si cerca di ottenere un margine più grande tra gli oggetti di classi differenti.

Abbiamo che $B_{1}$ è più robusto di $B_{2}$.

Se non è lineare invece applichiamo un altra funzione che possiamo identificare una divisione.
![[IMG-Classificazione-20261109-1.png]]

## Valutazione
-  **Accuratezza**: buone performance

-  **Interpretabilità**: **modello non interpretabile**, la spiegazione è difficile non è facile se non descrivendo che la predizione avviene e le funzioni che vengono applicate ogni volta.

-  **Incrementalità**: non incrementale

-  **Efficienza**: La tecnica di trasformazione è sempre necessaria e consuma tante risorse

-  **Scalabilità**: media scalabilità

-  **Robustezza**: resistente al rumore e agli outliers

# Artificial Neural Networks
Si ispira alla struttura delle reti neurali del cervello umano, dove ogni **neurone rappresenta una unità di elaborazione**. Poi abbiamo le **synapses che sono le connessioni con le varie unità di elaborazione.**![[IMG-Classificazione-20261109-2.png]]

Ci sono differenti tipologie di reti neurali che possono essere applicate per contesti differenti. Le differenti architetture sono per differenti task, come:
- **Numerical Vector Classification**: [[#Feed Forward NN]] (FFNN)
- **Image Understanding**: [^1]Convolutional NN (CNN)
- **Time Series Analysis**: Recurrent NN (RNN)
- **Denoising**: Auto Encoders

## Feed Forward NN
![[IMG-Classificazione-20261109-3.png]]
Ci sono tre livelli:
- Input Layer
- Hidden Layer
- Output Layer

Si usano quando si hanno in input dei vettori numerici, processati da un architettura **fully connected**, che generano in output la probabilità di appartenenza dell'oggetto alle diverse classi, **si assegna l'etichetta predetta quella con la probabilità più alta**.

C'è un layer di intermezzo che si chiama **Hidden Layer**, che presenta delle caratteristiche specifiche (che non si sa cosa).

L' architettura viene definita ***fully connected***, perché ogni nodo possiede $n$ uscite, che sono una per ogni nodo del layer successivo

Le connessioni come si vede dall'immagine possiedono dei pesi.

### Struttura del Neurone
![[IMG-Classificazione-20261109-4.png]]

Prende in input una serie di vettori $x$, nella quale gli applicano un peso $w$, poi svolge un somma pesata dei risultati ottenuti, finche non si va ad applicare poi in output una **funzione di attivazione** $f$.

Nell'output della somma pesata $\sum$, c'è una componente chiamata **fattore correttivo** $\mu_{k}$, cioè una correzione che viene applicata all'output per avere una risposta corretta.

### Funzioni di attivazione
Le funzioni di attivazione $f$ possono essere scelte, tra 4 possibili opzioni che cercano di simulare l'attivazione biologica, queste sono:
- **Binary Step**: che a seconda del valore che riceve in input fa una discretizzazione, cioè converte il valore o in $0$ oppure in $1$.

- **RelU**: che per i valori negativi, setta il valore a 0, mentre per i positivi applica una funzione lineare

- **Sigmoid**: per i numeri naturali che resituisce un valore che è compreso tra 0 ed 1
![[IMG-Classificazione-20261110-1.png]]
- **TanH** (Tangente Iperbolica): restituisce un valore che và da 1 ad -1![[IMG-Classificazione-20261110.png]]

L'unico layer che possiede una diversa funzione di attivazione è il layer di output, questo layer ha una funzione che si chiama **Softmax**. Questa funzione viene applicata solo all'output layer considerando tutti i neuroni in input, che viene interpretato come una **distribuzione delle probabilità** rispetto alle etichette dei valori di classe.
![[IMG-Classificazione-20261110-2.png]]

### Creare la FFNN
Prendiamo un dataset di training in input dove si vanno a definire i **valori dei pesi** ($w$) per ogni nodo e il **valore dell'offset** (la funzione di correzione $\mu$), eseguendo un approccio iterativo sul dataset di training.

L'algoritmo base è il seguente:
1. Si danno **valori casuali ai pesi e all'offset**
2. Si fanno le iterazioni sui dati di training, dove per ogni iterazione si calcola la rete

### Valutazione dell'FFN
- **Accuratezza**: molto alta

-  **Interpretabilità**: il modello e la predizione non sono interpretabili

-  **Incrementalità**: non è incrementale

-  **Efficienza**: la costruzione del modello richiede molto tempo e un tuning dei parametri molto complesso, la classificazione invece è molto veloce

-  **Scalabilità**: è mediamente scalabile sia dal punto di vista della dimensione del training set che da quello del numero di attributi
  
-  **Robustezza**: è robusto rispetto a rumore e outliers, richiede un training set molto grande
# Model Evaluation

>[!info]
>Sono dei **metodi per confrontare le performance del modello**, bisogna decidere come suddividere la porzione dei dati che viene utilizzata per addrestare e quella utilizzata per la valutazione.

La metrica di valutazione del modello avviene tramite l'accuratezza dell'associazione del dato e dell'etichetta che viene assegnata.

L'obbiettivo è quello di stimare quantitativamente, **quanto il modello performa nella distribuzione della classificazione**, oppure il costo che impiega, quando il modello svolge una classificazione sbagliata. Inoltre le performance si misurano anche dalla dimensione del dataset di training.

## Curva di Apprendimento
Prendiamo la curva di apprendimento di un modello di esempio:
![[IMG-Classificazione-20261109-5.png]]

Nel grafico vediamo che se andiamo a testare il modello con diversi sample di dati, l'**accuratezza del modello va ad aumentare con la dimensione del sample**. Questo però è possibile se e solamente se si vanno a schedulare il sample dei dati, questo è possibile in due modi: 
1. **Arithmetic sampling**:

2. **Geometric sampling**:

>[!warning] Effetti di una dimensione del sampling bassa
>Si possono creare più bias e diverse varianti, causati dalla dimensione ridotta del sampling

## Partitioning Data
Con un unico dataset, dobbiamo capire come partizionarlo in due diverse sezioni, uno per il training ed uno per la validazione. Questo tramite due tecniche:
1. **Hold Out** 80/20: 80%  per il training mentre il 20% per il testing, utilizzata per dataset molto grandi (partizionamento fisso).

2. **Cross Validation**: si divide il set di dati in $k$ sotto-gruppi, dove si svolge il training in $k-1$ dataset, mentre l'ultima partizione la uso per la validazione (partizionamento variabile).
   >[!example]
   >Se prendessimo 5 partizioni, 4 di queste vengono usate per il training, mentre l'ultimo viene utilizzato per il testing.
   >

**Ma come li distribuiamo i dati?** Andiamo a stratificare il sample in modo da generare le partizioni, ogni gruppo mantiene la stratificazione. ?? ()

### Hold Out
Partizionamento fisso, lo utilizzo come detto prima con un dataset molto grande e il partizionamento è molto costoso. Si possono però anche decidere porzioni fissi differenti, come per esempio: 75% training mentre 25% testing.

### Cross Validation
Viene combinato con la Stratified (Stratified Cross Validation), più il dataset è piccolo, la dimensione di $k$, deve essere grande, mentre se si ha un dataset piccolo, si prende una dimensione di $k$ piccolo.

**Leave-one-out**: dove si ha che $k=n$, cioè che è grande tutta la partizione, questo usato solo in dataset molto piccoli.

## Model Performance estimation
La pipeline è training -> validation -> test, dove si vanno ad effettuare il calcolo delle metriche. Prendiamo per esempio un dataset che si deve suddividere in 3 partizioni:
1. **60% per il Training**: si sceglie la configurazione ottimale dei parametri
2. **20%** **per la Validation**: si sceglie il modello migliore
3. **20% per il Test**: si testa il modello.

Si può usare l'[[#Hold Out]] per scegliere il blocco dell'80% (training + validation), mentre il 20% per il testing. Oppure si può usare la [[#Cross Validation]], dove si divide in training e validation.

### Valutazione Accuratezza
![[IMG-Classificazione-20261109-6.png]]

Sono però limitate e non sono sempre utilizzate, queste perché possono fornire parametri sbagliati e non corretti.![[IMG-Classificazione-20261109-7.png]]

Il metodo migliore è con il *richiamo* e la *precisione*, dove abbiamo:
- **Richiamo**:![[IMG-Classificazione-20261109-8.png]]
  Che sono il numero di oggetti che sono assegnati correttamente, che viene **diviso con il numero di oggetti che appartengono alla classe C**

- **Precisione**:![[IMG-Classificazione-20261109-9.png]]
  
  La precisione che viene svolta l'assegnamento che si prende come dividendo sempre il numero di oggetti correttamente assegnati a C, mentre il divisore sono gli **oggetti che sono assegnati a C**
  
Per massimizzare questi due parametri si svolge una formula (da vedere meglio a cosa serve nel dettaglio):
$$F = \frac{2rp}{r+p}$$

## ROC (Receiver Operating Characteristic)
Inventato per individuare i segnali, che è un trade-off, tra i valori positivi e i falsi allarmi. Si utilizzano le curve che possono essere di due tipologie:

- **TPR**: True Positive Rate, nell'asse delle $y$:
  $$TPR = \frac{TP}{TP+FP}$$
- **FPR**: False Positive Rate, presente nell'asse delle $x$:
  $$TPR = \frac{FP}{FP+TP}$$

---
[^1]: Significato: https://www.treccani.it/vocabolario/convoluzione/
