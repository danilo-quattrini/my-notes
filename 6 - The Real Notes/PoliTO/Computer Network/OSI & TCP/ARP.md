---
created: 2026-10-03
tags:
  - baby
topics:
  - OSI & TCP / IP
  - TCP/IP
  - IP
  - "[[School]]"
author: Danilo Quattrini
---
# ARP
---
## Questions
- Che cos'è l'ARP?
- Come viene utilizzato?
- Come funziona? 
- Che succede se l'host sorgente non conosce l'host di destinazione?
- **Gestione dell'overhead:** Per quale motivo i sistemi operativi moderni scartano le informazioni contenute negli ARP Request inviati dagli altri host della LAN invece di inserire preventivamente la mappatura IP-MAC nella propria cache?

---
## Definizione
>[!info] Definzione
>ARP (Address Resolution Protocol) è un protocollo che si trova al **livello applicativo** (L4) che  mappa dinamica un **indirizzo IP (L3)** con un'**indirizzo MAC (L2)** della scheda di rete ([NIC](https://www.geeksforgeeks.org/computer-networks/nic-full-form/))  associata, che deve trovarsi sulla stessa LAN locale.

Viene utilizzato perché per instradare i pacchetti al livello fisico c'è la necessità di conoscere l'indirizzo MAC del destinatario

## Come funziona
- Se l'host conosce l'IP di destinazione e la mappatura è già presente nella **ARP cache**, genera direttamente un frame L2 unicast.
    
- Se l'indirizzo MAC è sconosciuto, invia un **ARP Request** in **broadcast** (ricevuto da tutti gli host della LAN).
    
- Solo l'host che riconosce il proprio IP risponde con un **ARP Reply** in **unicast** contenente il suo MAC address.
    
- Entrambi gli host salvano la mappatura nella propria **ARP cache con un timeout**. Ogni pacchetto IP in ingresso con quella sorgente IP-MAC **refresha** (resetta a zero l'età) la voce nella cache.
## Condizioni di Nota
Gli host moderni **non salvano** in cache gli **ARP Request** inviati dagli altri host in broadcast a meno che **non siano i diretti interessati della richiesta** (cioè quello che l'host sorgente ricercava), per evitare overhead nella gestione della cache e rallentamenti nei tempi di ricerca.
# Reference
---

