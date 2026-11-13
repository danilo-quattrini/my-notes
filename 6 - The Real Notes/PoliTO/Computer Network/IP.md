---
created: 2026-02-14T15:43:00
tags:
  - baby
topics:
  - "[[School]]"
  - Cybersecurity
  - TCP/IP
  - IP
author: Danilo Quattrini
---
# IP
---
## Questions
### Concetti Generali del protocollo IP
**Definizione e caratteristiche:** 
- Come viene definito il protocollo IP e perché viene descritto con le proprietà _Connectionless_ e _Best Effort_?   
 **Affidabilità:** Quale componente si occupa del recupero degli errori o del controllo del flusso se il protocollo IP non garantisce la consegna o l'ordine dei pacchetti?
 
**Campi del datagramma IP:**
	- Spiega cos'**è un datagramma IP**, da quale due macro-famiglie è diviso?
	- Quanti righe ci sono all'intero del datagramma IPv4?
	- Spiega le componenti principali dell header nella prima riga
	- Spiega le componenti principali dell header nella prima seconda?
	- Spiega le componenti principali dell header nella prima terza?
	- Chec cosa si intende per MTU ?
    - Qual è la funzione del campo _Time to Live (TTL)_ all'interno del datagramma IP?    
    - Cosa protegge il _Header Checksum_ e cosa lascia invece scoperto?    
    - Disegna un Datagramma di esempio.

**Protocolli ausiliari:** Quali sono i ruoli principali di **ICMP** e **ARP** all'interno dell'architettura di rete?
### Indirizzamento IPv4 e Classi
- **Struttura degli indirizzi:**
    - Da quanti bit è composto un indirizzo IPv4 e in quali due parti logiche è suddiviso?
    - Che differenza c'è tra _limited broadcast_ e _direct broadcast_?
- **Classi di indirizzi:**
    - Quali sono i bit più significativi (MSB) e la subnet mask di default per le classi A, B e C?   
    - Perché si sottrae 2 al calcolo del numero di host utilizzabili per una rete ($2^n - 2$)?
    - A cosa sono destinate la **Classe D** e la **Classe E**?
    - Quali sono i limiti fondamentali dell'indirizzamento a classi che hanno portato all'adozione di CIDR?
### CIDR e Subnetting
**Definizione e caratteristiche**: 
	- A che costa sta l'acronimo CIDR? Perché è stato adottato tale indirizzamento?
	- Data la notazione CIDR `/22`, qual è la corrispettiva Subnet Mask in notazione decimale puntata?
	- Quanti bit sono riservati alla parte host e quanti indirizzi IP _utilizzabili_ per i dispositivi fornisce questa subnet?

### IP Routing Tabelle Di Routing
**Principi di instradamento:**
- In che modo un router decide quale rotta utilizzare in presenza di più corrispondenze (match) nella tabella di routing per lo stesso IP di destinazione? Spiega il funzionamento dell'algoritmo _Longest Prefix Matching_.
- Che cos'è una _Default Route_ (`0.0.0.0/0`), quale lunghezza di prefisso possiede e quando viene consultata?
 **Esercizio di aggregazione rotte (CIDR Summarization / Supernetting):**
 Considera le seguenti quattro sottoreti adiacenti con prefisso `/24`:
        
    - `130.192.0.0/24`
            
    - `130.192.1.0/24`
            
    - `130.192.2.0/24`
            
    - `130.192.3.0/24`
            
Qual è il prefisso supernet aggregato unico in notazione CIDR che le racchiude tutte e quattro ottimizzando la tabella di routing?
        
**Analisi di Routing Table:**
Un pacchetto è diretto all'IP di destinazione `200.23.19.7`. Nella tabella di routing sono presenti le seguenti voci:
        
    1. `200.23.16.0/20` verso Interface 1
            
    2. `200.23.18.0/23` verso Interface 2
            
    3. `0.0.0.0/0` verso Interface 3
Verso quale interfaccia verrà instradato il pacchetto e perché?

---

## Definizione
>[!quote] Internet Protocol
>**Internet Protocol** (**IP**), è un [protocollo di rete](https://it.wikipedia.org/wiki/Protocollo_di_rete "Protocollo di rete"), che si occupa di indirizzamento/[instradamento](https://it.wikipedia.org/wiki/Instradamento "Instradamento"), appartenente alla [suite di protocolli Internet TCP/IP](https://it.wikipedia.org/wiki/Suite_di_protocolli_Internet "Suite di protocolli Internet") su cui è basato il funzionamento della rete [Internet](https://it.wikipedia.org/wiki/Internet "Internet").

Correntemente sono usate due versioni del protocollo IP, l'originaria [versione 4](https://it.wikipedia.org/wiki/IPv4 "IPv4") e la più recente [versione 6](https://it.wikipedia.org/wiki/IPv6 "IPv6") ([[IPv6|IPv6]]), nata dall'esigenza di gestire meglio il crescente numero di dispositivi ([host](https://it.wikipedia.org/wiki/Host "Host")) connessi ad [Internet](https://it.wikipedia.org/wiki/Internet "Internet").
### Caratteristiche del protocollo
Il protocollo di rete IP definisce il formato del datagramma che viene inviato sulla rete, il piano di indirizzamenti e le regole di invio dei pacchetti sulla rete. 

Questo protocollo viene definito come:
- *ConnectionLess*:  perché **non stabilisce una connessione prima che il datagramma** viene inviato sulla rete, ma spera che arrivi a destinazione.
  
- *Best Effort*:  perché quando inviano i pacchetti sulla rete non è garantito che tali pacchetti arrivino al destinatario. Tali pacchetti possono ritardare la consegnare, perdersi oppure corrompersi

**Come gestisce gli errori?**
La gestione degli errori non viene definita direttamente dal protocollo IP, ma viene delegata all'**end system** (es. TCP), cioè si affida al protocollo per controllare che non ci siano errori nell'invio di tale pacchetti
### Datagramma IP
>[!quote] Che cos'è un datagramma
> Un datagramma è definito come un **Protocol Data Unit** (PDU) cioè un dato messaggio, che viene inviato sulla rete come un'unità autonoma di dati.
> E' divisa in due macro sezioni:
> - **Header (Intestazione):** Contiene i metadati di controllo e di instradamento (come indirizzo sorgente e di destinazione, lunghezza, meccanismi di controllo e frammentazione) necessari ai router per inoltrare il pacchetto lungo la rete. Ha una dimensione standard minima di **20 byte** (5 righe da 32 bit/4 byte ciascuna), che può estendersi fino a **60 byte** in presenza di opzioni.
>   
> - **Payload (Carico utile):** Contiene i dati provenienti dai livelli superiori dell'architettura ISO/OSI o TCP/IP (ad esempio un segmento **TCP** o un messaggio **UDP**).

![[Screenshot 2026-10-03 at 13.06.37.png]]
Questo sopra è un esempio di datagramma IP che è composto da le seguenti componenti
#### Prima Riga (0 - 31bit)
- **version (4 bit):** Definisce la versione del protocollo IP utilizzata. Per IPv4, il valore binario impresso è sempre `0100` (4 in decimale). Questo campo consente ai dispositivi di rete di capire subito come interpretare il resto dell'header.
    
- **header length / IHL (Internet Header Length) (4 bit):** Specifica la lunghezza totale dell'header misurata in **parole di 32 bit (4 byte)**.
    
    - Poiché il campo è di 4 bit, può rappresentare valori da 0 a 15.
    - La dimensione minima senza opzioni è di 20 byte, espressa col valore `5` cioè `0101` ($5 \times 4\text{ byte} = 20\text{ byte}$).
    - La dimensione massima (con 40 byte di opzioni) è espressa col valore `15`  cio+ `1111`($15 \times 4\text{ byte} = 60\text{ byte}$).
        
- **DS (Differentiated Services) (Type of Service) (6 bit):** In origine chiamato _Type of Service (ToS)_, fa parte del meccanismo di **Qualità del Servizio (QoS)**. Viene impiegato per classificare il traffico e **dare priorità ad alcuni tipi di dati** (ad esempio traffico VoIP o streaming in tempo reale rispetto alle e-mail).
    
- **ECN (Explicit Congestion Notification) (2 bit):** Consente ai router di segnalare l'imminenza di una congestione di rete senza dover scartare direttamente i pacchetti.
    
- **total length (in bytes) (16 bit):** Indica la dimensione complessiva dell'intero datagramma (Header + Payload) espressa in byte.
    
    - Essendo a 16 bit, la dimensione massima teorica di un datagramma IPv4 è di $2^{16} - 1 = 65.535\text{ byte}$
#### Seconda Riga (32 - 63 bit)
Quando un datagramma supera la **Maximum Transmission Unit (MTU)** del link di livello 2 su cui deve viaggiare, i router devono suddividerlo in frammenti più piccoli. Questa riga gestisce proprio la ricostruzione del pacchetto originario presso l'host di destinazione.

La seconda riga dell'header è composta da i seguenti bit:
- **Identification (16 bit):** Un identificativo univoco assegnato dall'host mittente a tutti i frammenti derivati dallo stesso datagramma originale. Tutti i frammenti di un singolo datagramma avranno il medesimo valore di _Identification_.
    
- **Flags (3 bit):** Tre bit di controllo per il processo di frammentazione:
    
    - **Bit 0:** Riservato per usi futuri, dev'essere sempre impostato a `0`.
        
    - **DF (Don't Fragment):** Se impostato a `1`, indica ai router di **non frammentare** il pacchetto. Se la MTU del link è inferiore alla dimensione del pacchetto, il router lo scarta e invia al mittente un messaggio d'errore ICMP (_Destination Unreachable - Fragmentation Needed_).
        
    - **MF (More Fragments):** Se impostato a `1`, indica che il frammento corrente **non è l'ultimo** e ne seguiranno altri. Se è impostato a `0`, segnala che si tratta dell'ultimo frammento (o che il pacchetto non è mai stato frammentato).
        
- **Fragment offset (13 bit):** Indica la posizione (offset) del blocco di dati contenuto nel frammento rispetto all'inizio del payload originale, misurata in **unità di 8 byte (64 bit)**. **Consente al ricevente di ricomporre esattamente i frammenti nell'ordine corretto,** anche se arrivano disordinati.
#### Terza riga (64 - 95)
- **Time-To-Live (TTL) (8 bit):** Un contatore di sopravvivenza per evitare che pacchetti smarriti rimangano a circolare all'infinito nella rete a causa di cicli di instradamento (routing loops). Ogni router che attraversa decrementa il valore del TTL di 1. Se il TTL raggiunge lo `0`, il pacchetto viene eliminato e viene inviato al mittente un messaggio **ICMP** _Time Exceeded_.
- **Protocol (8 bit):** Specifica a quale protocollo di livello superiore (Transport Layer) appartengono i dati trasportati nel _payload_. Alcuni dei valori numerici standard più diffusi sono:
    - `1`: ICMP
    - `6`: TCP
    - `17`: UDP
- **Header checksum (16 bit):** Un codice di controllo per verificare la presenza di errori intervenuti nei soli bit dell'**header** durante la trasmissione. Poiché il campo TTL diminuisce ad ogni salto di router, l' _header checksum_ viene ricalcolato e aggiornato a ogni router attraversato. _(Nota: non protegge il payload, la cui integrità è verificata dai protocolli di livello superiore come TCP/UDP)_.
## IPv4
*Internet Protocol Version 4*, protocollo di rete che è caratterizzato dalla rappresentazione degli **indirizzi IP** a ben (32 bit).
###  Indirizzo di Rete (IP Address)
>[!info]
>Sono dei numeri valori che vengono assegnati a dei computer / device che sono connessi ad una rete ed utilizzano il protocollo di rete per la comunicazione.

**Perché vengono utilizzati?** Il loro scopo è quello di identificare un dispositivo che appartiene ad una rete o di individuare la posizione / locazione in cui si trova. 

**Come lo si rappresenta?** :
Lo si rappresenta ad un formato di 32 bit per rappresentare ben $2^{32} = 4.294.967.296$ indirizzi ip univoci, sono denominati a 32 bit, perché sono raggruppati in 4 gruppi da 8 bit (4 byte), come ad esempio il seguente IPv4:
$$(192.168.1.1)_{10} = (11000000.10101000.00000001.00000001)_{2}$$
Sopra abbiamo una rappresentazione in base 10, in decimale ed una in base 2 binaria, vedremmo che ci sarà utile convertile il numero da decimale a binario
![[Pasted image 20260908110909.png|1088]]

Come vediamo sopra abbiamo alcuni dei bit che sono riservati alla rete, cioè quei gruppi che identificano in che porzione di rete ci troviamo, e la parte degli host che vedremmo meglio in dettaglio in seguito.
### Struttura di base di un indirizzo IPv4
Come abbiamo prima citato un IPv4 ha ben 32 bit che sono divisi in due parti logiche:

- **network part** (parte di rete): i bit più significativi, identificano la rete a cui l’host appartiene;
    
- **host part** (parte di host): i bit meno significativi, identificano l’host all’interno di quella rete.

Tutti i dispositivi che condividono la stessa _network part_ appartengono alla stessa **IP network** e sono tipicamente collegati allo stesso segmento fisico (stesso link layer).

### Classi di IPv4
Gli IPv4 possono essere divisi in 5 diverse classi: **A, B, C, D, E**, ognuna di queste classi sono particolari per come hanno il numero dei bit assegnati all rete e i numero dei bit assegnati agli host tra cui ci sono anche diversi numeri di bit riservati ad ogni classe.

- **Classe A**: Indirizzo IP che ha ben 8 bit che sono riservati per la rete compreso del bit significativo (denominato anche MSB *most significant bit*) che è sempre **0** gli altri 7 bit sono usati per identificare la rete, la maschera di rete (subnet mask) è $255.0.0.0$.
  
  Si possono utilizzare ben:
  $$2^{24} - 2 = 16.777.214$$
  host da assegnare, questo perché il calcolo di quanti host si possono avere dato un determinato IP (escludendo broadcast e rete), con $n$ il numero di bit che sono disponibili per è il seguente:
	$$host = 2^{(32−x)}−2$$
  ![[Pasted image 20260908124338.png|1042]]
  Dall'immagine possiamo vedere che il primo bit è sempre zero e che si possono rappresentare dalla network: 0 fino al 127
- **Classe B**: Ci sono ben 16 bit riservati alla rete tra cui ci sono ben 2 bit che sono sempre $10$ che sono i bit più significativi MSB, si possono rappresentare ben $2^{16}-2 = 65.534$ host e la maschera di rete di default è $255.255.0.0$.
  ![[Pasted image 20260908125157.png|848]]
	Dall'immagine possiamo vedere che i primi due bit sono 1 e 0 e che si possono rappresentare dalla network: 128 fino al 191

- **Classe C**: Rete di classe C ha la caratteristica di avere ben 24 bit riservati alla rete tra cui 3 bit significativi che sono $110$ che non cambiano mai. Vengono utilizzate per piccole infrastrutture di rete e ha la maschera di default di $255.255.255.0$.![[Pasted image 20260908125544.png|849]]
Per le altri classi sono sempre gli stessi concetti solo che cambiano il numero dei bit riservarti alla rete e i bit più significativi, come vediamo dalle immagini di esempio per la classe D e la classe E
![[Pasted image 20260908125956.png|880]]
![[Pasted image 20260908130141.png|880]]

Prendiamo anche questa tabella per semplificarci il concetto

| Class | Leading Bits (MSB) | Net ID Bits | Host ID Bits | No. of Networks | Usable Hosts / Network    | Start Address | End Address     |
| ----- | ------------------ | ----------- | ------------ | --------------- | ------------------------- | ------------- | --------------- |
| A     | 0                  | 8           | 24           | 2⁷ = 128        | $2^{24} − 2 = 16,777,214$ | 0.0.0.0       | 127.255.255.255 |
| B     | 10                 | 16          | 16           | 2¹⁴ = 16,384    | $2^{16} − 2 = 65,534$     | 128.0.0.0     | 191.255.255.255 |
| C     | 110                | 24          | 8            | 2²¹ = 2,097,152 | $2^{8} − 2 = 254$         | 192.0.0.0     | 223.255.255.255 |
| D     | 1110               | —           | —            | —               | —                         | 224.0.0.0     | 239.255.255.255 |
| E     | 1111               | —           | —            | —               | —                         | 240.0.0.0     | 255.255.255.255 |
Il concetto di utilizzare le classi per rappresentare delle reti oggi viene usato poco o quasi per niente, questo perché limita a chi costruisce una nuova rete di dover utilizzare o un numero elevato di host oppure un numero ristretto. Per questo motivo è stato introdotto l'utilizzo di una nuova notazione chiamata [[CIDR]]

## Indirizzi IP Speciali
Ci sono indirizzi che sono dedicate ad identificare la rete che sono definiti **indirizzi di rete**, che sono tutti gli indirizzi che possiedeno i bit degl'host tutti a 0![[Screenshot 2026-09-23 at 16.53.34.png]]
 $$(192.168.1.0)_{10} = (11000000.10101000.00000001.00000000)_{2}$$
L'esempio di sopra è l'**indirizzo di rete**

$$(192.168.1.255)_{10} = (11000000.10101000.00000001.11111111)_{2}$$
 Questo indirizzo identifica tutti gli host che appartengono alla stessa rete, viene definito **broadcast**, dove tutti i bit degli host sono ad $1$. La differenza tra il **limited broadcast** dal **direct broadcast** è che il primo lo possiamo utilizzare solo localmente all'interno della nostra rete, mentre il direct lo si può utilizzare anche per inviare pacchetti ad altre reti differenti.

**loopback**: identifica la macchina stessa, cioè il **localhost** che è rappresentato in questo modo.
$$(127.0.0.1)_{10} = (10000000.00000000.00000000.00000001)_{2}$$

 Prendiamo l'esempio di come si rappresenta il nostro computer collegato alla rete
 ```bash
 en0: flags=8863<UP,BROADCAST,SMART,RUNNING,SIMPLEX,MULTICAST> mtu 1500
        options=6460<TSO4,TSO6,CHANNEL_IO,PARTIAL_CSUM,ZEROINVERT_CSUM>
        ether 22:47:fb:bf:84:a1
        inet6 fe80::447:26ff:51ac:cf74%en0 prefixlen 64 secured scopeid 0xe
        inet 172.21.146.33 netmask 0xfffffe00 broadcast 172.21.147.255
        nd6 options=201<PERFORMNUD,DAD>
        media: autoselect
        status: active
 ```

Il link da un router ad un'altro devono essere con una netmask di /30, dove è possibile rappresentare ben $4$ host dove 1 è riservato alla rete ed uno al broadcast e ci rimangono ben 2 ip utilizzabili che sono quelli che daremmo tra i vari router.

# Reference
---
[Classful IP Addressing](https://www.geeksforgeeks.org/computer-networks/introduction-of-classful-ip-addressing/)
