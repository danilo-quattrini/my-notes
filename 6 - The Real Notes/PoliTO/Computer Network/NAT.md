---
created: 2026-10-17
tags:
  - baby
topics:
author: Danilo Quattrini
---
# NAT
---
## Che cos'è il NAT e perché è stato introdotto?

Il **NAT (Network Address Translation)** è un meccanismo di rete che permette di modificare gli indirizzi IP (e le porte) all'interno degli header dei pacchetti IP mentre questi transitano attraverso un router o un firewall.

**Il problema originario:** Negli anni '90, con l'esplosione di Internet, ci si è resi conto che gli indirizzi IPv4 pubblici (circa 4,3 miliardi) si sarebbero esauriti molto in fretta. **La soluzione:** È stato creato uno spazio di **indirizzi IP privati** (RFC 1918, es. le reti `192.168.x.x`, `10.x.x.x`, `172.16.x.x`). Questi indirizzi possono essere usati liberamente all'interno di qualsiasi rete locale (LAN), ma **non sono instradabili su Internet**. Il NAT agisce come un "traduttore" al confine tra la rete privata e la rete pubblica (Internet), permettendo a un'intera LAN di affacciarsi all'esterno utilizzando uno o pochissimi indirizzi IP pubblici.

## Come funziona?
Quando un host con indirizzo IP privato vuole comunicare con un server su Internet, il pacchetto attraversa il router (che funge da NAT gateway). Il router esegue queste operazioni:

1. **Intercettazione (Outbound):** Il router riceve il pacchetto dall'host interno. Prende l'indirizzo IP sorgente (privato) e lo sostituisce con il proprio indirizzo IP sull'interfaccia pubblica.
    
2. **Tabella di Traduzione (NAT Table):** Il router annota questa modifica in una tabella interna (NAT Table), tenendo traccia della connessione in modo da sapere a chi recapitare l'eventuale risposta.
	
3. **Risposta (Inbound):** Quando il server esterno risponde, invia il pacchetto all'indirizzo IP pubblico del router. Il router consulta la sua NAT Table, trova l'indirizzo IP privato dell'host che aveva originato la richiesta, riscrive l'indirizzo IP di destinazione e inoltra il pacchetto nella rete locale.

## NAT Table
![[Pasted image 20261017125451.png|1040]]
Nello studio del NAT si utilizzano quattro termini specifici per identificare gli indirizzi da diverse prospettive:

- **Inside Local (Locale Interno):** L'indirizzo IP privato dell'host nella rete locale (es. `192.168.1.10`).
    
- **Inside Global (Globale Interno):** L'indirizzo IP pubblico assegnato al router NAT, che rappresenta l'host verso l'esterno (es. `80.105.10.2`).
    
- **Outside Global (Globale Esterno):** L'indirizzo IP pubblico del server o dell'host di destinazione su Internet.
    
- **Outside Local (Locale Esterno):** L'indirizzo dell'host esterno così come appare alla rete interna (nella maggior parte dei casi coincide con l'Outside Global).
## Tipi di NAT
Ci sono 3 tipi di NAT:
### Static NAT
Consiste in una mappatura **uno-a-uno (1:1)** tra un indirizzo IP privato e un indirizzo IP pubblico.

>[!info] **Utilizzo** 
È utile quando si ha un server (es. Server Web o Mail) all'interno della rete privata che deve essere sempre raggiungibile dall'esterno con lo stesso IP pubblico.
    
>[!danger] **Svantaggio**
> Non fa risparmiare indirizzi IPv4, poiché richiede un IP pubblico per ogni IP privato che si vuole mappare.
### Dynamic NAT
Mappa un indirizzo IP privato a un indirizzo IP pubblico scegliendolo da un **pool (gruppo) di indirizzi pubblici** a disposizione del router.

>[!info] **Utilizzo** 
>Quando si ha un numero di IP pubblici a disposizione, ma non abbastanza per tutti gli host interni. L'IP pubblico viene "noleggiato" temporaneamente.
    
>[!danger] **Svantaggio:**
> Se il pool di IP pubblici è esaurito in un determinato momento, un nuovo host interno non potrà navigare su Internet finché non se ne libera uno.

### Port Address Translation or NAT Overload
Questa è la soluzione utilizzata oggi giorno, chiamata. **Port Address Translation** (PAT), ci permette di utilizzare lo stesso indirizzo IP privato che però viene assegnato ad un unico e solo indirizzo IP pubblico. Questo è **possible tramite l'utilizzo di diverse porte**.

>[!exampl] **Esempio:**
>- Host A (`192.168.1.10:3000`) naviga in rete. Il router traduce in `[IP_Pubblico]:50001`.
>- Host B (`192.168.1.11:3000`) naviga in rete. Il router traduce in `[IP_Pubblico]:50002`. 
>   
>Quando tornano le risposte, il router legge la porta di destinazione (`50001` o `50002`) e capisce esattamente a quale Host interno (A o B) inoltrare il pacchetto.

## Vantaggi e Svantaggi

I vantaggi di utilizzare un NAT sono i seguenti
- **Conservazione degli indirizzi IPv4:** Ha evitato (o ritardato drasticamente) l'esaurimento globale degli IP.
    
- **Sicurezza intrinseca (Obfuscation):** Nasconde la struttura e gli indirizzi della rete locale dall'esterno. Senza specifiche regole di "Port Forwarding", nessun host esterno può iniziare autonomamente una connessione verso un host interno.
    
- **Flessibilità e Manutenibilità:** Permette di cambiare provider internet (e quindi l'IP pubblico) senza dover ricombiare tutti gli indirizzi IP interni della propria LAN.
    

**Svantaggi:**

- **Rottura del principio End-to-End:** Il protocollo IP nasceva per far parlare direttamente due host in modo trasparente. Il NAT altera gli header (Layer 3 e Layer 4), complicando protocolli come IPSec, VoIP (SIP) e applicazioni Peer-to-Peer (P2P).
    
- **Overhead computazionale:** Il router deve elaborare ogni singolo pacchetto in transito, modificare gli header e ricalcolare il checksum, introducendo un lieve ritardo (latenza).
    
- **Necessità di ALG (Application-Level Gateway):** Alcuni protocolli (come l'FTP) inseriscono il proprio indirizzo IP anche all'interno del "payload" del pacchetto (Layer 7). Il NAT base non basta, serve un ALG che ispezioni il traffico applicativo e traduca anche gli IP al suo interno.
