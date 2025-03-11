2025-03-06 15:40

Status: #baby 

Tags: [[Math]]

---
# Index
---
- [1.1 Partial and total function](#1.1%20Partial%20and%20total%20function)
- [1.2 Injective function](#1.2%20Injective%20function)
- [1.3 Surjective function](#1.3%20Surjective%20function)
- [1.4 Bijective Function](#1.4%20Bijective%20Function)
- [1.5 Other Functions](#1.5%20Other%20Functions)
# 1.0 Functions
---
Mostreremmo in queso capitolo il concetto di $funzione$ in ambito matematico e in ambito informatico, cioè come il libro andrà a trattare le funzioni al suo interno.

> [!quote] **Funzione in matematica**
> Si dice funzione una relazione chiamata $f$ tra due insiemi che chiameremmo $X$ e $Y$, dove il primo insieme viene chiamato $dominio$ della funzione, il secondo viene chiamato $codomio$.
> 
> Tale relazione $f$ possiede degli elementi del dominio, che ad ognuno di loro, $x$ verrà associato ad uno ed un solo elemento del co-dominio $f(x)$ .
> 
![[function-definitio.png]]

La condizione che deve soddisfare affinché una funzione, venga chiamata tale è la seguente:

> [!hint] **Che cosa deve soddisfare per chiamarsi funzione?**
> Dati due insiemi che abbiamo definito precedentemente i loro nomi, non lo ripeterò, gli elementi di tali insiemi $x \in X$ deve essere associato ad un solo elemento del co-dominio $y \in Y$, e l'elemento $y$ che verrà associato ad $x$ verrà ridenominato $f(x)$ e si legge *f di x*.
> 
> ![[second-function-definition.png]]
## 1.1 Partial and total function
Ora però definiamo due diverse tipologie di funzioni che troviamo all'interno del libro e sono la funzione $totale$ e $parizale$.

> [!quote] **Funzione parziale & totale**
> Data una funzione con dominio $X$ e co-dominio $Y$, diciamo che la funzione è $parziale$ se il dominio di definizione è sottoinsieme di $X$.
> 
> Caso in cui il dominio di definizione coincida con $X$ allora diciamo che la funzione è anche $totale$.

Abbiamo tutte le funzioni che sono $parziali$, cioè abbiamo che ogni insieme è sottoinsieme di se stesso e viene inteso che la funzione $parziale$ contiene parte degli elementi dell'insieme del dominio $X$ se nel caso tale sotto-insieme possiede tutti gli elementi di $X$ allora diciamo che questa funzione diventa $totale$.

Definiamo che una funzione non è definita su un certo input $x$ in questo modo $f(x)\uparrow$ (inteso che la funzione $f(x)$ diverge sul dato input diremmo  inseguito),  caso contrario invece avviene se il dato input invece viene definito da tale funzione $f(x)\downarrow$ (cioè che la funzione $f(x)$ converge, cioè che l'input appartiene al dominio di definizione).

## 1.2 Injective function
Andremmo a dare una definizione dettagliata di funzione iniettiva.

> [!quote] **Funzione Iniettiva**
> Definiamo che la funzione $f$ è $iniettiva$ se a elementi distinti del dominio vengono associati elementi distinti del co-dominio. $$\forall x,y \in Dom(f), x \neq y\Rightarrow f(x)\neq f(y)$$ 
> ![[injective-function.png]]

Si dovrà seguire questa check-list al fine di chiamare una funzione iniettiva tale:
- Ad ogni elemento in input nel dominio della funzione, ci sarà un unico elemento di output nell'insieme del co-dominio.
- Una **funzione inettiva è monotonica**[^1], cioè aumenta o diminuisce al muoversi nella linea dei numeri reali.
- Una **funzione iniettiva non possiede punti critici**, cioè punti in cui la derivata è zero o indefinita.
## 1.3 Surjective function
Prima di parlare del concetto di funzione suriettiva, dobbiamo introdurre il significato di $immagine$ di una funzione.

>[!quote] **Immagine**
>Avendo due insiemi che chiameremmo $A$ e $B$ diremmo che gli elementi dell'insieme $a \in A$, l'elemento $f(a) \in B$ verrà a chiamarsi **immagine** di $a$
>![[image-function-1.png]]
>
>Diremmo che l'*immagine* di 1 è 2, l'*immagine* di 2 è 7 e l'immagine di 3 è 6
>

Ora che sappiamo che cosa significa immagine di un elemento, possiamo introdurre il concetto successivo che si chiamerà *immagine della funzione*

>[!quote] **Immagine di una funzione**
>Il sotto insieme del co-dominio della funzione che prende come elementi, quelli che sono immagine del dominio, vengono ad essere chiamati **insieme immagine della funzione**
>
>![[function-imag.png]]
 >$$\mathrm{Im(f)} = \{f(a):a\in A\}$$
 >"Quello all'interno dell'insieme arancione"

Ora che abbiamo il concetto necessario per discutere dell'argomento, ora possiamo parlare del concetto di funzione suriettiva.

>[!quote] **Funzione suriettiva**
>Definiamo una funzione $suriettiva$, se l'immagine degli elementi del dominio, coincide con l'intero insieme del co-dominio.
>
>![[surjective-function.png]]
>

In matematichese possiamo ora esprimere il concetto in questo modo:
$$\forall y\in Cod(f),\exists x\in Dom(f) \ tale \ che \ f(x) = y$$
Tradotto, per ogni elemento del co-dominio, esistono elementi del dominio tali che le loro **immagini** coincidano con l'intero insieme del co-dominio

## 1.4 Bijective Function
Semplicemente andremmo ad illustrare il concetto di funzione biettiva:

>[!quote] **Definizione Funzione Biettiva**
>La funzione viene detta $biettiva$ se è sia $iniettiva$ che $suriettiva$
>
>![[bijective-function.png]]

Nel secondo caso la funzione non è $iniettiva$ perché gli elementi del dominio non sono associati ad elementi diversi del co-dominio, non essendo $iniettiva$ non sarà neanche $biettiva$.

Nel terzo caso c'è da dire che non è ne $iniettiva$ che $suriettiva$, perché gli elementi immagine del co-dominio non coincidono con l'intero insieme.

>[!info] **Spiegazione**
>Cioè che $x$ è associato ad $1$ che è la sua immagine, $y$ è associato a $2$ che è la sua immagine, ma $z$ è associato alla stessa immagine di $x$ cioè $1$ e non a $3$ rendendo l'insieme immagine della funzione un sotto-insieme che non coincide con l'intero co-dominio, regola che deve soddisfare affinché sia $suriettiva$.

## 1.5 Other Functions
Altre funzioni che andremmo a trattare sono di basso rilievo, ma sono sempre importanti per capire alcuni concetti del libro.

>[!quote] **Funzione Identità**
>Una funzione $id$ viene chiamata $funzione \ identità$ se dato in input un valore ad esempio $x$ andrà a ridare come output lo stesso valore inserito.
>
>![[identity-function.png]]
>$$id: \Bbb N \rightarrow \Bbb N \ dove \ \forall x \in \Bbb N, id(x) = x$$
>
>Cioè per ogni valore di $x$ nel dominio il risultato della funzione $id$ ridarrà lo stesso valore inserito
>

Altra funzione che introdurremmo sarà la $funzione \ indefinita$.

>[!quote] **Funzione Indefinita**
>Una funzione che viene denominata come $funzione \ indefinita$ con il simbolo $\emptyset$, cioè che per ogni input della funzione $\forall x\in\mathbb N$ questa diverge $\emptyset(x)\uparrow$.

Cioè in parole povere è una funzione parziale che non viene definita in nessun input, avendo sia il dominio che la sua immagine che sono vuoti.

Infine parleremmo della $funzione \ constante$.

>[!quote] **Funzione Constante**
>Per ogni numero $k$ che appartiene hai naturali, si viene a dire che la funzione $c_{k}=\mathbb N \rightarrow \Bbb N$ è $constante$, se per ogni input della funzione, questa ritorna il valore di $k$ a prescindere dal valore di $x$.
>$$\forall x \in \mathbb N,\ c_{k}(x)=k$$

Ad esempio se abbiamo come funzione $c_{1}(x)=1$ è una $funzione \ constante$ che ridarrà sempre 1.
# Reference
---
[^1]: **monotonico**: in terminologia matematica una funzione è monotona se il grafico di una funzione aumenta e diminuisce al variare di una delle variabili, di tale funzione.