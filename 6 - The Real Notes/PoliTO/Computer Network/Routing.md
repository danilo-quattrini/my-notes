---
created: 2026-10-05
tags:
  - baby
topics:
  - Cybersecurity
  - "[[School]]"
author: Danilo Quattrini
---
# Routing
---
# Questions
## Definizioni
- Che cos'è una routing table?
- Perché viene utilizzato l'indirizzo IP della rete invece di segnare i singoli host della rete?
- Quali sono le componenti di una tabella di routing?
## Connessioni tra host della stessa rete
- Come fa un host a capire che l'IP della destinazione fa parte della stessa sottorete?
- Cosa succede se la sorgente non ha nella propria ARP Cache l'indirizzo IP associato al MAC del destinatario?
- Serve coinvolgere il router se ci troviamo nella stessa rete?

## Connessione tra host di reti differenti
- Cosa succede se l'`AND` BIT A BIT tra IP destinazione e subnetmask sorgente non riporta alla network id della sorgente?
- Cosa deve fare l'host affinché possa inviare un pacchetto ad una rete differente?
- Cosa succede se il TTL dell'header del datagramma IP è a 0 quando il router riceve tale pacchetto dall'host, che messaggio di errore viene inviato? Che protocollo viene utilizzato per inviare tale messaggio di error.
- Che cosa deve controllare il router affinché

---
## Che cos'è una Routing Table
>[!quote] Definizione 
>La **Routing Table** è una struttura dati memorizzata all'interno della memoria RAM di ciascun router (e di ogni host IP) il cui **scopo primario è conservare la mappa di tutte le destinazioni di rete raggiungibili nella topologia** e indicare l'operazione di instradamento (**forwarding**) da effettuare per ciascuna di esse

In una rete basata sul protocollo IP, la Routing Table **non memorizza i singoli host finali**, ma memorizza **le reti IP (IP networks / sotto-reti)**. Questo approccio garantisce la scalabilità della rete Internet, evitando di dover memorizzare miliardi di indirizzi singoli.
## Componenti di una tabella di routing
![[Screenshot 2026-10-05 at 11.44.26.png]]
Per ogni rotta o destinazione, la tabella contiene tipicamente le seguenti informazioni fondamentali:

1. **Type (Tipo di rotta):** Indica la modalità con cui il router ha appreso la rotta:
    
    - **`C` (Directly Connected):** Rete direttamente collegata a un'interfaccia fisica o logica del router.
        
    - **`S` (Static):** Rota inserita manualmente da un amministratore di rete.
        
    - **`R` / `O` / `B` (Dynamic):** Rotte apprese tramite protocolli di routing dinamico (es. RIP, OSPF, BGP).
        
2. **Destination Network / Subnet Mask (Indirizzo di Rete/Prefisso):** L'intervallo di indirizzi IP appartenenti alla sottorete di destinazione (es. `130.192.1.0/24` o `10.0.0.0/22`).
    
3. **Next-Hop (Prossimo Salto):** L'indirizzo IP dell'interfaccia del router adiacente a cui inoltrare il pacchetto per farlo avvicinare alla destinazione finale. Per le reti direttamente connesse (`C`), il Next-Hop coincide solitamente con l'IP dell'interfaccia locale del router stesso.
    
4. **Cost / Metric (Costo o Metrica):** Un valore numerico che rappresenta la "distanza" o la bontà del percorso verso la destinazione (es. numero di hop, ritardo, larghezza di banda). La metrica viene usata durante la fase di routing per selezionare il percorso migliore.
## Come funziona la connessione tra Host della stessa rete ed Host di altre reti
Ci sono due scenari che andremmo ad analizzare, uno relativo agli host che fanno parte della stessa rete (subnet) **definiti intranet/Local** e quelli su reti diverse **inter-rete**.
### Comunicazione sulla stessa sottorete
Quando un host A deve comunicare con un host B che è presente nella stessa sotto-rete, deve eseguire questi passaggi:
1. Controllare che l'IP dell'host al quale deve inviare / comunicare, faccia parte della stessa rete, questo controllo lo svolge **l'host tramite un'operazione di `AND` bit a bit tra l'IP di destinazione e la sua subnetmask**. 
   Se il risultato dell'`AND` logico è uguale alla network ID dell'host di destinazione allora fanno parte della stessa sotto-rete
   >[!example] Esempio
   >Facciamo conto che abbiamo un IP sorgente `200.23.17.5` con subnetmask a `255.255.255.240.0` e vogliamo inviare un pacchetto all'ip `200.23.17.1`, 
   >$$\begin{align} 200.23.17.1  \\ 255.255.240.0 \\ \hline \\ 200.23.16.0 \end{align} $$
   >sotto forma di binary
$$\begin{align} 11001000.00010111.00010001.00000001 \\ 11111111.11111111.11110000.00000000 \\ \hline \\ 11001000.00010111.00010000.00000000 \end{align} $$
Vediamo che in questo caso l'IP fa parte della stessa sotto-rete perché ha lo stessa network ID dell'IP `200.23.17.5`
2. In questo scenario Non serve coinvolgere il router (Default Gateway), perché ci troviamo sulla stessa rete, quindi avremmo che:
	- Se Host A ha nella sua **ARP Cache**  l'IP di Host B al con il suo rispettivo indirizzo MAC, allora procede ad inviare il pacchetto nella rete.
	- Se il MAC non è nella cache, invia una richiesta **ARP Request in broadcast** sulla LAN. Host B risponde con un **ARP Reply in unicast** contenente il suo MAC, più in dettaglio [[ARP|qui]].
3. **Invio fisico:** Il pacchetto viene incapsulato in un frame ([[IP#Datagramma IP|datagramma]]) L2 (Ethernet) con MAC destinazione = MAC di Host B e trasmesso direttamente dallo switch locale

### Comunicazioni tra reti differenti
Nella comunicazione tra reti differenti, se nel passaggio `1` specificato prima, l'`AND` logico non porta come risultato la stessa network ID della rete sorgente allora significa che non fa parte della stessa rete, quindi L'host sorgente dovrà:
1. Invia un pacchetto al **Default Gateway** che sarà sempre collegato ad un router (non ne sono sicuro però mi sembra sia così), per poter comunicare con la rete esterna a lei.
2. Per poter inviare il datagramma al router L'host A deve inviare un ARP request in broadcast per ottenere L'indirizzo MAC del router.
3. **Elaborazione sul Router (L3 Routing):**
	- Il router riceve il frame L2, rimuove l'header Ethernet e analizza l'header IP del datagramma per leggere l'**IP di Destinazione**.
    
	- Il router decrementa il campo **TTL** di 1 (se arriva a 0, scarta il pacchetto e invia un `ICMP Time Exceeded`).
    
	- Consulta la sua **Routing Table** per individuare quale voce (rotta) corrisponde all'IP di destinazione.
    
	- Individuato il **Next-Hop**, incapsula il pacchetto IP in un nuovo frame L2 con il MAC del Next-Hop come destinazione fisica e lo invia sull'interfaccia di uscita opportuna.
    
	- Questo processo di salto in salto ("hop-by-hop") prosegue finché il pacchetto raggiunge il router direttamente connesso alla rete finale, che lo consegnerà all'host di destinazione tramite ARP.
## Algoritmo di Matching: Long Prefix Matching (LPM)
Dato un indirizzo IP di destinazione nel pacchetto che viene inviato da una rete ad un'altra, utilizzando un algoritmo chiamata *longest prefix matching*, che si attiva in caso di diversi IP che vengono matchati.

Per fare il match si fa l'operazione di `AND` tra bit a bit, tra l'IP di destinazione $200.23.17.1$ e la netmask dell'indirizzo IP sorgente, esempio con $255.255.240.0$
$$\begin{align} 200.23.17.1  \\ 255.255.240.0 \\ \hline \\ 200.23.16.0 \end{align} $$
sotto forma di binary
$$\begin{align} 11001000.00010111.00010001.00000001 \\ 11111111.11111111.11110000.00000000 \\ \hline \\ 11001000.00010111.00010000.00000000 \end{align} $$

## Tabella di Routing
Prendiamo l'esempio dell'immagine qui sotto e andiamo a creare la tabella di routing del **Router R1**
![[Screenshot 2026-09-23 at 17.19.56.png]]

| Type  | Destinazione      | Next-hop     | Cost |
| ----- | ----------------- | ------------ | ---- |
| **C** | 130.192.2.0 /24   | 130.192.2.1  | 0    |
| **C** | 130.192.3.0 /30   | 130.192.3.1  | 0    |
| **C** | 130.192.3.4 / 30  | 130.192.3.5  | 0    |
| **C** | 80.105..10.0 / 30 | 130.192.10.1 | 0    |
| **S** | 0.0.0.0 / 0       | 80.105.10.2  | 1    |
| **S** | 130.192.3.8/30    | 130.192.3.2  | 1    |
| **S** | 130.192.1.0/24    | 130.192.3.2  | 2    |
| **S** | 130.192.0.0/24    | 130.192.3.2  | 1    |
La **C** sta per connessione diretta e la **S** sta per statica, cioè c'è stato un'operatore che ha configurato la rete per conto sua. Lo 0.0.0.0 identifica la **default route** (rotta di default), che farà sempre match con qualsiasi rete, la userò per tutte le destinazioni che non faranno match sia prima che dopo, viene utilizzato per il contatto con l'internet, infatti il next-hop è il default gateway che sarebbe un **ISP** (Internet Service Provider).

La routing table sopra non è ottimizzata, ma la si può rendere più efficiente come per esempio raggruppare gli IP che hanno la stessa subnetmask (netmask).
>[!example]
>Si possono prendere gl'ultimi IP che hanno netmask a /24  e /30, li possiamo raggruppare alla netmask a /22, quindi avremmo l'ip di rete a 130.192.0.0/22 che possiamo rappresentare da 0.0 fino a 3.255 che sarebbe il broadcast
>$$\begin{align} (130.192.3.255)_{10} \\ \hline (10000010.110000000.000000 \| 11.111111111)_{2}\end{align} $$
>Questo ragionamento l'abbiamo fatto perché abbiamo bisogno di rappresentare 3 diverse sottoreti una con .1.0 una con .2.0  ed una con 3.0 prendendo 2 bit dalla rete a /24 e passiamo a /22 che da 254 bit si possono utilizzare ben 510 host

# Reference
---

