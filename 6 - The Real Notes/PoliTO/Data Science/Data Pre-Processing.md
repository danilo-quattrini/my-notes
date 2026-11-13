---
created: 2026-10-19
tags:
  - baby
topics:
  - Data
  - AI
  - Data Mining
author: Danilo Quattrini
---
# Data Pre-Processing
---
## Questions
- Che cosa sono gli attributi e i tipi degli attributi?
- Elenca i tipi di attributi che ci possono essere.
- Differenza tra attributi continui e discreti.
- Vengono considerati gli attributi ID e quelli identificativi in un dataset?
- Come si gestisce la qualità del dato in un dataset?
- Quali sono gli approcci che vengono utilizzati in un dataset per rimuovere i dati che sono ridondondanti?
---
## Introduzione
Ci sono 4 macro argomenti:
- Tipi di Dato e Proprietà
- Tecniche di Data Preparazione e Trasformazione
- Analizzare le [[Similarità e Dissimilarità|similarietà]] / distanza (quella euclidea) e le [[Similarità e Dissimilarità|dissimilarietà]], cioè scegliere la metrica adatta per l'analisi.
- Analizzare la correlazione tra due attributi, che va fatta sempre su ogni data-set da processare

## Tipi di Dato e Proprietà e Strutture
Si intende una collezione di oggetti di dato (righe di una tabella), che è caratterizzato da uno e più attributi (colonne della tabella).

Che possiedono dei tipo che possono variare dal: categorico, numerico, ecc.... Dove l'attributo può assumere valori diversi in base al dominio.
![[Screenshot 2026-10-19 at 18.17.12.png]]
### Proprietà
L'oggetto può essere uguale o distinto, si possono fare operazioni di moltiplicazione, addizione, divisioni... ordinamenti e così via, questo però dipende dal tipo di attributo che si possiede. 
![[Screenshot 2026-10-19 at 18.19.34.png]]
### Scala di misura degli attributi
Come vediamo nell'immagine sopra ogni attributo in base alle operazioni che possiede viene definito in un certo modo, andiamo a vedere i tipi di attributo:

- **Nominali**: sono caratterizzati da valori che possono essere o uguali tra loro oppure diversi ($=$ or $\not=$)
  >[!example]
  >Colore degli occhi, CAP, Stato civile, Genere

- **Ordinali**: che definiscono un ordine crescente o decrescente ($<, >, \le, \ge$), **tale ordine però non è quantificabili tramite numeri**.
  >[!example] 
  >Titolo di studio (Licenza media $<$ Diploma $<$ Laurea), Livello di gradimento (Basso, Medio, Alto), non posseggono dei valori numerici veri e propri ma sono delle *gerarchie*

- **A Intervallo (Quantitativi/Numerici):** Valori numerici in cui le differenze hanno un significato preciso, ma lo zero è arbitrario (non indica assenza della quantità)
  >[!example]
  >Temperatura in °C (0 °C non significa "assenza di calore", e 40 °C non è il "doppio" di 20 °C in termini termodinamici), Date del calendario.
  
  - **A Rapporto / Ratio (Quantitativi/Numerici):** Valori numerici con uno zero assoluto reale (assenza del fenomeno), esempio valori che sono identificati come $0$ non sono valori nulli se si parla di gradi centigradi 
### Attributi continui o discreti
Ci sono due categorie di attributi che sono rappresentabili come:

- **Discreti**: Valori finiti o numerabili (es. numero di figli, punteggio di un dadi). Spesso rappresentati come interi.
  
- **Continui**: Valori reali compresi in un intervallo (es. altezza, tempo di esecuzione). Rappresentati da numeri con virgola (float).

### Attributi Complicati
Valori come matricola o identificativi vengono ignorati, perché sono complessi e non necessari per l'analisi, capire quali sono gli attributi rilevati o no.

Sono per esempio: `ID_Cliente`, `Matricola`, `Codice_Fiscale`

### Tipi di Dati
- **Dati tabellari**: come documenti o transizioni.
  
- **Dati a forma di grafi**: insieme di relazioni che ci sono fra i vari dati.

- **Dati Transazionali:** Insiemi di elementi (_itemset_) acquistati o registrati insieme (es. carrello del supermercato).

- **Dati a Temporali / Ordinati / Tecnologici** : dati spaziali o temporali che rappresentano una sequenza di operazioni o generici.
#### Documento
I documenti sono dei tipi di dato [[Categorie Di Dati#Dati Semi-Strutturati|semi-strutturati]] oppure anche  [[Categorie Di Dati#Dati Non-Strutturati|non-strutturati]], dove il testo all'interno di un documento può essere organizzato in diversi modi. Il dato testuale può essere convertito da semi-strutturato ad un dato [[Categorie Di Dati#Dati Strutturati|strutturato]], facendo un operazione di pre-processing, **tramite una struttura matriciale**, dove ogni riga indica il documento, mentre le colonne sono le parole presenti nel documento, ogni cella indica il numero delle volte che le parole appare dentro al documento (come un counter di parole utilizzato in big data).![[Screenshot 2026-10-19 at 18.27.54.png]]

#### Dati Transazionali
Un dato speciale dove ogni record di una tabella è una transazione che involve un insieme di dati.

>[!example] Esempio
>Prendiamo le vendite di un supermercato.  La tabella sotto mostra l'insieme dei prodotti acquistati dai vari clienti durante la spesa, che sono separate dalle diverse transizioni.
![[Screenshot 2026-10-19 at 18.32.37.png]]

#### Dati a Forma di Grafi
![[Screenshot 2026-10-19 at 18.34.47.png]]I grafi rappresentano nell'immagine sopra che sono dei collegamenti a dei concetti tramite l'utilizzo dei nodi

#### Dati Ordinati
Qui c'è una sequenza di transazioni, dove però non hanno un ordine, ogni evento è una transazione atomica che non hanno significato di ordine.
![[Screenshot 2026-10-19 at 18.36.37.png]]

#### Dati Spaziali
![[Screenshot 2026-10-19 at 18.37.37.png]]

## Qualità del Dato
La qualità del dato è importante perché può impattare l'analisi e portare risultati sbagliati. **Nella fase di pre-processing i dati che non sono di qualità vanno eliminati**, meglio toglierli che mantenerli insieme.
### Quali sono i problemi in termini di qualità del dato?

Qui si parla del concetto di [[Knowledge Discovery Process#Rumore (Data Noise)|Rumore]] e Outliers, che quest'ultimi possono essere rimossi tramite algoritmi appositi che li individuano e li tolgono (outlier-detection), oppure altri algoritmi che sono citati [[Knowledge Discovery Process#Tecniche per rimuovere il rumore|qui]].

Anche l'assenza di valore è un problema, questo perché il dato manca oppure non è stato raccolto. Devo vedere la quantità dei missing value presenti nella colonna del mio data-set, cioè la percentuale di missing value è molto alta. Questa cosa può avvenire nella riga, ma bisogna valutare in che modo sia importante togliere la riga oppure no.

**Dati duplicati** oppure Dati Sbagliati che bisogna sistemare ed integrare.

### Trattamento dei Valori Mancanti (Missing Values)
Per trattare i dati mancanti si possono **rimuoverli in due dimensione**:

- **Rimozione della riga**: se vediamo che nella tabella il dato è spesso mancante e non influisce più del $5\%$ dell'inter data-set.

- **Rimozione della colonna**: si rimuove una colonna se e solamente se i dati di quella colonna mancano per più del $50\%$ o $30\%$ dell intera tabella

Si possono anche gestire i dati mancanti attraverso calcoli statistici, che vanno a sostituire i dati, tra cui:

- **Media** o **Mediana**. La mediana è preferibile in presenza di distribuzioni asymmetric o outlier.

- Sostituzione con la **Moda** (per attributi categorici)

**Imputazione tramite Modelli:** Stima del valore mancante usando algoritmi come _K-Nearest Neighbors (KNN)_ o modelli di regressione basati sulle altre variabili