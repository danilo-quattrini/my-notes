---
share_link: https://share.note.sx/1c1c1kk5#y9OhafJT09gABPLqtR06sU/q+X6DDNx5yc02Ani0cCQ
share_updated: 2026-04-27T10:51:16+02:00
---
**LEGGI PRIMA QUESTO**
>[!warning]- Aprimi 🥰
>Questo **materiale è condiviso gratuitamente**, ci terrei se mi facessi una piccola donazione per supportare il mio lavoro, non chiedo molto (mi sembro quelli della metro che chiedono i soldi), però mi farebbe piacere un piccolo pensiero 🙏😊.
>
>Grazie ancora!
>
>Il tuo parere conta tantissimo
>![[Pasted image 20260111134240.png]]
>
>https://buymeacoffee.com/danilo.quattrini


2024-10-10 10:28

Status: #baby 

Tags: [[School]], [[Programming]], [[Software Engineering]]

*made by Danilo Quattrini ©* check me out on [GitHub](https://github.com/danilo-quattrini)

---
>[!warning] IMPORTANTE UML
>La parte di UML la trovate [qui](https://share.note.sx/zj86yira#YrwnwHRe4ioRoI1p8Yn5/Bh7vqT7l53q8Rghey3YWyw)
# Table of Content
```table-of-contents
title: 
style: nestedList # TOC style (nestedList|nestedOrderedList|inlineFirstLevel)
minLevel: 0 # Include headings from the specified level
maxLevel: 0 # Include headings up to the specified level
include: 
exclude: 
includeLinks: true # Make headings clickable
hideWhenEmpty: false # Hide TOC if no headings are found
debugInConsole: false # Print debug info in Obsidian console
```
# 0.0 Introduzione
---
Ora andremmo a dare dei concetti (potrebbero servire come no idk) che sono la base dell'ingegneria del software, spiegando cosa sono nel dettaglio:

- **Software**: è un ==programma che specifica le istruzioni che un calcolatore dovrà eseguire al fine di raggiungere uno scopo==, identificandone anche tutti i documenti che lo descrivono e che sono stati messi a punto durante le varie fasi della produzione del sistema.

- **Ingegneria del software**: disciplina che studia le varie fasi e processi che portano alla produzione di uno specifico software. Consiste nell’applicazione di un approccio sistematico, disciplinato e quantificabile nello sviluppo, funzionamento e manutenzione del software.
  %%ci diventi dopo aver studiato come un'animale%%
- **Ingegnere** : ==colui  che ha strumenti e competenze matematiche per descrivere le caratteristiche del prodotto, separatamente da quelle del progetto==. Si appoggia più sull’esperienza e sul giudizio personale che su tecniche matematiche. ^383c21
## 0.1 Definizioni di "Ingegneria del Software"
- **IEEE**: Applicazione di un approccio sistematico, disciplinato e quantificabile allo sviluppo, supporto e manutenzione del software.
  
- **Sommerville:** Definisce l'ingegneria del software come una **disciplina che riguarda tutti gli aspetti della produzione in se per se del software.** Colui che viene definito [[#^383c21|ingegnere]] del software è in grado di organizzare il lavoro in modo sistematico ed ordinato, utilizzando le tecniche più appropriate e gli strumenti in suo possesso, in base alle esigenze dei cliente ai problemi da risolvere i vincoli che si incontrano durante il cammino e le risorse disponibili.

- **Ghezzi, Jazayeri, Mandrioli**: Definiscono l'Ingegneria del Software come una branca della scienza dell'informazione, dove involve principalmente lo sviluppo di sistemi software di grandi dimensioni, dove si necessita l'aiuto di un team. Differenziano il concetto di **Programmare**, come un'attività personale, cioè del singolo, da quello dell'Ingegneria del Software che prende le basi da un team e non dal singolo.
 
# 1.0 The 4's P
---
Le quattro 4 P (detto in inglese per fare il figo "four's P") sono un insieme di componenti o persone che sono presenti quando si viene a creare un progetto per la prima volta:

- **People – Project stakeholders**: nello sviluppo di un software complesso sono coinvolte molte persone (Business e Project Management, Development Team, Customers, End Users).
  
- **Product – La [[Programming Knowledge#^8837ca|codebase]] e relativi artefatti:** è l’obbiettivo finale e risponde alla domanda “cosa si vuole costruire?” di fatti l’obiettivo dell’IDS è quello di fornire metodi e strumenti affinché **la qualità di ogni artefatto risulti massima e comprensibili per future elaborazioni** (e.g. introduzione delle tecniche di programmazione orientata agli oggetti). ==L’obiettivo dell’ingegneria del software **NON** è quello di produrre documentazione!==

- **Project – le attività messe in campo per la produzione del prodotto:** sono tutte quelle attività da svolgere per realizzare il prodotto finale. Oltre  alla comunicazione tra consumer e sviluppatore, c'è l’ingegneria dei requisiti, ovvero lo studio di fattibilità, elicitazione[^1], specifica, analisi e validazione dei requisiti.
  Regola del (PRDITM) possiamo ricordarlo come **predict** in inglese:
	- Planning
	- Requirements
	- Design
	- Implementation
	- Testing
	- Maintenance

- **Process – come procedere nella produzione di un software:** definisce quali sono le attività da mettere in atto nello sviluppo di un prodotto software e come organizzarle. L’Ingegneria del Software ha definito diversi processi dalle diverse qualità adatte più o meno bene ai diversi ambiti di sviluppo, che vedremmo durante il capitolo successivo.

# 2.0 Ciclo di vita & processo di sviluppo

---
Quando si parla di ciclo di vita e di processo sviluppo, si va nel dettaglio e si parla prima della definizione di **_ciclo di vita_** di un prodotto.

>[!info]-  **Ciclo di Vita**
>Viene definito come una serie di stati che ente(o prodotto) assume nella sua vita a partire dalla sua nascita, fino alla dimissione (o, se si vuole rimanere in tema, "morte")

>[!info]- **Processo di Sviluppo**
>Il **_processo di sviluppo_** invece viene definito come tutti quei passi che vengono scelti ed adottati durante il ciclo di vita di un prodotto, cioè si intende:
> - che strategie si sono usate per compiere determinate azioni 
> - chi deve fare cosa per poter raggiungere tali obbiettivi.

![[Screenshot 2025-09-26 at 10.51.40.png]]

Il **processo di sviluppo software** andrà a rispondere le seguenti domande:
- **CHI?**: vuole dire chi sarà la **persona/entità responsabile** di una certa attività (nell'immagine sopra, per lo sviluppo di un DBMS c'è bisogno di un progettista).
- **COME?**: che risorse o metodi utilizzerà il nostro progettista per creare il DBMS? **(Diagramma ER Entity Relations)**
  >[!question]- **ER? CHE COS'E'?**
  >Bene vuol dire che al corso di base di dati avete copiato, oppure avete una memoria corta. 
  >In caso vedetevelo [qui](https://www.geeksforgeeks.org/dbms/introduction-of-er-model/) se siete interessati.
- **CHE COSA**?: che cosa andrà a costruire, in questo caso il DBMS.
- **QUANDO**?: il tempo necessario per farlo, cioè le tempistiche che deve rispettare.
## 2.1 Parti in causa (CHI)
Quando si viene a sviluppare o ad usare un software, ci sono molte ==persone che partecipano al loro concepimento== ed è fondamentale tener conto dei loro ruoli, esigenze e rapporti reciproci all'interno della progettazione.

Per questo motivo è fondamentale che l'ingegnere del software, comprenda l'ambiente in cui si viene a sviluppare il software e capire dove viene applicato quest'ultimo.

I ruoli che andremo ad elencare sono principalmente 4:

- **Sviluppatore**: colui che fa parte del processo di ==sviluppo del software==, come ad esempio programmatori, analisti o collaudatori.
- **Produttore**: viene intesa come un'organizzazione che ==produce un software==, lo *sviluppatore* è colui che fa parte di tale organizzazione (cioè dipendete del produttore).
- **Committente**: persona o organizzazione che ==richiede al *produttore* che software bisogna creare==.
- **Utente**: persona che ==utilizza il software==.
## 2.2 Specifica e Implementazione (CHE)
Dal punto di vista del progettista, cioè chi realizza un progetto,  i *requisiti* sono degli obblighi imposti dall’esterno (e quindi facente parte della specifica). L’*implementazione* invece è il risultato di una serie di scelte che vengono svolte ed infine applicate.

> [!question]- **Che cos'è il progetto?**
> Il **progetto** è un insieme di documentazioni che descrivono come realizzare un sistema.

> [!question]- **Che cos'è il vincolo?**
> Il **vincolo** è una condizione che un sistema deve soddisfare. Tali condizioni sono imposte da esigenze dovute a cause di tipo ambientali (fisiche, economiche, sociali) oppure da limiti tecnologici.
> 
> Un **vincolo è quindi un requisito** indipendente dalla volontà dell’utente.
> 

^cf3526

>[!warning] N.B
> La ***specifica*** è una raccolta di requisiti all'interno di un documento.
> 
> In definitiva ricordiamo che la _specifica_ ci dice ==cosa dobbiamo fare per creare il nostro sistema==, invece l'implementazione ci dice ==come si andrà a metter mano al prodotto==

## 2.3 Process Perspective
Un processo di sviluppo ha diverse tipologie di prospettive. Tali prospettive conducono alla produzione di un artefatto finale attraverso varie attività:

-  ***Activities Perspective***: definisce le attività che compongono un processo;

-  ***Workflow Perspective***: organizzazione, coordinazione e monitoraggio delle attività di lavoro all'interno di un team;

-  ***Data-flow Perspective***: definisce gli artefatti che ogni attività deve produrre e quelli che verranno creati al termine del progetto.

- ***Role/Actions Perspective***: definisce l'organizzazione e le responsabilità dei ruoli in un progetto in accordo al processo.
##  2.4 Attività del processo di sviluppo
Il ciclo di vita di un prodotto industriale comincia con la necessità di tale prodotto e prosegue con l'identificazione dei requisiti, il progetto, la produzione, la verifica e la transizione (deployment: consegna all'utente finale).

>[!info] **Processo di Sviluppo 2**
>Il ***processo di sviluppo*** organizza le attività del ciclo di vita, assegnando le risorse alle varie attività e fissandone le scadenze.

 Le prospettive si distinguono in base all'organizzazione delle varie attività di sviluppo (workflow perspective) e da documenti/modelli che questi  producono (data-flow perspective):

1. ***Comunicare***: vuol dire =="capire cosa deve fare il sistema software"== e quali sono i vincoli a cui deve sottostare il sistema.
   L’==ingegneria dei requisiti== prevede 4 task principali:
   
	- **studio della fattibilità**: comprendere le funzionalità fondamentali che il sistema deve implementare; 
	  
	- **elicitazione[^1] dei requisiti e analisi**: è il processo di raccolta e identificazione dei requisiti di un sistema software o di un prodotto.
	
	- **specifica dei requisiti**: i requisiti raccolti vengono formalizzati e descritti in dettaglio in un documento; 
	 ^79cffe
	- **validazione dei requisiti**: è il processo in cui si verifica che i requisiti specificati per un sistema software soddisfino effettivamente le esigenze degli utenti e degli stakeholder.
	
2. ***Modellazione***: una fase che  consiste nel creare una ==descrizione dell'entità del software (modello) che deve essere sviluppato== cioè la sua architettura i dati che devono essere scambiati, i componenti che fanno parte del sistema, le interfacce tra i vari elementi del sistema e gli algoritmi utilizzati.
3. ***Modellazione***: una fase che  consiste nel creare una ==descrizione dell'entità del software (modello) che deve essere sviluppato== cioè la sua architettura i dati che devono essere scambiati, i componenti che fanno parte del sistema, le interfacce tra i vari elementi del sistema e gli algoritmi utilizzati.
   
   Esistono ben due approcci alla modellazione del software:
   - **metodologia agile**: si concentrano sulla flessibilità, sulla collaborazione e sulla ==risposta rapida ai cambiamenti==;

   - **metodi strutturati**: come il modello a cascata, seguono un ==approccio più sequenziale e gerarchico allo sviluppo==.

1. ***Costruzione:*** fase della ==creazione del codice e del sistema== basandosi principalmente sui modelli definiti nelle varie attività precedenti (cioè quelle di modellazione). 
   
2. ***Verificare e validare:*** 
   - **verificare**: significa controllare che il sistema ==soddisfi i requisiti e le esigenze del committente/utente== (ispezione del codice o testing) alla fine del processo di sviluppo viene fatta la verifica.
   - **validare**: invece è l'attività che viene svolta ad ogni artefatto che si viene a produrre durante il processo di sviluppo, dove ==si controlla se tale artefatto ha rispettato le funzionalità (requisiti) che si sono definite all'inizio==.
     ![[Pasted image 20250917102822.png| Validare su ogni artefatto e verificare alla fine del processo di sviluppo]]  
5. ***Manutenzione:*** attività messe in atto sul software già rilasciato per dei motivi come:
   - **interventi correttivi** di problemi presenti
   - **perfettivi** per l’aggiunta di funzionalità 
   - **adattivi** per la portabilità del software.
## 2.5 Modelli di processi
Lo sviluppo di un software avviene attraverso la costruzione di una serie di **modelli**.

Un **modello** si intende come una ==descrizione astratta di un sistema== e viene utilizzato principalmente per studiarne alcune caratteristiche che saranno necessarie per conseguire un certo scopo. Ogni sistema dovrà essere rappresentato da diversi modelli, ognuno dei quali rappresenterà lo stesso sistema, ma in diversi aspetti, con livelli di dettaglio differenti. 

I modelli che andremo a discutere saranno i seguenti:
- [[#2.5.1 Modello a Cascata|Modello a Cascata]]
- [[#2.5.3 Modello Evolutivo|Modello Evolutivo]]
- [[#2.5.4 Modello Iterativo|Modello Iterativo]]
- [[#2.5.5 Model Driven Development|Model Driven Development]]
### 2.5.1 Modello a Cascata
Il **modello a cascata** consiste nell'==esecuzione in sequenza dei diversi passi== dello sviluppo software, dove ad ogni passo si producono dei **semilavorati** che sono dei documenti inerenti al processo o degli elaborati del codice sorgente o compilato. Questi verranno rielaborati e modificati nei passi successivi.

Nella prima fase si vanno a creare i requisiti che il software dovrà soddisfare e un piano temporale dettagliato. Poi si prosegue con la modellazione e creazione di un progetto (si passa alla programmazione) alla quale seguono verifica e rilascio del software. 

La particolarità di questo modello è che la **conclusione di una fase, implica l'inizio di quella successiva** e che la **produzione dei semilavorati è unidirezionale**, che cosa vuol dire? Si intende che alla conclusione di una fase i risultati di quest'ultima sono il punto di partenza di quella successiva e pertanto non possono influenzare passi precedenti.

![[waterfall-model.png]]
In questo modello che vediamo in figura,  i requisiti sono definiti inizialmente e non sono più modificabili se si passa ad una fase successiva del modello, questo **comporta delle problematiche.**

Se si vengono a scoprire degli errori od omissioni nel progetto o nelle specifiche, si necessita ripetere le fasi precedenti e modificare i semilavorati che sono stati prodotti fino ad ora.

Questa problematica rende il **modello inefficiente** e viene associato ad una **percentuale elevata di fallimenti**, per via del fatto che le specifiche definite inizialmente non vengono più modificate una volta stabilite.
### 2.5.2 Modello Evolutivo
Il modello cerca di prevalere su quello a cascata, discusso in precedenza, questo come?

Attraverso l'utilizzo di **prototipi**

> [!question]- Che cosa sono i **prototipi**?
> Sono delle versioni semplici di un sistema informativo, con la quale possiamo sperimentare diverse funzionalità. 

Ogni prototipo che si viene a creare viene **valutato**. Il risultato di tale valutazione determinerà il passo successivo. L'elaborato risulta completo e soddisfa ogni requisito. Potrebbe essere richiesto un futuro update, adattando il prototipo alle richieste dell'utente finale.

Questo comporta a diverse conseguenze:
>[!error] Problemi del modello evolutivo
>- **Organizzazione del sistema poco efficiente** a causa dei continui cambiamenti.
>- **Difficoltà nella manutenzione** del prodotto nel tempo.

Il nostro **prototipo** è un archetipo dell'applicazione. Un archetipo non sarà completo di tutte le funzionalità da implementare, ma è importante per l'analisi dei requisiti:

- **prototipo evolutivo**: Se il prototipo piace allora consideriamo l'opzione di lavorarci sopra ampliandolo e perfezionandolo nel tempo. Non sarà possibile scartare le scelte già fatte, perciò bisogna valutare attentamente i requisiti per non rendere il prodotto finale inadeguato.

- **prototipo throw-away**: Oppure possiamo optare di scartarlo e creare il prodotto da zero ex-novo (seguendo le tracce del prodotto scartato). Il risultato avrà una struttura diversa da quella originale. Questo approccio renderà il prodotto finale più adeguato, al prezzo di una maggiore inefficienza.
### 2.5.3 Modello  Iterativo
In questo modello troviamo un mix di quello a cascata e quello evolutivo, prendendo da ognuno di loro le qualità positive togliendo a sua volta quelle negative.

Il modello iterativo consiste nella creazione di mini-progetti che vengono denominati **iterazioni**, ogni iterazione ha come risultato un sistema eseguibile, testato e integrato, ==ma parziale==.
Ogni iterazione possiede una ==propria analisi dei requisiti, progettazione e implementazione==.

>[!done]  **Obbiettivo**
>Ogni iterazione che andremmo a svolgere dovrà **produrre delle versioni di lavoro software** e migliorarla gradualmente attraverso le varie iterazioni successive.

Il modello iterativo possiede diversi approcci che possiamo implementare:
- [[#2.5.4.1 Rilascio incrementale|rilascio incrementale]].
- [[#2.5.4.1 Sviluppo a spirale|sviluppo a spirale]].

In questo modello andremmo a ritrovarci con una serie di cicli strutturarti composti da **costruzione-feedback-adattamento** (cioè si passa da una fase di costruzione al ricevere il feedback da parte del cliente, fino a che non si adatta il lavoro sui feedback del cliente).

Con l'evolversi del sistema, quest'ultimo converge fino a che non si raggiungono i requisiti desiderati dal cliente. Così il progetto rispetterà le esigenze del cliente, riducendo di molto i cambiamenti finali dei vari requisiti.

>[!done] **Vantaggi sviluppo Iterativo**
>- Minor probabilità di fallire, migliora la produttività e riduce le percentuali dei difetti
>- Riduzione dei rischi maggiore
>- Si riceve un feedback anticipato del sistema che stiamo sviluppando coinvolgendo l'utente e adattandolo alle sue esigenze.
>- Si gestiscono bene i casi complessi nella fase di sviluppo.
>- Si ha un apprendimento attivo durante il processo iterativo, cioè quello che si impara durante un'iterazione può migliorare il processo di sviluppo.
#### 2.5.3.1 Rilascio incrementale
In questo processo andremmo ad utilizzare molti **mini-[[#2.5.2 Modello a Cascata|waterfall]] in sequenza**, cioè cosa viene inteso con questa affermazione?

Significa che ad ogni **iterazione** verrà lasciata una **versione del sistema funzionante** che potrà essere utilizzata a sua volta dal cliente. Dopo aver mostrato al cliente la versione del software funzionante, si **andranno a pianificare le iterazioni successive** in modo da introdurre nuove funzionalità.

> [!warning] **Importante**
> Ogni iterazione avviata **deve essere conclusa senza nessuna interferenza**

> [!Done] Vantaggi:
> - efficace nei **team di sviluppo molto piccoli**
> - Il cliente sarà sempre aggiornato sul sistema, dato che potrà provarlo senza dover aspettare il rilascio finale.
> - **riduzione dei rischi di fallimento**
> - Si vengono a testare maggiormente le funzionalità più importanti.

Non ci sono limiti di *incrementi* in questo approccio. Ciò garantisce un risultato finale di valore che soddisfi tutti i requisiti richiesti.

Questo sistema viene indicato maggiormente per affrontare le difficoltà nell'analisi e nella stesura dei requisiti.
#### 2.5.3.2 Sviluppo a spirale
In questo metodo di sviluppo, ad ogni *iterazione*, si effettua una **gestione dei rischi**.
![[Software-Life-Cycle.png]]

I punti chiave di questo modello di sviluppo consistono in:
- Definire gli ==obbiettivi e i rischi di una nuova iterazione== **(PLAN)**.
- ==Comprendere i rischi== e trovare le tecniche per gestirli **(RISK ANALYSIS)**.
- Si procede allo sviluppo e alla validazione dell'iterazione, effettuando i test necessari. **(ENGINEERING)**
- Si valuta se dopo questa iterazione è necessario svolgerne un'altra, oppure no. **(EVALUATE)**
I tempi sono ristretti.
### 2.5.4 Model Driven Development
Questo modello di sviluppo si basa sul **perfezionamento** e **continuazione** di un software pre-esistente.

Si parte da una base molto forte (modelli completi e di alto livello) adattandola ai requisiti e i vincoli richiesti, generando codice sorgente, documentazione a altri artefatti.

# 3.0 Unified Process
---
Lo **Unified Process (UP)** (Processo Unificato) è un ==processo iterativo standard per lo sviluppo del software e per la costruzione di sistemi orientati agli oggetti==, il processo è guidato dal rischio, dai casi d'uso ed [[#^86224f|incentrato sull'architettura]] (come [[UML|UML]]).

>[!warning]- Domanda di esame:
>**Quali sono le caratteristiche del processo unificato?**
>All'esame bisogna descrivere le seguenti quattro caratteristiche:
>- Incentrato sull'architettura
>- Processo iterativo.
>- Guidato dai casi d'uso.
>- Guidato dal rischio.

Ogni attività nello UP è definita come ***workflow*** o ***flusso di lavoro***, dove si applicano il modello dello sviluppo [[#2.5.4 Modello Iterativo|Iterativo]], [[#2.5.3 Modello Evolutivo|evolutivo]] e *adattivo*
con una **timebox** breve.

> [!question]- Che cos'è una **timebox**?
> La **timebox** viene definita come quell'arco di tempo che ogni iterazione possiede nel nostro UP.
> 
> **Esempio:**  se dichiariamo una tempistica di 2 settimane per concludere un'iterazione, allora quest'ultima ha una **timebox**, cioè una **deadline** (scadenza da rispettare). 

^8adb59
## 3.1 Caratteristiche del UP

- **GUIDATO DAL RISCHIO**: durante la fase di progettazione si possono riscontare dei rischi da evitare o ridurre. Il processo unificato li gestiste in 3 fasi principali:
	- **Identificare i**l rischio che comporta il fallimento del progetto.
	- **Prevenire** il rischio attuando un piano per poterlo gestire.
	- **Gestire** le aree di progetto in cui sono presenti i rischi più elevati o le incertezze più significative.
  
-  **GUIDATO DAI CASI D'USO**: nell'UP è importante definire i **casi d'uso** ( Use Case ), cioè dei diagrammi UML che mostrano l'interazione tra attori e sistema. Tale rappresentazione aiuta ad individuare i requisiti definiti dalle esigenze del cliente.

- **INCENTRATO SULL'ARCHITETTURA**: Già dalla prima fase di sviluppo, si andrà a progettare e definire una prima architettura sulla quale si baserà il nostro sistema. Uno sviluppo incentrato sull'architettura, ci permette di creare prodotti di qualità, che siano affidabili, robusti, scalabili e mantenibili.

Un team di sviluppo porrà maggior enfasi durante questa prima fase, creando diversi modelli UML. Questo per passare dalla fase di definizione dei requisiti alla creazione della [[Programming Knowledge#^8837ca|codebase]] (codice sorgente con file di configurazione del progetto).
^86224f

> [!info] **Architettura**
> L'insieme dei modelli UML che si andranno a creare, durante la fase di definizione dei requisiti, cioè che cosa il sistema dovrà soddisfare a pieno.
 
- **PROCESSO ITERATIVO E INCREMENTALE**: il modello UP si basa su cicli di [[#3.1 Iterations|iterazioni]] e incrementi, ma cosa sono gli incrementi?

> [!info] **Incremento**
> In un **processo di sviluppo incrementale** un progetto viene diviso in pezzi (*incrementi*), dove partendo dalla prima versione del progetto, si andrà a creare in successione, delle copie di quest'ultimo aggiungendoci nuove funzionalità.

^0b7b4f
Ogni *incremento comprende il risultato complessivo delle iterazioni*.
In ogni iterazione si analizza, progetta, realizza e valida una piccola parte del software producendo un sistema funzionante (anche se parziale e incompleto).

Lo scopo è quello di ottenere dei feedback rapidi dal cliente, capendo le sue esigenze.

![[Pasted image 20250821114318.png|Esempio di uno sviluppo incrementale]]

## 3.2 Iterations

>[!info] Definizione
L'iterazione, nel contesto del processo di sviluppo software, consiste in cicli ripetuti di:
> - **Pianificazione**
> - **Analisi**
> - **Progettazione**
> - **Implementazione**
> - **Test**
> - **Validazione del prodotto finale**
> - **Rilascio interno o esterno**

>[!question]- Che differenza c'è tra Progettare e Pianificare?
>Quando parliamo di **Pianificare** intendiamo quelle fasi in cui si definiscono gli obiettivi, strategie e azioni da applicare al fine di raggiungere un determinato risultato. 
>
>*"formulazione di un piano o di un progetto per ottenere un determinato obiettivo."*
>
>Invece in fase di **Progettazione**, si applicano strategie e azioni definite in fase di **Pianificazione**
>
>*"La progettazine specifica chi farà cosa, quando lo farà e come lo farà, stabilendo delle scadenze e delle milestone."*

![[Screenshot 2025-09-26 at 11.15.07.png]]

L'immagine è un esempio di come **funziona il processo di sviluppo iterativo**, ==cioè dei mini-progetti==, dove si pianificano le attività da svolgere, si comprende che cosa deve soddisfare il sistema e poi si implementa e testa quello che si è creato.

>[!warning] **NOTA BENE**
>Ogni iterazione deve essere [[#^8adb59|timeboxed]] in modo da evitare di portare alla lunga il processo.

Alla fine di ogni iterazione si ottiene un elaborato/prodotto software parzialmente funzionante.

Il prodotto software finale sarà la sovrapposizione delle varie iterazioni che sono organizzate in [[#3.3 Phases|fasi]] (vedremmo dopo cosa sono).

Molti metodi iterativi raccomandano una durata delle iterazioni da 2 a 6 settimane (in una settimana è difficile produrre abbastanza codice e ottenere dei feedback significativi. In più di 6 settimane la complessità diventa eccessiva e il feedback viene ritardato).

È bene definire un tempo in cui le iterazioni devono essere completate (timeboxing). Superata la scandenza, si passa all’iterazione successiva. Se durante la programmazione ci si accorge di non essere in grado di rispettare le tempistiche, conviene eliminare attività da un’iterazione per eseguirle nella successiva. Una iterazione di durata fissata è detta **timeboxed**.
## 3.3 Phases 

>[!info] Definizione
>Le **Fasi** sono dei macro-obbiettivi, dove in ognuno di loro si pongono delle task di breve o lunga durata, da dover completare in un lasso di tempo definito. 

Ogni fase produce dei semilavorati chiamati, **Milestones (pietra miliare):**

>[!question]- Che cos'é una **Milestone**?
>L'insieme degli obbiettivi che si sono raggiunti in ogni fase. Queste andranno a  definire il [[#2.0 Ciclo di vita & processo di sviluppo|ciclo di vita]] del progetto. Sono dei punti di salvataggio del nostro progetto.

Prendiamo d'esempio questa immagine che ci spiega bene come saranno le fasi dell'UP, le milestone e le iterazioni:

![[structure-UP.png|Divisione tra Iterazione, Fase e Milestones]]

Finché non si completano tutti gli obbiettivi, non si può passare alla fase successiva dello sviluppo software.

Ogni fase è suddivisa in un numero variabile di iterazioni e nel corso di ciascuna iterazione possono essere svolte tutte le attività richieste, dove alcune possono essere predominanti ed altre mancare.

Ad ogni [[#3.1 Iterations|iterazione]] si viene a generare una **baseline**, cioè l'insieme di artefatti e documentazioni che sono stati rivisti ed approvati da un team.

La baseline creerà la base per la successiva iterazione.

> [!question]- Che cos'è una **baseline**, in parole povere?
> La baseline viene intesa come una struttura da cui si può cominciare a svolgere dei lavori sopra, mi spiego meglio:
> 
> *"La baseline è un documento che utilizzeremmo da base per il nostro lavoro futuro"*.
> 
> Nel nostro progetto, sarà un modello/documento che andremmo a produrre in ogni [[#3.3 Phases|fase]], alla quale nella successiva si andrà a prendere di riferimento come base da cui lavorarci nell'iterazione successiva.
> 

La fase ha una durata di tempo che varia dalla complessità del progetto e dal team che ci lavora sopra.

Il processo unificato UP ha quattro fasi, ogni una delle quali possono presentare una o più iterazioni:

 - [[#3.3.1 Ideazione(Inception)|Ideazione]] - rosa
 - [[#3.3.2 Elaborazione (Elaborazione)|Elaborazione]] - giallo
 - [[#3.3.3 Costruzione (Construction)|Costruzione]] - arancione
 - [[#3.3.4 Transizione (Transition)|Transizione]] - blue
 - [[#3.3.5 Diagrammi e Modelli per ogni fase|Diagrammi e Modelli]] - utilizzati in ogni fase
 ![[UnifiedProcess.png|*Le quattro categorie delle fasi sono colorate differentemente*]]
### 3.3.1 Ideazione (Inception)

>[!objective] **Obbiettivo**
>Analizzare la fattibilità del progetto, studiando i rischi che comporta avviare un nuovo progetto da zero.

L'idea di base di questa fase è quella di definire il **Business Case**, cioè capire in quale mercato il progetto andrà ad intaccare.

**Strumenti**: vengono utilizzati **modelli dei casi d'uso** una **minima analisi dei requisiti**, una **pianificazione iniziale** per definire cosa si deve fare e infine una **valutazione dei rischi**.

>[!warning] **Lifecycle Objective Milestone**
>Obbiettivi da soddisfare in questa fase:
>- **Capire lo scopo del sistema**, l'utilizzo che ne viene fatto, la descrizione e quello che deve soddisfare (cioè i requisiti).
>- Avere l'**idea dell'architettura che svilupperemmo** (sarà  un’idea di come sarà costruito il sistema).
>- **Identificare e Documentare i primi rischi** del sistema.
>- **Costi e Tempi**, cioè capire se il nostro sistema è sostenibile economicamente e fattibile nei tempi stabili.
>- **Business Case completo**, definire un business case che ci definisce i vantaggi e il valore del sistema nel mercato.

>[!warning]- **N.B**
l'ideazione è una fase molto breve, non deve durare più di una settimana, in caso contrario, si dovrà ridefinire il progetto, questo perché si è definita una **specifica troppo dettagliata** e si andrà incontro allo spirito dell'UP.

### 3.3.2 Elaboration (Elaborazione)

>[!objective] **Obbiettivo**
Sviluppare un'ossatura solida della fase precedente, perfezionandola ed estendendola. Dimostrare che l'architettura funziona e che si ha un prodotto solido e sotto controllo.

Si creerà una **baseline** architetturale eseguibile (**che non è un prototipo, ma una prima versione del sistema dimostrata in modo parziale e funzionante**), aiutandoci a sviluppare le fasi successive del progetto.

**Strumenti:** vengono utilizzati i **diagramma di analisi del dominio** e viene definita anche una prima **fase di progettazione dell'architettura**, in conclusione andremmo a **definire una struttura complessiva del nostro sistema**.


>[!warning]  **Lifecycle Architecture Milestone**
>Fase completata se e solo se:
>- [ ] Modello dei **casi d'uso completo all'80%** , con documento che **descrive** il sistema.
>- [ ] Fornire un'**architettura eseguibile** che rispetta i requisiti definiti in precedenza;
>- [ ] Aver svolto una **revisione dei rischi** dove sono stati noti anche i rischi resuidi;
>- [ ] Aver incluso un **piano del progetto** ed approvato dalle parti coinvolte.
>- [ ] Accordo finale tra le parti **(Accordo firmato)**

> [!warning]- **N.B**
> Da qui in poi ora si passa alle **fasi più rischiose** in cui, la modifica o la ridefinizione del nostro progetto, risulterà molto complessa e potranno portare dei danni all'intero sistema.
### 3.3.3 Costruzione (Construction)

>[!objective] **Obbiettivo**
**Creare il primo prototipo funzionante**, cioè partendo dalla baseline architetturale (definitasi nella fase precedente), si andrà a creare il prodotto finale.

In questa fase si completerà la raccolta dei requisiti, definendo le analisi e i progetti portati avanti nelle fasi precedenti.

Quello che si produrrà in quest'ultima fase sarà la **prima beta del nostro prodotto**, tale milestone prende il nome di.

>[!warning] **Initial Operational Capability**
> Sarà il prodotto che conterrà le implementazioni delle funzionalità che si sono definite precedentemente nella specifica dei requisiti.

### 3.3.4 Transizione (Transition)

>[!objective] **Obbiettivo**
> Apportare le modifiche finale al nostro prodotto, che nella fase precedente, era solo una beta, ora deve diventare un **prodotto finito e completo**.

Prima il nostro sistema era solo funzionante localmente (cioè nell'ambiente di sviluppo personale), ma da questa fase, dopo un opportuna analisi fatta con gli utenti e corretti gli errori che si sono presentati durante le varie fasi, il prodotto **deve rispettare le aspettative descritte nella fase d'avvio**.

> [!warning]  **Product Release**
> - Gli utenti utilizzano attivamente il prodotto.
> - Pensare a come mantenerlo nel tempo e come documentarlo, per renderlo comprensibile.

### 3.3.5 Diagrammi e Modelli per ogni fase

Ogni fase ha dei suoi diagrammi e modelli che ci aiutano a sviluppare il nostro progetto, questi possono essere modificati ad ogni iterazione.

>[!info] **Per il progetto**
>Nella prima iterazione, partire dall'UC diagram che definisce il sistema completo in modo schematico, con i suoi attori e UC, nelle iterazioni successive avete tempo per modificarlo e aggiungere i FoE (Flow of Events)


| Fasi                                  | Diagrammi e Modelli                                                                                                                                                                 |
| ------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Ideazione <br>(Analisi dei requisiti) | Modello di dominio:<br>- Diagramma dei Casi d'Uso<br>- Diagramma delle Classi di Analisi                                                                                            |
| Elaborazione<br>(Progettazione)       | Modello di progettazione:<br>- Diagramma delle classi di Progetto<br>- Diagramma di Analisi<br>- Diagrammi di Sequenza<br>- Diagrammi delle classi di progetto per i DB (databases) |
| Costruzione<br>(Implementazione)      | - Diagramma di schema dei DB<br>- Diagrammi di sequenza più dettagliati                                                                                                             |
|                                       |                                                                                                                                                                                     |

## 3.4 Discipline dell'UP
---
Nell'ambito del Processo Unificato (*Unified Process*) ogni attività come ad esempio la creazione di un diagramma dei casi d'uso alla creazione di un diagramma delle classi di progetto, prende il nome di **disciplina** e stiamo dicendo in sostanza **cosa stiamo facendo in ogni fase**?

>[!quote] **Disciplina**
>Il termine *disciplina* viene intesa, come l'insieme delle attività e degli elaborati in una determinata area: 
>
>disciplina -> elaborato + attività svolte nel progetto.

>[!quote] **Elaborato**
>Il termine **elaborato** viene inteso come qualsiasi artefatto prodotto, durante le fasi di produzione di un progetto, ad esempio possiamo chiamare elaborato: il codice sorgente, i diagrammi che abbiamo sviluppato i documenti o gli schemi di base di dati.

Le discipline che andremmo a considerare ne sono ben 3:
- **Modello di business**: si andrà  a creare un **Modello di Dominio**, che ci servirà a definire i concetti e le relazioni del contesto applicativo (concetto = definire gli attori del sistema, relazioni del contesto applicativo = cosa andrà a fare l'attore dentro al nostro sistema)

- **Requisiti**: attraverso il diagramma dei **Casi d'Uso** e la **Specifica Supplementare** andremmo a descrivere i requisiti che si differiscono da:
	- **requisiti funzionali**: requisiti che descrivono cosa il sistema andrà a svolgere
	- **requisiti non funzionali**: non sono rivolti alle interazioni che svolgono il sistema, ma ad i singoli componenti come ad esempio (requisiti per le prestazioni, usabilità e quelli tecnici), cioè come il sistema si comporta.

- **Progettazione**: si passa dalla disciplina della pianificazione alla progettazione, dove andremmo a creare il Modello di progetto, cioè si andrà a trasformare i nostri requisiti in oggetti **software, interazioni e architettura**.

### 3.4.1 Discipline in relazione con le fasi
Le discipline che abbiamo appena citato sono in correlazione con le varie fasi di sviluppo che abbiamo precedentemente viso:

- **Ideazione (Inception)**: si passa alla disciplina del Modello di Business, dove si definiscono **requisiti** e i **business case**, i casi d'uso dove si svolge una *Progettazione* grossolana del''architettura che avrà il nostro sistema.
  > [!objective]  **OBBIETTIVO** 
  > Comprendere se il progetto è fattibile oppure no attraverso il **Business Case** e una valutazione dei rischi.

- **Elaborazione**: i *Requisiti* all'interno di questa fase saranno quasi definiti del tutto e si instaurerà già una base architetturale per il *Progetto*, cominciando a svolgere un'*implementazione* grossolana per capire come sarà l'esecuzione del progetto.
  > [!objective] **OBBIETTIVO**
  > Ridurre i rischi, completare l'architettura del progetto e fare in modo di avere un diagramma dei casi d'uso completo dell'80%.

- **Costruzione**: Si andrà ad implementare il nostro sistema in se per sè, con i vari test per verificare se vengono rispettate le funzionalità e i requisiti richiesti.
  >[!objective] **OBBIETTIVO** 
  > Arrivare al prodotto finito e completo, implementato di test e arrivare ad una versione completa.

- **Transizione**: Fase finale in cui si andrà a distribuire il prodotto all'utente finale, dove si andrà a risolvere i vari problemi che si sono riscontrati durante la fase di beta-testing.
> [!objective] **OBBIETTIVO**
> Concludere il progetto, rilascio agli utenti finali.

## 3.5 Domande d'esame

#### Prima Domanda

> **Q: Si consideri il processo di sviluppo unificato (Unified Process - UP) e si discutano le sue caratteristiche principali nonché le fasi che lo compongono.**

Le caratteristiche principali del processo unificato a differenza dei vari processi di sviluppo alternativi, sono principalmente:
 - **Guidato dai Casi d'uso**: cioè che ogni fase del processo comporta un'analisi delle interazioni che i nostri attori hanno all'interno del sistema attraverso l'utilizzo dei casi d'uso (*use-case*), che ci aiutano a capire come il sistema interagisce, definendo i requisiti minimi che il prodotto deve possedere.
 - **Incentrato sull'architettura**: nella fase di progettazione, si va a creare un'architettura del sistema che andremmo a sviluppare, cioè un'insieme di documenti che definiscono cosa il sistema andrà a fare e le componenti che saranno disponibili, comprese le relazioni che avranno tra loro.
 - **Guidato dal rischio**: cioè far si che nella prima fase di progettazione, si vada a comprendere quali sono i rischi che il nostro sistema può incorrere, identificando quali di questi possono comportare al fallimento del progetto, definendo un **business case**, saremmo in grado di gestire quei rischi che possono comportare il fallimento del progetto e prevenire il loro accadimento.

Fare un a descrizione delle seguenti fasi: 
- **Ideazione**
- **Elaborazione**
- **Costruzione**
- **Transizione**
#### Seconda Domanda

> **Q:** Nella descrizione delle caratteristiche si descriva come le stesse vengono declinate praticamente nello svolgimento delle attività di sviluppo.

#### Terza Domanda
> **Q:** Con riferimento al processo di sviluppo unificato (Unified Process - UP) si presentino gli aspetti salienti della milestone di Elaborazione definendo i principali vincoli da soddisfare per dichiarare la fase conclusa.

**A:** La fase dell'Elaborazione nel processo di Sviluppo Unificato, avviene in seguito alla fase di ideazione. In questa parte del processo di sviluppo si andrà a migliorare gli artefatti che si sono prodotti durate la fase precedente, per far si che definisca l'architettura del sistema e si vada a creare un prototipo. In questa fase si viene ad utilizzare maggiormente il modello delle classi di analisi  e si andrà a ridefinire il modello dei casi d'uso.

Tale fase può essere conclusa se si sono soddisfatti i seguenti requisiti:
- Diagramma dei casi d'uso all'80%
- Si è svolta una revisione dei requisiti e del business case.
- Si è definita un architettura del sistema funzionante.
- Si viene a documentare l'architettura e viene
# 4.0 Ingegneria dei requisiti
--- 
>[!info] Definizione
>E' la disciplina che serve per **comprendere cosa il sistema debba fare**, con le sue **proprietà essenziali** e i vincoli che deve rispettare. La fase dello scoprire, analizzare, documentare, validare quello che facciamo interagendo con l'utente e  i requisiti sono attività della disciplina dell'**ingegneria dei requisiti**

Le tecniche che utilizziamo saranno in base a quello che dobbiamo fare.
## 4.1 Software Intensive System (SIS)
Funzionalità offerte dai sistemi software, sono due macro categorie (ci concentreremmo più sulla prima):
- **Information system**: sistemi gestionali che manipolano e erogano informazioni, dove il dato viene inserito e manipolato, computazione eseguito sui compilatori standard;
  
- **Embedded Software-intensive System**: interagisce con il mondo fisico, acquisendo dati da quest'ultimo, parte di questi sistemi non sono eseguiti su general purpose, ma su sistemi embedded. 

## 4.2 Typical problems inside the SIS
Questa è una lista dei tipici problemi che si possono scontrare tipicamente.
![[List-of-problem.png]]

## 4.3 Requisiti

>[!info] Definizione
>Il requisito viene definito come la condizione o la capacità che un sistema deve raggiungere, affinché si possano soddisfare le richieste o le aspettative di un cliente.
### 4.3.1 Type of Requisite
Questa dipende dal destinatario del requisito e dal focus che si persegue nell'analisi e sono:

- **Destinatario** del requisito (**a chi sarà rivolto il requisito?**).
- **Carattere** del requisito (**che tipo di requisito sto definendo?**).
- **Origine** del requisito.
#### 4.3.1.1 Destinatari del requisito
  
>[!info] **Requisiti  per l'utente**
> Saranno scritti in modo che l'utente lo possa capite, descrivendo cosa fa il sistema in modo comprensibile (come ad esempio l'accesso al sistema oppure che il sistema calcola l'iva ), alto livello di astrazione usando un linguaggio naturale;

>[!info] **Requisiti per il sistema**
> Passo ulteriore a quelli dell'utente, non sono più gli utenti i destinatari, ma i progettisti o programmatori, utilizzando termini tecnici e precisi, spiegando il meccanismo del sistema, come ad esempio dopo 3 volte di tentativo di login si blocca il sistema;  
#### 4.3.1.2 Carattere del requisito

>[!info] **Requisito funzionale**
>Questo requisito ha l'obbiettivo di descrivere, quali funzionalità sono presenti all'interno del sistema, specificando i dati che andranno in input e i dati di uscita (output), nonché i comportamenti.

>[!summary] Caratteristiche di un requisito funzionale
> 1. **Descrivono il comportamento del sistema**: ad un input passato, il sistema deve essere in grado di ritornare una risposta specifica.
> 2. **Incentrato sulle funzionalità**: definendo delle operazioni, servizi o funzioni, che il sistema deve possedere.
> 3. **Orientati all'utente** : riflettendo le esigenze e le aspettative degli utenti finali o altri parti interessate.

>[!info] Requisiti **NON** Funzionali
>Non sono incentrati sulle funzionalità del sistema, ma sono concentrati sul comportamento che possiede quest'ultimo.

Tali requisiti **non vanno a descrivere le funzionalità che un sistema deve possedere**, ma sono necessari al fine di specificare le sue proprietà. Tali sono per esempio: la sicurezza, le prestazione, la scalabilità e l'usabilità

>[!summary] Caratteristiche di un requisito **NON** funzionale
> 1. **Descrivono la capacità del sistema**: cioè le proprietà che possiede un sistema, come per esempio la sicurezza o le prestazioni.
> 2. **Influenzano il design e l'architettura**: cioè possono cambiare le scelte architetturali e di design del sistema.
> 3. **Misurabili e Verificabili**: devono possedere una metrica quantitativa, per valutare la loro efficenza.

>[!warning] **N.B**
>I requisiti funzionali e non, sono diversi tra di loro, però sono entrambi definiti all'interno della [[#^79cffe|specifica dei requisiti]], NON POSSONO ESSERE ESCLUSI, è importante definire entrambi, per far si che si abbia un sistema che rispetti i requisiti richiesti.
>
>Se si vogliono separare allora si elencare separatamente in sezioni dedicate del documento.

 >[!info] **Requisito qualitativi**
 >Descrive come il sistema soddisfa il **requisito funzionale**, cioè vanno oltre alle funzionalità che un sistema soddisfa. Questo per esempio potrebbe intendersi come l'esperienza dell'utente mentre utilizza un sistema (UX) oppure come lo percepisce a livello visivo (ha un'ottima qualità grafica oppure no UI).
 >![[QualitativeRequirement.png]]
	
 > [!info] **Vincolo**
 > Sono delle limitazioni, dovute a fattori esterni o interi al sistema, queste causano delle problematiche o dei rallentamenti durante la fase di sviluppo. Questi requisiti definiscono parametri fissi o limitazioni che devono essere rispettati durante lo sviluppo del software;
 > 
 >Spiegazione più dettagliata [[#^cf3526|qui]]

#### 4.3.1.3 Origine dei requisiti

>[!info] **Requisiti di Dominio**
>Sono i requisiti che **nascono dal contesto specifico in cui il sistema verrà usato**, non dal software in sé.

Sono dei requisiti che provengono dal settore in cui il cliente o l'azienda provengono (sanitario, bancario, scolastico, ecc..), questi requisiti sono ovvi ai clienti, **ma non sono ovvi invece per chi dovrà sviluppare il sistema**.

>[!example]
>Esempi di requisiti di dominio:
>- Leggi sulla privacy dei dati dei pazienti.
>- Procedure operative.
>- Limiti tecnici.

I requisiti di dominio descrivono **come funziona il mondo reale in cui il software deve operare**, e il sistema deve adeguarsi a queste regole, non il contrario.
### 4.4 Come specificare i requisiti.

>[!summary] Tecniche e specifiche per definire i requisiti di sistema:
> - **Informale**: requisito di sistema con semantica ben definita, utilizzando un linguaggio naturale comprensibile all'utente, qualche volta possono rimanere ambiguii, ma sono semplici da utilizzare;
> - **Semi formale**: linguaggio formale, riduce le ambiguità della specifica informale, questo tramite l'utilizzo delle grafiche per rappresentare concetti (ad esempio [[UML]] è un linguaggio semi-formale);
> - **Formali**: sintassi e semantica son ben definiti, ma richiedono una competenza elevata per svolgere un'analisi di questo tipo. 

L'uso di una tecnica invece che un'altra dipende dal metodo utilizzato e il contesto, più vado nel formale più mi costa di tempo e denaro, per poter riflettere su cosa fare o no, verificando delle proprietà che non sempre abbiamo tempo di verificarne tutte. 

### 4.5 Formato dei requisiti.

La struttura di un documento della specifica dei requisiti è riportato qui di seguito:
- **ID**:  identificativo unico in un formato utile agli scopi;
- **Nome**: nome dell'azienda con cui ci interfacciamo
- **Descrizione**: descrizione dettagliata del requisito per dare un significato più dettagliato.
- **Sorgente**: L'origine del requisito, la provenienza, questo può venire dalle interviste, analisi con gli utenti normative o regole
- **Peso**: Priorità (critico, importante).
![[Screenshot 2026-01-17 at 16.55.49.png|Esempio di un formato di un requisito nella specifica dei requisiti.]]
### 4.6 Ambiguity in the natural language

Ci possono essere diverse ambiguità che sono presenti nel linguaggio che abbiamo, che possono impattare la specifica dei requisiti:

- **Lessicale**: termini che possono avere più significati, son polisemici, capire una cosa per un'altra.
- **Ambiguità sintattica**: la frase in questo caso ha più di un significato sintattico, errori di punteggiatura o di posizionamento di soggetto verbo e complemento.
- **Ambiguità semantica**: la frase possiede più interpretazioni e non una singola.
- **Ambiguità Pragmatica:** interpretazione che dipende dal contesto.

# 5.0 Attività dell'Ingegneria dei requisiti
--- 
>[!info] Definizione
>L'ingegneria dei requisiti è l'attività che viene svolta per definire i requisiti che un sistema dovrà possedere, dove si andrà ad identificare che cosa  farà il  sistema e in che contesto verrà utilizzato.

Le attività che vengono svolte durante l'ingegneria dei requisiti sono:
- [[#5.1 Studio fattibilità|Studio di fattibilità]]
- [[#5.1.1 Elicitazione dei requisiti|Elicitazione dei requisiti]]
- [[#5.1.2 Validazione dei requisiti|Validazione dei requisiti]]
- [[#5.1.3 Gestione dei requisiti|Gestione dei requisiti]]
## 5.1 Studio fattibilità

>[!info] Definizione
> Attività che ci permette di capire se il sistema conviene costruirlo oppure no,  facendo emergere delle necessità e capire se è indispensabile la sua esistenza.

>[!question] Domande dello studio di fattibilità
> - Il nostro prodotto andrà a risolvere il problema che il committente ci ha richiesto?
> - Il sistema può essere implementato con costi e tempi sostenibili?
> - Si possono integrare sistemi pre-esistenti al suo interno?

In base al risultato dello studio di fattibilità, il committente decide se firmare o no il contratto per la fornitura del software.

>[!summary] **Struttura di un documento (semilavorato) prodotto dallo studio di fattibilità**
> - **Descrizione del problema che deve essere risolto** dall’applicazione, in termini di obiettivi;
>   
> - **Insieme di scenari possibili per la soluzione**, sulla base di un’analisi delle conoscenze e delle tecnologie disponibili;
>   
> - **Modalità di sviluppo** del software con una stima dei costi e tempi richiesti.
## 5.2 Elicitazione dei requisiti
>[!info] Definizione
Processo di revisione, documentazione e comprensione delle esigenze/vincoli degli utenti.

### 5.2.1 Individuazione degli stakeholders (attori)
>[!info] Definizione
Persone/gruppi di interesse del sistema (es: clienti, sviluppatori, manager, regolatori)
Una entità può svolgere più ruoli.

>[!Fail] Problema!
>Il linguaggio tecnico del dominio applicativo può variare da persona a persona, illustrando un requisito con termini diversi. Ciò può ostacolare l'individuazione degli attori.

>[!done] Soluzione!
Per ovviare al problema è necessario classificare gli attori da più punti di vista:
> - **diretto:** raccolta dei requisiti dagli stakeholder primari (Chi interagisce col sistema)
> - **indiretto**: raccolta dei requisiti dagli stakeholder secondari (Chi influenza o è influenzato dal funzionamento del sistema)
> - **di dominio:** raccolta dei requisiti basata sulla conoscenza del dominio applicativo

La raccolta dei requisiti avviene all'interno dei confini del sistema (tutto ciò che interagisce col sistema). Tipiche fonti e destinazioni delle informazioni da analizzare sono: **persone, altri sistemi esterni, sensori e attuatori, tempo.**

>[!info] Tipi di attori
>- **Attore primario**: Chi interagisce direttamente col sistema traendone anche benefici.
>  
>- **Attore finale**: Sottoinsieme di attori primari. Chi trae beneficio diretto dal sistema. Chi interagisce col sistema svolgendo le attività principali per cui è stato progettato.
>  
>  
>- **Attore di supporto**: Chi fornisce informazioni o servizi al sistema o assistenza agli attori primari. **Non traggono benefici diretti dal sistema**.
>  
>  
>- **Attore fuori scena**: Chi influenza esternamente il funzionamento o i requisiti del sistema. (es: stakeholders che stabiliscono policy, regolamenti, interessi) Non rientrano tra gli attori menzionati.

### 5.2.2 Scoperta dei requisiti
>[!info] Definizione
Cosa deve fare il sistema e entro quali vincoli deve operare?
Le seguenti sono tecniche per individuare tali requisiti:
> - Interviste
> - Workshop
> - Tecniche ausiliarie

#### 5.2.2.1 Interviste
>[!info] Definizione
Sono interazioni (meeting) con i vari attori il cui scopo è individuare i requisiti di sistema in modo naturale, instaurando un rapporto di empatia con l'interlocutore.
Esistono 3 tipi di interviste:
> - **Interviste strutturate (standardised)**
> L'analista prepara una sequenza predefinita domande a cui l'intervistato dovrà rispondere esprimendo il suo punto di vista. Utile per raccogliere informazioni specifiche e quantitative.
> - **Interviste semi-strutturate (esplorative)**
> L'analista comincia con domande predefinite, ma l'intervista si evolve in base alle risposte dell'intervistato. Utile per raccogliere informazioni dettagliate.
> - **Interviste non strutturate**
> Simili a conversazioni, l'analista ha un elenco di temi da affrontare. È l'intervistato che decide il flusso dell'intervista. Utile per esplorare nuove idee, ma non garantisce la copertura di tutte le aree di interesse.

>[!summary] Struttura di un'intervista:
> 1. **Preparazione**
> - Definire l'obiettivo dell'intervista.
> - Selezionare ed invitare i partecipanti.
> - Selezionare il luogo dell'intervista.
> - Definire le domande.
> (è importante avere informazioni sull'intervistato)
> 2. **Esecuzione**
> - **Apertura:** Introdurre obiettivi e motivazioni
> - **Conduzione**: mantenere il focus e rispondere con dei feedback
> - **Chiusura**: fare un sommario di quanto scoperto
> 3. **Follow-up**
> - rielaborare il materiale raccolto
> - identificare i [^3]gasp
> - comunicare i risultati agli intervistati

> [!done] Vantaggi
> Efficace per ottenere le informazioni principali sulle necessità dei committenti. La difficoltà può essere medio-alta a seconda del numero di attori e delle tecniche adottate.

> [!fail] Svantaggi
> Non sono adatte per definire requisiti innovativi
#### 5.2.2.2 Workshop
>[!info] Definizione
Lavoro di gruppo da parte degli stakeholders per definire i requisiti di sistema (Può portare a risultati eccellenti)

>[!summary] Struttura di un workshop
> 1. **Preparazione**
> - Definire gli obiettivi
> - Definire [[#5.1.1.2.5 Tecniche ausiliarie| tecniche ]] da applicare e risultati attesi
> - Scegliere partecipanti e luogo
> - Identificare un moderatore (coordina le attività)
> - Identificare un minute-taker (redige il verbale della riunione)
> 2. **Esecuzione**
> - **Apertura:** esporre obiettivi, tecniche e regole da adottare nell'interazione
> - **Conduzione:** Il moderatore coordina le attività e il minute-taker redige un verbale
> - **Chiusura:** Vengono raccolti i risultati e illustrati sommariamente. Si definiranno possibili attività da svolgere successivamente
> 3. **Follow-up**
>- I risultati vengono organizzati dal segretario e fatte circolare tra i partecipanti che possono richiedere modifiche

> [!done] Vantaggi
> Efficace nell'identificazione di tutte le tipologie di requisiti (anche innovativi).

> [!fail] Svantaggi
> Sforzo alto data la partecipazione di molti stakeholders e molto costoso.

#### 5.2.2.3 Focus Groups

>[!info] Utilizzo
> Quando non si capisce che cosa vuole un sistema, si svolge un lavoro di gruppo, dove si viene ad identificare e a studiare il sistema. Questo alla fine porta alla produzione di un documento.

#### 5.2.2.5 Osservazioni e Etnografie

>[!info] Utilizzo
> Per chiarire l'uso e le reali necessità che potrà avere il sistema, si va ad osservare le interazioni che dei potenziali utenti svolgeranno su di essi.

#### 5.2.2.6 Questionari

>[!info] Utilizzo
> Lista di domande, distribuite agli stakeholder, dove si andrà a raccogliere le risposte a tali domande (le domande sono riferite ad un dominio del sistema).

#### 5.2.2.7 Perspective-based reading

>[!info] **Utilizzo**
> Si prendono dei documenti che si sono rivelati importanti e si fa un approfondimeto.

### 5.2.3 Tecniche ausiliarie

>[!info]- **Brainstorming**
Generalmente associato al workshop. Riunione di stakeholders in cui si discutono liberamente idee e soluzioni innovative.

>[!info]- **KJ Method**
Forma di brainstorming in contesti eterogenei. Utile per organizzare grandi quantità di dati. Si svolge in tre fasi:
> - **Riflessione individuale:** ogni partecipante esprime requisiti rilevanti dal proprio punto di vista.
> - **Presentazione e discussione:** Le carte vengono lette ad alta voce dal moderatore. I partecipanti possono fare domande e richiedere chiarimenti.
> - **Raggruppamento e sintesi:** Le carte più rilevanti vengono raggruppate. Potrebbero riferirsi a tematiche omogenee nel sistema.

>[!info]- **Prototyping**
Creazione di prototipi del sistema per raccogliere idee e feedback e requisiti dagli stakeholders.

>[!info]- **Mind mapping**
Tecnica visiva per organizzare i requisiti in modo strutturato, facilitandone la comprensione e l'analisi.

>[!info]- **Elicitation checklist**
Promemoria per verificare che tutti gli aspetti rilevanti del sistema siano stati considerati e documentati.

#### 5.1.1.3 Documentazione dei requisiti
La documentazione dovrebbe seguire il principio **MoSCoW** (determinare l'importanza dei requisiti secondo gli stakeholders)

- **M - Must (Deve)**: Requisiti essenziali per il successo del progetto; senza di essi, la consegna è un fallimento​
    
- **S - Should (Dovrebbe)**: Importanti ma non vitali; possono essere rinviati se necessario, con workaround alternative​.
    
- **C - Could (Potrebbe)**: Desiderabili se c'è tempo e risorse extra; aggiungono valore ma non sono prioritari.​
    
- **W - Won't (Non avrà)**: Esclusi dalla release corrente, ma possibili in futuro; accettati come non implementabili ora.

Viene definito un **formato standard** per la definizione dei requisiti che **dipende dal processo adottato**.

Si possono far emergere requisiti con la **descrizione di scenari d'uso** (come viene utilizzato il sistema):
- Cosa ci si aspetta all'inizio di uno scenario
- Descrizione del flusso normale di uno scenario
- Descrizione di cosa può andar storto nel flusso normale
- Informazioni su attività che potrebbero svolgersi in parallelo
- Descrizione dello stato finale del sistema
### 5.1.2 Validazione dei requisiti

>[!info] Definizione 
>La **validazione dei requisiti** è un processo fondamentale per capire se i requisiti che si sono specificati e raccolti nella fase di elicitazione, siano validi al fine di soddisfare le esigenze del progetto.

>[!summary] Controlli per eliminare problematiche dai requisiti
> - **Controllo di validità**: consiste nel capire e controllare se i requisiti che si sono raccolti siano validi per le specifiche del progetto e le necessità dell'utente.
> - **Controllo di consistenza**: i requisiti devono seguire un filo logico e non devono essere contraddittori.
> - **Controllo di completezza**: i requisiti devono includere tutte le funzionalità che devono essere presenti nel sistema.
> - **Controllo di concretezza** : cioè semplicemente sapere se i requisiti siano fattibili dal punto di vista di costi, tempi e sulla loro reale implementazione.
> -  **Verificabili**: i requisiti devono essere rappresentati in modo che si possa dare un criterio di valutazione.

Ci sono altre attività che vengono svolte durante questa fase e sono le seguenti.

>[!eye] **Revisione dei Requisiti**
>Viene svolta una revisione da parte di un team misto tra *stakeholder* e team di sviluppo, nella quali si cerca di rendere chiari i requisiti che si sono raccolti e fare in modo che siano completi
>Questo processo può essere informale oppure formale.

>[!summary] **Prototipizzazione**
>Vengono creati dei prototipi del sistema in base ai requisiti che si sono raccolti, questo per far si che si possa mostrare come il sistema andrà a  funzionare in base alle richieste degli *stakeholder*, si riceveranno dei feedback utili per poter svolgere delle modifiche aggiuntive o migliorie.

>[!bug] **Generazione Casi Test**
>Ci saranno delle sessioni in cui gli utenti andranno a far parte della validazione dei requisiti, cioè saranno partecipi ai test di controllo del sistema, fornendo feedback e aspettative sulle esigenze reali del sistema.
### 5.1.3 Gestione dei requisiti

>[!warning] **Premessa**
>I requisiti durante lo sviluppo del software sono spinti da forti cambiamenti, cioè non sempre i requisiti sono fissati, perciò ci possiamo definire due tipologie:
>1. **Volatili**: cioè possono cambiare durante la fase dello sviluppo.
>2. **Stabili**: rimangono sempre gli stessi una volta che vengono definiti.

Ora passiamo al termine di **Gestione dei Requisiti**.

>[!info] Definizione
>Sono tutte quelle **attività che comportano la gestione, la validazione e il controllo** delle modifiche che si sono fatte a dei requisiti, artefatti o componenti software che hanno subito delle modifiche.

La gestione del requisito è una tecnica utilizzata per far si che si possa individuare e gestire un requisito da modificare. Ci sono dei passi che vengono svolti durante tale gestione.

1. Identificare il requisito che deve subire la modifica, trovarlo nel sistema e capire che parti del progetto coinvolgono.
   
2. Per eseguire una modifica si eseguono dei passi ben definiti e strutturati, questo per esempio lo si può fare  precedentemente dopo aver individuato il requisito da modificare.
>[!example] **Esempio:**
>1. Si parte da una richiesta di modifica di un requisito.
>2. Il team lo valuta approvando o rifiutando il requisito.
>3. Dopo aver ricevuto l'approvazione si a svolgerà la modifica e si aggiornerà la specifica dov'è dettagliato il requisito.

3. Si specificano degli strumenti per tracciare la modifica che si è svolta, analizzando la conseguenza che può portare la modifica di tale requisito.

4. Utilizzo di strumenti per salvare le modifiche che si sono svolte (databases, fogli di calcolo e cazzate varie).

##### 5.1.3.1 Tracciabilità dei requisiti

>[!info] Definizione
>La **tracciabilità dei requisiti**, viene intesa come lo studio e l'analisi tra il requisito e le relazioni che possiede con gli artefatti del progetto

La tracciabilità serve per **capire le origine del requisito**, cioè come viene realizzato e verificato. Ogni requisito viene verificato tramite casi di test, cioè cosa si intende per casi test?

>[!warning] **Casi test**
>- Ogni requisito possiede dei casi test, cioè devono possedere uno o più test che lo verificano.
>- Dai test si possono verificare quale requisito è quello che causa più problematiche.

Per evitare che quello che si è definito nei requisiti venga svolto si realizza una **matrice di tracciabilità**, cioè una tabella che faccia in modo **che nulla venga dimenticato** e che il progetto rimanga **coerente con le decisioni iniziali**.
![[Pasted image 20260130160150.png]]

# 6.0 Pattern GRASP
---
>[!info] Definizione
***GRASP*** (**G**eneral **R**espon**S**ibility **A**ssignment **P**atterns) sono un insieme di pattern che vengono utilizzati nella progettazione orientata agli oggetti, che **definiscono delle linee guida**,  su **come assegnare le responsabilità alle classi e agli oggetti**. 

Questi pattern **non vengono utilizzati per creare nuove informazioni**, ma sono utili per far si che si possano generalizzare alcuni concetti standard della programmazione, migliorandone anche la documentazione, che verrà generata applicando tali pattern.

>[!summary] Responsabilità di un oggetto
> - **fare:** cioè eseguire delle operazioni su se stesso, chiedere ad altri oggetti di eseguire alcune operazioni oppure controllare e coordinare le attività di altri oggetti.
> - **conoscere**: conoscere i propri dati che possiede, conoscere gli oggetti che sono correlati oppure, conoscere che cosa può derivare oppure calcolare.

Ogni responsabilità può essere applicata ad un singolo oggetto oppure ad una collaborazione di quest'ultimi.

**RDD** ( **R**esponsibility **D**riven **D**evelopment), cioè l'approccio con cui andremmo ad assegnare le responsabilità ai nostri oggetti, sono definite dall'iterazione dei seguenti passi:
1. Troviamo ed identifichiamo le responsabilità che ci servono, considerandone una per volta.
2. Ogni responsabilità verrà delegata ad una classe, cioè assegneremo la responsabilità alle classe che dovrà soddisfare tale compito.
3. Ci domandiamo: **la classe sarà in grado di soddisfare tale responsabilità?**, in caso contrario,  ha bisogno dell'aiuto di altre classi per poter operare la responsabilità assegnatagli.
>[!warning] **N.B**
> I pattern **GRASP** definiscono già degli schemi ben precisi su come poter assegnare queste responsabilità.
> 
> Gli schemi sono i seguenti:
> - Creator
> - Information Expert
> - Low Coupling
> - Controller
> - High Cohesion
> - Pure Fabrication
> - Indirection
> - Polymorfism
> - Protected Variations

## 6.1 Creator

>[!info] **Definizione** 
>Definisce la responsabilità in cui si dice, quale classe  avrà la responsabilità di creare una nuova istanza di una certa classe?

Date due classi **A** e **B** diremmo che la classe **A** sarà in grado di creare **B** se e solamente se:
- **A** contiene o aggrega con una composizione oggetti di tipo **B**.
- **A** registra oggetti di tipo **B**.
- **A** usa oggetti di tipo **B**.
- **A** possiede le informazioni necessarie per creare **B**.

>[!example] Esempio
>La classe **A** sarà il nostro **Cliente**, invece la classe **B**, sarà **Ordine**, un Cliente crea un Ordine perché conosce quest'ultimo e usa oggetti di quel tipo.

>[!done] Vantaggi
>Favorisce il Low Coupling, perché la classe B è in relazione con A.

>[!fail] Svantaggio
>La creazione può rimanere molto complessa, dovendo delegare la creazione a classi terze.

## 6.2 Information Expert

>[!info] **Definizione** 
>E' un design che assegna la responsabilità agli elementi che possiedono le informazioni necessarie per conseguire tale responsabilità.

Questo pattern non ti offre l'implementazione di come assegnare la responsabilità alla classe che possiede le informazioni per compierla, ma **ti offre un metodo per ragionare su quale classe si debba inserire delle responsabilità**

>[!example] Esempio
>Se un oggetto `Ordine` deve calcolare il suo totale, l'operazione `calculateTotal()` dovrebbe essere assegnata alla classe Ordine stessa, poiché essa possiede le informazioni sugli articoli e i prezzi (`price` `List<Product>`).


>[!done] Vantaggi
>- **Incapsulamento**: le operazioni e i dati sono centralizzati in un'unica classe
>- **basso accoppiamento**: le classi non conoscono il comportamento della classe che possiede tali responsabilità.
>- **alta coesione**: la classe fa cose che le compete.
>- **manutenibilità**: se cambia un comportamento interno, solo la classe cha possiede tale responsabilità ne è affetta.

>[!fail] Svantaggio
> Si può rischiare di assegnare molte responsabilità alla stessa classe, violando il principio di Single Responsibility e rendendo la classe **bloated** (cioè una **GOD** class)

## 6.3 Low Coupling

>[!info] **Accoppiamento** 
>Si intende con il concetto di accoppiamento, la connessione o la dipendenza che esiste tra due elementi. La modifica su uno dei due elementi ( elementi = classi), può ripercuotere l'elemento a cui è connesso.

Vediamo degli esempio di accoppiamento:
- La classe **A** contiene degli attributi, istanze o collezione di oggetti di tipo  classe **B**.
- La classe **A** richiama delle operazioni di **B**.
- La classe **A** crea oggetti di tipo **B**
- Il metodo della classe **A** contiene un parametro di tipo **B**.
- La classe **A** è una sotto classe di **B**
- **B** è un'interfaccia di **A**.

**Low Coupling:** è utile quando vogliamo **ridurre l'accoppiamento tra le classi**, cioè non vogliamo che una classe conosca le implementazioni o gli attributi di un'altra.

>[!example] Esempio
Evita che una classe Pagamento conosca dettagli sull'implementazione della classe Ordine. Usa interfacce o pattern come il [[Design Pattern#6.4.1 Factory pattern|Factory Pattern]] per ridurre l'accoppiamento.

>[!done] Vantaggi
>Ridurre le dipendenze tra le classi ci permette di creare un sistema mantenibile nel tempo, di facile **comprensione** e **riutilizzabile**.

>[!fail] Svantaggio
> Non è necessario ridurre la dipendenza tra classi che contengono elementi stabili.

## 6.4 Controller
>[!info] 
>Il pattern è definito di delega perché non svolge operazioni in se, ma assegna delle responsabilità quando gli vengono date (tipo come come Christian quando non vuole cucinare e assegna la responsabilità a  Sara), cioè controlla che la responsabilità venga assegnata alla classe di sua  compotenza.

Questo pattern **non svolge operazioni al suo interno**, ma ha il compito di orchestrare le richieste che gli vengono passate.

>[!example] Esempio
>Si va richiamare l'operazione di: ```creaOrdine(cliente, data)```
> Una classe `SistemaGestioneOrdini` potrebbe agire come controller per le operazioni relative agli ordini, mandando la richiesta di creare l'ordine alla classe di sua responsbilità.

>[!done] Vantaggi
> Maggiore riuso, disaccoppiamento tra l'UI e il modello di dominio

>[!fail] Svantaggio
> può diventare troppo complesso, accumulando troppe responsabilità e diventando difficile da mantenere.

## 6.5 High Cohesion

>[!info] Coesione
>La coesione viene intesa come quanto sia correlate le operazioni che sta svolgendo un elemento software, cioè se le operazioni che sta eseguendo sono coerenti con il suo dominio.

Questo pattern ci aiuta a capire se un determinato elemento stia eseguendo solamente le funzionalità di un dominio specifico, cioè:

>[!example] Esempio
>Prendiamo una classe `Fattura`, questa classe dovrà avere solo delle responsabilità riferite alla gestione delle fatture, non dovrà gestire operazioni della classe `Order`

Questo pattern deve rispondere alla domanda:

>[!quote]
>**Le responsabilità di questa classe sono tutte legate allo stesso scopo?**

Semplicemente quando vediamo una classe dovremmo capire se questa verrà a possedere solo una singola occuppazione, cioè sarà considerata **alta coesione se non sta facendo altro che è fuori dal suo contesto**. (Christian ha il compito di andare in bicicletta, ma durante la sua sessione di bici ad un certo punto comincia a correre, se va in bici come fa allo stesso tempo a correre?)

**La coesione e l'accoppiamento sono inversamente proporzionali**:
questo perché, se si ha **un'alta coesione allora non ci sarà accoppiamento con altri elementi**. Invece **se si ha un'alto accoppiamento si avrà una bassa coesione**, questo perché le classi andranno a dipendersi a vicenda (alto accoppiamento) senza però avere ben chiaro il loro scopo principale (basse coesione).

>[!done] Vantaggi
> - Semplifica la manutenzione.
> - Maggiore sarà la compresione della classe.
> - Ci sarà un maggiore riutilizzo di quest'ultima.

>[!fail] Svantaggio
> Si può violare questo concetto se si vuole eseguire delle operazioni che riguardano le prestazioni.

## 6.6 Pure Fabrication

>[!info]
>Pattern che viene utilizzato quando si vuole aumentare la coesione e diminuire l'accoppiamento, non fa parte del dominio, ma serve per far si che risolve al problema:
>
>*Dove metto questa responsabilità che NON fa parte di nessun dominio.*

Questo scenario si presenta spesso in queste situazioni:
- Logging
- Persistenza
- Accesso a database

Questo patter è utile perché permette di delegare un compito completamente diverso dal dominio di un elemento, ad un elemento esterno che possiede solo quella responsabilità.

>[!example] Esempio
>Una classe `Logger` separa la responsabilità di assegnare ad ogni classe un metodo per salvarsi i suoi stati delegando tale operazione a la classe che svolge tale responsabilità.


>[!done] Vantaggi
> - Alta coesione
> - Basso accoppiamento.
> - Maggior riuso del codice.

>[!fail] Svantaggio
> Si può incorrere nella complessità della struttura.

## 6.7 Indirection

>[!info] Definizione
>**indirection = indirezione = comunicazione indiretta**
>> 
>Pattern che **da la responsabilità ad un elemento di mettersi in mezzo tra due elementi per fare in modo che possano comunicare tra di loro**, questo evitando di aumentare l'accoppiamento. Il beneficio di tale operazione è quello di aumentare la flessibilità del sistema e la manutenibilità.

Il flusso dell'operazione che fa l'indirection è quello di far in modo che due classi `A` e `B` dalla connessione:
```
A → B
```
ci sarà un intermediario di mezzo che:
```
A → I → B
```
Facendo in questo modo si ridurrà l'accoppiamento che si era formato precedentemente tra le due classi, in questo modo:
- `A` dipenderà dall'elemento `I`, senza conoscere `B`
- `B` a sua volta conoscerà `I` , senza interagire con `A`


>[!done] Vantaggi
> - Alta coesione
> - Basso accoppiamento.
> - Le modifiche di una classe non andranno ad intaccare l'altra (riduzione effetto domino).

>[!fail] Svantaggio
> Si può incorrere nella complessità della struttura.

## 6.8 Polymorphism

>[!info] Definizione
>Si viene ad usare il Polymorfismo quando si vuole gestire dei comportamenti degli elementi che variano da uno specifico tipo.

Il polimorfismo si può ottenere tramite ereditarietà di una classe astratta oppure attraverso l'utilizzo delle interfacce, questo ci permette di accomunare una famiglia di elementi che condividono una stessa funzionalità ma che variano per ogni tipo.

>[!example] Esempio
>definisci un'interfaccia Pagamento con un metodo processa(), e implementa tale metodo nelle sottoclassi PagamentoConCarta e PagamentoConBonifico


>[!done] Vantaggio
> Flessibile e facile da estendere per le future implementazioni.

>[!fail] Svantaggio
> Rischio di abusare del concetto per prevedere delle funzionalità future.

## 6.9 Protected Variations

>[!info] Definizione
>Quando vogliamo che gli elementi del sistema siano protetti da modifiche esterne o variazioni future. **NON VUOL DIRE PRIVATIZZARE GLI ATTRIBUTI O LE CLASSI**, ma fare in modo che il cambiamento sia contenuto e possa subire il meno impatto possibile.

Questo pattern serve a far si che si possa isolare le componenti che in futuro potranno avere delle variazioni, ad esempio:

- algoritmi
- servizi esterni
- regole di business instabili.

Sono delle componenti che possono rischiare di subire dei cambiamenti.

Il pattern risolve questo problema isolando il componente che potrà variare in vari modi: tramite un'interfaccia, una classe astratta, polimorfismo o con il concetto di composizione.

>[!example] Esempio
>Prendiamo sempre il modello dell'`Ordine`, questo se viene associato ad un singolo pagamento, come ad esempio `PayPal`, sarà in rischio di modifiche in caso si volesse aggiungere un nuovo metodo di pagamento.
>
>La soluzione sarà:
>```
>Ordine → MetodoPagamento (interfaccia)
MetodoPagamento → PayPal
MetodoPagamento → CartaCredito
>```

# 7. 0 Domande Capitolo 
>[!question]- GRASP
> 1. Che cosa sono i pattern GRASP e quale problema affrontano nella progettazione OO?
> 2. Che cosa si intende per _assegnazione delle responsabilità_ in un sistema orientato agli oggetti?
> 3. Definisci il concetto di **responsabilità** in ambito OO.
> 4. Spiega il significato di **alta coesione** e **basso accoppiamento**.
> 5. Perché alta coesione e basso accoppiamento sono spesso correlati?
> 6. Quali sono i principali rischi di un sistema con bassa coesione?
> 7. In che modo i GRASP supportano la manutenibilità del software?

>[!question]- Information Expert
> 8. Definisci il pattern **Information Expert** e spiega quale criterio utilizza.
> 9. Qual è la domanda chiave a cui risponde l’Information Expert?
> 10. Perché l’Information Expert favorisce l’incapsulamento?
> 11. Fornisci un esempio in cui l’Information Expert non è applicabile.
> 12. Quali problemi possono emergere applicando in modo eccessivo l’Information Expert?
> 13. Spiega la relazione tra Information Expert e alta coesione.

>[!question]- Controller
> 14. Definisci il pattern **Controller** secondo GRASP.
> 15. Qual è il ruolo del Controller in un caso d’uso?
> 16. Qual è la differenza tra **Controller di sistema** e **Controller per caso d’uso**?
> 17. Perché il Controller non dovrebbe contenere logica di business?
> 18. In che modo il Controller favorisce il disaccoppiamento tra UI e dominio?
> 19. Quali sono i segnali che indicano un Controller sovraccarico?

>[!question]- Alta Coesione
> 20. Definisci la coesione funzionale.
> 21. Come si valuta se una classe ha alta o bassa coesione?
> 22. Fornisci un esempio di classe con bassa coesione.
> 23. Perché l’alta coesione migliora la riusabilità del codice?
> 24. In quali casi può essere accettabile violare il principio di alta coesione?
> 25. Che relazione esiste tra alta coesione e responsabilità di una classe?

>[!question]- Pure Fabrication
> 26. Definisci il pattern **Pure Fabrication**.
> 27. Perché una classe Pure Fabrication non rappresenta un concetto del dominio?
> 28. In quali situazioni è opportuno introdurre una Pure Fabrication?
> 29. Quali vantaggi offre Pure Fabrication rispetto all’assegnazione diretta delle responsabilità al dominio?
> 30. Quali rischi comporta un uso improprio di Pure Fabrication?
> 31. Spiega la differenza tra Pure Fabrication e Information Expert.

>[!question]- Indirection
> 32. Definisci il pattern **Indirection**.
> 33. Perché il pattern si chiama Indirection?
> 34. In che modo Indirection riduce l’accoppiamento?
> 35. Qual è il ruolo dell’intermediario introdotto da Indirection?
> 36. Fornisci un esempio di applicazione di Indirection.
> 37. Qual è il costo principale dell’uso di Indirection?
> 38. Quali pattern GoF realizzano il principio di Indirection?

>[!question]- Protected Variations
> 39. Definisci il pattern **Protected Variations**.
> 40. Che cosa si intende per _punto di variazione_?
> 41. In che modo Protected Variations protegge il sistema dai cambiamenti?
> 42. Quali tecniche OO permettono di realizzare Protected Variations?
> 43. Perché le interfacce sono particolarmente adatte a implementare Protected Variations?
> 44. Qual è la differenza tra impedire una variazione e proteggerne l’impatto?
> 45. Quali sono i rischi dellal*distinzione tra i software che forniscono le stesse funzionalità**. Migliorare una qualità comporta la riduzione di un'altra, comportando dei contrasti tra di loro.Sono definiti come le proprietà del sistema. Sono critici tanto quanto quelli funzionali.dei requisiti >**Requisiti di prodotto** (Capacità del sistema)
- >**Requisiti Organizzativi** (Standard di documentazione)
- >**Requisiti  Evento** (Standard di accessibilità)
### 9.2 Quality and Meters

È necessario **definire delle metriche** per misurare i valori di qualità del software. Tutto ciò che è misurabile è definibile requisito qualitativo (non-funzionale).

>[!question] **Domande di un requisito qualitativo**
>- Come e quando possiamo dire che il requisito sia soddisfatto oppure no?
>- Come potrebbe essere rivista la specifica per renderlo verificabile?

Molti di questi requisiti sono **molto difficili e costosi da soddisfare** e alcune metriche sono difficili da definire. In oltre alcune qualità possono essere **inversamente proporzionali**.

>[!info] Definizione di una metrica
Le metriche rientrano nel dominio booleani con i valori:
> - 0: Nessun guasto
> - 1: Guasto rilevato
## 9.3 Qualità di un sistema
>[!info]- Reliability (Affidabilità)
Un sistema è affidabile se un utente può confidare nel suo comportamento. L'affidabilità è misurabile dal numero di errori manifestati in un certo numero di prove. (La percezione dell'affidabilità può variare da utente a utente)

>[!info]- Robustness (Robustezza)
Misura del comportamento del software in circostanze non previste.

>[!info]- Efficiency (Efficienza)
Misura le risorse necessarie al software per svolgere i propri compiti. Un software è efficiente se svolge dei compiti utilizzando una quantità di risorse minima.
Le prestazioni di un software si misurano col tempo impiegato nello svolgimento di un compito.
È possibile misurare l'efficienza di un software in vari modi:
> - misurazioni a run time
> - analisi
> - simulazione
> 
> Lo studio dell'efficienza può avere tre esiti: ottimo, medio, pessimo.

>[!info]- Usability (Usabilità)
Consiste nella semplicità che il software offre nel suo utilizzo. Ciò è definito dalla metrica **"tempo"**, in minuti o secondi. Misura in quanto si riesce a capire ed utilizzare il sistema. Ciò permette di **valutare tutti i fattori soggettivi**.

>[!info]- Verificabilità
La metrica utilizzata sono i numeri di input che fornisco la controllabilità e la osservabilità dei meccanismi di interazione. Più ne ho più sono testabili.

>[!info]- Manutenibilità
Possibilità di modificare il prodotto una volta rilasciato, adattandolo alle richieste dell'utente.

>[!info]- Riusabilità
Capacità e semplicità di un componente software nell'essere adoperato in contesti diversi.

>[!info]- Portabilità
Quanto è facile installare e utilizzare un software in contesti e piattaforme diverse.

>[!info]- Comprensibilità
Semplicità nell'individuare le responsabilità dei singoli componenti software.

>[!info]- Interoperabilità
Capacità del software di interagire con altri software. (La standardizzazione è fondamentale in questo contesto)
## 9.4 Qualità di un processo di sviluppo
>[!info]- Produttività
Efficien
za e velocità nel rilascio di un prodotto.

>[!info]- Timeliness
Rispetto delle scadenze.

>[!info]- Visibilità
Gli attori che partecipano allo sviluppo sanno a che punto dello sviluppo si trovano, attraverso una precisa definizione di eventi di transizione. (Importante soprattutto in team di sviluppo volatili)
## 10.0 Check the software validation
Capire se il nostro software risolva il problema che viene richiesto dal cliente e se lo fa nel modo "**correttamente**", confrontando il sistema software sviluppato, rispetto a quello che è stato descritto nei modelli e nei documenti dei requisiti software.

La validazione viene fatta con l'aiuto dell'utente finale, **concentrandosi sull'esigenza dell'utente e se il prodotto è coerente con la sua richiesta**, nella verifica si va a controllare se il nostro software che abbiamo sviluppato esegue gli output che abbiamo definito.  

### 10.1 Approaches of the verifiction and validation

+ **Approccio statico**: analisi statica dei codici sorgenti e altri documenti di progetto, verificando la conformità del sistema.
  
+ **Approccio dinamico**: testing - tramite l'utilizzo di test si eseguire il software e si scoprono i difetti.

- **Debugging**: capire dove si trova il guasto nel nostro sistema software, capire dove si riscontra il problema e risolverlo.  

### 10.2 Genesis of Failures 
Il *fallimento** è la manifestazione del guasto con un'osservazione di un funzionamento scorretto del programma.

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

[^1]: L’**elicitazione** è il processo di estrazione di **informazioni**, conoscenze o requisiti da una fonte, solitamente attraverso tecniche di intervista, osservazione o brainstorming, for more info go there [definizione elicitazione](https://www.edizionigoree.it/significato-elicitazione-definizione-etimologia/)
[^2]: **Pareto principle**: regola dell'80/20 dove l'80 percento delle conseguenze vengono dal 20 percento delle cause for more go to here [Pareto Priciple](https://en.wikipedia.org/wiki/Pareto_principle) 
[^3]: **gasp**: termine in inglese che significa che ci sono degli aspetti poco chiari dell'intervista
