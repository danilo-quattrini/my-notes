---
created: 2026-02-14T15:43:00
tags:
  - baby
topics:
  - "[[School]]"
  - Cybersecurity
  - TCP/IP
author: Danilo Quattrini
---
# IP
---
>[!quote] Internet Protocol
>**Internet Protocol** (**IP**), è un [protocollo di rete](https://it.wikipedia.org/wiki/Protocollo_di_rete "Protocollo di rete"), che si occupa di indirizzamento/[instradamento](https://it.wikipedia.org/wiki/Instradamento "Instradamento"), appartenente alla [suite di protocolli Internet TCP/IP](https://it.wikipedia.org/wiki/Suite_di_protocolli_Internet "Suite di protocolli Internet") su cui è basato il funzionamento della rete [Internet](https://it.wikipedia.org/wiki/Internet "Internet").

Correntemente sono usate due versioni del protocollo IP, l'originaria [versione 4](https://it.wikipedia.org/wiki/IPv4 "IPv4") e la più recente [versione 6](https://it.wikipedia.org/wiki/IPv6 "IPv6"), nata dall'esigenza di gestire meglio il crescente numero di dispositivi ([host](https://it.wikipedia.org/wiki/Host "Host")) connessi ad [Internet](https://it.wikipedia.org/wiki/Internet "Internet").

## IPv4

*Internet Protocol Version 4*, protocollo di rete che è caratterizzato dalla rappresentazione degli **indirizzi IP** a ben (32 bit).

Ma cosa sono gl'indirizzi IP o chiamati anche indirizzi di rete?

###  Indirizzo di Rete (IP Address)
>[!info]
>Sono dei numeri valori che vengono assegnati a dei computer / device che sono connessi ad una rete ed utilizzano il protocollo di rete per la comunicazione.

**Perché vengono utilizzati?** Il loro scopo è quello di identificare un dispositivo che appartiene ad una rete o di individuare la posizione / locazione in cui si trova. 

**Come vengono rappresentati?** Gl'indirizzi di rete che sono presenti oggi sono rappresentati in due formati:

1. Il primo è denominato **IPv4**, tale formato possiede ben 32 bit per rappresentare ben $2^{32} = 4.294.967.296$ indirizzi ip univoci, sono denominati a 32 bit, perché sono raggruppati in 4 gruppi da 8 bit (4 byte), come ad esempio il seguente IPv4:
$$(192.168.1.1)_{10} = (11000000.10101000.00000001.00000001)_{2}$$
Sopra abbiamo una rappresentazione in base 10, in decimale ed una in base 2 binaria, vedremmo che ci sarà utile convertile il numero da decimale a binario
![[Pasted image 20260908110909.png|771]]

Come vediamo sopra abbiamo alcuni dei bit che sono riservati alla rete, cioè quei gruppi che identificano in che porzione di rete ci troviamo, e la parte degli host che vedremmo meglio in dettaglio in seguito.

2. Il secondo formato viene denominato **IPv6**, questo nuovo formato di indirizzamenti ha una dimensione di ben 128 bit, questa nuova versione è stata ideata perché la versione con IPv4 stava terminando il numero di indirizzi utilizzabili. 

   Sono **rappresentati con 8 gruppo di valori esadecimali**, ogni gruppo è diviso dai due punti ":" e non dal punto
   ![[Pasted image 20260908105937.png]]
   
   come si vede dall'immagine ogni gruppo è composto da dei valori esadecimali che ogni lettera o numero sono 4 bit, in totale ogni gruppo contiene ben 16 bits.
### Struttura di base di un indirizzo IPv4
Come abbiamo prima citato un IPv4 ha ben 32 bit che sono divisi in due parti logiche:

- **network part** (parte di rete): i bit più significativi, identificano la rete a cui l’host appartiene;
    
- **host part** (parte di host): i bit meno significativi, identificano l’host all’interno di quella rete.

Tutti i dispositivi che condividono la stessa _network part_ appartengono alla stessa **IP network** e sono tipicamente collegati allo stesso segmento fisico (stesso link layer).

### Classi di IPv4
Gli IPv4 possono essere divisi in 5 diverse classi: **A, B, C, D, E**, ognuna di queste classi sono particolari per come hanno il numero dei bit assegnati all rete e i numero dei bit assegnati agli host

- **Classe A**: Indirizzo IP che ha ben 8 bit che sono riservati per la rete con il bit più significativo (denominato anche MSB *most significant bit*) che è sempre **0** gli altri 7 bit sono usati per identificare la rete.
  
  Si possono utilizzare ben:
  $$2^{24} - 2 = 16.777.214$$
  host da assegnare, questo perché il calcolo di quanti host si possono avere dato un determinato IP (escludendo broadcast e rete), con $n$ il numero di bit che sono disponibili per è il seguente:
	$$2^{n}-2 = host$$
  ![[Pasted image 20260908124338.png|744]]

- **Classe B**: Ci sono ben 16 bit riservati alla rete tra cui ci sono ben 2 bit che sono sempre $10$ che sono i bit più significativi MSB, si possono rappresentare ben $2^{16}-2 = 65.534$ host e la maschera di rete di default è $255.255.0.0$.
  ![[Pasted image 20260908125157.png|755]]
# Reference
---
[Classful IP Addressing](https://www.geeksforgeeks.org/computer-networks/introduction-of-classful-ip-addressing/)
