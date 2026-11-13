---
created: 2026-02-14T15:43:00
tags:
  - baby
topics:
  - Cybersecurity
  - OSI & TCP / IP
author: Danilo Quattrini
---
# Protocolli IPv6
---
## Che cosa va a cambiare nell'architettura?
![[Screenshot 2026-10-01 at 16.45.26.png]]
ARP non ci sarà più, perché faremmo tutto con ICMP, rimpiazzando ARP, IGMP neanche sarà più disponibile, che lo faremmo fare sempre con ICMP

Non basta solo questo, ma anche altri protocolli, ma si dovrà anche cambiare il DNS. Ma come fa a capire il DNS che utilizziamo IPv6 o IPv4? Semplicemente nella richiesta che fa il DNS invece di fare A, si farà AAAA.

Protocolli di routing cambieranno a loro volta, insieme con TCP e UDP
## Packet Header of IPv6
![[Screenshot 2026-10-01 at 16.54.03.png]]
Cambiano il **source address e destination address** che da **32 bit** passano a **128 bit**
![[Screenshot 2026-10-01 at 16.55.12.png]]
Ripasso del pacchetto IPv4.
- **Ver** (Versione): Cambiamento da Versione 4 a versione 6 con IPv6.
- **Lunghezza Pacchetto** (Payload Length / Total Length): lunghezza del pacchetto che inviamo
- **Type of Service** (ToS) or (Differentiated Service) (Traffic Class in IPv6): dove si indicava il tipo di traffico che utilizzavamo, per privilegiare un traffico che un'altro. 
- **Protocol** (in IPv6 Next Header): perché a livello IP ci dice cosa troviamo dopo, per esempio un protocollo TCP o UDP (guarda che finito header IP ci sarà UDP )
- **Time To Live** (In IPv6 **Hop Limit**): limite di tempo che un pacchetto può rimanere sulla rete, che viene decrementato di 1 in ogni router in cui passa.

I campi che sull'immagine è grigio-scuro **VENGONO ELIMINATI**, tranne per la frammentazione che si può aggiungere nella **Flow Label** e che viene frammentato direttamente dall'host e non più dal router che veniva fatta in IPv6.

L'host riceverà un messaggio ICMP dalla destinazione che dice che il pacchetto è troppo grande e che dovrà a lui stesso frammentarlo, in modo che l'host viene frammentato.
#### Parti Header rimossi dal IPv4 all' IPv6
**Checksum:** ridondante e non viene svolto
**Header**: ora possiede una dimensione fissa che è 40 byte

#### Parti dell'IPv6
Un flusso lo si identifica con **IP sorgente**, **IP destinazione**, **porta sorgente** e **porta destinazione e il protocollo** di livello 4 che identificano un flusso, questo ero lo standard per identificare un flusso nel protocollo IPv4. 

Per identificare un flusso ora non si usa più una quintupla, ma un numero che sceglie la sorgente con una certa logica, dove ci sarà un'etichetta differente per ogni operazione.
![[Pasted image 20261001171204.png]]
- **Flow Label**: Identifica il flusso a cui inviare l'informazione
- **Next Header**: si può mettere il protocollo 17: TCP  6: UDP, ma posso mettere anche il fragment header che è un campo aggiuntivo, oppure il campo per il routing, poi ci sono le **ESP** (Encapsulation Security Payload) e Authentication
![[Screenshot 2026-10-01 at 17.22.16.png]]

### Hop-by-Hop Extension Header
Viene usato per trasportare informazioni che devono essere esaminate da ogni router lungo la strada che percorre il pacchetto.
Ogni opzione è scritta nel formato **TLV** che sono Option Type, Option Length e Option Value fields. Con Option Type diciamo il tipo di opzione, la Length la lunghezza e il suo valore Value![[Screenshot 2026-10-01 at 17.25.14.png]]

## Incapsulamento
I pacchetti IPv6 sono incapsulati in 2 layer frame, sono tratti come nuovi protoccolli![[Screenshot 2026-10-01 at 17.49.12.png]]
Il fatto che sia dual stack vuol dire che possiamo mandare sia pacchetti IPv6 che IPv4, non succede mai dentro l'host ma avviene dentro la rete. Il vantaggio è che IPv4 continua ancora ad esistere all'interno della nostra macchina

## Address Mapping
Come facciamo a capire cosa scrivere nel livello MAC, se usassimo un IPv6 Unicast, si può usare un' approccio procedurale o Neighbor Discovery. Si prenderà gli ultimi 32 bit dell'IPv6 e si mette come prefisso 33-33 ![[Screenshot 2026-10-01 at 17.53.45.png]]

## Neighbor Discovery And Address Resolution
C'è una nuova funzione nuova chiamata ICMPv6, che è un sostituto di ARP, che tramite **Solicited-Node Multicast Address**, viene costruito in questo modo
### Solicited Node Multicast
![[Screenshot 2026-10-01 at 17.56.03.png]]
Prendiamo gli ultimi 24 bit dell'IPv6 ed aggiungiamo il prefisso `FF02` poi altri gruppi da `0000`
### Address Resolution
Si fa una sollecitazione con una chiamata ICMPv6, che sarà una chiamata multicast che richiede l'indirizzo MAC dell'host che vogliamo comunicare ![[Screenshot 2026-10-01 at 18.00.45.png]]
La risposta sarà un pacchetto ICMP Neighbor Advertisement  che rimanda indietro la risposta della richiesta, viene poi salvato il mappamento tra i PC che si sono comunicati tra di loro dentro la cache dell'host.

## ICMPv6
Lo utilizziamo apposto di ARP per Neighbor Discovery, lo utilizziamo per IGMP, per notificare gli errori. Il protocollo è fatto in questo modo, ed è inbustato in IPv6![[Screenshot 2026-10-01 at 18.09.05.png]]
Il body contiene "Who has the IPv6?", i Type code sono i seguenti:

![[Screenshot 2026-10-01 at 18.09.58.png]]
- **Time Exceed**: server per informare la sorgente che il TTL (chiamato in IPv6 Hop Limit) è scaduto.
Tutti sono importanti da vedere bene in dettaglio
### Messaggi di Errori

### Neighbor Advertisement
![[Screenshot 2026-10-01 at 18.16.22.png]]
- **Router**: è il **MAC** del router serve spesso e lo si identifica in maniera unovica, dove il router manda ogni tot dei **Neighbor Advertisement** agli host che sono collegati tra di loro
- **Solicited**: se viene solicitato dal router quando manda il messaggio di riconoscimento del router.
![[Screenshot 2026-10-01 at 18.19.15.png]]
### Host Membership Discovery
![[Screenshot 2026-10-01 at 18.20.20.png]]
Le report servono a dire al router che si è interessati ad un certo gruppo

## Configurare un'IPv6
Quali sono le informazioni che vogliamo e che servono per navigare. Server il prefisso che però viene fornito dall'ISP e l'interface identifier, il default gateway. Serve poi l'IP del DNS, l'hostname per un nome e domain name (opzionale). Infine il MTU (Maximum Transmission Unit).

Prendiamo come esempio questa spiegazione
$$\text{Indirizzo IPv6 (128 bit)} = \underbrace{\text{Network Prefix (64 bit)}}_{\text{Prefisso di rete}} + \underbrace{\text{Interface ID (64 bit)}}_{\text{Identificatore interfaccia}}$$
### Come Fare?
1. Farlo a mano
2. Usiamo il DHCP
3. Stateless Configuration, generazione in autonomia delle informazioni di prima e il prefisso che lo prendiamo dal router (importante e necessario)
4. Hybrid, informazioni che prendiamo dal DHCP, altre dal router ed altre dal DHCP.

Se lo facciamo a mano allora dobbiamo considerare che:
- **Network Prefix (64 bit):** Viene assegnato dal router o dall'ISP (ad esempio: `2001:db8:1234:5678::/64`).
    
- **Interface ID (64 bit):** Viene generato automaticamente dalla scheda di rete convertendo il suo **MAC Address (48 bit)** in un formato a **64 bit** tramite l'algoritmo **EUI-64** (Modified Extended Unique Identifier 64). 
### Generare L'Interface  ID
Lo possiamo inventare da soli, lo possiamo ottenere dal DHCPv6 o generato manualmente. Partendo dal MAC mi posso generare 64 bit che sono i bit necessari per l'**interface id**. Approccio chiamato EUI-48.

Si parte dai 48 bit del MAC e lo si configura nell'immagine qua sotto. Dove si divide l'indirizzo in due parti![[Screenshot 2026-10-01 at 18.27.14.png]]
Si può avere il MAC universale, che anche l'IP sarà univoco, cioè cosa vuol dire, che se parto da 0 si andrà ad 1. Ma se sul MAC c'era 1 allora bisogna metterlo nell'Interface ID che andremmo a generare a 0.
### Spiegazione passo passo
Prendiamo per esempio il MAC address `3C:06:30:4A:2F:10`
1. Si divide il MAC address esatto in due metà da 6 byte (6 cifre esadecimali ciascuna):

	- Prima metà: `3C:06:30`
    
	- Seconda metà: `4A:2F:10`
	
	Il primo byte dell'indirizzo MAC nell'esempio è `3C`.

2. Converti il primo byte in binario (8 bit):
    
    - `3` = `0011`
        
    - `C` = `1100`
        
    - `3C` = `0011 1100`
        
3. Individua il **7° bit da sinistra** (denominato bit **U/L, Universal/Local**) e **invertilo** (se è `0` diventa `1`, se è `1` diventa `0`):
    
    - Bit binari: `0 0 1 1 1 1` **`0`** `0`
        
    - Invertendo il 7° bit: `0 0 1 1 1 1` **`1`** `0`
        
4. Riconverti il byte modificato in esadecimale:
    
    - `0011` = `3`
        
    - `1110` = `E`
        
    - Nuovo primo byte: `3E`    

>[!tip] **Trucco rapido all'esame per il Passo 3:**
> 
> Invertire il 7° bit equivale matematicamente a fare un'operazione XOR con `0x02` sul primo byte:
> 
> - Se la seconda cifra del primo byte fa parte di `{0, 1, 4, 5, 8, 9, C, D}`, aggiungi 2 alla cifra.
>     
> - Se fa parte di `{2, 3, 6, 7, A, B, E, F}`, sottrai 2 alla cifra.
>     
>     _(Nel nostro caso: `C` (12) + 2 = `E` (14) $\rightarrow$ da `3C` a `3E`)_.
>     

#### **Passo 4: Formattare l'Interface ID in blocchi IPv6**

Raggruppa i 64 bit ottenuti in **4 gruppi da 4 cifre esadecimali** separati dai due punti (`:`):

$$\text{Interface ID} = \text{3E06:30FF:FE4A:2F10}$$

#### **Passo 5: Unire Prefisso e Interface ID**

Se il prefisso della rete è `2001:db8:1111:2222::/64`, l'indirizzo IPv6 completo sarà:

$$\mathbf{2001:db8:1111:2222:3e06:30ff:fe4a:2f10}$$

Se si desidera generare il **Link-Local Address** (che ha come prefisso fisso `fe80::/64`):

$$\mathbf{fe80::3e06:30ff:fe4a:2f10}$$

>[!warning] Importante
>Nel metodo classico **EUI-64** spiegato a lezione, gli ultimi 64 bit dell'IPv6 (l'Interface ID) vengono calcolati direttamente a partire dal MAC address dell'interfaccia di rete. Tuttavia, nei sistemi operativi moderni come **macOS**, **iOS**, **Windows** e **Linux**, l'utilizzo di EUI-64 **è stato abbandonato per impostazione predefinita** per ragioni di **privacy e sicurezza**:
### Address Prefix
Lo prendiamo dal router, lo prendiamo dal DHCPv6, generato automaticamente nell Link Local, che è sempre uguale `fe80::/64`. La configurazione a mano viene solo per i laboratori. Il router comunica il prefisso di rete.

Ci serve un pacchetto Router Advertisement tramite ICMP, che dice qual'è il prefisso di rete su una rete in cui si è connesso. Può avvenire in maniera **Solicited**, cioè che un host può solleciatare un router a rispondere. Oppure in maniera periodica i router mandano dei pacchetti chiamati Router Advertisement. Tutti questi pacchetti inviati avvengono in Multicast![[Screenshot 2026-10-07 at 16.11.38.png|960]]

#### Router Advertisement
![[Screenshot 2026-10-07 at 16.12.39.png]]
Ci sono le opzioni come l'**Hop-limit**, oppure per quanto tempo considerare le operazioni del router. Poi ci sono due flag **M** e **O**
- **M**: 1 le informazioni sono nel **DHCP**, 0 sono presenti nel pacchetto delle configurazioni
- **O**: 1 se ci sono altre configurazioni
- **Options**: che è formato del tipo T-L-V

#### Prefix Information Options
![[Screenshot 2026-10-07 at 16.15.53.png]]
- **L** : va bene sul prefisso privato **on-link**
- **A**: ci dice se possiamo usarlo in una configurazione automatica

### MTU (Maximum Transfer Option)
Assicura che gli host nella rete seguano la dimensione massima dei pacchetti sulla rete
![[Screenshot 2026-10-07 at 16.18.03.png]]

### Link Layer Address Option
Il router invia un indirizzo mac tramite questo pacchetto, questo ci serve per evitare una neighbor solicitation.![[Screenshot 2026-10-07 at 16.18.57.png]]

### ICMP Redirect
Viene inviato dal router ad un host per notificarlo che il router ha trovato un percorso migliore da inviare il pacchetto. Questo avviene se due router sono nella stessa rete.
![[Screenshot 2026-10-07 at 16.22.19.png|1112]]
Per l'IP destinazione, ti conviene passare per il router che è presente nel **Target Address** e nel campo options si mette il **MAC**  address del router target

## Duplicate Address Detection (DAD)
Meccanismo per verificare che nella rete ci sia un'altro host o un'interfaccia nella stessa rete. Cioè quando mandiamo un pacchetto per prendere l'indirizzo IPv6 di una rete, se entro 1 secondo non c'è nessuna risposta il nuovo IP che voglio prendere è valido. Per fare questo devo mandare un **Neighbor solicitation**, dove però il campo source (cioè l'IP sorgente dove manda il pacchetto) del pacchetto è **unspecified**  (solamente i due pallini ::). L'indirizzo IPv6 di destinazione è un **Solicited Node Multicast Address**

## Stateless Configuration: Basic Step
L'interface ID lo genero in uno dei modi, applico il [[#Duplicate Address Detection (DAD)|DAD]], devo iscriversi l'indirizzo IP nel multicast, dove si configura la NIC dicendo che farà parte di una rete. Poi viene inviato un pacchetto **ICMP Multicast Listener Report** che **se lo invia a se stesso**, questo IP viene utilizzato per la rete locale e non in internet.

## Stateless Configuration: Con i router
Stessa cosa come prima solo che il router create un indirizzo da un advertised prefix

## Scoped Address
![[Screenshot 2026-10-07 at 16.43.05.png]]
**%19**(Scope) alla fine dell'indirizzo IPv6 c'è un'interfaccia che ci aiuta a capire in quale porta bisogna inviare il pacchetto. Cioè identifica l'interfaccia al livello
# Reference
---

