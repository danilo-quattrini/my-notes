---
created: 2026-10-15
tags:
  - baby
topics:
  - Cybersecurity
  - "[[School]]"
author: Danilo Quattrini
---
# LAN & VLAN
---
## Question
### Introduzione
- Quali sono i vari dispositivi presenti in una LAN?
- Che cos'è una LAN?
- Come viene utilizzata?
- Come è nata la LAN?

### Repeater
- Che cosa sono i repeater?
- In che livello del modello ISO/ OSI lavorano?
- Che cosa fanno i repeater?
- Che condizioni le due reti devono avere affinché possano entrambi comunicare tramite un repeater?

### Bridge
- Che cos'è un bridge?
- In che livello ISO / OSI lavora?
- Si possono utilizzare due link fisici differenti se si ha un bridge fra due reti?
- Come si chiama il meccanismo per cui il bridge permette di evitare le collisioni?
- Quali sono i passaggi che svolge il bridge quando riceve una trama?
- Come viene denominato il protocollo Ethernet?
- Che differenza c'è tra un dominio di collisione e un dominio di broadcast?

### Half Duplex & Full Duplex
- Che differenza c'è tra un link half-duplex con uno full-duplex?
- Che particolarità possiede il full duplex che l'half duplex non ha?
- Usare un link full duplex tra un host ed un repeater, evita le collisioni?
- Quali sono i vantaggi di utilizzare un full-duplex?

### Switch 
- Che cosa sono gli switch?
- Come sono strutturare le LAN moderne?
- C'è più bisogno di utilizzare il protocollo CSMA/CD?
- Che cosa si intende per flooding negli switch?
- Che meccanismi deve avere lo switch per essere considerato "smart"?
---
## Storia dell WAN & LAN
Le reti locali nascono con l'idea di evitare di creare un circuito dove si mandano pacchetti. 
WAN e LAN hanno avuto un evoluzione distinti tra di loro, però alla fine vinse il protocollo IP
## Standard per la LAN
![[Screenshot 2026-10-15 at 16.16.47.png]]

## Dispositivi di una LAN in breve
- Livello 1: [[#Repeater|Repeater]], come gli [[#Hub|hub]] 
- Livello 2: Bridge / Switch 
- Livello 3: Router separa i dominii di broadcast (perché se no avremmo il broadcast su tutto internet), non è specifico per le LAN
### Repeater
Il Repeater, che è anche chiamato *relay*, che **opera solo al livello fisico**, nel modello [[OSI & TCP-IP]], prende il segnale a livello fisico e lo propaga, non fa nessuna operazione a livello algoritmo, ma propaga solo il segnale.
![[Screenshot 2026-10-15 at 16.20.42.png]]
Rigenera il segnale per estendere la portata del segnale, ci sono due cose fondamentali:
1. Il repeater lavora per la stessa tecnologia **Medium Access Control** (MAC)
2. Tra una porta e l'altra ci deve essere la stessa capacità, se in una porta (come ad esempio nell'host 2 H1) ci sono 100 Mb/s anche l'altro host deve avere la porta a 100 Mb/s. 
Il repeater deve operare su due canali dello stesso tipo e della stessa velocità.
#### Esempio
![[Screenshot 2026-10-15 at 16.25.27.png]]

### Hub 
Non c'è differenza tra Hub e Repeater, l'hub ha solo più di due porte.
![[Screenshot 2026-10-15 at 16.26.34.png]]
### Bridge
Siamo al livello due del modello ISO OSI,  introdotto dalla DEC nel 1983, all'inizio erano stati proposti come software, serviva per collegare diversi data link layer. **Ci permette di passare tra due tecnologie diverse** (esempio passiamo tra Ethernet a Wi-Fi oppure da Ethernet a Fast Ethernet)
![[Screenshot 2026-10-15 at 16.28.37.png]]

>[!info] N.B
>Si possono avere diversi physical link di diversa velocità se si ha un bridge.


![[Screenshot 2026-10-15 at 16.30.16.png]]
In questo esempio se mandiamo una trama, da H2 (host 2) ad H1 il bridge deve riceve i bit che vengono inviati ad H2 ed aspettare che arrivi tutte le informazioni prima di mandarle ad H1. **Il Bridge rigenera il segnale ma non solo, ci permette anche di cambiare la tecnologia.**

Per far si che si evitano le collisioni tra pacchetti che vengono inviati tra diversi host, c'è un meccanismo che il Bridge è in grado di fare, e sono queste tre cose utili:
1. Ricevere la trama e poi dopo salvarla nella memoria
2. Modificare il pacchetto (esempio Ethernet a Token Ring)
3. Mandarla 
Il fatto di salvare in memoria e inviare si chiama *store & foreword*
#### Esempio
![[Screenshot 2026-10-15 at 16.38.16.png]]

#### Bridge e Collisioni
![[Screenshot 2026-10-15 at 16.39.13.png]]
Mettiamo caso che H1 manda un pacchetto ad H3, anche H2 vede che anche il suo canale è libero quindi manda il pacchetto, ma però si creerà una collisione nel canale, perché stiamo usando un **Repeater**, che non gestisce un meccanismo intelligente, ma manda i pacchetti senza preoccuparsi di collisioni verso l'host H3.

Invece con il **Bridge** questa cosa non succede, perché il primo pacchetto che riceve il Bridge lo salva al suo interno e lo invia solamente dopo che è stato inviato il pacchetto successivo, questo è il meccanismo di *store & foreword*.

Ethernet è un protocollo (CSMA/ CD):
- *Carrier Sense*(CS) = controlla se il canale è libero per inviare il pacchetto (questo perché a livello fisico se il canale è attivo, cioè ad alto wattaggio allora vuol dire che è occupato se no non).

- *Multi Access* (MA) cioè che più dispositivi si possono connettere fra di loro.

- *Collision Detection* (CD) identifica le collisioni che sono presenti nella rete Ethernet, questo perché si vanno a vedere se ci sono dei segnali che non sono il linea e sono storti. 

- **Dominio di Collisione**: dove mi accorgo della collisione, cioè l'area di un cavo singolo, viene chiamato anche **network segment**.

- **Dominio di Broadcast**: l'areea dove le trame / pacchetti vengono inviate.

![[Screenshot 2026-10-15 at 16.48.41.png]]
Qui ci sono due **dominii di collisioni separati** ed un **singolo dominio di broadcast**

### Half and Full Duplex
In cavo **Half Duplex**, si possono solo inviare o riceve su quel cavo, cioè se un host invia un pacchetto tra un host ad un'altro, il canale è completamente occupato e si deve aspettare che il canale sia libero prima di svolgere qualsiasi nuova operazione.

**Full Duplex**, significa che ci sono canali diversi per inviare e ricevere pacchetti sulla rete.
![[Screenshot 2026-10-15 at 16.51.05.png]]
Sopra abbiamo l'esempio è che nel primo a sinistra se abbiamo un **hub con un canale full-duplex, avviene la collisione**, mentre se abbiamo un **Bridge questa collisione non avviene**, quindi full duplex + Bridge funziona.
#### Full Duplex
Introdotto con il Fast Ethernet che fa parte dello standard (802.3x)
![[Screenshot 2026-10-15 at 16.53.55.png]]
Il vantaggio di un full-duplex è di raddoppiare l **throughput**. Il traffico nelle LAN non è simmetrico. Non uso però il canale di up-link o il down-link allo stesso modo, solitamente si usa un canale più un down-link, in pratica non si usano spesso gli up-link.

>[!done] Vantaggio
>Non ci serve più il CSMA/CD, non avendo più collisioni, il meccanismo precedente non ci serve più perché non ci sono più collisioni.

Le LAN moderne sono tutte full-duplex e sono del tipo Hub-and-spoke, che sono collegati ad un dispositivo chiamato **Switch**, che **sarebbero dei bridge con più porte e architettura interna diversa**.
### Switch
Le LAN moderne sono basate sul full-duplex, switches ed ethernet, dove oggi ci sono i Gigabit Ethernet come (10GE, 100GE), dove non ci sono più i CSMA/CD, quando dichiamo **Switch** sarebbe l'**Ethernet Switch**. 

**Sono anche detti trasparenti**, cioè che siano plug and play e sono standardizzati dall IEEE 802.1D non richiedono nessuna modifica o configurazione del sistema. L'host agisce allo stesso modo sia che ci sia lo switch o no.
![[Screenshot 2026-10-15 at 17.08.58.png]]

Con router non mettiamo il MAC di destinazione dell'host in cui vogliamo inviare il pacchetto, ma mettiamo il MAC del router, conoscendo anche a che host abbiamo inviato il pacchetto.

![[Screenshot 2026-10-15 at 17.10.15.png]]
Uno switch può avere un indirizzo IP che serve per l'operatore per svolgere delle configurazioni, ma **non ci serve l'IP / MAC dello switch per poter comunicare sulla rete o su reti differenti**, permettendoci di non cambiare host senza dover smanettare su qualche configurazione, ottimo per qualsiasi cambiamenti che vogliamo fare.
#### Smart Forwarding
L'inoltro intelligente che abbiamo discusso prima, non sono così intelligenti, ma li possiamo rendere più **smart**. Se H1 manda una trama in H3 in **Unicast** e voglio che lo switch manda la trama solo ad H3 e non ad altri host, ma solo verso la destinazione.![[Screenshot 2026-10-15 at 17.16.01.png]]

Ma se mando un pacchetto in Multicast o Broadcast avviene il **flooding**, cioè lo switch manda i pacchetti a tutti gli host che sono connessi con lui, tranne alla porta dove ha ricevuto il pacchetto, oggi tutti con le trame multicast fanno flooding. Per le trame unicast come si fa a mandare verso solo alla destinazione che si vuole mandare?

Lo Switch ha delle informazioni sotto forma di tabella, che non è come la routing table, ma si chiama **forwarding table**, oppure si chiama anche **filtering database**. Questo perché siccome vogliamo evitare che le trame vengono mandate a tutti gli host della rete, si fa un'operazione di filtraggio, questo perché lo Switch si comporta come un bridge e come lui fa l'operazione di **store and forward**, che ci permette di fare queste tabelle.
![[Screenshot 2026-10-15 at 17.17.56.png]]

>[!info] Note sul **flooding**
>Il flooding che viene svolto dallo switch non avviene in tutte le porte in uscita allo stesso tempo, ma manda il pacchetto in tutte le porte in tempi differenti. L'hub **invece manda il pacchetto che riceve in flooding allo stesso tempo su tutte le porte in uscita**.

#### Smart Forwarding Technologies
Per ottenere questo "smart" forwarding i bridge/switch devono avere dei componenti al loro interno che sono definiti:
- Una tabella locale dove inviare i pacchetti [[#Filtering Database|Filtering Database]]
- Una stazione dove può imparare il percorso dei pacchetti [[#Backward Learning]]
- Un modo per evitare che i pacchetti girino all'infinito nella rete [[#The Loop Problem]]
##### Filtering Database
Sono delle tabelle contenuto all'interno dello switch nella quale si può trovare i seguenti campi:
- MAC di destinazione del pacchetto che si vuole inviare
- Porta nella quale inviare il pacchetto che ha ricevuto / dove è presente l'host
- Tempo in cui il pacchetto rimane dentro alla tabella (di default è 300s)
![[Screenshot 2026-10-15 at 17.42.39.png]]
Le tipologie di entry sono di tipo **dinamiche** o **statiche**.

- **Statiche** sono quelle che non vengono aggiornate dal *processo di learning* e sono solitamente 1000.

- **Dinamiche** vuol dire che lo switch da solo impara dove inviare i pacchetti a gli host, queste tabelle sono di dimensione di 2 a 64 mila **entries** (righe), che spesso bastano perché le entry dopo un pò vengono ripulite se non vengono più utilizzate.

Prendiamo come esempio la tabella di esempio fornita da Cisco.
![[Screenshot 2026-10-15 at 17.45.10.png]]
Tipicamente uno switch è fatto da 48 porte.
##### Forwarding Process
![[Screenshot 2026-10-15 at 17.47.29.png]]
In questo algoritmo sopra illustrato, **funziona sia per Unicast che per il traffico Multicast / Broadcast**.
Se si ha un match  del MAC nel DB si manda alla porta di destinazione, se no viene mandato a tutti in flooding (caso del **Forward on all Port** case).

Come fa a scrivere le entry nella tabella lo switch, c'è un algoritmo chiamato **backward learning**
##### Backward Learning
Se uno switch riceve da un **host 1** nella **porta 1** un pacchetto allora quell'host è raggiungibile dalla **porta 1**, e quindi aggiungo la entry nella **filtering database**.![[Screenshot 2026-10-15 at 17.56.36.png]]
Prendiamo un esempio all'inizio gli switch non sanno niente, mettiamo caso che h1 vuole mandare un pacchetto ad h2, lo switch 1, S1 salva la porta di h1 e la assegna ad h1. La trama lo riceve anche S2 che segna porta 2 assegnata ad h2. Poi dopo c'è l'invio effettivo della trama all'host 2 H2.

Da notare che all'inizio **TUTTI GLI SWITCH FANNO FLOODING**, perché si devono salvare nella propria filtering table, l'origine di dov'è H1.
![[Screenshot 2026-10-15 at 17.59.39.png]]
Quando H2 risponderà ad H1, S2 si aggiorna la tabella dove aggiungerà H2 è nella porta 3, ma siccome nella sua tabella conosce l'esistenza che la porta 2 è dove c'è H1 allora non farà flooding come era all'inizio, ma lo manda nella porta 2 invece che nella porta 2 ed 1.

>[!info] Come vengono pulite le entry di un di uno switch
>C'è un processo in background (Discard Zombies) che fa pulizia delle entry vecchie, cioè quelle che sono nella tabella da tanto tempo.

### Network and Host Mobility
Vorremmo gestire la mobilità degli host, assumiamo che un host si sposta da una rete ad un'altra
![[Screenshot 2026-10-15 at 18.13.07.png]]
Ma ora lo switch deve aggiornare la tabella, perché ora H2 si trova in un altra porta, **questo non è un problema**, perché se l'host 2 manda un'ARP request ho un pacchetto in broadcast allora lo switch cambia le informazioni all'interno della sua tabella.

Ma se non viene fatto broadcast allo ci saranno degli switch che non si aggiornano![[Screenshot 2026-10-15 at 18.16.12.png]]

>[!info] Summary
>Se si manda una trama in unicast ci sono problemi (che in realtà non ci sono), in broadcast / multicast invece tutti gli switch sanno del cambiamento di porta dell'host.

Ci possono essere però problemi con i NIC **fault tolerant**, che hanno due cavi una per una connessione ethernet ed una wifi, questo NIC speciale usati solo nei server che devono essere sempre attivi hanno due interfacce, che però se una di queste interfacce hanno un guasto, l'interfaccia che non ha un guasto manda un pacchetto in broadcast. 
![[Screenshot 2026-10-15 at 18.23.19.png|1066]]

### MAC Flooding Attack
L'host manda delle trame di continuo e dei MAC fasulli che vengono assorbiti dagli switch. Si possono generare dei MAC che vanno a riempiere le tabelle degli switch, come nell'immagine sottostante. Questo serve per ridurre le performance dello switch.![[Screenshot 2026-10-15 at 18.27.06.png|1120]]
**Una difesa è limitare il numero dei MAC in una specifica porta** oppure se il numero delle richieste è troppo elevate in un certo secondo o tempo stabilito allora si blocca la porta.

### The Loop Problem
Nel caso si utilizzi una topologia a maglia si possono generare dei cicli che rendono impossibile operare il backward learning. Questo perché quando si mandano dei pacchetti in multicast o in broadcast, non essendoci un campo nei pacchetti inviati che decrementi la sua "vita" nella rete, allora essi continueranno a girare nella rete all'infinito.
![[Screenshot 2026-10-15 at 18.29.52.png|1120]]
Il loop non smetterà mai perché non decrementa nessun *TTL* (Time To Live) e questo viene chiamato **Broadcast Storm** dove l'unica soluzione è quella di staccare / disabilitare il cavo (*Stacca Stacca ci hanno rintracciato*).
#### Which frames can generate loop?
>[!info] Chi generano i loop?
Possono essere generati tramite trame mandate in broadcast / multicast oppure trame unicast a stazioni che non esistono

#### How to solve the loop?
Per evitare che avvenga flooding infinito, non pefforza dobbiamo staccare il cavo, ma si può applicare un algoritmo chiamato **spanning tree**, dove gli switch si mettono d'accordo quale link bisogna disabilitare.![[Screenshot 2026-10-15 at 18.38.45.png]]

#### Spanning Tree
Dobbiamo rendere la rete come una struttura ad albero, infatti se si toglie un link da uno switch ad un'altro si vanno a generare degli alberi, che ci evitano di creare dei loop, cioè delle topologie di rete ad anello che mandano pacchetti all'infinito.
### Router
I router operano al livello 3 e sono gli unici dispositivi che separano il dominio di broadcast, diverse reti con diversi prefissi.![[Screenshot 2026-10-15 at 18.46.16.png]]

## Virtual Lan (VLAN)
La domanda da chiedersi è se conviene utilizzare una singola ed enorme LAN oppure diverse piccole LAN?
![[Screenshot 2026-10-21 at 16.40.08.png]]

Si sono viste però che ci sono diversi down-grade nell'utilizzare una LAN questi sono di tre tipi:
-  ***Performance**:* una singola LAN ha molto più traffico broadcast oppure flooded (ad esempio STP reconfiguration).

- ***Privacy e sicurezza:*** una singola LAN è più vulnerabile a intrusioni e attacchi.

- ***Gestione**:* reti più piccole sono più facili da gestire.

>[!info] Risposta
>Conviene utilizzare differenti reti LAN  piccole dimensioni

Fisicamente si può creare diverse LAN all'interno di un edificio, andando poi a collegare tali switch a diversi edifici in modo da creare delle reti LAN piccole e separate. Come nell'immagine sotto.![[IMG-LAN & VLAN-20261110.png]]

Tale operazione però è indubbiamente molto costoso, perciò sono state realizzate le **Virtual LANs (VLAN)**.
che consentono a un set di porte specifiche di uno switch di simulare che facciano parte di un dominio di broadcast differente, utilizzando un unica infrastruttura di rete. Per far parlare le VLANs è necessario un router con tutte le sottoreti connesse, permettendo la comunicazione in modo tradizionale anche se la rete di origine è in realtà la medesima.

>[!warning]
>Attenzione: il traffico di livello 2 non può attraversare le VLANs.

Un altro modo è connettere il router a un unica interfaccia che lavora per entrambe le sottoreti, ottenendo il **one arm router**.
![[Screenshot 2026-10-21 at 16.44.43.png]]
Usiamo un solo link che però passano più VLAN, condividendo l'infrastruttura fisica su diversi processi che girano. Due VLAN di rete devono avere due reti differenti, perché sono considerate come rete differenti.

Per **connettere più VLAN è necessario un router** (livello 3) per eseguire il lookup, l’header di livello 2 viene scartato (non può viaggiare tra VLAN) in favore di uno nuovo creato con un differente indirizzo MAC.

Il broadcast non può attraversare VLAN differenti, per questo non è possibile utilizzare ARP per individuare gli indirizzi MAC di un’altra VLAN. Gli host di Virtual LANs differenti devono fare riferimento a reti IP differenti.

Il modo più semplice per associare un frame a una VLAN è marcarlo all’arrivo in base alla porta attraversata. Se però non si altera la trama, l’informazione sarà evidenziata solo all’interno dello switch locale che ha attraversato ma non agli altri switch. 

Per superare questo problema è stato introdotto il tagging, ovvero un campo aggiuntivo di 4 byte nella trama ethernet contenente il **vlanID**, in modo da identificarlo anche negli switch rimanenti.
![[Screenshot 2026-10-21 at 16.55.54.png]]
Lo standard 802.1Q sarebbe la porzione di header composta da 4 byte che identifica la trama ethernet da  mandare nelle varie VLAN

### Tipologie di Porte
Per fare ciò è necessario apportare delle piccole modifiche al protocollo MAC già esistente, in particolare un nuovo framing (per il tagging) indipendente dall’indirizzo MAC e la lunghezza massima dei frame deve essere estesa di 4 byte, questa operazione viene svolta dallo switch.

Le porte si dividono in:

- **Access**: inviano e ricevono trame non taggate (default sugli end systems come host, switches, servers, routers ecc), vengono solitamente utilizzato per connettere end‑stations alla rete. Il formato del frame non deve essere cambiato dagli host (che non sa dell’esistenza della VLAN).
	
- Trunk: inviano e ricevono trame taggate, devono essere configurate esplicitamente. Spesso viene utilizzato nelle connessioni switch‑to‑switch e per connettere server/router.

Nell’immagine che segue, in cui tutte le porte sono di tipo access, l’host H1 è in grado di comunicare con l’host H4 in quanto i valori configurati su porte access non sono propagate al di fuori dallo switch.
![[Screenshot 2026-10-21 at 17.16.24.png]]

==Vedere come le VLAN vengono associate agli host==

### VLAN & Spanning Tree
Ho facciamo Spanning Tree per infrastruttura oppure si può fare Per-VLAN Spanning Tree, facendo si che il link sia disabilitato  in diversi campi
![[Screenshot 2026-10-21 at 17.25.42.png]]