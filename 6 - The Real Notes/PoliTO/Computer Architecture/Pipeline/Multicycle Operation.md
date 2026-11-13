---
created: 2026-10-11
tags:
  - baby
topics:
  - Architecture 
  - Pipeline
  - "[[School]]"
author: Danilo Quattrini
---
# Multicycle Operation
---
## Questions
### Definitions
- Che cos'è una multicycle pipeline?
- Come viene divisa la fase di execute nella multicycle pipeline?
- Quali sono i parametri per la prestazione di una pipeline multicycle? Elencali e descrivili
### New Hazard
- Qual sono i nuovi hazard che vengono coinvolti in una struttura multi-cycle pipeline?
- Cos'è un hazard strutturale? Come può avvenire?
- Quali sono le categorie di hazard di dato?
- Descrivimi la differenza tra un hazard di dato e strutturale.
- Quali sono i tipi di hazard di dato?
---
Ci sono valori numerici che sono interi e a virgola fissa, dove le elaborazioni sono efficienti con formati di numeri più piccoli. I numeri reali hanno la necessità di essere convertiti in un formato che il calcolatore possa elaborare e una serie di iterazione, perché ci sono istruzioni complesse.
Per fare questo si può pensare ad un clock molto lento, ma non è efficiente quindi si pensa di aumentare il numero dei passaggi da svolgere per fare i calcoli di moltiplicazione, divisone e addizione, che semplificano i numeri ma aumentano la complessità.

Da una struttura pipelined per interi passiamo ad una struttura parallelizzata per i numeri a virgola mobile:
![[Screenshot 2026-10-11 at 18.32.13.png]]

Dove la fase di execute viene parallelizzata, ma il resto rimane uguale. Nella fase di ex ci sarà una fase di elaborazione intera, ma ci saranno fase di elaborazione di numeri reali (floating point). Il simulatore di permette di creare strutture di questo tipo, facendo solo operazioni con numeri interi o reali configurandole a loro volta.

La fase di _Execute_ ora si divide in più unità funzionali separate:

- **Unità intera:** Semplice e a singolo ciclo.
    
- **Sommatori/Sottrattori in virgola mobile**.
    
- **Moltiplicatori in virgola mobile**.
    
- **Divisori/Radici quadrate**

## Parametri di Prestazione Con Numeri Reali
Nelle configurazioni dobbiamo tener conto della la latenza e l’intervallo di inizializzazione, dove:
- **Latenza** è il numero dei colpi dei clock da un’istruzione che produce un risultato e l’istruzione successiva che utilizza tale risultato. Da un‘istruzione A che possiamo definire in qualsiasi modo, la latenza ci dice quante altre istruzioni di mezzo ci servono per far sì che l’istruzione B possa riceve il risultato di A? Questo è un numero che **va da 0 per operazioni con interi** (grazie al [[Pipeline#Forwarding|forwarding]]) e può essere un valore più grande se si parlano di operazioni con floating point.

- **Intervallo di Inizializzazione (Initiation Interval)** Il numero di colpi di clock che devono passare tra due operazioni dello stesso tipo (ADD, SUB, MUL, DIV) nella stessa unità (devono essere tutte e due interi o entrambi floating point).
> [!example] Esempio
> Quando ho due istruzioni dello stesso tipo, come la somma fra due registri che contengono due interi, la seconda può entrare nella stessa unità, un colpo di clock dopo e non deve attendere che si completi l'operazione precedente.
> 

- **Unità Pipelined (es. moltiplicatore):** Possono accettare una nuova istruzione a ogni ciclo di clock (intervallo = 1 non nei casi reali), cioè se ci sono due istruzioni di moltiplicazione una dietro all'altra,  indipendenti, che entrano nello stesso istante.
  
- **Unità Non-Pipelined (es. divisore):** Devono completare l'intera operazione prima di poter accettare una nuova istruzione (intervallo molto alto).
![[Screenshot 2026-10-12 at 13.18.38.png]]
## Nuova Complicazione (Nuovi Hazard)[^1]
L'introduzione di latenze differenti genera nuove criticità hardware che sono i seguenti:

 ### [[Pipeline#Rischi Di Tipi Strutturali|Hazard Strutturali]] più frequenti:
    
- Se un'unità **non è pipelined** (come detto prima la divisore), un'istruzione successiva dello stesso tipo non può accedere alla fase di calcolo e costringe il processore a stallare (_stall_) nella fase di _Decode_.
        
- Conflitti nella fase di _Memory_ (in parte non frequenti) o _Write Back_ (più frequenti) se più istruzioni completano la fase di _Execute_ contemporaneamente.

![[Screenshot 2026-10-12 at 13.30.05.png]]
L'istruzione di moltiplicazione fra due numeri floating point impiega più tempo per poter completare la propria esecuzione, come vediamo da `M1` fino ad `M7` e completerà la **write-back** nella posizione 11. Le seguenti istruzioni invece possono invece finire ad eseguire il **write-back** allo stesso tempo come l'operazione di moltiplicazione (segnato in rosso). 
        
Per risolvere le istruzioni che vanno a modificare un registro che verrà utilizzato nell'istruzione successiva, come l'esempio di `f2` che viene modificato in `fadd.d f2, f4, f6` e poi caricato dalla memoria in `fld f2, 0(x2)`, **devono stallare nella fase di decodifica** e far completare l'istruzione precedente, come  `fadd.d f2, f4, f6`, prima di andare a fare la load.
        
### Hazard sui Dati (Data Hazard):
Ci sono 3 nuovi tipi di Data Hazard:

- **RAW (Read After Write) Dipendenza Vera:** Un'istruzione cerca di leggere un registro prima che un'operazione precedente (ad alta latenza) vi abbia scritto il valore.
  
  Prendiamo un esempio di come si può presentare un hazard di tipo **Read After Write**
  >[!example] Esempio
  >Prendiamo due istruzioni $I_{1}$ e $I_{2}$ che sono le seguenti:
  >$$I_1: \text{fdiv.d } \mathbf{f0}, f2, f4 \quad (\text{Scrive } f0)$$
$$I_2: \text{fadd.d } f6, \mathbf{f0}, f8 \quad (\text{Legge } f0)$$

Vediamo che la prima istruzione deve scrivere il risultato della divisone in `f0`, mentre l'istruzione `fadd.d` ha bisogno del registro `f0` per poter svolgere l'addizione.

*Read After Write* = Legge Prima di Scrivere, cioè l'istruzione successiva legge prima che l'istruzione precedente abbia finito di scrivere il risultato

>[!warning]  N.B
>È una dipendenza "reale" (i dati fluiscono da $I_1$ a $I_2$). Si risolve inserendo stalli (bubbles) o tramite forwarding hardware.

> [!info] **Strategia di Re-scheduling**
>Cerca se ci sono altre operazioni indipendenti (come gli incrementi dei registri intero/puntatore o il caricamento dell'elemento successivo se applichi il unrolling) che possono essere collocate **tra** la `fmul.s` e la `fadd.s` per coprire la latenza della moltiplicazione.

-  **WAR (Write After Read) – Anti-dipendenza (_False Hazard_)**:  prendiamo un esempio per capirlo meglio abbiamo due istruzioni $I_{1}$ e $I_{2}$, che sono le seguenti:
  >[!example] Esempio
  >$$I_1: \text{fsub.d } f12, \mathbf{f8}, f14 \quad (\text{Legge } f8)$$
$$I_2: \text{fadd.d } \mathbf{f8}, f9, f14 \quad (\text{Scrive } f8)$$

  Abbiamo la prima istruzione $I_{1}$ che deve leggere il valore del registro `f8`, ma se tale istruzione in una pipeline  **out-of-order** viene letta **dopo che l'istruzione di addizione `fadd.d` scrive su `f8`**   allora il risultato sarà sbagliato.
  
  >[!quote]
  >*Write After Read* = Scrive Prima di Leggere

- **WAW (Write After Write) Dipendenza di Output (_False Hazard_):** Se un'istruzione a bassa latenza termina prima di un'istruzione a più alta latenza iniziata precedentemente, rischia di sovrascrivere il registro di destinazione prima del tempo, lasciando poi il registro con un valore errato.
>[!example] Esempio
>Prendiamo sempre due istruzioni $I_{1}$ ed $I_{2}$
>$$I_1: \text{fdiv.d } \mathbf{f0}, f2, f4 \quad (\text{Scrive } f0)$$
$$I_2: \text{fsub.d } \mathbf{f0}, f8, f14 \quad (\text{Scrive } f0)$$

Notiamo ora che l'accesso al registro `f0` viene fatto da tutte e due le istruzioni $I_{1}$ ed $I_{2}$, questo, questo **provoca un errore nell'output del risultato**. Perché se l'operazione di sottrazione $I_{2}$, che possiede una latenza bassa (esempio 2), completa la sua esecuzione prima di $I_{1}$ e salva il risultato nel registro `f0`,  allora l'istruzione di divisione $I_{1}$  ri-scriverà il risultato della sua operazione sempre sul registro `f0`, portando quindi a risultati sballati.

### Hazard Reali vs Falsi Hazard
Qui si intendono gli hazard che sono **provocati da vere dipendenze di dato**, cioè l'hazard RAW è l'unico e vero hazard, questo perché esiste un passaggio fisico di informazioni. Non è possibile evitarlo se non aspettando che il dato venga calcolato.

Mentre gli altri due hazard:
**WAR e WAW sono Falsi Hazard (Hazard di Nome):** Non c'è scambio di dati tra le istruzioni. Il conflitto si genera unicamente perché l'assembler o il compilatore ha riutilizzato lo stesso registro di supporto ($f0$ o $f8$) per due calcoli indipendenti.

>[!example] **Integrazione nei Processori Reali (Caso MIPS R4000):**
>Esempio di architettura a 8 stadi di pipeline (superpipelined).
>Aumenta i cammini di _forwarding_, allunga il _load delay slot_ (2 cicli anziché 1) e il _branch delay slot_ (3 cicli anziché 2).

## Esempio di Stalli in una Pipeline

>[!example]
>![[Screenshot 2026-10-12 at 13.42.26.png]]
>Dall'immagine vediamo che viene eseguita la prima istruzione in tranquillità, ma nella pipeline alla seconda istruzione `fmul.d f0, f4, f6`, nella fase di decodifica si rende conto che il registro `f4` deve ancora essere elaborato dall istruzione precedente. Quindi **hazard di dato**, deve stallare fino a che non arriva alla **write-back**. Siccome la moltiplicazione ha una latenza di 6 ed un'inizializzazione di 1 allora dobbiamo aspettare ben 7 colpi di clock dopo la decodifica prima di leggere dalla memoria e scrivere il risultato. Questo comporterà all'istruzione successiva della pipeline `fadd.d f2, f0, f8` a dover stallare fino a che non viene eseguita la memory e write-back dall'istruzione precedente.
>I primi due sono **HAZARD DI DATO**, mentre l'ultimo è **HAZARD STRUTTURALE**, perché non posso entrare in memoria prima che l'istruzione precedente abbia completato la writeback (causate principalmente dalle store `fsd`)

# Reference
---

[^1]: **Data Dependences and Hazard**: page 151 for more details of the book *Hennessy & Patterson*
