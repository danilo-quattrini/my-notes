1. Che cos'è una funzione in C?
La funzione in C è una porzione di codice (pezzo di codice) che possiamo utilizzare nel nostro **main**, per eseguire calcoli. 

2. Differenza tra dichiarazione e definizione?
La prima consiste nel dichiarare l'esista di una funzione dentro al codice, senza **implementarla**, la seconda invece verrà **implementata** con i suoi calcoli.

3. Sintassi di una funzione in C?
<*tipo_funzione*> <*nome_funzione*> (<**tipo_parametro**><**parametro**>,...)

4. Cosa succede se non passiamo tutti i parametri di una funzione?
Da errore perché la funzione ha bisogno di tutti i parametri che dichiariamo.

5. Cosa rappresenta un "parametro", come vengono passati?
Il parametro viene inteso come quella variabile che passiamo ad una funzione e vengono passati/inseriti dentro alle funzioni che dichiariamo nel main, ad esempio:

nome_funzione(parametro1,parametro2);

6. Cosa succede se una funzione dichiarata come ad esempio (int,float,double, ecc..), non ritorna nessun valore?
   
   Non viene dichiarato nessun valore e quindi non si può salvare il suo risultato.
   
   
7. Che cos'è un prototipo di una funzione?
   Dichiarazione di una funzione a inizio codice, ad esempio:
   
    int differenza(int,int);
   void differenza2(int*,int,int);
  
