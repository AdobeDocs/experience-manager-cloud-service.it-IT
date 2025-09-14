---
title: Crea integrazione API
description: Utilizza espressioni Forms adattive per aggiungere convalida, calcolo e attivazione o disattivazione automatica della visibilità di una sezione.
feature: Adaptive Forms, Foundation Components
role: User
hide: true
hidefromtoc: true
source-git-commit: 53e476981874597bfb7f9293e67b2d135c72b318
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 3%

---


# Crea integrazione API

In questa esercitazione, vengono create 2 integrazioni API

- GetAllCountries restituisce un elenco di paesi
- GetChildren - Restituire i figli diretti del paese o dello stato rappresentato dal geonameId

## GetAllCountries - Configurazione integrazione API

- Configurazione integrazione API

   - Nome visualizzato: GetAllCountries → un&#39;etichetta per questa API nel sistema.

   - URL API: `https://secure.geonames.org/countryInfoJSON` - l&#39;endpoint da chiamare.

   - Metodo HTTP: GET - stai effettuando una semplice richiesta GET.

   - Tipo di contenuto: JSON; è prevista una risposta in formato JSON.

- Opzioni:

   - Crittografia Obbligatoria deselezionata: nessun livello di crittografia oltre HTTPS.

   - Esegui al client selezionato: la chiamata viene eseguita dal client/browser, non dal lato server.
- Tipo di autenticazione
   - Nessuno: poiché l’API GeoNames non richiede le chiavi OAuth o API nelle intestazioni
- Input:
   - La sezione di input definisce ciò che viene inviato nell’API
   - **nomeutente** Tipo di →: String, inviato nella query. Impostazione predefinita: gbedekar.
   - Ogni richiesta aggiunge ?username=gbedekar all’URL
- Output
   - L’output definisce quali campi della risposta JSON devono essere estratti e utilizzati.
La risposta GeoNames si presenta così:

  ![risposta JSON](assets/geonames-data.png)
   - Mappati due campi dall’interno dell’array geonames:

     geonames[*].geonameId → come numero

     geonames[*].countryName → come stringa

     [*] significa che si ripete per ogni paese nell&#39;array.



![ottieni tutti i paesi](assets/api-integration.png)


## GetChildren

Richiede a GeoNames i figli diretti del luogo il cui geonamesId viene passato come parametro di query

- Configurazione integrazione API

   - Nome visualizzato: GetAllCountries → un&#39;etichetta per questa API nel sistema.

   - URL API: `https://secure.geonames.org/children` → l&#39;endpoint da chiamare.

   - Metodo HTTP: GET → una semplice richiesta GET.

   - Tipo di contenuto: è prevista una risposta JSON → in formato JSON.

- Opzioni:

   - Crittografia Elemento obbligatorio deselezionato → nessun livello di crittografia oltre HTTPS.

   - Esegui sul client selezionato → la chiamata viene eseguita dal client/browser, non dal lato server.
- Tipo di autenticazione
   - Nessuno: poiché l’API GeoNames non richiede le chiavi OAuth o API nelle intestazioni
- Input:
   - Definisce cosa viene inviato nell’API
   - **nomeutente** Tipo di →: String, inviato nella query. Impostazione predefinita: gbedekar.
   - Ogni richiesta aggiunge ?username=gbedekar all’URL
   - **geonameId** -> tipo: String. Restituisce gli elementi figlio del paese rappresentato dal geonameId
   - **tipo** =>Stringa. L’impostazione su json restituisce la risposta in formato JSON.
- Output
   - Definisce quali campi della risposta JSON devono essere estratti e utilizzati.
La risposta GeoNames si presenta così:

  ![risposta JSON](assets/child-elements-data.png)
   - Mappati due campi dall’interno dell’array geonames:

     geonames[*].geonameId → come numero

     geonames[*].name → come stringa

     [*] significa che si ripete per ogni paese nell&#39;array.


![get-children](assets/get-children-api-integration.png)
