---
created: 2026-09-30
tags:
  - baby
topics:
  - Data
  - DataWareHouse
author: Danilo Quattrini
---
# Progettazione Logica
---
## Questions
- Che cos'è uno schema logico?
- Come lo si rappresenta?
- Che chiavi vengono usate per identificare una tabella nello schema logico?
- Come vengono trasformate le dimensioni che appartengono ad una tabella di fatti in uno schema logico?
- Quali sono i due approcci che vengono utilizzati per gestire gli archi multipli?

---
La **progettazione logica** consiste nella rappresentazione dello schema delle tabelle mediante il modello relazionale ROLAP (i modelli MOLAP e HOLAP non sono molto utilizzati).
Lo schema delle tabelle viene fatto tenendo a mente la progettazione concettuale, il carico di lavoro, il volume dei dati e i vincoli di sistema (direttive per ETL). La progettazione logica, in questo caso **consente la ridondanza dei dati e la de-normalizzazione** delle tabelle.

La de-nomalizzazione non è una cosa negativa, perché ci rende capaci di eseguire query veloci ed efficienti.

## Schema Logico
![[Screenshot 2026-09-30 at 12.14.14.png]]
Questo è l'esempio di uno **schema logico a stella**, cosa succede dallo schema concettuale a quello logico?

La/e **dimensione/i**, diventano delle singole tabelle, al quale viene aggiunta una chiave primaria [[Termini Data Science#"Chiave Surrogata" vs "Chiave Primaria"|chiave surrogata]], cioè ci sarà sempre un *ID_nome_dimensione*

I **Fatti** diventano anche loro delle tabelle però con **chiavi primarie costruire** dalla combinazione delle **chiavi esterne delle dimensioni** e le **misure sono rappresentate come attributi della tabella**.

Una **dimensione opzionale**, in base alle specifiche di progetto può essere inclusa o meno nella chiave primaria (nel secondo caso è possibile avere solo un valore possibile per l’attributo opzionale relativamente a quella chiave primaria)

## Archi Multipli
Le query che caratterizzano un'**arco multiplo sono di due tipi**:
- **Pesato**: viene inserito il peso nell'arco multiplo (il peso è un attributo della bridge table)
- **D'Impatto**: non si considerano minimamente i pesi.

L'arco multiplo può essere modellato in due modi:
- Tabella che modella l'arco multiplo, chiamata **bridge table**, che modella le relazioni molti a molti (questa è la soluzione utilizzata maggiormente), che sarebbe l'immagine nella sinistra.
- Si può anche spostare l'arco multiplo in un'altra tabella dei fatti, questo è chiamato approccio **Push-down**
![[Screenshot 2026-09-30 at 12.20.25.png]]
## Dimensione degenere
Una **dimensione degenere** è una dimensione costituita da un solo attributo ed è rappresentabile mediante 3 soluzioni distinte:

- **Junk dimension**: in presenza di più dimensioni degeneri esse vengono raggruppate figurando come unica dimensione (relazionate in contenuto). La nuova dimensione deve poter rappresentare tutte le possibili combinazioni delle dimensioni al suo interno, questa soluzione viene quindi attuata solo per cardinalità limitate del dominio degli attributi.
  
- **Push Down** nella tabella dei **fatti** (per attributi di dimensione contenuta – es pochi kB) e nella rispettiva chiave primaria.
  
- Viene trattata come una **dimensione normale**, ciò consente l’aggiunta futura di gerarchie
# Reference
---

