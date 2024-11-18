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
# Reference
---
 [^1]: L’**elicitazione** è il processo di estrazione di **informazioni**, conoscenze o requisiti da una fonte, solitamente attraverso tecniche di intervista, osservazione o brainstorming, for more info go there [definizione elicitazione](https://www.edizionigoree.it/significato-elicitazione-definizione-etimologia/)

