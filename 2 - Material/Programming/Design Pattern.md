---
share_link: https://share.note.sx/mlyeikio#KL/1j2iPkchuJXQszkeNjtdKFazHDjXiTEm6FafDpTw
share_updated: 2024-11-20T11:58:39+00:00
---
2024-10-07 11:20

Status: #devoleped

Tags: [[Programming]] [[Software Engineering]]

---
# Design Pattern

## 0.0 Index
---
- [0.0 Index](#0.0%20Index)
- [1.0 Introduction of OOP](#1.0%20Introduction%20of%20OOP)
- [2.0 Class hierarchies](#2.0%20Class%20hierarchies)
- [3.0 OOP pillars](#3.0%20OOP%20pillars)
- [4.0 Relation between objects](#4.0%20Relation%20between%20objects)
- [5.0 SOLID principals](#5.0%20SOLID%20principals)
- [6.0 Design Pattern](#6.0%20Design%20Pattern)
- [6.3 Category of Design pattern](#6.3%20Category%20of%20Design%20pattern)
- [6.4 Creational pattern](#6.4%20Creational%20pattern)
- [7.0 Structural Design Patterns](#7.0%20Structural%20Design%20Patterns)
- [8.0 Behavioral Design Patterns](#8.0%20Behavioral%20Design%20Patterns)

## 1.0 Introduction of OOP
---
La **O**bject - **O**riented - **P**rogramming è un paradigma di programmazione che consiste nel raccogliere pezzi di informazione o dati e far in modo di creare dei gruppi, chiamati *objects* (oggetti in italiano), questi sono definiti in un'insieme di *blueprints*(regole in italiano) che sono create dal programmatore, queste son chiamate **classi**.
![[RapprenstazioneDellaClasse.png|]]
Questo sopra illustrato è un esempio di classe, con nome *Cat*,troviamo qui sull'immagine una spiegazione della classe in notazione _UML_, che verrà utilizzata molto spesso in seguito in questo documento.

Nel libro viene fatto un'esempio che spiega la differenza tra classe ed istanza, questo tramite l'utilizzo di due gatti _Oscar_ e _Luna_ che saranno le **istanze** della classe Gatto, hanno gli stessi **stati** (Fields nel libro) e **comportamenti** o detti anche **metodi** della classe (Methods nel libro), insieme questi due sono detti _membri_ della loro classe.

> [!tip]
> Quello che viene salvato all'interno di un campo di una classe o di un'istanza di essa viene chiamato ***state*** (stato in italiano), invece tutti i metodi definiti in una classe sono chiamati ***behavior*** (comportamenti in italiano).
## 2.0 Class hierarchies
---
Prendiamo d'esempio che il nostro vicino abbia un cane che è  un genere di animale come il gatto, possiede quasi gli stessi comportamenti di quest'ultimo.
Si conosce il suo nome, razza, età e colore, proprietà che sono comuni anche nel gatto, quindi cosa si fa? 
Due classi diverse con gli stessi metodi e attributi, ma aggiungendo solo un singolo comportamento diverso?

La cosa migliore da fare senza rendere il codice *complesso* e *ripetuto* sarebbe quella di creare una **[[Programming Knowledge#Abstract class|classe astratta]]**, ==questo perché si hanno metodi e stati in comune tra i due animali che potranno essere condivisi tra le due classi o detti anche==  [[#3.3 Inheritance (ereditarietà)|ereditati]] da come vedremmo dopo dalla classe `Animal` .

>[!info]
>`Animal`  nel libro sarà in grassetto ma per rappresentare una classe astratta si fa con il font in *italics*

### 2.1 Superclass & Subclasses
In questo caso abbiamo come classi `Cat` e `Dog`, questi avendo come detto precedentemente molti attributi e metodi in comune, creeremmo una classe in comune `Animal` che generalizzerà i comportamenti e gli stati che possono avere un gruppo di animali, il nome che gli daremmo sarà ***superclass***, i figli che erediteranno le istanze e gli attributi della classe superiore, verranno chiamati ***subclasses***.

![[ExampleOfClassHierarchy.png]]

Nel caso più professionale possiamo dire che la classe `Animal` sia una sottoclasse di una superclasse più generale come `Organism` che racchiude anche il genere di organismi diversi da quelli animali, compresi anche quelli vegetali `Plants`.

![[ClassHierarcyOfOrganism.png]]

La sottoclasse `Cat` e `Dog` sono quelle che possono, ampliare e modificare completamente, il comportamento della classe genitore quanto vogliono (rispettando sempre i loro ruoli).

## 3.0 OOP pillars
---
In the context of **_OOP_** there are 4 mains pillars: 
- [[#3.1 Abstraction|Abstraction]]
- [[#3.2 Encapsulation  |Encapsulation]]
- [[#3.3 Inheritance (ereditarietà)|Inheritance(ereditarietà)]]
- [[#3.4 Polymorphism |Polymorphism]]
### 3.1 Abstraction
Significa che ogni qualvolta si va a rappresentare un'oggetto del mondo reale in un programma, difficilmente (molto spesso non richiesto), si riesce a descrivere tutte le caratteristiche nel dettaglio di tale oggetto al suo interno.
Noi ==creiamo dei modelli che ne rappresentano==, tramite i loro attributi ed i loro comportamenti, ignorando quello che non è necessario.
![[AbstractionExample.png]]

>[!faq]
**_Abstraction:_** è un modello del mondo reale o di un fenomeno, che  rappresentiamo in un contesto limitato, con una descrizione molto accurata ed ignorando il resto.
### 3.2 Encapsulation
Prima di parlare dell'incapsulamento, dobbiamo capire il concetto che si nasconde dietro.
Quando si deve utilizzare la macchina non si va a controllare lo stato della batteria o dei cavi e neanche far funzionare il motore manualmente per farla partire, si mette la chiave nella fessura e la si accende senza troppi pensieri.

Ecco questo è cosa fanno principalmente, le nostre _interfacce_ all'interno dei nostri oggetti, vanno a nascondere i dettagli di quest'ultimi, mostrando solo quello che gli oggetti di altre classi possono interagire.

Quando parliamo di incapsulamento ci sono due modi di dire.

--- start-multi-column: ID_6rdl
```column-settings
Number of Columns: 2
Largest Column: standard
```

### Encapsulate
---
L'abilità di un oggetto di mostrare comportamenti e stati solo a determinati oggetti da lui scelti, esponendo solo interfacce limitate al resto del programma.

--- column-break ---
### To encapsulate
---
Far in modo che i metodi di una classe siano `private`, rendendoli accessibili solo a questi ultimi.
Fatta eccezione per attributi o metodi che sono `protected`, cioè che sono utilizzabili dalle proprie sottoclassi.

--- end-multi-column

Le ==interfacce== e ==classi astratte== sono quelle più utilizzate per la programmazione basta sull'astrazione e l'incapsulamento e ne seguono perfettamente le direttive. Con la keyword `interface` o `protocol` vai a creare un _contratto_ tra oggetti. Non troverai mai dentro ad un interfaccia degli attributi, ma solo metodi (behaviours in english).

Ora vediamo un'esempio di come si comporta un'interfaccia  in questo caso particola.

![[IncapsulationExample.png]]

Qui si vede che la classe `Airport` dipenda dall'interfaccia `FlyingTransport` che prenderà a sua volta il metodo di tale interfaccia `fly(origin, deestination, passenger)`, tale metodo dichiarato nell'interfaccia ed implementato nelle classi `Helicopter`, `Airplane`, `Domesticated Gryphon`  può variare quello presente al suo interno, ma mantenendo sempre la [[Programming Knowledge#Method signature |firma del metodo]]
### 3.3 Inheritance (ereditarietà)
Con ereditarietà si intende come, l'abilità di una classe di poter estendere se stessa, in modo di poter evitare di creare codice duplicato, riutilizzando metodi e i suoi attributi (solo se sono protected).

Con l'ereditarietà la sottoclasse  dovrà riutilizzare anche le implementazioni della classe superiore, come tutti i metodi astratti e le stesse interfacce che usa, anche se non hanno senso.

> [!caution]
> **_Importante:_** una sottoclasse può essere estesa solo da una ed un sola super classe.

### 3.4 Polymorphism
Se avessimo uno zaino pieno di gatti e cani, quando peschiamo ad occhi chiusi, non sappiamo cosa andremmo  a pescare, ma possiamo capirlo dal verso che fa, con la sua concreta classe che svolge quest'azione.

Vediamo questo codice d'esempio cosa fa.
``` java
bag = [new Cat(), new Dog()];

foreach (Animal a : bag)

a.makeSound()

// Meow!

// Woof!
```

Per ogni elemento dell'array bag eseguirà prima il metodo presente nella classe `Cat` e poi quello di `Dog`, ma il programma non sa cosa sia presente nella variabile `a` , grazie però al meccanismo del _Polymorphism_ il programma può tracciare il metodo della sottoclasse nella quale possiamo trovare le corrispettive azioni che svolgeranno.

>[!help]
>Il _Polimorfismo_ è quell'abilità di un programma di trovare l'oggetto di una classe ed utilizzare la sua implementazione, anche se non si conosce il tipo nel contesto utilizzato.

## 4.0 Relation between objects
---
Ci sono principalmente 4 tipi di relazioni tra oggetti:
- [[#4.1 Association|Association]]
- [[#4.2 Dipendence|Dipendece]]
- [[#4.3 Composition|Composition]]
- [[#4.4 Aggregation|Aggregation]]
### 4.1 Association
![[AssociationExample.png]]
L'_associazione_ ==consiste nel figurare che un oggetto usa o interagisce con un'altro==, la freccia può essere unidirezionale o bidirezionale. Viene usato per rappresentare una campo che è presente in una classe.

### 4.2 Dipendence
![[DipendenzaRappresentazione.png]]
La _dipendenza_ è una variante di associazione, la sua caratteristica è quella di non essere forte e robusta come quest'ultima, cioè che vuole dire? Questo sta a significare che ==due oggetti si dipendono quando non c'è una connessione permanente tra loro==.
 Quando c’è una dipendenza, significa che se cambiamo qualcosa nella prima classe (come la sua struttura, i metodi o le proprietà), potrebbe essere necessario cambiare anche l’altra classe, perché altrimenti smetterebbe di funzionare correttamente.
### 4.3 Composition
![[ComposizioneExample.png]]
La _composizione_ significa che un oggetto avrà il ruolo di contenitore (whole in inglese) che sarà un insieme composto da una o più istanze un altro oggetto (chiamato componente part in inglese), questo vuol dire che ==il componente non può esistere da solo senza il suo contenitore.==
In UML il nostro _contenitore_ sarà quello che avrà il diamante pieno, il _componente_ invece sarà dove punta la freccia.
### 4.4 Aggregation
![[AggregationRelation.png]]
L'_aggregazione_ è una variante più leggera della composizione, questo vuol dire che il contenitore non controlla pienamente il ciclo di vita del suo componente, ==in sostanza il componente può esistere anche senza la necessità di un suo contenitore, collegandosi anche a più contenitori alla volta!==
## 5.0 SOLID principals
---
I principi solidi sono stati creati per rendere il software più flessibile, mantenibile nel tempo ed estendibile, ne sono ben 5 e si distinguono dal loro acronimo.
Li puoi trovare qui sulle note [[SOLID Principals]], oppure se vuoi in dettaglio eccoli qui ognuno di loro:
- [[SOLID Principals#S - ingle responsibility|Singola responsabilità]]
- [[SOLID Principals#O - pen/ closed|Open Close]]
- [[SOLID Principals#I - nterface Segregation|Separazione interfacce]]
- [[SOLID Principals#L - iskov Substitution|Sostituzione di Liskov]]
- [[SOLID Principals#D - ependecy inversion|Inversione di dipendenza]]
## 6.0 Design Pattern
--- 
Il **design pattern** così chiamato, sono delle ==strutture ideate per risolvere dei problemi che si presentano==, sono aperti ed estendibili, nel senso che possono essere utilizzate per risolvere più problemi e si possono migliorare nel tempo, adattandoli ai problemi che riscontriamo, si possono incrociare multipli design patterns se si vuole.

### 6.1 What Problem we are talking about?
---
#### 6.1.1 Generic Problems
Ci possono essere problemi legati alla gerarchia delle classi, questo cosa vuol dire?
Date tot classi che risolvono un problema software, andremmo a creare la soluzione più adatta, per gestire la loro gerarchia.
La soluzione a tale problema è l'utilizzo delle _interfacce_ queste se sono stabili e ben progettate, si potrà gestire bene la comunicazione con gli oggetti di una determinata classe.

Se tali interfacce sono gestite correttamente si risolverà il problema, che si può riscontrare solitamente se non si crea un buon progetto, cioè **minimizzare le dipendenze**, cosa vuol dire?
Far in modo che gli oggetti di una classe non richiamino se stessi, ma che questo compito venga gestito dall' interfaccia stessa.

Se tali soluzioni vengono applicate per ogni problema, si produrrà del **codice estendibile nel tempo**.
#### 6.1.2 Specific problems

Uno dei problemi che un design pattern può risolvere, sarebbe quello della **navigazione di una struttura dati complessa**. 

Oppure come posso **separare la gestione delle interfaccia da quella dell'implementazione di una classe**?

Come **implementare lo stesso codice/algoritmo su più classi, senza doverlo duplicare più volte**?

I design pattern complicano il codice nel tempo, ma questo però a fin di bene perché avremmo in cambio **estendibilità** e la **compatezza** del codice nel tempo.
### 6.2 Structure of Design Pattern
---
![[ExampleDesignPatternState.png | center]]
Questo è un esempio di Design pattern chiamato **State**, ogni design pattern è composto da diversi elementi da considerare:

- **Nome del pattern**: questo per conoscere che problema andremmo a risolvere, le sue soluzioni e cosa comporta usare un determinato design pattern invece che un altro.

- **Problema**: conosceremmo il problema per la quale si va ad applicare lo specifico design pattern scelto.

- **Soluzioni**: comporta descrivere ogni elemento del design pattern le sue relazioni, responsabilità e le collaborazioni.
 
- **Conseguenze**: molti design pattern devono seguire i [[#3. Solid principals |principi solidi]], altri invece hanno come conseguenza quelli di violarli, ma non risultano essere dei problemi se porterà alla buon riuscita del code.

Sono soluzioni che sono state adottate nel campo, quindi meglio sempre **prendere qualcosa di già fatto**.

>[!quote]
>_"Don't reinvent the wheel"_ 

Conoscere un problema in anticipo vuol dire, saper battere la concorrenza, ecco perché molti dei design pattern sono generici, per far sì che si possano applicare a soluzioni già esistenti, senza ulteriore perdita di tempo.

Far in modo che sia **comprensibile e chiaro** il codice o progetto è lavoro del design pattern, nel caso mettessimo mano ad un progetto dopo mesi che non ci lavoriamo, si possono riscontrare problematiche di comprensione e lettura, se quest'ultimo non è ben descritto.
Come un "**vocabolario**" il design pattern oltre ad essere comprensibile a noi, deve esserlo per gli altri progettisti software in gioco nel nostro progetto.

Ultimo ma non meno importante, **il design pattern permette di rendere il codice ed  il progetto più snello e comprensibile**

> [!help]
> **Refactoring**: stravolgere il progetto e il codice nel caso non si possa fare niente per risolvere un determinato problema già in uno stato avanzato.

Questo lo si può fare tramite sempre l'utilizzo di design pattern ben studiati solo per il refactoring (_for see more [refactoring.guru](https://refactoring.guru/refactoring)_).

## 6.3 Category of Design pattern
---
In base al loro _ruolo_ si vengono a differenziare i suoi vari tipi.
--- start-multi-column: ID_fy5j
```column-settings
Number of Columns: 3
Largest Column: standard
```
### Creational
--- 
Offrono servizi per la __creazione e gestione__ di oggetti.

--- column-break ---
### Structural
--- 

Creano delle separazioni tra interfacce e implementazioni, utili per **modelli complessi**.

--- column-break ---
### Behavioral
--- 
Modificare il comportamento degli oggetti **senza dover modificare grandi porzioni di codice**.

--- end-multi-column
In base al loro _dominio_ (scope in inglese) ci sono due tipologie di design pattern.
--- start-multi-column: ID_x0lr
```column-settings
Number of Columns: 2
Largest Column: standard
```

### Class pattern
---
- Sono quelli focalizzati sulla **relazione tra classe e sottoclasse**
- Presenti solitamente in casi di relazioni statiche come ad esempio quelle **espresse tramite l'ereditarietà**

--- column-break ---

### Object pattern
---
- Si focalizzano sugli oggetti cioè le **istanze delle classi** e le loro corrispettive relazioni.
- Presenti nel caso di **situazioni dinamiche** gli oggetti possono cambiare il loro stato durante l'esecuzione e si viene ad usare la [[#4.3 Composition|composizione]]

--- end-multi-column
## 6.4 Creational pattern
---
Sono quei ==pattern che permettono di astrarre la generazione di istanze di una classe==, in modo da far si che si creano sistemi indipendenti da come i suoi oggetti sono composti, creati e rappresentati.
Gli oggetti vengono creati da delle specifiche _strutture_. 

### 6.4.1 Factory pattern
Questo pattern ci permette di creare nuovi oggetti per estendere l'utilizzo della nostra ==applicazione utilizzando questo meccanismo di creazione di  oggetti che siano simili tra loro== (cioè che implementano la stessa interfaccia), senza dover specificare le loro classi  concrete.

Questo pattern creare dei _veri e propri prodotti_ e permette anche di far in modo che le sottoclassi possano modificare gli oggetti restituiti dal factory method, non solo si riesce anche a cambiare completamente la logica della creazione senza dover metter mano sul codice intero.
![[FactoryMethod.png]]
>[!done] Vantaggi 
>- Il client non dipende dalla classe concreta del prodotto, ma dalla sua interfaccia permettendone la sua estendibilità
>- Gli oggetti sono trattati come astratti.  
#### 6.4.1.1 Factory method structure
>[!info] Consiglio esame
>All'esame chiederà la sua struttura e la sua descrizione.

![[StrutturaFactoryMethod.png]]
La struttura del _design pattern factory_ è composto da questi 4 metodi:

1. ***Product***: interfaccia comune utilizzata da tutti gli oggetti che verranno creati dalla classe ***Creator*** e dalle sue corrispettive sottoclassi.
   
2. ***Concrete Products***: sono le implementazioni dell'interfaccia sopra citata ***Product***.
   
3. ***Creator:*** è ==colui che crea gli oggetti== tramite la dichiarazione, del metodo factory `createProduct()` che creerà oggetti  di tipo `<<interface>> Product` che possono essere o il `ProductA` o `ProductB`.
^e3e396
4. ***Concrete Creator***: son metodi che sovrascrivono il **Creator** che restituiranno uno specifico prodotto.
   
> [!tip] Ricorda
> Tutti i prodotti sono basati sull'interfaccia, che sarà il tipo di ritorno del metodo factory che abbiamo citato prima cioè ***Creator***

#### 6.4.1.2 When we use it?
Si possono utilizzare i factory method in 3 casi specifici:

1. ***Unknown types***: quando non conosciamo i tipi di metodi che andremmo a generare, separandoci dalla creazione di ogni suo oggetto dal suo utilizzo, _così facendo si può estendere il codice_.
   
2. ***Extends Library or Framework***: estendere librerie o framework, come ad esempio [[Programming Knowledge#Overriding (sovrascritto)|sovrascritto]] un metodo di una classe per fargli fare diverse funzionalità.
   
3. ***Optimize resources***: riutilizzare risorse esistenti invece di crearne nuove.

#### 6.4.1.3 How we implement it?
Per implementare tale design pattern bisogna prima di tutto:

- ==Implementare un'interfaccia che dichiarerà dei metodi comuni che questi verranno ad essere utilizzati== da ogni prodotto. 
  
- Poi si andrà a creare un metodo _factory_ vuoto dentro alla classe astratta [[#^e3e396|Creator]], da tener d'occhio che il tipo di ritorno di tale metodo sia lo stesso dell'interfaccia prodotto.
  
- Sostituire i costruttori con il metodo _factory_ che abbiamo creato in precedenza (nel caso creare un parametro che controlli il tipo di ritorno del metodo).
  
- Creare le sottoclassi di [[#^e3e396|Creator]] per ogni prodotto che si va a creare e infine [[Programming Knowledge#Overriding (sovrascritto)|sovrascrivere]] ogni metodo della sottoclasse.
  
- Rendere astratto il metodo factory nel caso sia vuoto dopo le varie estrazioni.
#### 6.4.1.4 Pros and Cons

> [!done] ## Pros
> - **Disaccoppiamento**: crea una distanza e isola il _[[#^e3e396|creator]]_ con i suoi "figli" o detti anche sottoclassi.
> - **Single responsibility**: rispetta il principio di [[SOLID Principals#S - ingle responsibility|singola responsabilità]] dei SOLID.
> - **Open Closed**: ci permette di creare nuovi prodotti(quindi estendere il codice), senza però modificare il codice esistente. 

>[!fail] ## Cons
>- **More complexity:** può introdurre più complessità, nel caso si andrebbe ad aggiungere sempre nuove sottoclassi per ogni prodotto.
>- **Optimal scene:** funziona meglio quando viene introdotto in una gerarchia di classi _[[#^e3e396|creator]]_ già presente.

### 6.4.2 Abstract  Pattern
Permette di raggruppare famiglie di oggetti, lo scopo è lo stesso  del factory cioè creare degli oggetti solo che si va anche a creare delle famiglie di oggetti specifici.
[^1]: ![[AbstractFactory.png]]
Come vediamo qui sull'immagine abbiamo diverse famiglie di diversi oggetti, gli oggetti sono la `Chair`, `Sofa`, `Coffe Table` sono poi categorizzati in diverse famiglie, l'abstract ci permette di far si che si viene ad inserire un nuovo mobile, si potrà applicare le stesse famiglie di quelle precedenti. ^f2083e

>[!tip] Scope
>Lo scopo dell'abstract factory è quello di creare un'interfaccia che va a creare delle famiglie di oggetti che sono correlati o dipendenti, senza conoscerne la sua classe concreta.
#### 6.4.2.1 Abstract Factory Solution
1. **Phase:**
	   Per applicare tale design pattern, bisogna prima di tutto creare le interfacce per ogni famiglia di oggetti che vogliamo creare ad esempio (sedia, sofa, tavolo) e per ognuna di loro un'interfaccia che corrisponda alla tipologia/variante dell oggetto (sediaVittoriana, sediaModerna ecc..).
	   
2. **Phase:**
	   Si va a creare l'**Abstract Factory** che dovrà implementare dei metodi la creazione della famiglia di oggetti come createChair(); createTable(); e così via che _ritorneranno prodotti astratti_ che abbiamo definito nell'interfaccia. 
3. **Phase:**
	   Si va a creare la **factory concreta** per ogni variante cioè che vuol dire, la parte nella quale si crea ogni classe che genererà una specifica tipologia di stile di  forniture ad esempio _ModernFornitureFactory_  creerà solo `ModernChair`, `ModernSofa` e `ModernCoffeTable`

![[AbstractFactoryConcept.png]] ^fd1c79
#### 6.4.2.2 Abstract Factory Structure
![[AbstractFactoryStructure.png]]

1. **Abstract Products:** creeremmo interfacce distinte, ma correlati per ogni famiglia di prodotti come (Chair, Sofa, ecc...).
 ^d05c69
2. **Concrete Products:** implementazione specifica di ogni stile di ***abstract products*** organizzate per tipo come (es. ModernChair, VictorianSofa ecc...)

3. **Abstract Factory**: si può dichiarare come classe astratta o interfaccia, il factory ha la funzione di dichiarare i metodi di creazione di ciascun abstract product(es. _createChair()_, _createSofa()_ ecc) ==avrà come tipo di ritorno l'interfaccia dei prodotti==.
 ^1163b7
4. **Concrete Factory**: implementerà le dichiarazioni dell'interfaccia **Abstract Factory**, ==queste creerà solo una specifica variante del prodotto==(cioè non può creare un ModernForniture se il suo compito è quello di generare VittorianForniture).

5. **Client**: lavorerà con le factory e i prodotti in modo indiretto tramite interfacce astratte  senza dover essere legato ad una specifica variante/stile, utilizzando qualsiasi factory/prodotto a sua scelta.
#### 6.4.2.3 When we use it?
Quando si lavora con **famiglie di prodotte correlate** senza che essi dipendano da classi concrete, creando interfacce che fornisce oggetti per ogni famiglia di prodotti / stili di prodotti, facendo si che non si creano confusioni tra le famiglie create o mismatch.
#### 6.4.2.3 How we implement it?
Si deve prima di tutto mappare i prodotti in una matrice come nella [[#^f2083e|figura]], si dichiarano poi le interfacce astratte per ogni tipo di prodotto, far implementare queste interfacce da delle classi concrete che ne utilizzeranno i loro componenti.
Creare l'**Abstract Factory** che gestisce la creazione degli oggetti definendo i metodi per la creazione di ogni prodotto, poi implementare questi metodi nelle classi **Factory Concrete**, cioè quelle che faranno il lavoro di creazione delle varianti di prodotto (`ArtDeco`, `Victorian` ecc..).
Infine sostituire le chiamate dirette ai costruttori di prodotti, con chiamate hai metodi di creazione della factory, cioè il client non andrà mai ad implementare oggetti direttamente dai product ma dalla [[#^1163b7|abstract factory]].
#### 6.4.2.4 Pros and Cons

> [!done] ## Pros
> - **Compatibility garanted**: cioè vuol dire che i prodotti creati da una factory sono sempre compatibili tra loro implementando interfacce simili.
> - **Low dipendece**: cioè il codice del client non ha una relazione stretta legata ai prodotti concreti.
> - **Single responsibility**: rispetta il principio di [[SOLID Principals#S - ingle responsibility|singola responsabilità]] perché il codice di creazione dei prodotti è centralizzato ad una sola interfaccia che gestisce tale creazione.
> - **Open/Closed**: principio rispettato perché si possono aggiungere varianti di prodotti senza modificare il codice esistente.

>[!fail] ## Cons
>- **More complexity:** può introdurre più complessità, nel caso si andrebbe ad aggiungere sempre nuove classi ed interfaccie per ogni prodotto.

### 6.4.3 Builder  Pattern
Ci permette di creare oggetti complessi step-by-step , cioè questi ultimi  richiedono inizializzazioni dettagliate che spesso sono nidificati nei costruttori, cioè ==si possono rappresentare differenti rappresentazioni di un oggetto usando lo stesso costrutto==. Un esempio che possiamo illustrare è quello della casa che può essere una semplice abitazione oppure una più complessa, compresa di giardino, sistema di riscaldamento ed impianto idraulico.
![[ExampleOfBuilderProblem.png]]
Questo lo si fa con un costruttore, che però quando alcuni parametri non servono, rimangono `null` ed inutilizzati.
>[!tip] Scope
>Separare la costruzione di un oggetto complesso, dalla sua rappresentazione, questo da far in modo di creare dallo stesso processo di costruzione, estrapolarne differenti modelli di rappresentazione e non uno singolo.
#### 6.4.3.1 Builder Solution
1. **Separate builder code**:
   La costruzione degli oggetti vengono delegate a delle classi separate chiamatesi  **builder** si possono avere più builder che fanno cose differenti.
   
2. **Building step-by-step**:
   Si eseguono dei passi ben precisi per la creazione degli oggetti (`buildDoor`, `buildWall` ecc...) così possiamo costruire solo ciò che ci serve in quel momento.

3. **Flexibility and Reusability**:
   Builder differenti possono implementare gli stessi passaggi in modo differenti(es. muro in pietra, legno, oro).

4. **(Optional) Director**:
   Questa classe ha il ruolo di dettare l'ordine dei passi alle classi builder per la fase della costruzione, nasconde i dettagli di ogni passaggio al client ed inoltre permette il riutilizzo del codice.
   ![[BuilderExample.png]]
#### 6.4.3.2 Builder Structure
![[BuilderStructure.png]]
Partiamo come sempre dalle interfacce:

1. **Builder:**
   Creazione dell'interfaccia builder, che dichiara i passi comuni a tutti e da far eseguire, per la costruzione del prodotto.

2. **Concrete Builder**:
   Le nostre classi concrete che identificano le tipologie di builder, cioè che fanno? Forniscono le implementazioni dei passi che vengono richiesti dall'interfaccia **Builder**.

3. **Product**:
   Le classi che abbiamo definito andranno a creare dei prodotti che ==possono non appartenere alla stessa gerarchia o interfaccia==, ricordare bene!!, non c'è nessuna correlazione tra l'interfaccia Builder e il prodotto che andremmo a creare.

4. **Director:**
   Class che ci permette di definire l'ordine dei passi, per la costruzione, che come detto in precedenza ci permette di creare configurazioni riutilizzabili.

5. **Client**: 
   Il client ha il compito di associare ad un **Builder** uno specifico **Director**, questo tramite il costruttore del director o passandolo al metodo di produzione.
   
Qui si possiede una logica molto differente perché si andrà prima a fare un setting di ogni variabile, poi dopo si va  a creare l'oggetto.
#### 6.4.3.3 Builder  when we use it?
Usato per **evitare la creazione di costruttori con troppi parametri opzionali e complessi** e ci fa in modo di creare l'oggetto, passo dopo passo, **utile anche per la creazione di oggetti che hanno la stessa rappresentazione**(es. casa in legno o pietra) utilizzando lo stesso set di passi di costruzione.
Infine viene per la creazione di oggetti assai complessi, garantendo la completezza del prodotto.

#### 6.4.3.4 Pros and Cons
> [!done] ## Pros
> - **Flexible building**: ci permette di creare oggetti passo dopo passo, ritardare i passaggi o eseguirli in modo ricorsivo.
> - **Reusable code**: ci permette di poter creare un codice riutilizzabile nel tempo, per rappresentare diversi tipi di prodotto.
> - **Single responsibility**: rispetta il principio di [[SOLID Principals#S - ingle responsibility|singola responsabilità]] perché il codice di creazione dei prodotti è centralizzato ad una sola interfaccia che gestisce tale creazione.

>[!fail] ## Cons
>- **More complexity:** può introdurre più complessità, nel caso si andrebbe ad aggiungere sempre nuove classi ed interfaccie per ogni prodotto.

### 6.4.4 Prototype pattern
Il design pattern in questione, serve a far si che si possa creare un'esatta copia di un oggetto che già esiste, se volessimo farlo senza l'utilizzo del design pattern, si dovrebbe creare lo stesso oggetto nella stessa classe e copiargli i valori interni, cosa non sempre possibile su tutti i campi dato che ==alcuni possono essere privati o non visibili==, oppure ci sono ==oggetti che sono dipendenti dalla classe e non possono essere modificati==. 

#### 6.4.4.1 Prototype Solution
La soluzione al problema che si pone nel copiare l'oggetto di una determinata classe ,==consiste nel permettere all'oggetto stesso di svolgere la clonazione da solo, tramite l'utilizzo comune di un'interfaccia che viene data solo agli oggetti che vogliono svolgere tale processo==, permettendo all'oggetto di non essere legato alla classe stessa. 

L'interfaccia che verrà creata conterrà solo un metodo `clone()`, che avrà il compito di creare una copia precisa dell'oggetto che si vuole creare, portandosi i campi interni dell'oggetto copiato.

#### 6.4.4.2 Prototype Structure
![[PrototypeStructure.png]]
Vediamo nel dettaglio la struttura del prototype:

1. `«interface»` ***Prototype***: si crea l'interfaccia dove si andrà a creare il metodo che svolgerà la clonazione.

2. ***ConcretePrototype***: sarà quella classe che implementerà la clonazione degli oggetti, copiandone i dati originali, impostando anche le varie casistiche di oggetti che possiedono ricorsioni.

3. ***Client***: colui che andrà ad eseguire la clonazione dei vari oggetti, seguendo l'interfaccia prototype.
#### 6.4.4.3 Prototype registry Implementation
![[PrototypeRegisty.png]]
1. ***Registro di Prototipi***: Fornisce un modo facile per accedere ai prototipi più utilizzati, memorizzando un insieme di oggetti predefiniti pronti per essere copiati. La versione più semplice è una mappa nome → prototipo.
#### 6.4.4.4 Prototype Example
![[PrototypeExample.png]]
In questo esempio andremmo a vedere come funziona la [[Programming Knowledge#Abstract class|classe astratta]] `Shape` e le figure che ruolo hanno:

- Le classi che estendono la classe astratta, avranno il metodo clone per clonare gli oggetti.
- La sottoclasse può richiamare il metodo della classe che clona del genitore prima di dover copiare i campi nel metodo risultante, cioè quello che viene in output.
#### 6.4.4.5 Prototype  when we use it?
Usare il pattern prototype **quando vogliamo che il nostro codice  non debba dipendere dalla classe concreta  e dagli oggetti che vogliamo copiare**, facendo si che ci sia un'interfaccia che renda possibile utilizzare il codice del client senza dipendere dalla classe concreta.

Oppure possiamo utilizzarlo quando vogliamo che non si creano troppe sottoclassi che si differenziano solo nel modo in cui inizializzano i loro oggetti.

#### 6.4.4.5 Pro and Cons?
> [!done] ## Pros
> - **Cloning**: ci permette di copiare oggetti esistenti in altre classi senza dipendere dalle classi che l'hanno creati 
> - **Reusable code**: ci permette di togliere codice di inizializzazione ripetuto perché ci saranno i prototipi predefinitivi.
> - **Easy creation**: ci permette di creare facilmente oggetti complessi;
> - **Inheritance substitution**: offre un'alternativa all'ereditarietà per la gestione delle configurazioni di oggetti complessi.

> [!danger] ## Cons
> - **Cloning circular objects**: La clonazione di oggetti complessi con riferimenti circolari[^2] può essere complicata.
> 	

### 6.4.5 Singleton pattern
Con il singleton risolviamo due comuni problemi nella programmazione, violando però il [[SOLID Principals#S - ingle responsibility| principio di singola responsabilità]]:
1. **Ensure that a class has a single instance**: perché controlliamo quante istanze ha una classe? Fondamentale controllare le istanze di una classe quando si parla di controllo degli accessi a delle risorse come i DB o i file, quindi ci assicuriamo che la classe ne possieda solo una. Permettendo a una sola istanza di esistere, si riduce la possibilità di duplicati non necessari, sprechi di memoria o problemi di sincronizzazione

2. **Create an access point for that instance**: con il singleton possiamo svolgere lo stesso compito di una variabile globale, cioè renderla accessibile a  tutti, ma a differenza di quest'ultima, che può subire dei mutamenti se modificata da un esterno,  **con il Singleton la proteggiamo da potenziali sovrascritture accidentali da codici esterni**, offrendo un punto di accesso centralizzato. 
#### 6.4.5.1 Singleton Solution
Con il singleton abbiamo due principali approcci che sono sempre presenti:

- Fare in modo che **il costruttore della classe sia privato**, permettendo così di evitare istanze delle classi in modo accidentali con l'operatore `new`.

- Creare un metodo statico che si comporta come costruttore, questo metodo chiama il costruttore precedentemente messo come `private` per creare l'oggetto e salvarlo in una variabile statica e le chiamate a tali metodo ritornano le variabili che sonno salvate all'interno del costruttore privato.
#### 6.4.5.2 Singleton Structure
![[SingletonStructure.png]]
1. La class `Singleton` dichiara il metodo statico `getInstance()` che ritorna l'istanza della classe stessa.

Il costruttore della classe `Singleton` deve essere nascosto e non visibile dal `Client` in modo che si possa solo accedere tramite il metodo `getInstance()` che sarebbe l'unico modo di prendere l'oggetto della classe `Singleton`.

#### 6.4.5.3 Singleton when use it?
Lo si può utilizzare in due casi:

- Quando vogliamo **condividere una singola istanza di una classe, per renderla disponibile a tutti i client**.Per esempio vogliamo condividere il singolo database con più parti del del programma.

- Quando vogliamo il pieno controllo delle variabili globali. 
#### 6.4.5.4 Singleton how implement it?
1. Aggiungere una variabile `private` e `static` per salvare l'istanza del singleton
```java
class Singleton{
	private static Singleton instance;
}
``` 

2. Dichiarare un metodo pubblico per ottenere l'istanza del singleton
```java
class Singleton{
	private static Singleton instance;

	private static Singleton(){
		...
	}
	public static Singleton getInstance(){
	}
}
```

3. Ora bisogna fare l'implementazione che consiste nel creare un nuovo oggetto di tipo `Singleton()` e metterlo nella variabile privata che abbiamo inizializzato prima e il metodo deve tornare l'istanza di quest'ultimo.
```java
class Singleton{
	private static Singleton instance;

	private static Singleton(){
		...
	}
	public static Singleton getInstance(){
		....
		this.instance = new Singleton();
		return this.instance
	}
}

```

4. Rendere il costruttore della classe privato e il metodo statico che è `public` sarà quello accessible che sarà in grado richiamare il costruttore della classe, ma non altri oggetti.

5. Nel codice del `Client` sostituire le chiamate dirette alla classe `Singleton` con le chiamate la metodo `public static` che abbiamo creato.  

#### 6.4.5.5 Singleton how implement it?
> [!done] ## Pros
> - **Single instance**: sei sicuro che la classe abbia solo una singola istanza.
> - **Single access point to that instance**
> - **Only required**: l'oggetto viene inizializzato solo quando viene richiesto.

> [!danger] ## Cons
> - **Violating the first principle**:  viola il [[SOLID Principals#S - ingle responsibility| principio di singola responsabilità]], questo tramite:
>   
> 	-  Combinazione delle istanze (controllo della creazione e accesso) con il comportamento della classe.
> 	  
> 	- Aggiunge responsabilità di gestione globale che normalmente non dovrebbero competere alla logica interna della classe.
> 	  
> - **Mask bad design**: ad esempio quando componenti di un programma si conoscono troppo a vicenda;
> - **Special treatment**: per il multithreading si possono rischiare incombenze con la creazione di oggetti dello stesso tipo, dovendo gestire tale problematica a parte.   
> 

## 7.0 Structural Design Patterns
---
I pattern strutturali sono quelli che ci permettono di combinare oggetti e classi, per creare grandi strutture, mantenendole flessibili ed efficienti nel tempo.

### 7.1 Adapter pattern
Il _design pattern adapter_ ha la funzione di poter prendere in input una specifica interfaccia, incomprensibile per la classe, rendendola accessibile.
#### 7.1.1 Adapter solution
Come funziona questo design? Come fa a rendere disponibile tali interfacce a classe che non sono compatibili?

- Il nostro _adapter_ prima di tutto crea una interfaccia che sia compatibile con l'oggetto esistente.
- Il nostro oggetto esistente(cioè quello che vogliamo passargli i file convertiti) chiama i metodi dell _adapter_.
- l'adapter converte e inoltra le chiamate all'oggetto target nel formato previsto.
![[Adapter-Example.png]]
In questo esempio vediamo che prima, l'app della borsa non riusciva a prendere i dati dalla banca perché non possedeva il file con il formato giusto.Con la creazione dell adapter ora i dati che prende in input l'XML li converte in formato JSON 

#### 7.1.2 Adapter Structure
La struttura del design pattern _adapter_  la composizione degli oggetti per gestire interfacce incompatibili.
![[Adapter-Structure.png]]
Spieghiamo nel dettaglio come funziona tale struttura:
1. Il `Client` conterrà la logica business del programma.
2. Il `«interface» Client interface` conterrà quelle interfacce che che le altre classi dovranno seguire al fine di poter collaborare con la classe client prima citata.
3. La classe `Service` è una classe che viene utilizzata ed utile in alcune occasioni, ed è quella che il `Client` non può usare perché possiede  interfacce incompatibili con quest'ultima.
4. Infine c'è la classe `Adapter` che implementa l’interfaccia del client(tramite l'interfaccia `«interface» Client interface`) e avvolge il service (si usa l'[[#4.4 Aggregation|aggregazione]]), traducendo le chiamate del client nel formato atteso dal service.

Il vantaggio di utilizzare un approccio del genere consiste che il client non è legato alla classe concreta _adapter_ quindi si possono implementare diversi adapter senza modificare il codice sorgente, un'altro vantaggio è quello che se l'interfaccia della classe `Service` cambia non non c'è bisogno di cambiare tutto il codice ma si va a create un nuovo _adapter_.

Come funziona la **classe adapter** internamente? Il Class `Adapter` utilizza l’ereditarietà per gestire interfacce incompatibili, ereditando le interfacce sia dal client che dal service.
![[Adapter-Internal.png]]
Che funzionalità possiede l'adapter?
- Non avvolge oggetti: eredita direttamente comportamenti da entrambe le classi (client e service).
- L’adattamento avviene tramite il metodo dell'**[[Programming Knowledge#Overriding (sovrascritto)|override]] dei metodi**.
- Può essere utilizzato al posto di una classe client esistente.
Con ==java però da come sappiamo non possiamo fare l'ereditarietà multipla==, questo è solo possibile tramite C++.
#### 7.1.3 Adapter example
![[Adapter-Example 1.png]]
Qui abbiamo un problema di incompatibilità, dove la figura del rettangolo, non si adatta al foro che abbiamo in alto a sinistra, per sapere come il nostro parallelepipedo entra nel buco come facciamo?
Possiamo **utilizzare il nostro adapter per calcolarci il raggio del parallelepipedo** e controllare se può oppure no entrare nel buco:
- L’Adapter si comporta come un cilindro.
- Imposta il raggio del cilindro pari a metà della diagonale del quadrato (calcolata dal metodo `getRadius()` che ritornerà un tipo per compatibile per la classe `RoundHole`).
- Questo ==raggio rappresenta il cerchio minimo che può contenere la forma quadrata==.

#### 7.1.4 When use the adapter?
Quindi in definitiva quando possiamo utilizzare realmente questa classe all'interno del nostro programma?
Lo possiamo usare quando:

- **Interfacce Incompatibili**: si utilizza il pattern Adapter quando vuoi ==usare una classe esistente, ma la sua interfaccia non è compatibile con il resto del tuo codice==.
  
- **Classe che fa da traduttore**: L'Adapter crea una classe intermedia che ==agisce come traduttore tra il tuo codice e una classe legacy==, di terze parti, o con un'interfaccia inconsueta.
  
  - **Estendere funzionalità mancanti:** se diverse super classi mancano di funzionalità, non conviene fare una sottoclasse solo per implementarla, ma con ==l'adapter possiamo aggiungere funzionalità in modo dinamico==

#### 7.1.5 How we can implement it?
Per implementare il design pattern Adapter possiamo seguire i seguenti passi: 

1. **Capire quali sono le classi incompatibili:**  
   sono due gli attori che ci interessano trovare per creare il design, il primo sarà il **client che offrirà il servizio**(nell'esempio di prima la banca), quest'ultimo sarà immodificabile dal punto di vista del codice poi il client o i **client che vogliono usufruire di tale sevizio** (la classe che elabora solo i file JSON).
   
2. **Dichiarare l'interfaccia del client che offrirà il servizio**: 
   dettare le regole al fine di far comprendere a chi utilizzerà tale client che servizio quest'ultimo offrirà, tramite apposita interfaccia.

3. **Creare la classe Adapter**: 
   cioè creare la classe, ma per ora lasciare i metodi di quest'ultima vuoti e non implementarli.

4. **Aggiungi il Riferimento al Servizio**: 
   cioè creare un campo all'interno della classe adapter che servirà in seguito a memorizzare il riferimento alla classe che offre il servizio (può essere inizializzato nel costruttore o nei metodi dell adapter). 

5. **Implementare i metodi dell'interfaccia Client**: 
   Fai in modo che l’adapter delega il lavoro reale alla classe di servizio, gestendo la conversione di interfacce o formati. 

6. **Usa l'Adapter Tramite l’Interfaccia del Client**: 
   I client dovrebbero interagire con l'adapter tramite l'interfaccia del client, permettendo modifiche all adapter senza influire sul codice del client.

#### 7.1.6 Pros and Cons
> [!done] ## Pros
>- **Single Responsibility Principle:** Permette di separare il codice per la conversione di interfacce o dati dalla logica principale del programma.
> 
> - **Open/Closed Principle**: È possibile introdurre nuovi tipi di adapter senza modificare il codice client esistente, purché comunichino tramite l’interfaccia del client

>[!fail] ## Cons
>- **More complexity:** La complessità del codice aumenta per via dell’introduzione di nuove interfacce e classi. Talvolta è più semplice modificare direttamente la classe di servizio per renderla compatibile.

### 7.2 Bridge Pattern
Il _design pattern bridge_ prende in input una classe e lo ==divide in due insiemi di classi separate chiamate astrazione e implementazione== dove ognuno di loro sarà implementato in maniera differente.
Vediamo un esempio di qu
### 7.? Design Pattern Composite
Il pattern composite ci permette di gestire oggetti aggregati, con l'utilizzo di un interfaccia comune che sia applicabile su tutta la struttura.
Con questo design pattern si va ad esplorare in profondità all'interno di un albero di oggetti, senza dover conoscere l'oggetto stesso ma li tratteremmo con lo stesso metodo indifferentemente dal tipo di metodo che abbiamo.
#### ?.? Composite Structure
![[Screenshot 2024-10-30 at 14.31.42.png]]
1. **`Interface` Component**:
2. **Leaf**:
3. **Composite**:
4. **Client**:

****## 8.0 Behavioral Design Patterns

### 8.1 Command Pattern
Il _design pattern command_ serve per gestire la parte della ridondanza del codice, facendo parte del principio di separazione di responsabilità o detto anche [[#S - ingle responsibility|single responsibilty]], creare ogni bottone per ogni operazione, che contengono i dettagli della richiesta, eliminando le sottoclassi e riducendo le ridondanze
![[ButtonImage.png]]
#### 8.1.1 Command Structure
![[Structure.png]]
1. **Sender (invoker)**: inizia la richiesta attivando il comando 
2. **Interfaccia Command**
3. **Concrete Command**: vanno ad implementare l'interfaccia `«interface» Command`
4. **Receiver**:
5. **Client**: Definisce il sender e l'invoker configurando i comandi concreti passando tutti i parametri.
#### 8.1.2 Command where we use it?
Lo utilizziamo per parametrizzare oggetti con azioni, serealizzare comandi trasformarle e salvarli come stringhe e mettendoli in coda, registrarli e inviarli per l'esecuzione remoto.
Implementare operazioni annullabili conservando i backup di quest'ultimi.
# Reference
---
 - Book: _Dive into Design Patterns by Alexander Shvets_ 
 - [_Refactoring Guru_](https://refactoring.guru/design-patterns)
 - For more detail about factory method: [Factory Method](https://refactoring.guru/design-patterns/factory-method)
 - For more detail about abstract method: [Abstract Method](https://refactoring.guru/design-patterns/abstract-factory)
- [^2]: Un **riferimento circolare** si verifica quando due (o più) oggetti si riferiscono l’uno all’altro direttamente o indirettamente