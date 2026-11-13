---
created: 2026-11-03
tags:
  - baby
topics:
author: Danilo Quattrini
---
# ARM Cortex M3
---
![[IMG-ARM Cortex M3-20261103.png]]

ISA che possono essere di due categorie:
- 32 bit
- 16 bit con istruzioni compresse

Però non scegliamo quale tipo di istruzioni andiamo ad utilizzare, questo perché sarà il compilatore a fare tale lavoro. Come sappiamo ARM non vende dispositivi fisici, ma vende un micro-controllore, ma ci venderà tutto il sistema che ci permette di collegare con il mondo esterno oltre alla CPU.
![[IMG-ARM Cortex M3-20261103-1.png]]
## Cortex-M3 Datapath
![[IMG-ARM Cortex M3-20261103-2.png]]

## Cortex-M3 Pipeline
![[IMG-ARM Cortex M3-20261103-3.png]]

## Branch Pipeline
![[IMG-ARM Cortex M3-20261103-4.png]]

>[!warning] N.B
>I salti sono un problema in quanto richiedono **3 cicli  di clock per essere completati**.
>Nel caso peggiore, il salto indiretto viene preso e avviene sempre che la pipeline viene svuotate e riempita. Inoltre, non è supportato il delayed branch mechanism.

## Load Register LDR Pipeline
![[IMG-ARM Cortex M3-20261103-5.png]]


## Programmer View 
Ci sono i seguenti componenti importanti da dover far caso come programmatore:
- 16 + 2 registri che sono a 32 bit
- Gestione del consumo di potenza in modo efficiente
- Gestione delle interruzioni in modo efficiente
- Debug del nostro sistema, aggiungendo dei break-points dove possiamo vedere com'è lo stato di un registro all'interno del processore.
- Realizzato per essere completamente programmabile in C e in ASM

## Set dei Registri Cortex-MX3
![[IMG-ARM Cortex M3-20261103-6.png]]

>[!warning]
>Lo Stack Pointer avrà due repliche uno per il *processo normale* (SP_proc) e uno per le *operazioni importanti* (SP_main), quelle che vediamo nell'immagine.

## PSR - Program Status Register
Ci sono dei flag che sono utilizzati per identificare il risultato di un operazione, che sono spiegati anche [[CPU Components#Status Flag|qui]] in parte.

IL registro è diviso in 3 parti:
- Se voglio guardare i flag guardo l'Application Program Status Register (APSR)
- **E**xecution **P**rogram **S**tatus **R**egister (EPSR)
- Se invece voglio vedere dove il programma si è interrotto allora guardo la parte del registro chiamato **I**nstruction **P**rogram **S**tatus **R**egister (IPST)
  
![[IMG-ARM Cortex M3-20261103-7.png]]

## Processor Operating modes and levels
Ci sono due modi che operano il processore, che sono il:
- Thread mode:
- Handle Mode

Poi ci sono due livelli di accessi, che sono il:
- **user level**:  accesso limitato a tutte le risorse.
- **privileged level**: accede a tutte le risorse

## AMBA BUS System
![[IMG-ARM Cortex M3-20261103-8.png]]

Ci sono 3 tipologie di AMBA bus:
- The Advanced high-Performance Bus (AHB)
- The Advanced System Bus (ASB)
- Advanced Peripheral Bus (APB)

## Clock Distribution

## Gestione della Potenza Energetica
Diversi sistemi di riposo (idle) che sono supportati:
- **Sleep Now**: aspetta per un evento di interruzione 

- **Sleep On Exit**: interrompe la propria esecuzione subito dopo il ritorno dell'ultimo Instruction Register (ISR)

- **Deep Sleep**

Ci sono anche due modi per "risvegliare" il processore, tramite dei *Wake Up Interrupt Controller* (WIC):
- External wake-up detector

## Mappa della memoria
![[IMG-ARM Cortex M3-20261103-9.png]]

## Gestione delle Eccezioni
## Gestione delle Interruzioni
![[IMG-ARM Cortex M3-20261103-10.png]]
E’ supportata una interruzione non mascherabile INTNMI. Insieme al processore è presente un **N**ested **V**ectored **I**nterrupt **C**ontroller (NVIC) che supporta fino a 240 interrruzioni esterne.
![[IMG-ARM Cortex M3-20261103-11.png]]