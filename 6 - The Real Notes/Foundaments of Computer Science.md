---
share_link: https://share.note.sx/x55z3eyu#SFVgtoBmnCXdpbKyaR8bKF6HApBqtzbx8i2+TwLIjJQ
share_updated: 2025-03-18T09:25:41+01:00
---
2025-03-04 16:26

Status: #baby 

Tags: [[Programming]], [[General Knowledge]], [[Math]]

Other notes: *[click here](https://francescopalozzi.notion.site/Appunti-39bc6581d2c9426280d354c261187919)*

Formulario: *[click here](https://francescopalozzi.notion.site/Formulario-Fondamenti-efd19dff3ff94e488d24661e0fd325d7)*

Esercizi: [click here](https://097475.github.io/computazione-calcolabilita/excercises.html)

---
> [!warning] **N.B**
> In questi appunti ci sono solo le parti che ritengo necessarie per la comprensione dei concetti, ci saranno immagini e formule, ma per altri chiarimenti, leggere il libro nel capitolo/parte che viene citata nelle *footnotes*
# Index
---


# 1.0 Stringhe e Linguaggi
---
Prima di tutto partiamo con due concetti fondamentali, il primo è quello di *Alfabeto*, il secondo è quello di *Stringa*.

> [!quote] **Definizione**
> ***Alfabeto***: viene definito come quell'insieme, non vuoto, di elementi che non posseggono interpretazione.
> 
> $$ A = \{ a, b, c, \dots , x, y, z \} $$

Invece abbiamo anche il concetto di *Stringa* che viene inteso come:

> [!quote] **Definizione**
> ***Stringa***: viene intesa come quell'insieme finito di simboli di un determinato *Alfabeto*
> 
> $$ S = aabbcc, ab135, abdef $$ stringhe che appartengono all'Alfabeto $$ A = \{a, b, c, \dots, 0,1, \dots, 9\} $$
> è una sequenza di simboli ottenuta per concatenazione di simboli.

Per rappresentare la *stringa vuota* si usa il lambda $\lambda$.

> [!important] **Usato spesso** 
> 
> $$\lambda \implies striga vuota$$

---
Per la nostra stringa possiamo rappresentare ora il concetto di *lunghezza*, che viene espressa dalla funzione $l(\alpha)$ dove $\alpha$ viene a indicare la stringa che utilizziamo.

> [!important] **Esempio**
> Prendiamo come esempio questa stringa:
> $$\alpha=adfal$$ la lunghezza di $\alpha$ sarà il numero dei simboli che contiene la stringa, quindi: $$l(\alpha) = 5$$

Come possiamo pensare giustamente anche la nostra lamba avrà una lunghezza che sarà 0, dato che è una stringa vuota, non possiede nessun simbolo.
$$l(\lambda )=0$$
Possiamo anche concatenare le stringhe, date due stringhe appartenenti ad un'alfabeto $A$ che possiamo denominare $\alpha$ e $\beta$ la loro unione sarà una nuova stringa che prenderà il nome di $\gamma$ .

> [!important] **Esempio**
> Prendiamo la stringa $\alpha=bdfkasd$ e $\beta=kfdla$ avremmo la concatenazione dei due con:
> $$\gamma = bdfkasdkfdla$$
> 
> Rappresenteremmo la concatenazione con il pallino: •.

Esiste un'altro modo per rappresentare la concatenazione, come ad esempio, la concatenazione di più simboli dello stesso tipo.

Si viene a rappresentare una stringa su un alfabeto qualsiasi, viene allora definito. $\alpha^{i}$ dove abbiamo che $i\in \mathbb N$, illustriamo qualche esempio di questa concatenazione.
$$ab^{2}c^{3} = abbccc$$
$$a^{4}d^{5}e^{2} = aaaadddddcc$$
$$(ab)^3=ababab$$
---
Descriviamo anche il concetto di $sottostringa$ introducendolo in questo modo:
> [!quote] **Definizione**
> Diciamo che una data stringa $\alpha$ è una sotto stringa di $\beta$ se $\beta=\gamma•\alpha•\rho$ dove $\gamma$ e $\rho$ sono delle stringhe 

Facciamo un'esempio di $sottostringa$ per capire bene il concetto:
$$\beta=fdad \qquad sono \ sottostringhe:\ \lambda,f,fd,fda,dad,ad,fdad$$
Si viene poi ad evidenziare il concetto di *suffisso* e *prefisso* proprio e non, prendiamo lo stesso esempio di prima:
$$\beta = fdad \qquad suffisso:\ \lambda,d,ad,dad \qquad prefisso: \lambda ,f,fd,fda$$
Sono considerati suffissi e prefissi propri se $\gamma \neq\lambda \ or \ \rho\neq\lambda$ , nell'esempio prima sono tutti e due suffissi e prefissi propri perché o prima o dopo dei simboli ci sono altri simboli e non sono vuoti ($ad$ prima avrà $fd$ quindi è un suffisso proprio).

Possiamo anche dire che è prefisso se data una stringa $\beta=flavio$ possiamo generare da quest'ultima tramite la $concatenazione$ stringhe insieme generino la stringa finale.
$$\gamma = fla \ \rho=vio \qquad \gamma•\rho=flavio$$
Bisogna dire che è un **prefisso e il suffisso sono delle stringhe**.

---
Poi possiamo rappresentare l'inversa di una stringa tramite l'utilizzo della notazione $\alpha^{rev}$ dove che sta a indicare la sua $inversa$ cioè ad esempio:

>[!important] **Esempio**
>Prendiamo ad esempio una stringa casuale $\alpha=afdae$ la sua inversa sarà $\alpha^{rev}=eadfa$ con la stringa composta da un solo simbolo sarà $\alpha^{rev}=\alpha$ stessa cosa per la stringa vuota $\lambda^{rev}=\lambda$

## 1.1 Linguaggi e insieme di stringhe

Definiamo ora il concetto che dato un determinato alfabeto $A$, da quest'ultimo possiamo generare una serie di stringhe che sono racchiuse in un insieme che denotiamo con $A^{*}$, se volessimo escludere la stringa vuota allora il nome dell'insieme cambia e sarà $A^{+}$, quindi potremmo anche dire in termini matematici che:$$A^{+}=A^{*}\ - \{\lambda\}$$
Il nostro alfabeto $A$ può possedere anche un ordinamento che potrà essere deciso da noi, ad esempio prendiamo un alfabeto qualsiasi $A=\{a_{1},a_{2},\dots,a_{n}\}$ dove le nostre $a$ sono i simboli dell'alfabeto, e impostiamo un ordinamento totale tramite il simbolo $<$ di maggiore all'interno dell'insieme, avendo così il nostro ordine totale all'interno dell'insieme, lo visualizzeremmo alla fine in questo modo:
$$a_{1} < a_{2} < \dots < a_{n}$$
Definendo un ordine all'interno del nostro alfabeto, andremmo anche a definirlo in concomitanza con le stringhe che andremmo a generare da tale alfabeto.

---
Esiste perciò una regola che definiamo per ordinare le stringhe all'interno di un determinato alfabeto e lo definiamo con il termine di $lessicografica$

> [!quote] **Definizione**
> Prese due stringhe $\alpha$ e $\beta$ generate da un alfabeto $A$ che possiede un ordinamento, prendiamo caso che $\alpha <\beta$, si definisce il termine che $\alpha$ è $lessicograficamente \ minore$ di beta o viceversa, dove diremmo che $\beta$ è $lessicograficamente \ maggiore$ di alpha, se vale uno dei due casi:
> - $\alpha$ è prefisso proprio di $\beta$
> - nel caso $\alpha$ possiede un prefisso $\gamma• a$ e $\beta$ avrà pure lui un prefisso $\gamma• b$, dove la nostra stringa gamma $\gamma\in A^{*}$, ma in questo caso se escludessimo il gamma, avremmo $a,b\in A$, dove $a < b$ nell'ordinamento di $A$

^f2e44b

Consideriamo l'alfabeto $D = \{0,1, 2, 3, 4, 5, 6, 7,8, 9\}$ delle cifre decimali dove si fissa, come di consueto, $0 < 1 < 2 < ... < 9$.

L'ordine che ne deriva sui naturali, intesi come stringhe in $A^{*}$ non è il loro ordine abituale: $16 < 160$ perché il primo è un prefisso proprio del secondo e $151 < 153$ perché per $\gamma = 15$ abbiamo che $1 < 3$, ma $10 < 5$, perché per $\gamma = \lambda$ abbiamo che $1 < 5$.

Chiarito ora il concetto di $lessicografia$ ora passiamo alla definizione di $linguaggio$

>[!quote] **Definizione**
>Dato un determinato alfabeto $A$, da cui possiamo generare delle stringhe che faranno poi parte dell'insieme $A^{*}$, il $linguaggio$ che definiamo con la notazione $L$ è un sottoinsieme di $A^{*}$.

Cioè con il $linguaggio$ andremmo a definire dei vincoli nell'insieme delle stringhe che andremmo a generare da un'alfabeto $A$, ad esempio:

- L'*insieme dei numeri primi è un linguaggio* su $D = \{0,1,2,..., 9\}$ (e su qualunque altro alfabeto per i naturali). 
- L'insieme delle parole della lingua italiana è un linguaggio sull'alfabeto S delle lettere latine.
- L'insieme dei numeri binari palindromi[^1] è un linguaggio sull'alfabeto $B = \{0, 1\}$ delle cifre binarie.

Nei $linguaggi$ possiamo anche trovare anche la tipologia che fa parte dell'insieme vuoto $\varnothing$, cioè non ci sono stringhe presente nel linguaggio che segue la condizione che viene posta, da non confondere con il concetto di stringa vuota mostrata dal simbolo del $lambda$ $\{\lambda \}$.

# 2.0 Funzioni
---
Per analizzare il concetto di funzione andremmo a vedere appunti che sono presenti qui:
[[Functions]]

# 3.0 Definition of Algorithm
---
Ci saranno dieci punti che verranno illustrati e spiegati nella maniera più comprensibile all'essere umano, delle regole che un algoritmo deve seguire per chiamarsi tale, le elencheremmo qui sotto:

-  **Il nostro algoritmo è di lunghezza finita.** 
	   Cioè si conclude non è infinito.
***
- **Esiste questo $agente\  di \ calcolo$ che esegue la computazione (calcoli matematici) svolgendo le istruzioni dell'algoritmo.**
---
- **Il nostro $agente \ di \ calcolo$ possiede una memoria che salva al suo interno i dati in input, output e i risultati dei calcoli intermedi della computazione**.
---
-  **Il calcolo avviene per passi discreti**
	 Cioè un passo dietro all'altro.
---
- **Il calcolo non è probabilistico.** 
	Cioè non esiste nessuna legge sulla probabilità che un passo successivo possa essere compiuto o no, ma è definito, cioè si sa per certo che cosa avverrà dopo una computazione fatta in precedenza (per questo si dice deterministico).
---
- **Non deve esserci alcun limite finito alla lunghezza dei dati in ingresso**.  
	Cioè l'input di un dato deve essere arbitrariamente grande quando si vuole, di qualsiasi dimensione.  
---
- **Non deve esserci alcun limite finito alla quantità di memoria disponibile dall’agente di calcolo**.  
	Cioè il nostro calcolatore, chiamiamolo così non avrà memoria illimitata (realmente non esiste oggi giorno un computer con memoria illimitata, ma grande abbastanza da poter svolgere i calcoli di grandi dimensione).  
---
  
- **Deve esserci un limite finito alla complessità delle istruzioni eseguibili dall’agente di calcolo**.(Il punto 8 è collegato con il 1°). 
	Il collegamento viene perché l'algoritmo non solo deve possedere dei passi finiti, ma la complessità dei singoli passi deve essere limitata a un uso parziale della memoria dell'agente di calcolo.  
---
- **Non c’è alcun limite finito al numero di passi della computazione.**  
	Il punto dice che non si può sapere a priori in quanti passi un algoritmo concluderà la sua esecuzione sulla base dell'input che inseriamo.  
---  
- **Sono ammesse computazioni con un numero di passi infinito, computazioni che non terminano mai.**  
	Questo avviene solo nei problemi che non possiedono una soluzione, portando così al prolugamento della computazione del problema ad un punto senza fine (cioè non portano più risultati).
## 3.1 Algorithm that cannot solve all the functions

Partiamo dall'esistenza di questo insieme che chiameremmo $S$, dove troveremmo un linguaggio per esprimere algoritmi e anche un agente di calcolo che esegue questi algoritmi.

Semplicemente in questo capitolo vedremmo che ci saranno problemi che non sono algoritcamente risolvibili, qualsiasi sia il nostro insieme $S$ di partenza, cioè che non ci saranno sempre soluzioni per la sua risoluzioni.

Facciamo esempi di due algormi che sono differenti, ma che calcolano la stessa funzione
```js
begin
	input(x);
	output(x+1)
end
```
 
In questo caso la funzione è sempre da dominio e co-dominio $f:\mathbb N\to \mathbb N$, ma se prendiamo in questo caso l'esempio qui sotto:
```js
begin
	input(x);
	x := x + 1;
	x := x - 1; 
	output(x + 1)
end
```
La funzione è sempre la stessa, ma l'algoritmo $sitatticamente$ è sempre lo stesso, questo per spiegare il concetto che vediamo dopo.

Definiamo come $A$ l'insieme degli algoritmi presenti all'interno dell'insieme $S$, quindi $A \subset S$, poi troviamo la funzione che viene calcolata dall'algoritmo presente nell'insieme $A$, che chiameremmo $f_{A}$, che come dominio avremmo i possibili input dell'algoritmo e come co-dominio i possibili output dell'algoritmo.

$$A_{S} \to f_{A}:\mathbb N \mapsto \mathbb N$$

Ad ogni input data alla funzione $f_{A}$, ci possono essere casi in cui l'algoritmo $A$ non termina, dicendo così che la **funzione sarà indefinita**, sul quel dato input, cioè che quei valori che non riescono a far concludere l'algoritmo, non faranno parte del dominio di definizione (dominio), della funzione.

>[!example] **Esempio**
>Ad esempio se abbiamo un input $n$, la funzione la definiamo che $diverge$, in questo caso tramite questa notazione $f(n)\uparrow$, cioè che la funzione non è definita, cioè che va in loop.

> [!warning] **Importante**
> Le funzioni che vedremmo da qui in poi avranno come dominio e co-dominio valori naturali $f:\mathbb N \to \mathbb N$, lo vedremmo meglio in dettaglio nel capitolo 4.4.2 e 4.4.3 dove qualsiasi sequenza di input e di output può essere codificata come un numero naturale.

Ad ogni algoritmo $A$ corrisponde a una sola funzione che calcola, ma la funzione può essere calcolata da più di algoritmi, oppure la funzione può esistere da sola e non essere calcolata da nessun algoritmo, denotiamo la differenza di $A$ come **singolo algoritmo** invece $A_{S}$ l'**insieme di tutti gli algoritmi in** $S$.

Definiamo allora:
$$F_{S} = \{f_{A}\ |\ A \in A_{S}\}$$
Spiegate in parole umane, $F_{S}$ sarebbe un insieme che contiene tutte le funzioni $f_{A}$, che possono essere calcolate dagli algoritmi presenti nell'insieme $A_{S}$.

Definiamo l'insieme delle funzioni dai naturali ai naturali:
$$F=\{f:\mathbb N \to \mathbb N \}$$
Diciamo anche la l'insieme delle funzioni calcolate da un algoritmo:
$$F_{S} \subset F$$
Cioè l'insieme delle funzioni calcolabili è un sottoinsieme stretto delle funzioni dai naturali ai naturali, come sopra citato.

Poi non si sa come si comincia con il concetto di dire che due insieme infiniti che identifichiamo come $I$ hanno l a sessa cardinalità, se possiamo metterli in [[Functions#1.2 Injective function|corrispondenza biunivoca]] (vedere la definizione di funzione iniettiva che spiega anche la biunivocità).
$$|I_{1}| = |I_{2}|$$
>[!example] **Esempio**
>Per esempio l'insieme dei numeri naturali e l'insieme dei numeri pari hanno la stessa cardinalità perché sono in corrispondenza biunivoca tramite $x → 2x$, cioè la sua funzione sarebbe $f(x)=2x$, dove per ogni naturale del dominio viene associato un valore del co-dominio, che sarebbe un multiplo di $2$.
> 

Se $I_{1}$ può essere messo in corrispondenza biunivoca con un sottoinsieme di $I_{2}$ allora diremo che:
$$|I_{1}| \le |I_{2}|$$
Se in tal caso invece non c'è alcuna  biettività tra i due insiemi allora si scrive così:$$|I_{1}| \lt |I_{2}|$$
Allora c'è sto Cantor che ha scoperto una cosa figa, che la cardinalità dell'insieme $I$ sarà strettamente minore dell'insieme dei suoi sottoinsiemi, che viene indicata con $2^{I}$(spiegata a cazzo, ma vuol dire la quantità di sotto-insiemi che si possono generare da un insieme), facciamo un esempio che si possa capire tipo meglio.

Abbiamo un insieme che chiameremmo $T$ che è composto da $n$ elementi al suo interno, quindi la cardinalità dell'insieme sarà la quantità di elementi al suo interno, cioè $n$, quindi sarà $|T|=n$, fino a qui ci siamo.

Il sotto insieme viene identificato da una stringa binaria, dove rappresenteremmo $1$ se l'elemento fa parte del sotto-insieme o $0$ se non c'è, facciamo un esempio:

>[!example] **Esempio**
>Prendiamo come ad esempio $T=\{1,2,3\}$ , l'$i-esimo$ elemento dell'insieme ad esempio $i=0$ sta per $t_{0}=1$, come negli array, stesso ragionamento, indice che punta all'elemento dell'array (elemento dell'insieme), se diciamo ad esempio $101$, sarebbe che il primo elemento è incluso nel sotto-insieme, il secondo no perché è $0$, il terzo si, quindi avremmo come sotto-insieme $\{ 1,3 \}$

Il numero dei bit della stringa binaria va in base alla cardinalità dell'insieme preso in considerazione, in questo caso $|T|=3$ quindi saranno $3$ i bit della sequenza binaria e si potranno generare $2^{3}= 8$ sotto-insiemi.
 
Infine diciamo che i numeri dei sotto-insiemi che si possono generare da un insieme dipende da quanti elementi ci sono nell'insieme. (non era difficile, ma sul libro spiega super complesso).
$$numero\ di \ sottoinsiemi=\{|T| = n \ tale \ che \ 2^{n}\}$$
> [!example] **Altri esempi**
> - $T=\{ 5,2,3,7,0 \}$ se dicessimo in binario $10100$, sarebbe il sotto insieme $\{ 5,3 \}$
> - $T=\{ 5,2,3,7,0 \}$ se dicessimo in binario $10111$, sarebbe il sotto insieme $\{ 5,3,7,0 \}$
> - $T=\{ 5,2,3,7,0,2,8 \}$ se dicessimo in binario $1011011$, sarebbe il sotto insieme $\{ 5,3,7,2,8 \}$
> 
> Avremmo quindi che l'insieme dei sotto-insiemi di $T$ con cardinalità che sarà $|T|=5$ dove $2^{5}=32$ sotto-insiemi generabili.

Ora qui le cosi si fanno quasi complicate, allora prendiamo ora l'insieme dei numeri naturali $\mathbb N$ e come abbiamo visto in precedenza, la teoria si può applicare anche a questo insieme, cioè.

>[!quote] **Teorema**
>La cardinalità dell'insieme dei numeri naturali $\mathbb N$ è (strettamente) minore della cardinalità dell'insieme dei suoi sottoinsiemi $2^{\mathbb N}$

Ora dimostriamo che questa teoria non è sempre valida per ogni valore binario tramite la $diagonalizzazione$
$$
\begin{array}{c|cccccc}

i \backslash j & 0 & 1 & 2 & 3 & 4 & \dots \\

\hline

0 & b_{00} & b_{01} & b_{02} & b_{03} & b_{04} & \dots \\

1 & b_{10} & b_{11} & b_{12} & b_{13} & b_{14} & \dots \\

2 & b_{20} & b_{21} & b_{22} & b_{23} & b_{24} & \dots \\

3 & b_{30} & b_{31} & b_{32} & b_{33} & b_{34} & \dots \\

\vdots & \vdots & \vdots & \vdots & \vdots & \vdots & \ddots

\end{array}
$$
Esempio svolto con dei numeri veri e con dei sottoinsiemi.
$$\begin{array}{c|cccccc}

i \backslash j & 0 & 1 & 2 & 3 & 4 & \dots \\

\hline

0 & 1 & 0 & 1 & 0 & 1 & \dots \quad \text{(Sottoinsieme dei pari)} \\

1 & 0 & 0 & 1 & 0 & 0 & \dots \quad \text{(Sottoinsieme \{2\})} \\

2 & 1 & 1 & 1 & 1 & 1 & \dots \quad \text{(Sottoinsieme di tutti i numeri)} \\

3 & 0 & 1 & 0 & 1 & 0 & \dots \quad \text{(Sottoinsieme dei dispari)} \\

\vdots & \vdots & \vdots & \vdots & \vdots & \vdots & \ddots

\end{array}$$
Nella dimostrazione, immaginiamo di elencare tutti i sottoinsiemi di $\mathbb{N}$ in una **tabella infinita**.

- Ogni riga della tabella rappresenta un sottoinsieme di $\mathbb{N}$.

- Ogni colonna corrisponde a un numero naturale.

- Gli elementi della tabella, $b_{ij}$, sono **0 o 1** e indicano se il numero j appartiene al sottoinsieme associato alla riga $i$.

$$
\begin{array}{c|cccccc}

i \backslash j & 0 & 1 & 2 & 3 & 4 & \dots \\

\hline

0 & \mathbf{1} & 0 & 1 & 0 & 1 & \dots \quad \text{(pari)} \\

1 & 0 & \mathbf{1} & 0 & 1 & 0 & \dots \quad \text{(dispari)} \\

2 & 0 & 0 & \mathbf{1} & 1 & 0 & \dots \quad \text{(\{2,3\})} \\

3 & 1 & 1 & 0 & \mathbf{1} & 1 & \dots \quad \text{(\{0,1,3,4\})} \\

4 & 0 & 0 & 0 & 0 & \mathbf{0} & \dots \quad \text{(\{5,6,7\})} \\

\vdots & \vdots & \vdots & \vdots & \vdots & \vdots & \ddots

\end{array}
$$
Ora andremmo a dimostrare che esiste un sottoinsieme che non è presente nell'insieme dei naturali $\mathbb N$ e che non esiste una corrispondenza biunivoca tra $\mathbb N \to 2^{\mathbb N}$.

 Prendiamo la diagonale della tabella sopra, cioè prendiamo i valori $b_{jj}$ cioè i valori nella posizione $b_{00},\ b_{11},\ b_{22}$ e così via, dove a ogni valore binario, gli facciamo il complemento, ad esempio:$${b}_{00}= 0 \qquad diventa \qquad \bar{b}_{00}=1$$ Questi valori li salviamo su una nuova sequenza di bit che chiameremmo $D$, che avrà come cardinalità $d_{j} = \bar{b}_{jj}$, esempio:

| $j$ | $b_{jj}$ (cifra diagonale) | $d_{j}$ (cifra invertita e salvata) |
|:---:|:--------------------------:|:-----------------------------------:|
|  0  |             1              |                  0                  |
|  1  |             1              |                  0                  |
|  2  |             1              |                  0                  |
|  3  |             1              |                  0                  |
|  4  |             0              |                  1                  |
| ... |            ...             |                 ...                 |
Come vediamo la sequenza che abbiamo creato tramite il complemento della diagonale esiste all'interno della tabella $D=01001$ ed è un sottoinsieme di $\mathbb N$, ma non è presente in nessuna riga della tabella (intesa come sottoinsieme) cioè non uò essere associata a nessun numero naturale $i$.

Leggere per più dettaglio del concetto della non cardinalità dei numeri naturali, pag 25-26

# 4.0 Turing Machine
---
Ora vediamo come è la struttura di una macchina di Turing in forma illustrativa.
![[touring-machine.png]]
La nostra macchina è un nastro che è suddivisa in $celle$ dove a ogni cella troviamo o un simbolo di un alfabeto $A=\{ a_{0},a_{1},\dots,a_{n} \}$ oppure il simbolo $\star$ che si chiama "bianco", che significa assenza di simbolo, questo simbolo è presente di default sia a destra che a sinistra del nastro in modo infinito.

Si presenta anche la testina che svolge il compito di scrivere i simboli all'interno del nastro oppure anche leggere cosa contiene quella cella del nastro.

L'unità di controllo interagisce con la testina in modo da poter leggere cosa contiene la singola cella in quell'istante, oppure scrivere il simbolo dell'alfabeto che abbiamo prefissato in precedenza.

Evidenziamo che la computazione avviene per passi discreti, cioè che la macchina possiede una sequenza finita di passi, che sono presenti all'interno dell'insieme che nominiamo come $Q=\{ q_{0,},q_{1},\dots,q_{m} \}$ e che ogni passo la macchina si comporterà in questo modo:
1. Controlla in che stato si trova, tra quelli elencati sopra nell'insieme.
2. La testina che punta alla cella del nastro in questo momento scrive il simbolo che gli viene ordinato, presente nell'alfabeto definito (ricordiamo che in ogni alfabeto è sempre definito il simbolo $\star$ bianco).
3. La macchina ora dopo aver scritto nella cella, si sposta a destra o a sinistra.
I passi ora descritti sono dei **programmi** che diamo in input alla nostra MdT, detto anche delle semplici operazioni;

Queste operazioni le definiamo come una quintupla $(q,a,q',a',x)$, il programma che diamo alla Mdt sarebbe questa quintupla, che la identifichiamo come.

>[!info] **Descrizione della quintupla**
>$$(q,a,q',a',x)$$
>- $q$: Identifica in che stato si trova la testina in questo momento, cioè adesso.
>- $a$: Sarebbe il simbolo che sta leggendo la testina nel momento $q$
>- $q'$: Lo stato successivo che la MdT dovrà svolgere nella seguente computazione, cioè dopo la sostituzione del simbolo da parte della testina, la macchina andrà in questo stato.
>- $a'$: Il simbolo che scriverà nello stato attuale $q$
>- $x$:  Dove vogliamo che la testina si sposti, il valore di $x$ può prendere come simboli $x=+1$ dove si sposta a destra, oppure $x=-1$ la testina si sposta a sinistra. 

Questa ora sarà il nostro punto di riferimento, perché le MdT le descriveremmo tramite queste quintuple, non con il nastro le  celle e la testina.

Per descrivere il programma che la MdT utilizzeremmo la $matrice \ di \ transizione$ oppure chiamata anche $matrice \ funzionale$.

Esempio di $matrice \ di \ transizione$
$$\def\arraystretch{1.5} \begin{array}{c|c|} & simboli& ....\\\hline q_0 & funzione di transizione&...\\\hline \vdots \end{array}$$
Abbiamo nelle colonne i simboli del nostro alfabeto che denotiamo così $A=\{ a_{0},a_{1}, \dots,\star \}$ dove decidiamo noi l'alfabeto che utilizzeremmo, le righe invece della nostra tabella sarebbe lo stato in cui si trova la macchina in quel preciso momento (come nell'esempio di prima sarebbe il nostro $q$ e il simbolo che sta leggendo sarebbe $a$).

Quindi identifichiamo la coppia $(q,a)$ la posizione e il simbolo che sta leggendo la testina in nell'istante $q$ e $a$ il simbolo che sta leggendo, l'incrocio dei due valori nella matrice possiamo trovare o l'operazione che viene ad essere eseguita, cioè la terna $(q',a',x)$, che abbiamo spiegato prima cosa fa, oppure la casella della matrice in nella posizione $(q,a)$ è vuota, il che vuol dire, non svolge nessuna operazione e termina.

Prendiamo come esempio una semplice lettura di una stringa **01**, definendo prima di tutto l'alfabeto $A=\{ 0,1,\star \}$ i suoi stati $Q=\{ q_{0},q_{1},\dots,q_{n} \}$ e lo spostamento destra o a sinistra.

|         | $0$           | $1$           | $\star$            |
| ------- | ------------- | ------------- | ------------------ |
| $q_{0}$ | $(q_{1},0,1)$ |               |                    |
| $q_{1}$ |               | $(q_{2},1,1)$ |                    |
| $q_{2}$ |               |               | $(q_{2},\star,-1)$ |
| ...     |               |               |                    |
Nello stato $q_{2}$ la macchina termina la sua esecuzione, quindi non svolge più alcuna operazione.

Ora diamo una definizione formale di macchina di Turing.
>[!quote] **Definizione**
>Una macchina di Turing denotata in questo modo **MdT** sarebbe una quadrupla $(Q,A,\delta, q_{0})$ dove:
>- $Q$ sarebbe l'insieme di stati che la macchina può possedere, non vuoto $.
>- $A$ sarebbe l'alfabeto che definiamo, compreso anche di simbolo $\star$ bianco.
>- $\delta$ è una funzione che va da $Q \times (A\cup \{ \star \})$ che sarebbe tradotto in $(q,a)$ fino a $Q \times (A\cup \{ \star \})\cup{-1,+1}$ cioè detto anche $(q,a,x)$, il nome che prende questa funzione si chiama $funzione \ di \ transizione$ e gli elementi che abbiamo citato, tutti insieme $(q,a,q',a',x)$ vengono chiamate $regole \ di \ transizione
>- $q_{0} \in Q$ sarebbe lo stato iniziale da dove comincia.

Per identificare che una MdT svolge una determinata operazione, lo facciamo descrivendola in questo modo:
$$(q,a){\to}(q',a',x)$$
La nostra MdT che abbiamo appena citato, viene definita $deterministica$ cioè che la terna $(q',a',x)$ sopra se $\exists$ è **unica nel suo genere ed è assegnata a una sola funzione di transizione** $(q,a)$.

Altro concetto importante nella MdT è quello delle $configurazione \ istantanea$, cioè un frame o fotografia dello stato attuale in cui si trova la macchina durante la sua computazione.

Questa è rappresentata tramite una quadrupla:

>[!info] **Descrizione configurazione Istantanea** 
>$$(\xi,q,a,\eta)$$
>- Il simbolo $\xi$ che si chiama **"xi"** sta a significare la stringa precedente alla lettera che stiamo leggendo, che la lettura arriva fino a quando non si incontra nel nastro l'ultimo $\star$ disponibile, in questo caso $a$ (chiamato prefisso). 
>- $q$ sarebbe lo stato in cui ci stiamo trovando nel momento della "fotografia"
>- $a$ sarebbe la lettera che stiamo leggendo nella cella del nastro, nello stato $q$
>- Il simbolo $\eta$ che si chiama **"eta"** sarebbe la stringa dopo la lettera che stiamo leggendo, fino a quando non si arriva sempre al simbolo $\star$ (chiamato suffisso).

Da notare che le stringa che è prefisso $\xi$ e suffisso $\eta$ del simbolo che viene letto $a$ avranno come alfabeto $A=\{a_{0},a_{1},\dots a_{n},\star \}$, compreso anche la star.

>[!example] **Example**
>Prendiamo come configurazione $C_{i}=(a\star c,q_{i},c,ght)$ in questa configurazione abbiamo come prefisso
>- $\xi = a\star c$
>- stato in cui ci troviamo è $q_{i}$
>- simbolo letto $a=c$
>- stringa che fa da prefisso $\eta=ght$
>
![[example-instant-configuration.jpg]]

fondamentale anche per comprendere quello che verrà spiegato dopo (non da me ma dal libro), il concetto di $passo \ di \ computazione$, che rappresenteremmo in questo modo:$$\vdash_{M}$$
Questo simbolo sta a significare che dalla $configurazione \ istantanea$, che sul libro viene chiama $C$ a quella successiva $C'$ si ha un'operazione che viene seguita di mezzo, decisa dalla MdT, che nominiamo $M$ , facciamo un esempio per capire bene:

>[!example] **Esempio**
>Prendiamo una configurazione istantanea $C=(11,q_{0},1,1\lambda)$ e la nostra MdT ci dice che l'operazione che dobbiamo eseguire è questa $(q_{0},1)\to(q_{1},1,+1)$, questa $computazione$ ci porterà allo stato successivo $C'=(111,q_{1},1,\star)$, per rappresentare che tra le due $istatanee$ si è svolta una $computazione$ di tipo $M$, sarà:
>$$C\vdash_{M}C'$$
>

Alla fine di tutte le computazioni, cioè la macchina di Turing non ha più nessuna operazione da svolgere, allora si scrive così:
$$\not\vdash_{M}$$
Con la barra che identifica la fine delle operazioni.

Alla fine diremmo che la macchina di Turing $M\downarrow w$ converge sull'input $w$ se esiste una configurazione finale $C_{i}=(\xi,q_{i},a_{i},\eta)$, in caso contrario diverge e si scrive $M\uparrow w$ cioè ci saranno configurazioni infinite.

Il resto della spiegazione di questo capitolo veditela sul libro a pagina 31-35, che stranamente è spiegato bene.

## 4.1 Function calculated by Turing Machine.
Siccome la MdT è un calcolatore, allora come tale, calcolerà delle funzioni, dove prenderà degli input, che sarebbe il dominio della funzione e restituirà gli output, cioè ad una sua immagine.

Andremmo a spiegare un concetto importante, che ci servirà dopo durante tutto il nostro percorso in questa avventura molto divertente e sarà utile per definire in maniera "formale" la computabilità.

Prendiamo un qualsiasi alfabeto $A$, che come abbiamo detto in precedenza è un insieme non vuoto di simboli, e una MdT che elabora (analizza) delle stringhe su  questo alfabeto. 

>[!quote] **Definizione**
>Sia una funzione $f$ che possiede come dominio e immagine delle stringhe presenti nell'insieme $A^{*}$ , una MdT che ricordiamo è una quadrupla $M=(Q,A,\delta,q_{0})$, calcola una funzione $f$ se e solo se $\forall w\in A^{*}$, (cioè per ogni stringa che appartiene all'insieme delle stringhe generate da un alfabeto $A$) avvengono una dei due casi:
>- $w$ appartiene al dominio della funzione $f$, allora diciamo che $M\downarrow w$ cioè $converge$ sulla stringa e ridà come output l'immagine della funzione $f(w)$.
>- caso contrario se $w$ non fa parte del dominio della funzione $f$ allora diciamo che $M\uparrow w$ diverge sull'input.
>
>In conclusione diciamo che una funzione si dice $calcolabile\ secondo\ Turing$, se esiste una MdT che riesce a calcolarla, altrimenti non è $calcolabile$.

Parte del libro poi fa un esempio di come una macchina di Turing, faccia la somma tra due naturali, esempio da vedere a pagina 36.

## 4.2 Decide if a function is calculable or not.
In questo caso il titolo non aiuta molto, ma questo capitolo parlerà se la MdT converge oppure no su un determinato linguaggio $L$ che decidiamo su un dato alfabeto $A$, cioè come la macchina identifica un linguaggio in un determinato alfabeto.

Allora abbiamo la nostra macchina $M$, che conterrà lo stesso alfabeto del linguaggio che utilizzeremmo, cioè che $M=(Q,A,\delta,q_{0})$, quindi avremmo in questione due casi in cui la macchina $M$ andrà a gestire il linguaggio $L$:

>[!info] **Decidibilità**
>Nel primo caso andremmo a dire senza contare il linguaggio utilizzato, che la macchina avrà due output possibili, "SI" e "NO", cioè che per ogni stringa $w\in A^{*}$, presa in input dalla macchina $M$, può assumere due comportamenti:
>- la macchina convergerà sul "SI" se la stringa presa in input apparterrà al linguaggio, cioè $w\in L$.
>- caso in cui la stringa presa in input non appartenga al linguaggio, convergerà sul "NO", quindi sarà $w\not\in L$.
>  
>  Allora diremmo che la nostra macchina $M \ decide \ L$.

>[!info] **Semi-decidibilità**
>Il secondo caso a differenza del primo abbiamo che la macchina non convergerà su degli output, ma sulla stringa $w\in A^{*}$ se questa stringa appartiene al linguaggio $L$, allora diremmo:
>- la macchina $M\downarrow w$ se quest'ultima appartiene al linguaggio $L$, cioè $w\in L$.
>- caso contrario la macchina $M\uparrow w$ se non appartiene al linguaggio $L$, cioè $w\not\in L$.

Nell ultimo caso che abbiamo visto, quando la macchina di Turing $M\downarrow w$ converge sulla stringa e il linguaggio $L$ si compone delle parole che vengono accettate, allora diremmo che il linguaggio $L$ viene $riconsciuto$ dalla macchina $M$

Diamo ora nel dettaglio le definizioni che abbiamo citato precedentemente.
>[!quote] **Decidibilità**
>Un linguaggio $L$ viene definito $decidibile$ se esiste una macchina di Turing $M$ che sa decidere $L$, caso contrario diremmo $indecidibile$, la funzione che viene calcolata dalla macchina, viene definita come, $funzione\ caratteristica$ e si scrive in questo modo:
>$$\chi_{L}=\begin{cases} 
 1\space \space se \space w\in L\\ 0\space \space se \space w\not\in L
\end{cases}$$

>[!quote] **Semi-decidible**
>Un linguaggio $L$, si definisce $semi-decidibile$ se esiste una macchina di Turing che $accetta$ tale linguaggio, oppure possiamo dire, $M \ accetta \ L$, la funzione che viene calcolata dalla MdT viene chiamata, $funzione\ semi-caratteristica$, ed è rappresentata in questo modo.
>$$\chi_{L}'=\begin{cases} 1\space \space se \space w\in L\\ \uparrow \space se\space w\not\in L \end{cases}$$

Questi due concetti si collegano molto al capitolo [[Foundaments of Computer Science#4.2 Decide if a function is calculable or not.|vedere se una funzione è calcolabile secondo Turing]], perché se le funzioni prima citate non sono calcolabili, allora non possiamo dire che tale linguaggio sia decidibile oppure no.

Possiamo anche dire che un linguaggio se è decidibile, sarà anche semi-dicidible, basterebbe solo sostituire l'output della $funzione \  caratteristica$ che quando la stringa appartiene al linguaggio $L$ allora risponderà $SI$ e quando non appartiene dire di $NO$, quando una macchina di Turing $M$ converge su tale stringa dichiarerà "SI" e quando diverge "NO".

Vedere esempio del libro a pagina 38 per capire meglio l'esempio.

## 4.3 Numbering the Turing's Machines with Gödel method.

In questo capitolo andiamo ad introdurre il concetto che la macchina di Turing è messa in corrispondenza biunivoca con in numeri naturali, cioè che ogni numero naturale è assegnato a una e una sola MdT, quindi possiamo utilizzare i numeri naturali sia come input che come denotazione della macchina.

Vediamo ora un esempio di enumerazione di Gödel.
![[enumeration-of-turing-machine.png]]

Diremmo che i numeri $0,1,2,3,\dots$ corrispondono a una macchina di Turing MdT$_{0}$, MdT$_{1}$, MdT$_{2}$, MdT$_{3}$, cioè l'$i-esima$ macchina di Turing $MdT_{i}$ che corrisponde al numero naturale $i$.

Diciamo anche che le funzioni dalla macchina di Turing  può essere enumerata allo stesso modo.
![[enumeration-of-the-turing-functions.png]]
Però a differenza di prima non ci sarà una corrispondenza biunivoca, perché più MdT possono calcolare la stessa funzione $\varphi$, quindi diremmo che la $i-esima$ MdT calcolerà la $i-esima$ funzione $\varphi_{i}$, diremmo che la funzione è definita su un input $w$ se la MdT $M$ converge sull'input $w$ cioè che le funzione $\varphi(w)\downarrow$, in caso contrario $\varphi(w)\uparrow$.

### 4.3.1 Decode Turing Machines
Allora definiamo una macchina di Turing $M$ e un alfabeto $A$ fissato che appartiene a tale macchina, poi l'insieme degli stati della macchina $Q$, e la sua funzione di transizione $\delta$.

Ad ognuna di loro gli assegneremmo un numero naturale, vedremmo in seguito come.

>[!quote] **Definizione**
>C'è una corrispondenza biunivoca tra i numeri naturali $\mathbb N$ e le MdT definite su un certo alfabeto $A$. 

Prima di tutto dobbiamo definire un alfabeto $A=(a_{1},a_{2},\dots,a_{m})$ con i vari simboli che sono diversi da loro $a_{1}\not=a_{2}\not=\dots\not=a_{m}$ , definiamo gli stati $Q=(q_{0},q_{1},\dots,q_{n})$ e lo spostamento della testina a destra o a sinistra $+1$ o $-1$.

Esiste tale funzione $\#_{0}$ che numererà gli stati, i simboli dell'alfabeto e lo spostamento della testina, in questo modo:
![[example-numeration.png]]
In questo modo abbiamo valori che sono $\ge 3$ maggiori uguali a 3, rendendo la funzione iniettiva.

Per le altre funzioni vedere il libro a pagina 41-49, gli argomenti trattati non sono argomento solito che mette negli esami, quindi penso che non ho bisogno di trattarlo nel dettaglio, se nel caso volete le pagine sono sopra e ve le vedete.

## 4.4 Not deterministic Turing Machines
Andremmo ora a trattare di una macchina di Turing definita come "non deterministica", che servirà in seguito per comprendere alcune dimostrazioni di teoremi importanti, ma alla fine vedremmo che equivale in definitiva alla macchina di Turing tradizionale.

Ricordiamo sempre che la macchina di Turing è una quaterna $M=(Q,A,\delta,q_{0})$, dove abbiamo l'insieme dei simboli dell'alfabeto $a\in A \cup{\{\star  \}}$, l'insieme dei suoi stati $Q$ e  la funzione di transizione $\delta$, su quest' ultima è importante denotare una cosa.

Sappiamo che la funzione ha come dominio $(q_{i},a_{i})$ e come co-domionio la terna $(q_{i}',a_{i}',x)$ dove con $x$ denotiamo la posizione in cui la testina si deve muovere, oppure esiste anche il caso in cui la funzione esclude il suo dominio dominio  $(q_{i},a_{i})$ cioè la macchina di Turing $M$ si ferma non appena incontra la coppia $(q_{i},a_{i})$.

Nel caso di una macchina di Turing non deterministica abbiamo che la nostra coppia $(q,a)$ potrà scegliere più terne $(q',a',x)$ e non solamente una.

In questo modo rendiamo la nostra funzione $\delta$ da una relazione che andava dall'insieme $Q\times (A\cup\{\star  \})$ (cioè il nostro $(q,a)$) alla terna $Q\times(A\cup\{\star  \}\times \{ -1,+1 \}$  (cioè la terna $(q',a',x)$)si comporrà dell unione di questi due insiemi, formando una 5-utpla.
$$Q\times (A\cup\{\star  \})\times Q\times(A\cup\{\star  \}\times \{ -1,+1 \}$$
Diamo una definizione formale di MdT non deterministica.

>[!quote] **Definizione**
>Una macchina di Turing "non deterministica" è una quadrupla $M=(Q,A,\delta,q_{0})$ (come nella definizione di macchina di Turing classica), solo che la sua $funzione\ di\ transizione$ cambia in così.
>$$Q\times (A\cup\{\star  \})\times Q\times(A\cup\{\star  \}\times \{ -1,+1 \}$$

# Reference
---
[^1]: **palindromo**: viene definito palindromo quelle parole, numeri o sequence di lettere che possono essere lette da entrambi i versi, sia da sinistra a destra, che da destra fino a sinistra ad esempio: 3663, radar, 12321, ecc..