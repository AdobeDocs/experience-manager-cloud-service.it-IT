---
title: Integrare il selettore dei frammenti di contenuto con un’applicazione Adobe
description: Integra il selettore Frammento di contenuto con varie applicazioni Adobe.
role: Admin, User, Developer
source-git-commit: a16d9e9fa6483a89283c595372abcc437d1d962e
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 1%

---

# Integrare il selettore dei frammenti di contenuto con l’applicazione Adobe {#integrate-content-fragment-selector-with-adobe-application}

Il Selettore dei frammenti di contenuto consente di integrarsi con varie applicazioni Adobe per consentire loro di lavorare insieme senza problemi.

## Prerequisiti {#prerequisites}

Se stai integrando il Selettore frammento di contenuto con un’applicazione Adobe, utilizza i seguenti prerequisiti:

* [Prerequisiti](/help/headless/content-fragment-selector/overview.md#prerequisites)
* imsOrg
* imsToken
* apikey

## Integrare il selettore dei frammenti di contenuto con un’applicazione Adobe {#integrate-content-fragment-selector-with-an-adobe-application}

Nell&#39;esempio seguente viene illustrato l&#39;utilizzo del selettore di frammenti di contenuto durante l&#39;esecuzione di un&#39;applicazione Adobe in Unified Shell o quando è già stato generato un `imsToken` per l&#39;autenticazione.

Includi il pacchetto del selettore frammento di contenuto nel codice utilizzando il tag `script`, come illustrato nell&#39;esempio seguente.

* Una volta caricato lo script, la variabile globale `PureJSContentFragmentSelectors` è disponibile per l&#39;utilizzo.
* Definisci il selettore frammento di contenuto [proprietà](/help/headless/content-fragment-selector/properties.md):

   * le proprietà `imsOrg` e `imsToken` sono entrambe necessarie per l&#39;autenticazione nell&#39;applicazione Adobe
   * la proprietà `handleSelection` viene utilizzata per gestire i frammenti selezionati.

* Per eseguire il rendering del selettore frammento di contenuto, chiamare la funzione `renderFragmentSelector`.
* Il selettore dei frammenti di contenuto viene visualizzato nell&#39;elemento contenitore `<div>`.

Seguendo questi passaggi, puoi utilizzare il selettore dei frammenti di contenuto con la tua applicazione Adobe.

```html {line-numbers="true"}
<!DOCTYPE html>
<html>
<head>
    <title>Fragment Selector</title>
    <script src="https://experience.adobe.com/solutions/CQ-fragmentss-selectors/static-fragments/resources/fragments-selectors.js"></script>
    <script>
        // get the container element in which we want to render the FragmentSelector component
        const container = document.getElementById('fragment-selector-container');
        // imsOrg and imsToken are required for authentication in Adobe application
        const fragmentSelectorProps = {
            imsOrg: 'example-ims@AdobeOrg',
            imsToken: "example-imsToken",
            apiKey: "example-apiKey-associated-with-imsOrg",
            handleSelection: (fragmentss: SelectedFragmentType[]) => {},
        };
        // Call the `renderFragmentSelector` available in PureJSContentFragmentSelectors globals to render FragmenttSelector
        PureJSContentFragmentSelectors.renderFragmentSelector(container, fragmentSelectorProps);
    </script>
</head>

<body>
    <div id="fragment-selector-container" style="height: calc(100vh - 80px); width: calc(100vw - 60px); margin: -20px;">
    </div>
</body>

</html>
```

### ImsAuthProps {#imsauthprops}

Le proprietà `ImsAuthProps` definiscono le informazioni di autenticazione e il flusso utilizzati dal selettore frammento di contenuto per ottenere un `imsToken`. Impostando queste proprietà è possibile controllare il comportamento del flusso di autenticazione e registrare i listener per vari eventi di autenticazione.

Per informazioni dettagliate sulle proprietà, vedere [Proprietà ImsAuthProps](/help/headless/content-fragment-selector/properties.md#imsauthprops-properties)

### ImsAuthService {#imsauthservice}

La classe `ImsAuthService` gestisce il flusso di autenticazione per il selettore di frammenti. È responsabile dell&#39;ottenimento di un `imsToken` dal servizio di autenticazione Adobe IMS. `imsToken` viene utilizzato per autenticare l&#39;utente e autorizzare l&#39;accesso all&#39;archivio AEM as a Cloud Service. `ImsAuthService` utilizza le proprietà `ImsAuthProps` per controllare il flusso di autenticazione e registrare i listener per vari eventi di autenticazione. È possibile utilizzare la funzione `registerFragmentsSelectorsAuthService` per registrare l&#39;istanza `ImsAuthService` con il selettore frammenti. Le seguenti funzioni sono disponibili nella classe `ImsAuthService`. Tuttavia, se si utilizza la funzione `registerFragmentsSelectorsAuthService`, non è necessario chiamare queste funzioni direttamente.

Per informazioni dettagliate sulle proprietà, vedere [Proprietà ImsAuthService](/help/headless/content-fragment-selector/properties.md#imsauthservice-properties)

### Convalida con il token IMS fornito {#validation-with-provided-ims-token}

```javascript
<script>
    const apiToken="<valid IMS token>";
    function handleSelection(selection) {
    console.log("Selected fragment: ", selection);
    };
    function renderFragmentSelectorInline() {
    console.log("initializing Fragment Selector");
    const props = {
    "repositoryId": "delivery-p64502-e544757.adobeaemcloud.com",
    "apiKey": "ngdm_test_client",
    "imsOrg": "<IMS org>",
    "imsToken": apiToken,
    handleSelection,
    hideTreeNav: true
    }
    const container = document.getElementById('fragment-selector-container');
    PureJSContentFragmentSelectors.renderFragmentSelector(container, props);
    }
    $(document).ready(function() {
    renderFragmentSelectorInline();
    });
</script>
```

### Registrare i callback al servizio IMS {#register-callbacks-to-ims-service}

```java
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
