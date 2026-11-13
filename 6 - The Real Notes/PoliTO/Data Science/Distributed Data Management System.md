---
created: 2026-11-02
tags:
  - baby
topics:
  - Data
author: Danilo Quattrini
---
# Distributed Data Management System
---
**Che cosa servono i database distribuiti?** Beh a questa domanda rispondiamo che abbiamo le necessità di performance migliori, cioè avere diverse macchine, che hanno potenze distribuite, anche se i singoli non sono potenti, insieme possono cointribuire a migliorare le performance.

>[!example] Esempio
>Vogliamo per esempio creare i sistemi distribuiti che possano mantenere copie del dato in diversi nodi, per evitare che se un nodo si rompa, perdiamo completamente tutte le informazioni che abbiamo salvato.

## SQL Execution
La query può essere mandata direttamente sul server, oppure si può preparare la query prima di doverla eseguire nel database, questo per evitare attacchi di tipo sql injection, ma non solo, la si può utilizzare anche in contesti differenti per utilizzi futuri.

## Che cosa si vuole ottenere con il sistema distribuito
Vogliamo mantenere i dati in tutti i vari e differenti cluster e mantenere il paradigma ACID, si può far avvicinare i dati agli utenti di diverse aree geografiche rendendo i dati disponibili in tutti i fronti.

## Data Fragmentation
Dato un database relazione R, la frammentazione dei dati (data fragmentation) è un sotto-insieme della relazione, in termine di tuple, schema o tabelle. Si possono eseguire la frammentazione in 3 dimensioni differenti:
- **Orizzontale**
- **Verticale**
- **Mixed**

### Orizzontale
La frammentazione orizzontale è un sotto insieme delle relazione R che è una tupla che segue le seguenti regole:
- Stesso Schema di R
- Ottenuta tramite una media delle partizioni $\phi_{p}$
In questa parte **non abbiamo frammenti che si sovrappongono tra di loro**, questo è come eseguire la clausola `WHERE` nelle query SQL.

### Verticale
La frammentazione verticale invece si ricava da un sotto-insieme della relazione R, che devono seguire le seguenti regole.

>[!info] Clausole
>Si ottiene da una media di $\pi_{X}$, dove avremmo che:
>- X è un sotto-insieme dello schema della relazione R
>- La chiave primaria deve essere sempre presente in ogni sotto-insieme in modo di ricostruire lo schema.
>  Tutte le tuple sono incluse e i frammenti si possono sovrapporere tra di loro.

Questo è come eseguire la `SELECT` nelle query SQL

==(da vedere prima)==

# Classificazioni delle Transazioni
Ci sono due tipologie di transazioni che possono essere del tipo:
- **Remote request**: si leggono solo i dati del DBMS in modo da vedere il contenuto dei database.
- **Remote transaction**: non si vanno solo a leggere i valori dei DB ma si vuole operare sui database, mantenendo la consistenza dei dati.

Questo lo si può estendere nel mondo dei Distributed Data Management System. Questo viene sempre visto allo stesso modo di prima come:
- **Distributed Transaction**: questo viene eseguito su ogni tipologia di query SQL, che però vengono svolte in un singolo server nella quale però ha bisogno di atomicità.
  
- **Distributed Request**: quando abbiamo query SQL che richiedono dati in diversi server / cluster e non in uno solo, dove si ha la necessità di ottimizzare tale operazioni

# Distributed DBMS Technologies
## ACID Properties
Le proprietà ACID sono un acronimo che stanno per:
- **A** (Atomicità): richiedono tecniche distribuite con 2 phase commit (da vedere cosa intende per phase commit.), una transazione può avvenire o non avvenire (booleana)
- **C** (Consistenza): cioè che i dati siano consistenti e non hanno repliche.
- **I** (Isolazione): Una transazione che avviene sulla stessa base di dati in modo isolata.
- **D** (Durabilità): Il dato è salvato dentro i db e non si potrà modificare

## Distributed Query Optimization
*Distributed query optimization* questa è una query che viene ricevuta in un DBMS e che dovrà eseguire. Queste **query sono separate in sottogruppi che vengono mandate singolarmente a diversi DB**

Tramite il 2 phase commit, si cerca di risolvere delle problematiche dovute alla indisponibilità del nodo o di problemi alla rete, in cui per riconoscere il nodo dentro la rete si mandano pacchetti di ACK (Acknowledgement).

## 2 Phase Commit

>[!info] Obbiettivo
>L'obbiettivo del 2 phase commit è quello di concludere il messaggio della transazione distribuita.

Si pensa alla transazione parallela come un matrimonio, dove il prete è colui che gestisce il matrimonio e fa sposare la coppia. La coppia invece sono i partecipanti che **devono essere entrambi d'accordo per sposarsi**.

### Ruoli del 2 Phase Commit
All'interno della transizione distribuita questi due ruoli sono definiti in termini tecnici come:

- **Transaction Manager** (**TM** ): colui che coordina la transazione che viene svolta tra due RM.

- **Resource Manager** (RM): che sono i diversi server DBMS che vogliono svolgere la transizione loro.

>[!warning] N.B
>Ogni attore può essere un TM, anche il cliente può diventare un Transaction Manager.

Ogni TM e RM contengono al loro interno dei **Log** che sono necessari per salvare gli stati che possiede il TM, che sono:
- **Prepare**: contengono gli ID dei vari resource managers (RMs) che partecipano alla transazione (Node ID + Process ID)

-  **Global Commit** / **Abort**: la decisione che ha svolto il TM per la transazione che sta gestendo.

- **Complete**: scrive il risultato alla fine della transazione.

Mentre I RM nei loro log contiene un messaggio di ***Ready*** dove una RM vuole cominciare una transizione che tale transizione, dopo aver deciso di cominciare **non è possibile fermarla / modificarla** una volta iniziata.
==(DA COMPLETARE)==
# X-Open-DTP
E' un protocollo di coordinazione dei 2-phase commit, cioè un **protocollo per gestire le transizioni parallele**. Questo protocollo ha come base:
-  Un singolo cliente
- Un singolo TM
- Diversi RMs
## Interface
Definisce un interfaccia tra client TM chiamata **TM Interface** e l'interfaccia tra TM e RM che viene denominata come **XA Interface**, che sono le interfacce che sono offerete dai DBMS
## Standard Features
Gli RM sono elementi passivi che ricevono delle richieste di operazioni da parte dei TM, nella quale tali **TM hanno il controllo del protocollo**.

Tale protocollo possiede due ottimizzazioni:
1. [[#Presumed Abort|Presumed Abort]]
2. [[#Read Only|Read Only]]

Ci sono delle decisioni euristiche che possono modificare l'evoluzioni delle transizioni in caso si presenti dei fallimenti.

### Presumed Abort
Quando il TM non possiede nessuna informazione nei propri log riguardo alla transizione, quando un RM invia una richiesta di recovery, la TM va a **rispondere con un abort**.

Questo approccio andrà a ridurre il **numero delle chiamate sincrone** nei log, ma alcune operazioni sincrone servono ancora per il global commit che deve eseguire il TM e il ready commit che deve eseguire il RM.
### Read Only
Viene scoperto dal RM quando scopre che non è stata volta una modifica nel suo database, durante la transizione.
