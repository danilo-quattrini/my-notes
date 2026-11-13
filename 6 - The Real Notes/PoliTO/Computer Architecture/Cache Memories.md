---
created: 2026-02-14T15:43:00
tags:
  - baby
topics:
  - Architecture 
  - "[[School]]"
author: Danilo Quattrini
---
# Cache Memories
---
*Appendix B.1 in the book Computer Architecture Quantitve Approach*
## Questions
### Definizioni
- Che cosa sono le cache?
  
- Perché ci servono le memorie cache?
  
- Com'è strutturata la cache all'interno di un laptop, mobile o desktop?
  
- Che cos'è la **località di referenza** nelle cache e quanti tipi ne esistono? Come funziona con la memoria cache invece?
## Prestazioni della cache
- Qual'è la formula per calcolare le prestazioni della cache?
  
- Fai un esempio di come si possa calcolare il tempo medio delle prestazioni della cache se si ha un hit ratio di $0.7 - 0.6$.

## Struttura della cache
- Da quanti e quali macro-elementi è composta la struttura della cache?
  
- Com'è strutturata una linea della cache, cioè quali sono le componenti che ne fanno parte?
  
- Come funzionano i bit di validità? Quali sono i bit di validità? Qual'è la differenza che intercorrono tra le due tipologie di bit di validità?
  
- Quali sono le operazioni aggiuntive che può svolgere la cache?

- Che cos'è la *Cache Eviction*?

## Calcoli Cache
- Come si calcola il numero delle righe che ci sono in una cache? Di che cosa abbiam bisogno?
# Cache
---
## Introduzione
>[!quote] Che cosa sono?
>Le prestazioni dei processori sono aumentate negli ultimi 50 anni nei confronti della memoria, il processore va mille volte più veloce a differenza della memoria. La memoria cache è nascosta, cioè è nascosta dall'utente.

Ricompare l'architettura di [[Computer Architecture#Von Neumann Architecture (Princeton Architecture).|Von Neumann]], come illustrato in questa immagine, nuovamente faremmo vedere l'immagine dell'architettura
![[Screenshot 2026-10-13 at 10.05.59.png]]

Riguardare questa parte perché l'hai già fatta [[Computer Architecture#Classification|qui]], dove parla dell'architettura di Von Neumann e quella Harvard. Semplicemente quella Harvard divide la memoria in due parti dove la prima è quella dedicata alle istruzioni mentre l'altra parte della memoria ai dati.
![[Screenshot 2026-10-20 at 11.53.03.png]]

Nei sistemi odierni le cache sono rappresentati in questo modo:![[Screenshot 2026-10-13 at 10.07.51.png]]
Le cache sono memorie molto più veloci, più costose, e più grandi dei registri come si vede nell'immagine l'accesso alla cache impiega solitamente `1ns` (nano secondo). La memoria RAM è 100 volte più lenta della cache, perché la cache ha una dimensione più grande dei registri ben `64 KB` a differenza di `1000 bytes` dei registri, ma a differenza della memoria RAM e della Storage (Hard Disk) l'accesso alla cache è nettamente più veloce.

Solitamente ci sono 3 livelli di cache che vanno a crescere per quanto si parla di dimensione e accesso a tali memorie, basta vedere l'immagine, ogni livello, dal più basso al più alto è contenuto al suo interno `L1 -> L2 -> L3`.

## Idea della cache
Il processore dovrà chiedere istruzioni e dati, che dovranno essere consegnare al processore ad un singolo colpo di clock. Le cache usano un principio chiamato **località di referenza** di due tipi:
- **Temporalità Locale**: se un programma ad un tempo $t$ accede alla memoria, è più probabile che il programma possa accedere alla stessa cella di memoria in un tempo $t_{0} + \nabla t$.

- **Località Spaziale**: se ad un tempo $t_{0}$ il programma accede alla memoria ad una cella di memoria $x$ è più probabile che al tempo $t_{0} + \nabla t$ il programma andrà anche ad accedere alla memoria con l'indirizzo $x \pm$

Con la memoria cache invece funziona allo stesso modo, se in un determinato tempo 0, $t_{0}$ viene caricato il blocco di memoria che ha bisogno il processore nella cache, sarà più probabile che in un tempo $\nabla t$ il programma accederà alla locazione della cache e caricherà il dato che ha bisogno.

## Prestazioni della Cache
Prendiamo i seguenti elementi:
- $h$: cache hit ratio
- $C$: tempo accesso alla cache
- $M$: tempo di accesso alla memoria quando il dato non è alla cache
L'accesso medio sarà:
$$t_{avg}= h * C + (1 - h)*M$$
>[!example] Esempio
>Prendiamo come esempio l'accesso alla cache con valore di hit ratio $0.8$ -  $0.9$
>$$T_{avg} = 0.8 * 2*10^{-9}$ + (1 - 0.8) * 50 * 10^{-9}$$
## Organizzazione Cache
La cache si divide in una parte dati e una parte di *controllo* (Cache Controller). La **parte di dati** a sua volta e divisa in un **directory array** un **data array**, in cui ogni entry è una cache line caratterizzata da un **bit di validità**. (*validity bit*), un **tag** e un **blocco di dati** (data block).
![[Screenshot 2026-10-13 at 10.22.55.png]]
Quando un processore ha **64 KB**  per il livello di cache 1, bisogna tener conto che la parte dei **64KB sono presenti SOLO NELLA PARTE DEI DATA ARRAY**, viene nascoste le parti della **directory array**.

- **Data Block **: Contiene uno o più blocchi di memoria dove le informazioni della cache vengono salvate (dati o istruzioni).

- **Tag**: Identifica in modo univoco ogni linea di cache

- **Bit di Controllo**: bit che sono relativi alla validità della cache, questo può servire per rimuovere valori spazzatura, per far si che si controllino che i valori siano validi oppure no.
	- **Bit di validità (V)** : ti segnala se la linea all'interno del processore è valido oppure no.
	- **Dirty Bit (D)**: rappresenta che il dato è stato modificato nella cache.
>[!example] Esempio
>Se abbiamo la cache vuota, poi leggi la slide della cache `14` che viene spiegato l'esempio.

### Operazioni aggiuntive della cache
La cache possiede anche altre operazioni che può svolgere al suo interno, queste sono:

 - **Intercettare gli indirizzi** che vengono prodotti dal processore.
   
 - **Controllare la presenza di un blocco di dati** che il processore vuole accedere.
   
 - Caricare il blocco di dati nel data block.
   
 - Rimpiazzare un vecchio blocco di dati con uno aggiuntivo.

Quest'ultimo processo prende il nome di *Cache Eviction*, cioè l' **abilità della cache di rimuovere vecchi blocchi di dati, per far spazio a dei nuovi se la cache è piena oppure ci sono certe regole da dover applicare.**

### Dimensione della cache
Le linee di cache moderne hanno dimensioni tipiche di **32, 64 o 128 byte per linea**. Quindi se abbiamo una cache di dimensione di 1Kb (1024 Byte), e sappiamo che ogni linea può avere una dimensione tra quelle sopra elencante allora avremmo
$$\text{Numero di cache line} = \frac{1024\text{ byte}}{32\text{ byte/linea}} = 32\text{ cache line}$$
Nel caso di una cache a livello 1 se volessimo avere meno linee di cache non ci basta più che ogni singola linea sia grande **32** byte, ma avremmo bisogno di più byte, tipo $64$ Byte, ed avremmo quindi:
$$\text{Numero di cache line} = \frac{65.538\text{ byte}}{64\text{ byte/linea}} = 1024\text{ cache line}$$
Quindi la formula si può tradurre in:
$$\text{Numero di cache line} = \frac{n}{m} $$
Dove:
- $n$ = dimensione del blocco dati della cache (`L1  -> 64Kb, L2 -> 256Kb, ecc..`)
- $m$ = dimensione di un singola linea di cache ($32$, $64$, $128$ Byte)

### Controllo della Cache
Quando un dato della memoria deve essere indirizzato, l'istruzione della CPU è composto da:
- **Offset**: indica la word da caricare all’interno del blocco
  
- **Tag**: server per controllare se il valore è già presente nella cache oppure no, controlla se il **tag è già presente nella cache**.
  
- **Index**: indica la cache line, cioè indica la linea in cui è presenta il dato nella cache

![[Screenshot 2026-10-13 at 10.45.51.png|1120]]

Per individuare un blocco in cache è sufficiente un multiplexer (decoder) che opera sull’indirizzo:

![[Screenshot 2026-10-13 at 10.52.01.png]]

Sopra vediamo dall'immagine che il decoder controlla se il tag esiste all'interno della cache e ritornerà un risultato che può essere **H** che sta per **Hit** oppure **M** che sta per **Miss**. Se il dato è presente nella cache allora viene inviato al processore  se no no.

Non basta solo il tag per identificare la linea della cache, ma c'è la necessità anche di avere di un indice. Nel caso di 1024 byte saranno sufficienti 10 bit per l’index, 3 bit per l’offset e 19 bit per il tag. Dunque il diagramma totale appare come segue:
![[Screenshot 2026-10-13 at 10.53.23.png]]
La cache è normalmente situata tra il CPU e il bus (oppure tra la memoria principale e il bus, ma non conviene). Ogni volta che il processore effettua un accesso in memoria allora la cache interpreta l’indirizzo e controlla se la word è già in cache o meno.

## Posizione della Cache
![[Screenshot 2026-10-13 at 10.54.11.png]]

## Processore e Cache
Ci sono due stadi in cui il processore quando vuole interagire con la cache per prendere un dato può ritrovarsi con un **cache hit**, cioè il dato che il processore aveva bisogno è stato trovato in cache.

Nel caso invece il processore non trova il valore che cercava nella cache allora si dice **cache miss**, la cache può rispondere in due modi:

- Accede alla memoria carica il blocco mancante, successivamente risponde alla richiesta. Il tempo di accesso è maggiore rispetto a un sistema cache‑free.

- Accede alla memoria e risponde immediatamente alla richiesta (load through o early restart). Questa tecnica richiede un costo maggiore in termini di hardware relativi alla cache, ma le miss hanno un impatto minore sulle performance della cache.

>[!info] Cosa succede al processore?
>Una *cache miss* viene gestita in ambito hardware dal processore, che comporta però al processore di passare ad un esecuzione *in-order* stallando e fermandosi finchè il dato non è presente.



la cache riduce il tempo di accesso alla memoria di un fattore dipendente dal ratio tra il tempo di accesso alla cache e alla memoria.

## Harvard Architecture for Caches
Le cache oggi giorno sono separate in cache di istruzioni e cache di dati. La cache per le istruzioni è solitamente più semplice da gestire rispetto a quella dei dati, in quanto le istruzioni non possono essere cambiate (a differenza dei dati che sono variabili).

Se vengono utilizzate due cache l’architettura del sistema prende il nome di Harvard architecture, caratterizzato dall’esistenza di due memorie separate tra dati e codice andando direttamente in contrasto con quella che era l’architettura di Von Neumann.

Le caratteristiche sono:
- **cache size**: dimensione della cache
- **block size**: dimensione di un blocco di memoria
- **mapping**: tipo di mappatura
- **replacing algorithm**: algoritmo di rimpiazzamento
- meccanismo di aggiornamento della memoria

### Cache Size
La dimensione della cache è molto importante in termini di costi e performance. Man mano che la dimensione aumenta si ha un incremento dei costi, delle prestazioni di sistema ma una riduzione della velocità della cache. Le dimensioni solitamente variano da qualche kB a qualche MB

### Mapping
![[Screenshot 2026-10-13 at 11.00.50.png]]

Il meccanismo attraverso cui una **cacheline** viene associata ad un blocco di memoria è detto mapping. E’ importante assicurarsi che la verifica di presenza di un dato per un certo indirizzo sia sufficientemente veloce.

Il tipo di mappatura è detto modello di associatività, e può essere:
- **direct mapped**: numero del blocco di memoria modulo totale dei blocchi in cache, questo si fa come detto prima con l'operazione di modulo, dove si prende l'indirizzo di memoria e si fa il modulo con il totale dei blocchi presenti nella cache. La formula è la seguente:
	- $n$ la locazione di memoria che vogliamo allocare il valore
	- $x$ numero totale dei blocchi della cache.
	  $$n \ MOD \ x = cache\_line$$
	
- **set associative**: numero del blocco modulo totale dei blocchi in cache diviso livello di associatività. Permette di salvare ogni elemento della memoria in due linee della memoria (utile quando abbiamo elementi che vengono chiamati molto più spesso in modo da salvarli). Garantisce che i dati più utilizzati possono essere ritrovati in cache. (ci permette di salvare un dato in due linee invece che in una singola lineea di memoria)
 ^055d27
- **fully associative**: ogni linea della memoria può essere salvata in qualsiasi posizione della cache. Salva l’indirizzo completo (tag scompare).

#### Effetti dell'associatività della cache
![[Screenshot 2026-10-16 at 08.51.30.png]]
### Algoritmo di Rimpiazzamento
Ci sono diverse possibilità se le linee della cache sono tutte piene, si possono fare in diversi modi:
- **Random**: semplice ed efficace, può andare bene, non è costosa, ma non è la migliore
- **Least Recently Used** (LRU): traccia l'elemento che è stato utilizzato tanto tempo fa e viene rimpiazzato, utilizzando dei contatori, l'elemento che sta da tanto tempo dentro la cache viene tolto e rimpiazzato.
- **First-In First-Out** (FIFO): 
- **Least Frequently Used** (LFU): quello che è stato utilizzata di meno viene tolta e sostituita con una nuova, più difficile da utilizzare.
![[Screenshot 2026-10-16 at 08.56.52.png]]
Nella soluzione LRU, c'è la necessità di due bit per linee, che aumentano la quantità di memoria che dovrà allocare dentro la cache. FIFO-SC (Second Change), costa poco e funziona in certi momenti è identico come FIFO, dove c'è un puntatore all'ultimo elemento utilizzato. Il valore esterno è il numero della via, mentre il bit esterno è chiamato il clock bit. Le linee che si utilizzano spesso vengono marcate e salvate 
#### pLRU Algoritmo
Avremmo un albero binario dove vedrò quale sarà la foglia da eliminare.
![[Screenshot 2026-10-16 at 09.09.51.png]]

Prendiamo un esempio che in questo caso dovremmo allocare nella stessa linea di memoria lo stesso dato, come in questa immagine sotto.
![[Screenshot 2026-10-16 at 09.10.31.png]]
(==vedere da slide 36 a 45==)

## Main Memory Update
Come aggiornare la memoria principale? Con le cache possiamo scrivere e leggere al loro interno in modo veloce ed efficace. Ci sono due strategie:
- **Write Back**
- **Write Through**

### Write Back
Quando ho una cache con associatività ad uno, quando il programma deve accedere ad una linea di cache che deve essere sostituita allora vado ad aggiornare la memoria. Nel momento in cui la linea nella cache deve essere sostituita allora posso scrivere dentro la memoria.

#### Che problemi ha questa strategia?
- La memoria non avrà dati aggiornati.
- Se ho un sistema a multi-processore e se ho un altro processore che vuole utilizzare lo stesso dato, il secondo processore avrà un dato vecchio e non aggiornato.
- Non è possibile recuperare il dato se ci sono dei problemi nel sistema.

### Write Through
Ogni volta che c'è una scrittura un dato in cache, allora viene scritto anche nella memoria. Si va ad utilizzare di più il BUS di sistema che va a rallentare le operazioni principali.

### Write Allocate
In caso di miss in scrittura, il dato viene allocato in cache, cioè utilizzo la cache come direzione per le scritture. Questo meccanismo viene utilizzato spesso con il write-back.

### No Write-Allocate
Scrivo direttamente in memoria e non nella cache

## Cache Coherence
Più processori che vogliono accedere alla stessa locazione di memoria. Come nell'immagine sotto viene mostrato, bisogna gestire la consistenza / coerenza dei dati.
![[Screenshot 2026-10-16 at 09.32.54.png]]
**Coerenza**:
- La lettura deve ritornare il dato più precedente.
- Si deve scrivere alla stessa locazione di 
**Consistenza**:
- Se il processore scrive in una locazione A seguito da una locazione B, tutti i processori devono vedere sia i nuovi valori di B che quelli di A

### MESI Protocol
- Modified: 
- Exclusive: Valore letto in memoria ma non ancora modificato. Solo la cache possiede questo valore.
- Shared: Valore letto in memoria ma non ancora modificato. IL valore è stato letto da un'altro processore.
- Invalid: La lineea non è valida perché è stato modifica dall'esterno. Un valore condiviso è stato modificato da un processore differente
## Livelli delle Cache
Il livello più basso devono essere un sotto insieme del livello più alto, cioè L1 è un sottoinsieme di L2 ed L2 è sotto-insieme di L3![[Screenshot 2026-10-16 at 09.43.43.png]]
Una cache di livello 1 L1 è grande 192 kB, mentre le cache di L2 vanno da 2 a 4 MB, mentre le cache a livello 3 sono a 8MB
## Esercizi sulla Cache
Da una cache possiamo prendere l'informazioni della sua architettura e vogliamo sapere quante linee di cache ci sono:

La cache ha una zona di dati di 64Kb, direct mapping, ogni linea della cache e della memoria  a dimensione di 4 byte , gli indirizzi sono a a 32 bit. 

Determinare la struttura della cache, quante linee ci sono, la dimensione del tag e tenere in conto i **validity bit** e i **dirty bit**  e i bit relativi al rimpiazzamento. Come faccio a determinare la dimensione reale della cache?
1. Devo determinare quante sono le linee di cache sapendo la dimensione della sezione e i 4 bytes per ogni blocco.
2. Devo trovare la dimensione dell'offset, poi dell'indice (index) e poi alla fine possiamo trovare il tag.
$64 / 4$ mi darà il numero di linee.

Gli indirizzi hanno 30 bit togliendo i due degli indirizzi $32 - 2$ dei bit riservati all'indirizzo, quindi avremmo che la memoria ha $2^{30}$ linee  o blocchi.

Per trovare il numero di linee nella cache si fa la dimensione della zona di dati della cache $64$Kb diviso alla dimensione di ogni linea della cache $4$ Byte, quindi  il **numero delle linee della cache** sarà:
$$64Kb \ / 4B = 16 Kb = 2^{14}$$

1. Prima bisogna sapere la dimensione della cache
2. Secondo sapere la dimensione della linea
### Esercizio complex
![[Screenshot 2026-10-16 at 10.41.35.png]]
Seguendo quello detto prima bisogna prima trovare la dimensione della cache leggendo il testo, che in questo caso è nella parte dove c'è scritto **cache memory of 4KB (data only)**, organizzato in 2-way in un [[#^055d27|set associative]] ,per prendere il numero di bit che basta trovare la potenza di due che viene il risultato di 4KB cioè:
$$2^{12}=4096 Byte$$

Poi bisogna trovare la dimensione delle linee, che dal testo prima si legge nella parte in cui dice **cache lines contain 256 bits = 32 Bytes** 
#### Come trovare l'Offset, l'Index e il Tag?
Dobbiamo leggere dalla consegna la dimensione dell'indirizzo, che è espresso come **Addresses are expressed on 32bits**, siccome sappiamo che un indirizzo è diviso in 3 parti in 2 way-associative allora si ha 
$$\text{Indirizzo (32 bit)} = \text{Tag} + \text{Index} + \text{Offset}$$
L'offset si calcola supponendo che
# Reference
---

