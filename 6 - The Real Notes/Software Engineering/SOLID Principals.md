---
share_link: https://share.note.sx/jo9vo0o3#TuKBOaZtdX0U3SzhENPGG1M96UoxW076P0ru0BxJaXM
share_updated: 2026-01-06T10:16:21+01:00
---
 2024-11-20 19:11

Status: #baby 

Tags: [[Programming Knowledge]], [[OOP]], [[3 - Tags/Java]]

---
# SOLID Principals
---
## S - ingle responsibility

>[!quote] Definition 
>Una classe deve avere solo un singolo motivo per dover cambiare.

Ogni classe possiede la propria responsabilità e si deve fare in modo che  gestisca le sue operazioni, senza andar a fare più del necessario, _la classe deve avere solo una ragione per cambiare_.

Guardiamo questo esempio di classe `Employee` che non è gestita bene.
![[ExampleOfSolidPrinciple.png]]
In questo caso vediamo che possiede ben due _responsabilità_, una è quella della stampa dello `printTimeSheetReport()` e la seconda è quella di prendere i nomi dei dipendenti `getName()`, questo viola il principio quindi per risolvere tale situazione si farà così.
![[SolutionOfSingleResponsibility.png]]

>[!warning] **Perché è importante nella progettazione.** (exam question)
>1. Per la progettazione l'utilizzo del principio di singola responsabilità, aiuta nel ridurre la complessità dei progetti che si svilupperanno, creando un codice che sarà semplice mantenerlo nel tempo. 
>2. Durante la fase di mantenimento, se non si cerca di semplificare il codice che si andrà a modificare, si andrà facilmente in confusione, questo perché avendo una classe che ha molte responsabilità, se dovessimo modificare almeno una di queste, potremmo rischiare di modificare altri componenti che non vogliamo rompendo il codice. 

## O - pen/ closed 

>[!quote] Definition 
>Le classi devono essere aperte ad estensioni *Open*, ma chiuse alle modifiche esterne *Closed*.

Una classe viene definita _Open_ nel caso si riesce ad aggiungerci nuovi attributi, metodi oppure [[6 - The Real Notes/Java/Java#Overriding (sovrascritto)|sovrascrivere]] i metodi implementandone nuove funzionalità ecc.. In Java per rendere una classe _Closed_ si viene ad utilizzare il modificatori d'accesso [[6 - The Real Notes/Java/Java#`final`|final]], nei vari attributi o metodi che vogliamo non siano modificabili dalle estensioni della classe oppure da classi esterne.

>[!tip] Programming Tip
>Se sai che una classe contiene un bug, non andare a creare una sottoclasse che ne vada a risolvere il problema, ==il figlio (sottoclasse) non è responsabile dei problemi del padre (superclasse)==.

Guardiamo ora un'esempio di come possiamo applicare questo principio ad una classe `Order`, che nel nostro caso contiene tanti metodi per la gestione degli ordini ed è molto complicata la classe, tanto da rischiare di poter rompere l'intera app se si fanno delle modifiche.

![[O-penClosexample.png]]
La soluzione da applicare sarebbe quella di utilizzare un design pattern chiamato _Strategy_ %%mettere il link con il suo design pattern%%intanto vedremmo qui la risoluzione.
![[Strategy-applied.png]]
Ora grazie all'interfaccia `Shipping` possiamo derivare le varie classi che implementeranno i metodi di spedizione, senza dover utilizzare la classe principale `Order`.

> [!warning] **Perché è importante nella progettazione.** (exam question)
> 1. Nella progettazione è utile avere delle classi che siano aperte a delle estensioni, cioè si possono usare dei metodi o degli attributi del padre, in modo che possiamo aggiungere o modificare delle funzionalità al nostro software.
> 2. Si eviterà di dover modificare la classe che conterrà i metodi che vogliamo utilizzare, cioè se durante la fase di sviluppo non vogliamo che la classe che ci eroga tali metodi e attributi sia modificabile, basterebbe mettere il metodo o l'attributo come [[6 - The Real Notes/Java/Java#`final`|final]], così non si rischierà di modificare i comportamenti del padre.
## L - iskov Substitution [^1]

>[!quote] Definition
>Quando una classe è estesa da una sua sottoclasse, **la sottoclasse dovrebbe poter essere utilizzata al posto della classe genitore**,  senza rompere o modificare il funzionamento del codice esistente.

Ciò vuol dire che quando estendiamo una classe, la sottoclasse deve avere gli stessi comportamenti della classe genitore (super-classe), cioè quando si sovrascrive un metodo della super-classe, questo non deve essere sostituito interamente con qualcos'altro ma solo modificato in parte.

Questo principio contiene delle checklist affinché venga rispettato pienamente (non possiede libera interpretazione), vediamoli insieme:

1. Quando una sottoclasse sovrascrive `@Override` un metodo della super classe, i **tipi di parametro** del metodo nella sottoclasse devono essere **uguali o più astratti** rispetto ai tipi di parametro usati nel metodo della super classe.
   
   Questo cosa vuol dire:
	-  Se nella super-classe il metodo accetta un parametro di un certo tipo, nella **sottoclasse non possiamo restringere quel tipo.**
	  
	-  Possiamo, però, usare un tipo più generico (cioè una super-classe del tipo originale) o lo stesso tipo. 
	
	In altre parole, il metodo della sottoclasse dovrebbe essere in grado di **accettare almeno gli stessi tipi di input** che il metodo della super-classe può accettare, se non di più.

2. Quando si sovrascrive un metodo di una superclasse in una sottoclasse, il **tipo di ritorno** del metodo sovrascritto Deve essere **lo stesso tipo** del metodo nella superclasse, oppure può essere un **sottotipo** (cioè una classe derivata) del tipo di ritorno della superclasse.
   
   Questo cosa vuol dire:
	- Che ad esempio se nella sottoclasse si viene a sovrascrivere un metodo `buyCat(): BengalCat` il client riceverà un tipo di gatto che fa parte della famiglia gatti quindi è apposto.
	  
	  - Nel caso però si venga a sovrascrivere il metodo in questo modo `buyCat(): Animal`, il codice si romperebbe perché non si sa che tipo di animale sta ritornando il metodo della sottoclasse (un pesce? una scimmia?).
	
	Stesso esempio lo si può fare nel mondo della programmazione, nell'esempio dei tipi dinamici, cioè non ha senso che il metodo base se ritorna una stringa allora il suo metodo esteso ritorni un numero. 
	
2. Quando si crea una sottoclasse e si sovrascrive un metodo della superclasse, è importante che il metodo sovrascritto **non aggiunga nuove eccezioni** che il metodo originale (della superclasse) non prevede.

Prendiamo come esempio una classe che chiameremmo  `FileReader`, che verrà estesa da un `SecureFileReader`, che implementa un'ecezione.
 ```java
class FileReader {  
    public String readFile(String path) {  
        return "Reading file: " + path;  
    }  
}  
  
class SecureFileReader extends FileReader {  
    @Override  
    public String readFile(String path) {  
        if (!userHasAccess(path)) {  
            throw new SecurityException("Access denied");  
        }  
        return super.readFile(path);  
    }  
  
    private boolean userHasAccess(String path) {  
        return false;  
    }  
}
   ```

Questo è un **esempio di come si viola il principio di Liskov**, introducendo un eccezione dove la classe non dovrebbe 

_For more detail about other examples and rules read from page 57 to 60 of the book Dive into Design Patterns by Alexander Shvets_.

> [!warning] **Perché è importante nella progettazione.** (exam question)
> 1. Non si va a modificare il comportamento dei metodi che sono presenti nella classe del genitore, questo è utile quando si va ad implementare un framework, nella quale sappiamo ci sono dei metodi che devono rispettare tali funzionalità.
> 2. Ci aiuta a capire se una sottoclasse rimane compatibile con il codice che è presente nella superclasse, cioè non va a modificare i comportamenti della superclasse e avremmo un codice coerente con le specifiche.

## I - nterface Segregation 

>[!quote] Definition
>I client non devono obbligatoriamente dipendere da metodi che non utilizza

Questo principio afferma che **è meglio avere diverse interfacce specifiche e più piccole piuttosto che un’unica interfaccia grande e generica**, cioè che ogni interfaccia dovrebbe essere **limitata** e **mirata** a un singolo ruolo o gruppo di funzionalità.

Permettendo a ogni classe di implementare solo le interfacce che realmente servono al suo comportamento. **Interfacce troppo grandi e generiche** possono creare problemi, ==poiché forzano le classi che le implementano a definire metodi inutili o che non hanno senso per la classe==.
#### Example

Quando andremmo ad esempio a creare un interfaccia `Animal` che definiremmo così

```java
interface Animal {
    void walk();
    void fly();
    void swim();
}
```

Così facendo costringiamo alla classe che implementerà questa interfaccia come ad esempio `Dog` a dover utilizzare metodi che non gli si ad dicono, come il `fly()` or `swim()` (nella realtà un cane può nuotare, ma non tutti quindi non andrebbe bene comunque).

Per risolvere questa problematica si cerca di creare interfacce più piccole e implementarle solo direttamente alle classi che ci interessa, eccone un esempio di interfaccia.

```java
interface walk {
    void walking();
}
interface fly {
    void flying();
}
interface swim {
    void swimming();
}
```

Ora, possiamo assegnare a ogni classe solo le interfacce che realmente utilizza:

```java
class Dog implements walk, swim {
    public void walking() { /* implementazione */ }
    public void swimming() { /* implementazione */ }
}

class Bird implements walk, fly {
    public void walking() { /* implementazione */ }
    public void flying() { /* implementazione */ }
}
```
## D - ependecy inversion 

>[!quote] Definition
> Il principio afferma che i **moduli di alto livello**  non dovrebbero dipendere direttamente dai **moduli di basso livello** , ma entrambi dovrebbero dipendere da astrazioni (_interfaces or abstract classes_). Inoltre, le astrazioni non devono dipendere dai dettagli concreti (**dalle implementazioni**); al contrario, sono i dettagli che devono dipendere dalle astrazioni

Ma cosa sono i moduli di alto e basso livello?

- **Low-level classes**: che sarebbero i moduli di basso livello sono tutti quelle operazioni, che intaccano il trasferimento dei dati sulla rete, operazioni sul disco oppure la connessione a una base di dati.

-  **High-level classes:** che sarebbero i moduli di alto livello, contiene della logica che riguarda ordinare di fare qualcosa alle classi di basso livello? (che vuol dire non lo so, il libro lo spiega così penso lo vedremmo dopo)
![[Pasted image 20260106094651.png| Esempio di modulo ad alto livello e di basso]]

In questo caso avremmo che la classe  `Computer` dipenderà dalla classe `Keyboard`, questo lo vediamo anche perché c'è la relazione di [[Design Pattern#4.3 Composition|composizione]].
```java
//Keyboard class  
class Keyboard {  
      
    public void type() {  
        System.out.println("Typing...");  
    }  
   
}
//Computer class  
class Computer {  
      
    // Direct dependency  
    private Keyboard keyboard = new Keyboard();   
   
    public void useKeyboard() {  
        keyboard.type();  
    }  
}
```

In questo esempio avremmo un accoppiamento elevato tra la classe `Computer` e `Keyboard`, rendendole dipendenti fra di loro. Questo perché se un giorno volessimo introdurre una nuova classe `WirelessKeyboard` o `GamingKeyboard`, dovremmo violare il principio  [[#O - pen/ closed|open-closed]] modificando la classe `Computer`. 

```java
// Esempio violazione del principio Open-Close
//Computer class  
class Computer {  
      
    // Direct dependency  
    private Keyboard keyboard = new Keyboard();   
   
    public void useKeyboard() {  
	    if(keyboard instanceof WirelessKeyboard)
	        keyboard.type();
	    else
		    keyboard.type();
    }  
}
```

Per creare l'astrazione possiamo farlo tramite le interfacce o le classi astratte, in questo esempio andremmo a definire un interfaccia, che avrà il compito di creare l'astrazione e non far dipendere i moduli sia di alto che di basso livello tra di loro, ma farli dipendere dalle astrazioni.
![[Pasted image 20260106100741.png | Esempio di applicazione del principio di inversione delle dipendenze]]

Un esempio del codice lo potrete trovare [^2]qui.

Il principio di inversione delle dipendenze ci suggerisce di lavorare prima con le classi di alto livello e poi con quelle inferiori con dei metodi che vedremmo qui:

1. Per prima cosa, si creano delle _interfacce_ per le operazioni che verranno svolte nel livello inferiore, dove però quelle di alto livello dipenderanno Ad esempio, supponiamo che la logica di business abbia bisogno di aprire un report invece di chiamare direttamente `openFile(x)`, `readBytes(n)`, `closeFile(x)`, possiamo definire un’interfaccia di alto livello con un metodo singolo chiamato `openReport(file)`, questo lo rende molto più semplice, dato che `openReport` descrive l’intento dell’operazione e non i dettagli tecnici.
2. Bisogna far **dipendere I moduli di alto livello alle astrazioni**(cioè alle interfacce che abbiamo creato),  invece di farle dipendere su **moduli di basso livello**, creando una relazione più leggera.
3. Dopo aver fatto tale operazioni, le classi di basso livello dipenderanno anche loro dalle astrazioni, invertendo la logica della direzione delle dipendenze.
> [!warning] **Perché è importante nella progettazione.** (exam question)
> 1. Nella progettazione è importante fare in modo che si possano creare dei modelli di alto livello che dipendono dalle astrazioni, in modo che si riduca l'accoppiamento dei vari componenti.
# Reference
--- 
[^1]: Example more easier to understand is there: [Liskov Sobstitution Principle](https://medium.com/@ahmedtahaelelemy/understanding-the-liskov-substitution-principle-a-deep-dive-into-solid-principles-b02ac6a18ee3)

[^2]: [Dipendecy Inversion](https://medium.com/javarevisited/mastering-dependency-inversion-in-java-58320e5143f8)
