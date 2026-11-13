---
created: 2026-10-17
tags:
  - baby
topics:
author: Danilo Quattrini
---
# Pipeline Exceptions
---
## Questions
- Che cosa sono le **eccezioni**?
- Che differenza c'è tra **interruzione** ed **eccezione**?
- Quali sono le cause di un **eccezione**?
## Classification
- Come si classificano le eccezioni?
## Handling
- Come vengono gestite le eccezioni dai vari processori ARM, x86, RISC-V
- Cosa sono la Gestione delle eccezioni precise?
- Quali sono le cause e come si possono risolvere se non si gestiscono le eccezioni in modo preciso? 

---
## Definizione
Le eccezioni sono situazioni nella quale il processore si deve fermare perché ci sono stati dei problemi o degli errori causati dal programma, che non hanno eseguito delle operazioni. Nella pipeline gestire le eccezioni è complesso perché le istruzioni vengono eseguite in parallelo, rendendo il processo di identificazione e gestione complesso.

Spesso si confondono i termini come **eccezione (exception)** ed **interruzione (interruption)**, dove il primo viene inteso come un blocco dello stato / esecuzioni delle  CPU nel performare ulteriori operazioni.

Le interruzioni invece sono causate da dispositivi I/O e non sono inerenti al processore, esempio quando si fa un reset.
## Cause delle Eccezioni
Le eccezioni possono avvenire quando si eseguono operazioni con valori in floating point e ci sono degli overflow, oppure possono avvenire per i seguenti casi:
- Malfunzionamento dei dispositivi Hardware.
- Overflow o Underflow di operazioni con numeri interi.
- Operazioni che non sono state definite.
- Spegnimento del computer.
Queste sono alcuni delle cause dovute alle eccezioni

## Classificazione di Eccezioni
Le eccezioni si possono classificare dal modo in cui vengono generate:
- **Sincrone**: se provengono da un programma che lancia (`throw`) un eccezione sempre nello stesso punto
- **Asincrone**: provengono da dispositivi esterni hardware

Dal modo in cui vengono viste o non si possono definire come:
- **Mascherabili**: cioè quelle eccezioni che possono essere sorpassate o ignorate dal processore.
- **NON-Mascherabili**: eccezioni nella quale non si possono evitare (come il reset o perdita di alimentazione)

Dal modo in cui si può ritornare allo stato precedente oppure no sono:
- **Ripristinabili** o **NON-Riprisitinabili**: cioè se il processore è in grado di ritornare allo stato precedente oppure no.
## Meccanismo di Gestione delle eccezzioni  su (ARM, x86, RISC-V)
Sono divisi in 4 fasi e sono le seguenti:
1. **Fase di Rilevamento**: il processore si accorge che c'è un interruzione all'interno della pipeline ed interrompe l'esecuzione.
2. **Fase di Salvataggio**: Il processore poi salva lo stato del Program Counter (PC) e dei relativi flag (CPSR / flag vari).
3. **Fase di Gestione**: nella fase di gestione si va a prendere il codice identificativo dell'errore o lo si individua in un vettore di errori (Interrupt Vector Table), poi si esegue una routine per la gestione dell'error.
4. **Fase di Ritorno**: dopo che la routine è stat gestita si ritornerà ad eseguire nuovamente il processo che si era stoppato precedentemente.
## Gestione delle eccezioni Precise (Precise Exceptions)
Un'eccezione viene definita precisa se e solamente se, quando viene gestita:
- Le istruzioni precedenti all'eccezione sono state completate prima che l'evento avvenisse.
- Le istruzioni successive all'eccezione non vanno a cambiare il valore dei registri o della memoria

Gestire però le eccezioni in un processore a multi-ciclo è molto complesso e laborioso, questo perché bisogna tener conto che ci sono operazioni che posso completare la loro esecuzione durante l'avvenimento di un'eccezione.

>[!example] Esempio
>Prendiamo queste istruzioni eseguite su dei single floating point numbers:
>```asm
>fdiv.df0,f2,f4
>fadd.df10,f10,f8
>fsub.df12,f12,f14
>```
>L'operazione di divisione impiega più cicli di clock per completare la propria esecuzione, mentre la sottrazione e l'addizione invece impiegano solo pochi cicli di clock e riescono a completare la loro esecuzione prima. Solo che però se ci sono degli errori durante la esecuzione della sottrazione allora l'**eccezione sarà imprecisa** (out-of-order completition)

Dall'esempio però come si può risolvere a questo problema?
1. Accettare eccezioni imprecise (sconsigliato, causa errori nei dati).
    
2. Rallentare l'esecuzione delle istruzioni veloci per forzare il completamento in ordine.
    
3. Utilizzare strutture hardware (come buffer temporanei o la fase di _Commit_) per salvare temporaneamente i risultati e scriverli nei registri definitivi solo in ordine (_In-order completion / Write-back_)
# Reference
---

