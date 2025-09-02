---
share_link: https://share.note.sx/1c1c1kk5#y9OhafJT09gABPLqtR06sU/q+X6DDNx5yc02Ani0cCQ
share_updated: 2025-09-02T15:08:26+02:00
---
2024-10-10 10:28

Status: #baby 

Tags: [[Programming]], [[Software Engineering]]

---
# Ingegneria del software

## 0.0 Introduzione
---
Ora andremmo a dare dei concetti (potrebbero servire come no idk) che sono la base dell'ingegneria del software, spiegandone cosa sono in dettaglio:

- **Software**: è ==programma che specifica le istruzioni che un calcolatore dovrà eseguire al fine di raggiungere uno scopo== Identificandone anche tutti i documenti che lo descrivono e che sono stati messi a punto durante le varie fasi della produzione del sistema.

- **Ingegneria del software**: disciplina che studia le varie fasi e processi che portano alla produzione di uno specifico software. Consiste nell’applicazione di un approccio sistematico, disciplinato e quantificabile nello sviluppo, funzionamento e manutenzione del software.
  %%ci diventi dopo aver studiato come un'animale%%
- **Ingegnere** : ==colui  che ha strumenti e competenze matematiche per descrivere le caratteristiche del prodotto, separatamente da quelle del progetto==. Si appoggia più sull’esperienza e sul giudizio personale che su tecniche matematiche. ^383c21
## 0.1 Definizioni di "Ingegneria del Software"
- **IEEE**: Applicazione di un approccio sistematico, disciplinato e quantificabile allo sviluppo, supporto e manutenzione del software.
  
- **Sommerville:** Definisce l'ingegneria del software come una **disciplina che riguarda tutti gli aspetti della produzione in se per se del software.** Colui che viene definito [[#^383c21|ingegnere]] del software è in grado di organizzare il lavoro in modo sistematico ed ordinato, utilizzando le tecniche più appropriate e gli strumenti in suo possesso, in base alle esigenze dei cliente ai problemi da risolvere i vincoli che si incontrano durante il cammino e le risorse disponibili.

- Ghezzi, Jazayeri, Mandrioli: Definiscono l'ingegneria del Software come una branca della scienza dell'informazione, dove involve principalmente lo sviluppo di sistemi software di grandi dimensioni, dove si necessita l'aiuto di un team. Differenziano il concetto di **Programmare**, come un'attività personale, cioè del singolo, da quello dell'Ingegneria del Software che prende le basi da un team e non dal singolo.
 
## 1.0 The 4's P
---
Le quattro 4 o (detto in inglese per fare il figo four's P) sono un insieme di componenti o persone che sono presenti quando si viene a creare un progetto per la prima volta e sono:

- **People – Project stakeholders**: nello sviluppo di un software complesso sono coinvolte molte persone (Business e Project Management, Development Team, Customers, End Users).
  
- **Product – La [[Programming Knowledge#^8837ca|codebase]] e relativi artefatti:** è l’obbiettivo finale e risponde alla domanda “cosa si vuole costruire?” di fatti l’obiettivo dell’IDS è quello di fornire metodi e strumenti affinché **la qualità di ogni artefatto risulti massima e comprensibili per future elaborazioni** (e.g. introduzione delle tecniche di programmazione orientata agli oggetti). ==L’obiettivo dell’ingegneria del software **NON** è quello di produrre documentazione!==

- **Project – le attività messe in campo per la produzione del prodotto:** sono tutte quelle attività da svolgere per realizzare il prodotto finale. Oltre  alla comunicazione rivolta al consumer e allo sviluppatore e l’ingegneria dei requisiti, ovvero lo studio di fattibilità, elicitazione[^1], specifica, analisi e validazione dei requisiti.
  Regola del (PRDITM) possiamo ricordarlo come **predict** in inglese:
	- Planning
	- Requirements
	- Design
	- Implementation
	- Testing
	- Maintenance

- **Process – come procedere nella produzione di un software:** definisce quali sono le attività da mettere in atto nello sviluppo di un prodotto software e come organizzarle. L’Ingegneria del Software ha definito diversi processi dalle diverse qualità adatte più o meno bene ai diversi ambiti di sviluppo, che vedremmo durante questo documento uno ad uno.

## 2.0 Ciclo di vita & processo di sviluppo
---
Quando si parla di ciclo di vita e di processo sviluppo, si va nel dettaglio e si parla prima della definizione di **_ciclo di vita_** di un prodotto, esso ==viene definito come una serie di stati che sono stati compiuti da un ente(o prodotto) nella sua vita a partire dalla sua nascita, fino alla dimissione (o se vogliamo dire rimanendo in tema "morte")==.

Il **_processo di sviluppo_** invece viene definito come tutti quei passi che vengono scelti ed adottati durante il ciclo di vita di un prodotto, ciò ==si intende che strategie si sono usate per compiere determinate azione== e chi deve fare cosa per poter raggiungere tali obbiettivi.
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

Essi sono degli obblighi imposti dall’esterno (e quindi facente parte della specifica) mentre l’*implementazione* è il risultato di una serie di scelte che vengono svolte ed infine applicate.

> [!info] **Che cos'è il progetto?**
> Il **progetto** è inteso come una serie di documentazioni che servono a descrivere come andremmo a realizzare il nostro sistema.

> [!quote] **Che cos'è il vincolo?**
> Il **vincolo** viene inteso come quella condizione che un determinato sistema deve soddisfare, che sono imposte da esigenze dovute a cause di tipo ambientali (fisiche, economiche, sociali) oppure da limiti tecnologici.
> 
> Un **vincolo è quindi un requisito** indipendente dalla volontà dell’utente.
> 

>[!warning] N.B
> La ***specifica*** sarebbe un insieme che contiene una serie di requisiti, questi ne descrive in dettaglio le sue caratteristiche, spiegandone il suo utilizzo e in che sistema fa parte.
> In definitiva ricordiamo che la _specifica_ ci dice ==cosa dobbiamo fare per creare il nostro sistema==, invece l'implementazione ci dice ==come si andrà a metter mano al prodotto==
> 

### 2.3 Process Perspective
Il processo di sviluppo che abbiamo precedentemente discusso, possiede diverse tipologie di prospettive, che queste conducono alla produzione di un artefatto finale, tramite l'esecuzione di diverse attività:

-  ***Activities Perspective***: definisce di quali attività si compone un processo;

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

Nella prima fase si va a creare i requisiti che il software dovrà soddisfare e un piano temporale dettagliato. Poi si prosegue con la modellazione e viene creato un progetto  ', si passa alla programmazione, alla quale seguono verifica e rilascio del software. 

La particolarità di questo modello è che la **conclusione di una fase, implica l'inizio di quella successiva** e che la **produzione dei semilavorati sia unidirezionale**, che cosa vuol dire? Si intende che alla conclusione di una fase i risultati di quest'ultima sono il punto di partenza di quella successiva e pertanto non possono influenzare passi precedenti.

![[waterfall-model.png]]
In questo modello che vediamo in figura,  i requisiti sono definiti inizialmente e non sono più modificabili se si passa ad una fase successiva del modello, questo **comporta delle problematiche**.

Se si vengono a scoprire degli errori od omissioni nel progetto o nelle specifiche, si necessita ripetere le fasi precedenti e modificare i semilavorati che sono stati prodotti fino ad ora.

Questa problematica rende il **modello inefficiente** e viene associato ad una **percentuale elevata di fallimenti**, per via del fatto che le specifiche definite inizialmente non vengono più modificate una volta stabilite.
#### 2.5.3 Modello Evolutivo
Il modello cerca di prevalere su quello a cascata, discusso in precedenza, questo come?

Attraverso l'utilizzo di **prototipi**

> [!info] Che cosa sono i **prototipi**?
> Sono delle versioni semplici di un sistema informativo, con la quale possiamo sperimentare diverse funzionalità. 

Ogni prototipo che si viene a creare, viene **valutato** e il risultato di tale valutazione, andrà a determinare il passo successivo finché non si arriverà alla creazione del prodotto, adottandosi alla richiesta finale del cliente, l'elaborato risulta completo e soddisfa ogni requisito, almeno fino a quando non viene richiesto un futuro update.

Questo comporta a diverse conseguenze:
>[!error] Problemi del modello evolutivo
>- **Organizzazione del sistema poco efficiente** a causa dei continui cambiamenti.
>- **Difficoltà nella manutenzione** del prodotto nel tempo.

Il nostro **prototipo** è una rappresentazione dell'ideale applicazione, che andremmo a creare, non sarà completa di tutte le funzionalità che dovremmo implementare, ma per l'analisi dei requisiti è importante valutare che fine farà il nostro prototipo:

- Se il prototipo piace allora consideriamo l'opzione di lavorarci sopra ampliandolo e perfezionandolo nel tempo chiamatosi questo, **prototipo evolutivo**.

- Oppure possiamo optare di scartarlo e creare il prodotto da zero ex-nuovo (seguendo le tracce del prodotto scartato) **prototipo throw-away**.

Quest'ultimo avrà una struttura diversa alla fine quando si verrà a creare il prodotto finale, questo evitando problematiche in ambito di efficienza.

Nel caso del prototipo evolutivo, non si avranno possibilità di scartare le scelte che si faranno nelle fasi successive del processo, ma verranno prese "seriamente", cioè non si potranno scartare, una volta decise, delle implementazioni al nostro prototipo, rendendo la realizzazione del sistema inadeguata al prodotto finale.
#### 2.5.4 Modello  Iterativo
In questo modello troviamo un mix di quello a cascata e quello evolutivo, prendendo da ognuno di loro le qualità positive togliendo a sua volta quelle negative.

Nel modello iterativo consiste nella creazione di mini-progetti che vengono denominati **iterazioni**, ogni iterazione ha come risultato un sistema eseguibile, testato e integrato, ma parziale.
Ogni iterazione possiede una propria analisi dei requisiti, progettazione e implementazione.

>[!done]  **Obbiettivo**
>Ogni iterazione che andremmo a svolgere dovrà **produrre delle versioni di lavoro software** e migliorarla gradualmente attraverso le varie iterazioni successive.

Il modello iterativo possiede diversi approcci che possiamo implementare:
- [[#2.5.4.1 Rilascio incrementale|rilascio incrementale]].
- [[#2.5.4.1 Sviluppo a spirale|sviluppo a spirale]].

In questo modello andremmo a ritrovarci con una serie di cicli strutturarti composti da **costruzione-feedback-adattamento** (cioè si passa da una fase di costruzione al ricevere il feedback da parte del cliente, fino a che non si adatta il lavoro sui feedback del cliente).

Con l'evolversi del sistema, quest'ultimo converge fino a che non si raggiungono i requisiti desiderati dal cliente, creando un progetto appropriato riducendo di molto i cambiamenti finali dei vari requisiti.

>[!done] **Vantaggi sviluppo Iterativo**
>- Minor probabilità di fallire, migliora la produttività e riduce le percentuali dei difetti
>- Riduzione dei rischi maggiore
>- Si riceve un feedback anticipato del sistema che stiamo sviluppando coinvolgendo l'utente e adattandolo alle sue esigenze.
>- Si gestiscono bene i casi complessi nella fase di sviluppo.
>- Si ha un apprendimento attivo durante il processo iterativo, cioè quello che si impara durante un'iterazione può migliorare il processo di sviluppo.
##### 2.5.4.1 Rilascio incrementale
In questo processo andremmo ad utilizzare molti **mini-[[#2.5.2 Modello a Cascata|waterfall]] in sequenza**, cioè cosa viene inteso con questa affermazione?

Significa che ad ogni **iterazione** verrà lasciata una **versione del sistema funzionante** che potrà essere utilizzata a sua volta dal cliente, ma non finisce qui, nel mentre che si mostra al cliente la versione del software funzionante, si **andrà anche a pianificare le varie iterazioni successive** in modo da introdurre nuove funzionalità.

> [!warning] **Importante**
> Ad ogni iterazione avviata, questa **deve essere conclusa senza nessuna interferenza**

I vantaggi ad utilizzare un modello iterativo con un approccio a rilascio incrementale 
consiste nel:
- efficace nei **team di sviluppo molto piccoli**
- Il cliente sarà sempre aggiornato sul sistema, dato che potrà provarlo, senza dover aspettare il rilascio finale.
- **riduzione dei rischi di fallimento**
- Si vengono a testare maggiormente le funzionalità più importanti.

Non ci sono limiti in questo approccio, si possono ripetere quanto si vuole i vari *incrementi* in modo da ridurre il rischio di fallimento del sistema, ma non solo, si viene anche a produrre nuovo valore (inteso come qualità del prodotto finale che si andrà a creare) e questo fino a quando non si saranno soddisfatti tutti i requisiti richiesti.

Questo sistema viene indicato maggiormente, quando si viene a trovare difficoltà nell'analisi dei requisiti, ed è difficile la sua stesura.

##### 2.5.4.2 Sviluppo a spirale
In queso metodo di sviluppo si viene ad introdurre il concetto di **gestione dei rischi** su ogni *iterazione*, importante perché, si verrà ad identificare di che tipo di pericolo si parla valutandolo e definendone i vari metodi per la sua gestione, optando se necessità o no di un'ulteriore iterazione.
![[Software-Life-Cycle.png]]

I punti chiavi di questo modello di sviluppo consistono in:
- Definire l'obbiettivo della nuova iterazione e i rischi che si corrono, nel svolgerla **(PLAN)**.
- Comprendere il rischio che si corre valutando le tecniche che si possono usare per la gestione di quest'ultimo **(RISK ANALYSIS)**.
- Si procede allo sviluppo dell'iterazione e alla sua validazione, cioè testando quello che si sta creando. **(ENGINEERING)**
- Si valuta se dopo questa iterazione, c'é la necessità di doverne svolgere un'altra, oppure no. **(EVALUATE)**
I tempi sono ristretti, si passa da una fase di testing a quella di pianificazione in caso si voglia apportare ulteriori modifiche e correzioni al risultato dello sviluppo.

#### 2.5.5 Model Driven Development
Questa tipologia di modello di sviluppo si basa su un modello software già esistente, cioè che ogni singola operazione di team, si basa sul **perfezionamento** e **continuazione** di un progetto già esistente.

Si parte da una base molto forte, cioè dei modelli completi e di alto livello, (cioè già fatti da qualcuno altro) e su questi ci si lavora sopra per poterci adattare ai requisiti e i vincoli richiesti, generando codice sorgente, documentazione a altri artefatti.

## 3.0 Unified Process
---
Lo **Unified Process (UP)** è un ==processo iterativo standardizzato per lo sviluppo del
software per la costruzione di sistemi orientati agli oggetti== questo è un 
processo guidato sia dal rischio che dai casi d'uso ed [[#^86224f|incentrato sull'architettura]] (come [[UML|UML]]), la baseline sono gli artefatti prodotti da un processo di sviluppo.

>[!question] Domanda d'esame
>Q: Quali sono le caratteristiche del processo unificato?
>A: Guidato dai casi d'uso e incentrato sull'architettura.

L’arco temporale del processo di sviluppo è suddiviso in **quattro fasi successive** 

>[!quote] Definition
>**Fase:** periodo di tempo in cui dedichiamo gli sforzi per raggiungere gli obbiettivi.

Ogni fase produce dei semilavorati chiamati, **Milestones (pietra miliare):** cioè insieme di obbiettivi delle fasi, definendo il ciclo di vita del progetto.

Ogni fase è suddivisa in un numero variabile di iterazioni e nel corso di ciascuna
iterazione possono essere svolte tutte le attività richieste, anche se, alcune attività
possono essere predominanti ed altre possono mancare.

Ad ogni iterazione si viene a generare una **baseline**, cioè l'insieme di artefatti e  documentazioni che sono state riviste ed approvate da un team, dove si va a creare la base per la successiva iterazione che si vuole svolgere.

> [!question] Che cosa si intende per **incremento**?
> L'incremento viene intesa come il frutto, succo di quello che si ottiene dalla differenza tra:
> baseline generata - iterazione - iterazione successiva = **Incremento**.
> Lo vedremmo in dettaglio [[#^cf1b78|qui]]


Ogni attività nello UP è definita come ***workflow*** o ***flusso di lavoro***, dove si vengono ad applicare i concetti come le *iterazioni*, *evolutivo* e *adattivo*  con **timeboxing** breve
> [!info] Che cos'è una **timebox**?
> La **timebox** viene definito come quell'arco di tempo che definiamo ad ogni iterazioni del nostro UP, cioè se dichiariamo una tempistica di 2 settimane per concludere un'iterazione, allora quest'ultima ha un **timeboxing**, cioè una **deadline**.
### 3.1 Iterations
L'iterazione definita nel contesto del processo di sviluppo software come ai cicli ripetuti di: pianificazione, progettazione, sviluppo, test e valutazione finale che vengono svolti durante la progettazione di un software per migliorarne le sue qualità.

Un’iterazione può essere considerata come un mini progetto che include le seguenti
attività:
- **Pianificare**
- **Raccolta Requisiti e Analisi**
- **Progettare**
- **Implementazione**
- **Integrazione e Test**
- **Validare e infine rilascio interno o esterno**
>[!question] Che differenza c'è tra Progettare e Pianificare?
>Quando parliamo di **Pianificare** intendiamo quelle fasi dove andremmo a definire gli obbiettivi, strategie e le azioni da applicare al fine di raggiungere un determinato risultato. 
>
>*"formulazione di un piano o di un progetto per ottenere un determinato obiettivo."*
>
>Invece quando andremmo a **Programmare** andremmo ad applicare le strategie e le azioni che sono state definite nella **Pianificazione**
>
>*"La programmazione specifica chi farà cosa, quando lo farà e come lo farà, stabilendo delle scadenze e delle milestone."*

Il prodotto software finale, sarà la sovrapposizione delle varie iterazioni, che sono organizzate in fasi (vedremmo dopo cosa sono).

Molti metodi iterativi raccomandano una durata delle iterazioni da 2 a 6 settimane (1 settimana è difficile produrre abbastanza codice e ottenere dei feedback significativi; in più di 6 settimane la complessità diventa eccessiva e il feedback viene ritardato). È bene definire un tempo in cui le iterazioni devono essere completate (timeboxing), oltre il quale è necessario passare all’iterazione successiva. Se durante la programmazione ci si accorge di non essere in grado di rispettare le tempistiche, conviene eliminare attività da un’iterazione per eseguirle nella successiva. Una iterazione di durata fissata è detta **timeboxed**.

### 3.2 Fundamentals Characteristics of UP
• **GUIDATO DAL RISCHIO**: durante la fase di progettazione si possono riscontare dei rischi che si possono evitare o  ridurre tramite il metodo UP, che si incentra principalmente in 3 fasi:
- Identificare il rischio che comporta il fallimento del progetto stesso.
- Prevenire il rischio attuando un piano per poterlo gestire.
- Gestire le aree di progetto in cui sono presenti i rischi più elevati o le incertezze più significative.
  
• **GUIDATO DAI CASI D'USO**: nel processo di sviluppo software in base al modello UP,  ci si concentra maggiormente nell'identificare e utilizzare i *casi d'uso*, chiamatesi anche *use-case*, cioè degli schemi, diagrammi UML che mostrano come l'utente o gli utenti (se sono presenti più attori)interagirà con il sistema stesso.
Grazie a queste rappresentazioni schematiche del sistema software e dopo aver analizzato tutti i casi possibili, **possiamo definire i requisiti** che sono richiesti e implementarli nel nostro software, in modo da avere un prodotto che rispetti le esigenze del cliente.

• **INCENTRATO SULL'ARCHITETTURA**: in questa parte del UP si pone una forte attenzione sull'architettura del sistema software. Cioè già dalla prima fase di sviluppo si andrà a progettare e definire l'architettura che il nostro software andrà ad avere, comportando una maggior enfasi su quest'ultimo, perché considerata importante e critica.
Lo sviluppo software incentrato su un'architettura, ci permetterà di creare software di qualità, affidabili, robusti, scalabili(cioè che si possono migliorare) e mantenibili.
Il team di sviluppo darà maggior enfasi durante questa fase di sviluppo, creando diversi modelli UML in modo da poter passare dalla fase di definizione dei requisiti alla creazione del codice e della [[Programming Knowledge#^8837ca|codebase]].^0a819d ^86224f
> [!info] **Architettura**
> Viene intesa come l'insieme dei modelli UML che si andranno a creare, durante la fase di definizione dei requisiti, cioè di cosa il sistema dovrà soddisfare a pieno.
 

• **PROCESSO ITERATIVO E INCREMENTALE**: il modello UP si basa su cicli di [[#3.1 Iterations|iterazioni]]  e incrementi, ma cosa sono gli incrementi?
> [!info] **Incremento**
> l'incremento o detto **processo di sviluppo incrementale**, si basa sull'idea di prendere un progetto e dividerlo in pezzi, dove partendo dalla prima versione del progetto, si andrà a creare in successione, delle copie di quest'ultimo dove si aggiungeranno sempre delle nuove funzionalità.

^cf1b78

Ogni *incremento comprende il risultato complessivo delle  iterazione*.
In ogni iterazione si analizza, progetta, realizza e valida una piccola parte del software producendo un sistema funzionante (anche se parziale e incompleto), così da ottenere feedback rapido dal cliente, in modo tempestivo e capire in ogni iterazione le sue esigenze.
![[Pasted image 20250821114318.png]]
### 3.3 Phases 
Le **Fasi** sono dei macro-obbiettivi, dove in ognuno di loro si pongono dei piccoli obbiettivi di breve o lungo termine, da dover raggiungere in un determinato tempo e finché non si completano, non si può passare alla fase successiva dello sviluppo software.

Ogni fase ha una durata che varia dalla complessità del progetto e dal team che ci lavora sopra, queste fasi sono divise in quattro categorie, dove ad ogni una di queste possono esser presenti una o più iterazioni:

 - [[#3.3.1 Ideazione(Inception)|ideazione]] - rosa
 - [[#3.3.2 Elaborazione (Elaborazione)|Elaborazione]] - giallo
 - [[#3.3.3 Costruzione (Construction)|Costruzione]] - arancione
 - [[#3.3.4 Transizione (Transition)|Transizione]] - blue
 - [[#3.3.5 Diagrammi e Modelli per ogni fase|Diagrammi e Modelli]] - utilizzati in ogni fase
 ![[UnifiedProcess.png|*Le quattro categorie delle fasi sono colorate differentemente*]]
#### 3.3.1 Ideazione(Inception):
**Obbiettivo:** Analisi della fattibilità del progetto, aggiungendoci anche uno studio dei rischi che comportano, avviare un nuovo progetto. L'idea di base di questa fase è quella di definire il **Business Case**, cioè capire a quale mercato il progetto andrà ad intaccare.

**Strumenti**: vengono utilizzati i **modelli dei casi d'uso** una **minima analisi dei requisiti**, una **pianificazione iniziale** per definire cosa fare e infine una **valutazione dei rischi**.

>[!warning] **Lifecycle Objective Milestone**
se non si definiscono i rischi o il business case, si dovrà abbandonare o ridefinire il progetto.

>[!info] **NB**
l'ideazione è una fase molto breve, non deve durare più di una settimana, in caso contrario, si dovrà ridefinire il progetto, questo perché si è definita una **specifica troppo dettagliata** e si andrà incontro allo spirito dell'UP.

#### 3.3.2 Elaborazione (Elaborazione)
**Obbiettivo**: sviluppare un'ossatura solida della fase precedente, perfezionandola ed estendendola, cioè creare un  una *baseline* architetturale eseguibile; (**che non un prototipo, ma una prima versione parziale funzionante**), aiutandoci a sviluppare le fasi successive del progetto.

**Strumenti:** vengono utilizzati i **diagramma di analisi del dominio** e viene definita anche una prima **fase di progettazione dell'architettura** , in conclusione andremmo a **definire una struttura complessiva del nostro sistema**.


>[!warning]  **Lifecycle Architecture Milestone**
>fase completata se e solo se:
>- [ ] Modello dei **casi d'uso completo all'80%**;
>- [ ] L'architettura del sistema deve essere **descritta** e **documentata**;
>- [ ] Fornire un'**architettura eseguibile** che dimostri di aver completato gli UC significativi;
>- [ ] Aver svolto una **revisione dei rischi e del business case** aggiornati;
>- [ ] Aver incluso una **pianificazione del progetto in modo complessivo**

> [!info] **N.B**
> Da qui in poi ora si passa alle **fasi più rischiose** in cui, la modifica o la ridefinizione del nostro progetto, risulterà molto complessa e potranno portare dei danni all'intero sistema.
#### 3.3.3 Costruzione (Construction)
**Obbiettivo**: si deve creare il primo prototipo funzionante, cioè partendo dalla *baseline architetturale*, si andrà a creare il prodotto finale, completando la raccolta dei requisiti e definire le analisi e i progetti portati avanti nelle fasi precedenti.

Quello che si produrrà in quest'ultima fase sarà la **prima beta del nostro prodotto**, tale milestone prende il nome di **Initial Operational Capability**, rappresenta il nostro sistema che conterrà un'implementazione delle funzionalità che si sono definite.

La fase si conclude con un periodo di beta-test.
#### 3.3.4 Transizione (Transition)
**Obbiettivo:** apportare le modifiche finale al nostro prodotto, che nella fase precedente, era solo una beta, ora deve diventare un **prodotto finito e completo**.
Prima il nostro sistema era solo funzionante localmente (cioè nell'ambiente di sviluppo personale), ma da questa fase, dopo un opportuna analisi fatta con gli utenti e corretti gli errori che si sono presentati durante le varie fasi, il prodotto **deve rispettare le aspettative descritte nella fase d'avvio**.

Completato quest'obbiettivo finale si è raggiunti la milestone: **Product Release**

> [!warning] **E invece se non fosse così?**
> Bhe sei fottuto, devi rifare tutto da capo, si deve ripetere il ciclo dall'inizio, cioè si riparte dall'ideazione all'elaborazione, ecc....


Attività saranno poste in ordine di importanza dall'alto quella più importante a quella meno.
![[DettaglioDelGrafico.png]]

#### 3.3.5 Diagrammi e Modelli per ogni fase
Ogni fase ha dei suoi diagrammi e modelli che ci aiutano a sviluppare il nostro progetto, questi possono essere modificati ad ogni iterazione.
>[!info] **Per il progetto**
>Nella prima iterazione, partire dall'UC diagram che definisce il sistema completo in modo schematico, con i suoi attori e UC, nelle iterazioni successive avete tempo per modificarlo e aggiungere i FoE (Flow of Events)


| Fasi                                  | Diagrammi e Modelli                                                                                                                                                                 |
| ------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Ideazione <br>(Analisi dei requisiti) | Modello di dominio:<br>- Diagramma dei Casi d'Uso<br>- Diagramma delle classi di analisi                                                                                            |
| Elaborazione<br>(Progettazione)       | Modello di progettazione:<br>- Diagramma delle classi di progetto<br>- Diagramma di analisi<br>- Diagrammi di sequenza<br>- Diagrammi delle classi di progetto per i DB (databases) |
| Costruzione<br>(Implementazione)      | - Diagramma di schema dei DB<br>- Diagrammi di sequenza più dettagliati                                                                                                             |

## 3.4 Discipline di UP
Nell'ambito del Processo Unificato (*Unified Process*) ogni attività come ad esempio la creazione di un diagramma dei casi d'uso alla creazione di un diagramma delle classi di progetto, prende il nome di **disciplina**

>[!quote] **Disciplina**
>Il termine *disciplina* viene intesa, come l'insieme delle attività e degli elaborati in una determinata area: 
>
>disciplina -> elaborato + attività svolte nel progetto.

>[!quote] **Elaborato**
>Il termine **elaborato** viene inteso come qualsiasi artefatto prodotto, durante le fasi di produzione di un progetto, ad esempio possiamo chiamare elaborato: il codice sorgente, i diagrammi che abbiamo sviluppato i documenti o gli schemi di base di dati.

Le discipline che andremmo a considerare ne sono ben 3:
- **Modello di business**: si andrà  a creare un **Modello di Dominio**, che ci servirà a definire i concetti e le relazioni del contesto applicativo (concetto = definire gli attori del sistema  , relazioni del contesto applicativo = cosa andrà a fare l'attore dentro al nostro sistema)

- **Requisiti**: attraverso il diagramma dei **Casi d'Uso** e la **Specifica Supplementare** andremmo a descrivere i requisiti che si differiscono da:
	- **requisiti funzionali**: requisiti che descrivono cosa il sistema andrà a svolgere
	- **requisiti non funzionali**: non sono rivolti alle interazioni che svolgono il sistema ma a i singoli componenti come ad esempio (requisiti per le prestazioni, usabilità e quelli tecnici)

- **Progettazione**: si passa dalla disciplina della pianificazione alla progettazione, dove andremmo a creare il Modello di progetto, cioè si andrà a trasformare i nostri requisiti in oggetti **software, interazioni e architettura**.

### 3.4.1 Discipline in relazione con le fasi
Le discipline che abbiamo appena citato sono in correlazione con le varie fasi di sviluppo che abbiamo precedentemente viso:

- **Ideazione (Inception)**: si passa alla disciplina del Modello di Business, dove si definiscono **requisiti** e i **business case**, i casi d'uso dove si 
## 4.0 Ingegneria dei requisiti
--- 
E' la disciplina che serve per **comprendere cosa il sistema debba fare**, con le sue **proprietà essenziali** e i vincoli che deve rispettare. La fase dello scoprire, analizzare, documentare, validare quello che facciamo interagendo con l'utente e  i requisiti sono attività della disciplina dell'**ingegneria dei requisiti**

Le tecniche che utilizziamo li utilizziamo in base a quello che dobbiamo fare
### 4.1 Software Intensive System
Funzionalità offerte dai sistemi software, sono due macro categorie (ci concentreremmo più sulla prima):
- **Information system**: sistemi gestionali che manipolano e erogano informazioni, dove il dato viene inserito e manipolato, computazione eseguito sui compilatori standard;
  
- **Embedded Software-intensive System**: interagisce con il mondo fisico, acquisendo dati da quest'ultimo, parte di questi sistemi non sono eseguiti su general purpose, ma su sistemi embedded. 
### 4.2 Challenge in the SIS
La complessità dei sistemi software è sempre crescente, necessitando sempre di nuovi approcci allo sviluppo, dove gli aspetti legati allo sviluppo.
_to be completed_...

### 4.3 Typical problems inside the SIS
Questa è una lista dei tipici problemi che si possono scontrare tipicamente.
![[List-of-problem.png]]

### 4.4 What is a Requisite?
>[!info] Definiton
>![[DefinitionOfRequirement.png]]
>

### 4.5 Type of Requisite
Questa dipende dal destinatario del requisito e dal focus che si persegue nell'analisi e sono:
- Si concentrano su ==chi è il **destinatario del requisito**==:
  
	- **Requisiti utente**: saranno scritti in modo che l'utente lo possa capite, descrivendo cosa fa il sistema in modo comprensibile (come ad esempio l'accesso al sistema oppure che il sistema calcola l'iva ), alto livello di astrazione usando un linguaggio naturale;
	
	- **Requisiti di sistema**: passo ulteriore a quelli dell'utente, non sono più gli utenti i destinatari, ma i progettisti o programmatori, utilizzando termini tecnici e precisi, spiegando il meccanismo del sistema, come ad esempio dopo 3 volte di tentativo di login si blocca il sistema;
	  
- Altri tipi ==sono in base alle **carattere del requisito**== e sono:
	- **Requisito funzionale**:  ha l'obbiettivo di descrivere una relazione input-output (fammi una somma di due numeri), chiede di creare una somma fra due numeri;
	  
	- **Requisito qualitativi**: descrive come il sistema soddisfa il **requisito funzionale** (fammi una somma di due numeri in due secondi), soddisfa la richiesta in un determinato tempo cioè due secondi.
	
	- **Vincolo**: sono un modo particolare per vincolare come deve essere sviluppato un software;

- Altra categoria sono l'**origine dei requisiti** 

### 4.6 How specify system requirements?
Ci possono essere diverse tecniche e specifiche per definire i requisiti di sistema:
- **Informale**: requisito di sistema con semantica ben definita, utilizzando un linguaggio naturale comprensibile all'utente;
  
- **Semi formale**: linguaggio formale, utilizzando delle grafiche per rappresentare concetti, con la semantica non sempre definita (ad esempio [[UML]] è un linguaggio semi-formale);

- **Formali**: sintassi e semantica son ben definiti. 
  
L'uso di una tecnica invece che un'altra dipende dal metodo utilizzato e il contesto, più vado nel formale più mi costa di tempo e denaro, per poter riflettere su cosa fare o no, verificando delle proprietà che non sempre abbiamo tempo di verificarne tutte. 

### 4.7 Ambiguity in the natural language
Ci possono essere diverse ambiguità che sono presenti nel linguaggio che abbiamo, che posssono impattare la specifica dei requisiti:

- **Lessicale**: termini che possono avere più significati, son polisemici, capire una cosa per un'altra.
  
- **Ambiguità sintattica**: la frase in questo caso ha più di un significato sintattico, errori di punteggiatura o di posizionamento di soggetto verbo e complemento.

- **Ambiguità semantica**: la frase possiede più interpretazioni e non una singola.

- **Pragmatica:** interpretazione che dipende dal contesto.
### 4.8 Qualitative Requisite
![[QualitativeRequirement.png]]
### 4.8 Restriction Requisite

>[!info] **Definition**
>Un determinato vincolo è un requisito  organizzativo che restringe il campo **TODO**. 
### 4.8 Requisite Domine

>[!info] **Definition**
>Un requisito di dominio è quello che deriva direttamente dallo specifico **dominio e o contesto applicativo**.

Molto difficile da far emergere, e cercare di trovarli e specificarli all'interno dell'analisi.

## 5.0 Engineering of requirement
--- 
Come trasformare le idee del comittente in qualcosa di concreto.

### 5.1 Factibility Study
**Studio preliminare** per capire se il sistema è conveniente costruirlo oppure no, facendo emergere le necessità e capire se continuare o meno, ci sono delle domande che vengono poste per questa attività:
%%METTERE LE DOMANDE%%

### 5.2 Elicitation  of analysis of requirement
Sbagliato chiedere all'utente cosa gli serve, il primo passo è identificare gli **"stakeholder"**
![[DifficultyOfRequirement.png]]
L'elicitazione viene influenzata alle caratteristica dei processi cognitivi umani, portando in considerazione i processi mentali di:
- **rimozione**
- **distorsione**: interpretazione errata di un concetto, distorta da preconcetti dell'utente;
- **generalizzazione**: semplificare il sistema, riducendo le statistiche.
Attenzione ai termini: **tutto, ogni, sempre, mai, nessuno, niente**.

### 5.3 Find of the requirements
Identificare i punti di vista, per capire e **classificare gli attori del nostro sistema** e possono essere 3 tipi **diretto**, **indiretto** e di **dominio**:

- Punto di vista **diretto**: chi interagisce direttamente con il sistema;
  
- Punto di vista **indiretto**: chi non ci interagisce, ma è interessato al sistema e il suo comportamento;
  
- Punto di vista di **dominio**: persone/attori che sono esperti del dominio o detto sistema che stiamo creando.
### 5.4 System and Actors
Attore è il ruolo che un'entità assume quando interagisce con il sistema, un'entità può **possedere più ruoli contemporaneamente**, che possono essere sistemi esterni oppure delle persone.

### 5.5 Classification of the actors
Ci sono altri attori che sono identificati con:
%% ELENCO DEGLI ATTORI %%
### 5.6 Finding the requirement: technique
Trovare gli attori dei nostri sistemi tramite l'utilizzo di:
- [[#4.6.2 Interview|Interviste:]] maggiore dettaglio nel seguito;
- [[#4.6.7 WORKSHOP|Workshops]]: maggiore dettaglio nel seguito;
- **Focus groups**: ==approfondimento aspetti del sistema che non sono chiari==, non avendo una chiara conoscenza del dominio, coinvolgendo esperti, focalizzarsi sullo specifico aspetto del dominio che non conosciamo.
- **Osservazione o etnografia:** derivare dei requisiti dalle persone che lavorano sul campo del nostro dominio, osservando come operano e i processi che seguono.
- **Questionari**: realizzare dei form per raccogliere informazioni da specifici stakeholder.
- Perspective-based reading: identificare tramite documenti specifici dettagli che non sono stati visualizzati in precedenza, svolgendo alla lettura approfondita.
#### 5.6.1 Aspect to define for each technique
Ogni tecnica segue dei passi che devono essere fornite nel dettaglio come:
- Preparazione
- Esecuzione
- Follow-up
  
Caratteristiche dell'approccio che utilizziamo possono essere descritte in questo modo:
- Benefici
- Complessità
- Fattore critica di sucesso
#### 5.6.2 Interview
Non prendere l'intervista come un esame universitario con domanda e risposta e porre sul giudizio la persona, ma mettere l'attore in una condizione di **massimo agio**, in modo che sia naturale nelle risposte.
**Non chiedere mai all'attore che cosa ha bisogno**, non sa mai cosa vuole l'attore, ogni intervista ha diversi momenti:

- **Interviste "standard"**: prepare le domanda in modo che risponda in modo preciso, proponendo il punto di vista dell'attore nel rispondere alla domanda.
  
- **Interviste a domande aperte**: permette di esplorare il concetto ampliando il discorso, però ci possono essere compromessi, basati sul fatto che quella persona andrà fuori contesto.

- **Intervista non strutturate**: procedere l'intervista con una discussione che viene guidato dall'intervistato.

Il risultato dell'intervista dipende dall'intervistatore (cioè colui che svolge l'intervista) che deve essere **bravo nell'ascoltare**.

#### 5.6.3 Prepare the interview
- **Definire l'obbiettivo dell'intervista:** chiarire la necessità dei specifici attori, o il comportamento del sistema in relazione alle specifiche richieste.
  
- **Selezionare il partecipate**: capire chi intervistare e se è giusta come persona da fare le domande o no.
  
- **Selezionare il luogo dell'intervista:** il luogo migliore sarebbe il posto dove si lavora che rende semplice la comunicazione, situazione rilassata, che non venga disturbata da qualcuno o da qualcosa come dispositivi elettronici.

- **Define the questions**: Utile avere delle informazioni sull'intervistato.

#### 5.6.4 Execution of the interview
- **Apertura:** introdurre l'obbiettivo e la motivazione di tale intervista, rendendola importante per il suo tempo che sta sacrificando per voi.

- **Conduzione**: portare dei fogli o dei materiali che siano utili per l'intervista.

- **Chiusura:** fare un sommario dell'intervista e delle parti clue. 

#### 5.6.5 Follow-up of the interview
- **Rielaborare**: riorganizzare il materiale che si possiede e definiti nel dettaglio dei requisiti, scenari e modelli che definiscono il sistema.
%% TO DO INSERIRE ALTRI DUE VANTAGGI%%
#### 5.6.6 Benefit of the interview
Le interviste sono molto importanti per ottenere e capire la **necessità del committente**. Queste però **non sono strumenti per fare innovazione  e creare dei requisiti nuovi e innovativi**

#### 5.6.7 Workshop
Lavoro di gruppo che porta a risultati eccellenti, ma prima va scelta la tecnica accessoria che verrà utilizzata per iniziare un workshop.

#### 5.6.8 Workshop preparation 
La preparazione consiste nel:
- **Definire degli obbiettivi**
- **Definire tecniche da applicare e risultati attesi**: Brainstorming, KJ method, Discussion, definizione iterativi di scenari, organizzazione di sottogruppi.
- **Scelta dei partecipanti, invito e accordo sugli obbiettivi**
- **Scelta del luogo**
- **Identificare il moderatore**
#### 5.6.9 Workshop execution
- **Apertura:** descrive l'obbiettivo del workshop, le tecniche che saranno utilizzate, l'agenda, le regole 
%% Complete with other stuff %%

#### 5.7.0 Workshop follow-up
Viene creato un 

#### 5.7.1 Workshop benefits and costs
Ottimo per l'innovazione con molte persone c'è più possibilità di innovare, molto costoso per quando riguarda di organizzazione e dei partecipanti.
#### 5.7.2 Workshop factor of success
%%Complete with the factor of success%%

### 5.8 KJ- Method
permette di far emergere i requisiti a partire da un gruppo di persone allo stesso tempo, composta da due fasi:
- **Riflessione individuale**
- **Lavoro di gruppo**

### 5.9 Document to define the requirements
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

#### 5.9.1 Format VOLERE
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
#### 5.9.2 Scene description
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