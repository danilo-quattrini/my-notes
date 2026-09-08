---
created: 2026-02-14T15:43:00
tags:
  - baby
topics:
  - "[[School]]"
  - AI
  - Data
  - BigData
author: Danilo Quattrini
---
# Knowledge Discovery Process
---
Il **Knowledge Discovery Process** (KDD) è un framework / processo iterativo che consiste nell'analizzare una porzione di dati da un dataset (dati grezzi), eseguire degli algoritmi su di essi (pulizia / intersezione dei dati) ed infine estrapolano informazioni nascoste, che possono rimanere utili per un'analisi futura. **Trasforma dati grezzi in conoscenza utile**.

## Fasi de KDD

Gli step del KDD sono i seguenti:
1.  **Data Selection (Selezione):** Dal magazzino dati centrale (Database o qualcos'altro), isoli solo la porzione o le variabili rilevanti per il tuo obiettivo (es. consideri solo gli ultimi 2 anni di vendite).
    
2. **Data Preprocessing (Pulizia e Integrazione):** [[#Rimozione del Rumore|Rimuovi il rumore]], gestisci i dati mancanti e integri sorgenti diverse armonizzando i metadati per garantire la qualità dei dati.
    
3. **Data Transformation (Trasformazione):** Prepari i dati per gli algoritmi (es. riducendo le dimensioni o normalizzando le scale numeriche tra 0 e 1).
    
4. **Data Mining (Estrazione dei Pattern):** Applichi algoritmi di Machine Learning (es. Alberi di Decisione, Clustering, Regressioni) per estrarre schemi nascondi (_pattern_).
    
5. **Interpretation / Evaluation (Valutazione):** Esamini i pattern ottenuti insieme agli esperti di dominio per capire se la conoscenza prodotta è **valida, nuova, utile e comprensibile**.

![[Pasted image 20260902094209.png]]

### Rumore (Data Noise)
>[!info] 
>In Data Science il **rumore** (noise) sono tutti quei dati errati, corrotti o fluttazioni anomale che **distorcono la vera natura del fenomeno** che si vuole studiare.

Con il termine di "rimozione del rumore" si intende quella fase del processo del [[Knowledge Discovery Process|KDD]] in cui si vanno a **rimuovere dati che sono considerati fuori dal comune** o che non sono inerenti con la realtà del dominio di studio.

>[!example]
>- Un sensore di temperatura registra: `20°C`, `21°C`, `20.5°C`, `-999°C` _(errore tecnico)_, `22°C`, `180°C` _(sbalzo di tensione)_. I valori `-999` e `180` sono rumore/outlier. Se l'algoritmo non li ignora, calcolerà una media errata e produrrà modelli sbagliati.

Vediamo degl'esempii di come si può rimuovere il rumore da un'insieme di dati:

- **Binning (Cestinatura):** Si ordinano i dati e si dividono in intervalli (bin), sostituendo poi ogni valore con la media o la mediana del suo intervallo per "smussare" le fluttuazioni erratiche.
    
- **Regressione:** Si adatta una funzione matematica (es. una retta) ai dati per identificare la tendenza reale e scartare i punti totalmente fuori traccia.
    
- **Clustering / Filtraggio degli Outlier:** Algoritmi di raggruppamento identificano i dati isolati dal resto della popolazione per eliminarli o correggerli.
### Metadata
I metadati sono dati che descrivono altri dati, cioè dei label (etichette) che definiamo ai dati per descrivere la loro natura, esempio di metadato può essere: tipo di dato (int, string, float, bool), unità di misura (kg, g, hg, m), la valuta di una moneta (euro, dollari, yen, ecc.)

Perché si utilizzano i metadati? L'utilizzo dei metadati server per far si che i dati siano tradotti con un linguaggio universale, questo perché i dati possono venire da fonti differenti e hanno la necessità di essere tradotti tutti in un'unico formato.

>[!example]
>Significa creare un dizionario comune per far capire agli algoritmi che due dati apparentemente diversi sono la stessa cosa.
>- _Sorgente A (Excel):_ Campo `Prezzo` (valore: `100`, metadato: `EUR`).
>- _Sorgente B (Database SQL):_ Campo `Amount` (valore: `110`, metadato: `USD`).
>
>**Come associarlo mentalmente:** Immagina l'integrazione dei metadati come **il traduttore universale dei dati**. Senza leggere e allineare i metadati, finisci per sommare 100 Euro e 110 Dollari ottenendo 210 (un numero errato). Integrare i metadati permette di unificare i dati in una struttura coerente prima che entrino negli algoritmi.
# Reference
---
[GeekForGeeks](https://www.geeksforgeeks.org/dbms/kdd-process-in-data-mining/)
