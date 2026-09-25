---
created: 2026-02-14T15:43:00
tags:
  - baby
topics:
  - Data
  - BigData
  - "[[School]]"
author: Danilo Quattrini
---
# Regole Di Associazione
---
>[!quote] Definizione
>Tecnica del Data Science che consiste nell'individuare pattern e correlazione tra i dati di diversa natura all'intero di un database tradizionale.

Le regole di associazione servono a individuare correlazioni e pattern frequenti all'interno di database transazionali (es. gli acquisti in un supermercato, la cosiddetta _Market Basket Analysis_).

Una regola si esprime nella forma:
$$
X \implies Y
$$
Dove preso un'insieme di *item* $I=\{i_{1}, i_{2}, \dots, i_{n}\}$ con $n\in N$ (che possono essere per esempio latte, burro, pasta, ecc), si prende un suo sotto insieme (una porzione / parte dell'insieme degli item ad esempio il pane e il burro) e questo sotto-insieme sarà $X$ e $Y$.

In parole più formali:
$$
X, Y \subseteq I
$$
Abbiamo $X$ ed $Y$ che sono sotto-insiemi di $I$ che nella formula sono chiamati:
- $X$ **Antecedente**: L'insieme o il singolo elemento acquistato o presente
- $Y$ **Conseguente**: l'oggetto a cui associamo $X$

Cioè se un record contiene $X$, allora è probabile che contenga anche $Y$

## Formula Matematica

Nella formula dobbiamo quindi considerare i seguenti elementi:

- $N$: sono il numero delle transizioni / record presenti nel database.
- $count(X)$: conta il **numero delle volte in cui $X$ è presente all'interno del database** con le transizioni
- $count(X \cup Y)$: conta il **numero dell volte in cui sia X che Y siano presenti all'interno del database**:

### Supporto (Support)
Calcola la percentuale di quante volte un'insieme di elementi si presente nel database (insieme di transizioni), cioè in percentuale quante volte un'elemento si ripete.
$$
\text{Supporto}(X \implies Y) = P(X \cap Y) = \frac{\text{count}(X \cup Y)}{N} • 100
$$
>[!info]
>**Significato:** È la percentuale (o frazione) di transazioni totali che contengono sia $X$ che $Y$

### Confidenza (Confidence)
Misura la forza dell'implicazione, cioè la probabilità condizionata che si verifichi $Y$ dato che si è verificato $X$
$$\text{Confidence}(X \implies Y) = P(Y \mid X) = \frac{\text{Supporto}(X \implies Y)}{\text{Supporto}(X)} = \frac{\text{count}(X \cup Y)}{\text{count}(X)}$$
>[!info]
>Tra tutti i record che contengono $X$, qual è la percentuale di quelli che contengono anche $Y$?

### Lift (Incremento)
Misura quanto la presenza di $X$ aumenti la probabilità che si verifichi $Y$, rispetto al caso in cui $X$ e $Y$ fossero del tutto indipendenti.

$$\text{Lift}(X \implies Y) = \frac{\text{Confidenza}(X \implies Y)}{\text{Supporto}(Y)} = \frac{P(X \cap Y)}{P(X) \cdot P(Y)}$$

- $\text{Lift} = 1$: $X$ e $Y$ sono indipendenti (nessuna associazione).
- $\text{Lift} > 1$: Associazione positiva ($X$ invoglia/aumenta l'acquisto di $Y$).
- $\text{Lift} < 1$: Associazione negativa (la presenza di $X$ rende meno probabile $Y$).
## Quale tipo di regola è più interessante?

In generale, le regole con **lift significativamente > 1** sono più interessanti, perché indicano una **vera associazione** oltre la semplice frequenza

Regole con lift ≈ 1 o < 1 possono comunque essere utili se:
- la confidenza è molto alta,
- e l’item Y ha un margine di guadagno elevato.
# Reference
---

