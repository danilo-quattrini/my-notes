---
created: 2026-02-14T15:43:00
tags:
  - baby
topics:
author: Danilo Quattrini
---
# Hardware Speculation
---
## Introduzione
Si può scommettere che l'operazione vada in modo che in un altra, mettendo insieme i concetti come:
- **Dynamic Branch Prediction**
- **Dynamic Scheduling**
- **Speculation**
La speculazione vuol dire che accettiamo che i salti siano giusti, andando ad eseguire delle istruzioni fuori ordine.

Si utilizzano in tutti i processori moderni

## Architettura 
L'architettura parte dall'algoritmo di Tomasulo, però c'è un problema con i salti,  che però vengono gestite dividendo la fase di execute in due fasi:
1. La computazione dei risultati che vengono passati ad 
2. La scrittura del dato nel banco dei registri o in memoria viene fatto in ordine e in uno stage diverso della pipeline, chiamata *instruction commit*

### ReOrder Buffer (ROB)
La struttura dati che contiene le istruzioni in ordine

#### ROB and register file
I dati temporanei andranno sul CDM, che però faranno riferimento ad una linea del ROB che andrà ad allocare un istruzione precisa.

#### ROB fields
Ogni riga del ROB ha quattro informazioni:
1. **Il tipo di istruzione**: potrebbe essere la branch, store o il registro
2. **La destinazione**: registro intero o reale, oppure un indirizzo di memoria
3. **Il valore**: parliamo del valore dei registri
4. **L'indicazione dello status**: cioè controlla se l'istruzione ha completato l'istruzione oppure no.

Ogni elemento deve avere una quantità di bit consistente.

L'architettura è la seguente:
![[Screenshot 2026-10-23 at 10.53.18.png]]

Quello rosso sono le modifiche che sono state fatte all'architettura di Tomasulo, dove ora il CDB ora **non manda le informazioni nel FP**, com'era prima, ma vanno direttamente nel nuovo buffer chiamato **Reorder Buffer**.

### Instruction Execution Steps
La fase di decodifica viene quindi divisa ora in 4 parti:
- Issue
- Execute
- Write Result
- Commit
#### Issue
Oltre alle operazioni base della issue come viste [[Dynamic Scheduling#Issue|qui]].

Devo controllare se c'è una linea nella **Reorder Buffer**, gli operandi disponibili ora possono essere anche presenti nel **Reorder Buffer**, dove il dato non è nel register bank, ma **si può trovare anche nel Reorder Buffer**

#### Execute
L'unita funzionale fa partire le operazioni e scrive il risultato nel CDB, scrivendo anche in quale linea del **Reorder Buffer** dovrà pizzare il risultato dell'esecuzione
#### Write Result
#### Commit (or Completion) Step
Quando l'istruzione finisce e succede che i dati nel reorder buffer aggiornano i registri o i l'istruzioni in memoria. L'elemento che era occupato dal re-order buffer viene liberato e si passa all'istruzione successiva della coda.

In realtà le reservation station vengono liberate prima.

### WAW & WAR hazar
Non si fermano, ma vengono mascherate perché vengono rinominate con le linee del reorder buffer

### RAW hazard
Si vanno a ridurre anche i rischi della memoria.

### Example
>[!esempio] Esempio
>```
>fld f6, 32(x2)
>fld f2,44(x3)
>fmul.d f0, f2, f4
>fsub.d f8, f2, f6
>fdiv.d f0, f0, f6
>fadd.d f6, f8, f2
>```
>Assumiamo la latenza delle operazioni
>- add: 2 clock cycles
>- multiply: 10 clock cycles
>- divide: 40 clock cycles
>  Solo il `fld` è stato già commitato, mentre le `fsub.d` e la `fadd.d`, sono state completate ma non ancora commitate perché stanno aspettando il completamento di `fmul.d` e infine la **fdiv.d** è stata eseguita

