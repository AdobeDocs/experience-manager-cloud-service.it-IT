---
title: Integrare Asset Selector con applicazioni non Adobe o di terze parti
description: Integra il selettore delle risorse con varie applicazioni Adobe, non Adobe e di terze parti.
role: Admin, User
exl-id: 55848de0-aff2-42a0-b959-c771235d9425
source-git-commit: 39b6bbc10507f0391583d9cdc054a1611b64326a
workflow-type: tm+mt
source-wordcount: '428'
ht-degree: 9%

---

# Integrazione con un’applicazione non Adobe {#integrate-asset-selector-non-adobe-app}

Asset Selector consente di integrare utilizzando varie applicazioni non Adobe o di terze parti per consentire loro di lavorare insieme senza problemi.

## Prerequisiti {#prereqs-non-adobe-app}

Se integri Asset Selector con un’applicazione non Adobe, utilizza i seguenti prerequisiti:

* [Metodi di comunicazione](/help/assets/overview-asset-selector.md#prereqs)
* imsClientId
* imsScope
* redirectUrl
* imsOrg
* apikey

Asset Selector supporta l&#39;autenticazione nell&#39;archivio [!DNL Experience Manager Assets] tramite le proprietà di Identity Management System (IMS), ad esempio `imsScope` o `imsClientID`, durante l&#39;integrazione con un&#39;applicazione non Adobe.

## Configurare il selettore risorse per un’applicazione non Adobe {#configure-non-adobe-app}

Per configurare Asset Selector per un’applicazione non Adobe, devi innanzitutto registrare un ticket di supporto per il provisioning, seguito dai passaggi di integrazione.

### Registrazione di un ticket di supporto {#log-a-support-ticket}

Passaggi per registrare un ticket di assistenza tramite Admin Console:

1. Aggiungi **Selettore risorse con AEM Assets** nel titolo del ticket.

1. Nella descrizione, includi i seguenti dettagli:

   * [!DNL Experience Manager Assets] come URL [!DNL Cloud Service] (ID programma e ID ambiente).
   * Nomi di dominio in cui è ospitata l’applicazione web non Adobe.

## Passaggi dell’integrazione {#non-adobe-app-integration-steps}

Utilizza questo file di esempio `index.html` per l&#39;autenticazione durante l&#39;integrazione di Asset Selector con un&#39;applicazione non Adobe.

Accedere al pacchetto Asset Selector utilizzando il tag `Script`, come illustrato nella *riga 9* alla *riga 11* del file `index.html` di esempio.

*La riga da 14* a *la riga 38* dell&#39;esempio descrive le proprietà del flusso IMS, ad esempio `imsClientId`, `imsScope` e `redirectURL`. La funzione richiede di definire almeno una delle proprietà `imsClientId` e `imsScope`. Se non si definisce un valore per `redirectURL`, verrà utilizzato l&#39;URL di reindirizzamento registrato per l&#39;ID client.

Poiché non è stato generato alcun `imsToken`, utilizzare le funzioni `registerAssetsSelectorsAuthService` e `renderAssetSelectorWithAuthFlow`, come mostrato nella riga 40 alla riga 50 del file `index.html` di esempio. Utilizzare la funzione `registerAssetsSelectorsAuthService` prima di `renderAssetSelectorWithAuthFlow` per registrare `imsToken` con il selettore risorse. [!DNL Adobe] consiglia di chiamare `registerAssetsSelectorsAuthService` quando si crea un&#39;istanza del componente.

Definisci l&#39;autenticazione e altre proprietà relative all&#39;accesso ad Assets as a Cloud Service nella sezione `const props`, come mostrato nella *riga 54* alla *riga 60* del file di esempio `index.html`.

La variabile globale `PureJSSelectors`, menzionata nella *riga 65*, viene utilizzata per eseguire il rendering del selettore risorse nel browser Web.

Il rendering del selettore risorse viene eseguito sull&#39;elemento contenitore `<div>`, come indicato nella *riga 74* alla *riga 81*. Nell&#39;esempio viene utilizzata una finestra di dialogo per visualizzare il selettore risorse.

```html {line-numbers="true"}
<!DOCTYPE html>
<html>

<head>
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta charset="utf-8">
    <title>Asset Selectors</title>
    <link rel="stylesheet" href="index.css">
    <script id="asset-selector"
        src="https://experience.adobe.com/solutions/CQ-assets-selectors/static-assets/resources/assets-selectors.js"></script>
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
        function renderAssetSelectorWithAuthFlowFlow() {
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

## Impossibile accedere all’archivio di consegna {#unable-to-access-delivery-repository}

>[!TIP]
>
>Se hai integrato il selettore delle risorse utilizzando il flusso di lavoro Registra, ma non riesci ancora ad accedere all’archivio di consegna, assicurati che i cookie del browser siano puliti. In caso contrario, nella console verrà visualizzato `invalid_credentials All session cookies are empty` errore.

>[!MORELIKETHIS]
>
>* [Integrare il Selettore risorse con varie applicazioni](/help/assets/integrate-asset-selector.md)
>* [Proprietà del Selettore risorse](/help/assets/asset-selector-properties.md)
>* [Integrare il Selettore risorse con Dynamic Media con funzionalità OpenAPI](/help/assets/integrate-asset-selector-dynamic-media-open-api.md)
>* [Personalizzazioni del Selettore risorse](/help/assets/asset-selector-customization.md)
