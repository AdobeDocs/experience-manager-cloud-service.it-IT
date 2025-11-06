---
title: API HTTP di Assets
description: Crea, leggi, aggiorna, elimina, gestisci le risorse digitali tramite API HTTP in [!DNL Experience Manager Assets].
contentOwner: AG
feature: Assets HTTP API
role: Developer, Admin
exl-id: a3b7374d-f24b-4d6f-b6db-b9c9c962bb8d
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1691'
ht-degree: 5%

---

# Gestire le risorse digitali con l&#39;API HTTP [!DNL Adobe Experience Manager Assets]{#assets-http-api}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-65/assets/extending/mac-api-assets.html?lang=en) |
| AEM as a Cloud Service | Questo articolo |

## Introduzione all&#39;API HTTP di AEM [!DNL Assets] {#overview}

L&#39;API HTTP di AEM [!DNL Assets] abilita operazioni CRUD (creazione, lettura, aggiornamento ed eliminazione) sulle risorse digitali tramite un&#39;interfaccia REST disponibile in /`api/assets`. Queste operazioni si applicano ai metadati delle risorse, alle rappresentazioni e ai commenti. Include [supporto per frammenti di contenuto](/help/assets/content-fragments/assets-api-content-fragments.md).

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

## Gestire i frammenti di contenuto {#content-fragments}

Un [frammento di contenuto](/help/assets/content-fragments/content-fragments.md) è una risorsa strutturata in cui sono memorizzati testo, numeri e date. Poiché esistono diverse differenze per `standard` risorse (come immagini o documenti), alcune regole aggiuntive si applicano alla gestione dei frammenti di contenuto.

Per ulteriori informazioni, vedere il supporto per [Frammenti di contenuto nell&#39; [!DNL Experience Manager Assets] API HTTP](/help/assets/content-fragments/assets-api-content-fragments.md).

>[!NOTE]
>
>Consulta [API di AEM per la distribuzione e la gestione strutturata dei contenuti](/help/headless/apis-headless-and-content-fragments.md) per una panoramica delle varie API disponibili e un confronto di alcuni dei concetti coinvolti.
>
>Sono disponibili anche [OpenAPI per frammenti di contenuto e modelli di frammenti di contenuto](/help/headless/content-fragment-openapis.md).

## Esamina il modello dati {#data-model}

L&#39;API HTTP [!DNL Assets] espone principalmente due elementi: cartelle e risorse standard. Inoltre, fornisce elementi dettagliati per i modelli di dati personalizzati utilizzati nei frammenti di contenuto. Per ulteriori dettagli, consulta Modelli di dati per frammenti di contenuto. Per ulteriori informazioni, consulta [Modelli dati per frammenti di contenuto](/help/assets/content-fragments/assets-api-content-fragments.md#content-models-and-content-fragments).

>[!NOTE]
>
>Sono disponibili anche [OpenAPI per frammenti di contenuto e modelli di frammenti di contenuto](/help/headless/content-fragment-openapis.md).

### Gestione cartelle {#folders}

Le cartelle sono simili alle directory dei file system tradizionali. Le cartelle possono contenere risorse, sottocartelle o entrambe. Le cartelle hanno i seguenti componenti:

**Entità**: le entità di una cartella sono i relativi elementi secondari, che possono essere cartelle e risorse.

**Proprietà**:

* `name`: nome della cartella (l&#39;ultimo segmento del percorso URL, senza estensione).
* `title`: viene visualizzato un titolo facoltativo al posto del nome della cartella.

>[!NOTE]
>
>Alcune proprietà della cartella o della risorsa sono mappate a un prefisso diverso. Il prefisso `jcr` di `jcr:title`, `jcr:description` e `jcr:language` viene sostituito con il prefisso `dc`. Pertanto, nel JSON restituito, `dc:title` e `dc:description` contengono rispettivamente i valori di `jcr:title` e `jcr:description`.

**I collegamenti** nelle cartelle espongono tre collegamenti:

* `self`: collegamento alla cartella stessa.
* `parent`: collegamento alla cartella principale.
* `thumbnail` (facoltativo): collegamento a un&#39;immagine di miniatura della cartella.

### Gestire le risorse {#assets}

In [!DNL Experience Manager] una risorsa contiene i seguenti elementi:

* **Proprietà e metadati:** Informazioni descrittive sulla risorsa.
* **File binario:** Il file caricato originariamente.
* **Rappresentazioni:** più rappresentazioni configurate, ad esempio immagini di varie dimensioni, diverse codifiche video o pagine estratte da file PDF/Adobe InDesign.
* **Commenti (facoltativo):** osservazioni fornite dall&#39;utente.

Per informazioni sugli elementi nei frammenti di contenuto, vedere [Supporto dei frammenti di contenuto nell&#39;API HTTP Experience Manager Assets](/help/assets/content-fragments/assets-api-content-fragments.md).

>[!NOTE]
>
>Sono disponibili anche [OpenAPI per frammenti di contenuto e modelli di frammenti di contenuto](/help/headless/content-fragment-openapis.md).

In [!DNL Experience Manager] una cartella contiene i seguenti componenti:

* Entità: i figli delle risorse ne sono le rappresentazioni.
* Proprietà.
* Collegamenti.

## Esplora le operazioni API disponibili {#available-features}

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
* Un set di coppie nome-valore, codificate come `application/www-form-urlencoded` o `multipart`/ `form`- `data`. Questi sono utili per creare una cartella direttamente da un modulo di HTML.

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

La creazione di risorse non è supportata tramite questa API HTTP. Per creare le risorse, utilizza l&#39;API [caricamento risorse](developer-reference-material-apis.md).

## Aggiornare un binario di risorse {#update-asset-binary}

Consulta [caricamento risorse](developer-reference-material-apis.md) per informazioni su come aggiornare i file binari delle risorse. Non è possibile aggiornare un binario di risorse utilizzando l’API HTTP.

## Aggiornare i metadati di una risorsa {#update-asset-metadata}

Questa operazione aggiorna i metadati della risorsa. Quando si aggiornano le proprietà nello spazio dei nomi `dc:`, viene aggiornata la proprietà `jcr:` corrispondente. Tuttavia, l’API non sincronizza le proprietà sotto i due spazi dei nomi.

**Richiesta**: `PUT /api/assets/myfolder/myAsset.png -H"Content-Type: application/json" -d '{"class":"asset", "properties":{"dc:title":"My Asset"}}'`

**Codici di risposta**: I codici di risposta sono:

* 200 - OK - se la risorsa è stata aggiornata correttamente.
* 404 - NON TROVATO - se la risorsa non è stata trovata o non è stato possibile accedervi all’URI specificato.
* 412 - PRECONDIZIONE NON RIUSCITA - se non è possibile trovare o accedere alla raccolta radice.
* 500 - ERRORE INTERNO DEL SERVER - se si verificano altri errori.

## Creare una rappresentazione di una risorsa {#create-an-asset-rendition}

Crea una rappresentazione per una risorsa. Se non viene fornito il nome del parametro della richiesta, il nome del file viene utilizzato come nome della rappresentazione.

**Parametri**: i parametri sono:

`name`: per il nome della rappresentazione.
`file`: file binario per la copia trasformata come riferimento.

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

## Segui le best practice e le limitazioni delle note {#tips-limitations}

* Assets e le relative copie trasformate non sono più disponibili tramite l&#39;interfaccia Web [!DNL Assets] e l&#39;API HTTP quando viene raggiunta l&#39;[!UICONTROL Ora di disattivazione]. L&#39;API restituisce un errore 404 se [!UICONTROL Ora di attivazione] è nel futuro o [!UICONTROL Ora di disattivazione] è nel passato.

* L’API HTTP di Assets restituisce solo un sottoinsieme di metadati. Gli spazi dei nomi sono hardcoded e vengono restituiti solo tali spazi dei nomi. Per i metadati completi, vedere il percorso della risorsa `/jcr_content/metadata.json`.

* Alcune proprietà della cartella o della risorsa sono mappate a un prefisso diverso quando vengono aggiornate utilizzando le API. Il prefisso `jcr` di `jcr:title`, `jcr:description` e `jcr:language` viene sostituito con il prefisso `dc`. Pertanto, nel JSON restituito, `dc:title` e `dc:description` contengono rispettivamente i valori di `jcr:title` e `jcr:description`.

**Esplora risorse correlate**

* [Traduci risorse](translate-assets.md)
* [Formati di file supportati dalle risorse](file-format-support.md)
* [Cerca risorse](search-assets.md)
* [Risorse collegate](use-assets-across-connected-assets-instances.md)
* [Rapporti sulle risorse](asset-reports.md)
* [Schemi di metadati](metadata-schemas.md)
* [Scaricare le risorse](download-assets-from-aem.md)
* [Gestire i metadati](manage-metadata.md)
* [Facet di ricerca](search-facets.md)
* [Gestire le raccolte](manage-collections.md)
* [Importazione in blocco dei metadati](metadata-import-export.md)
* [Pubblicare risorse in AEM e Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)

>[!MORELIKETHIS]
>
>* [Documenti di riferimento per sviluppatori per [!DNL Assets]](/help/assets/developer-reference-material-apis.md)
