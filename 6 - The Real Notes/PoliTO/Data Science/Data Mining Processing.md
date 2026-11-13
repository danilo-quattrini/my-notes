---
created: 2026-10-19
tags:
  - baby
topics:
  - Data
  - "[[School]]"
  - Data Mining
  - AI
author: Danilo Quattrini
---
# Data Mining Processing
---
## Introduzione
I dati non sono mai pronti per un algoritmo di data science o machine learning, quindi c'è la necessità di trasformarli in modo da renderli adatti ad algoritmi di machine learning. Le decisioni oggi vanno prese in base ai dati e dalle evidenze (approccio data driven).

## Definizione di Data Mining
>[!info] Definizione
>Processo dove si estrarre la conoscenza dai dati, perché deve mettere in evidenza del contenuto informativo precedentemente non noto. Questo processo avviene utilizzando diversi algoritmi a seconda dell'obbiettivo.

Si svolge un analisi esplorativa, per capire se i dati hanno un valore aggiunto. Si definisce un obbiettivo e si utilizza una tecnica per estrarre valore, questa conoscenza si chiama **pattern**, cioè delle correlazioni che ci sono tra i dati, che sono delle inferenze che vengono dai dati. **Le inferenze sono basate sui dati che abbiamo**.

>[!example] Esempio
>Supponiamo che vogliamo migliorare l'accesso al pronto-soccorso, in base ai pazienti che voglio accedere al pronto soccorso e il loro codice di importanza.  Per fare una buona analisi bisogna fare tantissime domande, queste vanno poste durante il processo di analisi. **Per estrarre valore bisogna porsi domande**.

Non si svolge più un analisi più strutturata come i processi di una data-warehouse, questa è una situazione iniziale meno definita, cioè non ci si basa su uno schema ben definito, ma **abbiamo bisogno di esplorare per trovare il dominio di interesse**. Bisogna mettere in discussione quello che stiamo facendo.

Si ritorna al concetto di [[Knowledge Discovery Process]], da vedere negli appunti per ripassare come funziona il processo dei dati.

## Tecniche Di Analisi
Ci sono diverse tecniche:
- **Descrittive**: vado ad interpretare i dati, come i pattern di acquisto di un milione di clienti, generando dei gruppi che includono clienti che hanno lo stesso pattern.

- **Predittivo**: genera un modello partendo dai dati, poi dal modello faccio delle previsioni, da un insieme di immagini dei cani, devo classificare la razza dei cani, questi sono definiti com apprendimento [[Supervised And Unsupervised|supervised]], cioè si vanno ad utilizzare degli input per poter allenare dei modelli per ritornare delle associazioni.

Andiamo a studiare questi algoritmi principalmente:
- [[Regole Di Associazione|Regole di associazione]]

- Algoritmi Di Classificazione (Random-Forest, Algoritmo basate sulle regole di Associative), vedremmo come validare la bontà dei modelli.

- Clustering.

Sono però necessarie degli algoritmi di **pre-processing**, per poter normalizzare i dati.  Per ogni macro famiglio esistono attività di [[Data Pre-Processing|pre-processing]], che spesso non servono, ma se vengono fatte miglioreranno il risultato.

