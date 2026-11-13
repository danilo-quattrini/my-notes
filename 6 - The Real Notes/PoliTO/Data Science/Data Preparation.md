---
created: 2026-10-20
tags:
  - baby
topics:
author: Danilo Quattrini
---
# Data Preparation
---
## Questions
- Quali sono le tecniche di pre-processing?
- Spiega il funzionamento dell'aggregazione
- Spiega che cos'è il sampling.
- Quali sono le varie tipologie di sampling sui dataset.
- Che cos'è la **riduzione dei dati**?

---
## Tecniche Di Pre-Processing
- **Aggregazione**: da un dato più generale ad uno più dettagliato
  
- **Sampling**: si prendono alcuni campioni del dataset per darle una rappresentazione
  
- **Riduzione Dimensionale**: diminuire il numero di features, andando ad applicare le tecniche di trasformazione, questo è necessario quando il dataset è pieno di features.
  
- **Selezione di Features**: riduzione dimensionale, andando a selezionare un sotto-insieme di attributi, quelli più significativi.
  
- **Creazione di Features**: quando ci sono features legata ad espressioni numeriche.
  
- **Discretizzazione e Binarizzazione**: da una variable continua ad una discreta.
  
- **Transformazioni degli Attributi**: quando si vanno a cambiare la natura degli attributi.
### Aggregazione
Quando **si combinano uno o più attributi in un singolo attributo**, questo processo di aggregazione andrà a ridurre la il numero di attributi o oggetti,  può generare un cambiamento di scala oppure il dato che si ottiene è più stabile (cioè che i dati tendono meno a cambiare in futuro).

>[!example]
>Trend ricavi giornalieri è un valore meno stabile perché dipende da molte variabili esterne, mentre se si aggrega per i ricavi mensili è più stabile.

Il processo può generare una riduzione, cioè ci sono meno righe da analizzare.![[Screenshot 2026-10-20 at 17.52.41.png]]

L'obbiettivo è quello di **trovare pattern ricorrenti**

### Sampling
Il *Sampling* avviene quando vogliamo una riduzione del data-set per analizzare uno specifico campo / sezione del dataset. 

>[!example] Analogia
>*Samplig* = esempii o di dati presi a campione in un dataset che però fanno parte della stessa categoria.


![[Screenshot 2026-10-20 at 17.58.31.png]]

#### Tipi di Sampling
Vogliamo un **Sampling** rappresentativo del fenomeno che vogliamo modellare, se non ho un data-set che rappresenta un fenomeno allora non ha senso lavorare su quei dati, voglio delle distribuzioni affini.

Il sampling si può estrarre in modo "randomico", che però non può ricomparire nel sampling nuovamente oppure c'è quello con rimpiazzi, che ogni elemento che viene selezionato in modo casuale ne viene rimosso in uno già presente.

Il sampling usato spesso è quello **statificato**, dove si divide i dati in diverse parti / partizioni e si seleziona delle percentuali di dati da ogni partizione, decidere su quale variabile è efficace fare una decisione.

### Dimensionalità del Dato
Un dato che ha un numero di feature elevate, più variabili definisco, più il gruppo passa da essere omogeneo a disomogeneo. Più variabili si utilizzano più si aumenta l'entropia (la varietà dei dati).![[Screenshot 2026-10-20 at 18.18.08.png]]

In ascissa le numero delle dimensioni, nelle ordinate c'è una metrica che sintetizza la distribuzione, valori più piccoli più il dato è sparso mentre se i valori sono grandi i dati sono meno sparsi.

### Riduzione Dimensionale
Si riduce la sparsità dei dati in un data-set,  che ci aiuta a generare un modello predittivo più robusto andando a ridurre la memoria e il tempo richiesto dagli algoritmi di dataminig per  ritornare un risultato. Ci permette inoltre di visualizzare il dato in maniera più semplice, togliendo valori irrilevanti e rimuovendone il rumore.

- **PCA** Principal Component Analysis 
- Singular Value decomposition
- Altri: tecniche. supervised e non-lineari

#### PCA
![[Screenshot 2026-10-20 at 18.28.46.png]]

### Selezioni di un Subset Feature
Scelgo le feature rilevanti, (lo stesso come la riduzione dimensionale non fa differenza) però ci sono diversi metodi che sono:
- **Brute-force**: provare qualsiasi input di dati da dare all'algoritmo di data-science
  
- **Embedded Approach**: In questo approccio si va a eseguire una selezione nel processo della data-mining, questo però è fattibile se si ha una dimensione dei dati molto bassa, se no consumiamo troppo tempo.
  
- **Filter Approach**: Viene fatto un filtraggio prima che i dati vengano dati in pasto all'algoritmo di data-mining
  
- **Wrapper Approach**: l’algoritmo di data science viene utilizzato come black-box per trovare il subset migliore. Il modello identifica combinazioni diverse di attributi dando diversi output. Mediante il confronto degli output, seleziono quello che genera un risultato più accurato.
#### Creazioni Di Feature
La creazione di una attribute può catturare delle informazioni importanti in modo efficace, che sono molto più efficienti degli attributi originali.

### Discretizzazione
E' il **processo di convertire un attributo continuo in un attributo ordinario**, ci aiuta a convertire un numero apparentemente infinito di valori in un numero ben definito. Questo metodo è utilizzato maggiormente negli algoritmi di [[Classificazione|classificazione]] ci sono due tipi di discretizzazione:

**Supervised:** dove si utilizzano delle etichette per identificare delle classi di dati.

**Unsupervised**: ==(da vedere meglio come funzionano)==
### Binarizzazione
**Metodo che mappa un attributo in uno o più valori binari.** Questo è possibile farlo da un attributo continuo, se quest'ultimo prima viene mappato in un attributo categorico.

>[!example] Esempio
> (altezza-> {basso, medio, alto})

Dagli attributi categorici poi si passa a mapparli in valori binari:
>[!example]
> {basso, medio, alto} -> {100, 010, 001}

 questo tipo di codifica in cui solo un bit per volta ha valore 1 è chiamato one-hot encoding
### Trasformazione di un attributo
Consiste nell'usare una funzione che mappa un intero set di un valori di attributo in un nuovo valore. 

Questi possono essere uno dei seguenti:

- **Normalizzazione**: tecnica che consiste nell'aggiustare / correggere i valori che sono al di fuori di un determinato range, media od occorrenza. Consiste nella maggior parte dei casi nel trasformare gli attributi in un range tra -1 a 1.
		- **Normalizzazione Min Max**, scalare i valori di un dataset tra 0 a 1:
			$$v' = \frac{v-min_{A}}{max_{A} - min_{A}} * (new\_max_{a} - new\_min_{A}) + new\_min_{A}$$
			normalizza $v'$ nell'intervallo $[\ new\_min_{A}, new\_max_{A} \]$
			
>[!example] Esempio
>$$X = [20, \; 30, \; 40, \; 50, \; 60]$$
>Prendiamo questo data-set dell'eta di 5 individuii, noi vogliamo normalizzare, prendiamo il valore più piccolo $20$ e il valore più grande $60$, ed applichiamo la formula per ogni elemento del vettore, cioè esempio per il primo elemento la scala sarà:
>$$v'=\frac{20-20}{60-20} = \frac{0}{40} = 0$$
>Così via per tutti gli altri, fino ad arrivare a 
>$$X_{\text{Min-Max}} = [0.00, \; 0.25, \; 0.50, \; 0.75, \; 1.00]$$


- **Standardizzazione**: lo spiego [[Standard Deviation|qui]] come funziona