---
created: 2026-02-14T15:43:00
tags:
  - baby
topics:
  - Data
  - BigData
  - "[[School]]"
  - AI
author: Danilo Quattrini
---
# Classificazione
---
>[!quote]
>E' una Tecnica della Data Science di tipo [[Supervised And Unsupervised|supervised]] che consiste nell'associare un oggetto ad una **categoria predefinita** sulla base delle sue caratteristiche

La classe è sempre una variabile **categorica** (discreta), non continua. Quando la variabile target è numerica continua si parla di **regressione**, non di classificazione.

## Formalizzazione del problema
Hai un dataset di training composto da record del tipo:
$$(x,y)$$
dove:

- $x=(x1,x2,…,x_{d})$  è un vettore di **feature** (attributi, variabili esplicative, input), come ad esempio l'età il  reddito il numero di visite, tempo sul sito, ecc.
        
- $y$ è l’**etichetta di classe** (output, target, variabile dipendente) come ad  esempio “compra” / “non compra”, “spam” / “ham”.
L’obiettivo è imparare una **funzione modello**:

$$f: x \mapsto \hat{y}$$​

che, dato un nuovo $x_{\text{new}}$, restituisca una classe predetta $\hat{y}_{\text{new}}$ ​il più possibile vicina alla vera classe (che non conosciamo per i nuovi dati)

## Fasi della classificazione
Il processo di classificazione viene solitamente descritto in **tre fasi**:

1. **Costruzione del modello (training / apprendimento)**
2. **Valutazione del modello (testing / validazione)**
3. **Uso del modello (classificazione di nuovi dati)**

Vediamole in dettaglio

### Costruzione del modello
# Reference
---

