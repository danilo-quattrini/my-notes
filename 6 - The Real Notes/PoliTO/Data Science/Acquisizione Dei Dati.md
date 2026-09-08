---
created: 2026-02-14T15:43:00
tags:
  - baby
topics:
  - Data
  - "[[School]]"
  - BigData
author: Danilo Quattrini
---
# Acquisizione Dei Dati
---
## Pull Based vs Push Based

La differenza dipende da **chi prende l'iniziativa** nel trasferimento del dato tra la fonte e il Data Center

| **Modalità**                           | **Chi attiva la comunicazione?**          | **Funzionamento**                                                                                  | **Esempio Pratico**                                                                                                                                                                        |
| -------------------------------------- | ----------------------------------------- | -------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Pull-based** _(pull come su github)_ | **Il Data Center -> (noi)**               | Il nostro sistema fa periodicamente una richiesta ("tira a sé" il dato) alla fonte per scaricarlo. | Un **Web Crawler** che ogni notte visita i siti dei concorrenti per estrarre i prezzi dei prodotti.                                                                                        |
| **Push-based** _(A spinta)_            | **La Fonte (il mittente) -> Data Center** | La fonte invia ("spinge") continuamente i dati verso il Data Center non appena vengono prodotti.   | Una **telecamera di videosorveglianza** che invia un flusso video continuo (_stream_), oppure il tracciamento dei click di un utente (_clickstream_) inviato istantaneamente a ogni click. |
# Reference
---

	