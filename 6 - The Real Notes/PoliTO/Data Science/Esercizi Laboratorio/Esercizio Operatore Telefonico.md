---
created: 2026-10-27
tags:
  - baby
topics:
  - Data
  - DataWareHouse
author: Danilo Quattrini
---
# Esercizio Operatore Telefonico
---
## Schema concettuale
![[Screenshot 2026-10-27 at 16.27.04.png]]

## Schema Logico
Calls(**Id_Time**, **Id_Location**, **Id_PhoneRate**, price, number_of_calls)

Time(**Id_Time**, Month, Year, DayOfTheWeek)

Location(**Id_Location**, _Id_Reciver_, _Id_Caller_, City, Province, Region)

PhoneRate(**Id_PhoneRate**, PhoneRateType)

## Query
Seleziona
- il reddito annuo per ogni tariffa telefonica,
- il reddito totale per ogni tariffa telefonica, il reddito annuo totale e il reddito totale
```sql
SELECT

P.PHONERATETYPE,

T.DATEYEAR,

  

-- 1. Reddito annuo per ogni tariffa (aggregazione base del GROUP BY)

SUM(PRICE) AS REDDITO_ANNUO_PER_TARIFFA,

  

-- 2. Reddito totale per ogni tariffa (sommato su tutti gli anni)

SUM(SUM(PRICE)) OVER (

PARTITION BY P.PHONERATETYPE

) AS REDDITO_TOT_PER_TARIFFA,

  

-- 3. Reddito annuo totale (sommato su tutte le tariffe per ciascun anno)

SUM(SUM(PRICE)) OVER (

PARTITION BY T.DATEYEAR

) AS REDDITO_ANNUO_TOT,

  

-- 4. Reddito totale complessivo (finestra vuota su tutto il dataset)

SUM(SUM(PRICE)) OVER () AS REDDITO_TOT_COMPLESSIVO

  

FROM FACTS
--- JOIN CONDITION
JOIN PHONERATE P ON FACTS.ID_phoneRate = P.ID_phoneRate
JOIN TIMEDIM T ON FACTS.ID_time = T.ID_time
GROUP BY P.PHONERATETYPE, T.DATEYEAR;
```

Seleziona il numero mensile di chiamate e il reddito mensile. Associa il RANK a ogni mese in base al suo reddito 1 per il mese con il reddito più alto, 2 per il secondo, ecc., l'ultimo mese è
quello con il reddito più basso)
```SQL
SELECT T.DATEMONTH,

-- NUMERO MENSILE DI CHIAMATE

SUM(FACTS.NUMBEROFCALLS) AS NUM_MENSILE_CHIAMATE,

-- REDDITO MENSILE

SUM(FACTS.PRICE) AS REDDITO_MENSILE,

-- CREA UN RANK PER IL MESE CON IL REDDITO PIU' ALTO
-- POI ORDINA LA SOMMA IN MODO DECRESCENTE PER FAR SI DI AVERE
-- UN ORDINE DAL PIU' PICCOLO AL PIù GRANDE
RANK() OVER(

ORDER BY SUM(FACTS.PRICE) DESC

) AS MIGLIOR_REDDITO

  

FROM FACTS
JOIN TIMEDIM T ON FACTS.ID_TIME = T.ID_TIME
GROUP BY T.DATEMONTH;
```

