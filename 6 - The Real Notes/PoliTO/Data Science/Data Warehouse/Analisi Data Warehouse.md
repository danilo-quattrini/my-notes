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
- [[#Analisi OLAP|Analisi OLAP]]
- [[#Analisi Mediante Data Mining|Analisi Mediante Data Mining]]
- [[#Presentazione Dei Risultati]]
- [[#Ricercare le motivazioni (Drill-Down)]]
### Analisi OLAP 
OLAP che sta per (Online Analytical Processing) è **una tecnologia per eseguire query complesse ed analizzare grandi dimensione di dati in modo veloce ed interattivo**. Con OLAP è possibile svolgere delle operazioni di aggregazione (SUM, MUL, DIV, GROUP BY, ecc...) per capirci come quelle eseguite nei database tradizionali, solamente che lo si svolge su più dimensioni. 

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
## Analisi Mediante Data Mining
L'analisi mediante Data Mining consiste nell'utilizzare [[Modello Predittivo|modelli predettivi]]  per **eseguire previsioni o scoprire pattern nascosti**, su dei dati che si vanno ad analizzare nella DW.

>[!example]
>- Prevedere quali clienti hanno più probabilità di abbandonare (churn)
>- Identificare quali prodotti vengono spesso acquistati insieme.
>- Stimare la domanda futura di un prodotto.

>[!warning] OLAP Vs Data Mining
>Nell'analisi OLAP noi andiamo a svolgere un'analisi descrittiva del dato, descrivendo il risultato che i dati mostrano (es. quanto ho venduto? 3 prodotti nel mese di dicembre). Mentre un'analisi tramite Data Mining si svolge una previsione, cioè quanto un determinato evento sia probabile che avvenga o che un determinato oggetto si comporti in quel modo si svolge delle previsioni.

## Presentazione Dei Risultati
Una volta analizzati i dati, i risultati devono essere **presentati** in modo chiaro e fruibile.    Strumenti tipici:
    
- **Dashboard** (cruscotti con indicatori chiave, KPI).     
- **Report** (tabelle, grafici, mappe).
- **Strumenti di BI** (Power BI, Tableau, Qlik).

L’obiettivo è trasformare i numeri in **informazioni visive** che i manager possano capire e usare per svolgere delle decisioni.

## Ricercare le motivazioni (Drill-Down)
Per cercare le motivazioni di una data decisione o risultato di una query si svolge un'operazione chiamatasi **drill-down**, dove si va ad analizzare i dettagli dei risultati di una determinata query o richiesta aggregata (cioè composta da più micro-risultati).

>[!example] Esempio
>Stiamo analizzando le vendite dell'anno 2026 di un prodotto sulla bellezza, se si applica il drill-down allora si va ad analizzare le vendite di ogni mese, si scende ancora nell'analisi e si possono analizzare anche le vendite di ogni settimana, fino ad arrivare ai giorni del mese e così via.

In sostanza il **Concetto chiave** è che  il drill-down aumenta la **precisione** e il **dettaglio** dell’analisi (da anni → mesi → settimane → giorni).

Esiste anche l’operazione opposta, il **roll-up**, che aggrega i dati (da giorni → settimane → mesi → anni).
# Reference
---

