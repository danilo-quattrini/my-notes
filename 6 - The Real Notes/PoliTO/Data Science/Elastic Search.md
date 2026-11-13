---
created: 2026-11-03
tags:
  - baby
topics:
  - Data
author: Danilo Quattrini
---
# Elastic Search
---
**La query ora diventa un testo** (esempio una ricerca di google al livello base in base alle parole). Da questo testo vado a trovare dei **match** vicine che siano simile o che siano rilevanti per il sistema per la ricerca. Il risultato sarà una lista di tuple ordinate.
## Introduzione
>[!info] Che cos'è?
> Distribuzione che ci permette di eseguire un'analisi ed una ricerca avanzata in tempo reale.

![[IMG-Elastic Search-20261103.png]]

Questo è un sistema non relazione, che prende dei documenti semi-strutturali (JSON), dove si contiene diversi formati di testo che possono essere: date, array di valori, longitutide, latitudine, numeri.

**Ogni documento è indicizzato e ricercabile**, cioè che possiede una chiave ed un valore:
```json
[
	key: value
]
```
semplicemente come un documento JSON

# Rappresentazione dei Dati
## Associazione Tra SQL e Elastic
C'è un parallelismo tra Elastic e SQL, dove si ha il caso dove ogni campo in Elastic non sono obbligatori come le colonne in SQL e ci possono essere più valori di differenza natura o di natura uguale.
![[IMG-Elastic Search-20261103-1.png|1040]]

Nell'immagine sotto abbiamo quello prima era in SQL ora in Elastic si traduce in questo modo.
![[IMG-Elastic Search-20261103-2.png]]
**Cluster**: insieme di documenti distribuiti che sono collegati tra di loro in un determinato modo.

### `index`

L'`index`  è una keyword che viene utilizzata per inserire un documento all'interno di Elasticserach se viene utilizzata come accezzione di verbo.  Se viene utilizzata come accezione di  nome l'`index` contiene la collezione di documenti

### Document
Il documento è una collezione di elementi, rappresentati in JSON, che contengono del testo ed è identificato da un indice (`index`) che ci aiuta a capire dov'è il documento e un `id` che identifica il documento.

# Querying & Searching
Si possono svolgere le query in due diversi pesi:
- **Hard**: simile come una query SQL e sono delle query che vengono svolto in uno specifico dato.
  
- **Soft**: query che viene svolta nell'intero testo, dove svolte un matching in base alla ricerca per chiave ritornando un risultato ordinato.

Si possono combinare i due approcci che si sono appena descritte.

## Concetti chiavi

>[!info] Mapping
>Quando si parla di **mapping**, si intende come il processo di come i dati sono interpretati o associati al suo significato, per esempio si può indovinare il tipo di dato che possiede il tipo di variabile `date`

>[!info] Analysis
>Come il processo di ricerca nell'intero documento di testo viene performata.

>[!info] Query DSL (Domain Specific Language)
>C'è un linguaggio SQL dedicato in Elastic che però nel corso non viene utilizzato.