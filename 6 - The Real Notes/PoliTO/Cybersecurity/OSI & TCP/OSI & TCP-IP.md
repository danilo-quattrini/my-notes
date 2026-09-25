---
created: 2026-02-14T15:43:00
tags:
  - baby
topics:
  - Cybersecurity
  - "[[School]]"
author: Danilo Quattrini
---
# OSI & TCP-IP
---
>[!quote]
>Il modello OSI e il modello TCP/IP descrivono entrambi **come le informazioni sono trasmesse tra i dispositivi nella rete**. Sono divisi in livelli, dove ogni livello si occupa di uno specifico compito e se ha bisogno può comunicare con il livello sottostante.

![[Pasted image 20260916131113.png]]
La differenza tra i due modelli è che il primo modello quello OSI è strutturato in 7 livelli, più teorico e dettagliato, mentre il modello TCP/IP è composto da ben 4 livelli e descrivono le reti moderne.

Sopra vediamo un esempio di come sono i vari modelli con i propri protocolli.
## Modello OSI
Il modello OSI che sta per ***Open System Interconnection*** è uno standard architetturale utilizzato per computer che comunicano tra loro cioè [^1]interoperabili. Come abbiamo visto in precedenza tale struttura è composta da 7 livelli dal livello 

Il 1° livello è quello più vicino al mezzo fisico, fino al 7° livello più vicino all’utente e alle applicazioni.

| Livello | Nome              | Funzione principale                                    |
| ------- | ----------------- | ------------------------------------------------------ |
| 7       | Applicazione      | Servizi di rete usati dalle applicazioni               |
| 6       | Presentazione     | Formato, codifica, compressione e cifratura dei dati   |
| 5       | Sessione          | Apertura, gestione e chiusura delle sessioni           |
| 4       | Trasporto         | Comunicazione end-to-end, segmentazione e affidabilità |
| 3       | Rete              | Indirizzamento logico e instradamento                  |
| 2       | Collegamento dati | Comunicazione sul collegamento locale e indirizzi MAC  |
| 1       | Fisico            | Trasmissione dei bit attraverso il mezzo fisico        |

![[Pasted image 20260916131819.png|417]]
**Fisico → Collegamento dati → Rete → Trasporto → Sessione → Presentazione → Applicazione**

Vediamo i vari livelli nel dettaglio
- [[Physical Layer|Fisico]] (Physical Layer)
- [[Data Layer|Collegamento Dati]] (Data Layer)
- [[Network Layer|Rete]] (Network Layer)
- [[Transport Layer|Transporto]] (Transport Layer)

# Reference
---

[^1]: L'interoperabilità è, in ambito informatico, la capacità di un sistema o di un prodotto informatico di cooperare e di scambiare informazioni o servizi con altri sistemi o prodotti in maniera più o meno completa e priva di errori, con affidabilità e con ottimizzazione delle risorse.
