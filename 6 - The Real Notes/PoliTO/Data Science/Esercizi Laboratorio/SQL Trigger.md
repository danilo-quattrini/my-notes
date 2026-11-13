---
created: 2026-02-14T15:43:00
tags:
  - baby
topics:
author: Danilo Quattrini
---
# SQL Trigger
---
I **Trigger** sono delle operazioni che vengono svolte in SQL che si attivano dopo un operazione di **DML** (Data Manipulation Language, come INSERT, UPDATE, DELETE, ecc...). Per definire un trigger si fa in questo modo:
```SQL
CREATE OR REPLACE TRIGGER nome_trigger
AFTER INSERT ON tabella_che_riceve_la_modifica
FOR EACH ROW
BEGIN
END
```

- `CREATE OR REPLACE`: crea o rimpiazza il trigger se questo è già esistente.

- `AFTER INSERT ON...`: ci dice quando viene attivato il trigger, questo valore può essere anche `AFTER INSERT OR UPDATE OR DELETE`, si possono inserire tutte le operazioni DML

- `FOR EACH ROW`: Attiva il trigger per ogni singola riga inserita durante la transazione. 

- **La variabile pseudo-record `NEW`**: All'interno del blocco `BEGIN ... END`, si accede ai valori della riga appena inserita usando la sintassi `NEW.nome_colonna` (ad esempio `NEW.pocket_price` o `NEW.Id_date`). 
## Controllo di Valori Già Presenti
Per controllare dentro ad un trigger se quando si vanno ad inserire dei valori nuovi, oppure si devono fare delle modifiche a dei valori esistenti ci sono due approcci:

1. Costruttore `MERGE` ANSI, che si utilizza in questo modo:
```sql
MERGE table1 
	USING table2
	ON table1.key = table2.key
	
	WHEN MATCHED THEN UPDATE -- There are matching values in both tables; save the values from table2 
		SET -- set fields here, so for example firstname = table2.firstname
	
	WHEN NOT MATCHED BY TARGET THEN -- this is a new record
		INSERT -- list of fields to insert would follow, like an INSERT query
	
	WHEN NOT MATCHED BY SOURCE THEN -- this record was deleted
		DELETE -- Nothing else needs to go here; just the word DELETE 

```


# Reference
---
[DML](https://www.geeksforgeeks.org/sql/sql-ddl-dql-dml-dcl-tcl-commands/#:~:text=3,HR%27%2E)
[Merge Syntax](https://ericcameron.dev/database-merge.html)