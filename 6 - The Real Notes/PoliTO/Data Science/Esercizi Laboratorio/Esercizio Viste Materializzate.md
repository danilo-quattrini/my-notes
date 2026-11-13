---
created: 2026-11-03
tags:
  - baby
topics:
  - Data
  - SQL
author: Danilo Quattrini
---
# Esercizio Viste Materializzate
---
# Come si creano le viste materializzate
>[!info] Scopo delle viste?
>Lo scopo delle viste sono quelle di velocizzare l'esecuzione delle query per far si di utilizzare una query ottimizzata che possa soddisfare richieste differenti. [[Progettazione Fisica & Viste#Viste|qui]]

Quando viene fornito un insieme di interrogazioni / query ($Q_1, Q_2, \dots, Q_n$) e si richiede di velocizzarle tramite viste materializzate, il procedimento si scompone in quattro passaggi analitici.

## 1. Passaggio
Il primo passaggio è quello di creare una tabella con le colonne le query / interrogazioni che vogliamo ottimizzare, nelle righe invece abbiamo:

- **Raggrupamenti** (`GROUP BY`): le dimensioni su cui andiamo a raggruppare.

- **Filtri**: sarebbe quello che è presente nella clausola `WHERE`

- **Misure Aggregate**: su che dimensione stiamo facendo l'aggregazione / calcoli `SUM(), AVG(), SUB()` (es. `Anno = 2025`, `Nazionalità IN ('IT', 'DE')`).

## 2. Principio di Granularità
Una vista materializzata a un determinato livello di dettaglio può rispondere solo a query che richiedono una Granularità uguale o più sintetica (grossolana).

- **Regola di derivazione:** Se la vista $V_1$ contiene il dettaglio `(Mese, Tariffa)`, da essa è possibile ricavare i totali per solo `Mese` eseguendo un Roll-up su `Tariffa`.
    
- **Inversione non consentita:** Se si crea una vista raggruppata unicamente per `Mese`, è impossibile risalire al dettaglio per `Tariffa`.

## 5. Creazione Viste Materializzate
```SQL
CREATE MATERIALIZED VIEW nome_view
BUILD IMMEDIATE
REFRESH FAST ON COMMIT
AS 
	SELECT...
```
- **`CREATE MATERIALIZED VIEW nome_della_vista`**
    
    Definisce l'oggetto nel database. A differenza di `CREATE VIEW`, questa istruzione alloca uno spazio di memoria su disco dove salvare le righe risultanti.
    
- **`BUILD IMMEDIATE`**
    
    Specifica il momento del primo popolamento dei dati. `IMMEDIATE` indica al database di eseguire la query `AS SELECT ...` e riempire la vista subito dopo la sua creazione. (L'alternativa `BUILD DEFERRED` crea la struttura vuota rinviando il popolamento).
    
- **`REFRESH FAST ON COMMIT`**
    
    Stabilisce come e quando la vista materializzata viene aggiornata al variare dei dati nelle tabelle sorgente:
    
    - **`REFRESH`**: Indica la clausola di aggiornamento.
        
    - **`FAST`**: Sfrutta i Log della vista materializzata per eseguire un aggiornamento incrementale. Il database non ricalcola l'intera vista da capo, ma aggiorna unicamente i totali delle righe modificate o inserite.
        
    - **`ON COMMIT`**: L'aggiornamento avviene automaticamente ogni volta che viene eseguita un'operazione di `COMMIT` (salvataggio definitivo) sulle tabelle dei fatti principali.
        
- **`AS <Istruzione SELECT>`**
    
    Contiene la query SQL standard di aggregazione:
    
    - La clausola `SELECT` specifica le dimensioni da mantenere e le funzioni d'aggregazione (`SUM`).
        
    - Le clausole `FROM` e `JOIN` collegano la tabella dei fatti alle tabelle dimensionali.
        
    - La clausola `GROUP BY` definisce il livello esatto di granularità della vista. Non deve mai contenere clausole `WHERE` troppo restrittive se la vista deve servire più query con filtri diversi.
>[!warning]
>Quando si fanno le aggregazioni, non utilizzare mai l'operatore `AVG`, perché la media viene svolta solo e solamente dopo che la vista materializzata è stata creata, NON FARE CALCOLI DI MEDIE.

# Esercizio 1
```
INCASSO(IdSede, IdServizio, IdCategoriaAzienda, IdTempo, #Consulenze, Incasso)
SERVIZIO(IdServizio, Servizio, TipologiaServizio)
TEMPO(IdTempo, Data, Mese, Bimestre, Trimestre, Quadrimestre, Semestre, Anno)
SEDE-CONSULENTI(IdSede, Sede, Città, Regione, AreaGeografica, #Consulenti)
AZIENDA(IdCategoriaAzienda, CategoriaAzienda, SettoreCommerciale, Nazionalità)
```

### Query SQL

a) Per ogni coppia (tipologia dei servizi, semestre), visualizzare lʼincasso totale e il numero totale di consulenze, effettuate dai consulenti delle sedi site in Lombardia.
```sql
SELECT S.TipologiaServizio, T.Semestre,
--- INCASSO TOTALE
SUM(Incasso) AS INCASSO_TOTALE,
--- NUMERO TOTALE DI CONSULENZE
SUM(#Consulenze) AS NUMER_TOT_CONSULENZE_LOMBARDIA
FROM INCASSO
JOIN SERVIZIO S ON INCASSO.IdServizio = S.IdServizio
JOIN TEMPO T ON INCASSO.IdTempo = T.IdTempo
JOIN SEDE-CONSULENTI SC ON INCASSO.idSede = SC.IdSede
WHERE SC.Regione = 'Lombardia'
GROUP BY S.TipologiaServizio, T.Semestre
```

b) Considerando solo le aziende italiane e tedesche, selezionare per ogni coppia (Regione delle sedi dei consulenti, Servizio), lʼincasso totale e il numero di consulenze effettuate,
separatamente per ogni anno

```sql
SELECT SC.Regione, S.Servizio, T.Anno,
--- INCASSO TOTALE
SUM(Incasso) AS INCASSO_TOTALE, 
--- NUMERO CONSULENZE SEPARATE PER OGNI ANNO
SUM(#Consulenze) AS NUMERO_CONSULENZE --- <-- NON NECESSARIO LA FINESTRA DI CALCOLO
FROM INCASSO
JOIN SERVIZIO S ON INCASSO.IdServizio = S.IdServizio
JOIN TEMPO T ON INCASSO.IdTempo = T.IdTempo
JOIN SEDE-CONSULENTI SC ON INCASSO.idSede = SC.IdSede
JOIN AZIENDA A ON INCASSO.IdCategoriaAzienda = A.IdCategoriaAzienda
WHERE A.Nazionalità IN ("IT", "DE") --- <- ERROR DON'T USE AND &
GROUP BY SC.Regione, S.Servizio, T.Anno
```

Considerando solo gli incassi del 2017, 2018, e 2019, per ogni coppia (Tipologia dei servizi,
nazionalità dell azienda), visualizzare lʼincasso semestrale e lʼincasso semestrale medio per
consulenza

```sql
SELECT S.TipologiaServizio, A.Nazionalità, T.Anno, T.Semestre
--- INCASSO SEMESTRALE
SUM(Incasso) AS INCASSO_SEMESTRE
--- INCASSO SEMESTRALE MEDIO PER CONSULENZA
SUM(Incasso) / SUM(#Consulenze) AS INCASSO_SEMESTRALE_MEDIO

FROM INCASSO
JOIN SERVIZIO S ON INCASSO.IdServizio = S.IdServizio
JOIN TEMPO T ON INCASSO.IdTempo = T.IdTempo
JOIN SEDE-CONSULENTI SC ON INCASSO.idSede = SC.IdSede
JOIN AZIENDA A ON INCASSO.IdCategoriaAzienda = A.IdCategoriaAzienda
WHERE T.Anno = 2019 OR T.Anno = 2018 OR T.Anno = 2017
GROUP BY S.TipologiaServizio, A.Nazionalità, T.Anno, T.Semestre;
```

>[!warning] IMPORTANTE
>**Usa SOLO `GROUP BY` (senza `OVER`):** Quando la consegna ti chiede di calcolare totali o medie **al livello di dettaglio indicato nelle parentesi o nella frase** (es. _"per ogni regione, servizio e anno"_). L'aggregazione standard calcola il risultato esattamente per quel gruppo.
    
>[!warning]
**Usa le Window Functions (`OVER`):** Solo quando devi **confrontare nello stesso record due livelli di aggregazione diversi** (es. _"mostra il totale del singolo mese AFFIANCATO al totale dell'intero anno"_ o _"calcola la media mobile degli ultimi 3 periodi"_).

# Laboratorio 3
## Creazione della Tabella
Prendiamo 3 query che vogliamo ottimizzare
1. Selezionare il ricavo totale per ciascuna tipologia di tariffa telefonica e per ciascun mese dell'anno 2025. Selezionare inoltre il ricavo totale complessivo, il ricavo totale per ciascuna tipologia di tariffa telefonica indipendentemente dal mese e il ricavo totale per ciascun mese indipendentemente dalla tipologia di tariffa telefonica.
   
2. Selezionare il numero mensile di chiamate e il ricavo mensile. Associare a ciascun mese il valore di `RANK()` in base al relativo ricavo (1 per il mese con il ricavo più elevato, 2 per il secondo e così via, fino al mese con il ricavo più basso)

3. Per ciascun mese del 2025, selezionare il numero totale di chiamate. Associare a ciascun mese il valore di `RANK()` in base al numero totale di chiamate (1 per il mese con il maggior numero di chiamate, 2 per il secondo e così via, fino al mese con il minor numero di chiamate)

4. Selezionare il ricavo totale di gennaio 2025, separatamente per ciascuna tariffa telefonica.
   
5. Selezionare il ricavo mensile e il ricavo mensile cumulato dall'inizio dell'anno.


|                   | Q1                           | Q2                               |                         | Q4                                         | Q5           |     |     |
| ----------------- | ---------------------------- | -------------------------------- | ----------------------- | ------------------------------------------ | ------------ | --- | --- |
| **Raggrupamenti** | `PHONERATETYPE`, `DATEMONTH` | `DATEMONTH`                      | `DATEYEAR`, `DATEMONTH` | `PHONERATETYPE`, `DATEYEAR`                | `DATEMONTH`  |     |     |
| **Filtri**        | `DATEYEAR = '2025'`          |                                  | `DATEYEAR = '2025'`     | `DATEYEAR = 2025`, `DATEMONTH = '2025-01'` |              |     |     |
| **Aggregazioni**  | `SUM(PRICE)`                 | `SUM(NUMBEROFCALLS), SUM(PRICE)` | `SUM(NUMBEROFCALLS)`    | `SUM(PRICE)`                               | `SUM(PRICE)` |     |     |
|                   |                              |                                  |                         |                                            |              |     |     |


## Homework 1
### Vista Materializzata
Si considerino le seguenti query frequenti:

- Numero di noleggi e media dei chilometri percorsi per noleggio, per trimestre, tipo di alimentazione e regione di partenza degli ultimi due anni.
- Considerando i noleggi di auto con produttore “Fiat”, calcolare il numero cumulativo di noleggi e media progressiva annuale dei chilometri per noleggio, per trimestre, tipo di alimentazione e regione di partenza.
- Fatturato totale e fatturato medio per noleggio, per trimestre, tipo di alimentazione e regione di partenza.
- Numero di noleggi e durata media in ore, per anno e tipo di alimentazione.

**Definire mediante `CREATE MATERIALIZED VIEW` una vista materializzata, denominata `VM1`, utile ad accelerare tutte le query indicate. Motivare la struttura scelta rispetto ai tempi di risposta e allo spazio occupato.**

|   |   |   |   |   |
|---|---|---|---|---|
||**Q1**|**Q2**|**Q3**|**Q4**|
|**Aggregazioni**|COUNT(*), AVG(tot_kilometers)|COUNT(*), AVG(tot_kilometers)|SUM(pocket_price), AVG(pocket_price)|COUNT(*), AVG(end_hour - start_hour)|
|**Filtri**||model = "Fiat"|||
|**Raggrupamenti**|3m, fuel, region, year|3m, fuel, region|3m, fuel, region|year, fuel|
```SQL
CREATE MATERIALIZED VIEW VM1
BUILD IMMEDIATE
REFRESH FAST ON COMMIT
AS 
SELECT 
    D.year,
    D.3m,
    V.fuel,
    V.model,
    L.region,
    COUNT(*) AS NUM_TOT_NOLEGGI,
    SUM(R.pocket_price) AS TOT_POCKET_PRICE,
    SUM(R.tot_kilometers) AS TOT_KILOMETERS,
    SUM(R.end_hour - R.start_hour) AS TOT_ORE_NOLEGGIO
FROM rent R
JOIN DATE D ON D.Id_date = R.Id_date
JOIN LOCATION L ON L.Id_location = R.Id_start_location
JOIN VEHICLE V ON V.Id_vehicle = R.Id_vehicle 
GROUP BY 
    D.year, 
    D.3m, 
    V.fuel, 
    V.model, 
    L.region;
```

Il consumo di memoria su disco è contenuto. Raggruppando la tabella dei fatti al livello di sintesi `(Anno, Trimestre, Alimentazione, Modello, Regione)`, il numero totale di righe memorizzate diminuisce di diversi ordini di grandezza rispetto alle singole transazioni grezze.

### Insieme Minimale
>[!info]
>**Definire l’insieme minimale di attributi che permette di identificare le tuple appartenenti alla vista materializzata `VM1`.**

L'esercizio richiede di identificare la **chiave candidata minimale** (o chiave primaria) della vista materializzata `VM1`.

In altre parole, chiede di **trovare il minor numero possibile di colonne in grado di identificare univocamente ogni riga presente nella vista salvata su disco**.

### Applicazione passo-passo alla vista VM1

Gli attributi presenti nel `GROUP BY` della vista `VM1` sono:

- `D.year` (Anno)
    
- `D.3m` (Trimestre)
    
- `V.fuel` (Alimentazione)
    
- `V.model` (Modello)
    
- `L.region` (Regione)
    

Analisi della dipendenza tra le colonne:

- **`D.year` e `D.3m`:** Entrambi sono necessari. Il solo valore `3m` (es. Q1) si ripete ogni anno, mentre il solo `year` copre quattro trimestri distinti.
    
- **`L.region`:** Necessario per distinguere le regioni geografiche di partenza.
    
- **`V.model` e `V.fuel`:** Nel modello dei dati, il modello del veicolo determina univocamente la sua alimentazione ($\text{V.model} \rightarrow \text{V.fuel}$). Di conseguenza, conoscendo `V.model`, il valore di `V.fuel` è già determinato univocamente e risulta ridondante ai fini della chiave.
    

### Risposta al punto (b)

L'insieme minimale di attributi che identifica univocamente le tuple di `VM1` è:

$$\{ \text{D.year}, \text{D.3m}, \text{V.model}, \text{L.region} \}$$

>[!info]
>Se nel dominio applicativo non si ipotizza la dipendenza tra modello e alimentazione, l'insieme minimale coincide con l'intera clausola `GROUP BY`: $\{ \text{D.year}, \text{D.3m}, \text{V.fuel}, \text{V.model}, \text{L.region} \}$).