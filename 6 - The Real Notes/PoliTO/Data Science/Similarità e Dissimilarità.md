---
created: 2026-10-22
tags:
  - baby
topics:
author: Danilo Quattrini
---
# Similarità e Dissimilarità
---
>[!info] Definizone
>La **similarità** e la **dissimilarità** ci consentono di calcolare quanto simili o dissimili sono due oggetti, e vengono calcolate in diversi modi in base alle caratteristiche dell’attributo.

- La **similarità** $s(x,y)$: indica **quanto due attributi siano affini tra di loro**, se hanno un valore elevato allora sono affini, possono raggiungere anche valori molto elevati se sono molto affini tra loro e condividono le stesse proprietà.

- La **dissimilarietà** $d(x,y)$: identifica quando due oggetti siano distinti, diversi tra loro, questo valore può assumere 0 se sono identici tra loro, mentre può crescere se sono diversi.

Esistono diverse tecniche per misurare la similarità e dissimilarietà fra due oggetti:
## Distanza Euclidea
>[!info] Formula
>$$𝑑(𝑥, 𝑦) = \sqrt{ ∑^{n}_{k=1} (𝑥_{k}− 𝑦_{k})^{2} }$$

Sopra abbiamo la formula *Euclidea* con $n$ numero di attributi e $x_{k}$ e $y_{k}$ rispettivamente il $𝑘_{esimo}$ attributo degli oggetti $𝑥$ e $𝑦$. differente In questo si necessita la standardizzazione o la normalizzazine se le scala è differente.

## Distanza di Minkowski
Sarebbe una generalizzazione dei calcoli delle distanze
>[!info] Formula
>$$𝑑(𝑥, 𝑦) =  ∑^{n}_{k=1} [(|𝑥_{k}− 𝑦_{k}|)^{r}]^{\frac{1}{r}}$$

Dove abbiamo sempre i  $n$ attributi, e il valore degli attributi  $x_{k}$ e $y_{k}$ rispettivamente il $𝑘_{esimo}$ attributo degli oggetti $𝑥$ e $𝑦$, come la formula di prima solo che prendiamo il **valore assoluto** (cioè il valore senza segno) del risultato della differenza, elevato ad un valore $r$.

Il valore $r$ può assumere un valore che può essere:
- $r = 1$: (**Distanza di Manhattan**) somma le differenze assoulute degli attributi.
- $r = 2$ (**Distanza Di Euclide**)
- $r = \infty$: (distanza "**suprema**"), indica la massima differenza tra attributi.

## Proprietà delle distanze
Gli algoritmi di data mining, clustering (es. $K$-Means) e classificazione (es. $K$-Nearest Neighbors) necessitano di regole matematiche ben definite per garantire la convergenza e la correttezza dei risultati:

Ci sono delle proprietà comuni che sono:
- **Positiva**: se $d(x,y) \geq 0$ è uguale a $0$ se e solo se $x = y$: cioè indicano che due oggetti possono essere identici oppure che siano diversi tra di loro.
  
- **Simmetrica**: se $d(x,y) = d(y, x)$, serve per vedere se invertendo l'ordine degli attributi il risultato possa cambiare oppure no, questo **evita che l'ordine in cui si valutino gli attributi possano cambiare il risultato finale** .
  
- **Disuguaglianza Triangolare**: $𝑑(𝑥, 𝑧) ≤ 𝑑(𝑥, 𝑦) + 𝑑(𝑦, 𝑧)$ Garantisce che il percorso diretto tra due punti sia sempre minore o uguale a un percorso che passa per un terzo punto intermedio. Questa proprietà viene sfruttata dagli algoritmi per "potare" i calcoli inutili nella ricerca dei vicini più prossimi

- **Proprietà della Similarità ($s(x,y)=1 \iff x=y$, e $s(x,y)=s(y,x)$):** Assicurano che due oggetti identici abbiano similarità massima (pari a $1$) e che il grado di affinità sia simmetrico


## Proprietà della Similarietà
Ci sono delle **proprietà di similarietà**, che sono le seguenti:
- **Similarità massima:** $𝑠(𝑥, 𝑦) = 1$ se e solo se 𝑥 = 𝑦
- **Simmetria**: $𝑠(𝑥, 𝑦) = 𝑠(𝑦, 𝑥)$ 

## Distanza di Mahalanobis
>[!info] Formula
>$$𝑑(𝑥, 𝑦) = (x-y)^{T} (∑(x-y))^{-1}$$

Dove avremmo la sommatoria $∑$ che rappresenta la matrice di covarianza. Consente di calcolare la distanza fra due punti rapportandola alla distribuzione di tutti gli altri punti.

==Aggiungere esempio e spiegazione più dettagliata==

## Similarità tra vettori binari
>[!info] Perché viene usata?
Le tecniche per misurare la similarità fra **vettori binari**

Quando si analizzano dati strutturati sotto forma di **vettori di frequenza** o **insiemi binari** (es. dati di testo, carrelli della spesa, preferenze utenti), le distanze geometriche classiche come quella Euclidea o di Manhattan possono essere fuorvianti. In questi contesti si utilizzano metriche specifiche di similarità.

Dati due vettori binari $p$ e  $q$ ($𝑀_{i,j}$ rappresenta il numero di attributi che in $p$ assumono il valore 𝑖 (0 o 1) e in q assumono il valore 𝑗(0 o 1)).

Ci sono due modi per capire se i due vettori sono simili oppure no:
1. **Simple Matching**:
   $$SMC = \frac{M_{11}+ M_{00}}{M_{01}+M_{10}+M_{11} + M_{00}}$$
2. Jaccard Coefficents: indica il grado di sovrapposizione tra due insiemi, che si indica con `1` se sono sovrapposti `0` se non sono sovrapposti.
   $$J=\frac{M_{11}}{M_{01}+M_{10}+M_{11}}$$
   **Formula per Vettori**
   Prendiamo come esempio in questo caso due insiemi di elementi che sono identificati come $A$ e $B$, possiamo dire che questi due insiemi possono essere presenti in 3 stadi differenti:
	1. $M_{01}$: Ci sono attributi che non sono presenti in $A$, ma che sono presenti in $B$
	   
	2. $M_{10}$: Ci sono attributi che sono presenti in $A$, ma che non sono presenti in $B$
	   
	3. $M_{11}$: Ci sono attributi che sono presenti in $A$, e sono presenti anche in $B$
	
**Formula Per Insiemi**
$$J(A, B) = \frac{\vert{}A \cap B\vert{}}{\vert{}A \cup B\vert{}}$$

Il valore varia tra $0$ (nessun elemento in comune) e $1$ (insiemi identici).

Due clienti hanno i seguenti carrelli della spesa:

- Cliente $A$ = $\{\text{Latte, Pane, Caffè}\}$
    
- Cliente $B$ = $\{\text{Latte, Pane, Biscotti}\}$
    

1. Intersezione ($A \cap B$) = $\{\text{Latte, Pane}\} \rightarrow 2$ elementi.
    
2. Unione ($A \cup B$) = $\{\text{Latte, Pane, Caffè, Biscotti}\} \rightarrow 4$ elementi.
    
3. $J(A, B) = \frac{2}{4} = 0.5$ (50% di similarità).