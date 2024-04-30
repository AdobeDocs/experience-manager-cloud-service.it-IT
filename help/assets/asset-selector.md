---
title: Selettore risorse per [!DNL Adobe Experience Manager]  as a  [!DNL Cloud Service]
description: Utilizza il Selettore risorse per cercare, trovare e recuperare i metadati e le rappresentazioni delle risorse all’interno dell’applicazione.
contentOwner: KK
role: Admin,User
exl-id: b968f63d-99df-4ec6-a9c9-ddb77610e258
source-git-commit: b9fe6f4c2f74d5725575f225f8d9eb2e5fbfceb7
workflow-type: tm+mt
source-wordcount: '3908'
ht-degree: 45%

---


# Selettore risorse micro front-end {#Overview}

Il Selettore risorse micro front-end fornisce un’interfaccia utente che si integra facilmente con l’archivio di [!DNL Experience Manager Assets] in modo da poter sfogliare o cercare le risorse digitali disponibili nell’archivio e utilizzarle nell’esperienza di authoring dell’applicazione.

L’interfaccia utente micro front-end è resa disponibile nell’esperienza dell’applicazione utilizzando il pacchetto Selettore risorse. Eventuali aggiornamenti al pacchetto vengono importati automaticamente e l’ultimo Selettore risorse implementato viene caricato automaticamente all’interno dell’applicazione.

![Panoramica](assets/overview.png)

Il Selettore risorse offre molti vantaggi, tra cui:

* Facilità di integrazione con qualsiasi [Adobe](#asset-selector-ims) o [non Adobe](#asset-selector-non-ims) applicazioni che utilizzano la libreria JavaScript Vanilla.
* Facile manutenzione poiché gli aggiornamenti al pacchetto Selettore risorse vengono automaticamente distribuiti nel selettore risorse disponibile per l’applicazione. Non sono necessari aggiornamenti all’interno dell’applicazione per caricare le modifiche più recenti.
* Facilità di personalizzazione grazie alle proprietà disponibili che controllano la visualizzazione del Selettore risorse all’interno dell’applicazione.
* Filtri di ricerca full-text, predefiniti e personalizzati per passare rapidamente alle risorse da utilizzare nell’esperienza di authoring.
* Possibilità di cambiare archivi all’interno di un’organizzazione IMS per la selezione delle risorse.
* Possibilità di ordinare le risorse per nome, proporzioni e dimensioni e di visualizzarle nelle viste Elenco, Griglia, Galleria o Cascata.

<!--Perform the following tasks to integrate and use Asset Selector with your [!DNL Experience Manager Assets] repository:

1. [Install Asset Selector](#installation)
2. [Integrate Asset Selector using Vanilla JS](#integration-using-vanilla-js)
3. [Use Asset Selector](#using-asset-selector)
-->

<!--
## Setting up Asset Selector {#asset-selector-setup}

![Asset Selector set up](assets/asset-selector-prereqs.png)
-->

## Prerequisiti{#prereqs}

Devi accertarti di utilizzare i seguenti metodi di comunicazione:

* L&#39;applicazione è in esecuzione su HTTPS.
* L’URL dell’applicazione si trova nell’elenco Consentiti degli URL di reindirizzamento del client IMS.
* Il flusso di accesso IMS viene configurato e renderizzato utilizzando un pop-up sul browser web. Pertanto, i popup devono essere abilitati o consentiti nel browser di destinazione.

Se hai bisogno del flusso di lavoro di autenticazione IMS di Asset Selector, utilizza i prerequisiti precedenti. In alternativa, se sei già autenticato con il flusso di lavoro IMS, puoi aggiungere le informazioni IMS.

>[!IMPORTANT]
>
> Questo archivio funge da documentazione supplementare che descrive le API disponibili e alcuni esempi di utilizzo per l’integrazione di Asset Selector. Prima di installare o utilizzare il Selettore risorse, assicurati che all’organizzazione sia stato fornito l’accesso al Selettore risorse come parte del profilo Experience Manager Assets as a Cloud Service. Se non è stato eseguito il provisioning di, non è possibile integrare o utilizzare questi componenti. Per richiedere il provisioning, l’amministratore del programma deve generare un ticket di supporto contrassegnato come P2 da Admin Console e includere le seguenti informazioni:
>
>* Nomi di dominio in cui è ospitata l’applicazione che integra.
>* Dopo il provisioning, all’organizzazione verrà fornito `imsClientId`, `imsScope`, e un `redirectUrl` corrisponde agli ambienti richiesti che sono essenziali per la configurazione di Asset Selector. Senza tali proprietà valide, non è possibile eseguire i passaggi di installazione.

## Installazione {#installation}

Il selettore risorse è disponibile tramite CDN ESM (ad esempio, [esm.sh](https://esm.sh/)/[skypack](https://www.skypack.dev/)) e [UMD](https://github.com/umdjs/umd) versione.

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

## Integra il Selettore risorse utilizzando Vanilla JS {#integration-using-vanilla-js}

È possibile integrare qualsiasi [!DNL Adobe] o non Adobe con [!DNL Experience Manager Assets] e selezionare le risorse dall’interno dell’applicazione. Consulta [Integrazione di Asset Selector con varie applicazioni](#asset-selector-integration-with-apps).

L’integrazione viene eseguita importando il pacchetto Selettore risorse e connettendolo ad Assets as a Cloud Service tramite la libreria JavaScript Vanilla. Modifica un `index.html` o qualsiasi file appropriato all’interno dell’applicazione per:

* Definire i dettagli di autenticazione
* Accedere all’archivio Assets as a Cloud Service
* Configurare le proprietà di visualizzazione del Selettore risorse

Puoi eseguire l’autenticazione senza definire alcune delle proprietà IMS se:

* Stai integrando un’applicazione [!DNL Adobe] su [Unified Shell](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/aem-cloud-service-on-unified-shell.html?lang=it).
* Hai già generato un token IMS per l’autenticazione.

## Integrare Asset Selector con varie applicazioni {#asset-selector-integration-with-apps}

È possibile integrare Asset Selector (Selettore risorse) con diverse applicazioni, tra cui:

* [Integrare il selettore risorse con un [!DNL Adobe] applicazione](#adobe-app-integration-vanilla)
* [Integrare Asset Selector con un’applicazione non basata su Adobi](#adobe-non-app-integration)

>[!BEGINTABS]

<!--Integration with an Adobe application content starts here-->

>[!TAB Integrazione con un’applicazione di Adobe]

### Prerequisiti{#prereqs-adobe-app}

Se stai integrando Asset Selector con una risorsa, utilizza i seguenti prerequisiti [!DNL Adobe] applicazione:

* [Metodi di comunicazione](#prereqs)
* imsOrg
* imsToken
* apikey

### Integrare il selettore risorse con un [!DNL Adobe] applicazione {#adobe-app-integration-vanilla}

L’esempio seguente illustra l’utilizzo di Asset Selector durante l’esecuzione di un’ [!DNL Adobe] in Unified Shell o quando disponi già di `imsToken` generato per l’autenticazione.

Includi il pacchetto Asset Selector nel codice utilizzando `script` come mostrato nella _righe 6-15_ dell’esempio seguente. Una volta caricato lo script, la variabile globale `PureJSSelectors` è disponibile per l’uso. Definire il selettore risorse [proprietà](#asset-selector-properties) come mostrato nella _righe 16-23_. Il `imsOrg` e `imsToken` entrambe le proprietà sono necessarie per l&#39;autenticazione nell&#39;applicazione Adobe. La proprietà `handleSelection` è utilizzata per gestire le risorse selezionate. Per eseguire il rendering del Selettore risorse, chiama la funzione `renderAssetSelector` come indicato nella _riga 17_. Il Selettore risorse viene visualizzato nell’`<div>`elemento contenitore, come illustrato nelle _righe 21 e 22_.

Seguendo questi passaggi, puoi utilizzare Asset Selector con il tuo [!DNL Adobe] applicazione.

```html {line-numbers="true"}
<!DOCTYPE html>
<html>
<head>
    <title>Asset Selector</title>
    <script src="https://experience.adobe.com/solutions/CQ-assets-selectors/assets/resources/assets-selectors.js"></script>
    <script>
        // get the container element in which we want to render the AssetSelector component
        const container = document.getElementById('asset-selector-container');
        // imsOrg and imsToken are required for authentication in Adobe application
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

<!--For detailed example, visit [Asset Selector Code Example](https://github.com/adobe/aem-assets-selectors-mfe-examples).-->

+++**ImsAuthProps**
Il `ImsAuthProps` definiscono le informazioni di autenticazione e il flusso utilizzati da Asset Selector per ottenere un `imsToken`. Impostando queste proprietà è possibile controllare il comportamento del flusso di autenticazione e registrare i listener per vari eventi di autenticazione.

| Nome proprietà | Descrizione |
|---|---|
| `imsClientId` | Valore stringa che rappresenta l’ID client IMS utilizzato a scopo di autenticazione. Questo valore è fornito da Adobe ed è specifico per l’organizzazione AEM CS Adobe. |
| `imsScope` | Descrive gli ambiti utilizzati nell&#39;autenticazione. Gli ambiti determinano il livello di accesso dell&#39;applicazione alle risorse dell&#39;organizzazione. Più ambiti possono essere separati da virgole. |
| `redirectUrl` | Rappresenta l&#39;URL a cui l&#39;utente viene reindirizzato dopo l&#39;autenticazione. Questo valore viene in genere impostato sull’URL corrente dell’applicazione. Se un `redirectUrl` non viene fornito, `ImsAuthService` utilizza il redirectUrl utilizzato per registrare `imsClientId` |
| `modalMode` | Valore booleano che indica se il flusso di autenticazione deve essere visualizzato o meno in un modale (pop-up). Se impostato su `true`, il flusso di autenticazione viene visualizzato in un pop-up. Se impostato su `false`, il flusso di autenticazione viene visualizzato in un ricaricamento dell’intera pagina. _Nota:_ per una migliore interfaccia utente, è possibile controllare dinamicamente questo valore se il pop-up del browser è disabilitato. |
| `onImsServiceInitialized` | Funzione di callback chiamata quando viene inizializzato il servizio di autenticazione Adobe IMS. Questa funzione accetta un parametro, `service`, che è un oggetto che rappresenta il servizio Adobe IMS. Consulta [`ImsAuthService`](#imsauthservice-ims-auth-service) per ulteriori dettagli. |
| `onAccessTokenReceived` | Una funzione di callback chiamata quando un `imsToken` viene ricevuto dal servizio di autenticazione IMS di Adobe. Questa funzione accetta un parametro, `imsToken`, che è una stringa che rappresenta il token di accesso. |
| `onAccessTokenExpired` | Funzione di callback chiamata quando un token di accesso è scaduto. Questa funzione viene in genere utilizzata per attivare un nuovo flusso di autenticazione per ottenere un nuovo token di accesso. |
| `onErrorReceived` | Funzione di callback chiamata quando si verifica un errore durante l&#39;autenticazione. Questa funzione accetta due parametri: il tipo di errore e il messaggio di errore. Il tipo di errore è una stringa che rappresenta il tipo di errore e il messaggio di errore è una stringa che rappresenta il messaggio di errore. |

+++

+++**ImsAuthService**
`ImsAuthService` La classe gestisce il flusso di autenticazione per Asset Selector. È responsabile dell&#39;ottenimento di un `imsToken` dal servizio di autenticazione Adobe IMS. Il `imsToken` viene utilizzato per autenticare l’utente e autorizzare l’accesso al [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] Archivio risorse. ImsAuthService utilizza `ImsAuthProps` proprietà per controllare il flusso di autenticazione e registrare i listener per vari eventi di autenticazione. È possibile utilizzare il comodo [`registerAssetsSelectorsAuthService`](#purejsselectorsregisterassetsselectorsauthservice) funzione per registrare _ImsAuthService_ con Asset Selector. Le seguenti funzioni sono disponibili sul `ImsAuthService` classe. Tuttavia, se utilizzi il _registerAssetsSelectorsAuthService_ funzione, non è necessario chiamare queste funzioni direttamente.

| Nome funzione | Descrizione |
|---|---|
| `isSignedInUser` | Determina se l&#39;utente è attualmente connesso al servizio e restituisce di conseguenza un valore booleano. |
| `getImsToken` | Recupera l’autenticazione `imsToken` per l’utente attualmente connesso, che può essere utilizzato per autenticare le richieste ad altri servizi, ad esempio per generare la _rappresentazione delle risorse. |
| `signIn` | Avvia il processo di accesso per l&#39;utente. Questa funzione utilizza `ImsAuthProps` per visualizzare l&#39;autenticazione in una finestra a comparsa o in un ricaricamento dell&#39;intera pagina |
| `signOut` | Firma l’utente fuori dal servizio, invalidando il token di autenticazione e richiedendo di nuovo l’accesso per accedere alle risorse protette. Richiamando questa funzione verrà ricaricata la pagina corrente. |
| `refreshToken` | Aggiorna il token di autenticazione per l&#39;utente attualmente connesso, evitando la scadenza e garantendo l&#39;accesso ininterrotto alle risorse protette. Restituisce un nuovo token di autenticazione che può essere utilizzato per le richieste successive. |

+++

+++**Convalida con il token IMS fornito**

```
<script>
    const apiToken="<valid IMS token>";
    function handleSelection(selection) {
    console.log("Selected asset: ", selection);
    };
    function renderAssetSelectorInline() {
    console.log("initializing Asset Selector");
    const props = {
    "repositoryId": "delivery-p64502-e544757.adobeaemcloud.com",
    "apiKey": "ngdm_test_client",
    "imsOrg": "<IMS org>",
    "imsToken": apiToken,
    handleSelection,
    hideTreeNav: true
    }
    const container = document.getElementById('asset-selector-container');
    PureJSSelectors.renderAssetSelector(container, props);
    }
    $(document).ready(function() {
    renderAssetSelectorInline();
    });
</script>
```

+++

+++**Registrare i callback al servizio IMS**

```
// object `imsProps` to be defined as below 
let imsProps = {
    imsClientId: <IMS Client Id>,
        imsScope: "openid",
        redirectUrl: window.location.href,
        modalMode: true,
        adobeImsOptions: {
            modalSettings: {
            allowOrigin: window.location.origin,
},
        useLocalStorage: true,
},
onImsServiceInitialized: (service) => {
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
```

+++

<!--Integration with non-Adobe application content starts here-->

>[!TAB Integrazione con un’applicazione non Adobe]

<!--### Integrate Asset Selector with a [!DNL non-Adobe] application {#adobe-non-app-integration}-->

### Prerequisiti {#prereqs-non-adobe-app}

Se integri Asset Selector con un’applicazione non di Adobe, utilizza i seguenti prerequisiti:

* [Metodi di comunicazione](#prereqs)
* imsClientId
* imsScope
* redirectUrl
* imsOrg
* apikey

Il selettore risorse supporta l’autenticazione per [!DNL Experience Manager Assets] archivio che utilizza le proprietà di Identity Management System (IMS), come `imsScope` o `imsClientID` quando lo si integra con un’applicazione non Adobe.

+++**Configurare il selettore risorse per un’applicazione non di Adobe**
Per configurare Asset Selector per un’applicazione non di Adobe, devi innanzitutto registrare un ticket di supporto per il provisioning, seguito dai passaggi di integrazione.

**Registrazione di un ticket di supporto**
Passaggi per registrare un ticket di supporto tramite l’Admin Console:

1. Aggiungi **Selettore risorse con AEM Assets** nel titolo del biglietto.

1. Nella descrizione, includi i seguenti dettagli:

   * [!DNL Experience Manager Assets] as a [!DNL Cloud Service] URL (ID programma e ID ambiente).
   * Nomi di dominio in cui è ospitata l’applicazione web non Adobe.
+++

+++**Passaggi dell’integrazione**
Usa questo esempio `index.html` per l’autenticazione durante l’integrazione di Asset Selector con un’applicazione non Adobe.

Accedere al pacchetto Asset Selector utilizzando `Script` Tag, come mostrato nella *riga 9* a *riga 11* dell’esempio `index.html` file.

*Riga 14* a *riga 38* dell’esempio descrive le proprietà del flusso IMS, come `imsClientId`, `imsScope`, e `redirectURL`. La funzione richiede la definizione di almeno uno dei `imsClientId` e `imsScope` proprietà. Se non definisci un valore per `redirectURL`, viene utilizzato l’URL di reindirizzamento registrato per l’ID client.

Poiché non si dispone di un `imsToken` generate, utilizza `registerAssetsSelectorsAuthService` e `renderAssetSelectorWithAuthFlow` come mostrato nelle righe da 40 a 50 dell&#39;esempio `index.html` file. Utilizza il `registerAssetsSelectorsAuthService` funzione prima di `renderAssetSelectorWithAuthFlow` per registrare `imsToken` con il Selettore risorse. [!DNL Adobe] consiglia di chiamare `registerAssetsSelectorsAuthService` quando crei un’istanza del componente.

Definisci l’autenticazione e altre proprietà as a Cloud Service di Assets relative all’accesso in `const props` come mostrato nella *riga 54* a *riga 60* dell’esempio `index.html` file.

Il `PureJSSelectors` variabile globale, menzionata in *riga 65*, viene utilizzato per eseguire il rendering del selettore risorse nel browser web.

Il rendering del selettore risorse viene eseguito sul `<div>` elemento contenitore, come indicato in *riga 74* a *riga 81*. Nell&#39;esempio viene utilizzata una finestra di dialogo per visualizzare il selettore risorse.

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

+++

+++**Impossibile accedere all’archivio di consegna**

>[!TIP]
>
>Se hai integrato il selettore delle risorse utilizzando il flusso di lavoro Registra, ma non riesci ancora ad accedere all’archivio di consegna, assicurati che i cookie del browser siano puliti. In caso contrario, si finisce per ottenere `invalid_credentials All session cookies are empty` nella console.

>[!ENDTABS]

## Proprietà selettore risorse {#asset-selector-properties}

Puoi utilizzare le proprietà del Selettore risorse per personalizzarne il rendering. Nella tabella seguente sono elencate le proprietà che è possibile utilizzare per personalizzare e utilizzare il Selettore risorse.

| Proprietà | Tipo | Obbligatorio | Predefiniti | Descrizione |
|---|---|---|---|---|
| *barra* | booleano | No | false | Se contrassegnato `true`, il rendering del selettore risorse viene eseguito nella barra a sinistra. Se è contrassegnato `false`, il selettore delle risorse viene renderizzato nella vista modale. |
| *imsOrg* | stringa | Sì | | L’ID di Adobe Identity Management System (IMS) assegnato durante il provisioning di [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] per l’organizzazione. Il `imsOrg` È necessario specificare la chiave per autenticare se l’organizzazione a cui stai accedendo è in Adobe IMS o meno. |
| *imsToken* | stringa | No | | Token di connessione IMS utilizzato per l’autenticazione. `imsToken` è richiesto se si utilizza un [!DNL Adobe] per l&#39;integrazione. |
| *apiKey* | stringa | No | | Chiave API utilizzata per accedere al servizio di individuazione AEM. `apiKey` è richiesto se si utilizza un [!DNL Adobe] integrazione delle applicazioni. |
| *rootPath* | stringa | No | /content/dam/ | Percorso della cartella da cui il selettore risorse visualizza le risorse. `rootPath` può essere utilizzato anche sotto forma di incapsulamento. Ad esempio, dato il seguente percorso: `/content/dam/marketing/subfolder/`, il selettore risorse non consente di spostarsi all’interno di alcuna cartella principale, ma visualizza solo le cartelle secondarie. |
| *percorso* | stringa | No | | Percorso utilizzato per passare a una directory specifica di risorse durante il rendering del Selettore risorse. |
| *filterSchema* | array | No | | Modello utilizzato per configurare le proprietà del filtro. Questa funzione è utile quando desideri limitare determinate opzioni di filtro nel Selettore risorse. |
| *filterFormProps* | Oggetto | No | | Specifica le proprietà del filtro da utilizzare per perfezionare la ricerca. Ad esempio, tipo MIME JPG, PNG, GIF. |
| *selectedAssets* | Array `<Object>` | No |                 | Specifica le risorse selezionate quando viene eseguito il rendering del Selettore risorse. È necessario un array di oggetti che contenga una proprietà ID delle risorse. Ad esempio, `[{id: 'urn:234}, {id: 'urn:555'}]` Deve essere disponibile una risorsa nella directory corrente. Se devi utilizzare una directory diversa, specifica anche un valore per la proprietà `path`. |
| *acvConfig* | Oggetto | No | | Proprietà Visualizzazione raccolta risorse che contiene un oggetto contenente una configurazione personalizzata per ignorare le impostazioni predefinite. Inoltre, questa proprietà viene utilizzata con `rail` per abilitare la visualizzazione della barra del visualizzatore risorse. |
| *i18nSymbols* | `Object<{ id?: string, defaultMessage?: string, description?: string}>` | No |                 | Se le traduzioni OOTB non sono sufficienti per le esigenze dell’applicazione, puoi esporre un’interfaccia tramite la quale puoi trasmettere valori localizzati personalizzati tramite `i18nSymbols` prop Il passaggio di un valore tramite questa interfaccia sostituisce le traduzioni predefinite fornite e utilizza le tue. Per eseguire la sostituzione, è necessario passare un oggetto valido del [Descrittore del messaggio](https://formatjs.io/docs/react-intl/api/#message-descriptor) alla chiave di `i18nSymbols` che desideri sostituire. |
| *intl* | Oggetto | No | | Il selettore risorse fornisce le traduzioni OOTB predefinite. È possibile selezionare la lingua di traduzione fornendo una stringa di lingua valida attraverso la proprietà `intl.locale`. Ad esempio: `intl={{ locale: "es-es" }}` </br></br> Le stringhe di lingua supportate seguono i [Codici - ISO 639](https://www.iso.org/iso-639-language-codes.html) per la rappresentazione di nomi di lingue standard. </br></br> Elenco delle lingue supportate: Inglese - ‘en-us’ (impostazione predefinita) Spagnolo - ‘es-es’ Tedesco - ‘de-de’ Francese - ‘fr-fr’ Italiano - ‘it-it’ Giapponese - ‘ja-jp’ Coreano - ‘ko-kr’ Portoghese - ‘pt-br’ cinese (tradizionale) - ‘zh-cn’ Cinese (Taiwan) - ‘zh-tw’ |
| *repositoryId* | stringa | No | &#39;&#39; | Archivio da cui il Selettore risorse carica il contenuto. |
| *additionalAemSolutions* | `Array<string>` | No | [ ] | Ti consente di aggiungere un elenco di archivi AEM aggiuntivi. Se non vengono fornite informazioni in questa proprietà, vengono considerati solo la libreria di file multimediali o gli archivi di AEM Assets. |
| *hideTreeNav* | booleano | No |  | Specifica se mostrare o nascondere la barra laterale di navigazione della struttura delle risorse. Viene utilizzata solo nella vista modale e quindi questa proprietà non influisce sulla visualizzazione della barra. |
| *onDrop* | Funzione | No | | La proprietà consente la funzionalità di rilascio di una risorsa. |
| *dropOptions* | `{allowList?: Object}` | No | | Configura le opzioni di rilascio utilizzando un “elenco consentiti”. |
| *colorScheme* | stringa | No | | Configura il tema (`light` o `dark`) per il Selettore risorse. |
| *handleSelection* | Funzione | No | | Richiamata con un array di elementi di risorse quando queste sono selezionate e si fa clic sul pulsante `Select` nel modale. Questa funzione viene richiamata solo nella vista modale. Per la visualizzazione della barra, utilizza le funzioni `handleAssetSelection` o `onDrop`. Esempio: <pre>handleSelection=(risorse: risorsa[])=> {...}</pre> Per maggiori dettagli, consulta [Tipo di risorsa selezionato](#selected-asset-type). |
| *handleAssetSelection* | Funzione | No | | Richiamata con un array di elementi durante la selezione o la deselezione delle risorse. Questa funzione è utile quando si desidera ascoltare le risorse selezionate dall’utente. Esempio: <pre>handleSelection=(risorse: risorsa[])=> {...}</pre> Per maggiori dettagli, consulta [Tipo di risorsa selezionato](#selected-asset-type). |
| *onClose* | Funzione | No | | Richiamata quando viene premuto il pulsante `Close` nella vista modale. Questa è chiamata solo nella vista `modal` e ignorata nella vista `rail`. |
| *onFilterSubmit* | Funzione | No | | Richiamata con gli elementi filtro poiché l’utente modifica criteri di filtro diversi. |
| *selectionType* | stringa | No | singolo | Configurazione per la selezione `single` o `multiple` di risorse alla volta. |
| *trascinamentoOpzioni.inserisce nell&#39;elenco Consentiti* | booleano | No | | La proprietà viene utilizzata per consentire o negare il trascinamento di risorse non selezionabili. |
| *aemTierType* | stringa | No | | Consente di scegliere se visualizzare le risorse dal livello di consegna, dal livello di authoring o da entrambi. <br><br> Sintassi: `aemTierType:[0: "author" 1: "delivery"` <br><br> Ad esempio, se entrambi `["author","delivery"]` , il selettore dell’archivio visualizza le opzioni sia per l’authoring che per la consegna. |
| *handleNavigateToAsset* | Funzione | No | | È una funzione di callback per gestire la selezione di una risorsa. |
| *noWrap* | booleano | No | | Il *noWrap* consente di eseguire il rendering del selettore risorse nel pannello della barra laterale. Se questa proprietà non è menzionata, viene eseguito il rendering del *Vista finestra di dialogo* per impostazione predefinita. |
| *dialogSize* | acquisizione di piccole, medie, grandi, a schermo intero o intero | Stringa | Facoltativo | È possibile controllare il layout specificandone le dimensioni utilizzando le opzioni specificate. |
| *colorScheme* | chiaro o scuro | No | | Questa proprietà viene utilizzata per impostare il tema di un&#39;applicazione Asset Selector. Puoi scegliere tra tema chiaro o scuro. |
| *filterRepoList* | Funzione | No |  | È possibile utilizzare `filterRepoList` funzione di callback che chiama l’archivio Experience Manager e restituisce un elenco filtrato di archivi. |

## Esempi per utilizzare le proprietà del Selettore risorse {#usage-examples}

Puoi definire le [proprietà](#asset-selector-properties) del Selettore risorse nel file `index.html` per personalizzare la visualizzazione del Selettore risorse all’interno dell’applicazione.

### Esempio 1: Selettore risorse nella visualizzazione della barra

![rail-view-example](assets/rail-view-example-vanilla.png)

Se il valore di AssetSelector `rail` è impostato su `false` oppure non è menzionato nelle proprietà; per impostazione predefinita, Asset Selector (Selettore risorsa) viene visualizzato nella vista modale. Il `acvConfig` consente alcune configurazioni approfondite, come il trascinamento della selezione. Visita [abilitare o disabilitare il trascinamento della selezione](#enable-disable-drag-and-drop) per comprendere l’utilizzo di `acvConfig` proprietà.

<!--
### Example 2: Use selectedAssets property in addition to the path property

Use the `path` property to define the folder name that displays automatically when the Asset Selector is rendered. In addition, use the `selectedAssets` property to define the IDs for the assets that you need to select within the folder. Moreover, when you want to display assets that are pre-defined within the folder, you can use selectedAssets property.

   ![selected-assets-example](assets/selected-assets-example-vanilla.png)
-->

### Esempio 2: finestra popover dei metadati

Utilizza varie proprietà per definire i metadati di una risorsa da visualizzare mediante un’icona Info. La finestra popover Iinfo fornisce un insieme di informazioni sulla risorsa o sulla cartella, tra cui titolo, dimensioni, data di modifica, posizione e descrizione di una risorsa. Nell’esempio seguente, per visualizzare i metadati di una risorsa vengono utilizzate diverse proprietà, ad esempio: proprietà `repo:path` che specifica la posizione di una risorsa. <!--`repo` represents the repository from where the asset is showing, whereas, `path` represents the route from where the asset or folder is rendered.-->

![metadata-popover-example](assets/metadata-popover.png)

### Esempio 3: proprietà filtro personalizzata nella visualizzazione della barra

Oltre alla ricerca sfaccettata, il Selettore risorse consente di personalizzare vari attributi per perfezionare la ricerca da [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] applicazione. Aggiungi il seguente codice per aggiungere filtri di ricerca personalizzati nell’applicazione. Nell’esempio seguente, la ricerca `Type Filter` che identifica il tipo di risorsa tra Immagini, Documenti o Video o il tipo di filtro aggiunto per la ricerca.

![custom-filter-example-vanilla](assets/custom-filter-example-vanilla.png)

<!--

## Customization after integrating Asset Selector 

### Custom metadata

Assets display panel shows the out of the box metadata that can be displayed in the info of the asset. In addition to this, [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] application allows configuration of the asset selector by adding custom metadata that is shown in info panel of the asset.
-->

## Snippet di codice di configurazione funzionale{#code-snippets}

Definire i prerequisiti in `index.html` o un file simile nell’implementazione dell’applicazione per definire i dettagli di autenticazione per accedere al [!DNL Experience Manager Assets] archivio. Al termine, puoi aggiungere snippet di codice in base alle tue esigenze.

### Personalizzare il pannello dei filtri {#customize-filter-panel}

Puoi aggiungere il seguente frammento di codice in `assetSelectorProps` oggetto per personalizzare il pannello dei filtri:

```
filterSchema: [
    {
    header: 'File Type',
    groupKey: 'TopGroup',
    fields: [
    {
    element: 'checkbox',
    name: 'type',
    options: [
    {
    label: 'Images',
    value: '<comma separated mimetypes, without space, that denote all images, for e.g., image/>',
    },
    {
    label: 'Videos',
    value: '<comma separated mimetypes, without space, that denote all videos for e.g., video/,model/vnd.mts,application/mxf>'
    }
    ]
    }
    ]
    },
    {
    fields: [
    {
    element: 'checkbox',
    name: 'type',
    options: [
    { label: 'JPG', value: 'image/jpeg' },
    { label: 'PNG', value: 'image/png' },
    { label: 'TIFF', value: 'image/tiff' },
    { label: 'GIF', value: 'image/gif' },
    { label: 'MP4', value: 'video/mp4' }
    ],
    columns: 3,
    },
    ],
    header: 'Mime Types',
    groupKey: 'MimeTypeGroup',
    }},
    {
    fields: [
    {
    element: 'checkbox',
    name: 'property=metadata.application.xcm:keywords.value',
    options: [
    { label: 'Fruits', value: 'fruits' },
    { label: 'Vegetables', value: 'vegetables'}
    ],
    columns: 3,
    },
    ],
    header: 'Food Category',
    groupKey: 'FoodCategoryGroup',
    }
],
```

### Personalizzare le informazioni nella vista modale {#customize-info-in-modal-view}

Puoi personalizzare la visualizzazione dei dettagli di una risorsa facendo clic sul pulsante ![icona info](assets/info-icon.svg) icona. Esegui il codice seguente:

```
// Create an object infoPopoverMap and set the property `infoPopoverMap` with it in assetSelectorProps
const infoPopoverMap = (map) => {
// for example, to skip `path` from the info popover view
let defaultPopoverData = PureJSSelectors.getDefaultInfoPopoverData(map);
return defaultPopoverData.filter((i) => i.label !== 'Path'
};
assetSelectorProps.infoPopoverMap = infoPopoverMap;
```

### Attiva o disattiva la modalità di trascinamento della selezione {#enable-disable-drag-and-drop}

Aggiungi le seguenti proprietà a `assetSelectorProp` per attivare la modalità di trascinamento. Per disattivare il trascinamento della selezione, sostituisci `true` parametro con `false`.

```
rail: true,
acvConfig: {
dragOptions: {
allowList: {
'*': true,
},
},
selectionType: 'multiple'
}

// the drop handler to be implemented
function drop(e) {
e.preventDefault();
// following helps you get the selected assets – an array of objects.
const data = JSON.parse(e.dataTransfer.getData('collectionviewdata'));
}
```

### Selezione delle risorse {#selection-of-assets}

Il tipo di risorsa selezionato è un array di oggetti che contiene le informazioni della risorsa quando si utilizzano le funzioni `handleSelection`, `handleAssetSelection`, e `onDrop`.

Per configurare la selezione di una o più risorse, effettua le seguenti operazioni:

```
acvConfig: {
selectionType: 'multiple' // 'single' for single selection
}
// the `handleSelection` callback, always gets you the array of selected assets
```

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

Nella tabella seguente vengono descritte alcune delle proprietà importanti dell’oggetto Risorsa selezionata.

| Proprietà | Tipo | Descrizione |
|---|---|---|
| *repo:repositoryId* | stringa | Identificatore univoco dell’archivio in cui è memorizzata la risorsa. |
| *repo:id* | stringa | Identificatore univoco della risorsa. |
| *repo:assetClass* | stringa | La classificazione della risorsa (ad esempio immagine o video, documento). |
| *repo:name* | stringa | Nome della risorsa, inclusa l’estensione del file. |
| *repo:size* | numero | Dimensione della risorsa in byte. |
| *repo:path* | stringa | Posizione della risorsa all’interno dell’archivio. |
| *repo:ancestors* | `Array<string>` | Array di elementi predecessori per la risorsa nell’archivio. |
| *repo:state* | stringa | Stato corrente della risorsa nell’archivio (ad esempio attiva, eliminata e così via). |
| *repo:createdBy* | stringa | Utente o sistema che ha creato la risorsa. |
| *repo:createDate* | stringa | La data e l’ora in cui è stata creata la risorsa. |
| *repo:modifiedBy* | stringa | Utente o sistema che ha modificato per ultimo la risorsa. |
| *repo:modifyDate* | stringa | La data e l’ora dell’ultima modifica apportata alla risorsa. |
| *dc:format* | stringa | Il formato della risorsa, ad esempio il tipo di file (ad esempio, JPEG, PNG e così via). |
| *tiff:imageWidth* | numero | Larghezza di una risorsa. |
| *tiff:imageLength* | numero | Altezza di una risorsa. |
| *computedMetadata* | `Record<string, any>` | Oggetto che rappresenta un bucket per tutti i metadati di tutti i tipi di risorsa (archivio, applicazione o metadati incorporati). |
| *_collegamenti* | `Record<string, any>` | Collegamenti ipermediali della risorsa associata. Include collegamenti a risorse quali metadati e rappresentazioni. |
| *_collegamenti.<http://ns.adobe.com/adobecloud/rel/rendition>* | `Array<Object>` | Array di oggetti contenenti informazioni sulle rappresentazioni della risorsa. |
| *_collegamenti.<http://ns.adobe.com/adobecloud/rel/rendition[].href>* | stringa | URI della rappresentazione. |
| *_collegamenti.<http://ns.adobe.com/adobecloud/rel/rendition[].type>* | stringa | Tipo MIME della rappresentazione. |
| *_collegamenti.<http://ns.adobe.com/adobecloud/rel/rendition[].'repo:size>&#39;* | numero | Dimensione della rappresentazione in byte. |
| *_collegamenti.<http://ns.adobe.com/adobecloud/rel/rendition[].width>* | numero | Larghezza della rappresentazione. |
| *_collegamenti.<http://ns.adobe.com/adobecloud/rel/rendition[].height>* | numero | Altezza della rappresentazione. |

Per un elenco completo delle proprietà e un esempio dettagliato, consulta [Esempio di codice del Selettore risorse](https://github.com/adobe/aem-assets-selectors-mfe-examples).

## Gestione della selezione di risorse tramite lo schema a oggetti {#handling-selection}

La proprietà `handleSelection` viene utilizzata per gestire selezioni singole o multiple di risorse nel Selettore risorse. L’esempio seguente indica la sintassi di utilizzo di `handleSelection`.

![handle-selection](assets/handling-selection.png)

## Disabilitazione della selezione delle risorse {#disable-selection}

La funzione Disattiva selezione viene utilizzata per nascondere o disabilitare la selezione delle risorse o cartelle. La casella di controllo di selezione viene nascosta dalla scheda o dalla risorsa, che ne impedisce la selezione. Per utilizzare questa funzione, puoi dichiarare la posizione di una risorsa o cartella che desideri disabilitare in un array. Ad esempio, se vuoi disattivare la visualizzazione di una cartella in prima posizione, puoi aggiungere il seguente codice:
`disableSelection: [0]:folder`

Puoi fornire all’array un elenco di tipi mime (ad esempio immagine, cartella, file o altri tipi mime come immagine/jpeg) che desideri disabilitare. I tipi MIME dichiarati sono mappati in `data-card-type` e `data-card-mimetype` attributi di una risorsa.

Inoltre, le risorse con selezione disabilitata possono essere trascinate. Per disattivare il trascinamento di un particolare tipo di risorsa, puoi utilizzare `dragOptions.allowList` proprietà.

La sintassi per disabilitare la selezione è la seguente:

```
(args)=> {
    return(
        <ASDialogWrapper
            {...args}
            disableSelection={args.disableSelection}
            handleAssetSelection={action('handleAssetSelection')}
            handleSelection={action('handleSelection')}
            selectionType={args.selectionType}
        />
    );
}
```

>[!NOTE]
>
> Nel caso di una risorsa, la casella di controllo di selezione è nascosta, mentre nel caso di una cartella, la cartella non è selezionabile ma viene ancora visualizzata la navigazione della cartella indicata.

## Utilizzo del Selettore risorse {#using-asset-selector}

Dopo aver configurato il Selettore risorse ed aver effettuato l’autenticazione per utilizzarlo con l’applicazione [!DNL Adobe Experience Manager] as a [!DNL Cloud Service], puoi selezionare le risorse o eseguire varie altre operazioni per cercare le risorse all’interno dell’archivio.

![using-asset-selector](assets/using-asset-selector.png)

* **A**: [Nascondi/Mostra pannello](#hide-show-panel)
* **B**: [Selettore archivio](#repository-switcher)
* **C**: [Risorse](#repository)
* **D**: [Filtri](#filters)
* **E**: [Barra di ricerca](#search-bar)
* **F**: [Ordinamento](#sorting)
* **G**: [Ordinamento crescente o decrescente](#sorting)
* **H**: [Visualizzazione](#types-of-view)

### Nascondi/Mostra pannello {#hide-show-panel}

Per nascondere le cartelle nel menu di navigazione a sinistra, fai clic sull’icona **[!UICONTROL Nascondi cartelle]**. Per annullare le modifiche, fai di nuovo clic sull’icona **[!UICONTROL Nascondi cartelle]**.

### Selettore archivio {#repository-switcher}

Asset Selector consente inoltre di cambiare archivi per la selezione delle risorse. Puoi selezionare l’archivio desiderato dal menu a discesa disponibile nel pannello a sinistra. Le opzioni dell’archivio disponibili nell’elenco a discesa si basano sulla proprietà `repositoryId` definita nel file `index.html`. Si basa sull’ambiente dell’organizzazione IMS selezionata a cui accede l’utente connesso. I consumatori possono trasmettere un `repositoryID` preferito e, in tal caso, il Selettore risorse interrompe il rendering del selettore archivio ed esegue il rendering solo delle risorse dall’archivio specificato.
<!--
It is based on the `imsOrg` that is provided in the application. If you want to see the list of repositories, then `repositoryId` is required to view those specific repositories in your application.
-->

### Archivio risorse

Si tratta di una raccolta di cartelle di risorse che puoi utilizzare per eseguire le operazioni.

### Filtri predefiniti {#filters}

Il Selettore risorse fornisce anche opzioni di filtro predefinite per perfezionare i risultati della ricerca. Sono disponibili i seguenti filtri:

* `File type`: include cartelle, file, immagini, documenti o video
* `MIME type`: include JPG, GIF, PPTX, PNG, MP4, DOCX, TIFF, PDF, XLSX
* `Image Size`: include larghezza minima/massima, altezza minima/massima dell’immagine

  ![rail-view-example](assets/filters-asset-selector.png)

### Ricerca personalizzata

Oltre alla ricerca full-text, Asset Selector consente di cercare le risorse all’interno dei file utilizzando la ricerca personalizzata. Puoi utilizzare filtri di ricerca personalizzati sia nella vista modale che nella vista della barra.

![custom-search](assets/custom-search1.png)

Puoi anche creare un filtro di ricerca predefinito per salvare i campi che cerchi frequentemente e utilizzarli in un secondo momento. Per creare una ricerca personalizzata delle risorse, puoi utilizzare la proprietà `filterSchema`.

### Barra di ricerca {#search-bar}

Il selettore risorse consente di eseguire una ricerca full-text delle risorse all’interno dell’archivio selezionato. Ad esempio, se digiti la parola chiave `wave` nella barra di ricerca, vengono mostrate tutte le risorse con la parola chiave `wave` menzionata in una qualsiasi delle proprietà dei metadati.

### Ordinamento {#sorting}

Puoi ordinare le risorse all’interno selettore risorse per nome, dimensione o dimensione di una risorsa. Puoi anche ordinare le risorse in ordine crescente o decrescente.

### Tipi di visualizzazione {#types-of-view}

Il selettore risorse consente di visualizzare la risorsa in quattro diverse visualizzazioni:

* **![Vista a elenco](assets/do-not-localize/list-view.png) [!UICONTROL Vista a elenco]**: la vista a elenco mostra i file e le cartelle in modo scorrevole in una singola colonna.
* **![vista griglia](assets/do-not-localize/grid-view.png) [!UICONTROL Vista griglia]**: la vista griglia mostra i file e le cartelle in modo scorrevole in una griglia di righe e colonne.
* **![vista galleria](assets/do-not-localize/gallery-view.png) [!UICONTROL Vista galleria]**: la vista galleria mostra i file o le cartelle in un elenco orizzontale bloccato al centro.
* **![vista a cascata](assets/do-not-localize/waterfall-view.png) [!UICONTROL Vista a cascata]**: la vista a cascata mostra file o cartelle sotto forma di un Bridge.

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
*   **Configure** You can configure the files/folders that you want to show at the upfront. The assets that are chosen to view can be of any supported formats, for example, JPEG. It lets you control the display of various text or symbols as per your choice.
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
*   **Open in media library** Lets you open the asset in media library.
*   **Upload** Lets you upload an asset directly.
*   **Download** Downloads the asset in [!DNL Adobe Experience Manager] as a [!DNL Cloud Service].
-->
<!--

### Status of an asset

Asset Selector lets you know the status of your uploaded assets. The status can be `Approved`, `Rejected`, or `Expired` of the asset. 
-->
<!--

### Localization

The integration of Asset Selector with [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] allows localized content appear in your application.
-->



<!--Best Practice-->
<!--
+++**Control default selection of the filter**
You can make the selection of filter default by implementing the following code snippet:

```
"defaultValue": [
    "image/*",
    "application/*"
],

{
    "label": "Documents",
    "value": "application/*"
}
```

+++
-->
