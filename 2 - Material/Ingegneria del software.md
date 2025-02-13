---
share_link: https://share.note.sx/f9n2xdjq#y9OhafJT09gABPLqtR06sU/q+X6DDNx5yc02Ani0cCQ
share_updated: 2025-02-07T13:17:30+00:00
---
2024-10-10 10:28

Status: #baby 

Tags: [[Programming]], [[Software Engineering]]

---
# Ingegneria del software

- [0.0 Introduzione](#0.0%20Introduzione)
- [1.0 The 4's P](#1.0%20The%204's%20P)
- [2.0 Ciclo di vita di un processo](#2.0%20Ciclo%20di%20vita%20di%20un%20processo)
- [?.? Processo Unificato](#?.?%20Processo%20Unificato)
- [Inception (Avvio)](#Inception%20(Avvio))
- [Elaboration (elaborazione)](#Elaboration%20(elaborazione))
- [Construction (costruzione)](#Construction%20(costruzione))
- [Transition (transizione)](#Transition%20(transizione))
- [3.0 Ingegneria dei requisiti](#3.0%20Ingegneria%20dei%20requisiti)
- [4.0 Engineering of requirement](#4.0%20Engineering%20of%20requirement)
- [8.0 Activity diagram](#8.0%20Activity%20diagram)
- [9.0 Quality of the requirements](#9.0%20Quality%20of%20the%20requirements)
- [10.0 Check the software validation](#10.0%20Check%20the%20software%20validation)

## 0.0 Introduzione
---
Ora andremmo a dare dei concetti (potrebbero servire come no idk) che sono la base dell'ingegneria del software, spiegandone cosa sono in dettaglio:

- **Software**: è ==programma che specifica le istruzioni che un calcolatore dovrà eseguire al fine di raggiungere uno scopo== Identificandone anche tutti i documenti che lo descrivono e che sono stati messi a punto durante le varie fasi della produzione del sistema

- **Ingegneria del software**: disciplina che studia le varie fasi e processi che portano alla produzione di uno specifico software. Consiste nell’applicazione di un approccio sistematico, disciplinato e quantificabile nello sviluppo, funzionamento e manutenzione del software.
  %%ci diventi dopo aver studiato come un'animale%%
- **Ingegnere** : ==colui  che ha strumenti e competenze matematiche per descrivere le caratteristiche del prodotto, separatamente da quelle del progetto==. Si appoggia più sull’esperienza e sul giudizio personale che su tecniche matematiche.
## 1.0 The 4's P
---
Le quattro 4 o (detto in inglese per fare il figo four's P) sono un insieme di componenti o persone che sono presenti quando si viene a creare un progetto per la prima volta e sono:

- **People – Project stakeholders**: nello sviluppo di un software complesso sono coinvolte molte persone (Business e Project Management, Development Team,Customers, End Users);

- **Product – La [[Programming Knowledge#^8837ca|codebase]] e relativi artefatti:** è l’obbiettivo finale e risponde alla domanda “cosa si vuole costruire?” di fatti l’obiettivo dell’IDS è quello di fornire metodi e strumenti affinché la qualità di ogni artefatto risulti massima e comprensibili per future elaborazioni. ==L’obiettivo dell’ingegneria del software non è quello di produrre documentazione!==

- **Project – le attività messe in campo per la produzione del prodotto:** sono tutte quelle attività da svolgere per realizzare il prodotto finale. Oltre  alla comunicazione rivolta al consumer e allo sviluppatore e l’ingegneria dei requisiti, ovvero lo studio di fattibilità, elicitazione[^1], specifica, analisi e validazione dei requisiti.

- **Process – come procedere nella produzione di un software:** definisce quali sono le attività da mettere in atto nello sviluppo di un prodotto software e come organizzarle. L’Ingegneria del Software ha definito diversi processi dalle diverse qualità adatte più o meno bene ai diversi ambiti di sviluppo, che vedremmo durante questo documento uno ad uno.

## 2.0 Ciclo di vita di un processo
---
Quando si parla di ciclo di vita di un processo, si va nel dettaglio e si parla prima della definizione di _ciclo di vita_ di un prodotto, esso ==viene definito come una serie di stati che sono stati compiuti da un ente(o prodotto) nella sua vita a partire dalla sua nascita, fino alla dimissione (o se vogliamo dire rimanendo in tema "morte")==.

Il _processo di sviluppo_ invece viene definito come tutti quei passi che vengono scelti ed adottati durante il ciclo di vita di un prodotto, ciò ==si intende che strategie si sono usate per compiere determinate azione== e chi deve fare cosa per poter raggiungere tali obbiettivi.

### 2.1 Parti in causa
Quando si viene a sviluppare o ad usare un software, ci sono molte persone che partecipano al loro concepimento ed è fondamentale tener conto dei loro ruoli, esigenze e rapporti reciproci all'interno della progettazione.

Per questo motivo è fondamentale che l'ingegnere del software, comprenda l'ambiente in cui si viene a sviluppare il software e capire dove viene applicato quest'ultimo.

I ruoli che andremmo ad elencare sono principalmente 4:

- **Sviluppatore**: colui che fa parte del processo di sviluppo del software, come ad esempio programmatori, analisti o collaudatori.
- **Produttore**: viene intesa come un'organizzazione che produce un software, lo *sviluppatore* è colui che fa parte di tale organizzazione (cioè dipendete del produttore).
- **Committente**: persona o organizzazione che richiede al *produttore* che software bisogna creare.
- **Utente**: persona che utilizza il software.

### 2.2 Specifica e Implementazione
Dal punto di vista del progettista, cioè colui che viene a svolgere un determinato progetto, ha diversi _requisiti_, che sono questi?
Essi sono degli obblighi imposti dall’esterno (e quindi facente parte della specifica) mentre l’implementazione svoltasi è il risultato di una serie di scelte che vengono fatte ed applicate.

>[!warning] N.B
> La ***specifica*** sarebbe un insieme che contiene una serie di requisiti, questi ne descrive in dettaglio le sue caratteristiche, spiegandone il suo utilizzo e in che sistema fa parte.
> In definitiva ricordiamo che la _specifica_ ci dice ==cosa dobbiamo fare per creare il nostro sistema==, invece l'implementazione ci dice ==come si andrà a metter mano al prodotto==
> 

### 2.3 Process Perspective
Il processo di sviluppo che abbiamo precedentemente discusso, possiede diverse tipologie di prospettive, che queste conducono alla produzione di un artefatto finale, tramite l'esecuzione di diverse attività:

- ***Activities Perspective***: definisce di quali attività si compone un processo;

-  ***Workflow Perspective***: sono le relazioni temporali tra le attività che devono essere svolte e le possibili condizioni necessarie per verificare e poter avviare un’attività;

-  ***Data-flow Perspective***: definisce quali sono gli artefatti che devono essere prodotti dalle varie attività e quelli che verranno creati al termine del progetto.

- ***Role/Actions Perspective***: definisce i ruoli necessari nell’organizzazione al fine di portare avanti un progetto in accordo al processo nonché le responsabilità di tali ruoli in relazione alle attività da compiere.
### 2.4 Attività del processo di sviluppo
Ogni prodotto industriale ha un ciclo di vita che, a grandi linee, inizia quando si manifesta la necessità o l’utilità di quest'ultimo e prosegue con l’identificare i suoi requisiti, il progetto, la produzione, la verifica, e la consegna al committente (utente finale).

Tipicamente il nostro ***processo di sviluppo*** ==è un modo di organizzare le attività costituenti il ciclo di vita, consiste nell'assegnare risorse (non so cosa intende il ragazzo con risorse qui?) alle varie attività e fissarne le scadenze==. 

Questi si distinguono in base alla organizzazione delle differenti attività dello sviluppo (workflow perspective) e da documenti/modelli che questi  producono (data-flow perspective):

1. ***Comunicare***: si intende nel ==capire cosa deve fare il sistema software== e quali sono i vincoli a cui deve sottostare il sistema. 
   L’ingegneria dei requisiti prevede 4 task principali:
   
	- **studio della fattibilità**: comprendere le funzionalità fondamentali che il sistema deve implementare; 
	  
	- **elicitazione dei requisiti e analisi**: è il processo di raccolta e identificazione dei requisiti di un sistema software o di un prodotto i requisiti sono fondamentali perché definiscono cosa  deve fare e come deve comportarsi un sistema, per soddisfare le esigenze degli utenti;
	
	- **specifica dei requisiti**: i requisiti raccolti vengono formalizzati e descritti in dettaglio in un documento; 
	
	- **validazione dei requisiti**: è il processo di conferma che i requisiti specificati per un sistema software soddisfino effettivamente le esigenze degli utenti e degli stakeholder.
2. ***Modellazione***: una fase che  consiste nel creazione una descrizione dell'entità del software (modello) che deve essere sviluppato, la sua architettura i dati che devono essere scambiati, i componenti che fanno parte del sistema, le interfacce tra i vari elementi del sistema e gli algoritmi utilizzati.
   
   Esistono ben due approcci alla modellazione del software:
   - **metodologia agile**: si concentrano sulla flessibilità, sulla collaborazione e sulla risposta rapida ai cambiamenti;

   - **metodi strutturati**: come il modello a cascata, seguono un approccio più sequenziale e gerarchico allo sviluppo.

3. ***Costruzione:*** fase della creazione del codice e del sistema basandosi principalmente sui modelli definiti nelle varie attività precedenti (cioè quelle di modellazione).
   
4. ***Verificare e validare:*** verificare che il sistema soddisfi i requisiti e le esigenze del committente/utente (ispezione del codice o testing).
   
5. ***Manutenzione:*** attività messe in atto sul software già rilasciato per dei motivi come interventi correttivi di problemi presenti, perfettivi per l’aggiunta di funzionalità e adattivi per la portabilità del software.
### 2.5 Modelli di processi
Lo sviluppo di un software avviene attraverso la costruzione di una serie di **modelli**.

Un **modello** si intende come una descrizione astratta di un sistema e viene utilizzato principalmente per studiarne alcune caratteristiche che saranno necessarie per conseguire un certo scopo. Ogni sistema dovrà essere rappresentato da diversi modelli, ognuno dei quali rappresenterà lo stesso sistema, ma in diversi aspetti, con livelli di dettaglio differenti. 

I modelli che andremmo a discutere saranno i seguenti:
- [[#2.5.1 Modello a Cascata|Modello a Cascata]]
- [[#2.5.3 Modello Evolutivo|Modello Evolutivo]]
- [[#2.5.4 Modello Iterativo|Modello Iterativo]]
- [[#2.5.5 Model Driven Development|Model Driven Development]]
#### 2.5.2 Modello a Cascata
Il **modello a cascata** consiste nell'==esecuzione a sequenza dei diversi passi== dello sviluppo software, dove ad ogni passo si viene a produrre dei **semilavorati** che sono dei documenti inerenti al processo o degli elaborati del codice sorgente o compilato, che verranno rielaborati e modificati nei passi successivi.

Nella prima fase si va a creare i requisiti che il software dovrà soddisfare e un piano temporale dettagliato. Poi si prosegue con la modellazione e viene creato un progetto completo del software, si passa alla programmazione, alla quale seguono verifica e rilascio del software. 

La particolarità di questo modello è che la **conclusione di una fase, implica l'inizio di quella successiva** e che la **produzione dei semilavorati sia unidirezionale**, che cosa vuol dire? Si intende che alla conclusione di una fase i risultati di quest'ultima sono il punto di partenza di quella successiva e pertanto non possono influenzare passi precedenti.

![[waterfall-model.png]]
In questo modello che vediamo in figura,  i requisiti sono definiti inizialmente e non sono più modificabili se si passa ad una fase successiva del modello, questo **comporta delle problematiche**.

Se si vengono a scoprire degli errori od omissioni nel progetto o nelle specifiche, si necessita ripetere le fasi precedenti e modificare i semilavorati che sono stati prodotti fino ad ora.

Questa problematica rende il **modello inefficiente** e viene associato ad una **percentuale elevata di fallimenti**, per via del fatto che le specifiche definite inizialmente non vengono più modificate una volta stabilite.
#### 2.5.3 Modello Evolutivo
Il modello cerca di prevalere su quello a cascata, discusso in precedenza e questo come?

Attraverso l'utilizzo di **prototipi** cioè delle versioni semplici di un sistema informativo, con la quale possiamo sperimentare diverse funzionalità. 

Ogni prototipo che si viene a creare, viene **valutato** e il risultato di tale valutazione, andrà a determinare il passo successivo finché non si arriverà alla creazione del prodotto, adottandosi alla richiesta finale del cliente, l'elaborato risulta completo e soddisfa ogni requisito, almeno fino a quando non viene richiesto un futuro update.

Questo comporta a diverse conseguenze:

- **Organizzazione del sistema poco efficiente** a causa dei continui cambiamenti.
- **Difficoltà nella manutenzione** del prodotto nel tempo.

Il nostro **prototipo** è una rappresentazione dell'ideale applicazione, che andremmo a creare, non sarà completa di tutte le funzionalità che dovremmo implementare, ma per l'analisi dei requisiti è importante valutare che fine farà il nostro prototipo:

- Se il prototipo piace allora consideriamo l'opzione di lavorarci sopra ampliandolo e perfezionandolo nel tempo **prototipo evolutivo**

- Oppure possiamo optare di scartarlo e creare il prodotto da zero ex-nuovo (seguendo le tracce del prodotto scartato) **prototipo throw-away**
#### 2.5.4 Modello  Iterativo
#### 2.5.5 Model Driven Development

## ?.? Processo Unificato
---
Lo **Unified Process (UP)** è un ==processo iterativo standardizzato per lo sviluppo del
software per la costruzione di sistemi orientati agli oggetti== questo è un 
processo guidato sia dal rischio che dai casi d'uso ed incentrato sull'architettura (come [[UML|UML]]), la baseline sono gli artefatti prodotti da un processo di sviluppo.

>[!question] Domanda d'esame
>Q: Quali sono le caratteristiche del processo unificato?
>A: Guidato dai casi d'uso.

L’arco temporale del processo di sviluppo è suddiviso in **quattro fasi successive** 

>[!quote] Definition
>**Fase:** periodo di tempo in cui dedichiamo gli sforzi per raggiungere gli obbiettivi.

Ogni fase produce dei semilavorati chiamati,
**Milestones (pietra miliare):** cioè insieme di obbiettivi delle fasi, definendo il ciclo di vita del progetto.

Ogni fase è suddivisa in un numero variabile di iterazioni e nel corso di ciascuna
iterazione possono essere svolte tutte le attività richieste, anche se, alcune attività
possono essere predominanti ed altre possono mancare.

Qui troviamo il peso di ogni flusso di lavoro.
![[UnifiedProcess.png]]
Attività saranno poste in ordine di importanza dall'alto quella più importante a quella meno.
![[DettaglioDelGrafico.png]]
- **Fase d'avvio**: capire se possiamo cominciare il progetto oppure no
- **Fase elaborazione**: obbiettivo principale è quello creare un'architettura stabile del sistema, avendo anche un piano per la fase successiva.
- **Fase Transizione:** portare alla versione di prova in quello di rilascio
- **Fase di costruzione:**

--- start-multi-column: ID_9abd
```column-settings
Number of Columns: 4
Largest Column: standard
```

## Inception (Avvio)

--- column-break ---

## Elaboration (elaborazione)
--- 

--- column-break ---
## Construction (costruzione)
--- 

--- column-break ---

## Transition (transizione)
---




--- end-multi-column


Qui sono rappresentate nel dettaglio ogni fase di sviluppo dell'Unified Process e sono:
- **Requisiti (requirements)**: raccogliere i requisiti fondamentali, basandosi sul sistema che stiamo analizzando e sulla dimensione della complessità, definendo i requisiti (use case).

- **Analisi:** (creare un piccolo prototipo dei costi dello sviluppo).

- **Design:** finire il modello del design

- **Implementazione:** creare le base dell'architettura, baseline eseguibili e far in modo che soddisfino i casi d'uso che si presentano.

- **Test:** 
**Business case**: capire come vendere il software e dove frutta denaro.

## 3.0 Ingegneria dei requisiti
--- 
E' la disciplina che serve per **comprendere cosa il sistema debba fare**, con le sue **proprietà essenziali** e i vincoli che deve rispettare. La fase dello scoprire, analizzare, documentare, validare quello che facciamo interagendo con l'utente e  i requisiti sono attività della disciplina dell'**ingegneria dei requisiti**

Le tecniche che utilizziamo li utilizziamo in base a quello che dobbiamo fare
### 3.1 Software Intensive System
Funzionalità offerte dai sistemi software, sono due macro categorie (ci concentreremmo più sulla prima):
- **Information system**: sistemi gestionali che manipolano e erogano informazioni, dove il dato viene inserito e manipolato, computazione eseguito sui compilatori standard;
  
- **Embedded Software-intensive System**: interagisce con il mondo fisico, acquisendo dati da quest'ultimo, parte di questi sistemi non sono eseguiti su general purpose, ma su sistemi embedded. 
### 3.2 Challenge in the SIS
La complessità dei sistemi software è sempre crescente, necessitando sempre di nuovi approcci allo sviluppo, dove gli aspetti legati allo sviluppo.
_to be completed_...

### 3.3 Typical problems inside the SIS
Questa è una lista dei tipici problemi che si possono scontrare tipicamente.
![[List-of-problem.png]]

### 3.4 What is a Requisite?
>[!info] Definiton
>![[DefinitionOfRequirement.png]]
>

### 3.5 Type of Requisite
Questa dipende dal destinatario del requisito e dal focus che si persegue nell'analisi e sono:
- Si concentrano su ==chi è il **destinatario del requisito**==:
  
	- **Requisiti utente**: saranno scritti in modo che l'utente lo possa capite, descrivendo cosa fa il sistema in modo comprensibile (come ad esempio l'accesso al sistema oppure che il sistema calcola l'iva ), alto livello di astrazione usando un linguaggio naturale;
	
	- **Requisiti di sistema**: passo ulteriore a quelli dell'utente, non sono più gli utenti i destinatari, ma i progettisti o programmatori, utilizzando termini tecnici e precisi, spiegando il meccanismo del sistema, come ad esempio dopo 3 volte di tentativo di login si blocca il sistema;
	  
- Altri tipi ==sono in base alle **carattere del requisito**== e sono:
	- **Requisito funzionale**:  ha l'obbiettivo di descrivere una relazione input-output (fammi una somma di due numeri), chiede di creare una somma fra due numeri;
	  
	- **Requisito qualitativi**: descrive come il sistema soddisfa il **requisito funzionale** (fammi una somma di due numeri in due secondi), soddisfa la richiesta in un determinato tempo cioè due secondi.
	
	- **Vincolo**: sono un modo particolare per vincolare come deve essere sviluppato un software;

- Altra categoria sono l'**origine dei requisiti** 

### 3.6 How specify system requirements?
Ci possono essere diverse tecniche e specifiche per definire i requisiti di sistema:
- **Informale**: requisito di sistema con semantica ben definita, utilizzando un linguaggio naturale comprensibile all'utente;
  
- **Semi formale**: linguaggio formale, utilizzando delle grafiche per rappresentare concetti, con la semantica non sempre definita (ad esempio [[UML]] è un linguaggio semi-formale);

- **Formali**: sintassi e semantica son ben definiti. 
  
L'uso di una tecnica invece che un'altra dipende dal metodo utilizzato e il contesto, più vado nel formale più mi costa di tempo e denaro, per poter riflettere su cosa fare o no, verificando delle proprietà che non sempre abbiamo tempo di verificarne tutte. 

### 3.7 Ambiguity in the natural language
Ci possono essere diverse ambiguità che sono presenti nel linguaggio che abbiamo, che posssono impattare la specifica dei requisiti:

- **Lessicale**: termini che possono avere più significati, son polisemici, capire una cosa per un'altra.
  
- **Ambiguità sintattica**: la frase in questo caso ha più di un significato sintattico, errori di punteggiatura o di posizionamento di soggetto verbo e complemento.

- **Ambiguità semantica**: la frase possiede più interpretazioni e non una singola.

- **Pragmatica:** interpretazione che dipende dal contesto.
### 3.8 Qualitative Requisite
![[QualitativeRequirement.png]]
### 3.8 Restriction Requisite

>[!info] **Definition**
>Un determinato vincolo è un requisito  organizzativo che restringe il campo **TODO**. 
### 3.8 Requisite Domine

>[!info] **Definition**
>Un requisito di dominio è quello che deriva direttamente dallo specifico **dominio e o contesto applicativo**.

Molto difficile da far emergere, e cercare di trovarli e specificarli all'interno dell'analisi.

## 4.0 Engineering of requirement
--- 
Come trasformare le idee del comittente in qualcosa di concreto.

### 4.1 Factibility Study
**Studio preliminare** per capire se il sistema è conveniente costruirlo oppure no, facendo emergere le necessità e capire se continuare o meno, ci sono delle domande che vengono poste per questa attività:
%%METTERE LE DOMANDE%%

### 4.2 Elicitation  of analysis of requirement
Sbagliato chiedere all'utente cosa gli serve, il primo passo è identificare gli **"stakeholder"**
![[DifficultyOfRequirement.png]]
L'elicitazione viene influenzata alle caratteristica dei processi cognitivi umani, portando in considerazione i processi mentali di:
- **rimozione**
- **distorsione**: interpretazione errata di un concetto, distorta da preconcetti dell'utente;
- **generalizzazione**: semplificare il sistema, riducendo le statistiche.
Attenzione ai termini: **tutto, ogni, sempre, mai, nessuno, niente**.

### 4.3 Find of the requirements
Identificare i punti di vista, per capire e **classificare gli attori del nostro sistema** e possono essere 3 tipi **diretto**, **indiretto** e di **dominio**:

- Punto di vista **diretto**: chi interagisce direttamente con il sistema;
  
- Punto di vista **indiretto**: chi non ci interagisce, ma è interessato al sistema e il suo comportamento;
  
- Punto di vista di **dominio**: persone/attori che sono esperti del dominio o detto sistema che stiamo creando.
### 4.4 System and Actors
Attore è il ruolo che un'entità assume quando interagisce con il sistema, un'entità può **possedere più ruoli contemporaneamente**, che possono essere sistemi esterni oppure delle persone.

### 4.5 Classification of the actors
Ci sono altri attori che sono identificati con:
%% ELENCO DEGLI ATTORI %%
### 4.6 Finding the requirement: technique
Trovare gli attori dei nostri sistemi tramite l'utilizzo di:
- [[#4.6.2 Interview|Interviste:]] maggiore dettaglio nel seguito;
- [[#4.6.7 WORKSHOP|Workshops]]: maggiore dettaglio nel seguito;
- **Focus groups**: ==approfondimento aspetti del sistema che non sono chiari==, non avendo una chiara conoscenza del dominio, coinvolgendo esperti, focalizzarsi sullo specifico aspetto del dominio che non conosciamo.
- **Osservazione o etnografia:** derivare dei requisiti dalle persone che lavorano sul campo del nostro dominio, osservando come operano e i processi che seguono.
- **Questionari**: realizzare dei form per raccogliere informazioni da specifici stakeholder.
- Perspective-based reading: identificare tramite documenti specifici dettagli che non sono stati visualizzati in precedenza, svolgendo alla lettura approfondita.
#### 4.6.1 Aspect to define for each technique
Ogni tecnica segue dei passi che devono essere fornite nel dettaglio come:
- Preparazione
- Esecuzione
- Follow-up
  
Caratteristiche dell'approccio che utilizziamo possono essere descritte in questo modo:
- Benefici
- Complessità
- Fattore critica di sucesso
#### 4.6.2 Interview
Non prendere l'intervista come un esame universitario con domanda e risposta e porre sul giudizio la persona, ma mettere l'attore in una condizione di **massimo agio**, in modo che sia naturale nelle risposte.
**Non chiedere mai all'attore che cosa ha bisogno**, non sa mai cosa vuole l'attore, ogni intervista ha diversi momenti:

- **Interviste "standard"**: prepare le domanda in modo che risponda in modo preciso, proponendo il punto di vista dell'attore nel rispondere alla domanda.
  
- **Interviste a domande aperte**: permette di esplorare il concetto ampliando il discorso, però ci possono essere compromessi, basati sul fatto che quella persona andrà fuori contesto.

- **Intervista non strutturate**: procedere l'intervista con una discussione che viene guidato dall'intervistato.

Il risultato dell'intervista dipende dall'intervistatore (cioè colui che svolge l'intervista) che deve essere **bravo nell'ascoltare**.

#### 4.6.3 Prepare the interview
- **Definire l'obbiettivo dell'intervista:** chiarire la necessità dei specifici attori, o il comportamento del sistema in relazione alle specifiche richieste.
  
- **Selezionare il partecipate**: capire chi intervistare e se è giusta come persona da fare le domande o no.
  
- **Selezionare il luogo dell'intervista:** il luogo migliore sarebbe il posto dove si lavora che rende semplice la comunicazione, situazione rilassata, che non venga disturbata da qualcuno o da qualcosa come dispositivi elettronici.

- **Define the questions**: Utile avere delle informazioni sull'intervistato.

#### 4.6.4 Execution of the interview
- **Apertura:** introdurre l'obbiettivo e la motivazione di tale intervista, rendendola importante per il suo tempo che sta sacrificando per voi.

- **Conduzione**: portare dei fogli o dei materiali che siano utili per l'intervista.

- **Chiusura:** fare un sommario dell'intervista e delle parti clue. 

#### 4.6.5 Follow-up of the interview
- **Rielaborare**: riorganizzare il materiale che si possiede e definiti nel dettaglio dei requisiti, scenari e modelli che definiscono il sistema.
%% TO DO INSERIRE ALTRI DUE VANTAGGI%%
#### 4.6.6 Benefit of the interview
Le interviste sono molto importanti per ottenere e capire la **necessità del committente**. Queste però **non sono strumenti per fare innovazione  e creare dei requisiti nuovi e innovativi**

#### 4.6.7 Workshop
Lavoro di gruppo che porta a risultati eccellenti, ma prima va scelta la tecnica accessoria che verrà utilizzata per iniziare un workshop.

#### 4.6.8 Workshop preparation 
La preparazione consiste nel:
- **Definire degli obbiettivi**
- **Definire tecniche da applicare e risultati attesi**: Brainstorming, KJ method, Discussion, definizione iterativi di scenari, organizzazione di sottogruppi.
- **Scelta dei partecipanti, invito e accordo sugli obbiettivi**
- **Scelta del luogo**
- **Identificare il moderatore**
#### 4.6.9 Workshop execution
- **Apertura:** descrive l'obbiettivo del workshop, le tecniche che saranno utilizzate, l'agenda, le regole 
%% Complete with other stuff %%

#### 4.7.0 Workshop follow-up
Viene creato un 

#### 4.7.1 Workshop benefits and costs
Ottimo per l'innovazione con molte persone c'è più possibilità di innovare, molto costoso per quando riguarda di organizzazione e dei partecipanti.
#### 4.7.2 Workshop factor of success
%%Complete with the factor of success%%

### 4.8 KJ- Method
permette di far emergere i requisiti a partire da un gruppo di persone allo stesso tempo, composta da due fasi:
- **Riflessione individuale**
- **Lavoro di gruppo**

### 4.9 Document to define the requirements
Il documento è un formato strutturato per ogni requisito e sono di varia natura:
- **ID**: identificativo unico - serve per una questione di gestione del documento.
- **Nome:** Nome mnemonico tipicamente 
  **azione- nome**, esempio autenticazione-utente, non come caso d'uso ma come specifica, composta anche di una:

	- **Frase** con questi verbi "Deve/Dovrebbe/Può/Potrebbe", chiamato anche MoSCoW principle
	  esempio:
	  `Il sistema dovrebbe fare qualcosa`
	  Usarle in modo consistente, seguendo un **formato standard** 
	
- **Descrizione**: definisce ulteriormente il requisito che servono a migliorare quest'ultimo.  
- **Sorgente**: da dove proviene il requisito? serve per negoziare, quale requisito bisogna scegliere?, nel caso di dubbi o conflitti, grazie a questa possiamo attivare un processo di negoziazione. 

Si possono anche svolgere delle modalità di enfatizzare il testo tramite la tecnica dell'==evidenziare il testo==, evitando anche di usare **gergo informatico** (tecnico) ed infine il documento non deve essere bello esteticamente, ma è importante che sia **preciso e leggibile**.

#### 4.9.1 Format VOLERE
Formato per fare il documento dei requisiti:
- **ID**: identificativo unico - serve per una questione di gestione del documento.
- **Tipo:** tipo di requisito (utente, sistema, ecc..)
- **Evento** / **CU correlato**: in quale contesto ha senso
-  **Descrizione**: definisce ulteriormente il requisito che servono a migliorare quest'ultimo.  
- **Motivazione**: contestualizzare il requisito che abbiamo messo nel documento.
- **Sorgente**: da dove proviene il requisito? serve per negoziare, quale requisito bisogna scegliere?, nel caso di dubbi o conflitti, grazie a questa possiamo attivare un processo di negoziazione. 
- **Criterio di Valutazione**: come poter valutare il soddisfacimento del requisito.
- **Soddisfazione Cliente:** "Voto" o valutazione del soddisfacimento del requisito se sia stato implementato.
- **Insoddisfazione Cliente:** "Voto" o valutazione nel caso in cui il requisito non sia stato soddisfatto a pieno. 
- **Conflitti**: problematiche con altri requisiti del sistema.
- **Priorità:** quanto sia importante per il cliente tale requisito (bassa, media, alta).
- **Materiale di supporto:** documenti che possano migliorare la comprensione dei requisiti.
#### 4.9.2 Scene description
Si viene ad estrarre i requisiti tramite descrizione di **scenari d'uso**, dove ogni scenario comprende:
%%Lista di cosa comprende%%

### 5.0 Interaction points
Ogni software interagisce con altri software, le interfacce di interazione sono definite formalmente:
- Application Programming Interface ([[Programming Knowledge#What is an API|API]])
- Struttura dati
- %%other  to-do%%
### 6.0 Validation of requirements
Verificare che il requisito soddisfi certe condizioni:
- **Controllo di validità**: controllo che viene fatto insieme all'utente e si applica con il **requisito utente**
- **Controllo di consistenza**: controllare che il requisito **non sia contradditorio e sia coerente**
- **Controllo di completezza**: controllare che non ci dimentichiamo nulla
- **Controllo di concretezza**:in questo caso consiste nel verificare se il requisito che richiede qualcosa che possa essere implementato.
- **Verificabilità**: requisiti che 
### 7.0 Handle the requirements
Un requisito non è per sempre lo stesso, cioè non è mai fisso, ma e variabile cambia nel tempo, che possono essere **requisiti stabili** o **requisiti variabili** (esempio 80/20 di [^2]Pareto).
- **Requisiti stabili**: requisiti che cambiano molto poco nel tempo
- _to be continued_
## 8.0 Activity diagram
---
### 8.1 Petri  Net 
![[PetriNet.png]]
Calcola la funzione della divisione per intera di due
![[RappresentazioneDegliAutomi.png]]
il secondo esempio è la versione completa della rete di petri, con l'arco innebitore, considerando anche la possibilità del calcolo, abilitando la transizione se la piazza innebitore non ha più transizione.
![[GraphOfPiazza&Transition.png]]
in questo esempio la regola deve rispettare su **tutte le piazze entranti** non solo una ma anche p2 deve avere un pallino con la transizione brucia e ritorna un nuovo token(pallini) alla p2.
### 8.2 How Activity Diagram works?
Sono nella famiglia dei diagrammi comportamentali, che viene rappresentato come un grafo, rappresentando la sequenza di azioni che rappresentano il **comportamento dinamico di un sistema**, la semantica è descritta tramite le [[#8.1 Petri Net|reti di petri]].

### 8.3 How to use it?
Si viene utilizzato nel lavoro dell'analisi, con la modellazione grafica del flusso di un caso d'uso o tra più casi d'uso.

Oppure anche nel lavoro di progettazione, con la modellazione dettagliata di un'operazione o di specifici algoritmi.
### 8.4 Components of the AD
Ci sono i nodi che sono di tre tipi:
- [[#8.4.1 Node actions|azione]]
- [[#8.4.2 Node control|controllo]]
- [[#8.4.3 Node Object|oggetto]]
anche due tipi di archi:
- flussi di controllo
- flussi di oggetti
#### 8.4.1 Node actions
E' un rettangolo con degli angoli stondati, avendo flussi entranti ed uscenti, 

**Regole di attivazione**
- esiste un token per ogni arco entrante
- tutte le pre condizioni locali del nodo azione sono soddisfatte.

**Regole di uscita**
I token vengono emessi su ogni arco in uscita se la post-condizione viene valutata vera.

**Tipologia di nodi d'azione**:
- [[#8.4.1.1 Node action call|azione chiamata]]
- invia segnale
- accetta evento
- [[#8.4.1.2 Node action accept temporal event | espressione temporale]]

##### 8.4.1.1 Node action call
Questa può chiamare l'attività il comportamento e invocare anche un'operazione
![[NodeActionCalle.png]]
##### 8.4.1.2 Node action accept temporal event
Questo nodo ha un'espressione temporale e **genera un token solamente quando l'espressione, diventa vera**.
![[TimeHandeler.png]]
questi rappresentano con la clessidra il passare del tempo.
##### 8.4.1.3 Node action partition
Si può creare delle partizioni per raggruppare le azioni, che possono essere del tipo:
- casi d'uso
- classi
- ecc...
![[PartizioneAzione.png]]
Vediamo anche un'esempio di un "flight check-in".
![[FlightCheck-IN.png]]
Il focus avviene principalmente sulle attività, focus sugli step di una procedura, sull'obbiettivo.
#### 8.4.2 Node control
Gestiscono il flusso dei token della rete, gestendo anche più controlli tramite più archi che entrano nel nodo.
I nodi di controlli sono i presenti:
- nodo iniziale (start node)
- nodo finale attività (end node)
- nodo finale del flusso (expired)
![[NodesTypes.png]]
- nodo decisione (if-then-else) 
![[DecisionNode.png]]
- nodo fusione (fusion node)
- nodo biforcazione (merge node)
- nodo ricongiunzione (fork node)

![[ListOfControlNode.png]]
#### 8.4.3 Node Object
Sono nodi che rappresentano dei buffer per i dati, specificandone la dimensione specifica, i nodi possiedono un ordinamento FIFO (First In First Out) e hanno un comportamento di selezione «selezione», sono oggetti che fluiscono nella rete.

Qui sotto avremmo la rappresentazione dello stato dell'oggetto.
![[Screenshot 2024-12-16 at 13.58.13.png]]
Qui troviamo tutti i tipi di nodi oggetto
![[Screenshot 2024-12-16 at 13.55.50.png]]

## 9.0 Quality of the requirements
---
Il software è semplice da modellare/malleabile, cioè modificabile nel tempo ed i costi sono legati  al progetto e non alla produzione, perché facendone la copia non investiamo tempo/denaro in più.

Cosa intendiamo per qualità, in questo caso abbiamo due domini per specificare la qualità, una il **processo**, un'altro invece è il **prodotto**. Qualità viene intesa come quella caratteristica, proprietà o condizione che serve a **determinare la natura e a distinguere da altre istanze nella stessa categoria** (cioè notare le differenze dello stesso oggetto nel tempo e quello che cambia dalla sua versione precedente).

Noi come programmatori, ci interessa principalmente le **distinzioni dei software che forniscono le stesse funzionalità**, migliorare una qualità comporta la riduzione di un'altra, comportando dei contrasti tra di loro.

### 9.1 Quality requirements
Sono definiti come le proprietà del sistema, sono critici tanto quanto come quelli funzionali e difficili da soddisfare alcune delle volte.

Son classificati in questi tre tipi:
- **Requisiti di prodotto** (erogare il servizio di cui il prodotto nasce)
- **Requisiti Organizzativi**
- **Requisiti  Evento**

### 9.2 Quality and Meters
Necessario **definire delle metriche**, per poter associare valori di qualità, per poter misurare effettivamente la qualità di quello che facciamo, definendo una unità di misura ed una metrica ha senso parlare di requisito qualitativo (non-funzionale).

>[!info] **Specificare un requisito qualitativo**
>_Il sistema deve risultare usabile ad un'utenza esperta_
>- Come e quando possiamo dire che il requisito sia soddisfatto oppure no?
>- Come potrebbe essere rivista la specifica per renderlo verificabile?

Molti di questi requisiti sono **molto difficili e costosi da soddisfare** e le metriche sono difficili da definire su caratteristiche non funzionali, alcune qualità sono **negativamente correlate**.

La metrica avviene sul dominio booleani con i valori:
- 0: 
- -1:
### 9.3 Reliability (Affidabilità)
### 9.4 Usability(Usabilità)
Consiste nella semplicità che il software offre nel suo utilizzo, definita da una metrica che definiremmo come in questo caso il **tempo**, in minuti o secondi di quanto si riesce a capire ed utilizzare il sistema, offrendo buone performance e **valutare tutti i fattori soggettivi**.
### 9.5 Verificabilità
La metrica utilizzata sono i numeri di input che fornisco, la controllabilità e la osservabilità, meccanismi di interazione più ne ho più sono testabili

## 10.0 Check the software validation
Capire se il nostro software risolva il problema che viene richiesto dal cliente e se lo fa nel modo "**correttamente**", confrontando il sistema software sviluppato, rispetto a quello che è stato descritto nei modelli e nei documenti dei requisiti software.

La validazione viene fatta con l'aiuto dell'utente finale, **concentrandosi sull'esigenza dell'utente e se il prodotto è coerente con la sua richiesta**, nella verifica si va a controllare se il nostro software che abbiamo sviluppato esegue gli output che abbiamo definito.  

### 10.1 Approaches of the verification and validation

+ **Approccio statico**: analisi statica dei codici sorgenti e altri documenti di progetto, verificando la conformità del sistema.
  
+ **Approccio dinamico**: testing - tramite l'utilizzo di test si eseguire il software e si scoprono i difetti.

- **Debugging**: capire dove si trova il guasto nel nostro sistema software, capire dove si riscontra il problema e risolverlo.  

### 10.2 Genesis of Failures 
Il **fallimento** è la manifestazione del guasto con un'osservazione di un funzionamento scorretto del programma.

L'**errore** consiste nel processo logico che porta ad una non corrispondenza del software rispetto a quanto necessario come risultato dell'attività.

Il **guasto** sarebbe una parte del progetto che contiene la codifica dell'errore. 

### 10.3 Unit testing
Testing di singoli elementi presenti all'interno del software, tramite l'utilizzo di **stub** e/o **mock**, ci sono diverse strategie per definire dei casi di test:
- Flusso di dati
- Flusso di controllo
- Espressioni condizionali
- Dati in input 
- Cicli
Lo sviluppatore deriva dei casi di test tramite il codice, approccio (white box).

### 10.4 Integration testing
Verificare il funzionamento dei sottosistemi, ci son delle strategie di integrazione, come ad esempio:
- top-down
- bottom-up
- big-bang
# Reference
---
[^1]: L’**elicitazione** è il processo di estrazione di **informazioni**, conoscenze o requisiti da una fonte, solitamente attraverso tecniche di intervista, osservazione o brainstorming, for more info go there [definizione elicitazione](https://www.edizionigoree.it/significato-elicitazione-definizione-etimologia/)

[^2]: **Pareto principle**: regola dell'80/20 dove l'80 percento delle conseguenze vengono dal 20 percento delle cause for more go to here [Pareto Priciple](https://en.wikipedia.org/wiki/Pareto_principle) 