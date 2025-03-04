2025-03-04 16:26

Status: #baby 

Tags: [[Programming]], [[General Knowledge]]

Other notes: *[click here](https://francescopalozzi.notion.site/Appunti-39bc6581d2c9426280d354c261187919)*

Formulario: *[click here](https://francescopalozzi.notion.site/Formulario-Fondamenti-efd19dff3ff94e488d24661e0fd325d7)*

---
> [!warning] **N.B**
> In questi appunti ci sono solo le parti che ritengo necessarie per la comprensione dei concetti, ci saranno immagini e formule, ma per altri chiarimenti, leggere il libro nel capitolo/parte che viene citata nelle *footnotes*
# Index
---
%% TODO: creare la tabella dei contenuti %%

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

Per rappresentare la *stringa vuota* si usa il lambda $\lambda$.

> [!important] **Usato spesso** 
> 
> $$\lambda \implies striga vuota$$

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

Esiste un'altro modo per rappresentare la concatenazione, come ad esempio, la concatenazione di più simboli dello stesso tipo.

Si viene a rappresentare una stringa su un alfabeto qualsiasi, viene allora definito. $\alpha^{i}$ dove abbiamo che $i\in \mathbb N$, illustriamo qualche esempio di questa concatenazione.
$$ab^{2}c^{3} = abbccc$$
$$a^{4}d^{5}e^{2} = aaaadddddcc$$
$$(ab)^3=ababab$$
Descriviamo anche il concetto di *sottostringa* introducendolo in questo modo:
> [!quote] **Definizione**
> Diciamo che una data stringa $\alpha$ è una sotto stringa di $\beta$ se $\beta=\gamma\alpha\rho$ dove $\gamma$ e $\rho$ sono delle stringhe 

Facciamo un'esempio di *sottostringa* per capire bene il concetto:
$$\beta=fdad \qquad sono \ sottostringhe:\ \lambda,f,fd,fda,dad,ad,fdad$$
Si viene poi ad evidenziare il concetto di *suffisso* e *prefisso* proprio e non, prendiamo lo stesso esempio di prima:
$$\beta = fdad \qquad suffisso:\ \lambda,d,ad,dad \qquad prefisso: \lambda ,f,fd,fda$$
Sono considerati suffissi e prefissi propri se $\gamma \neq\lambda \ or \ \rho\neq\lambda$ , nell'esempio prima sono tutti e due suffissi e prefissi propri perché o prima o dopo dei simboli ci sono altri simboli e non sono vuoti ($ad$ prima avrà $fd$ quindi è un suffisso proprio).
# Reference
---
 

