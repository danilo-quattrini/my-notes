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
# Modello Predittivo
---
>[!info]
>Il modello predittivo è un algoritmo matematico o statistico che analizza i dati storici per identificare pattern (grafici) e relazioni, con l'obiettivo di stimare il valore di una variabile futura o sconosciuta su nuovi dati.

Nella fase di **Analisi** del processo di Data Science, si colloca subito dopo la _Descrizione analitica_ (che spiega cosa è successo) e serve da base per l' _Analisi prescrittiva_ (che suggerisce quale azione intraprendere).

## Tipologie di Modelli predettivi

La famiglia dei modelli predittivi si colloca nell [classe dei supervised](https://en.wikipedia.org/wiki/Supervised_learning), in cui l'algoritmo impara da un dataset contenente sia le caratteristiche d'ingresso (_feature_) sia le risposte corrette (_target/label_). Si dividono in due macro-famiglie fondamentali:

### Modelli di Classificazione
Utilizzati quando la variabile target è **categorica** (discreta). Rispondono a domande del tipo "sì/no" o dividono i dati in classi predefinite, cioè quando possiamo mettere i dati in uno specifico insieme.

>[!example]
>Rilevamento frodi finanziarie (può essere nel gruppo della transazione _lecita_ vs _frodolenta_), diagnosi medica, filtraggio spam (un'email può essere spam oppure no).

### Modelli di Regressione
Utilizzati per dati che si analizzano sono una variabile / o dati che sono in continua crescita (valori numerici), Calcolano un valore numerico preciso lungo un intervallo

>[!example]
>Stima del prezzo di un immobile, previsione della domanda di energia, calcolo del fatturato futuro

## Esempii di  Modelli Predittivi

| **Algoritmo / Modello**                          | **Tipo**                      | **Descrizione e Utilizzo Tipico**                                                                                                                                                   |
| ------------------------------------------------ | ----------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Regressione Lineare / Logistica**              | Regressione / Classificazione | I modelli più semplici ed interpretabili. La _Lineare_ stima trend numerici; la _Logistica_ calcola la probabilità che un evento appartenga a una determinata classe.               |
| **Alberi di Decisione (Decision Trees)**         | Entrambi                      | Strutture a ramificazione basate su regole di tipo _if-then-else_. Molto intuitivi, trasparenti nell'interpretazione dei risultati ma soggetti a _overfitting_ se troppo complessi. |
| **Random Forest e XGBoost (Ensemble Methods)**   | Entrambi                      | Combinano centinaia di alberi di decisione per creare predizioni estremamente accurate e robuste. Rappresentano lo standard _de facto_ per dati tabellari strutturati.              |
| **Reti Neurali (Deep Learning)**                 | Entrambi                      | Modelli complessi ispirati alla struttura del cervello umano. Ideali per gestire volumi massivi di dati **non strutturati** (immagini, video, audio, testo).                        |
| **Modelli per Serie Temporali (ARIMA, Prophet)** | Regressione                   | Algoritmi specializzati nella predizione di valori futuri tenendo conto della componente temporale, della stagionalità e dei trend (es. flussi di vendita mensili).                 |

# Reference
---

