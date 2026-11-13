---
created: 2026-10-14
tags:
  - baby
topics:
  - Cybersecurity
  - "[[School]]"
author: Danilo Quattrini
---
# Wireless & Cellular
---
## Questions
---
==(concetti da riprendere nella lezione precedente che si è persa 08-10-2026)==

## Architettura di Rete
In un'architettura cellulare è divisa in due parti:
- **Radio Access Network** (RAN)
- **Core Network**
Le **base station**, sono le antenne, poi ci sono degli switch o dei router.
![[Screenshot 2026-10-14 at 16.14.07.png]]

### Procedure
Ci sono diverse procedure:
1. **Registrazione**: cioè l'utente quando entra nella rete deve registrarsi sulla rete, grazie al DB, controlla se l'utente è registrato oppure no.

### Procedure sulla mobilità
#### Roaming
Il roaming la capacità della rete di tracciare nella rete l'utente che si sposta, se mi sposto all'estero, ci sarà un roaming internazionale. Effettuo un roaming ogni volta che mi sposto.

Come fa a tenere traccia della posizione dell'utente, questo tramite dei **Location Area Identifier** (LAI).
![[Screenshot 2026-10-14 at 16.18.11.png]]
Location Update, che aggiorna la posizione dell'utente sulla rete,
##### Location Updating
Procedura nella quale la posizione dell'utente viene aggiornata, un canale di controllo è sempre in broadcast in ogni cella di una LA
##### Paging
La rete per capire la cella corretta, utilizza la procedura di *Paging* è come un ARP request, però in questo caso sarà la LA a mandare un messaggio broadcast ed identifica gli utenti che sono presenti nella LA.
### Handover
Si riferisce alla capacità / procedura della rete di mantenere il servizio della rete all'utente,  quando si cambia / trasferisce da un'antenna / cella ad un'altra, quando il telefono si muove da un'area ad un'altra. Procedura complessa. Ci sono diversi tipi di handover:
- **Intra vs Inter Cell**: Vado a cambiare la frequenza
- **Soft vs Hard**: Soft posso essere connesso ad entrambe alle antenne allo stesso momento.
Le altre non sono importanti
## Evoluzione Della Rete Cellulare
![[Screenshot 2026-10-14 at 16.26.16.png]]

### IG: Prima Generazione
Prima generazione completamente analogica, un'utente una frequenza, tipo FDMA, solo traffico vocale disponibile, qualità del servizio basso, riservato ad utenti business.

### 2G: Seconda Generazione
Servizi avanzati dove si passa da un servizio analogico al digitale, tra cui ci sono gli SMS servizi di crittografia e decodifica avanzata della voce per ridurre la banda necessaria per la comunicazione. In diversi continenti c'erano diverse tecnologie, tra cui:
- IS-95 in USA
- GSM in Europa
- PDC in Giappone
### 2.5G: Extended Second Generation
Tentativo di aggiungere dei router sulla rete, dove c'era la possibilità di transferire i dati in diversi pacchetti
### 3G: Third Generation
Miglioramento del servizio dei dati, ma è stata considerata molto poco era stato un flop.
Non era il servizio che l'utente si aspettava rispetto ai costi, il CDMA (Code Division Multiple Access) è risultato complesso

### 4G: Fourth Generation
Hanno Generato una rete di tipo LTE (Long Term Evolution), con invio dei dati sulla rete a 250 Mb/s usano il MIMO. Inizialmente era solo un servizio dati, che però poi dopo hanno definito uno standard VoLTE (Voice Long Term Evolution), si possono fare chiamate anche VoIP.

### 5G: Fifth Generation
L'idea era quella di sostituire tutte le tecnologie wireless, dove l'idea era quella di utilizzare il 5G per qualsiasi soluzione. La rete deve offrire alta flessibilità e slicing, tramite la SDN (Software defined Networking)l 'introduzione del piano di flessibilità nei dati, e il NFV (Network Function Virtualization) si riferisce al **piano di dati**, dove le funzioni di rete non son più dispositivi hardware ma sono dei software che creano dei container o altri sistemi di virtualizzazione.
- **Piano dati** che a che fare con l'inoltro dei pacchetti nella rete.
- **Piano di controllo** ha a che fare con il controllo della rete e la segnalazione.

Ciò che viene venduto come 5G, non esiste ancora, ma è una 4G in cui è stato modificato il livello fisico, per qualsiasi cosa che si tratti di migliorare la prestazioni riguarda sempre il livello fisico. In realtà non deve essere chiamata 5G ma NSA (Not Stand Alone), la SA (Stand Alone) non vengono venduti agli utenti finali, ma alle aziende.

# GSM: The 2nd Generation
Seconda Generazione servizio unicamente voce ed SMS
## GSM Architecture
![[Screenshot 2026-10-14 at 16.54.53.png]]
E' una tecnologia unicamente a circuito e gli elementi sono i seguenti:

### MS (Mobile Station)
I telefoni
### SIM 
Microprocessore che permette al telefono di funzionare
### Base Station
Divisa in due parti:
- **Base Transceiver Station** (BTS): sarebbe l'antenna che permette al segnale di essere inviato
- **Base Station Controller** (BSC): componente di una Base Station dotato di un'intelligenza esempio, l'entità che manda il messaggio di [[#Paging|paging]], dove manda il messaggio broadcast su tutta la LA (Location Area). Oppure fa la transcodifica da 13 kb/s a 64 kb/s

### Network and Switching Subsystem (NSS)
I nodi di commutazione che si chiamano Mobile switching service, quello che che avrà un (G), sarà quello che è connesso al mondo esterno, nelle NSS ci sono i DB come HLR (Home Location Register), che si occupa di mantenere i parametri in un terminale mobile (telefono)
![[Screenshot 2026-10-14 at 17.00.50.png]]

**Visitor Location Register** (VLR)
![[Screenshot 2026-10-14 at 17.01.49.png]]

## Frequenze del GSM
Ci sono diverse bande, che sono intorno tra i 850Mhz, 900Mhz, 1800Mhz, 1900Mhz, la frequenza in ricezione è diversa da quella trasmessa, questo è gestito dal **FDD**(Frequency Division Duplex), terminale trasmette su una frequenza, ma riceve un'altra frequenza.![[Screenshot 2026-10-14 at 17.04.00.png]]

## GSM: Canali Fisici
E' basata su una FDMA / TDMA, dove in ogni frequenza vado a definire una schema TDMA, dove ogni frame TDM  è diviso in 8 slot. La combinazione fra **frequenza + time slot**, definisce il canale fisico dell'utente a cui è allocato.
![[Screenshot 2026-10-14 at 17.06.43.png]]
Ogni canale è organizzato in **"bursts"**,  non ci sono indirizzi sorgenti e destinazione, perché è una tecnologia a circuito, dove i blocchi di dato sono trasmessi su una rete fisica.

## Channel access - GSM frame
![[Screenshot 2026-10-14 at 17.10.39.png]]

## Channel Access - Timing Advance
Utilizzato per l'accesso al canale,  i ritardi di propagazione non sono nulli, dove i bit arrivano all'antenna ![[Screenshot 2026-10-14 at 17.13.57.png]]

## Burst Structure
Organizzazione dei bit all'interno degli slot
![[Screenshot 2026-10-14 at 17.16.47.png]]

## GSM: Canali Logici
Nel canale fisico è il come mando le informazioni sulla rete, che è una combinazione di time-slot e frequenze, ma non tutti i canali fisici sono uguale e posso definire canali logici, che definisce cosa mandare in quel canale fisico.

# LTE
Superare il problemi della WCDMA  ==(da rivedere)==
## Uso delle Bande di Frequenza
![[Screenshot 2026-10-14 at 17.29.29.png]]

## LTE Terminology
**User Plane**: piano dati dell'LTE
**Control Plane**: piano di controllo dell'LTE

## EPC - Components
![[Screenshot 2026-10-14 at 17.38.47.png|1120]]

## LTE Bearers
I *beares* sono dei tunnel tra ip & ip che mette in comunicazione lo user 
# Reference
---

