START
Basic

Front: S - Principio di Responsabilità Singola (Single Responsibility Principle)

Back: Ogni classe dovrebbe avere **una sola responsabilità** o motivo per cambiare. 
Esempio: una classe ReportPrinter non dovrebbe anche generare il report — la generazione spetta a ReportGenerator.
<!--ID: 1762602405617-->
END

START
Basic

Front: O - Principio Aperto/Chiuso (Open/Closed Principle)

Back: Le classi devono essere **aperte all’estensione**, ma **chiuse alle modifiche**. 
Esempio: evita di modificare codice esistente per aggiungere nuovi comportamenti — usa l’ereditarietà o le interfacce.
<!--ID: 1762602573337-->
END 

START

Basic

Front: L - Principio di Sostituzione di Liskov (Liskov Substitution Principle)

Back: Le sottoclassi devono poter sostituire le super classi **senza alterare il comportamento del programma**.

Esempio: se una sottoclasse cambia il significato di un metodo ereditato, viola il principio.
<!--ID: 1762602756491-->
END

START

Basic

Front: I - Principio di Segregazione delle Interfacce (Interface Segregation Principle)

Back: Meglio avere **interfacce piccole e specifiche** piuttosto che una grande interfaccia generica.

Esempio: evita di costringere le classi ad implementare metodi che non usano.
<!--ID: 1762602756494-->
END

START
Basic

Front: D - Principio di Inversione delle Dipendenze (Dependency Inversion Principle)

Back: Le classi dovrebbero dipendere da **astrazioni**, non da **implementazioni**.

Le alte e basse gerarchie devono essere indipendenti tra loro.
<!--ID: 1762602800993-->
END

TARGET DECK:  SOLID PRINCIPLE