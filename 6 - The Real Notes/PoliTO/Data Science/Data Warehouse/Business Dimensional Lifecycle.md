---
created: 2026-02-28
tags:
  - baby
topics:
  - Data
  - DataWareHouse
author: Danilo Quattrini
---
# Introduzione
---
## Questions
- Quali sono gli elementi fondamentali per progettare una DW?
- Come si realizza una DW? Qual'è l'approccio migliore?
### Business Dimensional Life Cycle
- Che cos'è e perché viene utilizzato?
- Macro-fasi del Business Dimensional Life Cycle
- **Il Lifecycle:** Quali sono i 3 binari che vengono sviluppati in parallelo durante la fase di _Progettazione_ del Business Dimensional Lifecycle?
- **Progettazione dei Dati:** In quale ordine logico (dal più astratto al più concreto) si sviluppano i 4 passaggi della progettazione dei dati (Fisica, Concettuale, ETL, Logica)?
- **Top-Down vs Bottom-Up:** Qual è il vantaggio principale dell'approccio _Bottom-Up_ rispetto al _Top-Down_?
- **I Requisiti:** Se il Direttore Vendite ti dice _"Voglio vedere il fatturato totale diviso per regione su base mensile"_, si tratta di un requisito _Applicativo_ o _Strutturale_? Perché?
- **Livelli Architetturali:** In base a quale requisito strutturale viene scelta la complessità dell'architettura (es. a 2 o a 3 livelli)?
---
## Che cosa serve per progettare una DW?
Quali sono gli aspetti da considerare per progettare una data warehouse.
- **Aspettative elevate da parte degli utenti**, cioè usano le DW per poter trovare delle soluzioni dei problemi aziendali.
- **Qualità dei dati e dei processi** **OLTP** di partenza, dove ci sono dei dati incompleti o inaffidabili, con dei processi aziendali non integrati e ottimizzati.
- Gestione “politica” del progetti: accettazione del sistema da parte degli utenti finali e collaborazione con i “detentori” dell’informazione (esempio creare un contratto tra l'azienda che offre un servizio e l'utente finale e fare accordi con le persone che detengono le informazioni al fine di poter creare il sistema). 

## Come si fa a realizzare una DW?
Ci sono due approcci:
- **Top Down**: in questo approccio si va a realizzare una data warehouse che da una visione globale e completa dei dati aziendali, che però comportano costi significativi e tempi di realizzazione lunghi. Richiede una visione troppo distesa e a lungo termine.
- **Bottom Up**: In questo approccio si va a creare la DW con un'insieme di [[Elementi di una Data Warehouse#Data Mart|Data Mart]], su diversi settori specifici che riducono i costi di realizzazione. Partiamo da un concetti circoscritti che sono separate tra di loro che possiamo unire.

 Qui sotto una tabella riassuntiva.

| **Approccio**           | **Metodologia**                                                                                                                                        | **Vantaggi**                                                    | **Svantaggi**                                                                                                           |
| ----------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------ | --------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------- |
| **Top-Down** (Inmon)    | Progetti e costruisci subito l'**intera DW aziendale** globale e integrata. Solo dopo crei i Data Mart per i singoli reparti.                          | Visione globale e coerente fin dal primo giorno.                | **Lento e costosissimo.** Rischio elevato di fallimento perché richiede troppo tempo prima di vedere i primi risultati. |
| **Bottom-Up** (Kimball) | Progetti prima **singoli Data Mart** (es. solo Vendite, poi solo Marketing) su contesti circoscritti e infine li unisci mediante dimensioni condivise. | **Economico e rapido.** Risultati subito visibili (Quick Wins). | Rischio di creare "isole di dati" separate se non sono ben coordinati.                                                  |
## Che cosa si fa per creare la DW?
![[Screenshot 2026-09-28 at 17.51.11.png]]
Per la realizzazione di una DW si esegue un Framework chiamato **Business Dimensional Lifecycle** che segue le seguenti macro fasi:

**Definizione Dei Requisiti (Ascolto)**
Ci sono delle interviste che vengono svolte a degli utenti che ci forniscono dei requisiti e richieste oppure i requisiti che il sistema deve soddisfare. 

**Fase di Progettazione**
Si svolgono delle decisioni in ambito di progettazione in diversi ambiti:
- **Infrastruttura / Tecnologia**: è necessario progettare l’architettura del sistema hardware (hw) e vanno selezionati quali prodotti software utilizzare (sw)
- **Dati** (il cuore della DW) qui si va a modellare il dato, dal **concetto più astratto a quello concreto**:
	- **Concettuale**: modellazione dimensionale mediante la quale devono essere definite le dimensioni di analisi, le metriche e le gerarchie delle dimensioni di analisi.
	- **Logico**: Traduci il modello concettuale in uno _Schema Logico Relazionale_ (es. schema a stella o fiocco di neve).
	- **Progettazione ETL**: Disegni come pulire, trasformare e riconciliare i dati dalle sorgenti eterogenee.
    - **Fisica**: Decidi come salvare i dati sui dischi (indici, viste materializzate) per fare in modo che le query siano velocissime
- **Applicazione:** Crei le dashboard, i report e gli strumenti di Data Science che userà l'utente.

**Attuazione**
 il sistema viene deployato, durante l’utilizzo potrebbero venir fuori nuovi requisiti che non sono stati considerati per i quali si torna in fase di progettazione

**Manutenzione & Monitoraggio**
Durante l'utilizzo dell'applicazione bisogna fare un'azione di monitoraggio, dove si vanno a capire le esigenze che la DW ha bisogno di soddisfare.

## Progettazione di Data Mart
Su un contesto azienda specifico andiamo ad applicare l'approccio bottom-up![[Screenshot 2026-09-28 at 17.57.22.png]]
1. **Requisiti Utente**: caratteristiche del sistema che voglio soddisfare, cioè che cosa deve fare lo strumento, il focus sono i dati, l'attenzione va posta sempre sui dati. Bisogna però partire dai requisiti dell'utente, cioè che tipo di analisi bisogna supportare e i dati necessari per supportare l'analisi.
   Dobbiamo trasformare i requisiti in un'insieme di specifiche più dettagliate, andando a capire quali sono le metriche da caratterizzare e i valori da predire.

2. **Progettazione Concettuale**: creare uno schema di fatto, sintetizza i dati che ho bisogno per l'analisi il modello multidimensionale che ne viene fuori contiene le dimensioni di analisi, le misure e le diverse gerarchie sulle dimensioni.
3. **Progettazione Logica**: Che va a define uno schema logico relazione, che deve essere alimentato da una schema di fatto, che vado ad inserire le informazioni utili per l'analisi
4. **Progettazione del Processo ETL**
5. **Progettazione Fisica**: step di progettazione che decide come i dati devono essere memorizzati sul disco e accesso sui dati, server per ottimizzare l'accesso ai dati in termini di tempo di esecuzione, lettura e scrittura su di essi. Per l'accesso immediato si usano strumenti accessori viste materializzate (query pre-compilato) o indici
6. **Riconciliazione**: vista comune sui sistemi informativi che rappresentano le sorgenti. Stessi dati che però vengono da contesti differenti. 
## Analisi dei requisiti
L’analisi dei requisiti consiste nell’effettuare delle interviste mirate agli utilizzatori del sistema
(business users) e a coloro che detengono le informazioni delle sorgenti (amministratori del sistema informativo) e nello scegliere uno o più data mart che faranno parte del progetto pilota. I data mart scelti devono essere strategici prevedendo un ritorno economico per l’azienda e devono essere alimentati da poche sorgenti affidabili. 
Distinguiamo due tipi di requisiti:
### Requisiti applicativi (Cosa vuole l'utente?)
Fatti, dimensioni e granularità temporale descrivono gli eventi di interesse, l’intervallo di storicizzazione e il carico di lavoro che caratterizzano i dati relativi al settore dell’azienda in cui vogliamo implementare il data mart, analizzando le dimensioni di interesse (KPI di interesse). Sono caratterizzati dal caricato del lavoro, cioè quali sono gli attori che ci frequentano e quanto il sistema deve sopportare.
### Requisiti Strutturali
**Periodicità dell’alimentazione**: Dato elaborato e trasferito in un determinato tempo in modo frequente, dove l'architettura può essere di due o tre livelli.

**Spazio disponibile**: stima dello spazio richiesto dal DW considerando anche la sparsità dei dati e dello spazio previsto per garantire maggiore efficienza, offerta dalla progettazione fisica (strutture accessorie come indici e viste materializzate)

**Tipo di architettura del sistema**: la scelta del numero di livelli è legata alla complessità del processo di ETL e al volume di dati da trasferire periodicamente

**Pianificazione del deployment**: fase di avviamento del progetto seguita da una fase di formazione degli utilizzatori del sistema
# Reference
---

