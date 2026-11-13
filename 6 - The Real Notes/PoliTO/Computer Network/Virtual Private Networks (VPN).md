---
created: 2026-11-11
tags:
  - baby
topics:
author: Danilo Quattrini
---
# Virtual Private Networks (VPN)
---
# Introduzione

>[!quote] Definizione
**VPN** (Virtual Private Network), cioè un infrastruttura comune che ci permette di attuare delle policy, come se fossimo in una rete privata.

Le **policies** sono la: Sicurezza, [[Multimedia Networking & Quality of Service|QoS]], Affidabilità, Indirizzamento.

Vediamo un caso d'uso semplice.
![[IMG-Virtual Private Networks (VPN)-20261111.png]]

Gli elementi chiavi che si vedranno con la VPN c'è un concetto che abbiamo visto in precedenza, cioè il **Tunnel**. Questo **Tunnel** è un contenitore o scudo che permette di rendere il traffico della rete sicuro, sfortunatamente non è presente in tutte le soluzioni.

L'operazione di tunneling lo svolge il **VPN Gateway** (dal punto di vista dell'indirizzamento), che sarebbe un convertitori di pacchetti che vengono mandati sulla rete per renderli sicuri.![[IMG-Virtual Private Networks (VPN)-20261111-1.png]]
Il NAT non va a cambiare l'indirizzo IP del pacchetto interno ma gli da semplicemente l'indirizzo IP pubblico.
# Motivazioni
La VPN serve per tagliare i costi nell'avere una rete privata. ![[IMG-Virtual Private Networks (VPN)-20261111-2.png]]

# Terminologie Base e Scenario
Le terminologie importanti da sapere per la VPN, sono le seguenti:
1. **End Point Authentication**: l'autenticazione dell'utente in un determinato servizio che dichiara chi è, cioè il server verifica se l'utente è quello che dichiara. Questo non è solo dal punto di vista dell'utente, ma anche il **VPN Gateway**, Può autenticarsi.

2. **Data Integrity**: quando invio un messaggio voglio essere sicuro che la destinazione riceva l'intero messaggio. Si manda una firma per la verifica dell'integrità del messaggio (tramite meccanismo di hash)

3. **Data Confidentiality**: vogliamo essere sicuri che i dati non vengano letti da utenti terzi se non all'utente finale. (tramite cifratura del messaggio, che viene decifrato dall'utente finale, ma non importante per l'esame)

4. **Data Separation**: non è una proprietà di sicurezza, ma riguarda la separazione dei dati.
#  Tunneling
![[IMG-Virtual Private Networks (VPN)-20261111-3.png]]

Si crea un canale virtuale, tra due aziende (sotto-reti) private, dove i VPN Gateway tolgono e aggiungono l'**header giallo**.

# Tipologie di VPN

## s2s (Site to Site)  VPN Tunneling
VPN per due sede aziendali, dove ci sono collegamenti tra due diverse subnet.
![[IMG-Virtual Private Networks (VPN)-20261111-5.png]]
## e2e End To End
Si crea un canale logico tra due end point (end-host), dove il canale parte da un pc e finisce direttamente in un altro pc.![[IMG-Virtual Private Networks (VPN)-20261111-4.png]]

## Remote VPN (usato da noi)
![[IMG-Virtual Private Networks (VPN)-20261111-6.png]]
Dal lato sinistro c'è il gateway mentre nel lato destro c'è il PC (host)

# VPN Scenario
Ci sono due scenari differenti, che sono:

## Intranet VPN
![[IMG-Virtual Private Networks (VPN)-20261111-7.png]]
Si proteggono i server specifici tramite firewall, che è un dispositivo che protegge ulteriormente i vari server.

## Extranet VPN
![[IMG-Virtual Private Networks (VPN)-20261111-8.png]]
Le varie azienda si collaborano, ma non si comunicano tutto, questo perché meglio non fidarsi.

Possiede semplicemente un livello di protezione in più.

Possono sorgere altri problemi con queste strutture, come ad esempio gli **overlap**, dove i vari dispositivi si trovano nella stessa rete. 
![[IMG-Virtual Private Networks (VPN)-20261111-9.png]]
può capitare di avere due host che possiedono lo stesso indirizzo IP. Si deve mettere anche un controllo nei vari punti di accesso della rete.

# Internet Access
## Centralized Internet Access
![[IMG-Virtual Private Networks (VPN)-20261111-10.png]]

Il router A farà da gateway, questo è la nostro punto di accesso per internet.
![[IMG-Virtual Private Networks (VPN)-20261111-11.png]]
Qui si possiede la sicurezza e soddisfa le policy che ho citato prima.
![[IMG-Virtual Private Networks (VPN)-20261111-13.png]]
Il motivo che si utilizza la VPN è quello che si va a cambiare il luogo in cui andremmo ad identificarci sulla rete.
## Distributed Internet Access
![[IMG-Virtual Private Networks (VPN)-20261111-12.png]]
Si distingue se si manda il pacchetto dall'azienda oppure da una locazione privata, che manda un indirizzo ip pubblico.

# VPN Topologie
Ci sono due topologie di VPN:
1. **HUB and Spoke**: cioè dove c'è un sito che fa da hub, cioè da Headquarter (quartier generale), approccio centralizzato dall'HQ quello che sulla figura è in alto a sinistra.
![[IMG-Virtual Private Networks (VPN)-20261111-14.png]]

2. **Mesh**: il sito 1 per parlare con il sito 2 può parlarci direttamente senza limiti, ma è difficile da configurare.

# Deployment Models, Previsioning Models & VPN Protocol Layer
Si possono classificare le VPN in un grafico 3 dimensionale.
![[IMG-Virtual Private Networks (VPN)-20261112.png]]
- Il **Deployment Model**, cioè il modello con cui si svolge il deployment, che può essere **Overlay** oppure **Peer**

- Il Provisioning Model, cioè chi crea la VPN può essere il **Customer** oppure il **Provider**.

- Il **Protocol Layer**: cioè i livelli ISO / OSI, dove si svolge il tunnel in diversi livelli

## VPN Categories
Si può mostrare il grafico prima illustrato tramite questo albero.
![[IMG-Virtual Private Networks (VPN)-20261112-1.png]]

Si andranno a vedere soluzioni **Overlay**(che la rete non partecipa alla realizzazione della VPN) e **Customer Provisioned**

### Overlay Model

>[!info] Definizione
>La rete pubblica (che è pensata per trasportare il traffico ad altri utenti, cioè quelli degli ISP), **NON PARTECIPA NELLA REALIZZAZIONE DELLA VPN**, non sapendo la destinazione delle VPN.

In questo approccio si va solo a connettere i vari **VPN Gateway**, dove ognuna di loro devono essere in contatto tra di loro. Il routing è performato dalle VPN gateway.

### Peer Model
Ogni **VPN gateway** interagisce con il router dell'operatore che diventa un suo Peer, questo permette ai gateway di poter **scambiare informazioni di Routing**. 
![[IMG-Virtual Private Networks (VPN)-20261112-2.png]]
Ottime performance, ma costi elevati da parte dell'operatore.

### Customer Provisioned
Il customer deve gestire e configurare le proprie VPN, includendo tutte le funzionalità che sono presenti nella VPN. Il Network provider non conosce il traffico che viene generato dai customer![[IMG-Virtual Private Networks (VPN)-20261112-3.png]]
Ci sono dei canali logici virtuali che sono collegati tra i vari **Customer Equipment**. Che sarà semplicemente un router che farà da CE e da **VPN Gateway**.
#### Accedere alle VPN Customer Provisioned
![[IMG-Virtual Private Networks (VPN)-20261112-5.png]]
Un tunnel end-point è il VPN gateway (quello a sinistra) e un altro tunnel end-point è il nostro computer (quello alla nostra destra).

>[!info] Spiegazione
>Quando facciamo partire la VPN facciamo partire un TUNNEL, che sarebbe la lineea arancione.
>![[IMG-Virtual Private Networks (VPN)-20261112-6.png]]
>Noi computer (30.1.1.1) Andiamo a chiedere l'indirizzo IP al VPN Gateway come un DHCP, sono nella stessa subnet, e svolgono un operazione di tunnel.
>![[IMG-Virtual Private Networks (VPN)-20261112-7.png]]
>Nella rete Internet pubblica vedrà il pacchetto rosso, questo perché sarà coperto dall'operazione di tunneling in modo da arrivare a destinazione del VPN Gateway.
### Provider Provisioned
L'ISP configura e possiede i dispositivi **VPN Gateway**, sono gestite dai Service Provider.
![[IMG-Virtual Private Networks (VPN)-20261112-4.png]]
L'operatore deve gestire le varie differenti aziende, che sono colorate con un colore differente.


## Layer N VPN 
A che livello andiamo a svolgere il tunnel? cioè a che livello trasportiamo il pacchetto interno?
### Layer 2 VPN
Abbiamo le **Virtual Private LAN Service**, che emulano le operazioni delle [[LAN & VLAN|LAN]], cioè si possiede la stessa LAN e simulano la LAN, questo approccio funziona solo con l'approccio [[#Provider Provisioned]], dove ci devono essere dei Router nel mezzo che si comunicano con il MAC.
![[IMG-Virtual Private Networks (VPN)-20261112-8.png]]

**IP-Only LAN-like Service**: i [[#Customer Provisioned|CE]], si comportano come host IP oppure router IP, solo i protocolli IP più ICMP e ARP, viaggiano nella VPN.

### Layer 3 VPN
![[IMG-Virtual Private Networks (VPN)-20261112-9.png|1040]]

### Layer 4 VPN Tunneling: s2s
![[IMG-Virtual Private Networks (VPN)-20261112-10.png]]
Si utilizza nel Livello 4 (Applicativo) di ISO / OSI che si utilizza il protocollo TCP con SSL/(TLS), utilizzato dai protocolli HTTPS, che ci dice che c'è una connessione sicura tra due VPN Gateway.

### Layer 4 VPN Tunneling: e2e
![[IMG-Virtual Private Networks (VPN)-20261112-12.png]]

# GRE - Generic Routing Encapsulation
L'avevamo visto anche [[IPv4 to IPv6|qui]], che funziona al livello IP e ha il pacchetto di questo formato:![[IMG-Virtual Private Networks (VPN)-20261112-13.png|1040]]
## Versione 0
Il GRE Header è formato da questi parametri:
![[IMG-Virtual Private Networks (VPN)-20261112-14.png]]
nella parte dei protocolli (*Protocol*) si avrà i seguenti protocolli:
![[IMG-Virtual Private Networks (VPN)-20261112-16.png]]
### Header Fields
![[IMG-Virtual Private Networks (VPN)-20261112-15.png]]

## Versione 1
![[IMG-Virtual Private Networks (VPN)-20261112-17.png]]
Hanno introdotto questo nuovo flag, chiamato **Acknowledgment Number** (A), con funzionalità avanzate, come:
![[IMG-Virtual Private Networks (VPN)-20261112-18.png]]
Con il Sequence Number e l'Acknowledge Number ci aiuta per il sequence detection e l'error detection.

# Layer 2 frame, within an IP packet
1. **[[#L2TP]]**
2. **[[#PPTP]]**: Protocollo Customer Provisioned, che però non è buono in ambito della sicurezza, nasce come protocollo proprietario e gestito da chiave
## L2TP
![[IMG-Virtual Private Networks (VPN)-20261112-19.png]]
Ci sono due siti aziendali e due VPN Gateway, che sono definiti come **LAC** (Access Concentrator che supporta la connessione alla L2TP) e **LNS** (Network Server Corporate Network). I pacchetti che vengono mandate tra il LAC e il LNS è di livello 2
### Tunnels & Sessions
![[IMG-Virtual Private Networks (VPN)-20261112-20.png]]
Un tunnel solo per gestire tutte le connessioni e c'è un CC che mantiene attivo il tunnel e tutte le configurazioni. Dove il LAC crea una sessione per ogni utente che cercano di connettersi al tunnel.

### Stabilire il Tunnel
Per configurare un tunnel c'è bisogno di un'autenticazione, basata sul **segreto condiviso**, che viene condiviso tra il LAC e LNS, cioè un autenticazione nella quale se il VPN Gateway se si vuole autenticare ad un altro Gateway, devono rispondere ad una domanda di sicurezza.

### Pacchetto Header
![[IMG-Virtual Private Networks (VPN)-20261112-21.png]]
### Header FLAG 
![[IMG-Virtual Private Networks (VPN)-20261112-22.png]]

### Sequence Number
![[IMG-Virtual Private Networks (VPN)-20261112-23.png]]

### Security Issue
C'è solo come autenticazione quella presente nel Tunnel e basta, per la sicurezza al livello di pacchetto si vedrà con [[#IPsec]]

# PPTP
![[IMG-Virtual Private Networks (VPN)-20261112-24.png]]
PTPP  Network Server che si intende come il Corporate VPN gateway, dove poi c'è anche un Access Concentrator

## Connessione PPTP
Funziona con il PPTP Data Tunneling, dove c'è anche l'header GRE![[IMG-Virtual Private Networks (VPN)-20261112-25.png]]
### Header PTPP
![[IMG-Virtual Private Networks (VPN)-20261112-26.png]]

Protocollo Deprecato
# IPsec VPN
Lo si vende sicuro, dove si aggiungono degli header in più, che sono chiamati.
## Authentication Header (AH)
Dove svolge l'autenticazione della sorgente e integrità dei dati, **ma non svolge la confidenzialità**.
![[IMG-Virtual Private Networks (VPN)-20261112-27.png]]
Questo header viene inserito tra l'**IP Header** e il **payload** e il router processano i datagrammi allo stesso modo. 

Si porta il riferimento alla sessioni, tramite un ID, che sono generate tramite dispositivi *end-to-end* (e2e) o *site-to-site* (s2s).

## Encapsulating Security Payload (ESP)
![[IMG-Virtual Private Networks (VPN)-20261112-28.png]]
Svolge la confidenzialità e l'autenticazione dell'host insieme all'integrità, che è identificato nell header IP con il protocollo 50. ESP aggiunge nel segmento TCP e UDP una parte di trailer e di header.

## IPsec VPN
![[IMG-Virtual Private Networks (VPN)-20261112-29.png]]
In questo esempio abbiamo una configurazione **site-to-site** (s2s) 
## Modalità di IPsec
### Transport Mode
![[IMG-Virtual Private Networks (VPN)-20261112-30.png]]
### Tunnel Mode
![[IMG-Virtual Private Networks (VPN)-20261112-31.png]]
serve per proteggere sia l'header che il payload.