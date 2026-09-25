---
created: 2026-09-21
tags:
  - baby
topics:
  - Data
  - BigData
  - "[[School]]"
  - AI
author: Danilo Quattrini
---
# Linear Regression
---
>[!quote] Definizione
>La Regressione Lineare è un'algoritmo statistico [[Supervised And Unsupervised#Supervised (Apprendimento Supervisionato)|supervisionato]] che crea delle relazioni / associazione tra una **singola variabile dipendente** ed **una o più variabili indipendenti**.

Questo tipo di algoritmo viene usato spesso per fare previsioni del meteo, analisi dei trend e nei [[Modello Predittivo|modelli predittivi]].

Ma cosa sono le variabili **indipendenti** e le variabili **dipendenti**?

>[!example]
>Prendiamo ad esempio un caso in cui le ore in cui si studia in giorno, implicano il superamento dell'esame con bel voto.

Nel contesto dell'esempio
- **Indipendente** (input): una variabile che non dipende da nessun'altra variabile se non da se stessa, in questo caso sono le ore che si sono studiate in una giornata, che non dipendono da niente.
  
- **Dipendente** (output): la variabile che dipende da un'altra variabile, cioè nel nostro caso il **voto dipende dalle ore studiate**

>[!info] Che cosa fa la Regressione Lineare in toto?
>La Regressione Lineare usa le variabili indipendenti per predirre l'outcome, (risultato) di quella dipendente.
## Best-Fit Line
Nella regressione lineare esiste il concetto di "best-fit line", cioè una linea che va a rappresentare la relazione che esiste tra una variabile indipendente da una dipendente.
### Scopo della Best-Fit Line
Lo scopo della best fit line è quello di minimizzare la differenza che esiste tra il dato presente nel grafo (che andremmo a vedere in breve) e la predizione fatta dal [[Modello Predittivo|modello predittivo]].
![[Pasted image 20260921122216.png]]

In sostanza lo scopo è quello di disegnare una linea dritta che riduce o minimizza la distanza tra i punti dei dati che si sono osservati (quelli che sulla figura sono grigi) e i risultati che si sono predetti o risultanti di un modello predittivo.

Vediamo un'altro grafo che ci aiuta a spiegare ogni singolo elemento della linea di regressione

![[Pasted image 20260921122501.png]]


>[!note] Formula della Best-fit line
>$$y=\beta_{0} + \beta_{1} * x$$
>- $y$ sarebbe la variabile che si è predetta
>- $\beta_{0}$ è l'**intercezione** (interception) che predice il valore di **Y** quando la variabile **X** è 0
>- $\beta_{1}$ è la **pendenza** cioè quanto è incrementato **Y** all'incrementare di una singola unità **X**.


Il risultato è un'equazione predittiva che ci stima il risultato di **Y** per ogni valore di **X**
Vediamo le singole variabili cosa sono e che cosa rappresentano.
- **Y** viene identificato come tutte le variabili dipendenti
- **X** sono tutte le variabili indipendenti
- La variabile $\beta_{0}$ è l'**intercezione** (interception) che predice il valore di **Y** quando la variabile **X** è 0
- La variabile $\beta_{1}$ e la **pendenza** ([[New Words#^d4dfce|slop]]), cioè quanto è incrementato **Y** all'incrementare di una singola unità **X**.

Essendo una funzione avremmo a che fare con il valore di **X** che cresce e che al contempo anche **Y** andrà a crescere con il cambiare di **X**, con la pendenza vediamo solo la differenza tra un stato ad un'altro.

## Formule
Vediamo ora le formule che ci serviranno per calcolare le variabili che abbiamo prima citato:

>[!quote] **Pendenza** (Slop)
$$\beta_{1}= \left[ n*\sum(X*Y) - \sum X * \sum Y \right] / \left[ n*\sum X^{2} - \left( \sum X \right)^{2} \right]$$

Vediamo i singoli elementi di questa formula:
- $n$: numero di dati che vanno ad analizzare;
- $\sum(X*Y)$: la somma del prodotto di ogni valore di $X$ per $Y$
- $\sum X$: la somma di tutti i valori di $X$
- $\sum X^{2}$: la somma del quadrato di ogni singolo valore di $X$
- $\left( \sum X \right)^{2}$: prima fai la somma di $X$, poi dopo fai il quadrato della somma.

>[!quote] Incremento (Increment)
>$$\beta_{0} = \overline{Y} - \beta_{1}*\overline{X}$$

Spieghiamo anche questa volta ogni singolo elemento della formula
- $\overline{Y}$ e $\overline{X}$: sono la media di tutti i valori di $Y$ e di $X$
- $\beta_{1}$: sarebbe la pendenza che abbiamo calcolato prima

>[!quote] Residual
>![[Screenshot 2026-09-22 at 13.51.31.png]]
>Prendiamo questo esempio per capirlo al meglio in un grafo dove abbiamo dei punti in cui nelle variabili indipendenti c'è il peso del topo, nelle variabili indipendenti c'è l'altezza del topo. 
>
>1. Prima si va a disegnare una linea
>2. Si misura tutte le distanze dei tra i punti attuali (che sarebbero i dati che si osservano ovvero l'output del modello) e la linea, che sarebbe il punto in cui noi abbiamo svolto la predizione del risultato e si sommano le varie distanze.
>
>Bene, la distanza tra un dato in output (cioè il punto sul grafo) e il dato predetto (quello presente sulla linea), viene chiamato **Residual**, la formula è la seguente:
>$$Residual=y_{i} - \hat{y}_{i}$$

Con il Residual ci si va calcolare la R-Square formula..

>[!quote] Definizione
>Il calcolo del coefficiente di determinazione chiamato anche. $R^{2}$ è una misura statistica che mostra quanto la variabile indipendente $x$  spiega bene la variazione della variabile dipendente $y$. 
>
>La formula che spiega tale variabile è la seguente:
>$$R^{2} = 1 - \left[ \sum(y-\hat{y})^{2} \right] / \left[ \sum(y - \overline{y})^{2} \right]$$
>- $\sum(y-\hat{y})^{2}$: sarebbe la somma delle differenze di tutti i residuals elevati al quadrato (SSR)
>- $\sum(y - \overline{y})^{2}$: la somma totale della differenza tra $y$ e la media di $\overline{y}$ al quadrato
>- $R^{2}$: è un valore che va da 0 ad 1
# Reference
---
Simple Linear Regression: [here](https://statisticsfundamentals.com/simple-linear-regression/simple-linear-regression-examples/)
