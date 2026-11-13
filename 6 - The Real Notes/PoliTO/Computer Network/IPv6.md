---
created: 2026-09-30
tags:
  - baby
topics:
  - Cybersecurity
  - TCP/IP
author: Danilo Quattrini
---
# IPv6
---
## Questions

- Che cos'è un'IPv6?
- Com'è formato L'IPv6?
- Che differenza c'è tra l'IPv6 e l'IPv4?
- Com'è la struttura di un IPv6?
- Come scrivere in un modo più semplice l'IPv6?
## Definizione di IPv6
Sono finiti gli IPv4, cioè non ci sono più IP del genere disponibili. **IPv6**, questo nuovo formato di indirizzamenti ha una dimensione di ben 128 bit, questa nuova versione è stata ideata perché la versione con IPv4 stava terminando il numero di indirizzi utilizzabili. 

Il motiva per cui non siamo ancora passati all'IPv6 è perché ci sono gli indirizzi privati, cioè che sono univoci all'interno della stessa subnet.

NAT (Network Address Translator): estremamente popolare 
Per connettere un milione di miliardi di bit ho bisogno di un minimo di almeno 107 bit, nel caso  più efficace. Dove però con 128 bit possiamo rappresentare un numero esagerato. Dove si avrà $2^{128}$![[Screenshot 2026-09-30 at 18.25.14.png]]
## Formato dell'IPv6
Sono **rappresentati con 8 gruppo di valori esadecimali**, ogni gruppo è diviso dai due punti
":" e non dal punto
![[Pasted image 20260908105937.png|1199]]

![[Screenshot 2026-09-30 at 18.31.36.png]]
come si vede dall'immagine ogni gruppo è composto da dei valori esadecimali che ogni lettera o numero sono 4 bit, in totale ogni gruppo contiene ben 16 bits (2byte).
### Shortcut (Semplificazioni)
- Il **primo** se ho un gruppo con tutti $0$, esempio $0000$, lo posso scrivere semplicemente a $0$![[Screenshot 2026-09-30 at 18.33.10.png]]
- La **seconda** invece è che invece di scrivere due volte zero, I DUE PUNTI NON SI POSSONO USARE PIU' DI UNA VOLTA![[Screenshot 2026-09-30 at 18.35.23.png]]
### Struttura dell'IPv6
I principi base dell'IPv4 sono uguali anche nell'IPv6, ma definiamo in maniera diversa il prefisso, quello che era il **network id** su IPv4 ora è il **prefisso** (Prefix) in IPv6, mentre la parte di host che c'era in IPv4 è diventato in IPv6 Interface ID (128-n bits).![[Screenshot 2026-09-30 at 18.38.53.png]]
Invece di chiamare sub-net, li chiamiamo **Link**, cioè diremmo che due host sono **on-Link**, se stanno sulla stessa rete, off-Link se devono comunicare direttamente tramite un router. Ci sono diversi tipi di IPv6, che sono i seguenti:
- [[#Multicast]]
- [[#Unicast]]
- [[#Anycast Address]]
![[Screenshot 2026-09-30 at 18.45.05.png]]
### Multicast
Possiedono un certo prefisso come quello dell'[[IP Multicast|IPv4 Multicast]] che iniziano con `1111 1111` che in esadecimale sarebbe `FF00::/8`
- Il tipo di multicast è di tipo **Well-known** Multicast (`FF00::/12`)
- **Transient** (FF10::/12) sono assegniati in modo molto casuale
- **Solicited-node Multicast** (FF02::/12): lo si utilizzano nelle ARP request
Nel prefisso posso definire uno *scope*, che definisce il range nel quale andiamo a trasferire il pacchetto nelle varie zonee![[Screenshot 2026-09-30 at 18.50.06.png]]

![[Screenshot 2026-09-30 at 18.50.58.png]]

### Unicast
#### Global Unicast
![[Screenshot 2026-10-01 at 16.08.43.png]]
Sono gli stessi di IPv4 solo che sono scritti in 128 bit, cambiano però la definizione del prefisso, perché sono suddivisi in 4 parti
- **Global Routing Prefix**: sono **n** che vengono dati all'**ISP**
- **Subnet ID**: sono **m** bit che identificano la subnet
Non specificano il prefisso quindi si avrà $3 + n + m$ bits, massima flessibilità ma si può rischiare di ritornare al problema dell'IPv4
![[Screenshot 2026-10-01 at 16.10.15.png]]
- **001**, primi bit che identificano che è un **Global Unicast**
- **ISP** (Internet Service Provider)
- (NLA) **Next Level Authority**, come per esempio l'azienda o il Politecnico
- (SLA) **Subnet Level Authority,** 
#### Link / Local site address
Sono gli indirizzi IPv6 privati, che sono due tipi:
- *Link local*: hanno prefisso `FE80::/64`, sono prefissi giusti per le subnet, con altri 64 bit per l'**interface-id**, funzionano per auto-configurazione, cioè ogni host può scegliere il proprio indirizzi **Link Local**, l'importante è che sia univoco nella rete locale
- *Site local* (*deprecated*): lo si possono utilizzare ma al suo rischio e pericolo
### Unique Local Address (ULA)
Cominciano con il prefisso`FC00::/7`, sono simili come il global unicast ma per le reti privati, li si possono utilizzare come indirizzi privati, ma con alte probabilità che questi indirizzi IP siano univoci![[Screenshot 2026-10-01 at 16.23.08.png]]
L'ottavo bit segna che l'IP è un IP locale, poi ci sono 40 bit che sono generati randomicamente (sono generati pseudo-randomicamente), 16 bit di subnet ID e 64 bit di interface ID.
- `FC00::/8` (`1111 1100`): se il bit flag L è `0`, può essere assegnato in futuro
- `FD00::/8` (1111 1101): se il bit flag L è `1` allora è assegnato localmente
### Embedded IPv4
Che servono per rappresentare in IPv6 un IPv4![[Screenshot 2026-10-01 at 16.34.35.png]]
Cioè è un escamotage per rappresentare un IPv4 su un IPv6 semplicemente mettendo a 0 i primi 80 bit, altri sedici bit a FFFF e rimangono ben 32 bit che sono la dimensione di un IPv4. I 32 bit finali sono rappresentati come un vero e proprio IPv4

### Loopback IPv6
Come l'IPv4 non cambia molto, ma sol il modo in cui lo rappresentiamo, con  `::1 (000…1)`

## Anycast Address
Qui abbiamo più dispositivi con lo stesso indirizzo IP e poi quando il router deve inviare un pacchetto in uno dei device che hanno lo stesso indirizzi ip, sceglie quello più vicino![[Screenshot 2026-10-01 at 16.40.37.png]]
Il router sceglierà la più vicina a noi (shortest path), approccio a minimo sforzo, lo facciamo solo con gli indirizzi ip che vogliamo duplicare, usata con le DNS pubbliche e CDN. Gli anycast li usiamo con gl'indirizzi **Global Unicast**
# Reference
---

