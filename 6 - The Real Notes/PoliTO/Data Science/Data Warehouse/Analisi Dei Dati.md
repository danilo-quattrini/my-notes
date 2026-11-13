---
created: 2026-09-29
tags:
  - baby
topics:
  - Data
  - BigData
author: Danilo Quattrini
---
# Analisi Dei Dati
---
## Questions
- Elenca le varie tipologie di **Analisi OLAP**, Qual è lo scopo primario di ciascuna di queste operazioni quando si esplora un cubo di dati?
  
- Quali sono le principali Funzioni OLAP? In che modo si differenziano dalle normali funzioni di aggregazione SQL (come una semplice `SUM()` con `GROUP BY`) rispetto a come restituiscono le righe?
  
- Che cos'è una finestra di calcolo? Quali sono i suoi tre elementi costitutivi e a cosa serve distinguere tra una finestra a livello fisico e una a livello logico?
### Funzioni OLAP
- Descrivi la Partizione cos'è e come funziona?

- Che differenza c'è tra la Partizione e la `GROUP BY`?

- Descrivi come funziona L'ordinamento delle righe?

- Descrivi come funziona la finestra di aggregazione?

- Su quali livelli viene utilizzata la **finestra di aggregazione**?

## Funzionalità di Ranking
- Cosa server il ranking?
  
- Come funziona il ranking?

- Quali sono i differenti modi per definire un rank?
---
Analisi utili per generare dashboard interattive, per generare report. Nell'analisi si svolgono delle **operazioni di aggregazione lungo diverse dimensioni.** Operazioni di confronto per far si che si vadano a creare delle analisi sulla base di dati / analisi precedenti (esempio confronto di dati delle vendite di un prodotto in mesi diversi). 

Tali confronti sono però complicati eseguirli solamente con delle query SQL, per tale ragione si utilizzano delle **tecniche di data mining**, per eseguire le analisi che necessitiamo.

## Analisi OLAP
Permette l’analisi dei dati mediante **diverse operazioni che possono essere combinate tra loro nella stessa query** e eseguite in sequenza in una stessa sessione [[Analisi Data Warehouse#Analisi OLAP|OLAP]]:
### Roll Up
Si vanno a ridurre i dati che si vanno ad analizzare aumentando il livello di gerarchia (cioè cambiare il tipo di group by) oppure eliminare una gerarchia
![[Screenshot 2026-10-01 at 10.14.26.png]]
Nell'esempio sopra abbiamo che le singole nazioni vengono raggrupate in una unica e singola colonna chiamata `Dollar Sales`, si riduce il dettaglio dei dati.

>[!example] Esempio
>Stai guardando un report che mostra le vendite di Gennaio 2026 per la città di Milano, Roma e Napoli. Il tuo manager ti chiede: "Com'è andata l'Italia nel 2026?". **Esegui un Roll Up eliminando la dimensione _Città_** e passando dal _Mese_ all'_Anno_. I dati di Milano, Roma e Napoli vengono aggregati nell'unico valore "Italia".
### Drill Down
si aumenta il livello di dettaglio, lo uso per analizzare un macro fenomeno, e lo uso per analizzare degli spostamenti di valori su dei dati specifici. Spesso si va ad aggiungere una nuova dimensione (esempio raggrupamento per città)

![[Screenshot 2026-10-01 at 10.17.40.png]]
Più dettagli si aggiungono più sparsità dei dati possono avvenire (cioè valori nulli nelle righe)
![[Screenshot 2026-10-01 at 10.18.19.png]]

>[!info]
>Nell'esempio sopra si è aggiunta una colonna, dove prima si aveva solo come colonne come  `Metrics` il valore di `Dollar Sales`, e nelle colonne `Years` i diversi anni in cui i determinati prodotti hanno fatturato.
>
>Quando si fa un operazione di **Drill Down**, vuol dire che si va ad **aggiungere una nuova colonna di interesse** , come in questo caso `Customer Region` che definisce un dettaglio maggiore ai dati andando a creare dei nuovi gruppi che sono in base alla regione in cui sono stati venduti i prodotti `Noth-East`, `Mid-Atlantic` ecc...
### Slice and Dice
Quando ci focalizziamo su un gruppo di dati specifico cioè un sotto-insieme di dati (sarebbe come fare la clausola **WHERE**)
![[Screenshot 2026-10-01 at 10.20.11.png]]
un micro-cubo è un'insieme di dati che soddisfano le condizioni della clausola che vogliamo focalizzare, cioè lo **Slice**, un predicato di uguaglianza che seleziona una “fetta” (lungo una dimensione di riferimento della DW) e il **Dice** invece predicato dove si seleziona un singolo cubetto (porzione di dimensione)
	
![[Screenshot 2026-10-01 at 10.23.13.png]]

### Pivot
Riorganizzazione dell’orientamento della struttura multidimensionale senza variare il livello di dettaglio, le informazioni sono sempre le stesse solo che vengono viste sotto un'altra prospettiva.
![[Screenshot 2026-10-18 at 18.31.52.png]]
Nella Pivot non stai cambiando o isolando dei dati, ma stai semplicemente ruotando l'ordine delle righe con le colonne.

>[!example]
>Prendiamo le vendite di dispositivi elettronici negli anni 2025 e 2026, per questi due anni vogliamo solo visualizzare le vendite dei Computer e degli Smartphone (operazione di Slice), il risultato viene così:
>
|**Categoria**|**2025**|**2026**|
|---|---|---|
|**Computer**|100k|120k|
|**Smartphone**|200k|150k|
Se invece volessimo vedere nelle righe gli anni e nelle colonne i dispositivi venduti, l'operazione di inversione dalle righe alle colonne si chiama 
**Pivot**.
Per capire al volo quale operazione stai facendo, chiediti: _"Se sommo tutti i numeri che vedo a schermo adesso, il totale è diverso rispetto a prima?"_. Se il totale cambia, hai fatto uno Slice & Dice o un Drill Down/Roll Up. Se il totale complessivo è identico e hai solo scambiato le righe con le colonne, hai fatto un Pivot.

| **Anno** | **Computer** | **Smartphone** |
| -------- | ------------ | -------------- |
| **2025** | 100k         | 200k           |
| **2026** | 120k         | 150k           |


## Estensioni del Linguaggio
Abbiamo le necessità di confrontare aggregati di diversi dettagli, per questo è stato creato un estensione del linguaggio SQL.  SQL è un linguaggio dichiarativo perché chiediamo cosa ci serve senza sapere come lo prende. L'estensione del linguaggio SQL parte da un base che sarebbe proprio SQL. 
 
Prendiamo un esempio con una base dati da una singola tabelle che sono le vendite:
![[Screenshot 2026-10-01 at 10.34.36.png]]
Per ogni coppia (città, mese) abbiamo un valore di importo, per ogni città visualizzare, questo è possibile con 
```sql
SELECT Città, SUM(Mese) [NUOVE FUNZIONALITà]
FROM Vendite
WHERE <conditions>
GROUP BY Città
```

Se c'è una `GROUP BY` , la `SELECT` deve contenere il valore della `GROUP BY`. l'ordine di lettura della query è prima legge i dati con il `FROM`, poi raggruppo con `GROUP BY` (se c'era una `WHERE`, faceva prima il filtro poi le raggruppava), infine faccio la `SELECT`.

>[!warning] N.B
>L'operazione di `SELECT`, viene svolta sempre per ultima.

Le nuove funzionalità saranno presente nella parte `[NUOVE FUNZIONALITà]`,  che si chiama **finestra di calcolo**.

## Funzioni OLAP
La finestra di calcolo può presentare una delle seguenti clausole, che però non necessariamente devono comparire tutti e tre:

1. **Partizionamento dei dati**: divido le righe in gruppi, senza dove collassare (diverso dal `GROUP BY`), spiegato [[#Partizionamento dei Dati (`PARTITION BY`)|qui]]

2. **Ordinamento delle Righe**: si fa una separazione all'interno di ogni partizione (simile a `ORDER BY`).

3. **Finestra di Aggregazione**: definisce l'insieme delle righe che devo considerare, per eseguire la funzione di aggregazione che ho indicato fuori dalla finestra di calcolo, spiegato [[#Finestra di Aggregazione (Frame Clause `ROWS` / `RANGE`)|qui]].


>[!info] Come funziona?
>La finestra di calcolo si definisce tramite la clausola **`OVER (...)`** dopo ogni operazione additiva (come `SUM`, `SUB`, ecc...). 

### Partizionamento dei Dati (`PARTITION BY`)
>[!info] Funzionamento
>Divide l'insieme dei dati in sotto-gruppi disgiunti (partizioni) in base ai valori degli attributi specificati. L'operazione della finestra viene eseguita **in modo indipendente all'interno di ciascuna partizione**

A differenza dell `GROUP BY` La clausola `GROUP BY` riduce le tuple del gruppo a una sola riga. Il `PARTITION BY` mantiene intatte tutte le righe originarie, affiancando ad ciascuna riga il valore aggregato calcolato sulla sua partizione.

>[!example] Esempio
>E' come se mettessi dei muri tra i dati presenti in una tabella
>![[Screenshot 2026-10-01 at 10.56.08.png]]
>Cioè tra le righe dalla prima di Milano fino a prima che arriva a Torino c'è un muro che divide le due righe, la `PARTITION BY`  lavora su ogni muro delineato


### Ordinamento delle Righe (`ORDER BY`)
>[!info] Definizione
>Definisce un **ordine sequenziale per le righe all'interno di ogni partizione**

Viene **utilizzato durante le operazioni di totali cumulativi**, medie mobili, per le funzioni di ranking (`RANK`, `DENSE_RANK`, `ROW_NUMBER`)

### Finestra di Aggregazione (Frame Clause: `ROWS` / `RANGE`)
>[!info] Definizione
>Definisce esattamente l'insieme dinamico di righe (il "frame" o sotto-finestra) da considerare per calcolare il valore aggregato **relativo alla riga corrente**.

La finestra di aggregazione può essere definita:
- **A Livello fisico**: formando il gruppo mediante conteggio delle righe, è adatto per dati più densi:
	- `ROWS 2 PRECEDING (o FOLLOWING)` (tra un'estremo inferiore alla riga corrente) La riga corrente e le 2 righe fisicamente precedenti.

	- `ROWS BETWEEN 3 PRECEDING AND 1 PRECEDING` (tra un'estremo inferiore e uno superiore) Da 3 righe prima a 1 riga prima della corrente.

	- `ROWS UNBOUNDED PRECEDING` (Tra l'inizio della partizione e la riga corrente) Dall'inizio della partizione fino alla riga corrente (utilissimo per **totali cumulativi**)
	
	- `ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING`: Dalla riga corrente fino alla fine della partizione.

- **A Livello Logico**: formando il gruppo in base alla definizione di un intervallo intorno alla chiave di ordinamento, è adatto per dati sparsi. 
	- `RANGE BETWEEN INTERVAL '2' MONTH PRECEDING AND CURRENT ROW`: Considera l'intervallo temporale/logico dei 2 mesi precedenti rispetto al valore della riga corrente.

## Funzionalità di Ranking
>[!info]
>Le funzioni di ranking assegnano una posizione/classifica a ciascuna riga all'interno della propria partizione, in base all'ordinamento specificato.

Esistono tre funzioni principali di ranking che si comportano in modo leggermente diverso in presenza di **valori paritari (ties)**:

| **Funzione**       | **Gestione dei Pari (Ties)**                             | **Sequenza dei Ranghi Successivi**                           |
| ------------------ | -------------------------------------------------------- | ------------------------------------------------------------ |
| **`ROW_NUMBER()`** | Assegna numeri consecutivi univoci, ignorando i pareggi. | $1, 2, 3, 4, 5, \dots$                                       |
| **`RANK()`**       | Assegna lo stesso valore alle righe a pari merito.       | **Lascia buchi nella numerazione:** $1, 2, 2, 4, 5 \dots$    |
| **`DENSE_RANK()`** | Assegna lo stesso valore alle righe a pari merito.       | **Non lascia buchi (sequenza densa):** $1, 2, 2, 3, 4 \dots$ |
### Differenza tra `RANK` e `DENSE_RANK`
La differenza è il modo in cui gestiscono l'ordinamento dei pari-meriti, cioè il `RANK()` quando andrà a gestire il pari-merito tra due partizioni differenti, gli assegnano lo stesso numero e alla partizione successiva va ad escludere il valore successivo andando a creare dei buchi, **salta i ranghi successivi**.
Mentre **`DENSE_RANK()` genera una numerazione continua e "densa"** senza saltare alcun numero


| Funzione       | Gestione dei Parimeriti  | Sequenza dei Ranghi successivi                                             | Presenza di Buchi |
| -------------- | ------------------------ | -------------------------------------------------------------------------- | ----------------- |
| `RANK()`       | Assegna lo stesso valore | Salta i posizionamenti intermedi in base al numero di righe a pari merito. | SI                |
| `DENSE_RANK()` | Assegna lo stesso valore | Assegna il numero intero immediatamente successivo.                        | NO                |


>[!example] Esempio
>Ipotizziamo una tabella di studenti con i relativi voti presi in un esame
>```SQL
SELECT Studente, 
Voto,
ROW_NUMBER() OVER (ORDER BY Voto DESC) AS Row_Num,
RANK() OVER (ORDER BY Voto DESC) AS Rank_Val,
DENSE_RANK() OVER (ORDER BY Voto DESC) AS Dense_Rank_Val
FROM Esami;```

#### Quando usare l'una o l'altra?

 **Usa `RANK()`** quando ti interessa la posizione relativa reale tenendo conto del numero totale di concorrenti/elementi che precedono (es. classifiche sportive ufficiose o concorsi: se due persone arrivano prime a pari merito, non esiste un secondo posto, ma si passa direttamente al terzo).
    
 **Usa `DENSE_RANK()`** quando ti interessa identificare le "fasce" di merito o i livelli di posizione senza perdere la continuità dei numeri (es. "voglio premiare i primi 3 livelli di stipendio più alti dell'azienda", indipendentemente da quante persone prendano lo stesso stipendio).

## Esempi Pratici
### Partizionamento, Ordine e Finestra Di Aggregazione
Prendiamo la tabella delle `vendite `

| ID  | **Citta** | **Mese** | **Importo** |
| --- | --------- | -------- | ----------- |
| 1   | Milano    | Gennaio  | 100         |
| 2   | Milano    | Febbraio | 150         |
| 3   | Milano    | Marzo    | 150         |
| 4   | Milano    | Aprile   | 200         |
| 5   | Roma      | Gennaio  | 80          |
| 6   | Roma      | Febbraio | 120         |
|     |           |          |             |
Dobbiamo calcolare la media mobile e il totale cumulativo per ogni città e mese
```sql
SELECT 
    Citta, 
    Mese, 
    Importo,
    -- 1. Totale Cumulativo
    SUM(Importo) OVER (
        PARTITION BY Citta 
        ORDER BY Mese 
        ROWS UNBOUNDED PRECEDING
    ) AS TotaleCumulativo,
    -- 2. Media Mobile (mese corrente + 2 mesi precedenti)
    AVG(SUM(Importo)) OVER (
        PARTITION BY Citta 
        ORDER BY Mese 
        ROWS 2 PRECEDING
    ) AS MediaMobile
FROM Vendite;
GROUP BY Citta, Mese
```

1. La partizione la facciamo con `PARTITION BY [COLONNA DA CUI FARE PARTIZIONE]` e faremmo un partizione dalla riga 1 fino alla quarta, se inseriamo la condizione `PARTITION BY Città`, dove prendiamo il gruppo `Milano` E `Roma`
2. **`ORDER BY Mese`**: Ordina i record di Milano in base alla sequenza temporale dei mesi.
3. **Calcolo `TotaleCumulativo` (`ROWS UNBOUNDED PRECEDING`)**:

    - _Gennaio (100)_: somma da inizio partizione a Gennaio = $100$.
        
    - _Febbraio (150)_: somma da Gennaio a Febbraio = $100 + 150 = 250$.
        
    - _Marzo (150)_: somma da Gennaio a Marzo = $100 + 150 + 150 = 400$.
        
    - _Aprile (200)_: somma da Gennaio ad Aprile = $100 + 150 + 150 + 200 = 600$.
Qui sotto abbiamo il calcolo del totale Cumulativo

| ID  | **Citta** | **Mese** | **Importo** | TotaleCumulativo |
| --- | --------- | -------- | ----------- | ---------------- |
| 1   | Milano    | Gennaio  | 100         | 100              |
| 2   | Milano    | Febbraio | 150         | 250              |
| 3   | Milano    | Marzo    | 150         | 400              |
| 4   | Milano    | Aprile   | 200         | 600              |
| 5   | Roma      | Gennaio  | 80          | 80               |
| 6   | Roma      | Febbraio | 120         | 200              |
4. **Calcolo `MediaMobile` (`ROWS 2 PRECEDING`)**:
	- _Gennaio (100)_: solo 1 riga disponibile = $100 / 1 = 100$.
    
	- _Febbraio (150)_: riga corrente + 1 precedente = $(100 + 150) / 2 = 125$.
    
	- _Marzo (150)_: riga corrente + 2 precedenti = $(100 + 150 + 150) / 3 = 133.33$.
    
	- _Aprile (200)_: riga corrente + 2 precedenti (Feb, Mar, Apr) = $(150 + 150 + 200) / 3 = 166.66$.

| ID  | **Citta** | **Mese** | **Importo** | TotaleCumulativo | MediaMobile |
| --- | --------- | -------- | ----------- | ---------------- | ----------- |
| 1   | Milano    | Gennaio  | 100         | 100              | 100         |
| 2   | Milano    | Febbraio | 150         | 250              | 125         |
| 3   | Milano    | Marzo    | 150         | 400              | 133         |
| 4   | Milano    | Aprile   | 200         | 600              | 167         |
| 5   | Roma      | Gennaio  | 80          | 80               | 80          |
| 6   | Roma      | Febbraio | 120         | 200              | 100         |
### Ranking delle Vendite
```
SELECT 
    Citta, 
    Mese, 
    Importo,
    ROW_NUMBER() OVER (PARTITION BY Citta ORDER BY Importo DESC) AS N_Riga,
    RANK() OVER (PARTITION BY Citta ORDER BY Importo DESC) AS Rango,
    DENSE_RANK() OVER (PARTITION BY Citta ORDER BY Importo DESC) AS RangoDenso
FROM Vendite;
```

| **Citta** | **Mese** | **Importo** | **ROW_NUMBER** | **RANK** | **DENSE_RANK** | **Spiegazione del comportamento**                                                               |
| --------- | -------- | ----------- | -------------- | -------- | -------------- | ----------------------------------------------------------------------------------------------- |
| Milano    | Aprile   | 200         | **1**          | **1**    | **1**          | Valore massimo, 1° posto per tutti.                                                             |
| Milano    | Febbraio | 150         | **2**          | **2**    | **2**          | Pari merito con Marzo.                                                                          |
| Milano    | Marzo    | 150         | **3**          | **2**    | **2**          | `RANK` e `DENSE_RANK` mantengono la parità al 2° posto.                                         |
| Milano    | Gennaio  | 100         | **4**          | **4**    | **3**          | `RANK` salta al 4° (perché c'erano due 2° posti). `DENSE_RANK` assegna il 3° posto senza buchi. |


>[!example] Esempio 1
>- Devo trovare l'importo delle vendite 
>- La media rispetto al mese corrente e ai due mesi precedenti, separatamente per ogni città
>IL primo si può fare in SQL normale, ma il secondo invece non si può fare ma server L'SQL esteso.
>
>1. la cosa da fare partizionare i dati rispetto alle città, per dividere ogni città
>2. Ordinare i mesi 
>3. la finestra di aggregazione è il mese corrente e i due mesi correnti
>4. che operazione devo fare? La media
>```sql
>SELECT Città, Mese, Importo, AVG(IMPORTO) 
>OVER (PARTITION BY Città, ORDER BY Mese ROW 2 PRECEDING)
>AS MediaMobile
>FROM Vendite
>```
>![[Screenshot 2026-10-01 at 10.56.08.png]]
>Come viene calcolata la `MediaMobile`, notare che c'è un errore  dal mese di dicembre la città di Milano fino ad ottobre sarebbe `210 / 3 = 70` non `60`. 
>

**Calcolo dei totali cumulativi**: visualizzare per ogni città e mese, dove partizione per città ordino per il mese, dove prendo con `ROW UNBOUNDED PRECIDING` (Tra l'inizio della partizione e la riga corrente)![[Screenshot 2026-10-01 at 11.14.51.png|1081]]

## Esempi di applicazione
>[!example] Esempio 2
>- Per ogni città visualizzare l'importo complessivo delle vendite
>```sql
>SELECT Citta, SUM(Importo)
>FROM Vendite
>GROUP BY Citta
>```
>Non possiamo usare solo l'importo perché non ci basta per fare il rapporto (divisione) tra l'importo totale delle vendite con il numero delle vendite, quindi si può fare con una query annidata:
>```sql
>SELECT Citta, Mese, Importo / ImportoComplessivo
>FROM (
>	SELECT Citta, SUM(IMPORTO) AS ImportoComplessivo
>	 FROM Vendite
>	 Group By Citta AS TF, Vendite AS V
>)
>WHERE TF.Citta = Vendite_TF
>```
>Con la finestra di calcolo si fa un partizionamento dell'importo
>```sql
>SELECT Citta, Mese, 
>Importo / SUM(Importo) OVER (PARTITION by Citta) AS PercCitta
>Importo / SUM(Importo) OVER () AS PerTotale # <- prende tutti i dati e sui dati calcola una somma dell'importo
>Importo/SUM(Importo) OVER (PARTITION BY Mese)AS PercMese
>FROM Vendite
>``` 
>
>

>[!example] Esempio 3
>Si supponga che la tabella Vendite contenga informazioni sulle vendite con granularità giornaliera
>
>**Visualizzare, per ogni città e mese**:
>- l’importo delle vendite
>- la media rispetto al mese corrente e ai due mesi precedenti, separatamente per ogni città
>```SQL
SELECT Città, Mese, SUM(Importo) AS TotMese,
AVG(SUM(Importo)) OVER (
PARTITION BY Città
ORDER BY Mese
ROWS 2 PRECEDING
)	AS MediaMobile
FROM Vendite, ...
WHERE <cond. join>
GROUP BY Città, Me
>```


>[!warning] N.B
>non posso utilizzare l'etichetta `TotMese` perché viene solo utilizzato in fase di visualizzazione e non si può utilizzare nella finestra di calcolo

## Estensione della `GROUP BY`
Si generano gruppi di cardinalità diverse, come risultato avremmo un numero maggiore di righe, andando ad assegnare il valore null per gli attributi che non servono per un calcolo della `GROUP BY`
### Perché estendere il `GROUP BY`
Fare più raggrupamenti della stessa query aumentano l'efficienza, **per far si che si eseguano group by diverse, avendo effettuato una sola volta l'operazione di lettura e join**. Si può indirizzare facendo più table function (query annidate), ma aumentano le operazioni di lettura e `JOIN`.

Per generare dei gruppi però abbiamo bisogno dei risultati ordinati, quindi prima bisogna ordinare i dati, creare dei sotto-gruppi e poi generare un record. Questo vale se i dati sono disgiunti, in caso di dati non disgiunti, tale ordinamento non c'è bisogno.

### Sintassi dell'estensione SQL per la `GROUP BY`
![[Screenshot 2026-10-06 at 17.54.07.png]]

Vediamo un esempio di **Roll Up** prendendo le seguenti tabelle dei fatti:

Tempo(**Tkey**, Giorno,Mese,Anno,…)
Supermercato(**Skey**, Città, Regione,…)
Prodotto(**Pkey**, NomeP, Marca,…)
Vendite(**Skey**, **Tkey**, **Pkey**, Importo)

Visualizzare per ogni coppia Città, Semestre:
- L'importo delle vendite
- L'importo complessivo delle vendite al trascorrere dei semestri, separatamente per Regione
- Assegnare ad ogni record un rank per importo delle vendite decrescente, separatamente
Come si fa questa query? Si farà usando l'estensione della `GROUP BY` dove si andrà a raggruppare per la prima condizione solo prodotto

**Importo Vendite**
```SQL
SELECT Città, Semestre, SUM(Importo)
FROM Vendite as V, Supermecato as S, Tempo as T
WHERE 
INNER JOIN S.Skey = V.SkEY 
INNER JOIN T.Tkey = V.TKey
GROUP BY Città, Semestre
```

**L'importo complessivo delle vendite al trascorrere dei semestri, separatamente per Regione** , quì serve la finestra di calcolo
```SQL
SELECT Città, Semestre, SUM(Importo) 
	SUM(SUM(Importo)) OVER(PARTITION BY Regione 
			   ORDER BY Semestre
			   ROWS UNBOUNDED PRECIDING
			   )
FROM Vendite as V, Supermecato as S, Tempo as T
WHERE 
INNER JOIN S.Skey = V.SkEY 
INNER JOIN T.Tkey = V.TKey
GROUP BY Città, Semestre, Regione
```

La prima `SUM` esterna è quella che si calcola per la finestra di calcolo, mentre la `SUM` interna è relativa alla group by.

>[!warning] Per le `WHERE CONDITION`
>`N` tabelle nella from `N-1` condizioni nella `JOIN`

## Esercizi
In base a questo schema per le vendite e la gestione del personale:
 **`Vendite`** (`ID_Vendita`, `Citta`, `Mese`, `Anno`, `Importo`, `ID_Prodotto`)
 **`Dipendenti`** (`ID_Dipendente`, `Nome`, `Dipartimento`, `Stipendio`, `Data_Assunzione`)
### Totale Cumulativo Annuale
Per ogni vendita registrata nella tabella `Vendite`, visualizzare `Citta`, `Anno`, `Mese`, `Importo` e il **Totale Cumulativo dell'Importo**. Il calcolo deve sommare progressivamente gli importi dall'inizio dell'anno fino al mese corrente della riga considerata, separatamente per ciascuna città e anno

```SQL
SELECT Citta, Anno, Mese, 
	SUM(Importo) OVER (
		PARTITION BY Citta, Anno
		ORDER BY Mese
		ROWS UNBOUNDED PRECEDING
	)
FROM Vendite
```

### Media Mobile a 3 Periodi (Frame Fisico)
Scrivere una query per calcolare la **media mobile delle vendite** su un intervallo di 3 mesi per ciascuna città. Per ogni record (`Citta`, `Mese`, `Importo`), calcolare la media dell'importo considerando la riga del mese corrente e le **due righe fisicamente precedenti** nell'ordine temporale dei mesi.

```SQL
SELECT Citta, Mese, 
	AVG(Importo) OVER (
		PARTITION BY Citta
		ORDER BY Mese
		ROWS 2 PRECIDING -- Current moth + 2 mothn preciding = 3 
	) AS MediaVendite,
	AVG(Importo) OVER (
		PARTITION BY Citta
		ORDER BY Mese
		RANGE BETWEEN INTERVAL '2' MONTH PRECEDING AND CURRENT ROW
		
	)
FROM Vendite
```

### Calcolo delle Percentuali sul Totale (Partizionamento e Finestra Vuota)
- `Citta`, `Mese`, `Importo`.
    
- L'incidenza percentuale dell'importo della vendita sul **totale delle vendite della rispettiva città**.
    
- L'incidenza percentuale dell'importo della vendita sul **totale complessivo di tutte le vendite aziendali**.

```SQL
SELECT Citta, Mese,  
(Importo / SUM(Importo) OVER(PARTITION BY Citta)) * 100 as PercentualeVenditeCitta,
(Importo / SUM(Importo) OVER()) * 100 as PercTotale
FROM Vendite
```
