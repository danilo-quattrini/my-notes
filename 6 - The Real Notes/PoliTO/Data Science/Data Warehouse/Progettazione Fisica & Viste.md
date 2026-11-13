---
created: 2026-10-05
tags:
  - baby
topics:
  - Data
  - "[[School]]"
author: Danilo Quattrini
---
# Progettazione Fisica
---
## Questions
### Viste
- Che cosa sono le viste materializzate?
- Qual'è la differenza tra una vista classica e una vista materializzata?
- A che cosa servono le viste materializzate?
- Come sono strutturate? Come vengono definite?
- Cosa conviene fare al progettista dati quando si devono creare delle viste?
### Progettazione Fisica
- Cosa intendiamo come progettazione fisica?
- Che cosa facciamo nella progettazione fisica
- Quali sono le fasi della progettazione fisica?
- Come si scelgono gli indici?

---
# Viste
>[!quote] Che cos'è una vista materializzata
>Le viste sono **sommari pre-calcolati** (tabelle già fatte e salvate sul disco) della tabella dei fatti che sono memorizzati direttamente nel DW e che permettono di aumentare l’efficienza delle interrogazioni che richiedono aggregazioni.

### Categorie di Viste
Le viste possono essere di due tipologie:
- **Vista classica (virtuale):** È un semplice **segnalibro** o una **ricetta**. Non contiene dati reali. Ogni volta che la interroghi, il database parte da capo, legge milioni di righe grezze dalla tabella dei fatti, esegue le somme e ti mostra il risultato. Se la query richiede 5 minuti per calcolare le somme, impiegherà 5 minuti ogni singola volta che la esegui.
    
- **Vista materializzata:** È un **piatto già cucinato e conservato in frigorifero**. Il database esegue la query pesante una volta sola (es. di notte), prende la tabella con i totali già calcolati e la **scrive su disco** come se fosse una vera tabella. Quando fai una domanda al database, questo non riscorrere miliardi di transazioni grezze: legge direttamente il risultato pronto in pochi millisecondi.
![[Screenshot 2026-10-07 at 11.47.43.png]]

Le **viste materializzate servono** per ottimizzare le query permettono di aumentare l’efficienza
delle interrogazioni che richiedono aggregazioni ma anche per rispondere a più interrogazioni diverse. 

>[!done] Vantaggi delle viste materializzate
>- **Riduzione dei tempi per le risposte delle query**: questo è dovuto dalla disponibilità della risposta della query all'interno della struttura dati (o DW)
>  
>- **Riduzione del calcolo**:  si evitano di ripetere le operazioni di aggregazioni (JOIN condition) in modo da evitare lo stress sui data warehouse
>  
>  - **Riutilizzo multi-query:** Una singola vista materializzata con un dettaglio intermedio (ad esempio le vendite giornaliere per città) è in grado di rispondere sia alla query _"qual è il totale settimanale per città?"_ sia a _"qual è il totale mensile per regione?"_, evitando di dover interrogare la tabella dei fatti originale

![[Screenshot 2026-10-07 at 11.55.26.png]]
Il **reticolo delle viste** rappresenta l’insieme delle viste materializzate di cui si ha bisogno, rappresentando, spostandosi verso il basso, le viste con un contenuto più aggregato.

Questo avviene utilizzando le istruzioni **SQL**, nella query si avrà o da viste con un contenuto meno aggregato di quello che si vuole generare. È opportuno inserire anche delle generalizzazioni rispetto alle dimensioni (ad esempio Stato per la dimensione Città) che permettono di riutilizzare la vista pur non occupando molto spazio aggiuntivo

Rispondo all query dei pallini verdi e rossi, si legge dal basso verso l'alto.

>[!question] A che cosa serve una vista materializzata?
Una vista materializzata può essere utilizzata per rispondere a più interrogazioni diverse

È necessario che l’insieme **“ottimo” minimizzi i tempi di esecuzione delle query** e di aggiornamento delle viste rispettando a dei vincoli:
- **Spazio disponibile su disco**: cioè se non si possiede molto spazio sul disco dobbiamo pensare a delle soluzioni semplici.
- Tempo a disposizione per l’aggiornamento (solitamente la periodicità dell’aggiornamento è giornaliera)
- Tempo di risposta
- **Freschezza dei dati**: con il processo [[Alimentazione del DW|ETL]] i dati quando vengono aggiornati o aggiunti in una data warehouse, quest'ultimi devono essere anche aggiornati all'interno delle viste, per poter ottenere la "freschezza" dei dati.
### Esempio Di ottimizzazione
![[Screenshot 2026-10-07 at 12.01.39.png]]
Supponiamo 3 interrogazioni (query $q$) su un **reticolo delle viste**, dove contengono le operazioni di `GROUP BY` (raggrupamento),  le possibile viste candidate sono i pallini verdi + i pallini gialle, che possono ridurre il tempo di esecuzione.
![[Screenshot 2026-10-07 at 12.03.25.png]]
Ho una vista che risponde a 3 interrogazioni, che avrà il livello di dettaglio più specifico, che avrà un costo più alto, perché sono più dettagliate, delle query $q_{1}$ e $q_{2}$ .
![[Screenshot 2026-10-07 at 12.05.24.png]]
Se ho una vista, avrà un dettaglio più specifico con un costo elevato ma più spazio tempo di aggiornamento.
![[Screenshot 2026-10-07 at 12.06.37.png]]
Soluzione intermedia creo due viste

Per vedere come viene applicata in SQL vedere [[Esercizio Viste Materializzate#5. Creazione Viste Materializzate|qui]]
# Progettazione Fisica
Nella progettazione fisica si prende in considerazione le diverse strutture fisiche e si definisce le strutture fisiche accessorie per migliorare le interrogazioni alla DW. 

Si andrà anche a velocizzare l'accesso ai dati, **questo tramiti indici per migliorare le interrogazioni delle query**. Ci sono anche qui le viste materializzate perché sono strutture accessorie che possono esserci o non (vengono utilizzate però nelle `GROUP BY`).

>[!info] Cosa sono gli indici? 
>Un **indice** è come l'**indice analitico in fondo a un libro**: una mappa separata che associa a ogni valore (es. la regione "Lombardia") la posizione esatta su disco (i _Row ID_ o numeri di pagina) in cui si trovano quei dati. Quando fai la query, il database non legge 500 milioni di righe, ma va a colpo sicuro sulla posizione indicata dall'indice.

## Fasi della progettazione fisica
La progettazione fisica è composta da diverse fasi:

- **Analisi del Carico di Lavoro e Stima dei Volumi:** Prima di creare indici a caso, si esaminano le query più frequenti e critiche fatte dagli utenti di business, stimando la quantità di dati da memorizzare e la sparsità dei dati (cioè la varietà dei dati).

- **Definizione delle strutture fisiche accessorie**:
  Qui si scelgono gli indici che variano in base all'utilizzo
	- **Indici di bitmap**: permettono di eseguire operazioni legate ai predicati di selezione più velocemente (clausole `WHERE`).
	  
	- **Indici per i Join**: pre-calcolano il **JOIN**, permettono di eseguire operazioni di join più velocemente memorizzando delle tabelle che contengono già i row id da andare ad

- **Tuning**: verificare se la progettazione fisica soddisfa le necessità applicative, se le necessità non vengono soddisfatte le strutture accessorie vanno riprogettate. In questa fase si osserva se le strutture fisiche vengono utilizzate o meno dall’ottimizzatore
  

## Scelta degli Indici
Per l’indicizzazione delle dimensioni è opportuno creare un indice per gli attributi coinvolti in


| Operazione SQL da velocizzare | Tipo di Attributo / Contesto                                                                               | Struttura Fisica da Scegliere | Spiegazione Pratica                                                                                                                                          |
| ----------------------------- | ---------------------------------------------------------------------------------------------------------- | ----------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Filtri di Selezione (`WHERE`) | **Alta Cardinalità**<br><br>(molti valori distinti, es. _Codice Cliente, Codice Fiscale, Numero Telefono_) | **Indice B-tree**             | Funziona come un albero di ricerca bilanciato: velocissimo quando devi cercare valori univoci o ristretti tra milioni di possibilità.                        |
| Filtri di Selezione (`WHERE`) | **Bassa Cardinalità**<br><br>(pochi valori distinti, es. _Sesso, Stato Ordine, Categoria, Regione_)        | **Indice Bitmap**             | Associa a ogni valore una stringa di bit (0 e 1). Occupa pochissimo spazio ed è super veloce nelle combinazioni logiche (`AND`, `OR`) tra più dimensioni.    |
| Operazioni di `JOIN`          | Legame tra Fatto e Dimensione (es. `FACTS.ID_Prodotto = PRODOTTO.ID_Prodotto`)                             | **Bitmap Join Index**         | Pre-calcola e memorizza l'operazione di `JOIN` direttamente all'interno dell'indice. Evita al database di dover unire fisicamente le due tabelle ogni volta. |
| **Operazioni di `GROUP BY`**  | Aggregazione di più valori per una determinata colonna della tabella                                       | Vista Materializzata          | Pre-calcola il risultato della `GROUP BY` e lo salva su disco come tabella pronta all'uso                                                                    |

