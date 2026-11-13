---
created: 2026-10-28
tags:
  - baby
topics:
  - Cybersecurity
author: Danilo Quattrini
---
# Multimedia Networking & Quality of Service
---
# Quality Of Service (QoS)
>[!quote] Definizione
>Quanto la rete performa bene e soddisfa le richieste di un applicazione, come il *delay*, *jitter*, (deviazione del segnale di rete), *loss*, *throughput*

Si deve sempre mantenere la continuità del flusso dei dati, inoltre dove il profilo di un  flusso generato deve essere lo stesso del del flusso che deve trasmettere.

Questo per far si che migliori l'interazione con l'utente e che deve avere una throughput molto basso perché devono mandare immagini e video in tempo reale.

## Engineering QoS for multimedia
**Overprovisioning** cioè l'operazione di potenziare la rete con componenti hardware in modo da ridurre i tempi di latenza.

>[!example]
>Prender un cavo da 1 Gbs ad 10Gbs andando a potenziare il cavo però non creeiamo potenza, ma stiamo creando congestione, questo perché il router deve gestire più pacchetti in entrata.
## Streaming Apps Requirements
Fornire dei ritardi sotto i 150ms, per far si che la comunicazione sia naturale e veloce. Poi la perdita dei pacchetti deve essere ridotta tra 1 ai 2 pacchetti

## Supportare il QoS
Per il supporto del quality of service ci sono diverse tipologie di tecniche che vengono applicate per la gestione dei pacchetti sulla rete:
- [[#Classificazione del traffico|Classificazione del traffico]].
- [[#Algoritmi di scheduling dei pacchetti]].
- [[#Controllo del Traffico sulla Rete]] in entrata sulla rete in diversi livelli.

>[!info] In parole povere
>Bisogna limitare il numero dei pacchetti che arrivano ai nodi della rete e far si che si gestiscano i pacchetti che devono arrivare prima di altri.
### Classificazione del traffico
La classificazione del traffico può avviene direttamente nel header del [[IP#Datagramma IP|datagramma IP]] e TCP/UDP. ![[IMG-Multimedia Networking & Quality of Service-20261111.png]]Oppure può essere gestita direttamente tramite degl'algoritmi complessi oppure delle implementazioni hardware di due tipi:
1. **ASIC**:  Application Specific Integrated Circuit
   
2. **CAM**: Content Addressable Memory

### Algoritmi di scheduling dei pacchetti
>[!info] Che cosa sono?
Sono degli algoritmi che decidono quale pacchetto deve andare prima nella rete

Questi algoritmi sono gestiti dentro ai router, questi algoritmi sono:
- **FIFO**: Semplice non c'è nessun QoS e segue semplicemente una coda![[IMG-Multimedia Networking & Quality of Service-20261111-1.png]]
  
- **Priority Queue**: il **traffico con maggiore priorità passa per prima**, sulla rete però il traffico che ha minore priorità rimane indietro.![[IMG-Multimedia Networking & Quality of Service-20261111-2.png]]
  Ogni coda possiede la propria priorità (come il check-in che si svolge in aeroporto), rischio di *starving*.

- **Round Robin / Weighted RR**: ogni coda possiede un'ordine per cui passare evitando di sovraccaricare la banda.![[IMG-Multimedia Networking & Quality of Service-20261111-3.png]]
  Si prende ogni singolo pacchetto da ogni coda e si mette un elemento per volta nella rete, andando a creare equità.

- **Weighted Fair Queue / DRR**: approssimare lo sharing dei pacchetti in modo equo, dove ad ogni coda do un peso. (Via di mezzo tra Priority queue e Round Robin)![[IMG-Multimedia Networking & Quality of Service-20261111-4.png]]
  >[!example]
  >Dalla coda blu prenderò un pacchetto, mentre alla coda verde 3 e la coda arancione invece 2, favorendo la coda verde.

### Capacità dello switch
Il tempo di elaborazione del router nel prendere un pacchetto da una coda in una porta A alla porta B, C o D, che questa operazione richiede del tempo.

**Vogliamo che il router sia veloce nel fare questa operazione**, si deve far in modo di avere la velocità di questa operazione, più veloce di quanto gli arriva il pacchetto al suo interno.

![[IMG-Multimedia Networking & Quality of Service-20261111-5.png]]

Lo **Switch Fabric** è il componente interno del router che gestisce il processo di mandare un pacchetto da una porta ad un altro.
### Controllo del Traffico sulla Rete
Il controllo del traffico avviene al livello di:
- **Pacchetto**: tramite lo [[#Shaping e il Policy]
 - **A priori**: cioè prima di creare la rete. 

	 - **[[#Network engineering]]**: cioè come fare la topologia della rete e dove mettere i router più potenti, per potenziare.
	   
	 - **[[#Traffic engineering]]**: decidere come inviare il traffico sulla rete, settando dei parametri [[Routing Essential#OSPF|OSPF]] per bilanciare il carico della rete. Questa posso farla in base a delle previsioni di quanto alto il traffico è nella rete.

#### Shaping e il Policy
Oltre a limitare gli utenti, si vuole che il traffico abbia un pattern da gestire. Cioè controllare come il traffico entra in rete. 

>[!info] Come si fa?
Questo è possibile riducendo il numero dei pacchetti o **riducendo il throughput nella rete**.

**Token Bucket**: si implementa un cesto (*bucket*) dove si mettono dei *token*, e si può mandare i pacchetti sulla rete **se e solamente se ci sono dei token nei bucket**. Questo ci permette di controllare il traffico perché si va a limitare il traffico in base al tempo di generazione dei token, che viene definita da una costante $R$ e la dimensione del bucket $B$. 

**Leaky Bucket**: è come il token bucket, ma non si possiede il *allows bursts*.
![[IMG-Multimedia Networking & Quality of Service-20261111-6.png]]

Il Token bucket utilizzato per il *policing*, mentre con il Leaky vado a svolgere uno *shaping*, cioè che vado a rallentare il pacchetto.

>[!note] N.B
Si possono combinare queste tecniche tra di loro
#### Network engineering / Traffic engineering
Ridimensionare la rete fisica oppure gestire il traffico sulla rete. Quest'ultima è possibile tramite 
una matrice chiamata **Traffic Matrix**.

Questa **Traffic Matrix** è proprio una matrice che possiede come colonne la sorgente, mentre come righe la destinazione.
![[IMG-Multimedia Networking & Quality of Service-20261111-7.png|1040]]
Se in una cella vedo che c'è un eccessivo utilizzo del traffico, allora vado a spostare l'host sorgente per riceve meno traffico. Questo è possibile **monitorando sempre lo stato della rete**.
![[IMG-Multimedia Networking & Quality of Service-20261111-8.png|1040]]
## Integrated Services (IntServ)
>[!warning] N.B
>Questa soluzione non viene utilizzata perché è troppo complesso e non è scalabile.

Primo Framework per la gestione della qualità del servizio, nato nel mondo della telefonia, dove c'è questa **richiesta di riservare le risorse** Reservation Protocol (RSVP).

I router in questo caso riservano delle risorse *per-flow*, svolgendo un *admission control* andando a controllare i pacchetti in entrata.

## Differentiated Services (DiffServ)
>[!info] N.B
> Leggero e più facile da maneggiare, però **è poco efficace**, questo perché crea della frizione nel traffico.

Framework dove non si riserva tutto end-to-end, dove non riservo più per flusso, ma **aggrego andando a classificare i pacchetti in categorie**. 

Creo dei servizi differenziati per classi e non per circuito.

**L'associazione di un flusso ad un classe lo decide l'operatore** e il router per leggere la classe di cui fa parte legge l'header IPv4 o IPv6 e vede il ToS in IPv4, che è presente nel [[IP#Datagramma IP|datagramma IP]] scelto dall'operatore. Oppure il Type of Class che è presente nel [[IPv6#Struttura dell'IPv6|datagramma]] in IPv6.

Lo si utilizza nel core degli ISP, nelle reti Wi-Fi e nelle reti enterprise.
