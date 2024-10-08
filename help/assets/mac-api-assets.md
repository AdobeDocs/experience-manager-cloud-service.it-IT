---
title: API HTTP di Assets
description: Crea, leggi, aggiorna, elimina, gestisci le risorse digitali tramite API HTTP in [!DNL Experience Manager Assets].
contentOwner: AG
feature: Assets HTTP API
role: Developer, Architect, Admin
exl-id: a3b7374d-f24b-4d6f-b6db-b9c9c962bb8d
source-git-commit: e3fd0fe2ee5bad2863812ede2a294dd63864f3e2
workflow-type: tm+mt
source-wordcount: '1695'
ht-degree: 6%

---

# API HTTP [!DNL Adobe Experience Manager Assets] {#assets-http-api}

| [Best practice per la ricerca](/help/assets/search-best-practices.md) | [Best practice per i metadati](/help/assets/metadata-best-practices.md) | [Hub di contenuti](/help/assets/product-overview.md) | [Dynamic Medie con funzionalità OpenAPI](/help/assets/dynamic-media-open-apis-overview.md) | [Documentazione per gli sviluppatori di AEM Assets](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-65/assets/extending/mac-api-assets.html?lang=en) |
| AEM as a Cloud Service | Questo articolo |

## Panoramica {#overview}

L&#39;API HTTP [!DNL Assets] consente operazioni di creazione-lettura-aggiornamento-eliminazione (CRUD) sulle risorse digitali, inclusi i metadati, sulle rappresentazioni e sui commenti, insieme a contenuti strutturati che utilizzano [!DNL Experience Manager] frammenti di contenuto. È esposto in `/api/assets` ed è implementato come API REST. Include [supporto per frammenti di contenuto](/help/assets/content-fragments/assets-api-content-fragments.md).

>[!NOTE]
>
> È disponibile un’implementazione OpenAPI modernizzata dell’API di gestione dei frammenti di contenuto. Per la documentazione completa, consulta [API di gestione dei frammenti di contenuto](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/sites/). Si consiglia di utilizzare la nuova implementazione OpenAPI. L’utilizzo esistente dell’API HTTP di Assets per i frammenti di contenuto deve essere migrato alla nuova OpenAPI di gestione dei frammenti di contenuto.

Per accedere all’API:

1. Aprire il documento del servizio API in `https://[hostname]:[port]/api.json`.
1. Segui il collegamento al servizio [!DNL Assets] che porta a `https://[hostname]:[server]/api/assets.json`.

La risposta API è un file JSON per alcuni tipi MIME e un codice di risposta per tutti i tipi MIME. La risposta JSON è facoltativa e potrebbe non essere disponibile, ad esempio, per i file PDF. Utilizza il codice di risposta per ulteriori analisi o azioni.

>[!NOTE]
>
>Tutte le chiamate API relative al caricamento o all&#39;aggiornamento di risorse o dati binari in generale (come le rappresentazioni) sono obsolete per [!DNL Experience Manager] come distribuzione di [!DNL Cloud Service]. Per il caricamento dei file binari, utilizza invece [API di caricamento binario diretto](developer-reference-material-apis.md#asset-upload).

## Frammenti di contenuto {#content-fragments}

Un [frammento di contenuto](/help/assets/content-fragments/content-fragments.md) è un tipo speciale di risorsa. Può essere utilizzato per accedere a dati strutturati, ad esempio testi, numeri, date e così via. Poiché esistono diverse differenze per `standard` risorse (come immagini o documenti), alcune regole aggiuntive si applicano alla gestione dei frammenti di contenuto.

Per ulteriori informazioni, vedere il supporto per [Frammenti di contenuto nell&#39; [!DNL Experience Manager Assets] API HTTP](/help/assets/content-fragments/assets-api-content-fragments.md).

>[!NOTE]
>
>Sono disponibili anche [OpenAPI per frammenti di contenuto e modelli di frammenti di contenuto](/help/headless/content-fragment-openapis.md).

## Modello dati {#data-model}

L&#39;API HTTP [!DNL Assets] espone due elementi principali, cartelle e risorse (per le risorse standard). Inoltre, espone elementi più dettagliati per i modelli di dati personalizzati che descrivono i contenuti strutturati nei frammenti di contenuto. Per ulteriori informazioni, consulta [Modelli dati per frammenti di contenuto](/help/assets/content-fragments/assets-api-content-fragments.md#content-models-and-content-fragments).

>[!NOTE]
>
>Sono disponibili anche [OpenAPI per frammenti di contenuto e modelli di frammenti di contenuto](/help/headless/content-fragment-openapis.md).

### Cartelle {#folders}

Le cartelle sono simili alle directory dei file system tradizionali. La cartella può contenere solo risorse, solo cartelle o cartelle e risorse. Le cartelle hanno i seguenti componenti:

**Entità**: le entità di una cartella sono i relativi elementi secondari, che possono essere cartelle e risorse.

**Proprietà**:

* `name` è il nome della cartella. È lo stesso dell’ultimo segmento nel percorso URL senza estensione.
* `title` è un titolo facoltativo della cartella che può essere visualizzato al posto del nome.

>[!NOTE]
>
>Alcune proprietà della cartella o della risorsa sono mappate a un prefisso diverso. Il prefisso `jcr` di `jcr:title`, `jcr:description` e `jcr:language` viene sostituito con il prefisso `dc`. Pertanto, nel JSON restituito, `dc:title` e `dc:description` contengono rispettivamente i valori di `jcr:title` e `jcr:description`.

**I collegamenti** nelle cartelle espongono tre collegamenti:

* `self`: collegamento a se stesso.
* `parent`: collegamento alla cartella principale.
* `thumbnail`: (facoltativo) collegamento a un&#39;immagine di miniatura della cartella.

### Risorse {#assets}

In [!DNL Experience Manager] una risorsa contiene i seguenti elementi:

* Proprietà e metadati della risorsa.
* File binario della risorsa caricato originariamente.
* Più rappresentazioni configurate. Possono essere immagini di diverse dimensioni, video di diverse codifiche o pagine estratte da file PDF o [!DNL Adobe InDesign].
* Commenti facoltativi.

Per informazioni sugli elementi nei frammenti di contenuto, vedere [Supporto dei frammenti di contenuto nell&#39;API HTTP Experience Manager Assets](/help/assets/content-fragments/assets-api-content-fragments.md).

>[!NOTE]
>
>Sono disponibili anche [OpenAPI per frammenti di contenuto e modelli di frammenti di contenuto](/help/headless/content-fragment-openapis.md).

In [!DNL Experience Manager] una cartella contiene i seguenti componenti:

* Entità: i figli delle risorse ne sono le rappresentazioni.
* Proprietà.
* Collegamenti.

## Funzioni disponibili {#available-features}

L&#39;API HTTP [!DNL Assets] include le seguenti funzionalità:

* [Recuperare un elenco di cartelle](#retrieve-a-folder-listing).
* [Creare una cartella](#create-a-folder).
* [Creare una risorsa (obsoleto)](#create-an-asset)
* [Aggiorna binario risorsa (obsoleto)](#update-asset-binary).
* [Aggiorna metadati risorsa](#update-asset-metadata).
* [Crea una rappresentazione di una risorsa](#create-an-asset-rendition).
* [Aggiorna una rappresentazione di risorsa](#update-an-asset-rendition).
* [Crea un commento risorsa](#create-an-asset-comment).
* [Copia una cartella o una risorsa](#copy-a-folder-or-asset).
* [Spostare una cartella o una risorsa](#move-a-folder-or-asset).
* [Eliminare una cartella, una risorsa o una copia trasformata](#delete-a-folder-asset-or-rendition).

>[!NOTE]
>
>Per maggiore leggibilità, gli esempi seguenti omettono le notazioni cURL complete. La notazione è correlata con [Resty](https://github.com/micha/resty) che è un wrapper di script per cURL.

<!-- TBD: The Console Manager is not available now. So how to configure the below? 

**Prerequisites**

* Go to `https://[aem_server]:[port]/system/console/configMgr`.
* Navigate to **Adobe Granite CSRF Filter**.
* Make sure the property **Filter Methods** includes: POST, PUT, DELETE.
-->

## Recuperare un elenco di cartelle {#retrieve-a-folder-listing}

Recupera una rappresentazione Siren di una cartella esistente e delle relative entità secondarie (sottocartelle o risorse).

**Richiesta**: `GET /api/assets/myFolder.json`

**Codici di risposta**: I codici di risposta sono:

* 200 - OK - operazione riuscita.
* 404 - NON TROVATO - la cartella non esiste o non è accessibile.
* 500 - ERRORE INTERNO DEL SERVER - se si verificano altri errori.

**Risposta**: la classe dell&#39;entità restituita è una risorsa o una cartella. Le proprietà delle entità contenute sono un sottoinsieme dell&#39;insieme completo di proprietà di ciascuna entità. Per ottenere una rappresentazione completa dell&#39;entità, i client devono recuperare il contenuto dell&#39;URL indicato dal collegamento con `rel` di `self`.

## Crea una cartella {#create-a-folder}

Crea un `sling`: `OrderedFolder` nel percorso specificato. Se viene fornito `*` invece del nome di un nodo, il servlet utilizza il nome del parametro come nome di nodo. La richiesta accetta uno dei seguenti elementi:

* Una rappresentazione Siren della nuova cartella
* Un set di coppie nome-valore, codificate come `application/www-form-urlencoded` o `multipart`/ `form`- `data`. Questi sono utili per creare una cartella direttamente da un modulo HTML.

Inoltre, le proprietà della cartella possono essere specificate come parametri di query URL.

Una chiamata API non riesce con un codice di risposta `500` se il nodo principale del percorso specificato non esiste. Una chiamata restituisce un codice di risposta `409` se la cartella esiste.

**Parametri**: `name` è il nome della cartella.

**Richiesta**

* `POST /api/assets/myFolder -H"Content-Type: application/json" -d '{"class":"assetFolder","properties":{"title":"My Folder"}}'`
* `POST /api/assets/* -F"name=myfolder" -F"title=My Folder"`

**Codici di risposta**: I codici di risposta sono:

* 201 - CREATO - su creazione riuscita.
* 409 - CONFLITTO - se la cartella esiste.
* 412 - PRECONDIZIONE NON RIUSCITA - se non è possibile trovare o accedere alla raccolta radice.
* 500 - ERRORE INTERNO DEL SERVER - se si verificano altri errori.

## Creare una risorsa {#create-an-asset}

Consulta [caricamento risorse](developer-reference-material-apis.md) per informazioni su come creare una risorsa. Non è possibile creare una risorsa utilizzando l’API HTTP.

## Aggiornare un binario di risorse {#update-asset-binary}

Consulta [caricamento risorse](developer-reference-material-apis.md) per informazioni su come aggiornare i file binari delle risorse. Non è possibile aggiornare un binario di risorse utilizzando l’API HTTP.

## Aggiornare i metadati di una risorsa {#update-asset-metadata}

Aggiorna le proprietà dei metadati della risorsa. Se si aggiorna una proprietà nello spazio dei nomi `dc:`, l&#39;API aggiorna la stessa proprietà nello spazio dei nomi `jcr`. L’API non sincronizza le proprietà nei due spazi dei nomi.

**Richiesta**: `PUT /api/assets/myfolder/myAsset.png -H"Content-Type: application/json" -d '{"class":"asset", "properties":{"dc:title":"My Asset"}}'`

**Codici di risposta**: I codici di risposta sono:

* 200 - OK - se la risorsa è stata aggiornata correttamente.
* 404 - NON TROVATO - se la risorsa non è stata trovata o non è stato possibile accedervi all’URI specificato.
* 412 - PRECONDIZIONE NON RIUSCITA - se non è possibile trovare o accedere alla raccolta radice.
* 500 - ERRORE INTERNO DEL SERVER - se si verificano altri errori.

## Creare una rappresentazione di una risorsa {#create-an-asset-rendition}

Crea una rappresentazione per una risorsa. Se non viene fornito il nome del parametro della richiesta, il nome del file viene utilizzato come nome della rappresentazione.

**Parametri**: i parametri sono `name` per il nome della rappresentazione e `file` come riferimento di file.

**Richiesta**

* `POST /api/assets/myfolder/myasset.png/renditions/web-rendition -H"Content-Type: image/png" --data-binary "@myRendition.png"`
* `POST /api/assets/myfolder/myasset.png/renditions/* -F"name=web-rendition" -F"file=@myRendition.png"`

**Codici di risposta**

* 201 - CREATO - se la rappresentazione è stata creata correttamente.
* 404 - NON TROVATO - se la risorsa non è stata trovata o non è stato possibile accedervi all’URI specificato.
* 412 - PRECONDIZIONE NON RIUSCITA - se non è possibile trovare o accedere alla raccolta radice.
* 500 - ERRORE INTERNO DEL SERVER - se si verificano altri errori.

## Aggiornare il rendering di una risorsa {#update-an-asset-rendition}

Gli aggiornamenti sostituiscono rispettivamente una rappresentazione di una risorsa con i nuovi dati binari.

**Richiesta**: `PUT /api/assets/myfolder/myasset.png/renditions/myRendition.png -H"Content-Type: image/png" --data-binary @myRendition.png`

**Codici di risposta**: I codici di risposta sono:

* 200 - OK - se la rappresentazione è stata aggiornata correttamente.
* 404 - NON TROVATO - se la risorsa non è stata trovata o non è stato possibile accedervi all’URI specificato.
* 412 - PRECONDIZIONE NON RIUSCITA - se non è possibile trovare o accedere alla raccolta radice.
* 500 - ERRORE INTERNO DEL SERVER - se si verificano altri errori.

## Aggiungere un commento a una risorsa {#create-an-asset-comment}

**Parametri**: i parametri sono `message` per il corpo del messaggio del commento e `annotationData` per i dati di annotazione in formato JSON.

**Richiesta**: `POST /api/assets/myfolder/myasset.png/comments/* -F"message=Hello World." -F"annotationData={}"`

**Codici di risposta**: I codici di risposta sono:

* 201 - CREATO - se il commento è stato creato correttamente.
* 404 - NON TROVATO - se la risorsa non è stata trovata o non è stato possibile accedervi all’URI specificato.
* 412 - PRECONDIZIONE NON RIUSCITA - se non è possibile trovare o accedere alla raccolta radice.
* 500 - ERRORE INTERNO DEL SERVER - se si verificano altri errori.

## Copiare una cartella o una risorsa {#copy-a-folder-or-asset}

Copia in una nuova destinazione una cartella o una risorsa disponibile nel percorso specificato.

**Intestazioni richiesta**: i parametri sono:

* `X-Destination` - Nuovo URI di destinazione nell&#39;ambito della soluzione API in cui copiare la risorsa.
* `X-Depth` - `infinity` o `0`. Se si utilizza `0`, verranno copiate solo la risorsa e le relative proprietà e non i relativi elementi figlio.
* `X-Overwrite` - Utilizzare `F` per impedire la sovrascrittura di una risorsa nella destinazione esistente.

**Richiesta**: `COPY /api/assets/myFolder -H"X-Destination: /api/assets/myFolder-copy"`

**Codici di risposta**: I codici di risposta sono:

* 201 - CREATO - se la cartella/risorsa è stata copiata in una destinazione non esistente.
* 204 - NESSUN CONTENUTO - se la cartella/risorsa è stata copiata in una destinazione esistente.
* 412 - PRECONDIZIONE NON RIUSCITA - se manca un’intestazione di richiesta.
* 500 - ERRORE INTERNO DEL SERVER - se si verificano altri errori.

## Spostare una cartella o una risorsa {#move-a-folder-or-asset}

Sposta una cartella o una risorsa nel percorso specificato in una nuova destinazione.

**Intestazioni richiesta**: i parametri sono:

* `X-Destination` - Nuovo URI di destinazione nell&#39;ambito della soluzione API in cui copiare la risorsa.
* `X-Depth` - `infinity` o `0`. Se si utilizza `0`, verranno copiate solo la risorsa e le relative proprietà e non i relativi elementi figlio.
* `X-Overwrite` - Utilizzare `T` per eliminare forzatamente una risorsa esistente oppure `F` per impedire la sovrascrittura di una risorsa esistente.

**Richiesta**: `MOVE /api/assets/myFolder -H"X-Destination: /api/assets/myFolder-moved"`

**Codici di risposta**: I codici di risposta sono:

* 201 - CREATO - se la cartella/risorsa è stata copiata in una destinazione non esistente.
* 204 - NESSUN CONTENUTO - se la cartella/risorsa è stata copiata in una destinazione esistente.
* 412 - PRECONDIZIONE NON RIUSCITA - se manca un’intestazione di richiesta.
* 500 - ERRORE INTERNO DEL SERVER - se si verificano altri errori.

## Eliminare una cartella, una risorsa o una rappresentazione {#delete-a-folder-asset-or-rendition}

Elimina una risorsa (-tree) nel percorso specificato.

**Richiesta**

* `DELETE /api/assets/myFolder`
* `DELETE /api/assets/myFolder/myAsset.png`
* `DELETE /api/assets/myFolder/myAsset.png/renditions/original`

**Codici di risposta**: I codici di risposta sono:

* 200 - OK - se la cartella è stata eliminata correttamente.
* 412 - PRECONDIZIONE NON RIUSCITA - se non è possibile trovare o accedere alla raccolta radice.
* 500 - ERRORE INTERNO DEL SERVER - se si verificano altri errori.

## Suggerimenti, best practice e limitazioni {#tips-limitations}

* Dopo l&#39;[!UICONTROL Ora di disattivazione], una risorsa e le relative rappresentazioni non sono disponibili tramite l&#39;interfaccia Web [!DNL Assets] e tramite l&#39;API HTTP. L&#39;API restituisce il messaggio di errore 404 se [!UICONTROL Ora di attivazione] è nel futuro o [!UICONTROL Ora di disattivazione] è nel passato.

* L’API HTTP di Assets non restituisce i metadati completi. Gli spazi dei nomi sono hardcoded e vengono restituiti solo tali spazi dei nomi. Per i metadati completi, vedere il percorso della risorsa `/jcr_content/metadata.json`.

* Alcune proprietà della cartella o della risorsa sono mappate a un prefisso diverso quando vengono aggiornate utilizzando le API. Il prefisso `jcr` di `jcr:title`, `jcr:description` e `jcr:language` viene sostituito con il prefisso `dc`. Pertanto, nel JSON restituito, `dc:title` e `dc:description` contengono rispettivamente i valori di `jcr:title` e `jcr:description`.

**Consulta anche**

* [Traduci risorse](translate-assets.md)
* [Formati di file supportati dalle risorse](file-format-support.md)
* [Cerca risorse](search-assets.md)
* [Risorse collegate](use-assets-across-connected-assets-instances.md)
* [Rapporti sulle risorse](asset-reports.md)
* [Schemi metadati](metadata-schemas.md)
* [Scaricare le risorse](download-assets-from-aem.md)
* [Gestire i metadati](manage-metadata.md)
* [Facet di ricerca](search-facets.md)
* [Gestire le raccolte](manage-collections.md)
* [Importazione in blocco dei metadati](metadata-import-export.md)
* [Pubblicare risorse in AEM e Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)

>[!MORELIKETHIS]
>
>* [Documenti di riferimento per sviluppatori per [!DNL Assets]](/help/assets/developer-reference-material-apis.md)
