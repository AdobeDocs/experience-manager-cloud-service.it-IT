---
title: API HTTP di Assets
description: Crea, leggi, aggiorna, elimina, gestisci risorse digitali utilizzando l’API HTTP in [!DNL Experience Manager Assets].
contentOwner: AG
feature: API HTTP di Assets, API
role: Sviluppatore,Architetto,Amministratore
exl-id: a3b7374d-f24b-4d6f-b6db-b9c9c962bb8d
translation-type: tm+mt
source-git-commit: b989833b7f1fa0c3de91f96e28a21859d97294cb
workflow-type: tm+mt
source-wordcount: '1522'
ht-degree: 1%

---

# [!DNL Adobe Experience Manager Assets] API HTTP  {#assets-http-api}

## Panoramica {#overview}

L’ API HTTP [!DNL Assets] consente operazioni di creazione-lettura-aggiornamento-eliminazione (CRUD) sulle risorse digitali, compresi i metadati, le rappresentazioni e i commenti, nonché contenuti strutturati utilizzando [!DNL Experience Manager] Frammenti di contenuto. Viene esposto in `/api/assets` e implementato come API REST. Include il supporto di [Frammenti di contenuto](/help/assets/content-fragments/assets-api-content-fragments.md).

Per accedere all’API:

1. Apri il documento del servizio API in `https://[hostname]:[port]/api.json`.
1. Segui il collegamento al servizio [!DNL Assets] che porta a `https://[hostname]:[server]/api/assets.json`.

La risposta API è un file JSON per alcuni tipi MIME e un codice di risposta per tutti i tipi MIME. La risposta JSON è facoltativa e potrebbe non essere disponibile, ad esempio per i file PDF. Per ulteriori analisi o azioni, fai riferimento al codice di risposta.

>[!NOTE]
>
>Tutte le chiamate API relative al caricamento o all’aggiornamento di risorse o file binari in generale (come le rappresentazioni) sono obsolete per [!DNL Experience Manager] come distribuzione [!DNL Cloud Service]. Per caricare i file binari, utilizza invece le API di caricamento binario diretto [a1/> .](developer-reference-material-apis.md#asset-upload-technical)

## Frammenti di contenuto {#content-fragments}

Un [Frammento di contenuto](/help/assets/content-fragments/content-fragments.md) è un tipo speciale di risorsa. Può essere utilizzato per accedere a dati strutturati, quali testi, numeri, date, tra gli altri. Poiché esistono diverse differenze tra le risorse `standard` (ad esempio immagini o documenti), per la gestione dei frammenti di contenuto si applicano alcune regole aggiuntive.

Per ulteriori informazioni, consulta [Supporto dei frammenti di contenuto in [!DNL Experience Manager Assets] API HTTP](/help/assets/content-fragments/assets-api-content-fragments.md).

## Dati, modello {#data-model}

L’ API HTTP [!DNL Assets] espone due elementi principali, cartelle e risorse (per le risorse standard). Inoltre, espone elementi più dettagliati per i modelli di dati personalizzati che descrivono contenuti strutturati in Frammenti di contenuto. Per ulteriori informazioni, consulta [Modelli di dati dei frammenti di contenuto](/help/assets/content-fragments/assets-api-content-fragments.md#content-models-and-content-fragments) .

### Cartelle {#folders}

Le cartelle sono simili alle directory dei file system tradizionali. Le cartelle possono contenere solo risorse, solo cartelle o cartelle e risorse. Le cartelle hanno i seguenti componenti:

**Entità**: Le entità di una cartella sono i relativi elementi secondari, che possono essere cartelle e risorse.

**Proprietà**:

* `name` è il nome della cartella. È lo stesso dell’ultimo segmento nel percorso URL senza estensione.
* `title` è un titolo facoltativo della cartella che può essere visualizzato al posto del suo nome.

>[!NOTE]
>
>Alcune proprietà della cartella o della risorsa sono mappate a un prefisso diverso. Il prefisso `jcr` di `jcr:title`, `jcr:description` e `jcr:language` viene sostituito con il prefisso `dc`. Quindi nei JSON restituiti, `dc:title` e `dc:description` contengono rispettivamente i valori di `jcr:title` e `jcr:description`.

**** LinksFolders mostrano tre collegamenti:

* `self`: Collega a se stesso.
* `parent`: Collega alla cartella principale.
* `thumbnail`: (Facoltativo) collega a un&#39;immagine miniatura della cartella.

### Assets {#assets}

In [!DNL Experience Manager] una risorsa contiene i seguenti elementi:

* Proprietà e metadati della risorsa.
* File binario della risorsa caricato originariamente.
* Più rappresentazioni configurate. Possono essere immagini di dimensioni diverse, video di codifiche diverse o pagine estratte da file PDF o [!DNL Adobe InDesign].
* Commenti facoltativi.

Per informazioni sugli elementi nei frammenti di contenuto, consulta [Supporto dei frammenti di contenuto in Experience Manager Assets HTTP API](/help/assets/content-fragments/assets-api-content-fragments.md).

In [!DNL Experience Manager] una cartella contiene i seguenti componenti:

* Entità: Gli elementi secondari delle risorse sono le relative rappresentazioni.
* Proprietà.
* Collegamenti.

## Funzioni disponibili {#available-features}

L&#39;API HTTP [!DNL Assets] include le seguenti funzionalità:

* [Recupera un elenco di cartelle](#retrieve-a-folder-listing).
* [Creare una cartella](#create-a-folder).
* [Creare una risorsa (obsoleto)](#create-an-asset)
* [Aggiorna binario risorsa (obsoleto)](#update-asset-binary).
* [Aggiornare i metadati delle risorse](#update-asset-metadata).
* [Crea un rendering](#create-an-asset-rendition) di una risorsa.
* [Aggiorna il rendering di una risorsa](#update-an-asset-rendition).
* [Crea un commento](#create-an-asset-comment) sulla risorsa.
* [Copia una cartella o una risorsa](#copy-a-folder-or-asset).
* [Sposta una cartella o una risorsa](#move-a-folder-or-asset).
* [Elimina una cartella, una risorsa o un rendering](#delete-a-folder-asset-or-rendition).

>[!NOTE]
>
>Per semplificare la leggibilità, gli esempi seguenti omettono le notazioni cURL complete. La notazione è correlata con [Resty](https://github.com/micha/resty) che è un wrapper di script per cURL.

<!-- TBD: The Console Manager is not available now. So how to configure the below? 

**Prerequisites**

* Go to `https://[aem_server]:[port]/system/console/configMgr`.
* Navigate to **Adobe Granite CSRF Filter**.
* Make sure the property **Filter Methods** includes: POST, PUT, DELETE.
-->

## Recupera un elenco di cartelle {#retrieve-a-folder-listing}

Recupera una rappresentazione Siren di una cartella esistente e delle relative entità secondarie (sottocartelle o risorse).

**Richiesta**:  `GET /api/assets/myFolder.json`

**Codici** di risposta: I codici di risposta sono:

* 200 - OK - successo.
* 404 - NON TROVATO - la cartella non esiste o non è accessibile.
* 500 - ERRORE SERVER INTERNO - se qualcos&#39;altro non funziona.

**Risposta**: La classe dell’entità restituita è una risorsa o una cartella. Le proprietà delle entità contenute sono un sottoinsieme dell&#39;intero insieme di proprietà di ciascuna entità. Per ottenere una rappresentazione completa dell’entità, i client devono recuperare il contenuto dell’URL indicato dal collegamento con un `rel` di `self`.

## Crea una cartella . {#create-a-folder}

Crea un elemento `sling`: `OrderedFolder` nel percorso specificato. Se viene fornito `*` al posto del nome di un nodo, il servlet utilizza il nome del parametro come nome del nodo. La richiesta accetta uno dei seguenti elementi:

* Una rappresentazione Siren della nuova cartella
* Un set di coppie nome-valore codificate come `application/www-form-urlencoded` o `multipart`/ `form`- `data`. Sono utili per creare una cartella direttamente da un modulo HTML.

Inoltre, le proprietà della cartella possono essere specificate come parametri di query URL.

Una chiamata API non riesce con un codice di risposta `500` se il nodo principale del percorso fornito non esiste. Una chiamata restituisce un codice di risposta `409` se la cartella esiste.

**Parametri**:  `name` è il nome della cartella.

**Richiesta**

* `POST /api/assets/myFolder -H"Content-Type: application/json" -d '{"class":"assetFolder","properties":{"title":"My Folder"}}'`
* `POST /api/assets/* -F"name=myfolder" -F"title=My Folder"`

**Codici** di risposta: I codici di risposta sono:

* 201 - CREATO - sulla creazione di successo.
* 409 - CONFLICT - se la cartella esiste.
* 412 - PRECONDIZIONE NON RIUSCITA - se non è possibile trovare o accedere alla raccolta radice.
* 500 - ERRORE SERVER INTERNO - se qualcos&#39;altro non funziona.

## Creare una risorsa {#create-an-asset}

Per informazioni su come creare una risorsa, consulta [Caricamento risorse](developer-reference-material-apis.md) . Non puoi creare una risorsa utilizzando l’API HTTP.

## Aggiornare il binario di una risorsa {#update-asset-binary}

Per informazioni su come aggiornare i file binari delle risorse, consulta [Caricamento risorse](developer-reference-material-apis.md) . Non è possibile aggiornare un binario di risorse utilizzando l’API HTTP.

## Aggiornare i metadati di una risorsa {#update-asset-metadata}

Aggiorna le proprietà dei metadati della risorsa. Se aggiorni una proprietà nello spazio dei nomi `dc:` , l’API aggiorna la stessa proprietà nello spazio dei nomi `jcr` . L’API non sincronizza le proprietà sotto i due namespace.

**Richiesta**:  `PUT /api/assets/myfolder/myAsset.png -H"Content-Type: application/json" -d '{"class":"asset", "properties":{"dc:title":"My Asset"}}'`

**Codici** di risposta: I codici di risposta sono:

* 200 - OK - Se Asset è stato aggiornato correttamente.
* 404 - NON TROVATO - se non è stato possibile trovare o accedere a Asset nell’URI fornito.
* 412 - PRECONDIZIONE NON RIUSCITA - se non è possibile trovare o accedere alla raccolta radice.
* 500 - ERRORE SERVER INTERNO - se qualcos&#39;altro non funziona.

## Creare un rendering delle risorse {#create-an-asset-rendition}

Crea un rendering per una risorsa. Se il nome del parametro della richiesta non viene fornito, il nome del file viene utilizzato come nome di rendering.

**Parametri**: I parametri sono  `name` per il nome del rendering e  `file` come riferimento al file.

**Richiesta**

* `POST /api/assets/myfolder/myasset.png/renditions/web-rendition -H"Content-Type: image/png" --data-binary "@myRendition.png"`
* `POST /api/assets/myfolder/myasset.png/renditions/* -F"name=web-rendition" -F"file=@myRendition.png"`

**Codici di risposta**

* 201 - CREATO - se la rappresentazione è stata creata correttamente.
* 404 - NON TROVATO - se non è stato possibile trovare o accedere a Asset nell’URI fornito.
* 412 - PRECONDIZIONE NON RIUSCITA - se non è possibile trovare o accedere alla raccolta radice.
* 500 - ERRORE SERVER INTERNO - se qualcos&#39;altro non funziona.

## Aggiornare un rendering di una risorsa {#update-an-asset-rendition}

Gli aggiornamenti sostituiscono rispettivamente il rendering di una risorsa con i nuovi dati binari.

**Richiesta**:  `PUT /api/assets/myfolder/myasset.png/renditions/myRendition.png -H"Content-Type: image/png" --data-binary @myRendition.png`

**Codici** di risposta: I codici di risposta sono:

* 200 - OK - se Rendering è stato aggiornato correttamente.
* 404 - NON TROVATO - se non è stato possibile trovare o accedere a Asset nell’URI fornito.
* 412 - PRECONDIZIONE NON RIUSCITA - se non è possibile trovare o accedere alla raccolta radice.
* 500 - ERRORE SERVER INTERNO - se qualcos&#39;altro non funziona.

## Aggiungi un commento a una risorsa {#create-an-asset-comment}

**Parametri**: I parametri sono  `message` per il corpo del messaggio del commento e  `annotationData` per i dati di annotazione in formato JSON.

**Richiesta**:  `POST /api/assets/myfolder/myasset.png/comments/* -F"message=Hello World." -F"annotationData={}"`

**Codici** di risposta: I codici di risposta sono:

* 201 - CREATO - se il Commento è stato creato correttamente.
* 404 - NON TROVATO - se non è stato possibile trovare o accedere a Asset nell’URI fornito.
* 412 - PRECONDIZIONE NON RIUSCITA - se non è possibile trovare o accedere alla raccolta radice.
* 500 - ERRORE SERVER INTERNO - se qualcos&#39;altro non funziona.

## Copiare una cartella o una risorsa {#copy-a-folder-or-asset}

Copia una cartella o una risorsa disponibile nel percorso specificato in una nuova destinazione.

**Intestazioni** richieste: I parametri sono:

* `X-Destination` - un nuovo URI di destinazione nell’ambito della soluzione API in cui copiare la risorsa.
* `X-Depth` -  `infinity` o  `0`. Utilizzando `0` viene copiata solo la risorsa e le relative proprietà e non le relative risorse figlie.
* `X-Overwrite` - Da utilizzare  `F` per impedire la sovrascrittura di una risorsa nella destinazione esistente.

**Richiesta**:  `COPY /api/assets/myFolder -H"X-Destination: /api/assets/myFolder-copy"`

**Codici** di risposta: I codici di risposta sono:

* 201 - CREATO - se la cartella/risorsa è stata copiata in una destinazione non esistente.
* 204 - NO CONTENT - Se la cartella o la risorsa è stata copiata in una destinazione esistente.
* 412 - PRECONDIZIONE NON RIUSCITA - se manca un&#39;intestazione di richiesta.
* 500 - ERRORE SERVER INTERNO - se qualcos&#39;altro non funziona.

## Spostare una cartella o una risorsa {#move-a-folder-or-asset}

Sposta una cartella o una risorsa nel percorso specificato in una nuova destinazione.

**Intestazioni** richieste: I parametri sono:

* `X-Destination` - un nuovo URI di destinazione nell’ambito della soluzione API in cui copiare la risorsa.
* `X-Depth` -  `infinity` o  `0`. Utilizzando `0` viene copiata solo la risorsa e le relative proprietà e non le relative risorse figlie.
* `X-Overwrite` - Utilizzare  `T` per eliminare forzatamente una risorsa esistente o  `F` per impedire la sovrascrittura di una risorsa esistente.

**Richiesta**:  `MOVE /api/assets/myFolder -H"X-Destination: /api/assets/myFolder-moved"`

**Codici** di risposta: I codici di risposta sono:

* 201 - CREATO - se la cartella/risorsa è stata copiata in una destinazione non esistente.
* 204 - NO CONTENT - Se la cartella o la risorsa è stata copiata in una destinazione esistente.
* 412 - PRECONDIZIONE NON RIUSCITA - se manca un&#39;intestazione di richiesta.
* 500 - ERRORE SERVER INTERNO - se qualcos&#39;altro non funziona.

## Eliminare una cartella, una risorsa o un rendering {#delete-a-folder-asset-or-rendition}

Elimina una risorsa (-tree) nel percorso specificato.

**Richiesta**

* `DELETE /api/assets/myFolder`
* `DELETE /api/assets/myFolder/myAsset.png`
* `DELETE /api/assets/myFolder/myAsset.png/renditions/original`

**Codici** di risposta: I codici di risposta sono:

* 200 - OK - Se la cartella è stata eliminata correttamente.
* 412 - PRECONDIZIONE NON RIUSCITA - se non è possibile trovare o accedere alla raccolta radice.
* 500 - ERRORE SERVER INTERNO - se qualcos&#39;altro non funziona.

## Suggerimenti, best practice e limitazioni {#tips-limitations}

* Dopo il [!UICONTROL Tempo di disattivazione], una risorsa e le relative rappresentazioni non sono disponibili tramite l’interfaccia web [!DNL Assets] e tramite l’API HTTP. L&#39;API restituisce un messaggio di errore 404 se il [!UICONTROL Al momento] è nel futuro o se il [!UICONTROL Tempo di disattivazione] è nel passato.

* L’API HTTP di Assets non restituisce i metadati completi. Gli spazi dei nomi sono codificati e vengono restituiti solo questi spazi dei nomi. Per metadati completi, vedi il percorso della risorsa `/jcr_content/metadata.json`.

* Alcune proprietà della cartella o della risorsa vengono mappate su un prefisso diverso quando vengono aggiornate utilizzando le API. Il prefisso `jcr` di `jcr:title`, `jcr:description` e `jcr:language` viene sostituito con il prefisso `dc`. Quindi nei JSON restituiti, `dc:title` e `dc:description` contengono rispettivamente i valori di `jcr:title` e `jcr:description`.

>[!MORELIKETHIS]
>
>* [Documenti di riferimento per sviluppatori per [!DNL Assets]](/help/assets/developer-reference-material-apis.md)

