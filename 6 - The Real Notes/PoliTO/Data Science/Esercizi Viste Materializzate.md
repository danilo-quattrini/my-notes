---
created: 2026-10-26
tags:
  - baby
topics:
  - Data
author: Danilo Quattrini
---
# Esercizi Viste Materializzate
---
## Esercizio 1
Prendiamo lo schema logico qui illustrato

INCASSO(**IdSede**, **IdServizio**, **IdCategoriaAzienda**, IdTempo, # Consulenze, Incasso) -> *FACTS*
SERVIZIO(**IdServizio**, Servizio, TipologiaServizio)
TEMPO(**IdTempo**, Data, Mese, Bimestre, Trimestre, Quadrimestre, Semestre, Anno)
SEDE-CONSULENTI(**IdSede**, Sede, Città, Regione, AreaGeografica, # Consulenti)
AZIENDA(**IdCategoriaAzienda**, CategoriaAzienda, SettoreCommerciale, Nazionalità)

## Query
Dato lo schema logico precedente, considerare le seguenti query di interesse:
>[!exercise] Query A
>Per ogni coppia (tipologia dei servizi, semestre), visualizzare l’incasso totale e il numero totale di consulenze, effettuate dai consulenti delle sedi site in Lombardia.


>[!exercise] Query B
>Considerando solo le aziende italiane e tedesche, selezionare per ogni coppia (Regione delle sedi dei consulenti, Servizio), l’incasso totale e il numero di consulenze effettuate, separatamente per ogni anno.


>[!exercise]  Query C
Considerando solo gli incassi del 2017, 2018, e 2019, per ogni coppia (Tipologia dei servizi, nazionalità dell'azienda), visualizzare l’incasso semestrale e l’incasso semestrale medio per consulenza

|                  | Query A                                            | Query B                                            | Query C                             |
| ---------------- | -------------------------------------------------- | -------------------------------------------------- | ----------------------------------- |
| `FROM`           | INCASSO, TEMPO, SERVIZIO, SEDE-CONSULENTI, AZIENDA | INCASSO, AZIENDA, SEDE-CONSULENTI, SERVIZIO, TEMPO | INCASSO, TEMPO, AZIENDA, SERVIZIO,  |
| Aggregazione     | `SUM(Consulenze)`, `SUM(Incasso)`                  | `SUM(Consulenza)`, `SUM(Incasso)`                  | `SUM(Consulenza)`, `SUM(Incasso)`   |
| Filtri (`WHERE`) | Regione (Lombardia)                                | Nazionalità (Italiane, Tedesche)                   | Anno (2017, 2018, 2019)             |
| `GROUP BY`       | Semestre, TipologiaServizio                        | Regione, Servizio, Anno                            | Nazionalità, TipoServizio, Semestre |


### Query A
```SQL
SELECT T.Semestre, S.TipologiaServizio, 
--- Visualizzare l’incasso totale e il numero totale di consulenze
SUM(INCASSO.Incasso) AS TOT_INCASSO
SUM(INCASSO.Consulenze) AS TOT_CONSULENZE
FROM INCASSO
JOIN SERVIZIO S ON S.IdServizio = INCASSO.IdServizio
JOIN TEMPO T ON T.IdTempo = INCASSO.IdTempo
GROUP BY T.Semestre, S.TipologiaServizio
```

### Creazione combinazione minimale
>[!example]
>Si individui la combinazione minimale di attributi che costituisce un identificatore per la vista
materializzata ViewIncassi

Combinazione minimale: Servizio, Semestre, Regione, Nazionalità

### Non Utilizzare la `CREATE`
Si ipotizzi che che la vista materializzata ViewIncassi sia gestita senza utilizzare l’istruzione `CREATE MATERIALIZED VIEW`. La tabella derivata che realizza la vista materializzata è definita dalla seguente istruzione SQL

``` sql
CREATE TABLE ViewIncassi
(
	Servizio VARCHAR(20),
	TipologiaServizio VARCHAR(20),
	Nazionalità VARCHAR(20),
	Semestre VARCHAR(20),
	Anno VARCHAR(20),
	Regione VARCHAR(20),
	IncassoTot INTEGER
	CHECK (IncassoTot IS NOT NULL and IncassoTot >0),
	NumConsulenzeTot INTEGER
	CHECK (NumConsulenzeTot IS NOT NULL and NumConsulenzeTot >0),
	PRIMARY KEY (Nazionalità, Semestre, Regione, Servizio)
)
```

Si scriva l’istruzione INSERT per il caricamento iniziale dei dati nella vista materializzata
ViewIncassi, utilizzando l’istruzione `INSERT(SELECT…)`

```sql
INSERT (Servizio, TipologiaServizio, Nazionalità, Semestre, Anno, Regione, IncassoTot, NumConsulenzeTot)

SELECT T.Semestre, S.TipologiaServizio, 
--- Visualizzare l’incasso totale e il numero totale di consulenze
SUM(INCASSO.Incasso) AS TOT_INCASSO
SUM(INCASSO.'#Consulenze') AS TOT_CONSULENZE
FROM INCASSO
JOIN SERVIZIO S ON S.IdServizio = INCASSO.IdServizio
JOIN TEMPO T ON T.IdTempo = INCASSO.IdTempo
GROUP BY T.Semestre, S.TipologiaServizio
```

### Creazione del TRIGGER
```sql
CREATE OR REPLACE TRIGGER Trigger_VM
AFTER INSERT ON INCASSO
FOR EACH ROW

DECLARE
	Anno_var INTEGER
	Semestre_var, Servizio_var, TipoServizio_var VARCHAR(20);
	Regione_var, Nazionalita_var VARCHAR(20);
	N INTEGER
BEGIN
---
END
```