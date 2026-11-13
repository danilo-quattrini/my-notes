---
created: 2026-10-13
tags:
  - baby
topics:
  - DataWareHouse
  - Data
  - "[[School]]"
author: Danilo Quattrini
---
# Esercizio Progettazione DW
---
>[!info]
>Link consegna [qui](https://www.kaggle.com/daniloquattrini)

---
## Introduzione 
Andremmo a rappresentare uno **schema concettuale** di quello che la consegna richiede in questo esempio avremmo una ditta di elettrodomestici, nella quale dobbiamo gestire un magazzino. Nello schema concettuale dobbiamo creare delle tabelle dei fatti, che abbiamo già visto come si fa in questi appunti [[Progettazione Concettuale#Conversione dal modello ER al modello DFM|qui]] che poi dopo sarà convertito in uno schema logico.

Poi si vanno a creare delle query tramite [[Analisi Dei Dati#Estensioni del Linguaggio|finestre di calcolo]].

E infine si creeranno delle [[Progettazione Fisica & Viste|viste materializzate]].

## Schema Concettuale
Per la realizzazione dello schema concettuale bisogna prima di tutto:

1. **Identificazione del fatto**: il primo punto per risolvere l'esercizio, ce ne possono essere uno o più fatti di interesse, questo lo si vede nel testo, che contengono delle misure (quantità, importo, conti, ecc...).
2. **identificare le dimensioni**: sono i punti nella quale si vanno a tagliare le nostre aggregazione, dove i dati possono avere dipendenze temporali.
	- **Identificare le gerarchie**: 
	- **Livelli minimi di aggregazione**
### Identificare i fatti
Leggendo il testo possiamo già identificare dei fatti, che saranno delle metriche, per esempio
![[Screenshot 2026-10-13 at 18.32.15.png]]
questa è una dimensione universo, che non mappiamo perché sono comuni a tutti i magazzini quindi non ci interessa.

Poi si legge il testo e si sottolinea le parti che sono dei fatti, che ho evidenziato di giallo e blu invece che sono le misure.![[Screenshot 2026-10-13 at 18.45.45.png]]
Nell'esame non sarà in figure ma sarà in forma testuale.![[Screenshot 2026-10-13 at 18.50.00.png]]

![[Screenshot 2026-10-14 at 11.42.57.png]]

==(da completare lezione 12/10/2026 minuto 34:03)==

### Formalismo Testuale
Siccome non andremmo a disegnare le tabelle dei fatti, ma si scriverà in forma testuale in questo sito: [Mermaid](https://mermaid.ai/app/projects/8edde0b7-1f09-4d1b-8abe-1fa9742ab108/diagrams/7e1429dc-6fae-4c6b-99a4-338932b5a8ec/version/v0.1/edit?shouldShowPopup=true&fromOnboarding=true)
```
flowchart LR

F[[

USO MAGAZZINI

---

sup_libera

suP_TOTALE

]]
```

Sopra si scrive una fact table in questo modo, si definisce una fact table con `F[[<nome_fatto>]]`

Per definire poi dopo le dimensioni del fatto, si fa il seguente codice con i tratti `---` 
```
F --- magazzino --- citta --- regione
```
Si possono creare le gerarchie in questo modo:
 ```
F --- Data --- M;

M --- 3M --- 6M --- anno;

M --- 4M --- anno;
 ```

Il risultato viene così
![[fact-table-electronics-shop.svg|1120]]

Stessa cosa invece lo vedremmo con la tabella prodotti:

## Schema Logico
Dopo aver creato lo schema concettuale si andrà a creare uno schema logico, che si dovrà fare in questo modo:
1. Definire gli attributi in relazione alla gerarchia
2. **Stima del carico di lavoro**: possiamo verificare se le dimensioni che abbiamo scelto siano le migliori e sono ottimizzate, senza nessuna eccedenza

===(Spiegare come avviene la progettazione logica)===

>[!warning] IMPORTANTE
>NON SI METTE LE CHIAVE PRIMARIE NEI FATTI NELLO SCHEMA LOGICO.
>Cioè scrivere: 
>- ❌ Uso_magazzino(_Id_usoMagazzino_) 
>- ✅ Uso_magazzion(Id_magazzino), vanno le chiavi primarie delle dimensioni, perché nell'ER sono entità che sono fuoriuscite da relazioni N-to-N


La progettazione logica del primo fatto che sarebbe **Magazzino è la seguente**:
- **Uso_Magazzino** (_Id_Magazzino_, _Id_Tempo_, sup_libera, sup_totale)

- **Magazzino** (_Id_Magazzino_, magazzino, citta, provincia, regione)

- **Tempo**(*Id_tempo*, Data, Mese, 3M, 4M, 6M, anno, settimana)

La progettazione logica dei Prodotti è la seguente (i duplicati vanno bene e devono esserci)
- **Prodotti** (*Id_Magazzino*, *Id_Modello*, *Id_Tempo*, \#Prodotti, valore), dove **#Prodotti** sarebbe il numero dei prodotti del fatto **Prodotti**

- **Modello**(*Id_Modello*, modello, categoria)

- **Tempo**(*Id_tempo*, Data, Mese, 3M, 4M, 6M, anno, settimana)

- **Magazzino** (_Id_Magazzino_, magazzino, citta, provincia, regione)
## Query
Dopo si svolgono le query
>[!exercise] Query 1
>Relativamente al primo trimestre dell’anno 2013, considerando solo i magazzini della città di Torino, trovare per ogni coppia (magazzino,data) il valore complessivo di prodotti presenti in tale data nel magazzino e il valore complessivo medio giornaliero di prodotti presenti nel magazzino nel corso della settimana precedente la data in esame (data in esame inclusa).

**Soluzione** 
```sql
SELECT m.magazzino , t.data, SUM(p.valore) 
	AVG(SUM(p.valore))OVER (
		PARTITION BY magazzino
		ORDER BY data 
		RANGE BETWEEN '6' DAY PRECIDING AND CURRENT ROW
	)
FROM Prodotti as p
JOIN Magazzino m on p.id_magazzino = m.id_prodotto
JOIN Tempo t on t.id_tempo = p.id_tempo
WHERE m.citta LIKE "Torino" AND t.3M LIKE "2013-1"
GROUP BY magazzino, data
```

>[!exercise] Query 2
>Relativamente all’anno 2004, trovare per ogni coppia(città,data):
>- La **percentuale** di superficie libera giornaliera nella città.
> - Associare ad ogni coppia un attributo di **rank** legato alla percentuale di superficie libera giornaliera nella città (1 per la coppia con la più bassa percentuale di superficieibera giornaliera).

**Soluzione**
```SQL
SELECT m.citta, t.data, 
SUM(UM.sup_libera) /  (UM.sup_totale) * 100 AS Percentuale
RANK OVER(
	ORDER BY SUM(UM.sup_libera) /  (UM.sup_totale) * 100 
)
FROM Uso_Magazzino as UM
JOIN Magazzion m ON m.Id_magazzino = UM.Id_magazziono
JOIN Tempo t ON t.Id_tempo = UM.Id_tempo
WHERE t.anno LIKE "2004"
GROUP BY m.citta, t.anno
```

NON si può scrivere nella `RANK OVER (ORDER BY Percentuale)` perché l'operazione di `SELECT`  fa tutto insieme, quindi bisogna riscrivere tutta l'operazione `SUM(UM.sup_libera) /  (UM.sup_totale) * 100`

>[!exercise] Query 3
>Relativamente all’anno 2013:
>- Trovare per ogni coppia (magazzino,mese) il valore complessivo medio giornaliero di prodotti presenti.

```sql
SELECT m.magazzino, t.mese, 
SUM(p.valore) / COUNT(DISTINCT(t.data))
FROM Prodotti AS P
JOIN Magazzino m ON p.Id_magazzino = m.Id_magazzion
JOIN Tempo t ON p.Id_Tempo = t.Id_Tempo
WHERE t.anno LIKE "2013"
GROUP BY m.magazzino, t.mese
```

**Soluzione 2**
```sql
SELECT m.magazzino, t.mese, 
AVG(SUM(Valore)) OVER (PARTITION BY t.mese, m.magazzion)

FROM Prodotti AS P

JOIN Magazzino m ON p.Id_magazzino = m.Id_magazzion
JOIN Tempo t ON p.Id_Tempo = t.Id_Tempo
WHERE t.anno LIKE "2013"

GROUP BY t.data, m.magazzino, t.mese
```
Perché ci sono due aggregazione cioè come mai c'è `AVG(SUM(Valore))`?
Seguendo l'ordine di esecuzione della query prima stiamo facendo un'aggregazione a `m.magazzino`, `t.mese`, `t.data`, le stiamo sommando con la `SUM` al risultato della`GROUP BY`, invece l'`AVG`, lo facciamo al risultato della finestra di calcolo, che in questo caso è riferito alla partizione (`PARTITION BY`).


# Esercizio Compagnia di Vini
![[Screenshot 2026-10-17 at 11.13.30.png]]

==(Da completare con spiegazione di come si è arrivati qui)==
![[wine-company.png]]

### Schema Logico
Tempo (**IdTempo**, Mese, 2M, 3M, 4M, 6M, Anno)
TipoVino(**IdTipoVino**, NomeTipoVino, DOC, DOP, DOCG)
LuogoAzienda(IdLuogoAzienda, Provincia, Regione, AreaGeografica)
LuogoDestinazione(IdLuogoDestinazione, Stato, Continente)
Confezione(IdConfezione, TipoConfezione)

Esportazione( **IdTempo**, **IdTipoVino**, **IdLuogoAzienda**, **IdLuogoDestinazione**,
                         IdConfezione, DimensioneOrdine, TotLitri, PrezzoTotale)

### Query
>[!info] Query 1
>Considerando solo i vini che hanno la certificazione “DOC” esportati in Asia, selezionare il prezzo medio al litro per ogni anno, la percentuale di litri esportati nell’anno rispetto al totale di tutti gli anni, e il totale cumulativo annuale di litri esportati. Si effettui l’analisi separatamente per ogni tipo di confezionamento

```SQL
SELECT C.TipoConfezione, T.Anno
	-- Selezionare il prezzo medio al litro per ogni anno
	SUM(Esportazione.PrezzoTotale) / SUM(Esportzione.TotLitri),
	
	-- La percentuale di litri esportati nell’anno rispetto al totale di tutti gli anni
	(SUM(Esportazione.TotLitri) / SUM(SUM(Esportazione.TotLitri)) OVER (PARTITION BY NomeTipoConfezione)) * 100,
	
	-- Il totale cumulativo annuale di litri esportati
	SUM(SUM(Esportazione.TotLitri)) OVER (
		PARTITION BY NomeConfezione
		ORDER BY T.Anno
		ROWS UNBOUNDED PRECEDING
	)
FROM Esportazione 
JOIN TipoVino TV ON Esportazione.IdTipoVino = TV.IdTipoVino
JOIN LuogoDestinazione LD ON Esportazione.IdLuogoDestinazione = LD.IdLuogoDestinazione
JOIN Tempo T ON Esportazione.IdTempo = T.IdTempo
JOIN Confezione C ON Esportazione.IdConfezione = C.IdConfezione
WHERE TV.DOC = 1 AND LD.Continente = 'Asia'
GROUP BY TV.DOC
```

>[!info] Query 2
> Per ogni regione:
> -  selezionare il prezzo medio al litro
>  - il numero medio di litri di vino esportati per provincia
>  - la percentuale di litri di vino esportati da ogni regione rispetto al totale dell’area geografica di appartenenza (Nord, Centro, Sud). 
> 
> Si effettui l’analisi separatamente per ogni anno

```SQL
SELECT T.Anno, LD.Regione, LA.AreaGeografica
-- Selezionare il prezzo medio al litro
SUM(Esportazione.TotLitri) / SUM(Esportazione.PrezzoTotale) 

--- Il numero medio di litri di vino esportati per provincia
--- Pattern media mensile
SUM(Esportazione.TotLitri) / COUNT(DISTINCT(LA.Provincia))

-- La percentuale di litri di vino esportati da ogni regione rispetto al totale dell’area geografica di appartenenza (Nord, Centro, Sud). 
100 * SUM(Esportazione.TotLitri) / SUM(SUM(Esportazione.TotLitri)) OVER(
	PARTITION BY T.Anno, LA.AreaGeografica
)

FROM Esportazione
JOIN Tempo T ON Esportazione.IdTempo = T.IdTempo
JOIN LuogoAzienda LA ON Esportazione.IdLuogoAzienda = LD.IdLuogoAzienda
WHERE
GROUP BY LD.Regione, T.Anno, LA.AreaGeografica
```
