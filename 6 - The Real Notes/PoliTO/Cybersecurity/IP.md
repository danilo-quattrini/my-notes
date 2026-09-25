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

**Come lo si rappresenta?** :
Lo si rappresenta ad un formato di 32 bit per rappresentare ben $2^{32} = 4.294.967.296$ indirizzi ip univoci, sono denominati a 32 bit, perché sono raggruppati in 4 gruppi da 8 bit (4 byte), come ad esempio il seguente IPv4:
$$(192.168.1.1)_{10} = (11000000.10101000.00000001.00000001)_{2}$$
Sopra abbiamo una rappresentazione in base 10, in decimale ed una in base 2 binaria, vedremmo che ci sarà utile convertile il numero da decimale a binario
![[Pasted image 20260908110909.png|879]]

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
  ![[Pasted image 20260908124338.png|848]]
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

## IP Routing
Dato un indirizzo IP di destinazione nel pacchetto che viene inviato da una rete ad un'altra, utilizzando un algoritmo chiamata *longest prefix matching*, che si attiva in caso di diversi IP che vengono matchati.

Per fare il match si fa l'operazione di AND tra bit a bit, tra l'IP di destinazione $200.23.17.1$ e la netmask con $255.255.240.0$
$$\begin{align} 200.23.17.1  \\ 255.255.240.0 \\ \hline \\ 200.23.16.0 \end{align} $$
sotto forma di binary
$$\begin{align} 11001000.00010111.00010001.00000001 \\ 11111111.11111111.11110000.00000000 \\ \hline \\ 11001000.00010111.00010000.00000000 \end{align} $$
## Tabella di Routing
Prendiamo l'esempio dell'immagine qui sotto e andiamo a creare la tabella di routing del **Router R1**
![[Screenshot 2026-09-23 at 17.19.56.png]]

| Type  | Destinazione      | Next-hop     | Cost |
| ----- | ----------------- | ------------ | ---- |
| **C** | 130.192.2.0 /24   | 130.192.2.1  | 0    |
| **C** | 130.192.3.0 /30   | 130.192.3.1  | 0    |
| **C** | 130.192.3.4 / 30  | 130.192.3.5  | 0    |
| **C** | 80.105..10.0 / 30 | 130.192.10.1 | 0    |
| **S** | 0.0.0.0 / 0       | 80.105.10.2  | 1    |
| **S** | 130.192.3.8/30    | 130.192.3.2  | 1    |
| **S** | 130.192.1.0/24    | 130.192.3.2  | 2    |
| **S** | 130.192.0.0/24    | 130.192.3.2  | 1    |
La **C** sta per connessione diretta e la **S** sta per statica, cioè c'è stato un'operatore che ha configurato la rete per conto sua. Lo 0.0.0.0 identifica la **default route** (rotta di default), che farà sempre match con qualsiasi rete, la userò per tutte le destinazioni che non faranno match sia prima che dopo, viene utilizzato per il contatto con l'internet, infatti il next-hop è il default gateway che sarebbe un **ISP** (Internet Service Provider).

La routing table sopra non è ottimizzata, ma la si può rendere più efficiente come per esempio raggruppare gli IP che hanno la stessa subnetmask (netmask).
>[!example]
>Si possono prendere gl'ultimi IP che hanno netmask a /24  e /30, li possiamo raggruppare alla netmask a /22, quindi avremmo l'ip di rete a 130.192.0.0/22 che possiamo rappresentare da 0.0 fino a 3.255 che sarebbe il broadcast
>$$\begin{align} (130.192.3.255)_{10} \\ \hline (10000010.110000000.000000 \| 11.111111111)_{2}\end{align} $$
>Questo ragionamento l'abbiamo fatto perché abbiamo bisogno di rappresentare 3 diverse sottoreti una con .1.0 una con .2.0  ed una con 3.0 prendendo 2 bit dalla rete a /24 e passiamo a /22 che da 254 bit si possono utilizzare ben 510 host
## IPv6
**IPv6**, questo nuovo formato di indirizzamenti ha una dimensione di ben 128 bit, questa nuova versione è stata ideata perché la versione con IPv4 stava terminando il numero di indirizzi utilizzabili. 

   Sono **rappresentati con 8 gruppo di valori esadecimali**, ogni gruppo è diviso dai due punti ":" e non dal punto
   ![[Pasted image 20260908105937.png]]
   
   come si vede dall'immagine ogni gruppo è composto da dei valori esadecimali che ogni lettera o numero sono 4 bit, in totale ogni gruppo contiene ben 16 bits.

# Reference
---
[Classful IP Addressing](https://www.geeksforgeeks.org/computer-networks/introduction-of-classful-ip-addressing/)
