---
created: 2026-09-24
tags:
  - baby
topics:
  - "[[School]]"
  - Data
  - DataWareHouse
author: Danilo Quattrini
---
# Analisi Data Warehouse
---
## Analisi della DW
Analizzare una Data Warehouse può avvenire in 4 modi:
- Analisi OLAP
### Analisi OLAP 
OLAP che sta per (Online Analytical Processing) è una tecnologia per eseguire query complesse ed analizzare grandi dimensione di dati in modo veloce ed interattivo. Con OLAP è possibile svolgere delle operazioni di aggregazione (SUM, MUL, DIV, GROUP BY, ecc...) per capirci come quelle eseguite nei database tradizionali, solamente che lo si svolge su più dimensioni. 

>[!help]
>**Cosa intendo con più dimensioni?** 
>Cioè con OLAP posso fare operazioni di aggregazione su tabelle differenti (es. vendite per prodotto, per mese, per regione)

>[!example]
>**Esempio pratico**:  
Un manager vuole sapere: “Quanto ho venduto di ogni prodotto nel Nord Italia, mese per mese, nell’ultimo anno?”  
Con OLAP, questa query viene eseguita in pochi secondi, anche se il DW contiene anni di storico
#### Tipologie di OLAP
| Tipo                              | Come funziona                                                                                                                    | Quando si usa                                                                                                   |
| --------------------------------- | -------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------- |
| **ROLAP** (Relational OLAP)       | I dati restano nel database relazionale (tabelle). Le query OLAP vengono tradotte in SQL e eseguite sul DBMS.                    | Quando i dati sono molto grandi e non vuoi duplicarli. Meno veloce su aggregazioni complesse, ma più scalabile. |
| **MOLAP** (Multidimensional OLAP) | I dati sono memorizzati in **cube multidimensionali** (array ottimizzati). Le aggregazioni sono **pre-calcolate** e memorizzate. | Quando serve massima velocità su query ripetitive. Ideale per dati densi e analisi frequenti.                   |
| **HOLAP** (Hybrid OLAP)           | Combina ROLAP e MOLAP: i dati dettagliati stanno nel relazionale, le aggregazioni stanno nei cube.                               | Quando vuoi un equilibrio tra velocità e scalabilità.                                                           |
|                                   |                                                                                                                                  |                                                                                                                 |

# Reference
---

