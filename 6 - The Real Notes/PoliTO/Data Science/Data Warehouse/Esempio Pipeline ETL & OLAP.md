---
created: 2026-09-28
tags:
  - baby
topics:
  - Data
  - DataWareHouse
author: Danilo Quattrini
---
# Esempio Pratico
---
## Scenario
Immaginiamo un'azienda di **e-commerce** (tipo un negozio online che vende elettronica) che vuole costruire un Data Warehouse per analizzare le vendite.
## Contesto aziendale
L'azienda ha:
- **Database operativo** (MySQL): gestisce ordini, clienti, prodotti in tempo reale.
- **File Excel**: il team marketing tiene traccia delle campagne pubblicitarie.
- **API esterne**: riceve dati sulle recensioni dei prodotti da Trustpilot.
- **Log del sito web**: registra ogni visita, click, carrello abbandonato.

**Obiettivo**: creare un DW che integri tutti questi dati per rispondere a domande come:

- "Quali prodotti vendono di più per regione?"
- "Le campagne marketing influenzano le vendite?"
- "Quali clienti stanno per abbandonare?"

## Funzionamento della ETL nella vita reale

### Estrazione (Extract)
Nella realtà si parte dalla fase di **Estrazione** (Extract) che consiste nell'estrarre come dice il nome i dati dalla sorgente/i, per esempio, abbiamo come nello scenario sopra 4 sorgenti differenti, dove ognuna di loro hanno bisogno di una chiamata differente per poter estrarre tali dati:
- Per il Database usiamo delle query (es `SELECT * FROM vendite WHERE date = "28/09/2026"`)
- Nel foglio excel invece eseguiamo uno script dove la cartella in cui si trova il file Excel viene analizzato ed estratto il dato.
- Con le API esterne invece si fa una richiesta HTTP per poter estrarre il dato.
- Scarica i log dal server web.

### Pulizia (Cleaning)
I dati una volta raccolti devono essere ripuliti e integrati, in modo da seguire gli standard che si sono definiti all'interno della DW, ci possono essere inoltre varie problematiche:

| Problema nei dati grezzi                                             | Azione di pulitura                          |
| -------------------------------------------------------------------- | ------------------------------------------- |
| Date in formati diversi (`27/09/2026`, `2026-09-27`, `Sep 27, 2026`) | Standardizza tutto in `YYYY-MM-DD`          |
| Clienti duplicati (stesso nome, email leggermente diversa)           | Unisci i duplicati, scegli l'email corretta |
| Valori nulli (es. `regione` mancante)                                | Imposta un valore default o scarta la riga  |
| Prezzi negativi (errore di inserimento)                              | Correggi o rimuovi le righe errate          |
| Recensioni con testo in lingue diverse                               | Rileva la lingua, traduci o scarta          |
|                                                                      |                                             |
Il risultato sarà dei dati puliti e consistenti che possono essere elaborati nella fase successiva del processo.
### Trasformazione (Transformation)
I dati devono essere trasformati in modo che si adatti alla DW, cioè si possono applicare delle operazioni sui dati 
# Reference
---

