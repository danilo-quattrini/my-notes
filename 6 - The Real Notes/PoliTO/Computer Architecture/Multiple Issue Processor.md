---
created: 2026-10-27
tags:
  - baby
topics:
author: Danilo Quattrini
---
# Multiple Issue Processor
---
Oltre a paralelizzare la fase di execute e decode, dobbiamo anche prendere più istruzioni alla volta, per fare ciò si utilizzano i processori *superscalari* che possiedono strategie statiche e dinamiche.
## Strategia Statica del Processore SuperScalare
Due istruzioni per colpo di clock e quando si fa uno scheduling statico allora le istruzioni dovevano essere uno di questi tipi
- Una load, store, branch o operazioni di interni tramite la **ALU**

- Operazione di floating point diversa dalla load e store

Vengono prese due istruzioni alla volta che però richiedono uno spazio di 64 bit, questa coppia di istruzioni si chiama *issue packet*. L'ordine delle istruzioni sono importanti, dove si richiedeva che le istruzioni con interni erano sempre le prime, **oggi però i processori non hanno questo problema**

>[!example] Esempio
>![[Screenshot 2026-10-27 at 08.49.17.png]]
>Se notiamo ora in ogni colpo di clock prendiamo due istruzioni alla volta e quello che vogliamo raggiungere è un CPI che sia vicino allo 0.5

>[!warning]
>L'issue packed devono contenere solo un istruzione di salto

## FP Units
Più unità floating point, meglio è perché avremmo risultati migliori nei processori, bisogna però stare attenti che se l'istruzione FP Load, store o move e la seconda istruzione invece è un operazione di FP di addizione, moltiplicazione, ecc... Allora si dovrà forzare a far stallare l'istruzione che esegue le operazioni di ALU.

## Branch Delay
![[Screenshot 2026-10-27 at 08.58.46.png]]

# Multiple Issue Dynamic
Si mette insieme tutto quello che si è detto fino ad ora

## Criticità del CDB

## Esempio 
Prendiamo il codice seguente
```
Loop:
	ld x2,0(x1) #x2=arrayelement
	addi x2,x2,1 #increment x2 
	sd x2,0(x1) #storeresult 
	addi x1,x1,8 #increment pointer esempio a 64 bit
	bne x2,x3,Loop #branch if not last
```

Consideriamo il processore che può fare le issue e la commit nello stesso clock cycle e considerare due casi:
- Senza Speculazione
- Con Speculazione
### Caso Senza Speculazione
![[Screenshot 2026-10-27 at 09.06.52.png]]

Le due prima istruzioni, che non hanno vincoli all'ordine delle istruzioni intere e floating point, l'unico vincoli è presente nella branch. La prima istruzione viene eseguita in modo tranquilla, leggendo da sinistra fino a destra. Mentre la seconda istruzione dovrà aspettare che l'istruzione sopra deve ancora finire, quindi l'**Executes at clock Cycle Number** avviene al clock cycle 5, cioè dopo che l'istruzione precedente ha scritto sul **CDB**.

### Caso con Speculazione
![[Screenshot 2026-10-27 at 09.25.24.png]]

## Come fare il calcolo sulla tabella
Consideriamo la issue per due, EXEcute 2, CDB per uno e i Commit per 1
![[Pasted image 20261028230646.png]]
### 1. Colonna ISSUE (Emissione)

**Regola:** Procedi rigorosamente dall'alto verso il basso.

- Controlla la capacità hardware. L'intestazione di solito ti dice quante istruzioni puoi emettere (qui è sottointeso un _Issue x2_).
    
- Assegna il ciclo 1 alle prime due istruzioni, il ciclo 2 alle successive due, il ciclo 3 alle successive, ecc.
    
- _Nota:_ L'unico motivo per ritardare un Issue è se le "Reservation Station" (le code di attesa) sono tutte piene, ma nei classici esercizi su carta si assume quasi sempre che ci sia spazio.

### 2. Colonna EXE (Esecuzione)

**Regola:** Un'istruzione inizia l'esecuzione nel primo ciclo utile in cui si verificano **tutte e tre** queste condizioni:

1. È stata già emessa (il ciclo di EXE deve essere strettamente maggiore del ciclo di Issue).
    
2. L'unità di calcolo (ALU, Moltiplicatore, ecc.) è libera.
    
3. **Tutti i dati sorgente sono pronti.**
    

**Come ragionare sui dati pronti (Dipendenze RAW):**

- Guarda la riga 3 (`fmul.s f3, f1, f1`): ha bisogno di `f1`. Chi calcola `f1`? La `flw` alla riga 1. Quando è pronto `f1`? Devi guardare la colonna **CDB** della riga 1, che indica il ciclo **4**. Poiché il dato viaggia sul bus al ciclo 4, la moltiplicazione lo "cattura" e inizia l'esecuzione al ciclo **5**.
    
- Guarda la riga 4 (`fdiv.s f4, f1, f2`): ha bisogno di `f1` (pronto al ciclo 4) e `f2` (pronto al ciclo 5). La divisione deve aspettare l'ultimo dato in ritardo. Inizierà al ciclo **6**.
    
- _Le istruzioni intere (`addi`):_ Modificano registri come `x1, x2, x3` che non dipendono dai lenti calcoli Floating Point. Possono partire subito un ciclo dopo il loro Issue (es. l'`addi x2` fa Issue a 4 e parte in EXE a 5).
    

### 3. Colonna MEM (Memoria - Solo per Load e Store)

**Regola:** È l'accesso fisico alla RAM. Ci entrano solo `flw` e `fsw`.

- **Per le Load (`flw`):** Vanno in MEM esattamente un ciclo dopo aver calcolato l'indirizzo in EXE. (es. riga 1: EXE al ciclo 2, MEM al ciclo 3).
    
- **Per le Store (`fsw`):** L'indirizzo viene calcolato subito in EXE, ma **non possono scrivere in memoria finché il dato da salvare non è pronto**.
    
    - _Esempio cruciale (riga 6):_ `fsw f5, 0(x4)`. L'indirizzo `0(x4)` viene calcolato velocemente in EXE al ciclo **4**. Ma cosa deve salvare? Il registro `f5`. Chi calcola `f5`? La `fadd` alla riga precedente, che scriverà `f5` sul CDB solo al ciclo **13**. Pertanto, la Store rimane "congelata" e potrà eseguire la fase MEM solo al ciclo **14**.
        

### 4. Colonna CDB (Scrittura del Risultato)

**Regola:** Il risultato viene trasmesso sul bus 1 ciclo dopo aver **finito** l'esecuzione (o la fase MEM per le Load).

- Devi conoscere le latenze del tuo hardware (quanti cicli dura la fase EXE).
    
- _Esempio riga 3 (`fmul.s`):_ Inizia a 5, scrive sul CDB a 9. Significa che ha impiegato 4 cicli (5, 6, 7, 8).
    
- _Esempio riga 5 (`fadd`):_ Inizia a 11, scrive sul CDB a 13. Significa che ha impiegato 2 cicli (11, 12).
    
- _Vincolo hardware:_ La tabella dice **CDB x2**. Se 3 istruzioni dovessero finire esattamente nello stesso istante, due scriverebbero sul CDB subito, la terza dovrebbe aspettare un ciclo in più per traffico sul bus.

>[!info] Regola 1
>Un'istruzione non può mai fare commit prima di aver calcolato il risultato. Quindi, il suo valore di Commit deve essere **almeno** `CDB + 1`. Se un'istruzione scrive sul CDB al ciclo 20, non può fare commit prima del ciclo 21.

>[!info] Regola 2
>Nessuna istruzione può scavalcare quella sopra di lei nella fase di Commit. Se l'istruzione 1 fa commit al ciclo 15, l'istruzione 2 non può fare commit al ciclo 14 (anche se aveva finito di calcolare molto prima). Il Commit dell'istruzione 2 sarà **almeno** uguale al Commit dell'istruzione 1.

### 5. Colonna COMMIT (Ritiro)

**Regola d'oro:** Il Commit deve essere **rigorosamente in ordine dall'alto verso il basso**, rispettando la capacità massima (COMMIT x2 = massimo due istruzioni ritirate per ciclo).

- Un'istruzione può fare commit se ha completato la sua fase CDB (o MEM per le store) **E** se tutte le istruzioni sopra di lei hanno già fatto commit o lo stanno facendo nello stesso ciclo.
    
- _Esempio di attesa forzata (riga 7, `addi x2`):_ Questa addizione ha finito il suo calcolo rapidissimo scrivendo sul CDB al ciclo **6**. Ma guarda il suo Commit: **15**. Perché? Perché l'istruzione sopra di lei (`fsw`) non finisce la sua fase MEM fino al ciclo 14. L'`addi` rimane bloccata nel Reorder Buffer per 9 cicli, aspettando pazientemente il suo turno per rispettare l'ordine originale del programma.
    
- _Accorpamento:_ Al ciclo 14 fanno commit la `fadd` e la `fsw` (2 istruzioni, il limite massimo). Al ciclo 15 si sblocca la coda e fanno commit le due `addi` (riga 7 e 8) che avevano finito di calcolare molto tempo prima.


### CASO SPECIALE CON DIVISIONE
![[IMG-Multiple Issue Processor-20261030.png]]

Qui sopra abbiamo un caso molto particolare, come vediamo in verde sono evidenziate delle righe che sembrano sbagliate ma in realtà non lo sono, questo perché se prendessimo la tabella come pensiamo doveva essere risolta vediamo una cosa importante.![[IMG-Multiple Issue Processor-20261030-1.png]]

Quelle evidenziate in giallo sono il nostro punto di interesse, vediamo che la prima divisione della seconda iterazione può andare in fase di execute nel clock cycle `13d`, questo perché gli operandi `f1` e `f2` sono pronti entrambi già dal ciclo di clock `12`, quindi può eseguire il calcolo alla 13.

MA SE VEDIAMO LA PRIMA DIVISIONE DELLA PRIMA ITERAZIONE, LEI LA ESEGUE 1 COLPO DI CLOCK IN RITARDO, quindi succede che la divisione con meno colpi di clock sovrasta / sorpassa la prima divisione del primo ciclo di clock andando ad occupare l'unità funziona prima di lei.

Questo comporta che la divisione della prima iterazione può partire solo se la prima divisione della seconda ha terminato.
![[IMG-Multiple Issue Processor-20261030-2.png]]

### In quali casi si verifica questo "Sorpasso"? (Formalizzazione)

Un'istruzione successiva nel codice ($I_{successiva}$) sorpassa un'istruzione precedente ($I_{precedente}$) nell'accesso a un'unità funzionale quando si verificano contemporaneamente queste 4 condizioni:

1. **Unità Funzionale Non-Pipelined (o con risorse limitate):** L'unità ha un intervallo di inizializzazione $> 1$, creando una competizione (hazard strutturale) per l'accesso.
    
2. **Stallo per Dati della prima istruzione ($I_{precedente}$):** $I_{precedente}$ ha subito un ritardo in stazione di riserva a causa di una dipendenza RAW lunga (es. una divisione precedente).
    
3. **Prontezza Indipendente della seconda istruzione ($I_{successiva}$):** $I_{successiva}$ è già stata emessa (fase di Issue) e i suoi operandi diventano disponibili sul CDB _prima_ che si risolva la dipendenza di $I_{precedente}$.
    
4. **Coincidenza di Tempistica (Window of Opportunity):** Nel ciclo esatto in cui l'unità funzionale si libera, $I_{successiva}$ ha già tutti gli operandi pronti, mentre $I_{precedente}$ non li ha ancora ricevuti (o li riceve nello stesso ciclo, potendo partire solo nel ciclo successivo).