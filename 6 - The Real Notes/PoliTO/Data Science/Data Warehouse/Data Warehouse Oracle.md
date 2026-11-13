---
created: 2026-10-08
tags:
  - baby
topics:
  - Data
  - DataWareHouse
author: Danilo Quattrini
---
# Funzioni OLAP
---
Prendiamo una tabella vendite:
```
VENDITE(_Città_, Data, Importo)
```
Eseguiamo un raggrupamento a livello fisico 
>[!example] Esempio
>Selezionare, separatamente per ogni città, per ogni data l’importo e la media dell’importo considerando la riga corrente e le due righe che la precedono
>```sql
>SELECT Città, Data, Importo AVG(Importo) 
>OVER ( PARTITION BY Città ORDER BY Data ROWS 2 PRECEDING) 
>AS MediaMobile
>ORDER BY Città, Data
>```
>
>1. Bisogna partizionare i dati? Si, rispetto a Città
>2. Bisogna fare l'ordinament? Si, per data e server per fare la media dell'importo

## Esempio di Ranking
Prendiamo lo schema:
```
FRN(_COD_F_, Nome, Sede_F)
ART(_COD_A_, Tipo, Colore, Peso)
PRG(_COD_P_, Nome, Sede_P)
FAP(_COD_F_, _COD_P_, _COD_A_, Q)
```
Selezionare per ogni articolo la quantità totale venduta e il “ranking” in funzione delle quantità totali vendute per ogni articolo. Qui devo raggruppare dalla Tabella FAP con il codice articolo (_COD_A_), e poi fare una classifica a tutti i prodotti, dove non serve fare il partizionamento ma devo fare un ordinamento decrescente
```sql
SELECT COD_A, SUM(Q) AS QTot,
RANK() OVER (
			ORDER BY SUM(Q)
		) AS RankVendite
FROM FAP
GROUP BY COD_A;
```


| COD_A  | QTot | Rank Vendite |
| ------ | ---- | ------------ |
| A2  1  | 300  | 1            |
| A5     | 1100 | 2            |
| A4     | 1300 | 3            |
| <br>A6 | 1300 | 3            |
| <br>A1 | 1900 | 5            |
| A3     | 4500 | 5            |

# Reference
---

