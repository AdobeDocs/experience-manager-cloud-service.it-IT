---
title: Selettore risorse per [!DNL Adobe Experience Manager]  as a  [!DNL Cloud Service]
description: Utilizza il Selettore risorse per cercare, trovare e recuperare i metadati e le rappresentazioni delle risorse all’interno dell’applicazione.
role: Admin, User
exl-id: cd5ec1de-36b0-48a5-95c9-9bd22fac9719
source-git-commit: 188f60887a1904fbe4c69f644f6751ca7c9f1cc3
workflow-type: tm+mt
source-wordcount: '1323'
ht-degree: 42%

---

# Proprietà del Selettore risorse {#asset-selector-properties}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuovo</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime e Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuovo</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuova</i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>Integrazione di AEM Assets con Edge Delivery Services</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuovo</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>Estensibilità interfaccia utente</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuovo</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>Abilita Dynamic Media Prime e Ultimate</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>Best practice per la ricerca</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>Best practice per i metadati</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>Content Hub</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>Dynamic Media con funzionalità OpenAPI</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>Documentazione di AEM Assets per sviluppatori</b></a>
        </td>
    </tr>
</table>

Puoi utilizzare le proprietà del Selettore risorse per personalizzarne il rendering. Nella tabella seguente sono elencate le proprietà che è possibile utilizzare per personalizzare e utilizzare il Selettore risorse.

| Proprietà | Tipo | Obbligatorio | Predefiniti | Descrizione |
|---|---|---|---|---|
| *barra* | Booleano | No | Falso | Se contrassegnato come `true`, il rendering del selettore risorse viene eseguito in una visualizzazione della barra a sinistra. Se è contrassegnato `false`, il rendering del selettore risorse viene eseguito nella vista modale. |
| *imsOrg* | Stringa | Sì | | L’ID di Adobe Identity Management System (IMS) assegnato durante il provisioning di [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] per l’organizzazione. La chiave `imsOrg` è necessaria per autenticare se l&#39;organizzazione a cui si accede è in Adobe IMS o meno. |
| *imsToken* | Stringa | No | | Token di connessione IMS utilizzato per l’autenticazione. `imsToken` è obbligatorio se si utilizza un&#39;applicazione [!DNL Adobe] per l&#39;integrazione. |
| *apiKey* | Stringa | No | | Chiave API utilizzata per accedere al servizio di individuazione AEM. `apiKey` è richiesto se si utilizza un&#39;integrazione dell&#39;applicazione [!DNL Adobe]. |
| *filterSchema* | Array | No | | Modello utilizzato per configurare le proprietà del filtro. Questa funzione è utile quando desideri limitare determinate opzioni di filtro nel Selettore risorse. |
| *filterFormProps* | Oggetto | No | | Specifica le proprietà del filtro da utilizzare per perfezionare la ricerca. Per! ad esempio JPG, PNG, GIF di tipo MIME. |
| *selectedAssets* | Array `<Object>` | No |                 | Specifica le risorse selezionate quando viene eseguito il rendering del Selettore risorse. È necessario un array di oggetti che contenga una proprietà ID delle risorse. Ad esempio, `[{id: 'urn:234}, {id: 'urn:555'}]` Deve essere disponibile una risorsa nella directory corrente. Se devi utilizzare una directory diversa, specifica anche un valore per la proprietà `path`. |
| *acvConfig* | Oggetto | No | | Proprietà Visualizzazione raccolta risorse che contiene un oggetto contenente una configurazione personalizzata per ignorare le impostazioni predefinite. Inoltre, questa proprietà viene utilizzata con la proprietà `rail` per abilitare la visualizzazione della barra del visualizzatore risorse. |
| *i18nSymbols* | `Object<{ id?: string, defaultMessage?: string, description?: string}>` | No |                 | Se le traduzioni OOTB non sono sufficienti per le esigenze dell&#39;applicazione, è possibile esporre un&#39;interfaccia tramite la quale è possibile passare i propri valori localizzati personalizzati tramite la proprietà `i18nSymbols`. Il passaggio di un valore tramite questa interfaccia sostituisce le traduzioni predefinite fornite e utilizza le tue. Per eseguire la sostituzione, è necessario passare un oggetto valido del [Descrittore del messaggio](https://formatjs.io/docs/react-intl/api/#message-descriptor) alla chiave di `i18nSymbols` che desideri sostituire. |
| *intl* | Oggetto | No | | Il selettore risorse fornisce le traduzioni OOTB predefinite. È possibile selezionare la lingua di traduzione fornendo una stringa di lingua valida attraverso la proprietà `intl.locale`. Ad esempio: `intl={{ locale: "es-es" }}` </br></br> Le stringhe di lingua supportate seguono i [Codici - ISO 639](https://www.iso.org/iso-639-language-codes.html) per la rappresentazione di nomi di lingue standard. </br></br> Elenco delle lingue supportate: Inglese - ‘en-us’ (impostazione predefinita) Spagnolo - ‘es-es’ Tedesco - ‘de-de’ Francese - ‘fr-fr’ Italiano - ‘it-it’ Giapponese - ‘ja-jp’ Coreano - ‘ko-kr’ Portoghese - ‘pt-br’ cinese (tradizionale) - ‘zh-cn’ Cinese (Taiwan) - ‘zh-tw’ |
| *repositoryId* | Stringa | No | &#39;&#39; | Archivio da cui il Selettore risorse carica il contenuto. |
| *additionalAemSolutions* | `Array<string>` | No | [ ] | Ti consente di aggiungere un elenco di archivi AEM aggiuntivi. Se non vengono fornite informazioni in questa proprietà, vengono considerati solo la libreria di file multimediali o gli archivi di AEM Assets. |
| *hideTreeNav* | Booleano | No |  | Specifica se mostrare o nascondere la barra laterale di navigazione della struttura delle risorse. Viene utilizzata solo nella vista modale e quindi questa proprietà non influisce sulla visualizzazione della barra. |
| *onDrop* | Funzione | No | | La proprietà consente la funzionalità di rilascio di una risorsa. |
| *dropOptions* | `{allowList?: Object}` | No | | Configura le opzioni di rilascio utilizzando un “elenco consentiti”. |
| *colorScheme* | Stringa | No | | Configura il tema (`light` o `dark`) per il Selettore risorse. |
| *Tema* | Stringa | No | Predefiniti | Applica il tema all&#39;applicazione Asset Selector tra `default` e `express`. Supporta anche `@react-spectrum/theme-express`. |
| *handleSelection* | Funzione | No | | Richiamata con un array di elementi di risorse quando queste sono selezionate e si fa clic sul pulsante `Select` nel modale. Questa funzione viene richiamata solo nella vista modale. Per la visualizzazione della barra, utilizza le funzioni `handleAssetSelection` o `onDrop`. Esempio: <pre>handleSelection=(risorse: risorsa[])=> {...}</pre> Per informazioni dettagliate, consulta [selezione di risorse](/help/assets/asset-selector-customization.md#selection-of-assets). |
| *handleAssetSelection* | Funzione | No | | Richiamata con un array di elementi durante la selezione o la deselezione delle risorse. Questa funzione è utile quando si desidera ascoltare le risorse selezionate dall’utente. Esempio: <pre>handleSelection=(risorse: risorsa[])=> {...}</pre> Per informazioni dettagliate, consulta [selezione di risorse](/help/assets/asset-selector-customization.md#selection-of-assets). |
| *onClose* | Funzione | No | | Richiamata quando viene premuto il pulsante `Close` nella vista modale. Questa è chiamata solo nella vista `modal` e ignorata nella vista `rail`. |
| *onFilterSubmit* | Funzione | No | | Richiamata con gli elementi filtro poiché l’utente modifica criteri di filtro diversi. |
| *selectionType* | Stringa | No | Celibe/Nubile | Configurazione per la selezione `single` o `multiple` di risorse alla volta. |
| *trascinamentoOpzioni.inserisco nell&#39;elenco Consentiti di* | booleano | No | | La proprietà viene utilizzata per consentire o negare il trascinamento di risorse non selezionabili. |
| *aemTierType* | Stringa | No |  | Consente di scegliere se visualizzare le risorse dal livello di consegna, dal livello di authoring o da entrambi. Sintassi <br><br>: `aemTierType:[0]: "author" 1: "delivery"` <br><br> Ad esempio, se vengono utilizzati entrambi `["author","delivery"]`, il commutatore dell&#39;archivio visualizza le opzioni sia per l&#39;autore che per la consegna. |
| *handleNavigateToAsset* | Funzione | No | | È una funzione di callback per gestire la selezione di una risorsa. |
| *noWrap* | Booleano | No | | La proprietà *noWrap* consente di eseguire il rendering del selettore risorse nel pannello della barra laterale. Se questa proprietà non è menzionata, per impostazione predefinita viene eseguita la visualizzazione *Finestra di dialogo*. |
| *dimensioneFinestraDiDialogo* | acquisizione di piccole, medie, grandi, a schermo intero o intero | Stringa | Facoltativo | È possibile controllare il layout specificandone le dimensioni utilizzando le opzioni specificate. |
| *colorScheme* | Chiaro o scuro | No | | Questa proprietà viene utilizzata per impostare il tema di un&#39;applicazione Asset Selector. Puoi scegliere tra tema chiaro o scuro. |
| *filterRepoList* | Funzione | No |  | È possibile utilizzare la funzione di callback `filterRepoList` che chiama l&#39;archivio Experience Manager e restituisce un elenco filtrato di archivi. |
| *expiryOptions* | Funzione | | | È possibile utilizzare tra le due proprietà seguenti: **getExpiryStatus** che fornisce lo stato di una risorsa scaduta. La funzione restituisce `EXPIRED`, `EXPIRING_SOON` o `NOT_EXPIRED` in base alla data di scadenza di una risorsa fornita. Consulta [personalizzare le risorse scadute](/help/assets/asset-selector-customization.md#customize-expired-assets). È inoltre possibile utilizzare **allowSelectionAndDrag** in cui il valore della funzione può essere `true` o `false`. Quando il valore è impostato su `false`, la risorsa scaduta non può essere selezionata o trascinata nell&#39;area di lavoro. |
| *showToast* | | No | | Consente al selettore risorse di visualizzare un messaggio popup personalizzato per la risorsa scaduta. |
| *metadataSchema* | Array | No | | Aggiungi un array di campi fornito per raccogliere i metadati dall’utente. Utilizzando questa proprietà, puoi anche utilizzare metadati nascosti che vengono assegnati automaticamente a una risorsa ma non sono visibili all’utente. |
| *onMetadataFormChange* | Funzione callback | No | | È costituito da `property` e `value`. `Property` è uguale a *mapToProperty* del campo passato da *metadataSchema* il cui valore è in fase di aggiornamento. Mentre,`value` è uguale al nuovo valore fornito come input. |
| *targetUploadPath* | Stringa |  | `"/content/dam"` | Percorso di caricamento di destinazione per i file che per impostazione predefinita sono nella directory principale dell’archivio delle risorse. |
| *nascondiPulsanteCaricamento* | Booleano | | Falso | In questo modo viene garantito se il pulsante Caricamento interno deve essere nascosto o meno. |
| *onUploadStart* | Funzione | No |  | Si tratta di una funzione di callback utilizzata per passare l&#39;origine di caricamento tra Dropbox, OneDrive o locale. La sintassi è `(uploadInfo: UploadInfo) => void` |
| *importSettings* | Funzione | | | Abilita il supporto per l’importazione di risorse da origini terze. `sourceTypes` utilizza un array delle origini di importazione che si desidera abilitare. Le origini supportate sono Onedrive e Dropbox. La sintassi è `{ sourceTypes?: ImportSourceType[]; apiKey?: string; }` |
| *onUploadComplete* | Funzione | No | | Si tratta di una funzione di callback utilizzata per passare lo stato di caricamento del file tra completato, non riuscito o duplicato. La sintassi è `(uploadStats: UploadStats) => void` |
| *onFilesChange* | Funzione | No | | Si tratta di una funzione di callback utilizzata per mostrare il comportamento di caricamento quando un file viene modificato. Trasmette il nuovo array di file in attesa di caricamento e il tipo di origine del caricamento. Il tipo di Source può essere nullo in caso di errore. La sintassi è `(newFiles: File[], uploadType: UploadType) => void` |
| *uploadingPlaceholder* | Stringa | | | È un’immagine segnaposto che sostituisce il modulo metadati quando viene avviato il caricamento della risorsa. La sintassi è `{ href: string; alt: string; } ` |
| *uploadConfig* | Oggetto | | | Si tratta di un oggetto che contiene una configurazione personalizzata per il caricamento. |
| *featureSet* | Array | Stringa | | La proprietà `featureSet:[ ]` viene utilizzata per abilitare o disabilitare una particolare funzionalità nell&#39;applicazione Asset Selector. Per abilitare un componente o una funzione, puoi passare un valore stringa nell’array oppure lasciare vuoto l’array per disabilitare tale componente. Ad esempio, per abilitare la funzionalità di caricamento nel selettore risorse, utilizza la sintassi `featureSet:[0:"upload"]`. |

<!--
| *rootPath* | String | No | /content/dam/ | Folder path from which Asset Selector displays your assets. `rootPath` can also be used in the form of encapsulation. For example, given the following path, `/content/dam/marketing/subfolder/`, Asset Selector does not allow you to traverse through any parent folder, but only displays the children folders. |
| *path* | String | No | | Path that is used to navigate to a specific directory of assets when the Asset Selector is rendered. |
| *expirationDate* | Function | No | | This function is used to set the usability period of an asset. |
| *disableDefaultBehaviour* | Boolean | No | False | It is a function that is used to enable or disable the selection of an expired asset. You can customize the default behavior of an asset that is set to expire. See [customize expired assets](/help/assets/asset-selector-customization.md#customize-expired-assets). |
-->
