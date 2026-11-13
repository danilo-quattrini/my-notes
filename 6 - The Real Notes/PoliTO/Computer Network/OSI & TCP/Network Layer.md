---
created: 2026-02-14T15:43:00
tags:
  - baby
topics:
  - OSI & TCP / IP
  - Cybersecurity
  - TCP/IP
  - "[[School]]"
author: Danilo Quattrini
---
# Network Layer
---
>[!quote]
>Il livello di Rete è quel livello del modello ISO / OSI e TCP / IP che si occupa di far comunicare diversi dispositivi collegati in diverse reti. Cioè in sostanza si occupa di indirizzamento e [instradamento](https://it.wikipedia.org/wiki/Instradamento "Instradamento") verso la giusta destinazione attraverso il percorso di rete più appropriato

Il livello di rete viene definito anche come *best effort*, questo perché non garantisce al 100% che i pacchetti che vengono inviati tra un destinatario e mittente arrivino sempre, ma ci possono essere delle problematiche durante il trasporto di tali pacchetti. La gestione dell’affidabilità viene affidata soprattutto al [[Transport Layer|livello di trasporto]].

Le principali funzionalità che possiede tale livello sono:

- **Inoltrare pacchetti** (_forwarding_), ovvero ricevere un pacchetto su una porta, immagazzinarlo e ritrasmetterlo su un'altra. Questa funzione è presente in tutti i [^1]nodi della rete e può comportare l'utilizzo di protocolli di livello collegamento differenti;

- **Frammentare e Riassemblare i pacchetti che riceve** se un pacchetto ricevuto ha una dimensione eccessiva per la rete su cui deve essere trasmesso, il livello di rete lo divide in frammenti e, in maniera complementare, si occupa di riassemblare i frammenti ricevuti al momento della consegna;

- **Instradare pacchetti**: ovvero determinare il percorso ideale per la trasmissione dei dati attraverso la rete a partire dall'indirizzo IP del destinatario. Nella maggior parte dei casi, questa funzione viene svolta dinamicamente tramite appositi [algoritmi](https://it.wikipedia.org/wiki/Algoritmi "Algoritmi"), che utilizzano le informazioni provenienti dai [protocolli di routing](https://it.wikipedia.org/wiki/Protocolli_di_routing "Protocolli di routing") sulle condizioni della [rete](https://it.wikipedia.org/wiki/Rete_informatica "Rete informatica"), le [tabelle di instradamento](https://it.wikipedia.org/wiki/Tabella_di_routing "Tabella di routing"), la priorità del servizio e altri elementi secondari;

Il dispositivo tipico del livello 3 è il **router**.

Il router riceve un pacchetto, osserva l’indirizzo IP di destinazione e consulta la propria tabella di routing per decidere il prossimo percorso.

>[!example]
`Rete A → Router 1 → Router 2 → Rete B`
I router lavorano principalmente con gli indirizzi IP, mentre gli switch lavorano principalmente con gli indirizzi MAC. 

L’unità di dati del livello 3 è il **pacchetto**. In alcuni contesti si usa anche il termine **datagramma IP**.
# Reference
---

[^1]: In informatica e telecomunicazioni un **nodo** è un qualsiasi dispositivo hardware del sistema in grado di comunicare con gli altri dispositivi che fanno parte della rete; può quindi essere un computer, una stampante, un fax, un modem ecc. In ogni caso il nodo deve essere dotato di una scheda di rete
