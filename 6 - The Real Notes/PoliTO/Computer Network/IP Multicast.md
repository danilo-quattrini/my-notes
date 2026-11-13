---
created: 2026-09-30
tags:
  - baby
topics:
author: Danilo Quattrini
---
# IP Multicast
---
L'idea è che c'è un nodo sorgente che vuole contattare molte destinazioni allo stesso momento.
>[!example] Esempio
>Video conferenza, partite di calcio, partite di basket, dove l'evento viene trasmesso da un singolo PC principale e altri computer invece che vogliono ricevere l'evento che sta visualizzando il computer principale.

La comunicazione avviene a livello IP, una soluzione potrebbe essere il **BROADCAST**, cioè contattare tutti gli host in rete su internet. La soluzione sarebbe **UNICAST**, c'è una sorgente ed un destinatario. Il **MULTICAST** ci permette di scalare meglio, perché la sorgente che vuole trasmettere e condividere le informazioni, lo fa solamente tramite un singolo pacchetto, e dopo la rete capisce quali sono gli host interessati.

I router e gli switch gestiranno l'invio dei messaggi (pacchetti) agli host che sono interessati al messaggio inviato da una determinata sorgente. I destinatari possono entrare nel MULTICAST oppure ne possono uscire, cioè posso fare una **join** o **leave** di un gruppo.

La complessità è delegata principalmente al / ai router, dove farà una copia del pacchetto ai vari destinatari che sono interessati al pacchetto.

## Come identificare un MULTICAST?
Si identificano gli host che fanno parte del multicast con un'indirizzo IP di classe D, che sono gli ip che cominciano con il primo byte a $1110$, cioè indirizzi ip che vanno da $224.0.0.0$ a $239.255.255.255$.

## Come fa un destinatario a far parte di un MULTICAST
Tramite un pacchetto **IGMP** (Internet Group Management Protocol), che viene incapsulato in un datagramma in un IPv4,  permette ai destinatari di far parte di un gruppo MULTICAST. Questo protocollo si può utilizzare solo in locale.![[Screenshot 2026-09-30 at 16.24.39.png]]
>[!example]
>Il computer verde **SOURCE** manda un pacchetto che dice di essere interessato a far parte del multicast.

## Cosa Succede Dentro la rete Locale?
Al livello locale tutti ricevono tutto, dato un determinato ip multicast $244.0.0.1$ a cui mandare un pacchetto. Devo Garantire che la scheda di rete non scarti il pacchetto e che identifica l'IP multicast. Al livello 2 nel modello TCP-IP, c'è il MAC address della sorgente, ma non possiamo mettere un MAC (che è di dimensione di 48 bit) di una destinazione perché tale destinazione non esiste dato che dobbiamo mandare un pacchetto ad un gruppo.![[Screenshot 2026-09-30 at 16.31.55.png]]

Per risolvere il problema che si presenta al livello 2 del modello TCP-IP, si è inventato uno standard RFC, dove il MAC (dimensione di 48 bit) ha un prefisso fisso sempre quello di `01-00-5E-0` (ogni gruppo di cifre sono `1 byte` cioè 8 bit), che occupa i primi 25 bit del MAC mentre gli ultimi 23 bit vengono copiati dall'indirizzo ip del destinatario che manda il pacchetto **multicast**.

La decisione di scegliere come primo byte `01` nel MAC address che usiamo per il multicast ==(motivo che centra con il little edian, poi non ho capito da rivedere)==

Se h1 manda un messaggio ARP (Address Request), dove richiede l'indirizzo mac dei computer che sono collegati in locale? Questo messaggio è mandato in broadcast, quindi h2 e h3 ricevono tale richiesta. Solo la macchina che possiede l'IP che ha richiesto h1  risponderà alla richiesta ARP.
![[Screenshot 2026-09-30 at 16.55.37.png]]

### Caso 3 host sono collegati ad uno switch
![[Screenshot 2026-09-30 at 16.49.12.png]]
Lo switch non manda tutto, ma solo a specifici host in base al MAC, cioè fa un filtraggio in base al MAC address richiesto dall'host (switch lavora a livello 2, mentre router a livello 3). 

*IGM Spoofing* , dove lo switch si **comporta quasi come un router**, ed utilizza i messaggi IGMP per filtrare solo gli host che vogliono il messaggio multicast, non molto consigliato perché complesso e costoso, lo si disabilita spesso.

![[Screenshot 2026-09-30 at 16.52.22.png]]
Operazione di **flooding**, cioè manda pacchetti a tutti gli host che sono collegati allo switch, poi sarà l'host a scartarlo se non è interessato. Sprechiamo pacchetti ma non sarà un problema

## Diestro alle singole network![[Screenshot 2026-09-30 at 16.56.55.png]]
H1 manda un pacchetto multicast, dove H2 e H3 lo riceveranno, mettiamo che H6 sia pure interessato al gruppo G (che contiene H1, H2, H3). H6 manda un messaggio IGMP (Membership Report Message) con ip $244.0.0.22$, per dire che è interessato al gruppo G. Solitamente i routers mandano pacchetti **IGMP General Query**  per capire quali sono i gruppi attivi nella rete locale.

**Multicast Routing Protocol**: dove i router si condividono le routing table ==(da vedere meglio)==

I messaggi che vengono inviati per poter entrare ed uscire in un determinato gruppo sono sempre del tipo **IGMP Membership Protocol**, solo che avrà una flag con JOIN se vuole entrare e LEAVE se vuole uscire. Spesso il messaggio di LEAVE non viene inviato e per risolvere a questo problema il router dopo un certo tempo, manda un messaggio **IGMP General Query** chiedendo se ci sono ancora host che sono interessati al gruppo multicast, se no viene tolto dal gruppo.

Il MULTICAST NON VIENE UTILIZZATO AL modello applicativo, perché oggi usiamo le connessioni a TCP perché tra host si creano delle sessioni e il multicast non viene supportato.
# Reference
---

