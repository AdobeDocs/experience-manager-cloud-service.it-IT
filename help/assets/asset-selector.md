---
title: Selettore risorse per [!DNL Adobe Experience Manager] come [!DNL Cloud Service]
description: Utilizza il selettore delle risorse per cercare, trovare e recuperare i metadati e le rappresentazioni delle risorse all’interno dell’applicazione.
contentOwner: Adobe
role: Admin,User
source-git-commit: 22d2a2235c8696fce76369d3ffe369bcbaa3f6f2
workflow-type: tm+mt
source-wordcount: '2355'
ht-degree: 3%

---


# Selettore risorsa microfrontale {#Overview}

Il selettore delle risorse Micro-Frontend fornisce un’interfaccia utente che si integra facilmente con [!DNL Experience Manager Assets as a Cloud Service] in modo da poter sfogliare o cercare le risorse digitali disponibili nell’archivio e utilizzarle nell’esperienza di authoring delle applicazioni.

L’interfaccia utente Micro-Frontend è resa disponibile nell’esperienza dell’applicazione utilizzando il pacchetto Asset Selector (Selettore risorse). Eventuali aggiornamenti al pacchetto vengono importati automaticamente e il Selettore risorse implementato più recente viene caricato automaticamente all’interno dell’applicazione.

![Panoramica](assets/overview.png)

Il Selettore risorse offre molti vantaggi, ad esempio:

* Facilità di integrazione con qualsiasi applicazione Adobe o non Adobe che utilizza la libreria JavaScript di Vanilla.
* Facile da mantenere, poiché gli aggiornamenti al pacchetto Selettore risorse vengono distribuiti automaticamente sul Selettore risorse disponibile per la tua applicazione. Non sono necessari aggiornamenti all’interno dell’applicazione per caricare le modifiche più recenti.
* Facilità di personalizzazione in quanto sono disponibili proprietà che controllano la visualizzazione del Selettore risorse all’interno dell’applicazione.

* Filtri di ricerca full-text, preconfigurati e personalizzati per individuare rapidamente le risorse da utilizzare nell’esperienza di authoring.

* Possibilità di cambiare archivi all’interno di un’organizzazione IMS per la selezione delle risorse.

* Possibilità di ordinare le risorse in base al nome, alle dimensioni e alle dimensioni e di visualizzarle nelle viste Elenco, Griglia, Galleria o Cascata.

Esegui le seguenti operazioni per integrare e utilizzare il Selettore risorse con il tuo [!DNL Experience Manager Assets as a Cloud Service] archivio:

* [Integrare il selettore delle risorse utilizzando Vaniglia JS](#integration-with-vanilla-js)
* [Definire le proprietà di visualizzazione del selettore risorse](#asset-selector-properties)
* [Usa selettore risorse](#using-asset-selector)

## Integrare il selettore delle risorse utilizzando Vaniglia JS {#integration-with-vanilla-js}

È possibile integrare qualsiasi [!DNL Adobe] o applicazione non Adobe con [!DNL Experience Manager Assets] come [!DNL Cloud Service] e seleziona le risorse dall’interno dell’applicazione.

L’integrazione viene eseguita importando il pacchetto Asset Selector (Selettore risorse) e connettendosi alle risorse as a Cloud Service utilizzando la libreria JavaScript di vaniglia. È necessario modificare un `index.html` o qualsiasi file appropriato all&#39;interno della tua applicazione a -
* Definire i dettagli di autenticazione
* Accedere all’archivio as a Cloud Service di Assets
* Configurare le proprietà di visualizzazione del Selettore risorse

<!--
Asset Selector supports authentication to the [!DNL Experience Manager Assets] as a [!DNL Cloud Service] repository using Identity Management System (IMS) properties such as `imsScope` or `imsClientID`. Authentication using these IMS properties is referred to as SUSI (Sign Up Sign In) flow in this article.

You can perform authentication without defining some of the IMS properties, such as `imsScope` or `imsClientID`, if:

*   You are integrating an [!DNL Adobe] application on [Unified Shell](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/aem-cloud-service-on-unified-shell.html?lang=en).
*   You already have an IMS token generated for authentication.

Accessing [!DNL Experience Manager Assets] as a [!DNL Cloud Service] repository without defining `imsScope` or `imsClientID` IMS properties is referred to as a non-SUSI flow in this article.
-->

Puoi eseguire l’autenticazione senza definire alcune delle proprietà IMS, se:

* Stai integrando un [!DNL Adobe] applicazione [Shell unificata](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/aem-cloud-service-on-unified-shell.html?lang=en).
* Hai già generato un token IMS per l’autenticazione.

## Prerequisiti {#prerequisites}

<!--
If your application requires user based authentication, out-of-the-box Asset Selector also supports a flow for authentication to the [!DNL Experience Manager Assets] as a [!DNL Cloud Service] repository using Identity Management System (IMS.)

You can use properties such as `imsScope` or `imsClientID` to retrieve `imsToken` automatically. You can use SUSI (Sign Up Sign In) flow and IMS properties. Also, you can obtain your own imsToken and pass it to Asset Selector by integrating within [!DNL Adobe] application on Unified Shell or if you already have an imsToken obtained via other methods (for example, using technical account). Accessing [!DNL Experience Manager Assets] as a [!DNL Cloud Service] repository without defining IMS properties (For example, `imsScope` and `imsClientID`) is referred to as a non-SUSI flow.
-->

Definisci i prerequisiti nella `index.html` file o un file simile all’interno dell’implementazione dell’applicazione per definire i dettagli di autenticazione per accedere al [!DNL Experience Manager Assets] come [!DNL Cloud Service] archivio. I prerequisiti includono:
* imsOrg
* imsToken
* apikey

<!--
The prerequisites vary if you are authenticating using a SUSI flow or a non-SUSI flow.

**Non-SUSI flow**

*   imsOrg
*   imsToken
*   apikey

For more information on these properties, refer to [Asset Selector Properties](#asset-selector-properties).

**SUSI flow**

*   imsClientId
*   imsScope
*   redirectUrl
*   imsOrg
*   apikey

For more information on these properties, refer to [Example for the SUSI flow](#susi-vanilla) and [Asset Selector Properties](#asset-selector-properties).
-->

## Installazione {#installation}

I selettori delle risorse sono disponibili tramite ESM CDN (ad esempio, [esm.sh](https://esm.sh/)/[skypack](https://www.skypack.dev/)) e [UMD](https://github.com/umdjs/umd) versione.

Nei browser che utilizzano **Versione UMD** (consigliato):

```
<script src="https://experience.adobe.com/solutions/CQ-assets-selectors/assets/resources/assets-selectors.js"></script>

<script>
  const { renderAssetSelector } = PureJSSelectors;
</script>
```

Nei browser con `import maps` supporto tramite **Versione ESM CDN**:

```
<script type="module">
  import { AssetSelector } from 'https://experience.adobe.com/solutions/CQ-assets-selectors/assets/resources/@assets/selectors/index.js'
</script>
```

Nella federazione dei moduli Deno/Webpack utilizzando **Versione ESM CDN**:

```
import { AssetSelector } from 'https://experience.adobe.com/solutions/CQ-assets-selectors/assets/resources/@assets/selectors/index.js'
```

### Tipo di risorsa selezionato {#selected-asset-type}

Il tipo di risorsa selezionato è una matrice di oggetti che contiene le informazioni sulla risorsa quando si utilizza il `handleSelection`, `handleAssetSelection`e `onDrop` funzioni.

**Sintassi dello schema**

```
interface SelectedAsset {
    'repo:id': string;
    'repo:name': string;
    'repo:path': string;
    'repo:size': number;
    'repo:createdBy': string;
    'repo:createDate': string;
    'repo:modifiedBy': string; 
    'repo:modifyDate': string; 
    'dc:format': string; 
    'tiff:imageWidth': number;
    'tiff:imageLength': number;
    'repo:state': string;
    computedMetadata: Record<string, any>;
    _links: {
        'http://ns.adobe.com/adobecloud/rel/rendition': Array<{
            href: string;
            type: string;
            'repo:size': number;
            width: number;
            height: number;
            [others: string]: any;
        }>;
    };
}
```

Nella tabella seguente sono illustrate alcune delle proprietà importanti dell’oggetto Risorsa selezionata.

| Proprietà | Tipo | Spiegazione |
|---|---|---|
| *repo:repositoryId* | stringa | Identificatore univoco per il repository in cui è memorizzata la risorsa. |
| *repo:id* | stringa | Identificatore univoco della risorsa. |
| *repo:assetClass* | stringa | La classificazione della risorsa (ad esempio, immagine o video, documento). |
| *repo:name* | stringa | Il nome della risorsa, inclusa l’estensione del file. |
| *repo:dimensioni* | numero | Dimensione della risorsa in byte. |
| *repo:path* | stringa | La posizione della risorsa all’interno dell’archivio. |
| *repo:predecessori* | `Array<string>` | Matrice di elementi precedenti per la risorsa nell’archivio. |
| *repo:state* | stringa | Stato corrente della risorsa nell’archivio (ad esempio, attiva, eliminata, ecc.). |
| *repo:createdBy* | stringa | L’utente o il sistema che ha creato la risorsa. |
| *repo:createDate* | stringa | La data e l’ora di creazione della risorsa. |
| *repo:modifiedBy* | stringa | L’utente o il sistema che ha modificato la risorsa per l’ultima volta. |
| *repo:modifyDate* | stringa | Data e ora dell’ultima modifica apportata alla risorsa. |
| *dc:format* | stringa | Il formato della risorsa, ad esempio il tipo di file (ad esempio, JPEG, PNG, ecc.). |
| *tiff:imageWidth* | numero | Larghezza di una risorsa. |
| *tiff:imageLength* | numero | Altezza di una risorsa. |
| *computedMetadata* | `Record<string, any>` | Un oggetto che rappresenta un bucket per tutti i metadati della risorsa di tutti i tipi (archivio, applicazione o metadati incorporati). |
| *_collegamenti* | `Record<string, any>` | Collegamenti ipertestuali per la risorsa associata. Include i collegamenti per risorse quali metadati e rappresentazioni. |
| *_links.http://ns.adobe.com/adobecloud/rel/rendition* | `Array<Object>` | Array di oggetti contenenti informazioni sui rendering della risorsa. |
| *_links.http://ns.adobe.com/adobecloud/rel/rendition[].href* | stringa | URI del rendering. |
| *_links.http://ns.adobe.com/adobecloud/rel/rendition[].type* | stringa | Il tipo MIME del rendering. |
| *_links.http://ns.adobe.com/adobecloud/rel/rendition[].&quot;repo:size* | numero | Dimensione del rendering in byte. |
| *_links.http://ns.adobe.com/adobecloud/rel/rendition[].width* | numero | Larghezza del rendering. |
| *_links.http://ns.adobe.com/adobecloud/rel/rendition[].height* | numero | Altezza del rendering. |

Per un elenco completo delle proprietà e un esempio dettagliato, visita [Esempio di codice del selettore risorse](https://github.com/adobe/aem-assets-selectors-mfe-examples).

<!--
### ImsAuthProps {#ims-auth-props}

The `ImsAuthProps` properties define the authentication information and flow that the Asset Selector uses to obtain an `imsToken`. By setting these properties, you can control how the authentication flow should behave and register listeners for various authentication events.

| Property Name | Description|
|---|---|
| `imsClientId`| A string value representing the IMS client ID used for authentication purposes. This value is provided by Adobe and is specific to your Adobe AEM CS organization.|
| `imsScope`| Describes the scopes used in authentication. The scopes determine the level of access that the application has to your organization resources. Multiple scopes can be separated by commas.|
| `redirectUrl` | Represents the URL where the user is redirected after authentication. This value is typically set to the current URL of the application. If a `redirectUrl` is not supplied, `ImsAuthService` will use the redirectUrl used to register the `imsClientId`|
| `modalMode`| A boolean indicating whether the authentication flow should be displayed in a modal (pop-up) or not. If set to `true`, the authentication flow is displayed in a pop-up. If set to `false`, the authentication flow is displayed in a full page reload. _Note:_ for better UX, you can dynamically control this value if the user has browser pop-up disabled. |
| `onImsServiceInitialized`| A callback function that is called when the Adobe IMS authentication service is initialized. This function takes one parameter, `service`, which is an object representing the Adobe IMS service. See [`ImsAuthService`](#imsauthservice-ims-auth-service) for more details.|
| `onAccessTokenReceived`| A callback function that is called when an `imsToken` is received from the Adobe IMS authentication service. This function takes one parameter, `imsToken`, which is a string representing the access token. |
| `onAccessTokenExpired`| A callback function that is called when an access token has expired. This function is typically used to trigger a new authentication flow to obtain a new access token. |
| `onErrorReceived`| A callback function that is called when an error occurs during authentication. This function takes two parameters: the error type and error message. The error type is a string representing the type of error and the error message is a string representing the error message. |

### ImsAuthService {#ims-auth-service}

`ImsAuthService` class handles the authentication flow for the Asset Selector. It is responsible for obtaining an `imsToken` from the Adobe IMS authentication service. The `imsToken` is used to authenticate the user and authorize access to the Adobe Experience Manager (AEM) CS Assets repository. ImsAuthService uses the `ImsAuthProps` properties to control the authentication flow and register listeners for various authentication events. You can use the convenient [`registerAssetsSelectorsAuthService`](#purejsselectorsregisterassetsselectorsauthservice) function to register the _ImsAuthService_ instance with the Asset Selector. The following functions are available on the `ImsAuthService` class. However, if you're using the _registerAssetsSelectorsAuthService_ function, you do not need to call these functions directly.

| Function Name | Description |
|---|---|
| `isSignedInUser` | Determines whether the user is currently signed in to the service and returns a boolean value accordingly.|
| `getImsToken`    | Retrieves the authentication `imsToken` for the currently signed-in user, which can be used to authenticate requests to other services such as generating asset _rendition.|
| `signIn`| Initiates the sign-in process for the user. This function uses the `ImsAuthProps` to show authentication in either a pop-up or a full page reload |
| `signOut`| Signs the user out of the service, invalidating their authentication token and requiring them to sign in again to access protected resources. Invoking this function will reload the current page.|
| `refreshToken`| Refreshes the authentication token for the currently signed-in user, preventing it from expiring and ensuring uninterrupted access to protected resources. Returns a new authentication token that can be used for subsequent requests. |
-->

### Esempio per il flusso non SUSI {#non-susi-vanilla}

Questo esempio illustra come utilizzare il selettore delle risorse con un flusso non SUSI durante l’esecuzione di un [!DNL Adobe] applicazione sotto Unified Shell o quando hai già `imsToken` generato per l&#39;autenticazione.

Includere il pacchetto Asset Selector nel codice utilizzando `script` , come mostrato in _linee da 6 a 15_ dell&#39;esempio seguente. Una volta caricato lo script, il `PureJSSelectors` la variabile globale è disponibile per l&#39;uso. Definire il selettore delle risorse [proprietà](#asset-selector-properties) come mostrato in _linee da 16 a 23_. La `imsOrg` e `imsToken` le proprietà sono entrambe necessarie per l’autenticazione nel flusso non SUSI. La `handleSelection` viene utilizzata per gestire le risorse selezionate. Per eseguire il rendering del selettore delle risorse, chiama il `renderAssetSelector` come indicato in _linea 17_. Il selettore delle risorse viene visualizzato nella sezione `<div>` elemento contenitore , come mostrato in _linee 21 e 22_.

Seguendo questi passaggi, puoi utilizzare il Selettore risorse con un flusso non SUSI nel tuo [!DNL Adobe] applicazione.

```html {line-numbers="true"}
<!DOCTYPE html>
<html>
<head>
    <title>Asset Selector</title>
    <script src="https://experience.adobe.com/solutions/CQ-assets-selectors/assets/resources/assets-selectors.js"></script>
    <script>
        // get the container element in which we want to render the AssetSelector component
        const container = document.getElementById('asset-selector-container');
        // imsOrg and imsToken are required for authentication in non-SUSI flow
        const assetSelectorProps = {
            imsOrg: 'example-ims@AdobeOrg',
            imsToken: "example-imsToken",
            apiKey: "example-apiKey-associated-with-imsOrg",
            handleSelection: (assets: SelectedAssetType[]) => {},
        };
        // Call the `renderAssetSelector` available in PureJSSelectors globals to render AssetSelector
        PureJSSelectors.renderAssetSelector(container, assetSelectorProps);
    </script>
</head>

<body>
    <div id="asset-selector-container" style="height: calc(100vh - 80px); width: calc(100vw - 60px); margin: -20px;">
    </div>
</body>

</html>
```

Ad esempio, visita [Esempio di codice del selettore risorse](https://github.com/adobe/aem-assets-selectors-mfe-examples).

<!--
### Example for the SUSI flow {#susi-vanilla}

Use this example `index.html` file for authentication if you are integrating your application using SUSI flow.

Access the Asset Selector package using the `Script` Tag, as shown in *line 9* to *line 11* of the example `index.html` file.

*Line 14* to *line 38* of the example describes the IMS flow properties, such as `imsClientId`, `imsScope`, and `redirectURL`. The function requires that you define at least one of the `imsClientId` and `imsScope` properties. If you do not define a value for `redirectURL`, the registered redirect URL for the client ID is used.

As you do not have an `imsToken` generated, use the `registerAssetsSelectorsAuthService` and `renderAssetSelectorWithAuthFlow` functions, as shown in line 40 to line 50 of the example `index.html` file. Use the `registerAssetsSelectorsAuthService` function before `renderAssetSelectorWithAuthFlow` to register the `imsToken` with the Asset Selector. [!DNL Adobe] recommends to call `registerAssetsSelectorsAuthService` when you instantiate the component.

Define the authentication and other Assets as a Cloud Service access-related properties in the `const props` section, as shown in *line 54* to *line 60* of the example `index.html` file.

The `PureJSSelectors` global variable, mentioned in *line 65*, is used to render the Asset Selector in the web browser.

Asset Selector is rendered on the `<div>` container element, as mentioned in *line 74* to *line 81*. The example uses a dialog to display the Asset Selector.

```html {line-numbers="true"}
<!DOCTYPE html>
<html>

<head>
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta charset="utf-8">
    <title>Asset Selectors</title>
    <link rel="stylesheet" href="index.css">
    <script id="asset-selector"
        src="https://experience.adobe.com/solutions/CQ-assets-selectors/assets/resources/asset-selectors.js"></script>
    <script>

        const imsProps = {
            imsClientId: "<obtained from IMS team>",
            imsScope: "openid, <other scopes>",
            redirectUrl: window.location.href,
            modalMode: true, // false to open in a full page reload flow
            onImsServiceInitialized: (service) => {
                // invoked when the ims service is initialized and is ready
                console.log("onImsServiceInitialized", service);
            },
            onAccessTokenReceived: (token) => {
                console.log("onAccessTokenReceived", token);
            },
            onAccessTokenExpired: () => {
                console.log("onAccessTokenError");
                // re-trigger sign-in flow
            },
            onErrorReceived: (type, msg) => {
                console.log("onErrorReceived", type, msg);
            },
        }

        function load() {
            const registeredTokenService = PureJSSelectors.registerAssetsSelectorsAuthService(imsProps);
            imsInstance = registeredTokenService;
        };

        // initialize the IMS flow before attempting to render the asset selector
        load();
        

        //function that will render the asset selector
            const otherProps = {
            // any other props supported by asset selector
            }
            const assetSelectorProps = {
                "imsOrg": "imsorg",
                ...otherProps
            }
             // container element on which you want to render the AssetSelector/DestinationSelector component
            const container = document.getElementById('asset-selector');

            /// Use the PureJSSelectors in globals to render the AssetSelector/DestinationSelector component
            PureJSSelectors.renderAssetSelectorWithAuthFlow(container, assetSelectorProps, () => {
                const assetSelectorDialog = document.getElementById('asset-selector-dialog');
                assetSelectorDialog.showModal();
            });
        }
    </script>

</head>
<body class="asset-selectors">
    <div>
        <button onclick="renderAssetSelectorWithAuthFlowFlow()">Asset Selector - Select Assets with Ims Flow</button>
    </div>
        <dialog id="asset-selector-dialog">
            <div id="asset-selector" style="height: calc(100vh - 80px); width: calc(100vw - 60px); margin: -20px;">
            </div>
        </dialog>
    </div>
</body>

</html>

```
-->

## Utilizzare le proprietà del selettore risorse {#asset-selector-properties}

Puoi utilizzare le proprietà del selettore delle risorse per personalizzare il modo in cui viene eseguito il rendering del selettore delle risorse. Nella tabella seguente sono elencate le proprietà che è possibile utilizzare per personalizzare e utilizzare il selettore risorse.

| Proprietà | Tipo | Obbligatorio | Predefiniti | Descrizione |
|---|---|---|---|---|
| *barra* | booleano | No | false | Se contrassegnato `true`, il selettore risorse viene rappresentato nella vista a sinistra. Se è contrassegnato `false`, il selettore delle risorse verrà riprodotto in visualizzazione modale. |
| *imsOrg* | stringa | Sì |  | ID di sistema Adobe Identity Management (IMS) assegnato durante il provisioning [!DNL Adobe Experience Manager] come [!DNL Cloud Service] per la tua organizzazione. La `imsOrg` per autenticare l&#39;organizzazione a cui stai accedendo è necessario utilizzare Adobe IMS o meno. |
| *imsToken* | stringa | No |  | Token portatore IMS utilizzato per l’autenticazione. `imsToken` non è richiesto se utilizzi il flusso SUSI. Tuttavia, è necessario se utilizzi il flusso non SUSI. |
| *apiKey* | stringa | No |  | Chiave API utilizzata per accedere al servizio AEM Discovery. `apiKey` non è richiesto se utilizzi il flusso SUSI. Tuttavia, è richiesto nel flusso non SUSI. |
| *rootPath* | stringa | No | /content/dam/ | Percorso cartella da cui vengono visualizzate le risorse. `rootPath` può essere utilizzato anche sotto forma di incapsulamento. Ad esempio, dato il seguente percorso, `/content/dam/marketing/subfolder/`, il Selettore risorse non consente di scorrere in nessuna cartella principale, ma visualizza solo le cartelle figlie. |
| *percorso* | stringa | No |  | Percorso utilizzato per passare a una directory specifica di risorse quando viene eseguito il rendering del selettore delle risorse. |
| *filterSchema* | array | No |  | Modello utilizzato per configurare le proprietà del filtro. Questa funzione è utile quando desideri limitare determinate opzioni di filtro nel Selettore risorse. |
| *filterFormProps* | Oggetto | No |  | Specifica le proprietà del filtro da utilizzare per perfezionare la ricerca. Ad esempio, tipo MIME JPG, PNG, GIF. |
| *selectedAssets* | Array `<Object>` | No |  | Specifica le risorse selezionate quando viene eseguito il rendering del selettore delle risorse. È necessario un array di oggetti che contenga una proprietà id delle risorse. Ad esempio: `[{id: 'urn:234}, {id: 'urn:555'}]` Una risorsa deve essere disponibile nella directory corrente. Se devi utilizzare una directory diversa, fornisci un valore per `path` anche proprietà. |
| *acvConfig* | Oggetto | No |  | Proprietà Vista raccolta risorse contenente un oggetto contenente una configurazione personalizzata che sostituisce i valori predefiniti. |
| *i18nSymbols* | `Object<{ id?: string, defaultMessage?: string, description?: string}>` | No |  | Se le traduzioni OOTB non sono sufficienti per le esigenze dell&#39;applicazione, puoi esporre un&#39;interfaccia attraverso la quale puoi trasmettere i tuoi valori localizzati personalizzati attraverso `i18nSymbols` prop. Il passaggio di un valore tramite questa interfaccia sostituisce le traduzioni predefinite fornite e utilizza le tue.  Per eseguire l&#39;override, è necessario trasmettere un valore valido [Descrittore messaggio](https://formatjs.io/docs/react-intl/api/#message-descriptor) alla chiave di `i18nSymbols` che si desidera ignorare. |
| *intl* | Oggetto | No |  | Il Selettore risorse fornisce traduzioni OOTB predefinite. È possibile selezionare la lingua di traduzione fornendo una stringa valida per le impostazioni internazionali tramite `intl.locale` prop. Ad esempio: `intl={{ locale: "es-es" }}` </br></br> Le stringhe internazionali supportate seguono le [ISO 639 - Codici](https://www.iso.org/iso-639-language-codes.html) per la rappresentazione dei nomi delle norme linguistiche. </br></br> Elenco delle impostazioni internazionali supportate: Inglese - &#39;en-us&#39; (predefinito) Spagnolo - &#39;es-es&#39; Tedesco - &#39;de-de&#39; Francese - &#39;fr-fr&#39; Italiano - &#39;it-it&#39; Giapponese - &#39;ja-jp&#39; Coreano - &#39;ko-kr&#39; Portoghese - &#39;pt-br&#39; Cinese (tradizionale) - &#39;zh-cn&#39; Cinese (Taiwan) - &#39;zh-tw&#39; |
| *repositoryId* | stringa | No | &#39;&#39; | Archivio da cui il Selettore risorse carica il contenuto. |
| *additionalAemSolutions* | `Array<string>` | No | [ ] | Ti consente di aggiungere un elenco di archivi AEM aggiuntivi. Se non viene fornita alcuna informazione in questa proprietà, vengono considerati solo archivi AEM Assets o media library. |
| *hideTreeNav* | booleano | No |  | Specifica se visualizzare o nascondere la barra laterale di navigazione della struttura delle risorse. Viene utilizzato solo nella visualizzazione modale e quindi non vi è alcun effetto di questa proprietà nella visualizzazione a barre. |
| *onDrop* | Funzione | No |  | La proprietà consente la funzionalità di rilascio di una risorsa. |
| *dropOptions* | `{allowList?: Object}` | No |  | Configura le opzioni di rilascio utilizzando &quot;inserire nell&#39;elenco Consentiti&quot;. |
| *colorScheme* | stringa | No |  | Configura il tema (`light` o `dark`) per il Selettore risorse. |
| *handleSelection* | Funzione | No |  | Viene richiamato con una matrice di elementi risorsa quando vengono selezionate le risorse e il `Select` fai clic sul pulsante modale . Questa funzione viene richiamata solo nella visualizzazione modale. Per la visualizzazione a barre, utilizza la funzione `handleAssetSelection` o `onDrop` funzioni. Esempio: <pre>handleSelection=(assets: Risorsa[])=> {..}</pre> Vedi [Tipo di risorsa selezionato](#selected-asset-type) per i dettagli. |
| *handleAssetSelection* | Funzione | No |  | Viene richiamato con una matrice di elementi mentre le risorse vengono selezionate o deselezionate. Questa funzione è utile quando si desidera ascoltare le risorse selezionate dall’utente. Esempio: <pre>handleSelection=(assets: Risorsa[])=> {..}</pre> Vedi [Tipo di risorsa selezionato](#selected-asset-type) per i dettagli. |
| *onClose* | Funzione | No |  | Richiamato quando `Close` nella visualizzazione modale viene premuto il pulsante . Viene richiamato solo `modal` visualizza e ignora `rail` visualizza. |
| *onFilterSubmit* | Funzione | No |  | Richiamato con elementi di filtro quando l’utente modifica criteri di filtro diversi. |
| *selectionType* | stringa | No | singolo | Configurazione per `single` o `multiple` selezione delle risorse alla volta. |

## Esempi per utilizzare le proprietà del selettore risorse {#usage-examples}

Puoi definire il Selettore risorse [proprietà](#asset-selector-properties) in `index.html` per personalizzare la visualizzazione del Selettore risorse all’interno dell’applicazione.

### Esempio 1: Selettore risorse nella vista a barre

![esempio di barra](assets/rail-view-example-vanilla.png)

Se il valore di AssetSelector `rail` è impostato su `false` oppure non è menzionato nelle proprietà, il Selettore risorse viene visualizzato nella vista Modale per impostazione predefinita.

<!--
### Example 2: Use selectedAssets property in addition to the path property

Use the `path` property to define the folder name that displays automatically when the Asset Selector is rendered. In addition, use the `selectedAssets` property to define the IDs for the assets that you need to select within the folder. Moreover, when you want to display assets that are pre-defined within the folder, you can use selectedAssets property.

   ![selected-assets-example](assets/selected-assets-example-vanilla.png)
-->

### Esempio 2: Puntatore metadati

Utilizza varie proprietà per definire i metadati di una risorsa da visualizzare tramite un’icona di informazioni. Il componente informazioni fornisce la raccolta di informazioni sulla risorsa o sulla cartella, tra cui titolo, dimensioni, data di modifica, posizione e descrizione di una risorsa. Nell’esempio seguente, diverse proprietà vengono utilizzate per visualizzare i metadati di una risorsa, ad esempio: `repo:path` specifica la posizione di una risorsa. <!--`repo` represents the repository from where the asset is showing, whereas, `path` represents the route from where the asset or folder is rendered.-->

![metadata-popopover-example](assets/metadata-popover.png)


### Esempio 3: Proprietà filtro personalizzato nella vista a barre

Oltre alla ricerca sfaccettata, il selettore delle risorse ti consente di personalizzare vari attributi per perfezionare la ricerca da [!DNL Adobe Experience Manager] come [!DNL Cloud Service] applicazione. Per aggiungere filtri di ricerca personalizzati nella tua applicazione, devi aggiungere il codice seguente. Nell’esempio seguente, la `Type Filter` cerca che filtra il tipo di risorsa tra Immagini, Documenti o Video o il tipo di filtro aggiunto per la ricerca.

![custom-filter-example-vanilla](assets/custom-filter-example-vanilla.png)

<!--

## Customization after integrating Asset Selector 

### Custom metadata

Assets display panel shows the out of the box metadata that can be displayed in the info of the asset. In addition to this, [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] application allows configuration of the asset selector by adding custom metadata that is shown in info panel of the asset.
-->

<!-- Property details to be added here. Referred the ticket https://jira.corp.adobe.com/browse/ASSETS-19023-->

<!--
## Asset Selector Object Schema {#object-schema}

Schema describes the object properties associated with an asset selected using Asset Selector. It uses the combination of data types and their values to validate the object describing the selected Asset using an Asset Selector.

**Schema Syntax**
````
interface SelectedAsset {
    'repo:id': string;
    'repo:name': string;
    'repo:path': string;
    'repo:size': number;
    'repo:createdBy': string;
    'repo:createDate': string;
    'repo:modifiedBy': string; 
    'repo:modifyDate': string; 
    'dc:format': string; 
    'tiff:imageWidth': number;
    'tiff:imageLength': number;
    'repo:state': string;
    computedMetadata: Record<string, any>;
    _links: {
        'http://ns.adobe.com/adobecloud/rel/rendition': Array<{
            href: string;
            type: string;
            'repo:size': number;
            width: number;
            height: number;
            [others: string]: any;
        }>;
    };
}
````

**Query Parameters**

| Parameter | Type | Description |
|---|---|---|
| repo:id | string | ID of an Asset |
| repo:name | string | The name of an Asset |
| repo:path | string | The path of an Asset |
| repo:size | number | Size of an Asset (in bytes) |
| repo:createdBy | string | ID of a user who created an Asset |
| repo: createdDate | string | The timestamp when an asset was created |
| repo:modifiedBy | string | ID of a user who modified the asset recently |
| repo:modifyDate | string | The timestamp when the asset was last modified |
| dc:format | string | MIME type of an Asset |
| tiff:imageWidth | number | The width of an image type of Asset |
| tiff:imageLength | number | The height of an image type of Asset |
| repo:state | string | The `Approved`, `Rejected`, or `Expired`state of an Asset |
| computedMetadata | string | It is an object that represents a bucket for all the Asset's metadata of all kinds (repository, application or embedded metadata) |
| _links | string | It represents the collection of links used in the Asset Selector. The links are represented in the form of an array. The parameters of an array include: `href`, `type`, `repo:size`, `width`, `height`, etc.  |

For the detailed example of Object Schema, click 
-->

## Gestione della selezione delle risorse tramite lo schema oggetto {#handling-selection}

La `handleSelection` viene utilizzata per gestire selezioni singole o multiple di Assets nel Selettore risorse. L’esempio seguente illustra la sintassi dell’utilizzo di `handleSelection`.

![selezione della maniglia](assets/handling-selection.png)

## Utilizzo del selettore risorse {#using-asset-selector}

Una volta configurato il Selettore risorse e autenticato per utilizzare il Selettore risorse con il [!DNL Adobe Experience Manager] come [!DNL Cloud Service] , puoi selezionare le risorse o eseguire varie altre operazioni per cercare le risorse all’interno dell’archivio.

![selettore di risorse](assets/using-asset-selector.png)

* **A**: [Nascondi/Mostra pannello](#hide-show-panel)
* **B**: [Switcher archivio](#repository-switcher)
* **C**: [Risorse](#repository)
* **D**: [Filtri](#filters)
* **E**: [Barra di ricerca](#search-bar)
* **F**: [Ordinamento](#sorting)
* **G**: [Ordinamento in ordine crescente o decrescente](#sorting)
* **H**: [Visualizza](#types-of-view)

### Nascondi/Mostra pannello {#hide-show-panel}

Per nascondere le cartelle nella navigazione a sinistra, fai clic su **[!UICONTROL Nascondi cartelle]** icona. Per annullare le modifiche, fai clic sul pulsante **[!UICONTROL Nascondi cartelle]** icona di nuovo.

### Switcher archivio {#repository-switcher}

Il Selettore risorse consente inoltre di cambiare archivi per la selezione delle risorse. Puoi selezionare l’archivio desiderato dal menu a discesa disponibile nel pannello a sinistra. Le opzioni dell’archivio disponibili nell’elenco a discesa sono basate sulle `repositoryId` definita nella `index.html` file. Si basa sugli ambienti dell’organizzazione IMS selezionata a cui l’utente ha effettuato l’accesso. I consumatori possono passare un `repositoryID` e in tal caso il Selettore risorse smette di eseguire il rendering del commutatore repo ed esegue il rendering delle risorse solo dal repository specificato.
<!--
It is based on the `imsOrg` that is provided in the application. If you want to see the list of repositories, then `repositoryId` is required to view those specific repositories in your application.
-->

### Archivio risorse

Si tratta di una raccolta di cartelle di risorse utilizzabili per eseguire operazioni.

### Filtri predefiniti {#filters}

Il selettore risorse offre anche opzioni di filtro predefinite per perfezionare i risultati della ricerca. Sono disponibili i seguenti filtri:

* `File type`: include cartelle, file, immagini, documenti o video
* `MIME type`: include JPG, GIF, PPTX, PNG, MP4, DOCX, TIFF, PDF, XLSX
* `Image Size`: include larghezza minima/massima, altezza minima/massima dell&#39;immagine

![esempio di barra](assets/filters-asset-selector.png)

### Ricerca personalizzata

Oltre alla ricerca full-text, il Selettore risorse ti consente di cercare le risorse all’interno dei file utilizzando una ricerca personalizzata. È possibile utilizzare filtri di ricerca personalizzati sia nella vista Modale che nella vista Barra.

![ricerca personalizzata](assets/custom-search.png)

È inoltre possibile creare un filtro di ricerca predefinito per salvare i campi che si cercano di frequente e utilizzarli in un secondo momento. Per creare una ricerca personalizzata per le risorse, puoi utilizzare `filterSchema` proprietà.

### Barra di ricerca {#search-bar}

Il Selettore risorse consente di eseguire una ricerca full-text delle risorse all’interno dell’archivio selezionato. Ad esempio, se digiti la parola chiave `wave` nella barra di ricerca, tutte le risorse con `wave` vengono visualizzate le parole chiave menzionate in una qualsiasi delle proprietà dei metadati.

### Ordinamento {#sorting}

Puoi ordinare le risorse in Selettore risorse per nome, dimensioni o dimensione di una risorsa. Puoi anche ordinare le risorse in ordine crescente o decrescente.

### Tipi di visualizzazioni {#types-of-view}

Il Selettore risorse consente di visualizzare la risorsa in quattro diverse viste:

* **![vista a elenco](assets/do-not-localize/list-view.png) [!UICONTROL Vista a elenco]**: Nella vista a elenco vengono visualizzati file e cartelle scorrevoli in un’unica colonna.
* **![vista a griglia](assets/do-not-localize/grid-view.png) [!UICONTROL Vista a griglia]**: Nella vista a griglia vengono visualizzati file e cartelle scorrevoli in una griglia di righe e colonne.
* **![vista a galleria](assets/do-not-localize/gallery-view.png) [!UICONTROL Vista a Galleria]**: Nella visualizzazione Galleria vengono visualizzati i file o le cartelle in un elenco orizzontale bloccato al centro.
* **![vista a cascata](assets/do-not-localize/waterfall-view.png) [!UICONTROL Vista a cascata]**: Nella vista a cascata vengono visualizzati file o cartelle sotto forma di Bridge.

<!--
### Modes to view Asset Selector

Asset Selector supports two types of out of the box views:

**  Modal view or Inline view:** The modal view or inline view is the default view of Asset Selector that represents Assets folders in the front area. The modal view allows users to view assets in a full screen to ease the selection of multiple assets for import. Use `<AssetSelector rail={false}>` to enable modal view.

    ![modal-view](assets/modal-view.png)

**  Rail view:** The rail view represents Assets folders in a left panel. The drag and drop of assets can be performed in this view. Use `<AssetSelector rail={true}>` to enable rail view.

    ![rail-view](assets/rail-view.png)
-->
<!--

### Application Integration

Asset Selector is flexible and can be integrated within your existing [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] application. It is accessible and localized to add, search, and select assets in your application. With Asset Selector you can:
*   **Configure** You can configure the files/folders that you want to show at the upfront. The assets that are chosen to view can be of any supported formats, for example, JPEG. It allows you to control the display of various text or symbols as per your choice.
*   **Perfect fit** Asset selector easily fits in your existing [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] application and choose the way you want to view. The mode of view can be inline, rail, or modal view.
*   **Accessible** With Asset Selector, you can reach the desired asset in an easy manner.
*   **Localize** Assets can be availed for the various locales available as per Adobe's localization standards.
-->
<!--

### Support for multiple instances

The micro front-end design supports the display of multiple instances of Asset Selector on a single screen.

![multiple-instance](assets/multiple-instance.png)
-->

<!--

### Controlled selection with multi-select

You can make default multi-selection of assets by specifying the assets to the component using `selectedAssets` property. You should specify an array of asset IDs. For example, `[{id: 'urn:234}, {id: 'urn:555'}].`
-->
<!--

### Action buttons

When you customize your application with Asset Selector based on ReactJS, you are provided with the following action buttons to perform various actions:
*   **Open in media library** Allows you to open the asset in media library.
*   **Upload** Allows you to upload an asset directly.
*   **Download** Downloads the asset in [!DNL Adobe Experience Manager] as a [!DNL Cloud Service].
-->
<!--

### Status of an asset

Asset Selector allows you to know the status of your uploaded assets. The status can be `Approved`, `Rejected`, or `Expired` of the asset. 
-->
<!--

### Localization

The integration of Asset Selector with [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] allows localized content appear in your application.
-->