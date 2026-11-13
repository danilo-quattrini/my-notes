---
created: 2026-10-07
tags:
  - baby
topics:
author: Danilo Quattrini
---
# IPv4 to IPv6
---
## Questions
---
- Come funziona la transizione?
- In quanti modi avviene la traduzione?
- Quali sono le limitazioni di un approccio dual-stack?
### Tunneling
- Come funziona il tunneling?
- Quali sono i due modi per trasformare un datagramma IPv6 ad IPv4, per far si che un IPv6 possa essere letto da un router?
- Come funziona la soluzione 6to4?
- Come mai la soluzione 6to4 è inutilizzata?
- Quali sono le limitazioni che non permettono alla soluzione 6to4 di mantenersi?
### Scalable Carrier-grade Solutions
- Quali sono i tipi di router che andremmo ad utilizzare nelle nostre soluzioni?
- Il NAT viene utilizzato ancora oggi, oppure presenta delle problematiche?
- Quale router andremmo ad introdurre nell'architettura IPv6, in una **scalable carrier solution**?
---
## Idealmente Cosa Succede?
Dobbiamo fare si che avvenga in modo **incrementale**, cioè i sistemi operativi devono supportare IPv4 e IPv6 simultaneamente, cioè si devono gestire entrambi i protocolli. Poi tale transizione deve essere **seamless** (senza interruzioni), cioè il passaggio deve avvenire in modo smooth senza che ci siano cambiamenti bruschi, per l'host deve essere tutto trasparente.
## Come si può fare la traduzione da IPv4 a IPv6?
![[Screenshot 2026-10-07 at 16.48.54.png]]
Il primo è quello di apportare un approccio **dual-stack**.
C'è un meccanismo di mapping (Address Mapping) fatto o dal router o dall'host stesso, cioè un algoritmo che va da 32 bit a 128 bit, se dovessimo trasformare un IPv6 ad un IPv4 che tendenzialmente non si fa però ci serve si usa un algoritmo che fa tale lavoro. Cioè un host IPv6 deve poter comunicare con un host IPv4

Il secondo **meccanismo che è il tunneling** dove prendiamo un pacchetto IPv4 lo imbustiamo dentro un IPv6, cioè Tunneling vuol dire aggruppare da una scatola IPv6 all'IPv4, cioè imbustare IPv4 dentro IPv6.
![[Screenshot 2026-10-07 at 16.51.34.png]]

L'ultimo meccanismo di traduzione è il **Translation Mechanism**, che invece di fare tunneling, fa direttamente la traduzione, questa operazione viene eseguita da un router che riceve IPv4 e IPv6 che dovrà tradurre in base alle esigenze della rete al quale deve mandare il pacchetto. Oltre a cambiare l'header il router dovrà capire cosa mettere nel [[IP#Datagramma IP|datagramma]] nell'indirizzo sorgente e destinazione.
### Step 1: Isolated IPv6 Connection
![[Screenshot 2026-10-07 at 16.55.11.png|1106]]
Ora che le reti stanno adottando il nuovo protocollo IPv6, dobbiamo avere reti che vanno ad interpretare IPv6
### Step 2:  Dispositivi che convertono IPv4 a IPv6
Si avranno dei router che andranno a fare una conversione da IPv4 a IPv6
![[Screenshot 2026-10-07 at 16.56.46.png]]
Oggi molti operatori hanno convertito la rete da IPv4 ad IPv6 e quindi comunicano nella stessa rete senza fare traduzioni o tunneling. Nonostante il supporto c'è in qualunque dispositivo, ma per ora siamo in una situazione in cui alcuni router gestiscono IPv6.
### Dual Stack Limitation
Ci sono delle limitazioni ad utilizzare l'approccio **dual-stack a lungo** andare, perché andremmo sempre ad utilizzare un IPv4 e questo non possiamo deciderlo noi ma dal sistema operativo, per questo ci sono anche problematiche tra la comunicazione tra dispostivi IPv4 e IPv6, che si evolvono in questi scenari:
- Host IPv6 che vuole comunicare con un host IPv6 su una rete IPv4

- Host IPv6 che vuole comunicare con un IPv4, dove un meccanismo di traduzione deve essere applicato, ma solo nel caso volessimo fare una comunicazione tra un host IPv6 ad un host IPv4, la **comunicazione inversa non può avvenire**.
### Tunneling Solutions
![[Screenshot 2026-10-07 at 17.18.52.png]]
Cioè faremmo tunnel da IPv6 ad IPv4, questo nel caso volessimo che un host IPv6 posso inviare dei dati attraverso una rete IPv4, come vediamo nell'immagine. Questo è il caso più comune oggi giorno che ci andremmo a lavorare sopra attraverso il semplice tunneling.
#### Traversing a IPv4-only Network
![[Screenshot 2026-10-07 at 17.21.29.png]]
Il router che legge IP sia IPv4 o IPv6, e deve fare la conversione, incapsula l'IPv6 dentro ad un datagramma IPv4. Al livello IPv4 mettiamo come sorgente.
![[Screenshot 2026-10-07 at 17.24.13.png]]
Come si fa tunneling, mettiamo nel campo protocol del [[IP#Datagramma IP|datagramma]] IPv4, il numero `41`, identificandolo come datagramma IPv4. Fanno questo passaggio di pacchetti IPv4 perché hanno solo bisogno di leggere l'header del protocollo IPv4, non gli interessa il contenuto del pacchetto.

Alternativa usiamo il protocollo **[[Virtual Private Networks (VPN)#GRE - Generic Routing Encapsulation|GRE]]** (Generic Routing Encapsulation), che non fa altro che creare un canale, mettendo il protocollo nel mezzo tra IPv4 e IPv6.
![[Screenshot 2026-10-07 at 17.27.24.png|1120]]
Se non ci sono queste protocolli si possono impostare a mano, in modo manuale, cioè a partire dall'IPv6 di H2, capiamo i 32 bit che vogliamo inviare.

Per la soluzione manuale ed automatica ci sono diverse soluzioni in base a se utilizzano i bit degli host oppure della network:
- **Host Centered**: 
	- IPv4-compatible addresses, 6over4
- **Network Centered**:
	- [[#Basic 6to4 Scenario|6to4]]
	- Tunnel Broker
	- ISATAP
	- Teredo
 Queste soluzioni però sono deprecate e non sono utilizzate.
##### Basic 6to4 Scenario
![[Screenshot 2026-10-07 at 17.35.41.png]]
C'è una rete IPv4 nell'intermezzo tra due reti IPv6, nella rete a sinistra c'è  la Rete 1 c'è il prefisso di rete che comincia con `2002::/16` che non tocchiamo e i seguenti 32 bit  `c001:0203`, mentre nella rete due c'è sempre lo stesso prefisso iniziale, ma con dopo i 32 bit a `09fe:02fc`, questi prefissi dopo i primi 16 bit (convertiti in binario) saranno trasporti ed utilizzati come IPv4 da dare al router per la rete che deve usare comunicare nella rete `IPv4 Internet`
>[!example] Esempio
>Se prendiamo il valore `c0010203` e lo convertiamo in binario come 
>```
>1100 0000 0000 0001 0000 0010 0000 0011
>```
>e creeiamo sottogruppi da 8 bit da questo numero binario, in questo modo:
>```
>11000000.00000001.00000010.00000011 -> 192.1.2.3
>```
>e convertiamo ogni ottetto in decimale avremmo il nostro IPv4, ecco la soluzione 6to4

Sfortunatamente però da questa soluzione **non ho libertà nei creare i prefissi nelle mie subnet IPv6,** sono soluzioni temporanee e non possiamo scalare la rete IPv6.
## Scalable Carrier-grade Solutions
Questa sono soluzioni utilizzata oggi giorno e sono chiamata **Scalable Carrier-Grade Solution**, sono soluzioni scalabili per garantire l'estendibilità della rete in futuro. In questo scenario andiamo ad analizzare host IPv6 che vogliono comunicare tra di loro, ma che nel mezzo c'è una rete ancora IPv4.![[Screenshot 2026-10-07 at 17.42.09.png|1120]]
Oppure host IPv4 che parlano con IPv4, ma sono su un canale IPv6![[Screenshot 2026-10-07 at 17.42.36.png|1120]]
Questi sono i due scenarii che andiamo a considerare nei seguenti capitolo.
### NAT is widely use today
Dentro casa avremmo diversi dispositivi collegati alla **CPE** (Customer Premises Equipment) che ci offre il nostro ISP, che quel CPE fa da NAT (come vediamo dall'immagine sotto si trova sopra al CPE) che però noi siamo collegati con il [[NAT|NAT]]44, dove in questa soluzione stiamo adattando un IPv4 privato ad uno pubblico (scenario classico domestico).
![[Screenshot 2026-10-07 at 17.43.51.png]]

Oggi anche nei dispositivi mobile vengono utilizzati IPv4 privati, che vengono chiamati come LSN (Large Scale NAT), perché è un NAT su larga scala, oppure si usa anche il termine di CGN (Carrier Grade NAT), viene chiamato così perché il NAT gestirà molti dispositivi diversi su larga scala.
![[Screenshot 2026-10-07 at 17.45.08.png]]
L'ultima configurazione è spesso presente negli operatori come Fastweb, dove ci sono due livelli di NAT, uno il classico CPE ed un'altro che è il **Large Scale Nat**(LSN), questa soluzione andrà ad evitare tanti indirizzi IP pubblici.![[Screenshot 2026-10-07 at 17.46.44.png]]
#### Problems with NAT
Il NAT però presenta dei problemi che sono importanti da considerare, come ad esempio, problemi per quanto riguarda la raggiungibilità dell'host all'esterno (definito come NAT Traversal), si risolve configurandolo a mano il NAT nel router. Oltre alla comunicazione con l'esterno che risulta problematica, il NAT è un **single point of failure**, che si trova a gestire tante connessioni da diversi host.
#### Same Architecture with IPv6
Se volessimo utilizzare IPv6 avremmo le stesse soluzioni, ma avremmo anche host dual-stack.
![[Screenshot 2026-10-07 at 17.49.39.png]]
Nelle prime due righe i router fanno anche da translation (che sono i router **AFTR** = address family transition router) che ricevono IPv6 e poi vanno a tradurli in IPv4 per soddisfare . Perché l'operatore nella linea privata ha un IPv6 ma dovremmo raggiungere comunque un'IPv6.

Nell'ultimo caso avremmo host con IPv6, ora avremmo solo un problema di traduzione e non più di tunneling. Le soluzioni come viste nell'immagine sono 3:
- [[#DS-Lite (Dual-Stack Lite)|DS-Lite]] (Dual Stack Lite)
- [[#A + P Address Plus Port| A + P]] (Address Plus Port)
- NAT64
##### AFTR address family transition router
Sono dei dispositivi che permettono di far si che gli host IPv4 possano comunicare tra di loro in una rete IPv6, tramite un meccanismo di traduzione. Usato in DS-Lite e A + P
![[Screenshot 2026-10-14 at 14.41.31.png]]
### DS-Lite (Dual-Stack Lite)
![[Screenshot 2026-10-07 at 17.54.28.png]]
Ci sono due casi
1. Host IPv6 che  con un altro host IPv6, non c'è nessun problema, quì non c'è la necessità di fare tunneling e niente (sull'immagine sarebbe il computer con il 6 rosso e con la lineea rossa).
2. In questa soluzione c'è il tunnel, dove il router CPE fa tunnel fra se stesso e la AFTR oppure chiamato anche CGN, nel CGN si fa anche NAT. Quindi il router CGN si trova a terminare il tunnel che si era creato tra il router CPE e se stesso,  inoltre va a fare anche da NATTING (chiamato NAT44 perché è a livello IPv4), traducendo il pacchetto l'IPv6 che incapsula IPv4 e mandarlo in internet.
![[Screenshot 2026-10-07 at 17.58.35.png]]
Il pacchetto inviato dalla CPE viene mandato poi alla CGN che verrà inviato poi all'host 2 (H2) che risponderà verso l'IP pubblico della CGN e non verso H1. Il NAT faceva associazione tra IPv4 sorgente con l'IPv4 Destinazione con le loro porte.

Questo sotto è il comportamento base del NAT, senza IPv6, in DS-Lite, deve invece anche capire l'indirizzo IPv6 della CPE, per fare tunnel inverso
![[Screenshot 2026-10-14 at 15.07.46.png]]
La CPE per poter inviare il pacchetto incapsulato (cioè che IPv4 viene incapsulato in IPv6), deve conoscere l'AFTR (o CGN), per conoscerlo la CPE deve essere**configurata mano  fornendo l'indirizzo IP della router AFTR** oppure viene utilizzato anycast
>[!done] Vantaggi
>- Riduce la necessità di utilizzare IPv4 a differenza di un approccio dual-stack

>[!danger] Problemi
>- Il NAT non è sotto il controllo del cliente, stessa cosa vale per la CGN
>- Problematica con i server, le mappe statiche e le porte non possono essere configurate
>
### A + P Address Plus Port
![[Screenshot 2026-10-07 at 18.09.27.png]]
Ora in questo scenario il NAT è sotto il controllo dell'utente, cioè l'operazione di Natting lo fa il CPE, in cui la tabella di natting sarà molto più piccola, perché ci sono pochi dispositivi connessi.

Tutto il resto è uguale, nello scenario sopra prima si manda il pacchetto IPv4 alla CPE, poi si fa tunneling tra la CPE e AFTR, dove il pacchetto IPv4 viene incapsulato in IPv6. L'AFTR alla fine farà la traduzione per la rete **IPv4 su Internet**.

L'accortezza è che ora nel router CPE, l'IP sorgente inviato dall'host 1 viene modificato con l'indirizzo pubblico della CPE e anche la porta viene cambiata in modo che si possa fare l'operazione di mapping. Cioè che cosa intendo con operazione di mapping? Intendo che  al ritorno del pacchetto inviato dalla AFTR, il router CPE tramite l'operazione di natting, dovrà far ritornare il pacchetto che ha ricevuto dalla AFTR all host 1 (cioè a chi ha inviato il pacchetto).

Al ritorno del pacchetto dall'host 2 all'interno del pacchetto che viene inviato dall'host 2 alla AFTR, ci sarà scritto l'indirizzo IP_DEST della CPE insieme anche alla PORT_DEST, sempre della stessa CPE.

La tabella che si gestirà la AFTR sarà una cosa del genere.
![[Screenshot 2026-10-14 at 15.33.24.png|1092]]
Dove associa ogni indirizzo IPv4 della CPE ad un indirizzo IPv6 che ha salvato all'interno del router, questo funziona se per ogni CPE ho degli IPv4 diversi, questa cosa non può piacere, quindi si utilizza un unico IPv4 per ogni CPE. 

Però siccome non si può associare ad un solo IPv4 diversi IPv6, **allora oltre all'indirizzo IPv4 nella tabella AFTR, viene messa anche la porta** (Address + Port ecco da dove prende il nome), funziona se e solo se ogni CPE che fa NAT sulla porta, deve utilizzare un range di porte differenti.

Così posso riciclare lo stesso indirizzo IPv4 pubblico.![[Screenshot 2026-10-14 at 15.39.53.png|1106]]
Come nell'immagine sopra, questo approccio funziona solitamente se ogni CPE sa che range di porte utilizzare, e quando l'AFTR dovrà associare un indirizzo IP ad un determinato CPE non guarderà solo l'indirizzo, ma anche la porta di destinazione. Questo ci permette di risparmiare l'utilizzo di diversi indirizzi IPv4.

**Come vengono assegnate le porte alla CPE?**
Le porte vengono assegnate in automatico alla CPE tramite un protocollo chiamato **PCP**(Port Control Protocol - RFC 6887) oppure attraverso **DHCPv6**
# Reference
---

