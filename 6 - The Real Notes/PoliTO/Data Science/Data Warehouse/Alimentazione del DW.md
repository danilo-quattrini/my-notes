---
created: 2026-10-07
tags:
  - baby
topics:
  - Data
  - DataWareHouse
  - "[[School]]"
author: Danilo Quattrini
---
# Alimentazione del DW
---
## Questions
- Come si preparano i dati per essere caricati nelle DW?
- Quali sono le fasi dell'alimentazione della DW?
### Estrazione
- Come funziona l'estrazione?
- Che tipologie di estrazione ci sono?
- Che dati vengono presi per la storicizzazione?
- Come può avvenire l'estrazione incrementale?
# Definizioni
--- 
Il processo di **Extraction, Transformation and Loading** (ETL) è il processo di preparazione dei dati da introdurre nel DW che è composto da estrazione dei dati dalle sorgenti, pulitura, trasformazione e caricamento. Questo processo **viene eseguito sia durante il primo popolamento** del DW comunicando prima di tutto le dimensioni, e poi la tabella dei fatti sia durante l’aggiornamento periodico dei dati.

## Estrazione
Durante la fase di estrazione avviene l’acquisizione dei dati dalle sorgenti, può avvenire secondo due diverse modalità:
- **Statica**: viene eseguita una fotografia dei dati dalle sorgenti, questà modalità viene utilizzata per il primo popolamento del DW 
- [[#Estrazione Incrementale|Incrementale]]: vengono presi in considerazione solo i dati nuovi o quelli aggiornati rispetto all’ultima estrazione, questa modalità viene utilizzata per l’aggiornamento periodico del DW.
In questa fase è importante avere a disposizione ed estrarre dati di **qualità**.

L’estrazione può avvenire su dati operazionali di natura diversa:
- **Storicizzati**: ogni operazione o modifica è memorizzata in maniera puntuale e per un periodo definito di tempo all’interno del sistema OLTP
- **Semi-storicizzati**: nel sistema OLTP viene memorizzato solo un numero limitato di stati, l’estrazione incrementale è più complessa da effettuare
- **Transitori**: il sistema OLTP mantiene solo l’immagine corrente dei dati, l’estrazione diventa operativamente molto complessa (es tabelle che contengono le scorte del magazzino)

### Estrazione Incrementale
L’estrazione incrementale può avvenire mediante tramite l'**assistenza di un applicazione che cattura le modifiche**, l’**uso di log** che storicizzano le modifiche, dei [^1]**trigger** che catturano le modifiche di interesse oppure l'**utilizzo di un timestamp** che marcano l’ultima modifica nel contesto di un record, richiede la modifica dello schema della base di dati e può perdere stati intermedi di modifica
![[Screenshot 2026-10-07 at 12.37.15.png]]
## Pulizia
Durante la fase di pulitura vengono eseguite operazioni volte al miglioramento della qualità dei dati, si opera su:
- Dati duplicati
- Dati mancanti
- Uso non previsto di un campo
- Valori impossibili o errati
- Inconsistenza fra valori logicamente associati

>[!info] Perché ci sono tali problemi?
>Questi problemi possono essere dovuti ad errori di battitura, differenze di formato dei campi o all’evoluzione del modo di operare dell’azienda.

Le tecniche di **data cleaning** o **data quality**:
 - **Tecniche basate su dizionari**: adatte per attributi con un dominio ristretto che presentano errori di battitura o formato
 -  **Tecniche di fusione approssimata**: adatte per il riconoscimento di duplicati/correlazioni tra dati simili:
	 - **Join approssimato:** viene fatta una join utilizzando gli attributi comuni che non rappresentano un identificatore (chiave)
	 - **Purge/merge**: i dati presenti in due diverse tabelle di partenza vengono uniti in una sola tabella, necessita l’identificazione e l’eliminazione dei dati duplicati e la gestione di due attributi simili ma in un formato diverso
- **Identificazione di outliers** o deviazioni mediante business rules
La strategia migliore è la prevenzione, rendendo più affidabili e rigorose le procedure di data entry OLTP.

**Join approssimato**
![[Screenshot 2026-10-07 at 12.46.25.png]]

**Purge / Merge**
![[Screenshot 2026-10-07 at 12.47.03.png]]

**Esempio di Pulitura**
![[Screenshot 2026-10-07 at 12.48.03.png]]

## Trasformazione
Durante la fase di trasformazione i dati vengono convertiti dal formato operazionale a quello del DW, ciò richiede una rappresentazione uniforme del dato che avviene in due fasi:
-  Sorgenti operazionali => Dati riconciliati (nella staging area):
	- Conversioni e normalizzazione
	- Matching
	- Eventuale filtraggio dei dati significativi
- Dati riconciliati => DW:

- Generazione di chiavi surrogate e di valori aggregati

## Caricamento
Durante la fase di **caricamento** gli aggiornamenti vengono propagati al DW, per mantenere
l’integrità le modifiche vengono effettuate nel seguente ordine:
1. Dimensioni
2. Tabella dei fatti
3. Viste materializzate

### Tabelle delle dimensioni
![[Screenshot 2026-10-07 at 12.53.33.png]]
- L’identificazione degli aggiornamenti
- L’individuazione della chiave surrogata mediante una tabella di lookup
- L’aggiornamento dei dati nella tabella delle dimensione

### Tabelle Dei Fatti
![[Screenshot 2026-10-07 at 12.54.50.png]]
- L’identificazione degli aggiornamenti
- L’individuazione della chiave surrogata relative alle dimensioni mediante tabelle di look-up
- Inserimento delle misure e caricamento nelle tabelle dei fatti

# Reference
---
[^1]: Un **trigger** in SQL è una procedura memorizzata nel database che viene **eseguita automaticamente** ("attivata") in risposta a uno specifico evento, come un inserimento (`INSERT`), una modifica (`UPDATE`) o un’eliminazione (`DELETE`) dei dati in una tabella. Servono principalmente per automatizzare controlli, calcoli o la registrazione di un registro delle modifiche (audit log).
