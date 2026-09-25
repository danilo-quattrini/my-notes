---
created: 2026-02-14T15:43:00
tags:
  - baby
topics:
  - "[[School]]"
  - Data
  - BigData
author: Danilo Quattrini
---
# Categorie Di Dati
---
I dati possono essere raggruppati in 3 macro famiglie, quest in base al modo in cui vengono ad essere memorizzati all'intero delle specifiche infrastrutture dati:
 ![[Pasted image 20260831114502.png|772]]

## Dati Strutturati

Dati organizzati in griglie rigide composte da **righe e colonne** (tipici dei database relazionali SQL o dei file Excel) e da una struttura standard. Ogni colonna ha un tipo di dato ben preciso (es. _Data_, _Numero_, _Testo breve_).

I dati strutturati possono includere sia dati quantitativi (come prezzi o cifre sul fatturato), sia dati qualitativi (come date, nomi, indirizzi e numeri di carte di credito). Ad esempio, un rapporto finanziario con nomi di società, valori di spesa e periodi di reporting organizzati in righe e colonne è considerato un dato strutturato.

>[!example]
> La tabella dei clienti di una banca (ID Cliente, Nome, Cognome, Saldo).

## Dati Non-Strutturati
Dati che **non hanno un formato o un modello di dati predefinito** (cioè non sono rappresentabili come dati elencati tra quelli strutturati). Non possono essere inseriti direttamente in tabelle senza prima essere analizzati.

I set di dati non strutturati sono in genere di grandi dimensioni (terabyte o petabyte di dati) e comprendono il **90% di tutti i dati generati dall'azienda**, come si vede dall'immagine di sopra

I dati non strutturati **possono contenere dati testuali e non**, così come dati qualitativi (commenti sui social media) e quantitativi (cifre incorporate nel testo).

Tali dati sono gestiti da [database non relazionali o NoSQL](https://www.ibm.com/it-it/think/topics/nosql-databases) oppure in [data lake](https://www.ibm.com/it-it/think/topics/data-lake), progettati per gestire enormi quantità di dati non elaborati in qualsiasi formato. Tali dati possono essere ad esempio:

> [!example]
> Dati non strutturati ma da fonti di dati testuali includono
> - E-mail
> - Documenti di testo
> - Post sui social media
> - Trascrizioni delle chiamate
> - File di testo dei messaggi, come quelli provenienti da Microsoft Teams o Slack
>   
> Esempi di dati non strutturati non testuali includono:
> - File di immagine (JPEG, GIF e PNG)
> - File multimediali
> - File video
> - Attività sui dispositivi mobili
> - Dati sensoriali dai dispositivi [Internet of Things](https://www.ibm.com/it-it/think/topics/internet-of-things) (IoT)

### Dati Semi-Strutturati 
Dati che non usano tabelle rigide, ma contengono **etichette (tag) o marcatori** per separare gli elementi.
    
>[!example]
> File **JSON** o **XML** (usati nei database NoSQL come MongoDB), non sono presenti in tabelle come quelli strutturati, ma son allo stesso tempo rappresentabili tramite dati ben precisi, come strighe, numberi, booleani e via .
# Reference
---

	