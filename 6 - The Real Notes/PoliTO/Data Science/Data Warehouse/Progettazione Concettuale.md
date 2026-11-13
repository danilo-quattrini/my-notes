---
created: 2026-10-05
tags:
  - baby
topics:
author: Danilo Quattrini
---
# Question
---
## Introduzione
- Come viene utilizzato un Dimensional Fact Model?
- Che differenza c'è tra un Dimensional Fact Model ed un modello relazionale E/R?
- Che cosa rappresenta un Dimensional Fact Model?
## ER vs DMF
- Come possiamo associare gli elementi del modello ER con quelli del DMF?
- Descrivi gli elementi di un DMF
- Che cos'è una dipendenza funzionale?
- Come si converte un modello ER ad uno DFM?
- Fammi un esempio di di un DFM.
## Costrutti Avanzati del DFM
- Quali sono i costrutti avanzati del DFM? [[#Costruttori Avanzati|risposta qui]]
- Spiega bene la differenza tra arco multiplo tra attributo dimensionale e fatto e invece tra attributo dimensionale ad attributo dimensionale.
- Perché è preferibile utilizzare un arco multiplo tra **attributi dimensionali** invece che tra **attributo e dimensione**?
- Fai un esempio di soluzione di come spostare l'arco multiplo dal fatto alla dimensione, tra le dimensioni stesse.
## Variazione dei Dati nel Tempo
- Quali sono le casistiche dei cambiamenti che possono subire gli attributi dimensionali nel tempo?
---
# Definizione
Schema logico normalizzato perché privo di ridondanze, per la qualità delle informazioni. Il modello E/R per avere questo schema **normalizzato** crea tante dipendenze tra le tabelle ed è pesante con le relazioni, inoltre non contiene nessun tipo di dato duplicato. 

Noi Invece vogliamo create una DW con dati già generati e cerchiamo di ridurre l'utilizzo dei JOIN. Per questo motivo una DW uno schema **de-normalizzat**o, dove le **duplicazioni vanno bene, e bastano che le query siano efficienti**.

# Dimensional Fact Model
Utilizziamo il ***Dimensional Fact Model*** che definisce schemi di fatto che **modellano i fatti, le dimensioni, le misure e le gerarchie** e rappresenta un modello grafico che offre una documentazione utile per la revisione dei requisiti e per comprendere a posteriori le motivazioni delle scelte fatte.![[Screenshot 2026-09-28 at 18.25.07.png]]
Questo modello viene utilizzato non per il singolo negozio ma per un'insieme di negozi. Prima si analizza un macro-trend, vedendo il fenomeno, si va a svolgere un analisi approfondita. 

## Corrispondenza tra modello ER e DFM
Con la tabella sottostante vediamo come associamo ogni elemento del modello ER con il DFM

| Modello E/R (Database Operativo / OLTP)                                                                                       | Dimensional Fact Model (Data Warehouse / OLAP) | Ruolo nella Data Warehouse                                                                                                                                |
| ----------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Entità / Relazione N-a-M (moliti-a-molti) centrale dove avvengono le transazioni** (es. _Vendita_, _Scontrino_, _Ricovero_) | **Fatto (Fact)**                               | Rappresenta l'**evento o il fenomeno aziendale di interesse da analizzare.**                                                                              |
| **Attributi numerici e aggregabili** delle entità transazionali (es. _Importo_, _Quantità_, _PrezzoTotale_)                   | **Misure (Measures)**                          | **Valori numerici aggregabili** (somma, media, conteggio) contenuti nello schema di fatto.                                                                |
| **Entità collegate con relazioni 1-a-N** attorno all'evento transazionale (es. _Cliente_, _Prodotto_, _Tempo_, _Negozio_)     | **Dimensioni** (Dimensions)                    | Assi o coordinate attraverso cui contestualizzare e "tagliare" ([[Analisi Dei Dati#^1e4921\|slice]] or dice) le misure.                                   |
| **Catene di Relazioni 1-a-N ed Entità Padri** (es. _Prodotto_ $\rightarrow$ _Categoria_ $\rightarrow$ _Reparto_)              | Gerarchie di Attributi Dimensionali            | Livelli di aggregazione per eseguire operazioni di _Roll-up_ e _Drill-down_, vedere esempio di sotto sull'immagine                                        |
| **Dipendenza Funzionale ($A \rightarrow B$)** o Relazione 1-a-N tra entità                                                    | Arco diretto tra attributi della gerarchia     | Un arco orientato con pallino indica che a ogni valore dell'attributo sorgente corrisponde un solo valore nell'attributo destinazione (relazione 1-to-N). |
|                                                                                                                               |                                                |                                                                                                                                                           |

Si possono creare delle **gerarchie sulle dimensioni**, che contengono attributi che possiamo fare le analisi che si chiamano **attributi dimensionali**![[Screenshot 2026-09-28 at 18.32.09.png]]
Tendenzialmente è meglio avere un overview sul trend e poi approfondire sul trend specifico, ma utilizzare uno strumento di supporto che mi permetta di navigare sui dati in diversi ambiti. Tale gerarchia possono contenere $N$ attributi. La notazione che viene utilizzata dalla dimensione $X$, posso aggiungere un'arco con un pallino, se tra prodotto e marca esiste una **dipendenza funzionale** cioè una relazione 1 to N tra due elementi.

Sulla **gerarchia esistono solo dipendenze funzionali,** che vanno esplicitate solo rispetto all'attributo più generale che compare. 

>[!warning] N.B
>Se leggiamo le dipendenze funzionali da destra verso sinistra allora stiamo vedendo da un concetto più generale ad uno più dettagliato

>[!warning] Cosa mettere nelle misure?
>Bisogna mettere valori che siano atomici e additivi, **le medie e i prezzi unitari non sono misure atomiche affidabili** (sono non-additive o derivate)


>[!example] Esempio
>Mese Settembre 2026, cioè analisi di un mese di un determinato anno, non di tutti gli anni. Cioè si possono analizzare. Data collegato a mese e mese è collegato a trimestre.
>

Nella gerarchia riportiamo gli attributi dimensionali, che sono quelli che vogliamo fare le analisi, i legami della gerarchia son dipendenze funzionali che sono relazioni (1-to-N nell'esempio di un modello ER)

Questa è la rappresentazione dal **Dimensional Fact Model**  al modello **ER**
![[Screenshot 2026-09-28 at 18.42.57.png]]

## Conversione dal modello ER al modello DFM
1. **Identificazione del Fatto:** Si sceglie la **Relazione N-a-M** o l'**Entità Transazionale** al centro del modello E/R (es. l'entità _Vendita_ o la relazione _Acquisto_ tra _Cliente_ e _Prodotto_).

2. **Estrazione delle Misure:** Gli attributi quantitativi/numerici contenuti nell'entità o relazione transazionale dell'E/R diventano le **misure** del fatto nel DFM.
    
3. **Mappatura delle Dimensioni:** Tutte le entità direttamente collegate all'entità transazionale tramite relazioni $1:N$ diventano le **dimensioni primarie** del fatto (es. _Data_, _Prodotto_, _Negozio_).
   >[!warning] Come strutturare la gerarchia delle dimensioni?
   >Si parte sempre dal **nodo foglia** (livello di dettaglio massimo, direttamente collegato al fatto) e si sale verso gli **attributi più generali** (es. `Partita_IVA` $\rightarrow$ `Provincia` $\rightarrow$ `Regione` $\rightarrow$ `Area_Geografica`).
    
4. **Costruzione delle Gerarchie:** Risalendo le relazioni $1:N$ a partire da ogni dimensione primaria verso le entità più generali (es. da _Prodotto_ verso _Marca_ e _Categoria_), si definiscono gli **attributi dimensionali** collegati da **dipendenze funzionali**.
>[!example]
>Nell'immagine sopra abbiamo l'elemento che descrive le relazioni molti a molti tra: Negozio, Prodotto e Data. Tale relazione che è denominata **Vendita**, diventerà il nostro **Fatto**. 
>![[Pasted image 20261006111608.png]]
>Dopo aver individuato il fatto si vanno a scrivere le **Misure** del fatto, che nel modello ER sono gli attributi della transizione (qt venduta, prezzo unitario, incasso), come nell'immagine sotto
>![[Pasted image 20261006111852.png]]
>Poi tutte le entità che sono attorno alla transizione, diventeranno delle **Dimensioni**, che sull'immagine saranno dei rettangoli ma nella realtà sono dei pallini con il nome dell'entità sopra:
>![[Pasted image 20261006112144.png]]
>Poi infine si vanno a modellare le **dipendenze funzionali** che sono le relazioni 1-ad-N che sono presenti tra gli attributi di dimensione e altre relazioni che presentano:
>![[Pasted image 20261006112617.png]]
## Costruttori Avanzati
Ci sono dei costrutti avanzati all'interno del **Dimensional Fact Model**:

**Non Additivi**: rappresentata da un arco tratteggiato identifica una metrica e una
dimensione non aggregabili.
>[!example]
>Come nell'immagine sotto, non è possibile stabilire il numero di clienti relativi a più prodotti perché in uno stesso scontrino ci possono essere prodotti diversi. Se prod_1 ha 100 clienti (100 vendite) e prod_2 ne ha 200, la somma totale dei clienti dovrebbe essere 300 ma in realtà ci saranno delle sovrapposizioni dovute al fatto che su uno scontrino ci possono essere sia prod_1 che prod_2.

**Arco Opzionali**:  rappresenta un attributo non disponibile per tutti i record, sostituisce l’indicazione della cardinalità nel modello ER.
 
**Attributi descrittivi**: una caratteristica di interesse nella quale non viene fatta un'analisi, cioè non faremmo un'analisi per singoli indirizzi o telefono. Rappresentano del contenuto informativo dell’attributo a cui essi sono collegati.
![[Screenshot 2026-09-29 at 17.51.17.png]]

**Convergenza**: ci possono essere dipendenze funzionali nella quale **convergono** ad un'unico attributo, perché hanno dipendenze comuni.![[Screenshot 2026-09-29 at 17.49.08.png]]
come nell'immagine sopra.

**Dimensione opzionale**, che sono rappresentati da un trattino prima della dimensione  rappresenta un attributo non disponibile per tutti i record, sostituisce l’indicazione della cardinalità nel modello ER.![[Screenshot 2026-09-29 at 17.50.32.png]]

**Gerarchia Condivisa**:  usare una gerarchia per due dimensioni di analisi![[Screenshot 2026-09-29 at 18.08.43.png]]

**Archi Multipli**: un arco multiplo è la rappresentazione di una **relazione molti a molti tra due attributi dimensionali** oppure tra dimensione e attributo
```
[DIMENSIONE A] ===== [DIMENSIONE B] oppure [FATTO] ===== [DIMENSIONE]
```
- Un arco multiplo può essere tra **dimensione** e il fatto come nell'immagine a in basso a sinistra, la **misura costo viene associato ad N attributi di dimensione diagnosi diverse**, che può generare una difficoltà maggiora nel processare le query.
- Un'arco multiplo tra un'attributo dimensionale ad un'altro attributo dimensionale, che rappresenta un **gruppo** di configurazioni.
![[Screenshot 2026-09-29 at 18.20.11.png]]

>[!info]
>Per far sì che non ci siano archi multipli tra dimensione e fatto, si cerca di creare un'altra dimensione che fa da gruppo, come nell'immagine sopra.

>[!example] Esempio Arco multiplo tra attributi dimensionali con il Negozio libri
>Nell'immagine di sopra abbiamo il fatto **Vendita** relativa agli attributi di dimensione **Data** e **Libro**, relative ad un negozio di libri. Vediamo che nell'immagine c'è un arco multiplo tra `Libro` e  `Autore`, questo vuol dire che:
>- Un libro può avere più autori.
>- Un autore può aver scritto più libri.

È l'approccio **preferibile** dal punto di vista architetturale. La **molteplicità viene isolata all'interno della gerarchia della dimensione**, perché **riduce la complessità delle query** di aggregazione ed **evita la duplicazione delle righe nella tabella dei fatti**.

**Attributo configurazionale**:  rappresenta un attributo multivalore che è solitamente caratterizzato da pochi valori distinti (<=10), è **rappresentabile mediante enumerazione dei valori possibili**, rappresentati in tabella come colonne che possono assumere un valore booleano, una seconda alternativa è quella di considerare l’**attributo configurazione come un normale attributo** (che nello schema logico diventa un attributo della tabella padre della gerarchia) ,oppure una chiave esterna alla tabella che contiene tutte le configurazioni possibili (dipende dalla numerosità delle configurazioni).![[Screenshot 2026-09-29 at 18.32.56.png]]

## Aggregazione
Con il termine di aggregazione intendiamo il processo in cui si vanno a creare dei gruppi sintetici di dati, passando da un dominio enorme, si **vanno ad identificare solamente le informazioni di interesse che vogliamo analizzare**.

>[!info] Parole Semplici
Andiamo a prendere una grande quantità di dati e li andiamo a sintetizzare e raggruppare per poter svolgere analisi specifiche e trend di mercato.

### Tipologie di Misure
Ci sono diverse tipologie di misure di aggregazione che vanno in base a come le misure (i valori della tabella dei fatti), si possono sommare:

- **Misure Additive**: si possono sempre sommare.
  >[!example] Esempio
  >Quantità di prodotti venduti. Puoi sommarla per giorno, per negozio, per categoria di prodotto. Il totale torna sempre.

- **Misure NON-Additive**: **NON** si possono sommare sulla dimensione del tempo.
>[!example] Esempio
>Il saldo del tuo conto corrente a fine mese. Se a Gennaio hai 1.000€ e a Febbraio hai 1.200€, a fine Febbraio NON hai $1.000 + 1.200 = 2.200€$! Hai 1.200€. Per sintetizzarle nel tempo si usa la media (`AVG`) o l'ultimo valore valido, non la somma.

- **Misure Non Aggregabili**: Esprimono un valore relativo o una percentuale.
>[!example] Esempio
>Il prezzo unitario di una mela (1,50 €/kg) o la percentuale di sconto (20%). Non ha senso sommare i prezzi unitari delle mele vendute in un mese; il risultato non rappresenterebbe nulla.

### Tipi di Aggregatori
Ci sono tre tipi di aggregatori:
- **Distributivo** (`SUM`, `MIN`, `MAX`): semplici da svolgere
>[!example]
>Se conosci già i totali delle vendite totali dei prodotti delle regioni Milano, Brescia e Bergamo, ti basta sommarli tra loro per ottenere il totale della Lombardia. Non ti serve rileggere tutti i singoli scontrini originali.

- **Algebrico** (`AVG`): ti servono calcoli differenti
>[!example]
>Nelle vendite dei prodotti se sai che Milano vende dei prodotti a 50€ e Bergamo a 40€ non puoi fare la media sommando il prezzo del prodotti di Milano e quello di Bergamo. Questo perché devi sapere quanti prodotti ha venduto una città e un'altra. 
>
>Per ricalcolare la media aggregata ti servono due informazioni di supporto: la somma totale e il conteggio degli elementi (`COUNT`) `SUM(prezzo_prodotti) * COUNT(n_prodotti_venduti)`.

- **Olistico** (le singole componenti non possono essere prese singolarmente).
>[!example] 
>Se conosci la mediana dei voti della classe A e la mediana della classe B, non puoi calcolare la mediana dell'intera scuola usando solo quei due valori. Sei costretto a **riprendere da capo tutti i dati grezzi** di tutti gli studenti, metterli in ordine e ricalcolarla.
## Schema di fatto vuoto
Uno schema di fatto vuoto è uno **schema di fatto in cui il fatto rappresenta il verificarsi di un evento e non contiene misure al suo interno**, è utile per conteggiare gli eventi accaduti e per rappresentare gli eventi non accaduti (insieme di copertura che è l’insieme di tutti i possibili casi, nell’esempio della frequenza alle lezioni l’insieme di copertura è il calendario delle lezioni). La misura può essere solo una count![[Screenshot 2026-09-29 at 18.37.29.png]]

## Variazione dei dati nel tempo
**Cosa succedono agli attributi dimensioni nel tempo?**
La variazione delle dimensioni o dei dati relativi ad un record, nel tempo, può essere gestita in tre modalità diverse:

**Sovrascrittura nel Tempo** (Rappresentazione del tempo di tipo 1):  il nuovo dato sovrascrive il dato attuale, la **traccia del valore precedente viene perso**.

**Nuova Istanza Incorrelata** (Rappresentazione del tempo di tipo 2): quando si svolge un cambiamento su un dato, si viene a creare una copia (istanza) del nuovo dato con i valori che si sono cambiati (gli eventi sono partizionati in base alla variazioni degli attributi dimensionali).

**Nuova Istanza Collegata a Quella Vecchia** (Rappresentazione del tempo di tipo 3) come nel caso precedente, si a creare una copia del dato che si vuole modificare / eliminare, ma ci sarà: 
- Una **coppia di valori di timestamp** (inizio e fine) per la gestione della validità del dato
- Un **attributo** che consenta l’identificazione della sequenza di variazione di una specifica istanza.

## Carico di Lavoro
Durante la progettazione è fondamentale definire il carico di lavoro che il sistema deve poter gestire. Il possibile carico reale previsto viene calcolato mediante reportistica standard e stime discusse con gli utenti, queste stime devono prevedere anche il successo del sistema (che porta ad un’aumento del numero di utenti nel tempo) e la variazione della tipologia delle interrogazioni nel tempo. Dopo l’avviamento del sistema esso deve essere monitorato e migliorato (fase di tuning).

## Volume dei dati
Bisogna capire in questa fase quanto occupa in termine di spazio un determinato **Data Mart** (DTM) e con delle **strutture accessorie**. 
-  Numero di eventi per ogni fatto
-  Numero di valori distinti negli attributi delle gerarchie
-  Lunghezza degli attributi
- Intervallo di memorizzazzione dei dati
-  **Sparsità**: il numero degli eventi accaduti non corrisponde a tutte le possibili combinazioni delle dimensioni
# Reference
---

