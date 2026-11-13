---
created: 2026-02-14T15:43:00
tags:
  - baby
topics:
  - OSI & TCP / IP
  - "[[School]]"
  - Cybersecurity
author: Danilo Quattrini
---
# Data Layer
---
Il Data Layer oppure chiamato anche livello di collegamento dati, organizza i bit del livello fisico in una struttura dati più formale chiamata **frame** oppure anche trama. Tale livello andrà a creare un [pacchetto](https://it.wikipedia.org/wiki/Pacchetto_\(reti\) "Pacchetto (reti)") (per più dettagli vedi [qui](https://it.wikipedia.org/wiki/Pacchetto_(reti))) di informazioni  provvisto di un nuovo _[header](https://it.wikipedia.org/wiki/Header "Header")_ (intestazione) e _tail_ (coda), usati anche per sequenze di controllo.

Funzioni importanti:

- creazione e interpretazione dei frame; 
- indirizzamento fisico tramite indirizzi MAC;
- controllo dell’accesso al mezzo trasmissivo;
- rilevamento degli errori;
- gestione della comunicazione locale;
- comunicazione tra schede di rete e switch.

L’indirizzo MAC identifica un’interfaccia di rete all’interno della rete locale. Un esempio di indirizzo MAC è:
```
A4:5E:60:12:34:56 or 8a:0c:e8:80:af:f5
```

Solitamente chi lavora a questo livello è lo switch or il bridge. 

Lo switch riceve i frame e decide su quale porta inoltrarli in base all’indirizzo MAC di destinazione.

Per esempio:

`Computer A → Switch → Computer B`

Se A e B appartengono alla stessa rete locale, lo switch può inoltrare il frame senza coinvolgere un router, conosce in questo caso l'indirizzo MAC del computer B.

L’unità di dati del livello 2 è il **frame** che è il modo in cui viene denominato il pacchetto dati al livello 2 del modelli ISO / OSI.
# Reference
---

