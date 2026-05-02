---
title: Proprietà di Contenuto verificato
description: Utilizzare le proprietà per personalizzare il rendering di Contenuto verificato quando viene integrato con l'applicazione.
role: Admin, User
badgeSaas: label="AEM Assets" type="Positive" tooltip="Si applica ad AEM Assets)."
exl-id: cd5ec1de-36b0-48a5-95c9-9bd22fac9719
source-git-commit: c92611e4b815e49887e175943b81177e60623067
workflow-type: tm+mt
source-wordcount: '2506'
ht-degree: 24%

---

# Installazione e proprietà di Content Advisor {#content-advisor-installation-properties}

Content Advisor è inoltre disponibile per l&#39;integrazione con applicazioni non Adobe (di terze parti), estendendo l&#39;individuazione intelligente delle risorse oltre le applicazioni Adobe. Lo stesso set di funzioni avanzate, tra cui ricerca basata sull’intelligenza artificiale, consigli in base al contesto, individuazione basata su resoconto della campagna, accesso alle rappresentazioni Dynamic Media, individuazione dei frammenti di contenuto, filtri e metadati di risorse, è supportato nelle integrazioni di terze parti.

## Prerequisiti{#prereqs}

Devi accertarti di utilizzare i seguenti metodi di comunicazione:

* L’applicazione host è in esecuzione su HTTPS.
* Non è possibile eseguire l’applicazione su `localhost`. Se si desidera integrare Contenuto verificato nel computer locale, è necessario creare un dominio personalizzato, ad esempio `[https://<your_campany>.localhost.com:<port_number>]`, e aggiungere il dominio personalizzato in `redirectUrl list`.
* Puoi configurare e aggiungere clientID nella variabile di ambiente di AEM Cloud Services con il rispettivo `imsClientId`.
<!--
* You can configure and add `ADOBE_PROVIDED_CLIENT_ID` into the AEM Cloud Service environment variable with the respective `imsClientId`.
![Asset Selector IMS Client id environment](assets/asset-selector-ims-client-id-env.png)
-->
* L’elenco degli ambiti IMS deve essere definito nella configurazione dell’ambiente.
* L’URL dell’applicazione si trova nell’elenco Consentiti degli URL di reindirizzamento del client IMS.
* Il flusso di accesso IMS viene configurato e renderizzato utilizzando un pop-up sul browser web. Pertanto, i popup devono essere abilitati o consentiti nel browser di destinazione.

Utilizzare i prerequisiti di cui sopra se è necessario il flusso di lavoro di autenticazione IMS di Content Advisor. In alternativa, se hai già effettuato l’autenticazione con il flusso di lavoro IMS, puoi aggiungere le informazioni IMS.

>[!IMPORTANT]
>
> Questo archivio funge da documentazione supplementare che descrive le API disponibili e gli esempi di utilizzo per l&#39;integrazione di Contenuto verificato. Prima di installare o utilizzare Contenuto verificato, verificare che all&#39;organizzazione sia stato assegnato l&#39;accesso a Contenuto verificato come parte del profilo Experience Manager Assets as a Cloud Service. Se non è stato fornito l’accesso, non è possibile integrare o utilizzare questi componenti. Per richiedere l’accesso, l’amministratore del programma deve generare un ticket di supporto contrassegnato come P2 da Admin Console e includere le seguenti informazioni:
>
>* Nomi di dominio in cui è ospitata l’applicazione di integrazione.
>* Dopo il provisioning, all&#39;organizzazione verranno forniti `imsClientId`, `imsScope` e un `redirectUrl` corrispondenti agli ambienti richiesti che sono essenziali per la configurazione di Content Advisor. Senza tali proprietà valide, non è possibile eseguire i passaggi di installazione.

## Installazione {#content-advisor-installation}

Contenuto verificato è disponibile tramite CDN ESM (ad esempio, [esm.sh](https://esm.sh/)/[skypack](https://www.skypack.dev/)) e versione [UMD](https://github.com/umdjs/umd).

Nei browser che utilizzano la **versione UMD** (scelta consigliata):

```
<script src="https://experience.adobe.com/solutions/CQ-assets-selectors/static-assets/resources/assets-selectors.js"></script>

<script>
  const { renderAssetSelector } = PureJSSelectors;
</script>
```

Nei browser con supporto di `import maps` che utilizzano la **versione ESM CDN**:

```
<script type="module">
  import { AssetSelector } from 'https://experience.adobe.com/solutions/CQ-assets-selectors/static-assets/resources/@assets/selectors/index.js'
</script>
```

Nella federazione di moduli Deno/Webpack utilizzando la **versione ESM CDN**:

```
import { AssetSelector } from 'https://experience.adobe.com/solutions/CQ-assets-selectors/static-assets/resources/@assets/selectors/index.js'
```

## Proprietà di Contenuto verificato {#content-advisor-propertiess}

È possibile utilizzare le proprietà di Contenuto verificato per personalizzare il rendering di Contenuto verificato. Nella tabella seguente sono elencate le proprietà che è possibile utilizzare per personalizzare e utilizzare Contenuto verificato.

| Proprietà | Tipo | Obbligatorio | Predefiniti | Descrizione |
|---|---|---|---|---|
| *barra* | Booleano | No | Falso | Se contrassegnato con `true`, Contenuto verificato viene visualizzato in una barra a sinistra. Se è contrassegnato `false`, il rendering di Contenuto verificato viene eseguito nella visualizzazione modale. |
| *imsOrg* | Stringa | Sì | | L’ID di Adobe Identity Management System (IMS) assegnato durante il provisioning di [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] per l’organizzazione. La chiave `imsOrg` è necessaria per autenticare se l&#39;organizzazione a cui si accede è in Adobe IMS o meno. |
| *imsToken* | Stringa | No | | Token di connessione IMS utilizzato per l’autenticazione. `imsToken` è obbligatorio se si utilizza un&#39;applicazione [!DNL Adobe] per l&#39;integrazione. |
| *apiKey* | Stringa | No | | Chiave API utilizzata per accedere al servizio di individuazione AEM. `apiKey` è richiesto se si utilizza un&#39;integrazione dell&#39;applicazione [!DNL Adobe]. |
| *externalBrief* | Stringa | No | | Consente di caricare un documento di riepilogo della campagna per individuare le risorse rilevanti senza immettere manualmente le parole chiave di ricerca. Contenuto verificato analizza le informazioni contenute nel documento della campagna per comprenderne le finalità e consiglia le risorse pertinenti disponibili in AEM Assets. |
| *filterSchema* | Array | No | | Modello utilizzato per configurare le proprietà del filtro. Questa opzione è utile quando si desidera limitare determinate opzioni di filtro in Contenuto verificato. |
| *filterFormProps* | Oggetto | No | | Specifica le proprietà del filtro da utilizzare per perfezionare la ricerca. Per! ad esempio JPG, PNG, GIF di tipo MIME. |
| *selectedAssets* | Array `<Object>` | No |                 | Specificare l&#39;Assets selezionato al momento del rendering di Contenuto verificato. È necessario un array di oggetti che contenga una proprietà ID delle risorse. Ad esempio, `[{id: 'urn:234}, {id: 'urn:555'}]` Deve essere disponibile una risorsa nella directory corrente. Se devi utilizzare una directory diversa, specifica anche un valore per la proprietà `path`. |
| *acvConfig* | Oggetto | No | | Proprietà Visualizzazione raccolta risorse che contiene un oggetto contenente una configurazione personalizzata per ignorare le impostazioni predefinite. Inoltre, questa proprietà viene utilizzata con la proprietà `rail` per abilitare la visualizzazione della barra del visualizzatore risorse. |
| *i18nSymbols* | `Object<{ id?: string, defaultMessage?: string, description?: string}>` | No |                 | Se le traduzioni OOTB non sono sufficienti per le esigenze dell&#39;applicazione, è possibile esporre un&#39;interfaccia tramite la quale è possibile passare i propri valori localizzati personalizzati tramite la proprietà `i18nSymbols`. Il passaggio di un valore tramite questa interfaccia sostituisce le traduzioni predefinite fornite e utilizza le tue. Per eseguire la sostituzione, è necessario passare un oggetto valido del [Descrittore del messaggio](https://formatjs.io/docs/react-intl/api/#message-descriptor) alla chiave di `i18nSymbols` che desideri sostituire. |
| *intl* | Oggetto | No | | Contenuto verificato fornisce traduzioni OOTB predefinite. È possibile selezionare la lingua di traduzione fornendo una stringa di lingua valida attraverso la proprietà `intl.locale`. Ad esempio: `intl={{ locale: "es-es" }}` </br></br> Le stringhe delle impostazioni internazionali supportate seguono [ISO 639 - Codici](https://www.iso.org/iso-639-language-codes.html) per la rappresentazione dei nomi degli standard delle lingue. </br></br> Elenco delle lingue supportate: inglese - &#39;en-us&#39; (impostazione predefinita) spagnolo - &#39;es-es&#39; tedesco - &#39;de-de&#39; francese - &#39;fr-fr&#39; italiano - &#39;it-it&#39; giapponese - &#39;ja-jp&#39; coreano - &#39;ko-kr&#39; portoghese - &#39;pt-br&#39; cinese (tradizionale) - &#39;zh-cn&#39; cinese (Taiwan) - &#39;zh-tw&#39; |
| *repositoryId* | Stringa | No | &#39;&#39; | Archivio da cui Contenuto verificato carica il contenuto. |
| *additionalAemSolutions* | `Array<string>` | No | [ ] | Ti consente di aggiungere un elenco di archivi AEM aggiuntivi. Se non vengono fornite informazioni in questa proprietà, vengono considerati solo la libreria di file multimediali o gli archivi di AEM Assets. |
| *hideTreeNav* | Booleano | No |  | Specifica se mostrare o nascondere la barra laterale di navigazione della struttura delle risorse. Viene utilizzata solo nella vista modale e quindi questa proprietà non influisce sulla visualizzazione della barra. |
| *onDrop* | Funzione | No | | La funzionalità al rilascio viene utilizzata per trascinare una risorsa e rilasciarla in un’area di rilascio designata. Consente interfacce utente interattive in cui le risorse possono essere spostate ed elaborate senza problemi. |
| *dropOptions* | `{allowList?: Object}` | No | | Configura le opzioni di rilascio utilizzando un “elenco consentiti”. |
| *tema* | Stringa | No | Predefiniti | Applicare il tema all&#39;applicazione Content Advisor tra `default` e `express`. Supporta anche `@react-spectrum/theme-express`. |
| *handleSelection* | Funzione | No | | Richiamata con un array di elementi di risorse quando queste sono selezionate e si fa clic sul pulsante `Select` nel modale. Questa funzione viene richiamata solo nella vista modale. Per la visualizzazione della barra, utilizza le funzioni `handleAssetSelection` o `onDrop`. Esempio: <pre>handleSelection=(risorse: risorsa[])=> {...}</pre> Per informazioni dettagliate, consulta [selezione di risorse](/help/assets/content-advisor-customization.md#selection-of-assets). |
| *handleAssetSelection* | Funzione | No | | Richiamata con un array di elementi durante la selezione o la deselezione delle risorse. Questa funzione è utile quando si desidera ascoltare le risorse selezionate dall’utente. Esempio: <pre>handleAssetSelection=(risorse: risorsa[])=> {...}</pre> Per informazioni dettagliate, consulta [selezione di risorse](/help/assets/content-advisor-customization.md#selection-of-assets). |
| *onClose* | Funzione | No | | Richiamata quando viene premuto il pulsante `Close` nella vista modale. Questa è chiamata solo nella vista `modal` e ignorata nella vista `rail`. |
| *onFilterSubmit* | Funzione | No | | Richiamata con gli elementi filtro poiché l’utente modifica criteri di filtro diversi. |
| *selectionType* | Stringa | No | Celibe/Nubile | Configurazione per la selezione `single` o `multiple` di risorse alla volta. |
| *trascinamentoOpzioni.inserisco nell&#39;elenco Consentiti di* | booleano | No | | La proprietà viene utilizzata per consentire o negare il trascinamento di risorse non selezionabili. Vedi [Proprietà dragOptions](/help/assets/content-advisor-customization.md#drag-options-property) |
| *aemTierType* | Stringa | No |  | Consente di scegliere se visualizzare le risorse dal livello di consegna, dal livello di authoring o da entrambi. <br><br> Sintassi: `aemTierType: "author"  "delivery"` <br><br> Ad esempio, se vengono utilizzati entrambi `["author","delivery"]`, il commutatore dell&#39;archivio visualizza le opzioni sia per l&#39;authoring che per la consegna. |
| *handleNavigateToAsset* | Funzione | No | | È una funzione di callback per gestire la selezione di una risorsa. |
| *noWrap* | Booleano | No | | La proprietà *noWrap* impedisce il wrapping di Contenuto verificato in una finestra di dialogo. Se questa proprietà non è menzionata, per impostazione predefinita viene eseguita la visualizzazione *Finestra di dialogo*. |
| *dimensioneFinestraDiDialogo* | S, M, L, fullscreen, fullscreenTakeover | Stringa | Facoltativo | È possibile controllare il layout specificandone le dimensioni utilizzando le opzioni specificate. |
| *colorScheme* | Stringa (chiara, scura) | No | | Questa proprietà viene utilizzata per impostare il tema di un&#39;applicazione Content Advisor. Puoi scegliere tra tema chiaro o scuro. |
| *filterRepoList* | Funzione | No | | Funzione che riceve l&#39;elenco del repository e restituisce un elenco filtrato. |
| *expiryOptions* | Funzione | | | È possibile utilizzare tra le due proprietà seguenti: **getExpiryStatus** che fornisce lo stato di una risorsa scaduta. La funzione restituisce `EXPIRED`, `EXPIRING_SOON` o `NOT_EXPIRED` in base alla data di scadenza di una risorsa fornita. Consulta [personalizzare le risorse scadute](/help/assets/content-advisor-customization.md#customize-expired-assets). È inoltre possibile utilizzare **allowSelectionAndDrag** in cui il valore della funzione può essere `true` o `false`. Quando il valore è impostato su `false`, la risorsa scaduta non può essere selezionata o trascinata nell&#39;area di lavoro. |
| *showToast* | | No | | Consente a Contenuto verificato di visualizzare un messaggio popup personalizzato per la risorsa scaduta. |
| *uploadConfig* | Oggetto | | | Si tratta di un oggetto che contiene una configurazione personalizzata per il caricamento. Per informazioni sull&#39;usabilità, vedere [configurazione caricamento](#content-advisor-customization.md#upload-config). |
| *uploadConfig* > *metadataSchema* | Array | No | | Questa proprietà è nidificata nella proprietà `uploadConfig`. Aggiungi un array di campi fornito per raccogliere i metadati dall’utente. Utilizzando questa proprietà, puoi anche utilizzare metadati nascosti che vengono assegnati automaticamente a una risorsa ma non sono visibili all’utente. |
| *uploadConfig* > *onMetadataFormChange* | Funzione callback | No | | Questa proprietà è nidificata nella proprietà `uploadConfig`. È costituito da `property` e `value`. `Property` è uguale a *mapToProperty* del campo passato da *metadataSchema* il cui valore è in fase di aggiornamento. Mentre,`value` è uguale al nuovo valore fornito come input. |
| *uploadConfig* > *targetUploadPath* | Stringa |  | `"/content/dam"` | Questa proprietà è nidificata nella proprietà `uploadConfig`. Percorso di caricamento di destinazione per i file che per impostazione predefinita sono nella directory principale dell’archivio delle risorse. |
| *uploadConfig* > *hideUploadButton* | Booleano | | Falso | In questo modo viene garantito se il pulsante Caricamento interno deve essere nascosto o meno. Questa proprietà è nidificata nella proprietà `uploadConfig`. |
| *uploadConfig* > *onUploadStart* | Funzione | No |  | Si tratta di una funzione di callback utilizzata per passare l&#39;origine di caricamento tra Dropbox, OneDrive o locale. La sintassi è `(uploadInfo: UploadInfo) => void`. Questa proprietà è nidificata nella proprietà `uploadConfig`. |
| *uploadConfig* > *importSettings* | Funzione | | | Abilita il supporto per l’importazione di risorse da origini terze. `sourceTypes` utilizza un array delle origini di importazione che si desidera abilitare. Le origini supportate sono Onedrive e Dropbox. La sintassi è `{ sourceTypes?: ImportSourceType[]; apiKey?: string; }`. Inoltre, questa proprietà è nidificata nella proprietà `uploadConfig`. |
| *uploadConfig* > *onUploadComplete* | Funzione | No | | Si tratta di una funzione di callback utilizzata per passare lo stato di caricamento del file tra completato, non riuscito o duplicato. La sintassi è `(uploadStats: UploadStats) => void`. Inoltre, questa proprietà è nidificata nella proprietà `uploadConfig`. |
| *uploadConfig* > *onFilesChange* | Funzione | No | | Questa proprietà è nidificata nella proprietà `uploadConfig`. Si tratta di una funzione di callback utilizzata per mostrare il comportamento di caricamento quando un file viene modificato. Trasmette il nuovo array di file in attesa di caricamento e il tipo di origine del caricamento. Il tipo di Source può essere nullo in caso di errore. La sintassi è `(newFiles: File[], uploadType: UploadType) => void` |
| *uploadConfig* > *uploadingPlaceholder* | Stringa | | | È un’immagine segnaposto che sostituisce il modulo metadati quando viene avviato il caricamento della risorsa. La sintassi è `{ href: string; alt: string; }`. Inoltre, questa proprietà è nidificata sotto la proprietà `uploadConfig`. |
| *featureSet* | Array | Stringa | | La proprietà `featureSet:[ ]` viene utilizzata per abilitare o disabilitare una particolare funzionalità nell&#39;applicazione Content Advisor. Per abilitare il componente o una funzione, puoi passare un valore stringa nell’array oppure lasciare vuoto l’array per disabilitare le funzioni aggiunte e disporre solo della funzionalità di base. Per abilitare ad esempio la funzionalità di caricamento in Contenuto verificato, utilizzare la sintassi `featureSet:["upload"]`. Analogamente, è possibile utilizzare `featureSet:["content-fragments"]` per abilitare i frammenti di contenuto in Contenuto verificato. Per utilizzare più funzionalità insieme, la sintassi è featureSet:[&quot;upload&quot;, &quot;content-fragments&quot;]. |

<!--
| *selectedRendition* | Object | | | This property allows users to define and control which renditions of an asset are displayed when the panel is accessed. This customization enhances user experience by filtering out unnecessary renditions and showcasing only the most relevant renditions. For example, `CopyUrlHref` allows you to use Dynamic Media renditions in your Asset Selector application (delivery URL). |
| *featureSet* | Array | String | | The `featureSet:[ ]` property is used to enable or disable a particular functionaly in the Asset Selector application. To enable the component or a feature, you can pass a string value in the array or leave the array empty to disable that component. For example, you want to enable upload functionality in the Asset Selector, use the syntax `featureSet:[0:"upload"]`. Similarly, you can use `featureSet:[0:"collections"]` to enable collections in the Asset Selector. Addidionally, use `featureSet:[0:"detail-panel"]` to enable [details panel](overview-asset-selector.md#asset-details-and-metadata) of an asset. Also, `featureSet:[0:"dm-renditions"]` to show Dynamic Media renditions of an asset.|
| *rootPath* | String | No | /content/dam/ | Folder path from which Asset Selector displays your assets. `rootPath` can also be used in the form of encapsulation. For example, given the following path, `/content/dam/marketing/subfolder/`, Asset Selector does not allow you to traverse through any parent folder, but only displays the children folders. |
| *path* | String | No | | Path that is used to navigate to a specific directory of assets when the Asset Selector is rendered. |
| *expirationDate* | Function | No | | This function is used to set the usability period of an asset. |
| *disableDefaultBehaviour* | Boolean | No | False | It is a function that is used to enable or disable the selection of an expired asset. You can customize the default behavior of an asset that is set to expire. See [customize expired assets](/help/assets/asset-selector-customization.md#customize-expired-assets). |
-->

### ImsAuthProps {#ims-auth-props}

Le proprietà `ImsAuthProps` definiscono le informazioni di autenticazione e il flusso utilizzati da Content Advisor per ottenere un `imsToken`. Impostando queste proprietà è possibile controllare il comportamento del flusso di autenticazione e registrare i listener per vari eventi di autenticazione.

| Nome proprietà | Descrizione |
|---|---|
| `imsClientId` | Valore stringa che rappresenta l’ID client IMS utilizzato a scopo di autenticazione. Questo valore è fornito da Adobe ed è specifico per la tua organizzazione Adobe AEM CS. |
| `imsScope` | Descrive gli ambiti utilizzati nell&#39;autenticazione. Gli ambiti determinano il livello di accesso dell&#39;applicazione alle risorse dell&#39;organizzazione. Più ambiti possono essere separati da virgole. |
| `redirectUrl` | Rappresenta l&#39;URL a cui l&#39;utente viene reindirizzato dopo l&#39;autenticazione. Questo valore viene in genere impostato sull’URL corrente dell’applicazione. Se non viene fornito `redirectUrl`, `ImsAuthService` utilizza il redirectUrl utilizzato per registrare `imsClientId` |
| `modalMode` | Valore booleano che indica se il flusso di autenticazione deve essere visualizzato o meno in un modale (pop-up). Se è impostato su `true`, il flusso di autenticazione viene visualizzato in un popup. Se è impostato su `false`, il flusso di autenticazione viene visualizzato in un ricaricamento dell&#39;intera pagina. _Note :_per una migliore interfaccia utente, è possibile controllare dinamicamente questo valore se la finestra popup del browser dell&#39;utente è disabilitata. |
| `onImsServiceInitialized` | Funzione di callback chiamata quando viene inizializzato il servizio di autenticazione Adobe IMS. Questa funzione accetta un parametro, `service`, che è un oggetto che rappresenta il servizio Adobe IMS. Per ulteriori dettagli, vedere [`ImsAuthService`](#imsauthservice-ims-auth-service). |
| `onAccessTokenReceived` | Funzione di callback chiamata quando viene ricevuto un `imsToken` dal servizio di autenticazione Adobe IMS. Questa funzione accetta un parametro, `imsToken`, che è una stringa che rappresenta il token di accesso. |
| `onAccessTokenExpired` | Funzione di callback chiamata quando un token di accesso è scaduto. Questa funzione viene in genere utilizzata per attivare un nuovo flusso di autenticazione per ottenere un nuovo token di accesso. |
| `onErrorReceived` | Funzione di callback chiamata quando si verifica un errore durante l&#39;autenticazione. Questa funzione accetta due parametri: il tipo di errore e il messaggio di errore. Il tipo di errore è una stringa che rappresenta il tipo di errore e il messaggio di errore è una stringa che rappresenta il messaggio di errore. |

### ImsAuthService {#ims-auth-service}

La classe `ImsAuthService` gestisce il flusso di autenticazione per Contenuto verificato. È responsabile dell&#39;ottenimento di un `imsToken` dal servizio di autenticazione Adobe IMS. `imsToken` viene utilizzato per autenticare l&#39;utente e autorizzare l&#39;accesso a [!DNL Adobe Experience Manager] come archivio Assets [!DNL Cloud Service]. ImsAuthService utilizza le proprietà `ImsAuthProps` per controllare il flusso di autenticazione e registrare i listener per vari eventi di autenticazione. È possibile utilizzare la comoda funzione [`registerAssetsSelectorsAuthService`](#purejsselectorsregisterassetsselectorsauthservice) per registrare l&#39;istanza _ImsAuthService_ con Contenuto verificato. Le seguenti funzioni sono disponibili nella classe `ImsAuthService`. Tuttavia, se si utilizza la funzione _registerAssetsSelectorsAuthService_, non è necessario chiamare queste funzioni direttamente.

| Nome funzione | Descrizione |
|---|---|
| `isSignedInUser` | Determina se l&#39;utente è attualmente connesso al servizio e restituisce di conseguenza un valore booleano. |
| `getImsToken` | Recupera l&#39;autenticazione `imsToken` per l&#39;utente attualmente connesso, che può essere utilizzata per autenticare le richieste ad altri servizi, ad esempio per generare la _rappresentazione della risorsa. |
| `signIn` | Avvia il processo di accesso per l&#39;utente. Questa funzione utilizza `ImsAuthProps` per mostrare l&#39;autenticazione in un popup o in un ricaricamento dell&#39;intera pagina |
| `signOut` | Firma l’utente fuori dal servizio, invalidando il token di autenticazione e richiedendo di nuovo l’accesso per accedere alle risorse protette. Richiamando questa funzione verrà ricaricata la pagina corrente. |
| `refreshToken` | Aggiorna il token di autenticazione per l&#39;utente attualmente connesso, evitando la scadenza e garantendo l&#39;accesso ininterrotto alle risorse protette. Restituisce un nuovo token di autenticazione che può essere utilizzato per le richieste successive. |

### contentFragmentSelectorProps {#content-fragment-selector-properties}

`contentFragmentSelectorProps` consente di configurare la modalità di accesso e visualizzazione dei frammenti di contenuto in Contenuto verificato. Attivando la funzione Frammenti di contenuto in `featureSet` e fornendo la configurazione richiesta, puoi integrare facilmente la selezione di Frammenti di contenuto insieme alle risorse. Questo consente agli utenti di sfogliare, cercare e selezionare Frammenti di contenuto all’interno della stessa interfaccia unificata, garantendo un’esperienza di selezione dei contenuti coerente tra risorse e contenuti strutturati.

```
const assetSelectorProps = {
     featureSet: [
       'upload',            /* Include upload or other featureSet values to ensure no missing functionality */
       'content-fragments', /* Content Fragments pill will be shown */
     ],
     contentFragmentSelectorProps: {
       /* Configures the Content Fragments Pill experience */
       /* ...props @aem-sites/content-fragment-selector MFE supports */
    }
}

<AssetSelector {...assetSelectorProps} />
```

In `contentFragmentSelectorProps` è possibile indicare qualsiasi proprietà disponibile in [Proprietà selettore frammento di contenuto](/help/headless/content-fragment-selector/properties.md).

Per informazioni su come integrare Content Advisor con le applicazioni Angular, React e JavaScript, vedere [Esempi di integrazione di Content Advisor](https://github.com/adobe/aem-assets-selectors-mfe-examples/tree/consolidate-docs-to-experience-league/examples).


