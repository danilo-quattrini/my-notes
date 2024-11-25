---
share_link: https://share.note.sx/f9n2xdjq#y9OhafJT09gABPLqtR06sU/q+X6DDNx5yc02Ani0cCQ
share_updated: 2024-11-07T10:55:34+00:00
---
2024-10-10 10:28

Status: #baby 

Tags: [[Programming]][[Software Engineering]]

---
# Ingegneria del software
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

- **Product – La codebase e relativi artefatti:** è l’obbiettivo finale e risponde alla domanda “cosa si vuole costruire?” di fatti l’obiettivo dell’IDS è quello di fornire metodi e strumenti affinché la qualità di ogni artefatto risulti massima e comprensibili per future elaborazioni. ==L’obiettivo dell’ingegneria del software non è quello di produrre documentazione!==

- **Project – le attività messe in campo per la produzione del prodotto:** sono tutte quelle attività da svolgere per realizzare il prodotto finale. Oltre  alla comunicazione rivolta al consumer e allo sviluppatore e l’ingegneria dei requisiti, ovvero lo studio di fattibilità, elicitazione, specifica, analisi e validazione dei requisiti.

- **Process – come procedere nella produzione di un software:** definisce quali sono le attività da mettere in atto nello sviluppo di un prodotto software e come organizzarle. L’Ingegneria del Software ha definito diversi processi dalle diverse qualità adatte più o meno bene ai diversi ambiti di sviluppo, che vedremmo durante questo documento uno ad uno.

## 2.0 Ciclo di vita di un processo
---
Quando si parla di ciclo di vita di un processo, si va nel dettaglio e si parla prima della definizione di _ciclo di vita_ di un prodotto, esso ==viene definito come una serie di stati che sono stati compiuti da un ente(o prodotto) nella sua vita a partire dalla sua nascita, fino alla dimissione (o se vogliamo dire rimanendo in tema "morte")==.

Il _processo di sviluppo_ invece viene definito come tutti quei passi che vengono scelti ed adottati durante il ciclo di vita di un prodotto, ciò si intende che strategie si sono usate per compiere determinate azione e chi deve fare cosa per poter raggiungere tali obbiettivi.

### 2.1 Specifica e Implementazione
Dal punto di vista del progettista, cioè colui che viene a svolgere un determinato progetto, ha diversi _requisiti_  e che sono questi?
Essi sono degli obblighi imposti dall’esterno (e quindi facente parte della specifica) mentre l’implementazione svoltasi è il risultato di una serie di scelte che vengono fatte ed applicate.

>[!warning] N.B
> La ***specifica*** sarebbe un insieme che contiene una serie di requisiti, questi ne descrive in dettaglio le sue caratteristiche, spiegandone il suo utilizzo e in che sistema fa parte.
> In definitiva ricordiamo che la _specifica_ ci dice ==cosa dobbiamo fare per creare il nostro sistema==, invece l'implementazione ci dice ==come si andrà a metter mano al prodotto==
> 

### 2.2 Process Perspective
Il processo di sviluppo che abbiamo precedentemente discusso, possiede diverse tipologie di prospettive, che queste conducono alla produzione di un artefatto finale, tramite l'esecuzione di diverse attività:

- ***Activities Perspective***: definisce di quali attività si compone un processo;

-  ***Workflow Perspective***: sono le relazioni temporali tra le attività che devono essere svolte e le possibili condizioni necessarie per verificare e poter avviare un’attività;

-  ***Data-flow Perspective***: definisce quali sono gli artefatti che devono essere prodotti dalle varie attività e quelli che verranno creati al termine del progetto.

- ***Role/Actions Perspective***: definisce i ruoli necessari nell’organizzazione al fine di portare avanti un progetto in accordo al processo nonché le responsabilità di tali ruoli in relazione alle attività da compiere.
### 2.3 Attività del processo di sviluppo
Ogni prodotto industriale ha un ciclo di vita che, a grandi linee, inizia quando si manifesta la necessità o l’utilità di quest'ultimo e prosegue con l’identificare i suoi requisiti, il progetto, la produzione, la verifica, e la consegna al committente (utente finale).

Tipicamente il nostro ***processo di sviluppo*** ==è un modo di organizzare le attività costituenti il ciclo di vita, consiste nell'assegnare risorse (non so cosa intende il ragazzo con risorse qui?) alle varie attività e fissarne le scadenze==. 

Questi si distinguono in base alla organizzazione delle differenti attività dello sviluppo (workflow perspective) e da documenti/modelli che questi  producono (data-flow perspective):

1. ***Comunicare***: si intende nel ==capire cosa deve fare il sistema software== e quali sono i vincoli a cui deve sottostare il sistema. L’ingegneria dei requisiti prevede 4 task principali:
   
	- **studio della fattibilità**: comprendere le funzionalità fondamentali che il sistema deve implementare; 
	  
	- **elicitazione[^1] dei requisiti e analisi**: è il processo di raccolta e identificazione dei requisiti di un sistema software o di un prodotto i requisiti sono fondamentali perché definiscono cosa  deve fare e come deve comportarsi un sistema, per soddisfare le esigenze degli utenti;
	
	- **specifica dei requisiti**: i requisiti raccolti vengono formalizzati e descritti in dettaglio in un documento; 
	
	- **validazione dei requisiti**: è il processo di conferma che i requisiti specificati per un sistema software soddisfino effettivamente le esigenze degli utenti e degli stakeholder.
2. ***Modellazione***: una fase che  consiste nel creazione una descrizione dell'entità del software (modello) che deve essere sviluppato, la sua architettura i dati che devono essere scambiati, i componenti che fanno parte del sistema, le interfacce tra i vari elementi del sistema e gli algoritmi utilizzati.
   
   Esistono ben due approcci alla modellazione del software:
   - **metodologia agile**: si concentrano sulla flessibilità, sulla collaborazione e sulla risposta rapida ai cambiamenti;

   - **metodi strutturati**: come il modello a cascata, seguono un approccio più sequenziale e gerarchico allo sviluppo.

3. ***Costruzione:*** fase della creazione del codice e del sistema basandosi principalmente sui modelli definiti nelle varie attività precedenti (cioè quelle di modellazione).
   
4. ***Verificare e validare:*** verificare che il sistema soddisfi i requisiti e le esigenze del committente/utente (ispezione del codice o testing).
   
5. ***Manutenzione:*** attività messe in atto sul software già rilasciato per dei motivi come interventi correttivi di problemi presenti, perfettivi per l’aggiunta di funzionalità e adattivi per la portabilità del software.
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
TO-DO

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
Attore è il ruolo che un'entità assume quando interagisce con il sistema, un'entità può **possedere più ruoli contemporaneamente**
# Reference
---
 [^1]: L’**elicitazione** è il processo di estrazione di **informazioni**, conoscenze o requisiti da una fonte, solitamente attraverso tecniche di intervista, osservazione o brainstorming, for more info go there [definizione elicitazione](https://www.edizionigoree.it/significato-elicitazione-definizione-etimologia/)

