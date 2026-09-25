---
created: 2026-09-24
tags:
  - baby
topics:
  - Data
  - BigData
  - "[[School]]"
author: Danilo Quattrini
---
# Data Warehouse
---
Oggi le aziende medio-grandi, sono composte da un sistema informativo, che gestiscono varie aspetti dell'azienda, come ad esempio: contratti, utenti, transazioni e altre informazioni utili. Tali basi di dati servono per l'operatività dell'azienda, ma si necessitano anche di delle strategie per mantenere tale basi di dati.

I sistemi a supporto decisionali servono ad aiutare il manager a prendere decisioni aziendali, oggi infatti si parlano di aziende *data driven*, cioè scelte ed operazioni svolte in base ai dati che si sono raccolti ed analizzati al fine di portare valore economico.

Le basi di dati già presenti nell'azienda sono importantissimi, questo perché lo possono utilizzare degli algoritmi predittivi, al fine di tirar fuori degli output che possano portare a decisioni che l'azienda prenderà.

Si parla infatti di **business intelligence** cioè la disciplina di supporto alla decisione
strategica aziendale con l'utilizzo di modelli predittivi

>[!info] Obbiettivo
>Trasformare i dati aziendali in informazioni fruibili

Tali predizioni o informazioni fruibili per l'azienda si devono possedere delle infrastrutture hardware e software adeguati.

>[!quote] Che cos'è una Data Warehouse?
>La **Data Warehouse** (DW) è una base di dati per il supporto alle decisioni mantenuta separatamente dalle basi di dati operative dell’azienda.

La differenza tra una DW e una base di dati tradizionale e che la DW contiene informazioni provenienti da diverse fonti (fogli Excel, CSV, contratti, ecc...), che vengono analizzate, ripulite, integrate and infine organizzati in modo coerente per consentire **analisi storiche e strategiche**.
## Motivo dell'Esistenza della Data Warehouse
Viene utilizzata una basi di dati separata da quella aziendale per motivi di:

- **Prestazioni**: se si eseguissero query complesse sui database aziendali, si potrebbe ridurre le performance dell'azienda, ogni ricerche complesse va a  ridurre le performance delle transazioni operative.
- **Qualità e Gestione dei dati** (qualità dei dati, dati integrati, consistenti, orientati ai soggetti di interesse, dipendenti dal tempo).

>[!warning] N.B
>Il Data Warehouse non serve per “far funzionare l’azienda oggi”, ma per **capire com’è andata l’azienda nel tempo** e supportare decisioni strategiche


## Rappresentazione di una Data Warehouse
È possibile rappresentare un data warehouse in due modi:

**Rappresentazione multidimensionale**: i dati vengono rappresentati come un ipercubo con tre o più dimensioni in cui gli assi direzionali sono le entità coinvolte e ogni intersezione contiene una o più misure (quantità, importo, …) relative a quelle determinate coordinate. ![[Screenshot 2026-09-24 at 11.04.27.png]]

>[!example]
>Prendiamo l'immagine sopra, il cubo nell'asse delle X avrà il Tempo, cioè la data in cui è stato caricato il prodotto per esempio. l'asse delle Y dove ci sono  i diversi negozii e nell'asse delle Z i prodotti. Ogni cella del cubo andrà a contenere la quantità dei prodotti, che in questo caso ne sono 3.


**Rappresentazione Relazionale (a stella)**: le misure presenti nella **tabella dei fatti** sono collegate alle entità (**tabella delle dimensioni**) attraverso delle relazioni.![[Screenshot 2026-09-24 at 11.14.23.png]]
**Tabella dei fatti (fact table)**: al centro dello schema, contiene le **misure** (valori numerici da analizzare, come quantità, importo, costo) e le **chiavi esterne** che collegano alle dimensioni.

**Tabelle delle dimensioni (dimension tables)**: intorno alla tabella dei fatti, contengono le **descrizioni** delle entità (es. tempo, prodotto, cliente, regione) e sono collegate alla tabella dei fatti tramite relazioni (chiavi esterne).

>[!example]
> Nell'immagine sopra abbiamo la tabella centrale che è quella dei fatti che sarebbe `Vendite` che avrà ideologicamente le chiavi come `id_negozio`, `id_tempo`, `id_prodotto` e altri attributi, mentre `Negozio`, `Tempo` e `Prodotti` sono tabelle delle dimensioni che sono attributi della tabella dei fatti.

La **tabella dei fatti** contiene le **misure** (numeri da analizzare), mentre le **tabelle delle dimensioni** contengono le **descrizioni** (contesto delle misure).
## Strumenti di Analisi
È possibile analizzare i dati secondo diverse tecniche:

- [[Analisi Data Warehouse#Analisi OLAP|Analisi OLAP]]

![[Screenshot 2026-09-24 at 11.20.24.png]]
# Reference
---

