Tag: [[Software Engineering]]

   >[!info] **What is the purpose of the system?**
   >Permetta la gestione, valorizzazione e tracciabilità dei prodotti agricoli di un territorio comunale.
   >

Abbiamo svolto un'analisi di cosa il testo ci andava a chiedere.
- # Piattaforma (Sistema/Marketplace)
  La piattaforma conterrà e farà:
	- ## Dati della ==filiera agricola== potrà (cosa  il sistema può far fare all'utente)
		- Caricare (Informazioni della filiera agricola)
		- Visualizzare (Mostrare la filiera sul sito)
		- Condividere informazioni su quest'ultimi (funzione per condivider sulle piattaforme social?)  
		- ### Dati dei prodotti:
			- Produzione 
			- Trasformazione
			- Vendita dei prodotti locali 
			  
	- ## Promozione del territorio ??
		- #### Prodotti tipico 
			- Provenienza del prodotto
			- Qualità del prodotto
			  
	- ## Organizzazione di eventi locali
		- Fiere
		- Visite guidate
		  
	- ## Tracciare il prodotto
		- Visualizzare intero ciclo produttivo (cioè com'è stato creato il prodotto dalla nascita fino ad ora)
		  
	- ### Informazioni e contenuti 
		- Verranno caricati dalle singole aziende agricole o mercati del territorio comunale 
		- #### Informazioni che possono caricare
			- Certificazioni 
			- Metodo di coltivazione
			- Pratiche di produzione
			  
	- ## Visualizzare sulla mappa "interattiva" i punti della filiera

Analizziamo ora gli attori che sono presenti nel nostro marketplace/sistema.
## Produttore
- *Caricare* informazioni sul proprio prodotto
- **Vendere** nel marketplace
## Trasformatore
- *Caricare* informazioni sui processi di trasformazione
- *Caricare* certificazioni di qualità 
- **Vendere** nel marketplace


# Commits notes

[update] **Title**
Date: 2025-04-10
-  creato relazione tra evento e utente generico, dove solo chi è presente in partecipanti di evento può partecipate.
- animatore può invitare `Trasformatore`, `Produttore` e `Distributore di tipicità`.
- aggiunti attributi su `Produttore`, come dati di produzione, certificazioni e metodi di coltivazione
- aggiunti attributi su `Trasformatore` certificazioni e trasformazioni.
- aggiunto che `Acquirente` può prenotare l'evento che viene creato dall'`Animatore`
- revisionare `Contenuto` e vedre attributi se servon `UserID` e `EventID`.
- togliere da documento nel capitolo Verbo nella sezione `Caricare` l'attributo `disponibilità`.
- Creata dipendenza da `Contenuto` a `Prodotto`, cioè se il prodotto viene approvato allora il contenuto cambia, quindi abbiamo messo la relazione di esistenza.
- Cambiato verbo dell'entità `Animatore della filiera` da `creare` a `organizzare`
- Creato interfaccia come classe di associazione tra `Contenuto` e `Condividere`, che quest'ultimo è tra `Contenuto` e la interfaccia esterna che abbiamo creato(da metter come «external») chiamata `«interface» SocialSystem (ext)`.

