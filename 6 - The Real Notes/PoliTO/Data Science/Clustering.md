---
created: 2026-02-14T15:43:00
tags:
  - baby
topics:
author: Danilo Quattrini
---
# Clustering
---
Algoritmi [[Supervised And Unsupervised#Unsupervised (Apprendimento NON Supervisionato)|Unsupervised]], cioè che non c'è bisogno di un etichetta di classe per assegnare delle etichette ai dati.

>[!info] Obbiettivo
>Trovare un partizionamento dei dati che appartengono ad un certo gruppo che sono simili, mentre quelli differenti in un altro.
>![[IMG-Clustering-20261111.png]]

Si partono dai dati e si **basano sulle caratteristiche dei dati** e **sul fenomeno che si sta analizzando**. Si sceglie la metrica della [[Similarità e Dissimilarità|similarità e dissimilarità]], che però si necessità di [[Data Preparation#Trasformazione di un attributo|normalizzare]] i dati in modo da definire sotto-gruppi distinti, lo scop è quello di **mantenereo la distanza dei sottogruppi alta**

## Applicazione del Clustering
Lo si svolge in una fase chiamata **Understanding**, cioè **capire la natura dei dati che si vanno ad utilizzare**.

>[!example]
>Esempio si possono creare dei gruppi di documenti, che contengono gli stessi attributi (es numero di parole che iniziano con "A" oppure diversi documenti che parlano di mercato e stock)

Si può utilizzare il clustering per la **Summarization**, cioè ridurre la dimensione dei dati che stiamo analizzando.

## Problema?
**Il problema si presenta nella validazione** delle partizioni che si sono creati. Questo perché non abbiamo una metrica con cui controllare che i sotto-gruppi, siano validi oppure no.![[IMG-Clustering-20261111-1.png]]

## Famiglie di Clustering
Un cluster è un insieme di gruppi che possono essere distinti in due macro-famiglie:
- **Partition Clustering**: ogni punto appartiene ad un solo ed unico gruppo
  
- **Hierarchical Cluster**: lo stesso oggetto può far parte di gruppi diversi, ma che allo stesso tempo può rappresentare partizionamenti diversi.

### Partitional Clustering
![[IMG-Clustering-20261111-2.png]]

### Hierarchical Cluster
![[IMG-Clustering-20261111-3.png]]

Nella soluzione in alto a sinistra, si ha 4 soluzioni differenti, dove ci possono essere diversi partizionamenti in base alle scelte dell'utente. 
![[IMG-Clustering-20261111-3 copy.png]]
Ogni ramo di un **algoritmo gerarchico del Dendrogramma** restituisce un diverso gruppo. Dall'esecuzione dell'algoritmo si può ottenere un dendrogramma tradizionale oppure non, questo non è deciso ma dall'organizzazione dei dati.

## Altre Distinzioni Di Cluster
- **Esclusivo vs Non-Esclusivo**: un punto appartiene ad un gruppo mentre non esclusivo se appartiene a più gruppi.

- **Fuzzyness**: ogni punto appartiene a tutti i cluster con un peso compreso tra 0 e 1 per ogni cluster
  
- **Parziale vs Completo**: ogni gruppo appartiene

- **Eterogeneo vs  Omogeneo**: un partizionamento eterogeneo o omogeno rispetto a diverse dimensioni, come ad esempio la cardinalità dei gruppi, la **forma** (cioè i cluster identificati possono avere la stessa forma se sono omogenei oppure forma differenti) e la **densità** (numeri di punti in una determinata area)

## Tipi di Clustering

Possono essere:
- **Cluster ben Separati**:
![[IMG-Clustering-20261111-4.png]]
- Center-Based: il gruppo lo rappresento con il centroide o il medoide (che è l'oggetto più vicini al centroide)

- Contiugity-Base: un cluster è un insieme di punti tali che un punto in un cluster sia più vicino a uno o più altri punti nel cluster che a qualsiasi altro punto che non è nel cluster 

- **Density-Based**: un cluster è una regione densa di punti, separati da zone a bassa densità, usato quando i cluster sono irregolari e in presenza di rumore e outliers![[IMG-Clustering-20261111-5.png]]

- **Cluster concettuali o Proprietà condivise**: individua cluster che condividono proprietà comuni o rappresentano un concetto in particolare
# Algoritmi di Clustering

- [[#K-means]]
- [[#Hierarchical ]]
- [[#Density-Based]]
## K-means
Algoritmo partizionale, dove un oggetto appartiene ad un solo e singolo punto, ogni cluster è associato ad un centroide (punto centrale). **Ogni punto è assegnato al cluster che è più vicino al centro**.

Abbiamo un valore di input chiamato $k$ che indica il numero dei cluster che vogliamo utilizzare. 
![[IMG-Clustering-20261111-6.png]]
Dato un numero specifico di punti (esempio 20), si vanno ad assegnare ad ognuno di questi il punto del centroide.

### Example
![[IMG-Clustering-20261111-7.png]]
Ci sono 3 gruppi differenti che sono differenti per i colori ($k=3$), per i **punti** $n$  che si hanno nel grafico e si svolgono delle **iterazioni** $I$ per i numeri degli attributi $d$. Quindi si possiede una complessità di:
$$O(k*n*I*d)$$
![[IMG-Clustering-20261111-8.png]]

### Formula SSE
La misura per poter eseguire il calcolo de k-means, è utilizzando il **Sum of Squared Error (SSE)**.  Dove si considera l'**errore  la distanza del punto al cluster più vicino**.

Per fare il calcolo e ottenere il SSE più basso è quello di **elevare al quadrato la distanza degli errori** e poi **sommare i quadrati**:
$$SSE = \sum^{k}_{i=1}\sum_{x\in C_{i}} dist^{2}(m_{i},x)$$
Analizzando i singoli parametri e simboli del calcolo:

- **$K$**: Il numero totale di cluster scelti nell'algoritmo.
    
- **$C_i$**: Il generico $i$-esimo cluster ($i = 1, 2, \dots, K$).
    
- **$x$**: Un singolo punto dati (istanza/record) appartenente al cluster $C_i$.
    
- **$m_i$**: Il punto rappresentativo (centroide o media) del cluster $C_i$. Si dimostra che, se la distanza usata è quella Euclidea, il punto $m_i$ che minimizza l'errore è proprio la **media** dei punti appartenenti a $C_i$:
$$m_i = \frac{1}{\vert{}C_i\vert{}} \sum_{x \in C_i} x$$
- **$dist(x, m_i)$**: La distanza geometrica (solitamente la [[Similarità e Dissimilarità#Distanza Euclidea|Distanza Euclidea]]) tra il punto $x$ e il centroide $m_i$.
    
- **$dist(x, m_i)^2$**: L'errore al quadrato. Elevare al quadrato la distanza serve a due scopi:
    
    1. Rende le differenze sempre positive.
        
    2. Penalizza in modo più severo i punti molto distanti dal centroide.

>[!info] Risultato
>Se si ha un SSE molto grande vuol dire che abbiamo un cluster sbagliato.

Quando si svolge il SSE con valori di $k$ alti, si avrà un **risultato di SSE che va a decrescere**
### Cluster vuoti e come gestirli
Scegliere causalmente i valori di $k$ può causare il problema dei **cluster vuoti**, questo perché ci possono essere dei punti che fanno parte a 2 cluster mentre il 3 rimane vuoto, perché il punto del centroide è troppo lontano e non raggiungibile da nessuno dei punti.

Per gestire i cluster vuoti si può scegliere uno di questi metodi:

- **Test Multipli**: cioè si svolgono dei testi su diversi valori di $k$ in modo da ottenere diversi valori di SSE, per far si che **prenda tra i vari test il minor SSE tra i vari test**

- **Soluzione Mista**: si parte da un sample di dati, che verrà poi dopo applicato in modo gerarchico finché non si trova i centroidi iniziali.
  
- **Selezionare i Centroidi Più distanti:** si vanno a scegliere tanti valori di $k$, finché non si prende i valori più distanti.

### Bisectiong K-means
![[IMG-Clustering-20261112.png]]
==(Da completare che non ho seguito)==

### Limitazioni del K-mean
![[IMG-Clustering-20261112-1.png]]
Si deve identificare 3 gruppi nativi, che però, applicando un k di 3 abbiamo dei risultati differenti, non è un risultato ottimale. 

Se abbiamo una densità diversa (cioè il numero dei punti nel grafo), con densità diversa non opera correttamente.![[IMG-Clustering-20261112-2.png]]

Come si può risolvere il problema dei *k-means*?  Si può **utilizzare un valore di k molto grande.![[IMG-Clustering-20261112-3.png]]**
Con 10 cluster abbiamo diversi gruppi che sono separati tra di loro. Questa soluzione si può attuare anche in una forma  differente![[IMG-Clustering-20261112-4.png]]
## Hierarchical  Clustering
Il tipo di risultato è diverso da quello partizionale, perché produce un insieme di risultati, che può essere visualizzato tramite un albero, chiamato **dendogramma**.
![[IMG-Clustering-20261112-5.png]]
Bisogna decidere il punto dove effettuare il taglio, che indicano la massima distanza degli oggetti che fanno parte dello stesso gruppo

### Punti di forza
1. Non si necessità di un valore iniziale
2. Possono possedere un significato

### Generazione del Clustering Gerarchico
Ci sono due tipi di cluster gerarchico
1. **Agglomerativo**:
2. **Divisivo**: 

#### Agglomerativo
Approccio più comune, definendo i cluster che devono essere raggruppati. Per poter utilizzare tale algoritmo si utilizza una **matrice di prossimità**.

![[IMG-Clustering-20261112-6.png]]

Si sceglie di aggregare C2 e C5, si toglie la riga e la colonna che si vuole aggiornare, **si aggiorna la matrice con la nuova unione** che si è creata.
![[IMG-Clustering-20261112-7.png]]

### Definire le distanze tra i cluster (similarietà dei cluster)
Questo si può fare tramite diverse misure di distanze:
- il **MIN** (Single Link): dove prendo la distanza più piccola tra tutte le distanze tra gli elementi del primo e del secondo cluster, nel caso della **similarietà si prende quella più alta.**![[IMG-Clustering-20261112-8.png]]

- **MAX** (Complete Linkage): si prende la distanza tra tutte le distanze, con quelle **con il valore più alto**, nella similarietà si prende tra tutti i punti, quelli che hanno la di![[IMG-Clustering-20261112-9.png]]

- **Group Average:** Si prende la media di tutte le distanze![[IMG-Clustering-20261112-10.png]]

- **Distance Between Centroid**

Gli altri non vengono spesso utilizzati e complessi, in sede di esame non li mette.
#### Example of MIN or Single Link
![[IMG-Clustering-20261112-11.png]]
Si devono calcolare le matrici medie di prossimità, cui si vanno a creare i gruppi che si vedono sopra nel dendogramma. Stessa cosa con le distanze, si devono creare dei gruppi, in base a quelli ch possiedono la distanza ridotta e si cominciano a creare i gruppi.
![[IMG-Clustering-20261112-12.png]]

Si comincia andando a prendere i **due punti che sono più vicini tra di loro**.
![[IMG-Clustering-20261112-13.png]]

#### Example of MAX or Complete Linkage
Prima si popola la matrice, calcolando la distanza euclidea, poi si aggregano i punti dei cluster più vicini. Se ho il MAX, la utilizzo per popolare la matrice. 

Per scegliere il cluster da mettere insieme si prendono i cluster che sono più vicini.
![[IMG-Clustering-20261112-14.png]]

**Pregi:** meno sensibile ai dati rumorosi.
**Difetti**: è sensibile ai valori molti grandi

#### Example Group Average
Eredita le caratteristiche positive del MIN e quella del MAX![[IMG-Clustering-20261112-15.png]]
## Density-Based Cluster
Algoritmo DBScan che **identifica gruppi di dati, che sono caratterizzati da una densità simile.** Cioè separa le zone spase da quelle dense.
![[IMG-Clustering-20261112-16.png]]

### DBSCAN
Prende due valori di input **Eps** che sono il numero dei punti in un raggio e **MinPts**, cioè il min point sarebbe il numero minimo di punti in un determinato cerchio.![[IMG-Clustering-20261112-17.png]]
C'è una fase di etichettatura dei punti che può assumere 3 valori: Noise Point, Border Point e Core Point:

- **CorePoint**: se all'interno di una circonferenza di raggio $y$ si hanno $x$ point che sono maggiori o uguali a **MinPoint**

- **Border Point**: se non è presente in una zona densa, ma è nel vicinato del core point?

- **Noise Point** Non è ne **Core** e neanche **Border**
  
Per individuare i punti si parte da una matrice di distanza, che sarebbe quella che abbiamo visto prima.

#### Algoritmo DBSCAN Applicati

1. Prima si etichetta i punti e si tolgono i punti rumorosi![[IMG-Clustering-20261112-18.png]]
2. Si esplora i vicinati dei core, che convergeranno in un unico cluster.![[IMG-Clustering-20261112-19.png]]

3. Crea i gruppi dei punti connessi in cluster separati.![[IMG-Clustering-20261112-20.png]]

4. Si assegna ad ogni punto il cluster associato.![[IMG-Clustering-20261112-21.png]]

Questo algoritmo funziona bene **per togliere il rumore**, e rilevamento degli outliers, la difficoltà che si presenta è nel trovare il valore di **Eps** e **MinPts**.
![[IMG-Clustering-20261112-22.png]]
Come si vede nell'immagine sotto si ha che se cambiassimo il valore di **Eps** ad uno più basso (9.61 invece di 9.75), si considererà solo i punti che sono più densi, quelli rossi, mentre quelli blu sono rumore che viene tolto.

### Determinare i valori di Eps e MinPts
![[IMG-Clustering-20261112-23.png]]

L'idea da come si vede sul grafico è quella di **prendere i $k$ punti più vicini che sono presenti in un cluster che possiedono una distanza simile tra di loro**.

Nel grafico se si prende il valore di $k = 4$ allora avremmo che ci saranno 1500 punti nel cluster che sono vicini tra ==... (da vedere meglio come funziona)==