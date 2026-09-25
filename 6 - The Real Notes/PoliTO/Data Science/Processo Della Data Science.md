---
created: 2026-09-22
tags:
  - baby
topics:
  - Data
  - BigData
  - "[[School]]"
author: Danilo Quattrini
---
# Processo Della Data Science
---
I dati spesso devono essere mostrati in maniera differente in base alle esigenze del cliente, questo per catturare l'attenzione delle persone che sta analizzando tali dati. Questa viene definita come **tecnica della data visualization**.

Il data scientist deve conoscere i dati che si ha a disposizione e capire che strumenti che ha a disposizione. I dati prima che vengono messi a disposizione dal data scientist devono seguire un processo, questo processo viene definito come **Processo Della Data Science**.
![[Screenshot 2026-09-22 at 17.50.55.png]]
## Fasi di processo della Data Science
Le fasi sono le seguenti
- [[#Generation (Generazione)|Generazione]]
- [[#Acquisizione (Acquisition)]]
- [[#Memorizzazione (Storage)]]
- [[#Analisi (Analytics)]]
### Generation (Generazione)
La generazione viene intesa come la risorsa o l'utente che esegue un azione che va a generare dati.

I dati possono essere generati in diversi modi, tali modi sono.
- **Generazione Attiva**: l'utente che crea dei post o video, per esempio, sono persone che in modo attivo, creano dei dati sulle diverse piattaforme.
- **Registrazione Passiva**: I dati che non sono generati in modo attivo da un utente, ma sono dati che vengono raccolti da operazioni / transizioni involontarie dell'utente, file di log (ad esempio accettare i cookie su un sito web).
- **Produzione automatica**: I dati vengono generati da strumenti IoT, cioè come per esempio sensori.

### Acquisizione (Acquisition)
La fase in cui si vanno a raccogliere i dati dalle risorse che generano tali dati, possono essere [[Acquisizione Dei Dati|Push Based]] e [[Acquisizione Dei Dati|Pull Based]], dai link seguenti si possono vedere le differenze tra push based e pull based.

Oltre alla raccolta / acquisizione dei dati, nelle fonti che la generano, nella fase di acquisizione si va inoltre **a Trasmettere i dati verso uno specifico data center tramite dei collegamenti veloci**. 

Inoltre per concludere il dato prima di essere storicizzato si svolge una **Preelaborazione**, dove si vanno a pulire i dati dal [[Knowledge Discovery Process#Rumore (Data Noise)|rumore]], integrare altri dati con dati di diversi fonti.

### Memorizzazione (Storage)
Si usano delle **infrastrutture di memorizzazione** per salvare i dati che si sono acquisiti, memorie locali (HDD, SSD) oppure memorie di rete (NAS, DAS) e si vanno ad installare dei sistemi di supporto per gestire tali dati come file systems, struttura dati chiave-valore, DB column-oriented, DB a documenti (MongoDB).

### Analisi (Analytics)
Sono divisi in 3 macro categorie:
- **Descrizione Analitica**: effettuano una caratterizzazione del dato, cioè descrivono il dato e la sua natura, dando dei label o dei [[Knowledge Discovery Process#Metadata|metadati]].
- **Predittivo**: da un set di dati, vedo in che categorie fanno ed addestro un algoritmo di classificazione, smistando il dato nelle diverse categorie (concetto del [[Supervised And Unsupervised|supervised]]).
	- **classificazione**: previsione del dato da dare ad un'etichetta
	- **previsione**: previsione di un valore numero
- **Prescrittivo**: un'algoritmo predittivo + una tecnica di ottimizzazione cioè ottimizzare il risultato dell'algoritmo predittivo.

Porre le domande giuste è importante per ottenere una corretta modellazione. Bisogna pensare a come adattare l'algoritmo alla caratteristiche dello Use Case che stiamo analizzando. Ci sono algoritmi predittivi che ci servono per poter estrarre valore nei dati o informazioni nascoste dai dati che sono generati.
# Reference
---

