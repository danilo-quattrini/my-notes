---
created: 2026-10-03
tags:
  - baby
topics:
author: Danilo Quattrini
---
# ICMP
---
## Questions
- Che cos'è un ICMP?
- Che funzionalità ha il protocollo ICMP?
- In quali livello TCP/IP si trova l'ICMP?
- Che struttura ha il protocollo ICMP?
- Quante categorie di ICMP ci sono?
- Quali sono i messaggi tipici di un protocollo ICMP?
- **Segnalazione degli errori:** Perché il protocollo IP necessita di ICMP se IP stesso è un protocollo _Best-Effort_?
- **Reindirizzamento (Redirect):** Quali condizioni di rete devono verificarsi affinché un router $R1$ decida di inviare un messaggio di _ICMP Redirect_ a un mittente?
- **Diagnostic & Controllo:**
    - Quale messaggio ICMP viene generato quando un router riceve un pacchetto IP con $TTL = 1$ che deve essere ulteriormente inoltrato?
        
    - Qual è il comportamento del router se un pacchetto supera la MTU del link di uscita, ha il bit **DF (Don't Fragment)** impostato a 1 e non può essere inoltrato? Quale messaggio ICMP invia?
---
## Definizione
>[!info] Definizione
>ICMP (Internet Control Message Protocol) è un protocollo di Livello 3 Network Layer utilizzato per servizi di **diagnosi e segnalazione**.

Tale protocollo viene incapsulato all'interno dell'header del protocollo [[IP]],  che nell'header del protocollo IP viene impostato ad 1.
![[Pasted image 20261003183550.png|1200]]
## La sua anatomia di base
Un messaggio ICMP ha sempre una struttura minimale:

- **Type (8 bit):** La macro-categoria del messaggio (es. Type 8/0 per Echo, Type 3 per Destination Unreachable, Type 11 per Time Exceeded).
    
- **Code (8 bit):** Il dettaglio o motivo specifico (es. per Type 3: Code 0 = Network Unreachable, Code 1 = Host Unreachable, Code 3 = Port Unreachable, Code 4 = Fragmentation Needed).
    
- **Checksum:** Per verificare l'integrità del messaggio.
    
- **Payload:** Spesso racchiude l'header IP originale + i primi 8 byte del payload del pacchetto che ha generato l'errore (così il mittente sa esattamente _quale_ sua socket/connessione ha causato il problema).
**Tale protocollo è di dimensione di 4 byte**

## Categorie di messaggi ICMP
Ci sono due categorie di messaggi ICMP
1. **Messaggi di Errore (Error Reporting):** Notificano al mittente originale che un suo pacchetto è stato scartato o ha incontrato un problema.
2. **Messaggi di Informativi / Query (Diagnostic):** Usati per fare richieste e risposte di controllo.

## Messaggi ICMP Principali

| Messaggio ICMP                              | Perché viene generato / A cosa serve                                                                                                                                              | Esempio Pratico                                                                                                                                                         |
| ------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Echo Request / Echo Reply                   | **Reply** Testare la raggiungibilità IP e misurare il tempo di andata e ritorno (RTT).                                                                                            | È la base del comando **`ping`**.                                                                                                                                       |
| **Time Exceeded**                           | Un router riceve un pacchetto con **TTL = 1**, lo decrementa a **0** e deve scartarlo per evitare loop infiniti.                                                                  | È il meccanismo sfruttato da **`traceroute`** (inviando pacchetti con TTL progressivo 1, 2, 3...)                                                                       |
| **Destination Unreachable**                 | Un dispositivo o router scarta un pacchetto perché non riesce a consegnarlo (es. porta chiusa, rete non in tabella di routing, o serve frammentazione ma il bit DF è a 1)         | Se imposti il bit **DF (Don't Fragment)** e invii un pacchetto più grande della MTU del link, il router invia un _ICMP Destination Unreachable (Fragmentation Needed)_. |
| [[Protocolli IPv6#ICMP Redirect\|Redirect]] | Un router $R1$ avvisa un host mittente $S0$ che per raggiungere quella destinazione esiste un altro router $R2$ sulla **stessa sottorete locale** che offre un percorso migliore. | Permette all'host di aggiornare la propria tabella di routing per i pacchetti successivi.                                                                               |

# Reference
---

