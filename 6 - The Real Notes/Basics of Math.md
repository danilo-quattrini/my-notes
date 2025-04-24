2025-03-21 16:27

Status: #baby 

Tags:  [[Math]], [[Fundamentals of Computer Science]]

---
# 0.0 Index
---
# 1.0 Sets
---
Un insieme è una collezione di elementi, che possiamo interpretare come un cesto che contiene degli elementi in comune tra loro, oppure posso contenere elementi differenti.

>[!example] **Esempio**
>I giochi che si fanno all'aperto possiamo raccoglierli in un insieme, {Calcio, Basket, Pallavolo,...}, sono elementi diversi che però hanno una categoria in comune, cioè che sono {**giochi all'aperto**}

## 1.1 How can we write a sets?
Ci sono due modi per poter rappresentare un'insieme, il primo è tramite la forma di Roster, il secondo è con il metodo "Set-Builder".
## Roster form
Il metodo di roster semplicemente consiste nello scrivere gli elementi dell'insieme dentro alle parentesi graffe -> {elemento1, elemento2, ecc...}, come ad esempio la rappresentazione dei multipli di 5 sono {5, 10, 15, 20, 25, 30, 35….}

Regole per la rappresentazione dell'insieme nella modalità di Roster.

>[!quote] **Regole per rappresentare l'insieme secondo Roster**
>- L'ordine degli elementi non è importante, gli elementi non sempre devono seguire una regola di ordinamento ad esempio $A= \{ a, b, c, d, e\}$ è uguale a dire $A= \{ e, d, a, c, b \}$.
>- Gli elementi all'interno dell'insieme non sono ripetuti, ad esempio la parola *apple*, nell'insieme non si presenterà due volte la $p$ e sarà quindi $A=\{a,p,l,e\}$.
>- L'insieme quando lo definiamo come $finito$ significa che rappresentiamo tutti gli elementi al suo interno, caso invece sia $infinito$, metteremmo i puntini all'ultimo elemento dell'insieme, per rappresentare che continua.

## 1.2 Complement of a Set
L'insieme che chiamiamo complemento e lo denotiamo con la linea sopra l'insieme $\overline A$ sarebbe un sottoinsieme $\subset$ dell'insieme $U$ universo, nel dettaglio possiamo specificarlo come:

>[!quote] **Definizione di Complemento**
>$$\overline A = \left\{  x \in U \ \cap \ x \not\in A  \right\}$$

In parole povere nell'insieme complemento ci sono tutti gli elementi esclusi dal secondo, cioè ad esempio se abbiamo un linguaggio $L=\{ 1,2,3,4,5,6,7 \}$ il suo complemento sarebbe tutti quei valore  che non sono dentro l'insieme che definiamo a sinistra quindi in questo caso:
$$\overline L = \mathbb N - L$$
cioè tutti i numeri maggiori di $7$ quindi $\overline L = \{ 8,9,10,\dots \}$
# Reference
---
 

