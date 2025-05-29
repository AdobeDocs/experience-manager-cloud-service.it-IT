---
title: Integrare Asset Selector con  [!DNL Adobe]  applicazione
description: Integra il selettore delle risorse con varie applicazioni Adobe, non Adobe e di terze parti.
role: Admin, User
exl-id: a0c030e2-2213-406b-ad92-4761f1e2ee9f
source-git-commit: 08fc43bc8edeea91bfeb01f053d435e136658e7f
workflow-type: tm+mt
source-wordcount: '813'
ht-degree: 15%

---

# Integrare Asset Selector con l’applicazione Adobe {#integrate-asset-selector-with-adobe-app}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Novità</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime e Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Novità</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Novità</i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>Integrazione di AEM Assets con Edge Delivery Services</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Novità</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>Estensibilità dell’interfaccia utente</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Novità</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>Abilitare Dynamic Media Prime e Ultimate</b></a>
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

Asset Selector (Selettore risorse) consente di integrare utilizzando diverse applicazioni Adobe per consentire loro di lavorare insieme senza problemi.

## Prerequisiti{#prereqs-adobe-app}

Utilizzare i seguenti prerequisiti se si integra Asset Selector con un&#39;applicazione [!DNL Adobe]:

* [Metodi di comunicazione](/help/assets/overview-asset-selector.md#prereqs)
* imsOrg
* imsToken
* apikey

## Integrare Asset Selector con un&#39;applicazione [!DNL Adobe] {#adobe-app-integration-vanilla}

Nell&#39;esempio seguente viene illustrato l&#39;utilizzo di Asset Selector durante l&#39;esecuzione di un&#39;applicazione [!DNL Adobe] in Unified Shell o quando è già stato generato `imsToken` per l&#39;autenticazione.

Includi il pacchetto Asset Selector nel codice utilizzando il tag `script`, come mostrato nelle _righe 6-15_ dell&#39;esempio seguente. Una volta caricato lo script, la variabile globale `PureJSSelectors` è disponibile per l’uso. Definisci il selettore risorse [proprietà](/help/assets/asset-selector-properties.md) come mostrato nelle _righe 16-23_. Le proprietà `imsOrg` e `imsToken` sono entrambe necessarie per l&#39;autenticazione nell&#39;applicazione Adobe. La proprietà `handleSelection` è utilizzata per gestire le risorse selezionate. Per eseguire il rendering del Selettore risorse, chiama la funzione `renderAssetSelector` come indicato nella _riga 17_. Il Selettore risorse viene visualizzato nell’`<div>`elemento contenitore, come illustrato nelle _righe 21 e 22_.

Seguendo questi passaggi è possibile utilizzare Asset Selector con l&#39;applicazione [!DNL Adobe].

```html {line-numbers="true"}
<!DOCTYPE html>
<html>
<head>
    <title>Asset Selector</title>
    <script src="https://experience.adobe.com/solutions/CQ-assets-selectors/static-assets/resources/assets-selectors.js"></script>
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

### ImsAuthProps {#ims-auth-props}

Le proprietà `ImsAuthProps` definiscono le informazioni di autenticazione e il flusso utilizzati da Asset Selector per ottenere un `imsToken`. Impostando queste proprietà è possibile controllare il comportamento del flusso di autenticazione e registrare i listener per vari eventi di autenticazione.

| Nome proprietà | Descrizione |
|---|---|
| `imsClientId` | Valore stringa che rappresenta l’ID client IMS utilizzato a scopo di autenticazione. Questo valore è fornito da Adobe ed è specifico per la tua organizzazione Adobe AEM CS. |
| `imsScope` | Descrive gli ambiti utilizzati nell&#39;autenticazione. Gli ambiti determinano il livello di accesso dell&#39;applicazione alle risorse dell&#39;organizzazione. Più ambiti possono essere separati da virgole. |
| `redirectUrl` | Rappresenta l&#39;URL a cui l&#39;utente viene reindirizzato dopo l&#39;autenticazione. Questo valore viene in genere impostato sull’URL corrente dell’applicazione. Se non viene fornito `redirectUrl`, `ImsAuthService` utilizza il redirectUrl utilizzato per registrare `imsClientId` |
| `modalMode` | Valore booleano che indica se il flusso di autenticazione deve essere visualizzato o meno in un modale (pop-up). Se è impostato su `true`, il flusso di autenticazione viene visualizzato in un popup. Se è impostato su `false`, il flusso di autenticazione viene visualizzato in un ricaricamento dell&#39;intera pagina. _Nota:_ per una migliore interfaccia utente, è possibile controllare dinamicamente questo valore se la finestra popup del browser dell&#39;utente è disabilitata. |
| `onImsServiceInitialized` | Funzione di callback chiamata quando viene inizializzato il servizio di autenticazione Adobe IMS. Questa funzione accetta un parametro, `service`, che è un oggetto che rappresenta il servizio Adobe IMS. Per ulteriori dettagli, vedere [`ImsAuthService`](#imsauthservice-ims-auth-service). |
| `onAccessTokenReceived` | Funzione di callback chiamata quando viene ricevuto un `imsToken` dal servizio di autenticazione Adobe IMS. Questa funzione accetta un parametro, `imsToken`, che è una stringa che rappresenta il token di accesso. |
| `onAccessTokenExpired` | Funzione di callback chiamata quando un token di accesso è scaduto. Questa funzione viene in genere utilizzata per attivare un nuovo flusso di autenticazione per ottenere un nuovo token di accesso. |
| `onErrorReceived` | Funzione di callback chiamata quando si verifica un errore durante l&#39;autenticazione. Questa funzione accetta due parametri: il tipo di errore e il messaggio di errore. Il tipo di errore è una stringa che rappresenta il tipo di errore e il messaggio di errore è una stringa che rappresenta il messaggio di errore. |

### ImsAuthService {#ims-auth-service}

La classe `ImsAuthService` gestisce il flusso di autenticazione per Asset Selector. È responsabile dell&#39;ottenimento di un `imsToken` dal servizio di autenticazione Adobe IMS. `imsToken` viene utilizzato per autenticare l&#39;utente e autorizzare l&#39;accesso a [!DNL Adobe Experience Manager] come archivio Assets [!DNL Cloud Service]. ImsAuthService utilizza le proprietà `ImsAuthProps` per controllare il flusso di autenticazione e registrare i listener per vari eventi di autenticazione. È possibile utilizzare la comoda funzione [`registerAssetsSelectorsAuthService`](#purejsselectorsregisterassetsselectorsauthservice) per registrare l&#39;istanza _ImsAuthService_ con Asset Selector. Le seguenti funzioni sono disponibili nella classe `ImsAuthService`. Tuttavia, se si utilizza la funzione _registerAssetsSelectorsAuthService_, non è necessario chiamare queste funzioni direttamente.

| Nome funzione | Descrizione |
|---|---|
| `isSignedInUser` | Determina se l&#39;utente è attualmente connesso al servizio e restituisce di conseguenza un valore booleano. |
| `getImsToken` | Recupera l&#39;autenticazione `imsToken` per l&#39;utente attualmente connesso, che può essere utilizzata per autenticare le richieste ad altri servizi, ad esempio per generare la _rappresentazione della risorsa. |
| `signIn` | Avvia il processo di accesso per l&#39;utente. Questa funzione utilizza `ImsAuthProps` per mostrare l&#39;autenticazione in un popup o in un ricaricamento dell&#39;intera pagina |
| `signOut` | Firma l’utente fuori dal servizio, invalidando il token di autenticazione e richiedendo di nuovo l’accesso per accedere alle risorse protette. Richiamando questa funzione verrà ricaricata la pagina corrente. |
| `refreshToken` | Aggiorna il token di autenticazione per l&#39;utente attualmente connesso, evitando la scadenza e garantendo l&#39;accesso ininterrotto alle risorse protette. Restituisce un nuovo token di autenticazione che può essere utilizzato per le richieste successive. |

### Convalida con il token IMS fornito {#validation-ims-token}

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

### Registrare i callback al servizio IMS {#register-callback-ims-service}

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

>[!MORELIKETHIS]
>
>* [Integrare il Selettore risorse con varie applicazioni](/help/assets/integrate-asset-selector.md)
>* [Proprietà del Selettore risorse](/help/assets/asset-selector-properties.md)
>* [Integrare il Selettore risorse con Dynamic Media con funzionalità OpenAPI](/help/assets/integrate-asset-selector-dynamic-media-open-api.md)
>* [Personalizzazioni del Selettore risorse](/help/assets/asset-selector-customization.md)
