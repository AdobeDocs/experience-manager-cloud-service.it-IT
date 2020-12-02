---
title: API HTTP di Assets
description: Creazione, lettura, aggiornamento, eliminazione, gestione di risorse digitali tramite l'API HTTP in [!DNL Adobe Experience Manager Assets].
contentOwner: AG
translation-type: tm+mt
source-git-commit: 5be8ab734306ad1442804b3f030a56be1d3b5dfa
workflow-type: tm+mt
source-wordcount: '1473'
ht-degree: 1%

---


# API HTTP di Assets {#assets-http-api}

## Panoramica {#overview}

L&#39;API HTTP Assets consente di creare-leggere-aggiornare-eliminare (CRUD) le operazioni sulle risorse digitali, inclusi i metadati, le rappresentazioni e i commenti, nonché il contenuto strutturato utilizzando [!DNL Experience Manager] Frammenti di contenuto. È esposto in `/api/assets` e viene implementato come REST API. Include il supporto di [frammenti di contenuto](/help/assets/content-fragments/assets-api-content-fragments.md).

Per accedere all&#39;API:

1. Aprite il documento del servizio API in `https://[hostname]:[port]/api.json`.
1. Segui il collegamento del servizio Risorse fino a `https://[hostname]:[server]/api/assets.json`.

La risposta API è un file JSON per alcuni tipi MIME e un codice di risposta per tutti i tipi MIME. La risposta JSON è facoltativa e potrebbe non essere disponibile, ad esempio per i file PDF. Per ulteriori analisi o azioni, fai affidamento sul codice di risposta.

Dopo la [!UICONTROL Ora di disattivazione], una risorsa e le relative rappresentazioni non sono disponibili tramite l&#39;interfaccia Web [!DNL Assets] e tramite l&#39;API HTTP. L&#39;API restituisce un messaggio di errore 404 se il [!UICONTROL Tempo di attivazione] è in futuro o se il [!UICONTROL Tempo di disattivazione] è passato.

>[!NOTE]
>
>Tutte le chiamate API relative al caricamento o all&#39;aggiornamento di risorse o file binari in generale (come le rappresentazioni) sono AEM come una distribuzione [!DNL Cloud Service]. Per caricare i file binari, utilizzate le API di caricamento binario diretto [API](developer-reference-material-apis.md#asset-upload-technical).

## Frammenti di contenuto {#content-fragments}

Un [frammento di contenuto](/help/assets/content-fragments/content-fragments.md) è un tipo speciale di risorsa. Può essere utilizzato per accedere a dati strutturati, come testi, numeri, date, ecc. Poiché le risorse `standard` sono diverse (ad esempio immagini o documenti), per la gestione dei frammenti di contenuto si applicano alcune regole aggiuntive.

Per ulteriori informazioni, consultate [Supporto per frammenti di contenuto nell&#39;API HTTP delle risorse del Experience Manager ](/help/assets/content-fragments/assets-api-content-fragments.md).

## Dati, modello {#data-model}

L’API HTTP Assets espone due elementi principali, cartelle e risorse (per le risorse standard).

Inoltre, espone elementi più dettagliati per i modelli di dati personalizzati che descrivono il contenuto strutturato nei frammenti di contenuto. Per ulteriori informazioni, vedere [Modelli di dati dei frammenti di contenuto](/help/assets/content-fragments/assets-api-content-fragments.md#content-models-and-content-fragments).

### Cartelle {#folders}

Le cartelle sono come directory nei file system tradizionali. Sono contenitori per altre cartelle o asserzioni. Le cartelle hanno i seguenti componenti:

**Entità**: Le entità di una cartella sono gli elementi secondari, che possono essere cartelle e risorse.

**Proprietà**:

* `name` è il nome della cartella. Equivale all’ultimo segmento nel percorso dell’URL senza estensione.
* `title` è un titolo facoltativo della cartella che può essere visualizzato al posto del nome.

>[!NOTE]
>
>Alcune proprietà della cartella o della risorsa vengono mappate con un prefisso diverso. Il prefisso `jcr` di `jcr:title`, `jcr:description` e `jcr:language` viene sostituito con il prefisso `dc`. Di conseguenza, nelle JSON restituite, `dc:title` e `dc:description` contengono rispettivamente i valori di `jcr:title` e `jcr:description`.

**I collegamenti** LinksFolders presentano tre collegamenti:

* `self`: Collegarsi a se stesso.
* `parent`: Collegare la cartella principale.
* `thumbnail`: (Facoltativo) collegamento alla miniatura di una cartella.

### Assets {#assets}

In [!DNL Experience Manager] una risorsa contiene i seguenti elementi:

* Proprietà e metadati della risorsa.
* Rappresentazioni multiple, ad esempio la rappresentazione originale (che è la risorsa caricata originariamente), una miniatura e varie altre rappresentazioni. Rappresentazioni aggiuntive possono essere immagini di dimensioni diverse, codifiche video diverse o pagine estratte da file PDF o  Adobe InDesign.
* Commenti facoltativi.

Per informazioni sugli elementi nei frammenti di contenuto, consultate [Supporto dei frammenti di contenuto in  API HTTP delle risorse di Experience Manager](/help/assets/content-fragments/assets-api-content-fragments.md).

In [!DNL Experience Manager] una cartella contiene i seguenti componenti:

* Entità: Gli elementi secondari delle risorse sono le relative rappresentazioni.
* Proprietà.
* Collegamenti.

## Funzioni disponibili {#available-features}

L&#39;API HTTP Assets include le seguenti funzionalità:

* Recuperate un elenco di cartelle.
* Creare una cartella.
* Creare una risorsa (obsoleto).
* Aggiorna binario risorsa (obsoleto).
* Aggiornare i metadati delle risorse.
* Creare una rappresentazione di una risorsa.
* Aggiornare una rappresentazione di una risorsa.
* Create un commento sulla risorsa.
* Copiate una cartella o una risorsa.
* Spostate una cartella o una risorsa.
* Eliminate una cartella, una risorsa o una rappresentazione.

>[!NOTE]
>
>Per semplificare la leggibilità, gli esempi seguenti omettono la notazione cURL completa. In realtà la notazione è correlata con [Resty](https://github.com/micha/resty) che è un wrapper di script per `cURL`.

<!-- TBD: The Console Manager is not available now. So how to configure the below? 

**Prerequisites**

* Go to `https://[aem_server]:[port]/system/console/configMgr`.
* Navigate to **Adobe Granite CSRF Filter**.
* Make sure the property **Filter Methods** includes: POST, PUT, DELETE.
-->

## Recuperare una cartella che elenca {#retrieve-a-folder-listing}

Recupera una rappresentazione Siren di una cartella esistente e delle relative entità figlie (sottocartelle o risorse).

**Richiesta**:  `GET /api/assets/myFolder.json`

**Codici** di risposta: I codici di risposta sono:

* 200 - Ok - successo.
* 404 - NON TROVATO - la cartella non esiste o non è accessibile.
* 500 - ERRORE SERVER INTERNO - se qualcos&#39;altro va storto.

**Risposta**: La classe dell&#39;entità restituita è una risorsa o una cartella. Le proprietà delle entità contenute sono un sottoinsieme dell&#39;intero insieme di proprietà di ciascuna entità. Per ottenere una rappresentazione completa dell&#39;entità, i client devono recuperare il contenuto dell&#39;URL indicato dal collegamento con un `rel` di `self`.

## Crea una cartella . {#create-a-folder}

Crea un nuovo elemento `sling`: `OrderedFolder` nel percorso specificato. Se viene fornito un `*` al posto del nome di un nodo, il servlet utilizza il nome del parametro come nome del nodo. Accettati come dati di richiesta è una rappresentazione Siren della nuova cartella o un set di coppie nome-valore, codificati come `application/www-form-urlencoded` o `multipart`/ `form`- `data`, utili per creare una cartella direttamente da un modulo HTML. Inoltre, le proprietà della cartella possono essere specificate come parametri di query URL.

Una chiamata API non riesce con un codice di risposta `500` se il nodo padre del percorso fornito non esiste. Una chiamata restituisce un codice di risposta `409` se la cartella esiste già.

**Parametri**:  `name` è il nome della cartella.

**Richiesta**

* `POST /api/assets/myFolder -H"Content-Type: application/json" -d '{"class":"assetFolder","properties":{"title":"My Folder"}}'`
* `POST /api/assets/* -F"name=myfolder" -F"title=My Folder"`

**Codici** di risposta: I codici di risposta sono:

* 201 - CREATO - sulla creazione di successo.
* 409 - CONFLICT - se la cartella esiste già.
* 412 - PRECONDIZIONE NON RIUSCITA - se non è possibile trovare o accedere alla raccolta radice.
* 500 - ERRORE SERVER INTERNO - se qualcos&#39;altro va storto.

## Creare una risorsa {#create-an-asset}

Consultate [caricamento delle risorse](developer-reference-material-apis.md) per informazioni su come creare una risorsa mediante le API. La creazione di una risorsa tramite l’API HTTP è obsoleta.

## Aggiornare il binario di una risorsa {#update-asset-binary}

Consultate [caricamento delle risorse](developer-reference-material-apis.md) per informazioni su come aggiornare i file binari delle risorse mediante le API. L&#39;aggiornamento di un binario di risorse tramite l&#39;API HTTP è obsoleto.

## Aggiornare i metadati di una risorsa {#update-asset-metadata}

Aggiorna le proprietà dei metadati della risorsa. Se si aggiorna una qualsiasi proprietà nello spazio dei nomi `dc:`, l&#39;API aggiorna la stessa proprietà nello spazio dei nomi `jcr`. L&#39;API non sincronizza le proprietà sotto i due spazi dei nomi.

**Richiesta**:  `PUT /api/assets/myfolder/myAsset.png -H"Content-Type: application/json" -d '{"class":"asset", "properties":{"dc:title":"My Asset"}}'`

**Codici** di risposta: I codici di risposta sono:

* 200 - OK - se la risorsa è stata aggiornata correttamente.
* 404 - NON TROVATO - se la risorsa non è stata trovata o a cui non è stato possibile accedere all&#39;URI fornito.
* 412 - PRECONDIZIONE NON RIUSCITA - se non è possibile trovare o accedere alla raccolta radice.
* 500 - ERRORE SERVER INTERNO - se qualcos&#39;altro va storto.

## Creare una rappresentazione di risorsa {#create-an-asset-rendition}

Create una nuova rappresentazione di risorsa per una risorsa. Se il nome del parametro della richiesta non viene fornito, il nome del file viene utilizzato come nome di rappresentazione.

**Parametri**: I parametri sono  `name` per il nome della rappresentazione e  `file` come riferimento del file.

**Richiesta**

* `POST /api/assets/myfolder/myasset.png/renditions/web-rendition -H"Content-Type: image/png" --data-binary "@myRendition.png"`
* `POST /api/assets/myfolder/myasset.png/renditions/* -F"name=web-rendition" -F"file=@myRendition.png"`

**Codici di risposta**

* 201 - CREATO - se la rappresentazione è stata creata correttamente.
* 404 - NON TROVATO - se la risorsa non è stata trovata o a cui non è stato possibile accedere all&#39;URI fornito.
* 412 - PRECONDIZIONE NON RIUSCITA - se non è possibile trovare o accedere alla raccolta radice.
* 500 - ERRORE SERVER INTERNO - se qualcos&#39;altro va storto.

## Aggiornare una rappresentazione di una risorsa {#update-an-asset-rendition}

Gli aggiornamenti sostituiscono rispettivamente una rappresentazione di risorsa con i nuovi dati binari.

**Richiesta**:  `PUT /api/assets/myfolder/myasset.png/renditions/myRendition.png -H"Content-Type: image/png" --data-binary @myRendition.png`

**Codici** di risposta: I codici di risposta sono:

* 200 - OK - se la rappresentazione è stata aggiornata correttamente.
* 404 - NON TROVATO - se la risorsa non è stata trovata o a cui non è stato possibile accedere all&#39;URI fornito.
* 412 - PRECONDIZIONE NON RIUSCITA - se non è possibile trovare o accedere alla raccolta radice.
* 500 - ERRORE SERVER INTERNO - se qualcos&#39;altro va storto.

## Aggiungere un commento a una risorsa {#create-an-asset-comment}

Crea un nuovo commento sulla risorsa.

**Parametri**: I parametri sono  `message` per il corpo del messaggio del commento e  `annotationData` per i dati di annotazione in formato JSON.

**Richiesta**:  `POST /api/assets/myfolder/myasset.png/comments/* -F"message=Hello World." -F"annotationData={}"`

**Codici** di risposta: I codici di risposta sono:

* 201 - CREATO - se il commento è stato creato correttamente.
* 404 - NON TROVATO - se la risorsa non è stata trovata o a cui non è stato possibile accedere all&#39;URI fornito.
* 412 - PRECONDIZIONE NON RIUSCITA - se non è possibile trovare o accedere alla raccolta radice.
* 500 - ERRORE SERVER INTERNO - se qualcos&#39;altro va storto.

## Copiare una cartella o una risorsa {#copy-a-folder-or-asset}

Copia una cartella o una risorsa disponibile nel percorso fornito in una nuova destinazione.

**Richiedi intestazioni**: I parametri sono:

* `X-Destination` - un nuovo URI di destinazione nell&#39;ambito della soluzione API in cui copiare la risorsa.
* `X-Depth` -  `infinity` o  `0`. Utilizzando `0` vengono copiate solo la risorsa e le relative proprietà e non le relative risorse figlie.
* `X-Overwrite` - Consente  `F` di evitare la sovrascrittura di una risorsa nella destinazione esistente.

**Richiesta**:  `COPY /api/assets/myFolder -H"X-Destination: /api/assets/myFolder-copy"`

**Codici** di risposta: I codici di risposta sono:

* 201 - CREATO - se la cartella/risorsa è stata copiata in una destinazione non esistente.
* 204 - NESSUN CONTENUTO - se la cartella o la risorsa è stata copiata in una destinazione esistente.
* 412 - PRECONDIZIONE NON RIUSCITA - se manca un&#39;intestazione di richiesta.
* 500 - ERRORE SERVER INTERNO - se qualcos&#39;altro va storto.

## Spostare una cartella o una risorsa {#move-a-folder-or-asset}

Sposta una cartella o una risorsa nel percorso specificato in una nuova destinazione.

**Richiedi intestazioni**: I parametri sono:

* `X-Destination` - un nuovo URI di destinazione nell&#39;ambito della soluzione API in cui copiare la risorsa.
* `X-Depth` -  `infinity` o  `0`. Utilizzando `0` vengono copiate solo la risorsa e le relative proprietà e non le relative risorse figlie.
* `X-Overwrite` - Utilizzare  `T` per forzare l&#39;eliminazione di una risorsa esistente o  `F` per impedire la sovrascrittura di una risorsa esistente.

**Richiesta**:  `MOVE /api/assets/myFolder -H"X-Destination: /api/assets/myFolder-moved"`

**Codici** di risposta: I codici di risposta sono:

* 201 - CREATO - se la cartella/risorsa è stata copiata in una destinazione non esistente.
* 204 - NESSUN CONTENUTO - se la cartella o la risorsa è stata copiata in una destinazione esistente.
* 412 - PRECONDIZIONE NON RIUSCITA - se manca un&#39;intestazione di richiesta.
* 500 - ERRORE SERVER INTERNO - se qualcos&#39;altro va storto.

## Eliminare una cartella, una risorsa o un rendering {#delete-a-folder-asset-or-rendition}

Elimina una risorsa (-tree) nel percorso specificato.

**Richiesta**

* `DELETE /api/assets/myFolder`
* `DELETE /api/assets/myFolder/myAsset.png`
* `DELETE /api/assets/myFolder/myAsset.png/renditions/original`

**Codici** di risposta: I codici di risposta sono:

* 200 - OK - Se la cartella è stata eliminata correttamente.
* 412 - PRECONDIZIONE NON RIUSCITA - se non è possibile trovare o accedere alla raccolta radice.
* 500 - ERRORE SERVER INTERNO - se qualcos&#39;altro va storto.
