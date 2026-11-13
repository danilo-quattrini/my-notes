---
created: 2026-10-21
tags:
  - baby
topics:
  - Cybersecurity
author: Danilo Quattrini
---
# Routing Essential
---
## Tassonomia

## Forwarding (Inoltro)
Operazione a piano dati (*data plane*), cioè trasmettere un pacchetto da un router ad un altro router. Non c'è nessuna decisione in tempo reale, ma i router guardano la routing-table in tempo reale. Quando il router riceve il pacchetto e decidere cosa farsene del pacchetto, dove i router si mettono d'accordo sul percorso da scegliere.![[Screenshot 2026-10-21 at 17.56.41.png]]

Vedremmo la fase di *control plane*, data una topologia del genere.![[Screenshot 2026-10-21 at 17.58.15.png]]

>[!example] Esempio
>Prendiamo come esempio i cartelli stradali, in questo caso ogni router possiede dei cartelli stradali, che indirizzano il pacchetto a dove andare per poter raggiungere una specifica direzione
### Procedure di Forwarding
Si fa forwarding con l'indirizzo di destinazione, ma non è l'unico modo che si chiama label swapping, dove si assegnano delle etichette a dei percorsi, che queste vengono visualizzate e inviate ad altre etichette (vedere con MPLS da collegare).

Esiste un altro modo che si chiama *Source Routing*, dove si viene a scrivere nel pacchetto l'intero percorso che deve fare il pacchetto. Cioè il pacchetto già possiede la strada che deve percorrere, questo approccio funziona se e solo se l'**host ha una visione della topologia**, cosa che all'inizio la rete non ha presente e non è spesso usato nelle case ma **usate nei data-center**.

>[!info] Routing vs Forwarding
>Non confondersi Routing con il forwarding, sono cose completamente differenti.

### Forwarding Process
Per fare Routing e Forwarding servono informazioni diverse, per le informazioni che servono per il routing utilizziamo una **Routing Information Base** (RIB) che sono delle tabelle di routing che presenta le liste di destinazioni presenti nella rete, mentre per il forwarding si utilizza il **Forwarding Information Base** (FIB), che è lo stesso una tabella ma è ordinata in modo che possa velocizzare il processo dei pacchetti.

## Algoritmi di Routing
Si dividono in due famiglie:
1. **Non adattativi**
	-  Static Routing
	- Manual Configuration
2. **Adattativi**

### Non Adattivi

#### Fixed Directory Routing
#####  Static Routing
![[Screenshot 2026-10-21 at 18.23.49.png]]

##### Manual Configuration
![[Screenshot 2026-10-21 at 18.20.17.png]]

**Funziona se l'operatore sa tutto**, ma non è facile sapere la topologia, molto facile fare gli errori e mandare in malfunzionamento qualcosa. **Va bene nei laboratori** dove ci sono pochi router e le **reti sono piccole**
#### Selective Flooding & Similar
##### Random
Non utilizzato
##### Flooding
Stesso come lo switch
##### Deflection or  "hot  potato"
Server per minimizzare il tempo che il router manda il pacchetto da una porta ad un altra se non è disponibile lo manda ad il router più vicino. 

### Algoritmi Adattivi
Ci sono diversi algoritmi
- Router Centralizzato
- Isolated Routing
- Distributed Routing
	- Distance Vector
	- Link State

#### Router Centralizzato
C'è un nodo chiamato **Routing Control Center** (RCC), che colleziona le informazioni da altri nodi. Questo approccio è molto simile a quello dell'operatore, solo che in questo caso è un programma. Il nodo centrale riesce a capire anche se la rete è congestionata oppure no
![[Screenshot 2026-10-21 at 18.35.50.png]]

In questo approccio ci sono dei vantaggi relativi all'**ottimizzare le performance e semplificare l'individuare le problematiche**. Però c'è il single point of failure e un bottleneck, perché il nodo centrale si deve gestire un bel pò di pacchetti.

#### Algoritmi Distribuiti
I router collaborano tra di loro e ci sono due grandi famiglie, che sono il distance vector, dove ho delle informazioni parziali e ce le facciamo bastare.

Cosa fanno gli algoritmi di **Distributed Routing**?

Ogni router genera informazione riguardo alla raggiungbiltà della rete locale, ricevono anche le informazioni della raggiungibilità della rete remota. Infine propsagano le informazioni riguardo alla raggiungiunbilità della rete remota![[Screenshot 2026-10-22 at 16.11.23.png]]

##### Algoritmo di "choosing criteria"
Gli obbiettivi che possiede questo algoritmo sono:
- Network coerenti per evitare i loop, oppure buchi neri (da vedere nel dettaglio, però un router che non sa dove mandare un pacchetto e lo scarta)
- Algoritmo devono operare in modo automatico, dando il minimo indispensabile al router

Un modo per raggiungere la consistenza è usare il criterio di "optimal", secondo a delle metriche che ci siamo definiti noi.
![[Screenshot 2026-10-22 at 16.11.49.png]]

Quali sono però le metriche che possiamo utilizzare, uno potrebbe essere:
1. La minima distanza, che potrebbe essere quantificato in KM o Metri, che però serve un meccanismo per misurare la distanza, questa distanza **possiamo farla in base al numero di router lungo il percorso (number of hops)** 
2. **Riduzione del delay** è una metrica anche importante per quanto riguarda il tempo che il pacchetto passa da un router ad un altro.
3. **Posso combinare più criteri tra di loro**, sia quello della minima distanza che quello della minimum delay

Scegliamo il criterio che vogliamo ma lo dobbiamo far seguire a tutti i router, che però dobbiamo ricordare che il **router deve calcolare il traffico**. Si possono accettare delle instabilità ma solo nel transitorio, dopo **si deve avere della consistenza**.

## Algoritmo di "Distance Vector"
Promo algoritmo proposto per il routing, dove ogni router manda periodicamente ai nodi adiacenti, un informazione che si chiama *distance vector*. Questa **informazione è un vettore che indica  la distanza (intesa come numero di hop)**. Ogni nodo deve mantenere anche due dati, che sono la **Distance Table** (DT) e la **Routing Table** (RT) dove per ogni destinazione possiede il *next hop*.

La distance vector ha le stesse informazioni della routing table solo che **non possiede il next hop**. La scelta del percorso si fa con l'algoritmo di *Bellman-Ford*, che sarebbe questa equazione:
>[!quote] Formula
>Avendo un router $x$, per raggiungere una destinazione $y$ $D_{x}(y)$, scegliamo fra tutti  i vicini $v$, scegliamo il vicino che ha il costo minore (questa funzione è ricorsiva):
>$$D_{x}(y)=min_{v}\{c_{x,v} + D_{v}(y)\}$$
>![[Screenshot 2026-10-22 at 16.56.58.png]]

>[!example] Esempio
>![[Screenshot 2026-10-22 at 16.58.42.png]]
>Lo scopo e raggiungere $z$ partendo da $u$, all'inizio i nostri vicini hanno questo costo
>- $c_{u,v} = 2$
>- $c_{u,x} = 1$
>- $c_{u,w} = 5$
>  
>  Poi abbiamo che i nodi vicini {$v, x, w$} hanno comunicato i costi che impiegano per arrivare a $z$, non si sa come ci comunicano (cioè si però hanno fatto dei loro calcoli loro)
>  ![[Screenshot 2026-10-22 at 17.03.26.png]]

### Distance Table
![[Screenshot 2026-10-22 at 17.05.38.png]]

La distance table è fatto come la figura sopra, che vediamo  per ogni nodo, **quanto ognuna di loro costano per raggiungere il nodo successivo o quello più lontano**. Dalla distance table passiamo passare alla routing table, semplicemente prendendo dalla distance table il next hop.
![[Screenshot 2026-10-22 at 17.06.57.png]]

#### Problemi con il "Distance Vector"
1. **Black Hole**: quando il router scarta un pacchetto
2. **Non si ha una visione globale della rete**
3. **Count Infinity**: specifico per il distance vector:
   >[!example] Esempio
   >![[Screenshot 2026-10-22 at 17.40.36.png]]
   >Ogni router ha il suo punto di vista a sinistra c'è il router B che ha la sua **distance table**, poi c'è il router C che la **distance table** sulla destra. C'è un guasto tra A e B, il router B invalida la distance table A, poi il router B manda il Distance Vector A a C, cambiando il costo di A ad 2 a 3 e questo processo lo fa all'infinito mandandosi questi cambiamenti a vicenda.
4. **Bouncing Effect**: si possono creare dei loop causate dalle informazioni inconsistenti, strettamente collegato al **counting to infinity**![[Screenshot 2026-10-22 at 17.49.46.png]]
   Simile al **broadcast storm** (che però non si poteva risolvere se non staccando la rete), però questo bouncing effect andrà a finire quanto il **TTL termina**

#### Soluzioni Per il Counting Effect
- Split Horizon
- Path Hold Down
- Route Poisoning
##### Split Horizon
Se il router C raggiunge la destinazione A, tramite B **è inutile per B provare a raggiungere A tramite C**.
![[Screenshot 2026-10-22 at 17.52.42.png]]

Quando c'è un guasto B ricalcola la routing table, B non ha comunicato la nuova modifica, B **diventa un buco nero che è meglio piuttosto che causare un counting effect**.

##### Path Hold Down
L'idea è che se c'è un guasto tutto le destinazioni raggiungibili da L, allora da quel router tutte le destinazioni non sono raggiungibili.
![[Screenshot 2026-10-22 at 18.00.43.png]]

Cioè si mette in quarantena il router **B**, facendo si che faccio passare i pacchetti in un determinato router invece che al router che sta in quarantena. Si possono combinare le soluzioni **Path Hold Down** con lo **Split Horizon**, perché da solo questa soluzione non funziona.

>[!info] Queste problematiche come avvengono?
>Queste problematiche avvengono perché i router hanno aumentato i costi, però questo andrà a bloccare delle rotte specifiche.

##### Poisoning Reverse
Una rotta invalida è annunciata ma andrà ad avere un costo infinito, invece di omettere la rotta. Questo approccio è molto più aggressivo 
![[Screenshot 2026-10-22 at 18.06.42.png]]

B annuncierà a costo infinito il raggiungimento di A, indicandone che è impossibile raggiungere tale router

### Bottom Line
>[!done] Vantaggi
>- Semplice da implementare
>- Configurazione molto facile

==(Completare con i cons)==
### Path Vector (Variant of Distance Vector)
Si manda anche l'informazione dei nodi attraversati, oltre alla distanza si mandano anche i vari path. Questo approccio andrà a far si che si vanno a **ridurre i loop**, ma con un costo di complicanza elevato.
![[Screenshot 2026-10-22 at 18.18.03.png]]

## Link State
**Ogni nodo manda dei costi relativi ai suoi link in broadcast a tutti gli altri nodi**. Nel Distance Vector si conosceva solo i vicini, mentre nel Link State, un nodo manda in broadcast l'informazione dei suoi link. 

>[!example] Esempio
>![[Screenshot 2026-10-22 at 18.20.58.png]]
>Il router A manda in broadcast a tutti i suoi vicini che lui è collegato con B, C e D, e poi la stessa cosa lo fa B con i sui vicini, notificandoli che lui è collegato ad A, F e G

Ogni nodo si costruisce la topologia sapendo l'informazione dei link, scoprendo tutti i link che sono nella rete, applicando l'algoritmo di Dijkstra per lo shortest path
![[Screenshot 2026-10-22 at 18.27.34.png]]

Ogni nodo della rete hanno le stesse informazioni, con diverse routing table, ma con il link state tutti i nodi partono con la stessa base.

## Routing Protocols
![[Screenshot 2026-10-28 at 16.13.19.png|1040]]

I protocolli di routing sono in grado di scambiare informazioni sulla rete e determinare il percorso migliore. I router si mandano dei pacchetti che servono per vedere se sono attivi oppure no. 

I protocolli sono tra il livello 3 e il livello 4, ogni ISP ha un proprio dominio con dei propri router, quando abbiamo parlato di algoritmi di [[#Link State]] questi non possono essere globali, perché ogni amministratore vuole avere il controllo sulla rete, questo vien definito come

### Autonomous System
Gli **autonomous system** sono delle sotto-reti raggruppate in base alla topologia  e a dei criteri di organizzazione (questo potrebbe essere per esempio un ISP), che possono mandarsi le stesse informazioni sa hanno un guasto.

Gli autonomous system vengono identificati tramite un numero a  byte, però siccome non bastavano più allora si sono aumentati a 4 byte, dove da prima che si aveva $2^{16}$ combinazioni, si sono passati a $2^{32}$

### Internet approach to scalable routing
Ci sono due approcci che sono presenti in un autonomous che sono:
- **Intra-AS routing**: ci saranno i routing tra gli host e routing tra gli host
- **Inter-AS routing**: ci sarà un routing tra AS e il gateway performa un inter domain router come fa lo stesso anche gli intra AS

## Intra-AS Routing
Anche conosciuto come *interior gateway protocol* (IGP), dove i più comuni sono:
- [[#OSPF]]
- [[#IGRP]]
### OSPF
*OSPF* (Open Shortest Path First) è un protocollo pubblico e disponibile per tutti i router che utilizza l'algoritmo di link state, il costo dei link è definito dalla formula $1$ diviso la banda del canale che comunicano tramite IP.
#### Feature avanzate
- **Sicurezza**: permette che tutti i messaggi OSPF devono autenticarsi prima di entrare in un router
- **Multiple**: percorsi che hanno lo stesso costo, con OSPF si possono usare entrambi ![[Screenshot 2026-10-28 at 16.44.07.png]]
- **Diverse metriche per lo stesso link**: ci sono diversi costi per Type of Service (TOS), in base al type of service presente nel pacchetto IPv6 che viene mandato tra i router.![[Screenshot 2026-10-28 at 16.49.09.png]]
  Per esempio si possono adottare due approcci, uno è quello di fare due tabelle distinte per il tipo di servizio![[Screenshot 2026-10-28 at 16.53.26.png]]
  
  Un'altra soluzione abbiamo invece una singola tabella dove c'è una colonna  in più per il TOS che però non è quella conveniente perché andiamo a cambiare l'algoritmo per  decodificare il pacchetto.![[Screenshot 2026-10-28 at 16.55.33.png]]
- **Supporto uni-cast & multi-cast**: viene denominato come Multicast(OSPF), che usa lo stesso database dello **OSPF**
  
#### Gerarchia OSPF
![[Screenshot 2026-10-28 at 17.01.26.png]]

>[!info] Importante
>Area di livello inferiore non possono comunicare tra di loro direttamente, ma devono passare dall'area 0 per comunicare. Esempio se `Area 2 ` deve inviare un messaggio ad `Area 1`, devono passare prima sopra in `Area 0` poi in `Area 2`, in questo ordine `Area 2 -> Area 0 -> Area 1`

Forma gerarchia a due livello, dove c'è l'`Area 0`(Area di **backbone**) dove si mettono i router più costose, mentre le aree sottostanti sono quelle che sono connesse nelle periferie


## Inter-AS Routing
Tra diversi AS ci sono diversi fattori su come instradare il traffico, dove per esempio ci interessa solo le performance oppure la policy domina sulle performance, questo per esempio in un:
- **inter-AS**: l'admin vuole il controllo sul traffico della sua rete.
- **intra-AS**: singolo admin che non c'è bisogno di controllo.

>[!example] Esempio per ragioni Economiche
>Una rete può preferire un percorso più lungo per ragioni economiche
>![[Screenshot 2026-10-28 at 17.13.43.png]]

>[!example] Esempio per  ragioni di Sicurezza
>![[Screenshot 2026-10-28 at 17.15.09.png]]
>Esempio se dobbiamo far si che la rete A vuole evitare di passare in B perché non si fida della rete, quindi prende un percorso lungo


>[!example] Esempio Route Hiding
>Inter-AS possono propagare parzialmente la connettività ad altri router.
>![[Screenshot 2026-10-28 at 17.17.54.png]]
> cioè se una rete A vuole comunicare con B, quest'ultimo non gli dice che conosce la rete C

## BGP (Border Gateway Protocol)
**BGP** (Border Gateway Protocol) è un protocollo che serve per fare comunicare AS / Operatori tra di loro. Possiede dei meccanismi per sapere la raggiungibilità degli AS e un meccanismo per propagare questa informazione sulla rete.

Ogni operatore usando BGP può annunciarsi agli altri AS comunicando che è disponibile sulla rete, che questo protocollo aiuta a capire se un router è raggiungibile oppure no.

**eBGP**: dove comunicano tra AS differenti
iBGP: comunicano invece nella stessa AS
### eBGP, iBGP connections
![[Screenshot 2026-10-28 at 17.43.08.png]]

### BGP Basics
Due reti AS differenti che usano il protocollo BGP comunicano tramite una connessino TCP

Si mandano messaggio di prefisso + attributi che si mandano la lista degli Autonomous System. Dove ci sono due importanti attributi:
1. **AS-PATH**: lista di Autonomus Systems indicando il prefisso si è mandato
2. **NEXT-HOP**: indica il router dentro l'AS fino al router successivo (next-hop)

### BGP Messages
I messaggi che si mandano tra AS sono attraverso una connessione di tipo TCP, dove si hanno i seguenti messaggi:
- **OPEN**: apre la connessione TCP fra AS mandano un pacchetto BGP peer per autenticarsi
- **UPDATE**: annuncia dei nuovi percorsi (o ne prende alcuni vecchi)
- **KEEPALIVE**: mantiene aperta la connessione in assenza di un update da parte di un AS
- **NOTIFICATION**: manda un messaggio in caso di errore, questo viene anche usato per notificare la chiusura di una connessione.

### BGP path advertisement
![[Screenshot 2026-10-28 at 18.09.14.png]]
Avendo una topologia di rete del genere un AS3 manda un *path advertisement* `AS3, X` tramite eBGP verso l'AS2 con il router 3a, L'AS2 per le policy che possiede mettiamo caso che accetta il pacchetto da AS3, il pacchetto che l'ha ricevuto lo manda in tutta la sua rete interna.

Dal route 2a l'AS2 manda il path advertisement ricevuto prima da AS3 verso l'AS1 tramite eBGP al router 1c questo per le policy che possiede AS2 fa questa operazione.

### Tabelle di Forwarding di BGP e OSPF
![[Screenshot 2026-10-28 at 18.13.47.png]]

### BGP Route Selection
Un router di un AS può voler conoscere di più di un router presente in un altro AS, per poter svolgere una scelta in base a:
- preferenza delle policy locali che possiedono
- Il percorso AS più corto
- Il router più vicino 
