---
created: 2026-09-28
tags:
  - baby
topics:
  - Data
  - DataWareHouse
  - "[[School]]"
author: Danilo Quattrini
---
# La Struttura di una Data Warehouse
---
## Questions
### **Sorgenti di Dati e Integrazione**
- Quali sono le Componenti di una DW?
- Quali sono le principali tipologie di sorgenti di dati da cui attinge un Data Warehouse (DW)?
- Perché le sorgenti rappresentano una sfida (warning) e quali operazioni di preelaborazione sono necessarie prima di integrare i dati nel DW?
### **Warehouse Aziendale vs Data Mart**

- Qual è il ruolo del Warehouse Aziendale (DW) e quali servizi offre agli utenti?
- Che cos'è un Data Mart e da quali due sorgenti differenti può essere alimentato?  
- Qual è la criticità/complicanza associata all'aggiornamento dei Data Mart derivati dal DW?
### **Server OLAP e Strumenti ETL**

- Quali sono le funzioni principali dei Server OLAP (ROLAP, MOLAP, HOLAP)?
- In quali due momenti temporali vengono eseguiti gli strumenti ETL?
- Descrivi le 4 fasi della pipeline ETL (Estrazione, Pulitura, Trasformazione, Caricamento) ed esplicita cosa avviene in ciascuna.
### **Metadati**
- Quali sono i 3 tipi di metadati descritti nel testo e cosa descrive ciascun tipo?
## Livelli DW
- Quali sono i Livelli della DW?
- Spiega il livello 2 in che cosa consiste e perché viene utilizzato?
- Pregi e difetti del livello 2 della DW.
- Spiega il livello 3 in che cosa consiste e perché viene utilizzato?
- Pregi e difetti del livello 3 della DW.
---
# Struttura di una DW
![[Screenshot 2026-09-28 at 11.12.40.png]]
Gli elementi fondamentali che sono parte di una Data Warehouse sono le seguenti:
- [[#Sorgenti di Dati|Sorgenti di Dati]]
- [[#Warehouse Aziendali|Warehouse Aziendale]]
- [[#Data Mart|Data Mart]]
- [[#Server OLAP|Server OLAP]]
- [[#Strumenti ETL|Strumenti ETL (Extract, Transform, Load)]]
- [[#Metadati|Metadati]]
## Sorgenti di Dati
Sono le **fonti esterne** da cui il DW preleva i dati. Possono essere:

- Database operativi aziendali (es. gestionale, CRM, ERP).
- File Excel, CSV.
- Feed esterni (es. social media, API, dati di mercato).
- Log di sistema, transazioni web.
    
>[!warning]
>Le sorgenti sono **eterogenee** (formati diversi, strutture diverse). Il DW deve integrarle in un formato coerente. Questa integrazione può essere svolta tramite un preelaborazione sui dati stessi (pulizia, rimozione ridondanze, integrazione e così via).

## Warehouse Aziendali (DW)
Sarebbe il cuore del sistema il database aziendale dove ci sono tutte le informazioni utili per svolgere le analisi OLAP, **dati storici** appuratamente ripuliti ed integrati dalle varie sorgenti. Oltre ad archiviare i dati sono utili perché offrono servizi di query analitiche agli utenti.

## Data Mart
Il data mart è un sottoinsieme della DW, che si concentra su un determinato aspetto o dominio che l'azienda vuole analizzare (es. marketing, vendite, finanza e così via). I **Data Mart**, possono provenire da due differenti sorgenti:
1. **Alimentato Dalla DW**: cioè sono una copia più ridotta della DW.
2. **Alimentato Dalle Sorgenti**: le sorgenti oltre ad inviare dati alla DW, le possono inviare direttamente alle Data Mart facendo parte della DW.
>[!danger] Occhio
>Solitamente le Copie delle DW se vengono aggiornate con nuovi dati, dovranno aggiornare anche a loro volta i Data Mart, risultando quindi un processo che può portare errori o complicanze.

## Server OLAP
I motori che eseguono le **query analitiche** ([[Analisi Data Warehouse#Analisi OLAP|ROLAP, MOLAP, HOLAP]]).
**A che cosa servono?**

Servono a:
- Calcolare aggregazioni complesse.
- Supportare operazioni OLAP ([[Analisi Dei Dati#Analisi OLAP|drill-down]], roll-up, slice, dice ==Collegare con i vari concetti spiegati==).
- Rendere veloci le query su grandi volumi di dati.
## Strumenti ETL (Execute Transform Load)
---
Sono degli strumenti che vengono utilizzati per poter ripulire ed integrare i dati nella DW, questi strumenti **vengono eseguiti in due momenti** :
1. **Al primo popolamento della DW** (Quando vengono caricati i dati per la prima volta)
2. **Aggiornamento Periodico**

Le fasi per la trasformazione dei dati è la seguente:

| Fase                  | Cosa succede                                                                       | Esempio                                                                                                |
| --------------------- | ---------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------ |
| **1. Estrazione**     | I dati vengono acquisiti dalle sorgenti (database, file, API, log, sistemi IoT).   | Leggo tutte le vendite dal database gestionale.                                                        |
| **2. Pulitura**       | I dati vengono puliti per migliorare qualità, consistenza e correttezza.           | Correggo formati di data, rimuovo duplicati, gestisco valori nulli.                                    |
| **3. Trasformazione** | I dati vengono convertiti dal formato operazionale a quello del DW (integrazione). | Unisco dati da più fonti, calcolo nuovi campi (es. margine = prezzo - costo), applico regole business. |
| **4. Caricamento**    | I dati trasformati vengono propagati nel Data Warehouse.                           | Inserisco i dati nella tabella dei fatti del DW.                                                       |
L'ETL è una pipeline (serie di fasi) che porta i dati dalle sorgenti al DW, pulendoli e trasformandoli lungo il percorso.
## Metadati
Più nel dettaglio viene descritto in questa parte [[Knowledge Discovery Process#Metadata|here]] dove descrivo in dettaglio cosa sono, in breve sono dati che descrivono altri dati, ma nella DW sono divisi in 3 tipi:

| Tipo                             | Cosa descrive                                                                     | Esempio                                                                    |
| -------------------------------- | --------------------------------------------------------------------------------- | -------------------------------------------------------------------------- |
| **Trasformazione e caricamento** | Le sorgenti e le trasformazioni applicate.                                        | “Il campo `data_vendita` viene convertito da `DD/MM/YYYY` a `YYYY-MM-DD`.” |
| **Gestione dei dati**            | La struttura dei dati nel DW (tabelle, colonne, relazioni, dati derivati).        | “La tabella `Fact_Vendite` ha una chiave esterna su `Dim_Prodotto`.”       |
| **Gestione delle query**         | Informazioni sulle query eseguite (SQL, uso di CPU/memoria, tempi di esecuzione). | “La query X ha impiegato 2 secondi e usato 500 MB di RAM.”                 |
# Livelli di una DW
Per livello (o tier) ci riferiamo alla **struttura dei moduli e degli strati intermedi di memoria/elaborazione** situati tra i sistemi operativi operazionali (OLTP, quelle a sinstra dell'immagine) e le applicazioni analitiche aziendali.
Ci sono due livelli distinti per rappresentare la struttura di una data warehouse:
## A due livelli
![[Screenshot 2026-10-04 at 12.10.10.png]]
### Come funziona
I dati vengono estratti direttamente dalle sorgenti eterogenee, trasformati "in corsa" (_on-the-fly_ in memoria) e caricati immediatamente nel DW target.
$$\text{Sorgenti Dati (OLTP / File / API)} \xrightarrow{\quad \text{ETL Direct / On-the-Fly} \quad} \text{Data Warehouse Aziendale (DW)}$$
>[!done] Vantaggi
>**vantaggi** fondamentali (rispetto a non avere un DW) sono:
>- Disaccoppiamento tra il **carico transazionale** (OLTP) e il carico analitico (OLAP).
>- Gestione indipendente delle differenti granularità temporali (dati storici vs dati operativi).

>[!warning] Svantiggio
>Poiché non esiste uno spazio intermedio su disco dove salvare gli stati intermedi:
>- **Tutta le fasi di ETL deve avvenire in un'unica transazione continua.**
>- Se la pipeline fallisce al 99% (es. per un errore di rete o un record corrotto), **l'intero processo viene bloccato e deve ripartire da zero** (rollback totale).
>- Imponendo un carico immediato ed estrazione continua sulle sorgenti operazionali, si rischia di saturare la banda dei database aziendali di produzione.
>

## A tre livelli
![[Screenshot 2026-10-04 at 12.26.16.png]]
In quest’architettura viene inserito un **livello intermedio di persistenza temporanea**: la **Staging Area** (o Operational Data Store - ODS).

>[!done] Separazione dell'Estrazione ($\mathbf{E}$) dal Caricamento ($\mathbf{L}$):
>-  L'estrazione ($\mathbf{E}$) dalle sorgenti di produzione può avvenire in finestre temporali veloci ed efficienti (es. di notte o a blocchi). I dati grezzi vengono "scaricati" così come sono nella Staging Area.
>- Una volta messi in sicurezza nella Staging Area, le operazioni pesanti di pulitura, riconciliazione e trasformazione ($\mathbf{T}$) avvengono **senza toccare o appesantire i database di produzione**.
>

>[!done] Tolleranza ai guasti (Fault Tolerance) e Ripristino
>Se il caricamento o la trasformazione falliscono, **non occorre ri-estrarre i dati dai sistemi sorgente**. I dati grezzi/intermedi sono già salvati nella Staging Area; basta rilanciare la trasformazione a partire da lì.

>[!done] **Integrazione e Pulizia Complessa:**
Permette di eseguire query SQL complesse di join, deduplica, controllo di integrità referenziale e arricchimento su grandi moli di dati eterogenei prima che arrivino alla struttura finale del DW.

>[!error] Problemi 
>- **Ridondanza di Storage:** I dati vengono salvati due volte (nella Staging Area e poi nel DW).
> - **Maggiore Complessità Architetturale:** Bisogna gestire e mantenere un'infrastruttura/database aggiuntivo.
# Reference
---

