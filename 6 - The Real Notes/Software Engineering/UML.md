---
share_link: https://share.note.sx/zj86yira#YrwnwHRe4ioRoI1p8Yn5/Bh7vqT7l53q8Rghey3YWyw
share_updated: 2026-01-23T23:59:12+01:00
---
2024-10-14 10:38

Status: #devoleped 

Tags: [[Programming]], [[Software Engineering]]

---
```table-of-contents
```

---
>[!warning] **IMPORTANTISSIMO**
>**UML** non è un linguaggio di programmazione!!!! Ma è un modo per strutturare e generare dei modelli grafici da seguire (in inglese chiamati [blueprints](https://dictionary.cambridge.org/dictionary/english/blueprint)), per generare codice.
# 1.0 What is UML?
---
UML (Unified Modeling Language) è un linguaggio per la progettazione, visualizzazione e documentazione di sistemi software e non.

Era stato progettato all'inizio per catturare solo i comportamenti di software complessi e non, ora ha un utilizzo più ampio e si utilizza in più sistemi, anche quelli di processi manifatturieri.

UML non è considerato un linguaggio di programmazione, ma ==un linguaggio figurativo== cioè utilizza solo immagini per descriversi con sintassi formale, cioè che segue delle regole e conferma la sua correttezza. 

Per questo si è trovato un modello comune per tutti i tipi di linguaggi e ==questo tramite l'utilizzo dei diagrammi== cioè una rappresentazione grafica di quello che dobbiamo fare.
![Purpose of UML|Esempio di diagramma figurativo](https://www.tutorialspoint.com/uml/images/purpose_of_uml.jpg)
Un diagramma **UML ci aiuta anche a capire le relazioni che sono presenti negli oggetti del nostro sistema**, cioè come interagiscono tra di loro durante il loro [[Ingegneria del software#2.0 Ciclo di vita & processo di sviluppo|ciclo di vita]], con l'intero sistema.

>[!info]- **Che cos'è un Oggetto?**
>L'oggetto è un entità che possiede dei dati, ma ha anche delle funzionalità per accedere e manipolare i dati stessi.
## 1.1 How we can use UML?
Può essere usato secondo diversi approcci al progetto:

-  **UML come abbozzo**: diagrammi informali e incompleti creati per esplorare parti difficili dello spazio del problema o della soluzione;

-  **UML come progetto**: diagrammi di progetto relativamente dettagliati per reverse engineering o per la generazione di codice;

-  **UML come linguaggio di programmazione**: la specifica completamente eseguibile di un sistema software con UML.
 
 È possibile rappresentare due differenti caratteristiche di un sistema:

- **struttura (statica)**: elementi necessari a modellare il sistema e come sono correlati;

- **comportamento (dinamico)**: ciclo di vita degli oggetti e specifica delle collaborazioni che ci sono tra gli oggetti per fornire le funzionalità richieste.
## 1.2 Perspective and Views of UML
Per la creazione del nostro UML è fondamentale concentrarsi su diverse tipi di prospettive e viste, in base al modello del mondo reale che andiamo a creare.

- [[UML#2.0 Conceptual model|punto di vista concettuale]]: diagrammi scritti e interpretati come descrizioni di oggetti del mondo reale o del dominio di interesse;

- **punto di vista software**: i diagrammi descrivono astrazioni o componenti software come implementazioni SW con riferimento a una particolare tecnologia o specifiche e interfacce di componenti software indipendentemente dalla implementazione.
![[Screenshot 2025-09-26 at 10.07.13.png]]

1. Il primo esempio rappresenta un **punto di vista concettuale** cioè una rappresentazione della realtà di come sarà il nostro sistema.

2. Il secondo invece viene definito **punto di vista software**, perché andremmo a illustrare concetti software come le classi, con i suoi metodi e attributi.
# 2.0 Conceptual model 
---
Il modello concettuale è una struttura nella quale si rappresentano i concetti e le loro relazioni, ed è uno dei primi step prima di disegnare il modello UML, questo perché riesce a far si che si possa capire quali saranno le entità del mondo reale e come interagiranno tra loro.

Cose _importanti_ da sapere per il modello concettuale:

- Costruire i [[#4.0 UML building blocks|blocchi UML]]
- Regole per connettere i blocchi [[#4.2 Relation|relazioni]]
- Meccanismi comuni dell'UML 
# 3.0 Object-Oriented concepts
---
Un oggetto contiene dei dati e dei metodi che quest'ultimi controllano e gestiscono tali dati.

Tali oggetti descrivono una gerarchia di modelli del mondo reale che esistono intorno a noi, come ad esempio l'[[Design Pattern#3.1 Abstraction|astrazione]], l'[[Design Pattern#3.2 Encapsulation|incapsulamento]] , l'[[Design Pattern#3.3 Inheritance (ereditarietà)|ereditarietà]] e il [[Design Pattern#3.4 Polymorphism|polimorfismo]] che possono essere tutti rappresentati in UML.
### 3.1 Analysis and Design of OO
Viene definito la OO (_Object-Oriented_) come un investigatore di oggetti e il design aiuta/collabora per identificare tale oggetti.

Il concetto principale dell'analisi della OO è quello di identificare i sistemi da dover progettare/sviluppare, analisi svoltasi anche nel caso di oggetti già esistenti.
Dopo aver identificato gli oggetti, si passa a creare delle relazioni tra loro e il design è concluso.
I passi principali della OO analysis son:

- Identificare gli oggetti/bocchi di un sistema 
- Identificare le loro relazioni.
- Creare un design per far in modo di renderlo convertibile in un OO language. 
### 3.2 Phase of the analysis
```bash
OO Analysis -> OO Desing -> OO Implementation using OO languages
```
1. La cosa fondamentale dell'analisi è quello di ==identificare gli oggetti e descriverli nella maniera appropriata==, questi devono essere identificati con le loro responsabilità.
   >[!info]- **Che cosa sono le responsabilità?**
   >Sono  delle task che devono soddisfare, se le responsabilità degli oggetti collaborassero tra loro si creerebbe un sistema completo.

2. Si passa poi al design, che consiste nel far in modo che i vari oggetti collaborino per completare le loro responsabilità, mettendo enfasi su quest'ultime durante il processo. 

3. L'ultimo step consiste nell'implementare il design creato nei linguaggi di programmazione ad OO come Java o C++.
### 3.3 Real Word use of UML
Possiamo usare i diagrammi UML per lo sviluppo di applicazioni web, creando un software che vada a soddisfare i requisiti che sono richiesti dal cliente.

UML ci fornisce dei diagrammi già pre impostati che possiamo utilizzare all'interno del nostro progetto:
>[!example] **Esempio di diagrammi predifinitivi**
>- Web app use case models
>- Web app implementation model
>- Web app deployment model
>- Web app security model
>- Web app site map

Ci aiuta anche a distinguere le varie azioni che si possono svolgere in ambito front-end e back-end, definendo le interazioni che andrà a svolgere l'utente con le varie connessioni alle pagine presenti nella nostra applicazione web, ad esempio mostrare gli [[HTML#0.1 hyperlink|hyperlinks]] presenti nella pagina.
# 4.0 UML building basics
---
Le basi della struttura di UML è composta da ben 3 elementi fondamentali:

- **I blocchi fondanti dell UML** che  possono essere definiti come un'insieme di [[#4.1 Things (entities)|oggetti]], [[UML#4.2 Relation|relazioni]] e [[UML#4.3 Diagrams|diagrammi]].
  
- Poi ci sono dei **meccanismi** che  si servono di tecniche comuni  cioè metodi, strategie o processi frequentemente usati per conseguire certi risultati e raggiungere specifici obbiettivi.  

- **L'architettura**: cioè come UML esprime la struttura di un sistema.
### 4.1 Things (entities)
Gli oggetti a loro volta sono classificati in diversi tipi:
-  _Strutturali_ 
- _Comportamentali_
- _Gruppo_ 
- _Annotativi_

>[!note]
>Gli **oggetti strutturali** sono parti statiche del modello che rappresentano gli elementi fisici e concettuali.

#### 4.1.1 Structure Things
Eccone alcuni diagrammi  _Strutturali_ da sapere.
![[EsempioDiOggetti strutturali.png]]

#### 4.1.2 Behavioral Things
Poi ci sono le entità _comportamentali_ che sono la parte dinamica dell'UML e sono i seguenti:
![[Behavioral.png]]
#### 4.1.3 Package Things
Le entità di _gruppo_ sono quelle che vengono utilizzate principalmente per raggruppare elementi di un modello UML (classi o oggetti).
![[Groupthing.png]]
#### 4.1.4 Annotational Things
L'ultima entità sarebbe quella di annotazione che contiene solo una descrizione o commento di un modello UML
![[AnnotationThing.png]]
### 4.2 Relation
Relazione è un sottoinsieme del prodotto cartesiano di due insiemi, **nell'UML le relazioni creano un sottoinsieme delle possibile combinazioni di un prodotto tra due insiemi**. 

Cioè in parole povere:

>[!info] Che cos'è una relazione?
>La relazione viene intesa come tutte le connessioni che ci sono tra gli elementi/oggetti, cioè come sono correlati gli elementi e che proprietà devono rispettarsi a vicenda.


![[RelazioneDisegno.png]]

Per info maggiori sulle relazioni, vedere la parte di [[Design Pattern#4.0 Relation between objects|relazioni tra gli oggetti]]
### 4.3 Diagrams

>[!info] Definizione
>Il _diagramma_ sarebbero una ==vista o detta anche semplicemente, la parte visiva e grafica del nostro sistema che vogliamo modellare==, mostrandone le entità (concetti), le relazioni che abbiamo visto precedentemente e i  vari vincoli esistenziali.

Sono ben 13 i diagrammi che possiede UML, non so se li vedremmo tutti, ma meglio di niente è.
![[UML diagrams.png]]

Ci sono due prospettive di visionare le *classi*, all'interno dei vari diagrammi

Vedremmo come sono divisi questi due macro famiglie dei diagrammi:
- **Diagrammi Strutturali (Statici)**: definiscono la struttura del nostro sistema, cioè le componenti che avrà, le relazioni che possiede e i dati (o attributi per il diagramma delle classi).
- **Diagrammi Comportamentali (Dinamici)**: sono quei diagrammi che andranno a specificare come i vari oggetti del nostro sistema si comportano ed interagiscono tra di loro, avremmo come esempio di diagrammi i sequence, gli activity e gli UC diagram.
### 4.4 Common Mechanism
Sono tecniche comuni per raggiungere specifici obiettivi:
- **Specifiche**: ai diagrammi che rappresentiamo si aggiungono anche delle informazioni aggiuntive, solitamente informazioni testuali, che le chiameremmo **specifiche**. Questi diagrammi quando possiedono delle specifiche gli danno una semantica (un significato), rendendo il diagramma completo e consistente.
  
- **Ornamenti**: ogni elemento ha una versione base ma può in generale essere arricchito per poter evidenziare informazioni aggiuntive. Sono usati per arricchire la modellazione UML e fornire informazioni aggiuntive su determinati elementi del modello;

- **Distinzioni Comuni**: metodi per distinguere gli elementi UML in modo differente, creando delle differenze tra i vari elementi, ci sono due tipologie di distinzioni comuni:
	- *classificatore vs. istanza*: 
	  Il **classificato** è la rappresentazione di una classe in Java mentre la rappresentazione concreta del classificatore sarebbe l'istanza della classe.
	
	- *Interfaccia vs. implementazione*: 
	  **Interfaccia** sarebbe un contratto, con una sequenza di operazioni, che una determinata classe deve rispettare se la va ad implementare, mentre l'**implementazione** sarebbe la realizzazione del contratto che si è definito.
	
# 5.0 Use case base mechanism
---
Approccio _user driven_ cioè che si interagisce con l'utente per ottenere principalmente i requisiti che servono al nostro sistema.
Per la descrizione degli scenari, ==si devono identificare gli attori== che faranno parte di un confine del sistema, poi si andrà a chiedere i casi d'uso del sistema che saranno dal punto di vista dell'attore/.i usare la forma passiva nei casi d'uso).
### 5.1 Elements
Ruolo che assumo un'entità esterna quando interagisce con un sistema, ==che può assumere più ruoli== e non sono le persone fisiche che pensiamo noi.
Come possiamo individuare un attore:

- Chi sta usando il sistemi? Chi lo installa?
- Chi partecipa alle varie fasi del sistema e al suo ciclo di vita?
- Chi ne ottiene le informazioni e chi ne fornisce?
 ![[ActorExample.png]]
Visualizzazione grafica dell'attore e del cliente che usa o fornisce un sistema.

>[!info] Actor
>**Attori** sono tutti coloro che interagiscono con il sistema, non per forza sono persone ma possono essere anche componenti hardware e software.

Sono divisi in tre macro categorie:
 - **Primari**: sono fondamentali per il sistema e ci interagiscono direttamente
 - **Supporto**: Offrono un servizio al sistema.
 - **Fuori Scena**: sono interessati al funzionamento del sistema, ma non ci interagiscono direttamente.

Ci sono i **Casi D'Uso** ed infine i Confini del sistema.
### 5.2 Format for use case
Ci sono principalmente 3 tipologie di formati.
![[DifferentForEachFormat.png]]
### 5.3 How specify them?
Le sezioni che compongono un caso d'uso sono le seguenti:

- ***Nome***: nome da ricordare per descrivere di cosa parlano.
- ***ID***: un numero di serie che gli diamo.
- ***Breve descrizione:*** per spiegare di cosa serve un caso d'uso.
- ***Attori***: specificati sia gli attori primari che quelli secondari.
- ***Pre-condizioni***: condizioni che si verificano prima di poter attivare il caso d'uso (autenticazione utente su piattaforma esse3).
- ***Sequenza degli eventi principali***: descrizione dei passi che avvengono nel caso d'uso.
- ***Post-condizioni***: cosa dovrà essere vero alla fine.
- ***Sequenza degli eventi alternativa***: eccezioni condizioni che si verificano durante il normale flusso di lavoro.

### 5.4 Principal sequence
Sarebbero i passi che fanno parte del caso d'uso, dove il primo passo (chiamato passo d'attivazione) viene compiuto dall'attore principale nel nostro sistema, la struttura dei vari passi si presenta in questa maniera:

>[!note]
>`<numero del passo> Il <qualcosa>"provoca"<qualche azione>`

Esempio: 
`1. Il cliente sta accedendo alla homepage`

Nel caso delle sequenze principali, si possono trovare due tipi di deviazioni:

- ***deviazione semplice:*** si crea solo una ramificazione della sequenza che prendiamo in considerazione.
- ***deviazione complessa:*** serie di eventi alternativi che possono accadere se non segue il normale flusso del lavoro.

>[!question] **Tips**
>- Si deve sempre scrivere le **frasi in forma passiva e non attiva**, in tal caso dopo non si capisce chi ha fatto cosa.
>  
>- Ogni volta che si fa una ramificazione interna da una sequenza si parte con il _Se_ e il suo numero successivo (come faccio io con i titoli e i sottotitoli in obsidian).
>  
>  Esempio:
> - 1 Il cliente acquista la spesa con la carta. (_sequenza principale_)
> 	- 1.1 Il pos richiede di scegliere con quale banca si vuole fare il pagamento.
> 	- 1.2 Il pos richiede di inserire il PIN e premere il tasto verde quando ha finito.
> 	  
>- Se dobbiamo far ripetere un'azione più e più volte usiamo il ciclo `for` o `while` oppure possiamo rimandare la nostra sequenza che vogliamo far ripetere ad una precedente.

### 5.5 Alternative Sequence 
Sono quelle che ==si verificano quando ad una sequenza principale si verificano casi di errori o eccezioni==, i casi in cui troviamo queste sequenze alternative ed agiscono su quelle principali sono:
- Quando la sequenza alternativa sostituisce quella principale.
- Dopo una sequenza principale.
- In qualunque parte nella sequenza principale.
  
>[!warning] **Attenzione**
>Una sequenza alternativa **non deve prevedere altre sequenze alternative** diventerebbe troppo complesso l'operato.

 Possono però prevedere al loro interno delle pre condizioni o delle post condizioni.

### 5.6 When we use a UC
Possiamo descrivere i nostri casi d'uso nei casi in cui ci siano **molti utenti che interagiscono con diverse funzionalità**, quando il nostro **sistema è dominato da requisiti funzionali**[^1] e se molte delle **interfaccia che abbiamo interagiscono con tanti sistemi**.

Per capire se stiamo seguendo un giusto livello d'astrazione dobbiamo eseguire dei test che ci permettono di verificare tale correttezza dell'operato in corso, questo tramite:
- Test del Capo
- Test Processo di Business Elementare
- Test della dimensione
# 6.0 Use Case advanced mechanism
---
Questi meccanismi servono per rendere il sistema più semplice evitando duplicazioni o casi nella quale si vanno a riscontrare delle problematiche nell'assegnazione dell'attore al caso d'uso specifico.

### 6.1 Generalization through actors
Quando si incontrano sistemi nella quale ci sono molti attori che utilizzano specifici casi d'uso di altri attori (nel caso grafico dove un attore si intreccia con casi d'uso di altri attori formando molte linee), oppure nel caso in cui un attore utilizza un sistema che presenta dei passi che sono simili o si distinguono per pochi passi.

Per ovviare a queste ripetizioni useremmo dei meccanismi di **generalizzazione** degli attori.
![[ExampleGeneralizationWithActors.png]]
### 6.2 Generalization through UC
L'utilizzo di una generalizzazione in un caso d'uso è dovuta principalmente a tre fattori scatenanti:
- Quando si vogliono **ereditare caratteristiche da un'altro UC**
- Quando si vogliono **aggiungere nuove caratteristiche non presenti precedentemente**.
- Quando si **modifica o ridefinisce una nuova caratteristica**.

Ora vedremmo come si rappresentano tale caratteristiche nella specifica dal punto di vista delle numerazioni:
- **Ereditata senza modifiche** - da x. non cambia la numerazione perché non è modificato (x.)
- **Ereditata ed rinumerato** - da x.y  ad (z.t)
- **Ereditata e ridefinita** - da x. sempre stesso passo ma modificato (_o_ x)
- **Ereditata, ridefinita e rinumerata** - x.y( _o_ z.t)
- **Aggiunta** - x. se prima non c'era aggiungere un nuovo numero.

>[!warning] N.B
>L'ereditarietà è comoda, ma non sempre necessaria e indispensabile
### 6.3 Inclusion 
Il meccanismo dell'inclusione, consiste nell'attivare un caso d'uso quando si arriva ad una specifica sequenza principale (o alternativa), ad esempio come vediamo da questa immagine, quando vado nel passo x del caso d'uso `Acquista Prodotto`, si andrà anche ad attivare il passo y del caso d'uso `Aggiungere Credito` 
![[FuntionalityOfInclude.png]]
`Aggiungere Credito` avrà il compito come le funzioni nei linguaggi di programmazione, si passa nelle sequenze del caso d'uso che includiamo, poi ritorniamo ai nostri passi originali, diremmo che **sarà un caso d'uso assestante**

>[!warning] **IMPORTANTISSIMO**
>Quando si fanno queste modifiche grafiche le si devono fare pure all'interno della specifica, descrivendone l'attivazione del caso d'uso assestante.
>![[SpecificationUC.png]]
>come vedi in figura evidenziato in blu bisogna ***specificarlo***

Cercare il modo di **non creare catene profonde di include** all'interno della specifica, garantendo sempre che le condizioni del caso d'uso che vogliamo includere sia attivato se no non attiviamo niente, devono essere garantite all'avvio e all'uscita.

### 6.4 Extension
Meccanismo per mandare delle specifiche nuove (come un Plug-in), il sistema funziona perfettamente, ma posso aggiungere delle nuove funzionalità che lo rendono migliore, cioè dei ganci per poter implementare future specifiche (esempio dei premi o sconti nella cassa dopo tot euro di spesa).
![[ExtensionExample.png]]
Lo `UseCaseEsteso` si aggancerà allo use case `Gestione Cassa` quando si attiveranno delle pre-condizioni al suo interno, come ad esempio quello del `SubTot`.

Il caso d'uso può esistere anche senza la sua estensione.
>[!question] **Cosa serve in conclusione?**
>L'estensione serve per **programmare future implementazioni di un caso d'uso esistente.**

# 7.0 Class diagram 
---
>[!info] **Che cos'è?**
>Il diagrammi delle classi **è un rappresentazione statica del sistema**, dove troveremmo gli attributi, i metodi e le relazioni che ci sono tra le varie classi.

Una classe ed un oggetto rispondo ad una relazione di *dipendenza steriotipata*?

>[!question] **Che vuol dire *dipendenza steriotipata*?**
>Vuol dire che due classi A e B possono avere una dipendenza tra di loro perché ci possono essere dei metodi della classe A che richiamano i metodi della classe B.

Prendiamo ad esempio di `GameConsole` e `Game`
![[Pasted image 20251210155827.png|GameConsole ha bisogno di Game per poter usare il metodo play]]

Si viene ad utilizzare il `<<dependency>>` per definire che una classe dipende da un'altra, lo abbiamo visto nelle [[#4.2 Relation|relazioni]], la freccia tratteggiata rossa indica la dipendenza.

>[!info]- **Perché si fa questo?**
>La dipendenza è una relazione molto debole, cioè la classe che dipende da un'altra non condivide attributi o operazioni, ma utilizza quest'ultima per svolgere alcune operazioni che possiede, lo si fa principalmente perché **si cerca di mante un alta coesione e un basso accoppiamento**, vedremmo meglio cosa vuol dire queste due cose.

>[!question]- Istanza = oggetto?
>**Si!** Sono tutte e due la stessa identica cosa, non fa differenza dire **istanza** di una classe o **oggetto** un'istanza di una classe è un oggetto concreto creato a partire dal modello (la classe), e non c'è differenza pratica tra i termini *oggetto* e *istanza*: spesso sono sinonimi, anche se in contesti precisi "istanza" insiste sul fatto che l'oggetto è una realizzazione di una specifica classe.
>
## 7.1 Object and Identity
Il concetto di _identità_ è definito come il riferimento a quell ==oggetto che si distingue da altri oggetti della sua stessa natura (stessa natura inteso che possiedono lo stesso puntatore)==, con la presenza di due concetti differenti e sono:
- **Stato:** valori dei suoi attributi e connessione ad altri oggetti
- **Comportamento**: azioni che possono essere richieste all'oggetto.   

È in genere utile distinguere tra le **azioni che possono causare un cambiamento di stato** e quelle che **invece lasciano immutato lo stato interno dell'oggetto stesso**.
## 7.2 Object structure 

>[!info] Definizione
>Un **diagramma degli oggetti** è una rappresentazione statica delle istanze delle classi (oggetti) e delle loro relazioni in un momento specifico.

**Diagramma degli oggetti** possiamo rappresentare il nome degli attributi della classe ed i valori che la compongono. 

![[ObjectStructure.png]]

>[!info] **Sottosezione Nome**:
Questa sopra presente è la rappresentazione grafica dell oggetto, con la prima riga il **nome dell'oggetto** e il **riferimento alla sua classe**.

>[!info] Sottosezione Attributi
>Poi abbiamo la lista degli attributi che compongono l'oggetto, in questo caso abbiamo:
>
>*nomeAttributo: tipoAttributo = "valore"*

## 7.3 Class structure

Un buon progetto **Object Oriented**, deve partire da un buon modello concettuale[^3], devo realizzare bene le classi che implementano siano arbitrarie, quelle classi che realizzano le funzionalità fondamentali devo rimandare a concetti concreti, cioè che siano nella realtà (non inteso come tangibili - toccabili), ma concetti che esistono nell'immaginario reale.

>[!quote]
>Le classi che sceglieremmo per rappresentare la realtà non è oggettiva, ma dipenderanno dalla prospettiva con cui vediamo la realtà.
>

Quindi quello che dovremmo fare sarà **scegliere i concetti più interessanti** (cioè quelli più rilevanti della realtà), l'obbiettivo finale non è quello di disegnare classi, ma un diagramma per rappresentare un modello concettuale.

## 7.4 UML notation

![[NotazioneDiClasse.png]]
- **Stereotipo**: data una tecnologia in input posso creare da quest'ultima uno stereotipo, che se dichiarato su una classe quest'ultima eredita dallo stereotipo le sue tecnologie (esempio: qualcuno ha steriotipato il concetto di studente, con nome, cognome, matricola ecc.., cioè si porta dietro una serie di attributi di un'altra classe ).
- **Valore etichettato:** Valori descrittivi di chi ha creato tale classe e descrizioni, non hanno influenza nella rappresentazione (tipo i commenti nel codice)
- **Ornamento di visibilità**: sono 4  e possono stare nei metodi o attributi della classe:
	-  **+**: [[Programming Knowledge#`public`|public]];
	-  **-**: [[Programming Knowledge#`private`|private]];
	-  **~**: package[^4];
	-  **#**: [[Programming Knowledge#`protected`|protected]];
- **Parametri IN - OUT**: parametri che passiamo ad un metodo **IN** e quelli che ritornano, cioè quelli in output (quelli output sono rappresentati fuori dal metodo esempio `getSaldo(): double` ritornerà un valore di tipo double in **OUT**);
- **Metodo o Attributo sottolineato**: sono metodi o attributi di classe cioè quelli che dichiariamo [[Programming Knowledge#`static`|static]];
- **Costruttore:** il costruttore nella notazione UML si scrive con il _create_ che poi dopo vengon sostituiti con il nome della classe nella scrittura del codice stesso

>[!warning] Step to follow for class namespaces
>- **UpperCamelCase**
>- **NO special character or letters with accents**
>- **name that explicit the scope of the class**

>[!warning] **Step to follow for attribute namespace**
>- lowerCamelCase
>- Visibilità (+,  - , #, ~)
>- Tipo - tipi primitivi (Integer, UnlimitedNatural, Boolean, String)
>- Molteplicità per rappresentare array con le parentesi quadre []
>- Si posson mettere parametri di tipo _isQuery_ [^5]

### 7.4.1 Model domain and project domain

>[!objective]
>Il **modello di dominio** e il **modello di progetto** sono due distinte rappresentazioni che andremmo a svolgere, per dare una visione chiara della struttura del sistema che andremmo a creare.
#### 7.4.1.2 Model domain

>[!info] Definizione
>I **modelli di dominio** sono quelli utilizzati per **descrivere il funzionamento del sistema e come le entità interagiscono tra di loro.** 

Il modello è utile quando abbiamo necessità di descrivere in modo generico come il sistema funzionerà, cioè delle interazioni che hanno le entità con il sistema in se.
![[Pasted image 20251210172856.png]]

Ci aiuto ad identificare i concetti chiave, a chiarire le relazioni e a stabilire una base solida per la progettazione del sistema.
#### 7.4.1.3 Model Project

>[!info] Definizione
>I **modelli di progetto** danno una rappresentazione più dettagliata del sistema, traducendo il modello di dominio in una soluzione pratica ed implementabile.

Si andrà principalmente a migliorare il modello di dominio che si è definito precedentemente nella fase di analisi e progettazione, rendendolo comprensibile ed applicabile per la fase di implementazione e mantenimento del sistema software.

![[Pasted image 20251210173921.png|Abbiamo dei metodi e degli attirbuti specificando come sarà il sistema]]

>[!info] **Summary**
>In sintesi, il **modello di dominio** rappresenta il cosa del sistema, mentre il **modello di progetto** rappresenta il come il sistema sarà realizzato.
## 7.5 Phase for create class diagram
Ci sono due tipologie di diagrammi di classe che possiamo rappresentare in base alla fase di sviluppo del progetto e sono ben due: 

- **Fase di analisi** ([[#7.4.1.2 Model domain|modello di dominio]]): e si basano principalmente su _cosa dovrà fare_ il sistema, realizzando un modello concettuale delle classi quello che posso immaginare sarà il progetto e verrà rappresentato: 
  
	- **nome** della classe rappresenta concetti della realtà;
	- **attributi fondamentali** che possono esser presenti;
	- **operazioni fondamentali** come operazioni o azioni (no costruttori o distruttori), in sostanza tutte le _responsabilità che possiede_ cioè cosa l'oggetto sa fare non va messo **nessun attributo al suo interno**;
	- **stereotipo** se lo definisco ed è richiesto in ambito business;
	- la classe ha una corrispondenza nella realtà (non quella tangibile), **non posso riportare qui la soluzione**
>[!quote] **N.B**
	>Non possiedo all'interno di questo diagramma concetti tecnologici o che riguardano la user interface, niente persistenza (cioè un dato o un'azione che rimane presente nel sistema dopo il suo riavvio/reset) o come lo faccio tale sistema

- **Fase di progetto:** spiega _come realizza_ tale sistema, ci troviamo nel mondo della soluzione del problema includendo i dettagli massimi che possiamo, aggiungendo al diagramma delle classi di analisi la:
  
	- **visibilità** degli attributi e metodi che abbiamo definito in precedenza;
	- **parametri** che prima non avevamo messo all'interno delle operazioni che saranno nel codice 
### 7.5.1 Classi Di Analisi
Dobbiamo capire per prima cosa, **quali saranno quelle classi che ci permette di soddisfare i requisiti che il nostro sistema ci richiede?**

Parliamo del concetto di **classe di analisi**, quest'ultima serve a rappresentare i concetti della realtà in modo da far si che il nostro sistema che andremmo a creare sarà capace di manipolare. Queste verranno infine perfezionate nelle classi di progetto, qui di seguito alcuni modelli che possiamo prenderne spunto:

- Modello di business;
- Modello dei requisiti;
- Modello dei casi d'uso;
- Descrizione dell'architettura;

Per avere una buona classe di analisi bisogna rispettare il vincolo sul nome, essere riconducibile alla realtà o al concetto che che ci interessa, deve possedere un'insieme ridotto di responsabilità e coeso (cioè deve essere coerente con la realtà che rappresentiamo) e infine ma non per ultimo ridurre le **interdipendeze[^6] con le altre classi**.

>[!error] **ERRORI DA EVITARE NEL PROGETTO**
>- **Classi isolate** che non collabora con nessuno e che non partecipa a nessuna responsabilità;
>- **Classi che rimandano a funzioni** cioè che possiede nomi di una funzione;
>- **Alberi di ereditarietà** ci sono troppe ereditarietà in una singola classe, **codice poco struttura e meno comprensibile**
#### 7.5.1 Individuare le Classi Di Analisi

>[!info] Definizione
>In questa fase si va ad individuare chi sono le entità principali del nostro sistema, comprendendo che relazione hanno a vicenda e le operazioni che svolgeranno. Questo per soddisfare i requisiti del sistema

Le tecniche principali identificare le classi analisi sono le presenti:

- Analisi **Nome-Verbo**;
- Classi **CRC** (C- Class, R- Responsibility, C- Collaborators);
- Elenchi di categorie concettuali;
- Modelli di dominio;
##### 7.5.1.1 Analysis name-verb
Si basa sul fatto di prendere un documento, in questo caso il nostro progetto, identificando prima di tutti due macro categorie: **Nomi** e **Verbi**.

Ci focalizziamo sulla realtà che il documento descrive dove i nomi rappresentano i **concetti** e i verbi sono le **attività**. 
- Si andrà a **creare una lista dei nomi e dei pronomi nominali** che saranno i nostri canditati per diventare delle classi;
  
- Elenco dei **verbi e dei predicati verbali che abbiamo trovato** all'interno del nostro documento Gli elementi in questa lista saranno i possibili candidati a **definire le responsabilità** delle classi.
##### 7.5.2.1 Analysis CRC (Class - Responsibility - Collaborators)
Attività di brainstorming, di team organizzata su due principale fasi, cioè oltre a scrivere classi e responsabilità si vengono anche a scrivere i **collaborator**.

Che sono delle classi che sono fondamentali per le altre classi a soddisfare una responsabilità, andando a collaborare nell'assolvere una responsabilità che la classe si è presa.

Come sono le fasi del CRC: 
- **Commenti** ed **Analisi** sono raccolte durante gli incontri di "brainstorming";
- Ognuno deve identificare tutte le cose che agiscono nel proprio domini;
- ﻿Ognuna di queste "cose" viene annotata in un post-it insieme al nome ed alle responsabilità che si ritengono importanti per la classe;
- Cercare di identificare le classi che potrebbero avere necessità di interagire ed annotare sul post-it.
  
Nella seconda fase i ==post-it vengono riconsiderati per capire quali devono acquisire lo status di classe nel modello concettuale e quali invece di attributo==. 

Nel dubbio il concetto viene inserito come classe.

### 7.6 Class Relations
Le **relazioni** che andremmo a trattare saranno tra le classi e gli oggetti e sono di diversa natura, il ==collegamento semantico tra due oggetti che consente ai due di scambiarsi messaggi==, cioè che un oggetto conosce l'altro e viceversa (in Object Oriented vuol dire invocare semplicemente un'altro metodo) è comunque necessario che chi vuole inviare un messaggio possa recuperare un riferimento a chi lo deve ricevere.

Questi collegamenti sono considerate delle connessioni dinamiche,  questo perché un **diagramma degli oggetti** che ==rappresenta un sistema in un certo momento, in un certo stato== che viene rappresentato dai **valori dei suoi parametri**, dove ci possono essere tra i suoi parametri riferimenti ad altri oggetti.
![[ObjectDiagram.png]]
Il diagramma in questione rappresenta un stato del sistema che noi vogliamo salvare (tipo una fotografia ad un'evento importante), questo esempio `Company` è collegato tramite un link a due `Department`,
#### 7.6.1 Class Association
Tra due classi esistono delle associazioni, quando queste classi hanno la possibilità di collaborare, **se esiste un collegamento tra oggetti deve esistere un associazione di qualche tipo tra le classi corrispondenti**.

Le associazioni sono indicate in questo modo:
- **nome dell'associazione**: che deve essere esplicativo (cioè con significato), letta in un solo verso da sinistra a destra 
- nome dei **ruoli**
- **molteplicità** (trucco per metterla leggere con il linguaggio naturale)
- **navigabilità**

#### 7.6.2 Class molteplicity 
Indicano ==la quantità degli oggetti che partecipano ad una specifica relazione==, ponendo un vincolo sulla cardinalità della relazione, Viene definita attraverso specifiche stringhe, che **indicano minimo e massimo** (come in DB solo che non si ha più n ma * ), **poste al termine dei due lati del simbolo di associazione**:
- 0...1 (min=0, max=1
- ﻿1 (min=1, max=1)
- 0...* oppure * (min=0, max=unbounded)
- ﻿1...* (min=1, max=unbounded)
- 1..6 (min=1, max=6)
- 1...4,6...9,12...15,17...* (unione di intervalli)
La molteplicità può e dovrebbe essere indicata nei modelli di analisi.
Nel caso **non venga indicata si assume indefinita**
#### 7.6.3 Class driving 
La navigabilità indica la possibilità di inviare messaggi(invocazione di un metodo) tra gli oggetti associati, i simboli usati per indicare la navigabilità sono questi due:

- →: la freccia indica di poter navigare nella direzione della freccia;
- x: indica che non si può navigare in quella direzione;
#### 7.6.4 Association and Attribute 
Per definire il concetto di associazione, lo definiamo come quell attributo che ha come tipo la classe di destinazione, quando si viene ad avere più di uno nella cardinalità si viene a creare un vettore o collezione di classi.

#### 7.6.5 Association Class
Sono delle classi che vengono utilizzate per dare semantica (cioè significato delle cose) alla relazione tra le classi,==cioè dare significato alla coppia delle classi che associamo==, tramite l'utilizzo di specifici attributi.

Come ad esempio:
- relazione azienda/lavoratore;
- relazione reificate (sala/incassi/titolo)

#### 7.6.6 Dependency
Per rappresentare relazioni più deboli, cioè sono delle interazioni tra le classi che non si mantengono nel tempo, sono considerate passeggere, non rappresentano la realtà nella sua continuità, le dipendenze sono di diverse tipo:

- [[#7.6.6.1 Use Dependency|Uso]]
- [[#7.6.6.2 Abstraction Dependency|Astrazione]]
- [[#7.6.6.3 Permit Dependency|Permesso]]
Queste dipendenze nel mondo delle classi di progetto sono presenti tra i seguenti elementi:

- classe e classe;
- package e package; 
- oggetti e classi;
- operazioni e classi;
  
Usarlo in modo parsimonioso e non sporadico, per rappresentarla si usa una freccia con la linea tratteggiata invece che continua, vedere [[#4.2 Relation|qui]].
##### 7.6.6.1 Use Dependency
>[!info] Definition
>Le dipendenze d'uso sono rese disponibili da un fornitore e vengono usate dai clienti per poter implementare un loro comportamento.

Le dipendenze d'uso possono essere caratterizzate in diversi tipi:
- **Usa**: 
	- Un metodo della classe **A ha bisogno di un parametro della classe B**
	- Un metodo della classe **A restituisce un valore della classe B**
	- Un metodo di una classe che **usa un oggetto della classe B anche se non come parametro**
	  
- **Chiama**: tra le operazioni di una classe cioè metto le linee tratteggiate tra i metodi delle classi (molto raro);
  
	- **Parametro:** parametri passati IN e OUT;

- **Invio**: invocazione di un metodo di una classe in qualche modo;

- **Istanza:** cioè un oggetto che viene richiamato da una classe diversa dalla propria;  
##### 7.6.6.2 Abstraction Dependency
>[!info] Definition
>Una relazione che si crea tra il fornitore e il cliente, dove però il fornitore è più astratto del cliente.

Possiamo trovare la relazione **traccia**, dove si vengono a segnare le modifiche che vengono svolte tra un modello vecchio a quello nuovo (esempio se dal vecchio modello al nuovo, si è cambiato il nome della classe si va a **tracciare il cambiamento**), 
poi abbiamo anche le relazioni **raffina**, **sostituisci** e **deriva-da** che sono più dettagliate e non servono a noi per ora, ma servono per passare ad un modello più raffinato.
##### 7.6.6.3 Permit Dependency
>[!info] Definition
>Il fornitore assegna diritti di accesso al proprio contenuto: in questo
modo il fornitore limita e controlla gli accessi al proprio contenuto.

Avendo in questo caso due tipologie di dipendenze una che riguarda l'**accesso** ed una che invece riguarda l' **importa** dove si ha una relazione transitiva (queste due sono riferite ai package)

### 7.7 Inheritance relations (Relazioni di ereditarietà)
Relazioni che vengono usate spesso sono quelle di **Generalizzazione** e **Specializzazione**, che coesistono tra due classi. (la prima spesso viene intesa anche come ereditarietà)

>[!tip] Example
>La **Generalizzazione**, si può rappresentare come studente concetto generico e studente magistrale come sotto insieme degli studenti.

La freccia per la generalizzazione la puoi vedere [[#4.2 Relation|qui]], questa relazione è molto vincolata, viene usata il verbo **"essere"**, esempio _studente essere anche studente magistrale_.

#### 7.7.1 Inheritance (Ereditarietà)
Prima di dover cercare le classi che vengono estese è buona norma cercare le classi generiche, per poi proseguire con la specializzazioni, tutte le sottoclassi specializzate ereditano:
- attributi
- operazioni
- relazioni
- vincoli
  
Le sottoclassi possono poi ridefinire ([[Programming Knowledge#Overriding (sovrascritto)|overriding]]) quanto definito nella superclasse. In molti casi non ha senso definire comportamento di un metodo direttamente nella superclasse. D'altra parte in alcuni casi il comportamento è generale per tutte le classi che possono essere ridefinite a partire dalla superclasse (caso delle operazioni astratte)

>[!danger] **IMPORTANTE**
>Cercare di non utilizzare il concetto di [[Design Pattern#3.3 Inheritance (ereditarietà)|ereditarietà]] su **classi che non conosciamo il loro ciclo di vita**.


![[ExampleOfEredity.png]]

>[!important] **N.B**
>Importante dover usare i concetti allo stesso livello d'astrazione, cioè i concetti devono essere coerenti con la realtà che ci troviamo, evitando di mischiare le astrazioni.

#### 7.7.2 Meta-models and Model
Per quanto riguarda l'astrazione è fondamentale distinguere tra modelli e meta-modelli.
![[ModelAndMetaModel.png]]
Sono composti da ben 4 livelli:
- **MOF** (Model Object Facilities): abbiamo come entità la `Class` che possiede degli attributi, creandoci dei costrutti di programmazione.

- **UML** : che possiede la `Generalization` che sarebbe una relazione tra due classi una generale una più specifica.

- **User Model** (M2): noi stiamo modellando in questo livello che rappresenta la realtà 

Dove c'è `«instanceOf»` vuol dire che quel determinato oggetto è un'istanza di un altro oggetto, cioè DVD è istanza di classe che vuol dire? Cioè che DVD è una classe oppure `name:String «instanceOf» Attribure` sta a significare che è un'attributo.

#### 7.7.3 Polymorphism concept
>[!quote] Definiton
>Etimologicamente risulta un composto di "poli-" e "morphe" dal significato di "dalle molte forme". 

Nel nostro contesto indica la capacità di assumere differenti comportamenti dipendentemente dal contesto, per vedere più nel dettaglio consultarsi [[Design Pattern#3.4 Polymorphism|qui]].

# 8.0 Diagrammi di Interazione
---
>[!info] **Definizione**
>Il diagramma è utile per illustrare come gli oggetti in un dominio lavorano tra di loro. Il loro utilizzo è incentrato sul mostrare come gli oggetti interagiscono in un sistema software.

E' un diagramma comportamentale e dinamico che descrivono il comportamento delle classi, per poter raggiungere certi obbiettivi, aggiungendo informazioni al modello, cioè un metodo alla classe che reagisce ad un determinato messaggio dall'esterno.
## 8.1 What are them?
Sono dei diagrammi che servono a realizzare i [[UML#5.0 Use case base mechanism|casi d'uso]] e metterli in azione, cioè rappresentare ogni sequenza che fa un determinato durate la sua interazione con un'altro oggetto.

Esempio di diagramma  di sequenza.
![[SequenceDiagram Hotel.jpg]]

Nei diagrammi di interazione ci sono due famiglie di elementi fondamentali.

### 8.1.1 **LifeLine** (linee di vita)

>[!info] Definizione
>Le linee di vita rappresentano un elemento di una classe in una determinata interazione. 
>Questa lifeline è formata da:
>- **Nome**
>- **Tipo**
>- **Selettore**


Un diagramma di interazione è composto da diverse notazioni della linea di vita che dovrebbero essere disposte orizzontalmente nella parte superiore del diagramma.

>[!fail] Non si devono sovrapporre due notazioni della linea di vita.

Vediamo nel dettaglio ogni singolo elemento di tipo **LifeLine**:
 - **Oggetto**: sono elementi che interagiscono tra di loro nel sistema durante la sequenza.![[Screenshot 2026-01-18 at 12.08.19.png]]
- **Attore**: L'attore è colui che possiede il caso d'uso e viene rappresentato da uno stickman.![[Screenshot 2026-01-18 at 12.12.09.png]]
>[!warning] PER L'ESAME
>**Boundary - Entity - Controller** non sono concetti che devono essere definiti nella teoria(nella spiegazione della teoria), ma solo nell'esercizio di creare i sequence diagram.

- **Entità**: una linea di vita con un elemento entità rappresenta i dati del sistema (persistenza, DB, contenitore di dati).![[Screenshot 2026-01-18 at 12.15.32.png]]
  - **Boundary**:  una linea di vita con un elemento boundary indica un elemento di sistema/software in un sistema, per esempio le schermate dell’interfaccia utente, i Gateway di database o i menù con cui gli utenti interagiscono, sono confini (obbligatorie da metter per l'esame quando si fa l'esercizio sui sequence).![[Screenshot 2026-01-18 at 12.15.54.png]]
- **Controller**: una lifeline con un elemento di controllo indica un’entità o un gestore di controllo. Organizza e programma le interazioni tra i confini e le entità e funge da mediatore tra di loro (nel progetto sarebbero le service, cioè coloro che svolgono operazioni logiche).![[Screenshot 2026-01-18 at 12.19.23.png]]
- **Focus d'attivazione**: viene posto su una **LifeLine** per indicare che un elemento del sistema è attivo per quel lasso di tempo.![[Screenshot 2026-01-18 at 12.21.33.png]]
### 8.1.2  **Messaggi**

>[!info] Definizione
>Un messaggio sono delle interazioni che esistono tra due **LifeLine (linee vita)**.
![[Screenshot 2026-01-18 at 12.27.38.png|Visione generale dei messaggi nei diagrammi di interazione]]


I messaggi possono essere divisi in 3 macro categorie:
- **Chiamate**: di una specifica operazione.
- **Creazione - Distruzione**: di una determinata istanza (oggetto)
- **Invio di un Segnale**

Vediamo i messaggi che sono presenti nelle diagramma delle interazioni:
- **Messaggio Sincrono**: messaggio nella quale la lifeline che invia tale messaggio per poter inviare un'altro messaggio, deve aspettare la risposta dalla lifeline in cui ha inviato il messaggio.![[Screenshot 2026-01-18 at 12.43.28.png]]
- **Messaggio Asincrono**:  messaggio che invia una lifeline, ma che non deve per forza (pefffffforrrrzaaa *cit. Dario Moccia*) ricevere una risposta per poter inviare un altro messaggio, può anche inviare un altro messaggio di seguito.![[Screenshot 2026-01-18 at 12.49.45.png]]
- **Messaggio Di Ritorno**: messaggio di risposta da parte di una **LifeLine**, cioè che ha terminato l'elaborazione del messaggio e restituisce il resoconto del messaggio.![[Screenshot 2026-01-18 at 12.52.12.png]]
- **Messaggio di Creazione**: specifica che una **LifeLine**, sta creando un nuovo [[#8.1.1 **LifeLine** (linee di vita)|oggetto]] e dimostra che si sta aggiungendo un nuovo oggetto nella sequenza.![[Screenshot 2026-01-18 at 14.48.30.png]]
- **Messaggio Distruzione**: messaggio che distrugge un oggetto creato.![[Screenshot 2026-01-18 at 14.52.34.png]]
- **Messaggio Perso o Trovato**: ![[Screenshot 2026-01-18 at 15.12.26.png]]
- **Self Message**: invocazione del metodo della stessa classe, cioè una chiamata interna ad un metodo interno ;![[Screenshot 2026-01-18 at 15.14.10.png]]
- **Recursive Message**: stesso del self solo che il metodo chiamata internamente, richiama altri metodi al suo interno che fanno parte della stessa classe (ricorsione);

## 8.2 Diagramma di sequenza

>[!info] Definizione
>E' una forma di diagramma di interazione, utilizzato nella fase di analisi per far si che si possa rappresentare e descrivere un caso d'uso.

Questi diagrammi sono utili per **rappresentare degli scenari**, ma cosa sono gli scenari?

Gli scenari sono una sequenza di azioni che sono svolte all'interno di un contesto della quale si sono già svolte delle scelte.

>[!help] Diagramma di Interazione vs. Sequenza.
>
>NON ESISTE UNA DIFFERENZA SONO LA STESSA COSA.
>
>I **diagrammi di interazione**, spiegano come gli oggetti collaborano scambiandosi  dei messaggi per eseguire un determinato comportamento.
>
>Mentre invece i **diagrammi di sequenza** sono una specifica categoria di diagrammi di interazione, solo che sono distinti dall'ordine temporale in cui sono inviati i messaggi.

### 8.2.1 Frammenti Combianatori

>[!info] **Definizione**
>Sono dei rettangoli che inseriamo in diversi segmenti di vita di una lifeline e possono avere dei comportamenti che possiamo specificare, a seconda delle condizioni che impostiamo esternamente.

![[FrameSquare.png]]
Nella figura sopra vediamo un esempio di frammento combinatorio,  cioè un **Frame** che al suo interno può contenere degli operandi di interazione. Queste possono essere divise da una linea tratteggiata che specifica una diversa interazione con un'altra.
![[Screenshot 2026-01-18 at 15.35.54.png| Esempio di creazione di un ordine]]

---
**opt (optional)**

Esegue la sequenza **solo se la guardia è vera**.
![[Pasted image 20260118154317.png]]
Equivalente a un `if` senza `else`.

---
**alt (alternative)**

Rappresenta **rami alternativi mutuamente esclusivi**.
![[Pasted image 20260118154303.png]]

Simile a una struttura `if – else if – else`.

---
**loop**

Modella un **comportamento ripetitivo**.
![[Pasted image 20260118154329.png]]
La guardia indica **condizione di iterazione o di uscita**.

La sintassi dei loop è data da: **loop (min, max)** **[condizione]** Il significato è:
Esegui il loop un numero minimo di volte **min** continua l’esecuzione finché
condizione è vera per un numero massimo di **max** volte.
![[Pasted image 20260118155105.png]]

---
**break**

Interrompe l’interazione corrente **uscendo dal frammento che lo contiene**.

![Break enclosing loop if y>0.](https://www.uml-diagrams.org/notation/sequence-operator-break.png "Break enclosing loop if y>0.")

---
**ref (reference)**

Rimanda a **un altro diagramma di sequenza**.

Serve per **modularizzare** e riusare interazioni complesse.

---
**par (parallelo)**

Le sequenze contenute sono eseguite **in parallelo**.
![[Pasted image 20260118154626.png]]
L’ordine dei messaggi tra rami diversi **non è deterministico**.

---
**critical**

Sezione **atomica**: nessun’altra interazione può interferire.
![[Pasted image 20260118154811.png]]
Usata per evitare **race condition**.

---
**seq (sequenzializzazione debole)**

Mantiene l’ordine **solo all’interno dello stesso ramo**.
![[Pasted image 20260118155511.png]]
Tra rami diversi l’interleaving è possibile.

---
**strict**

Impone un **ordine totale** dei messaggi.
![[Pasted image 20260118155602.png]]
Nessuna interleaving è consentita.

---
**neg**

Specifica **comportamenti non validi o proibiti**.
![[Pasted image 20260118155900.png]]
Specifica semplicemente che ciò non deve accadere.

----
**ignore**

Specifica i **messaggi che vengono ignorati durante l'interazione**
![[Pasted image 20260118160128.png]]
In questo esempio vengono ignorati i messaggi `get` e `set`, sono ammessi ma **non rilevanti**.

---
**consider**

Indica che **solo i messaggi elencati sono rilevanti**.
![[Pasted image 20260118160330.png]]
Tutti gli altri, se vengono inseriti saranno implicitamente ignorati.

---
**assert**
Definisce l’**unico comportamento corretto** in quel punto.
![[Pasted image 20260118160503.png]]
Qualsiasi altra sequenza è da considerarsi **errata**.

---



**Frammento Combinato** cambiamento di comportamento in base al controllo che facciamo internamente nel messaggio (con delle condizioni, ma non è sempre usato per questo), si eseguono uno delle operazioni dell'alt non tutti in simultanea.
![[FrammentiCombinatoriSequenziali.png]]

# 9.0 Activity Diagram
--- 
>[!info]
>Diagramma comportamentale che posso rappresentare come il sistema evolve nel tempo. Cioè il comportamento che ha il sistema e quali attività vengono svolte in base alle decisioni che vengono scelte.

Viene usato maggiormente per modellare **processi aziendali** (operazioni di creazione di un prodotto, aggiunta di un prodotto), **UC complessi** oppure si possono utilizzare per rappresentare gli **algoritmi** (esempio dei flowchart).

![[Pasted image 20260117193615.png|Esempio di Activity diagram]]

Ogni processo che opera viene associato ad un'**attività**, ma che cos'è un'**attività**?

>[!info] **Attività**
>L'attività è un contenitore che contiene i diagrammi principali e ci sono le funzionalità di alto livello. Ogni attività possiede al suo interno dei **nodi** e **archi**, questi hanno un flusso di lavoro completo che produce un risultato.![[Screenshot 2026-01-18 at 10.41.52.png]]

Semplicemente il contenitore dell'intero processo, nella quale troviamo come detto precedentemente oltre a degli archi anche dei **nodi**, quest'ultimi sono di 3 tipologie.

Vediamo in una prospettiva più ampia gli elementi dell'Activity Diagram.
![[Pasted image 20260118115105.png]]
## 9.1 Nodi

I nodi sono principalmente di 3 categorie:
### 9.1.1 Nodi Azione

>[!info] Definizione
>Operazione elementare che si svolge all'interno dell'attività, sarebbe un'operazione atomica.

Questo è un esempio di nodo azione:
![[Screenshot 2026-01-18 at 09.57.50.png]]

> [!question] **Cosa può fare il nodo azione?**
Il nodo azione è in grado di chiamare altre attività, dei comportamenti oppure invocare delle operazioni.

>[!question] **Come si attiva il nodo?**
>Il nodo si attiva se e solamente se una di queste due condizioni sono vere:
>- Esiste un **token** in un arco entrante
>- Se le **pre-condizioni del nodo sono soddisfatte**.

>[!question] Come può uscire il nodo?
>Il nodo azione può terminare la sua operazione se dopo aver completato le sue operazioni interne, verrà valutata la **post-condizione**.

Dopo la valutazione della **post-condizione** (che è presente all'interno del nodo), ci sono due scenari che possono avvenire:

- ✅ `true`:  condizione vera il nodo azione genererà nuovi token, che verranno passati ad ogni arco in uscita.
- ❌`false`: non si generano token, cioè non vengono emessi quest'ultimi.

> [!abstract] **Tipologie di nodo azione**
> Le tipologie di nodo azione sono:
> - **Azione chiamata:** invoca un’altra attività o operazione
> - **Invia segnale**: manda un evento asincrono
> - **Accettazione evento:** restano in attesa di un'evento
> - **Espressione temporale**: dipendono dal tempo

### 9.1.2 Nodi Controllo

>[!info] **Definizione**
>Sono dei nodi che gestiscono il flusso di controllo di un'attività, questi nodi **possono collegarsi tra le varie attività** e decidono l'ordine di esecuzione di quest'ultime. Indicano in che ordine le attività devono essere svolte.
>

Questi nodi **non svolgono delle operazioni interne**, ma sono solo necessari a gestire le attività e il flusso delle azioni, tramite delle scelte, dei cicli oppure dei parallelismi.

I nodi controllo sono i seguenti.
![[Screenshot 2026-01-18 at 10.44.41.png]]
Per vedere meglio l'immagine, cliccate [qui](https://www.ibm.com/docs/it/rsas/7.5.0?topic=diagrams-control-nodes).

### 9.1.3 Nodi Oggetto

>[!info] **Definizione**
>Sono dei nodi che definiscono **i dati o gli oggetti** presenti all'interno di un'attività.

Questi nodi sono delle istanze dei *classificatori*, cioè possono esistere in un determinato lasso temporale

>[!example] Esempio 
>Il Nodo Oggetto `Order` viene creato dopo eseguito il Nodo Azione `Fill Order` e termina la sua esistenza quando si passa all'azione `Review Order`
>![[Pasted image 20260118105714.png]]

I nodi oggetti sono dei [buffer](https://www.perplexity.ai/search/buffer-for-data-9LiIBtgnRc2bTlmOId3BTw#0)
# 10.0 Petri Nets
>[!info] Definizione
>Ci permette di rappresentare sistemi concorrenti, **asincroni**, **distribuiti**, **paralleli**, **non deterministici**, e/o stocastici, composta da una tupla:
> $$ < P, T, F, W, M0> $$

Descriviamo singolarmente gli elementi della tupla:
- $P$: sono chiamate **piazze** ed è un'insieme finito di stati che può avere il sistema. Ogni piazza può possedere un numero di **token**, cioè una quantità di elementi in input.
- $T$: sono le **transizioni**, sono degli eventi che possono attivarsi nel sistema, se e solamente se ci sono abbastanza token in input.
-  $F \subset \{P \times T \} \cup \{T \times P\}$: viene chiamato **relazione di flusso della rete di petri**, sarebbe un sottoinsieme del prodotto cartesiano tra le piazze e le transizioni.
- $W: F\to \mathbb{N}^{+}$: è una funzione che associa ad ogni flusso un valore (numero naturale positivo diverso da 0).
- $M_{0}: P \to \mathbb{N}$: si chiama **marcatura** ed indica lo stato iniziale della rete di petri.

>[!warning] **Nota importante**
>Un elemento può essere una piazza $P$ oppure una $T$ transizione, non può essere entrambe.

![[Pasted image 20260118113317.png| Elementi della rete di petri]]
## 10.0 Component diagram
---
Vengono riportate informazioni sulle macro componenti del software.
Si vengono a creare da un sistema principale in **sottosistemi**, che sono indipendenti tra di loro e che hanno obbiettivi ben definiti.

Ogni interazione tra i **sottosistemi** avvengono tramite l'utilizzo di interfacce, che vengono definite sulla base della composizione scelta che se stanno implementando un'interfaccia dovranno mantenere fede al loro scopo.

### 10.1 Interface

Le interfacce seguono il concetto della programmazione ad oggetti, ma in UML possiede una semantica a differenza della **OOP**, le informazioni semantiche sono come ad esempio descrizioni testuali o linguaggi che forniscono costruttori per la logica.

- Operazioni 
- Attributi
- Associazioni
- Vincoli
- Stereotipo
- Valori Etichettati
- Specifica del **Protocollo**
![[InterfaceView.png]]

### 10.2 Interface and Inheritance
![[interfaceEreditary.png]]

### 10.3 Component
Identifica un'insieme di funzionalità molto coese e specifica precisi servizi offerti e richiesti (interfacce). In generale una granularità tale per cui l'elemento non potrebbe costruire sistemi a se stante i.e un componente è fatto per essere **composto**, rappresentando il **sistema in macro componenti**.
![[ComponentDiagram.png]]
é possibile mostrare l'interno di un componente e gli elementi responsabili dei servizi offerti e richiesti.
![[componentRapresentatio.png]]
### 10.4 Advantages and Disadvantages of the interfaces
# Reference
--- 
 [UML](https://www.tutorialspoint.com/uml/index.html)

[^1]: Un **requisito funzionale** è un'affermazione di come un sistema deve comportarsi. Definisce cosa deve fare il sistema per soddisfare le esigenze o le aspettative dell'utente. I requisiti funzionali possono essere considerati come caratteristiche che l'utente rileva. [source](https://visuresolutions.com/it/blog/richieste-funzionali/)
 
[^2]: **metodologia** è la disciplina che studia l'evoluzione (teorico-pratica) del lavoro di ricerca sulla base del [metodo scientifico](https://it.wikipedia.org/wiki/Metodo_scientifico "Metodo scientifico")

[^3]: **modello concettuale**: si chiama così perché nasce con lo scopo di rappresentare i concetti (classi e associazioni tra classi) ed ha lo scopo di esprimere il significato di termini e concetti usati dagli esperti del dominio per discutere il problema, e di trovare le giuste relazioni tra concetti differenti

[^4]:  sono quei metodi che si possono condividere solo fra le classi che fanno parte della stesso gruppo o [[UML#Package|package]] 

[^5]: parametro che non cambia il suo stato dopo la sua invocazione, cioè lo stato può essere vero prima e dopo la sua esecuzione

[^6]: **interdipendenza**: Rapporto di intima connessione e di reciproca dipendenza tra più cose, fatti, fenomeni, ecc.: