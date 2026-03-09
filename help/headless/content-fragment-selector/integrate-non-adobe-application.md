---
title: Integrare il selettore dei frammenti di contenuto con applicazioni non Adobe o di terze parti
description: Integra il selettore Frammento di contenuto con varie applicazioni Adobe, non Adobe e di terze parti.
role: Admin, User, Developer
source-git-commit: 3af1a89489af96bf9c9908aea7fb20883956517b
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 5%

---

# Integrazione con un’applicazione non Adobe {#integration-with-non-adobe-application}

Il Selettore dei frammenti di contenuto consente di integrarsi con varie applicazioni non Adobe o di terze parti per consentire loro di lavorare insieme senza problemi.

## Prerequisiti {#prerequisites}

Se integri il selettore dei frammenti di contenuto con un’applicazione non Adobe, utilizza i seguenti prerequisiti:

* [Prerequisiti](/help/headless/content-fragment-selector/overview.md#prerequisites)
* imsClientId
* imsScope
* redirectUrl
* imsOrg
* apikey

Durante l&#39;integrazione con un&#39;applicazione non Adobe, il selettore dei frammenti di contenuto supporta l&#39;autenticazione nell&#39;archivio as a Cloud Service di Adobe Experience Manager (AEM) tramite le proprietà di Identity Management System (IMS), ad esempio `imsScope` o `imsClientID`.

## Configurare il selettore dei frammenti di contenuto per un’applicazione non Adobe {#configure-content-fragment-selector-for-a-non-adobe-application}

Per configurare il selettore dei frammenti di contenuto per un’applicazione non Adobe, è necessario innanzitutto registrare un ticket di supporto per il provisioning prima di procedere con i passaggi di integrazione.

### Registrazione di un ticket di supporto {#logging-a-support-ticket}

Passaggi per registrare un ticket di assistenza tramite Admin Console:

1. Aggiungi **Selettore frammenti di contenuto con frammenti di AEM** nel titolo del ticket.

1. Nella descrizione, includi i seguenti dettagli:

   * URL di Experience Manager as a Cloud Service (ID programma e ID ambiente).
   * Nomi di dominio in cui è ospitata l’applicazione web non Adobe.

## Passaggi dell’integrazione {#integration-steps}

Utilizza il seguente file di esempio `index.html` per l’autenticazione durante l’integrazione del selettore dei frammenti di contenuto con un’applicazione non Adobe:

* Accedere al pacchetto del selettore dei frammenti di contenuto utilizzando il tag `Script`.

* Definisci le proprietà del flusso IMS, ad esempio `imsClientId`, `imsScope` e `redirectURL`.

   * La funzione richiede di definire almeno una delle proprietà `imsClientId` e `imsScope`.
   * Se non si definisce un valore per `redirectURL`, verrà utilizzato l&#39;URL di reindirizzamento registrato per l&#39;ID client.

* Poiché nell&#39;esempio non è stato generato alcun `imsToken`, utilizzare le funzioni `registerFragmentsSelectorsAuthService` e `renderFragmentSelectorWithAuthFlow`.

   * Utilizzare la funzione `registerFragmentsSelectorsAuthService` prima di `renderFragmentSelectorWithAuthFlow` per registrare `imsToken` con il selettore frammento di contenuto.
   * Adobe consiglia di chiamare `registerFragmentsSelectorsAuthService` quando si crea un&#39;istanza del componente.

* Definire l&#39;autenticazione e altre proprietà relative all&#39;accesso as a Cloud Service ai frammenti nella sezione `const props`.
* La variabile globale `PureJSContentFragmentSelectors` viene utilizzata per eseguire il rendering del selettore dei frammenti di contenuto nel browser web.
* Il rendering del selettore dei frammenti di contenuto viene eseguito sull&#39;elemento contenitore `<div>`. Nell’esempio viene utilizzata una finestra di dialogo per visualizzare il Selettore frammento di contenuto.

**Esempio`ìndex.html`**

```html {line-numbers="true"}
<!doctype html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <link rel="icon" type="image/svg+xml" href="/vite.svg" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <title>testing-cf-mfe-integration-with-3rd-party-app</title>
        <script
            id="content-fragments-selector"
            src="https://experience.adobe.com/solutions/CQ-sites-content-fragment-selector/static-assets/resources/content-fragment-selector.js"
        ></script>
        <script>
            const imsProps = {
                imsClientId: '<IMS_CLIENT_ID>',
                imsScope:
                    'additional_info.projectedProductContext, AdobeID, openid, read_organizations',
                redirectUrl: window.location.href,
                onImsServiceInitialized: (service) => {
                    // invoked when the ims service is initialized and is ready
                    console.log('onImsServiceInitialized', service);
                },
                onAccessTokenReceived: (token) => {
                    console.log('onAccessTokenReceived', token);
                },
                onAccessTokenExpired: () => {
                    console.log('onAccessTokenError');
                    // re-trigger sign-in flow
                },
                onErrorReceived: (type, msg) => {
                    console.log('onErrorReceived', type, msg);
                },
            };

            function load() {
                const registeredTokenService =
                    PureJSContentFragmentSelectors.registerContentFragmentSelectorAuthService(
                        imsProps
                    );
                imsInstance = registeredTokenService;
            }

            // initialize the IMS flow before attempting to render the content fragment selector
            load();

            // function that will render the content fragment selector
            function renderContentFragmentSelectorWithAuthFlow() {
                const contentFragmentSelectorDialog = document.getElementById(
                    'content-fragment-selector-dialog'
                );

                const contentFragmentSelectorProps = {
                    inventoryViewToggleEnabled: true,
                    isOpen: true,
                    noWrap: false,
                    orgId: 'YOUR_ORG_ID@AdobeOrg',
                    // repoId: "author-p12345-e67890.adobeaemcloud.com", // if wanted to restrict to a specific repo
                    runningInUnifiedShell: false,
                    onDismiss: () => contentFragmentSelectorDialog.close(),
                    onSubmit: ({ contentFragments }) => {
                        const selectedContentFragment = contentFragments[0];
                        alert(selectedContentFragment.path);
                    },
                };
                // container element on which you want to render the ContentFragmentSelector component
                const container = document.getElementById('content-fragment-selector');

                /// Use the PureJSContentFragmentSelectors in globals to render the ContentFragmentSelector component
                PureJSContentFragmentSelectors.renderContentFragmentSelectorWithAuthFlow(
                    container,
                    contentFragmentSelectorProps,
                    () => contentFragmentSelectorDialog.showModal()
                );
            }
        </script>
    </head>
    <body>
        <div>
            <button onclick="renderContentFragmentSelectorWithAuthFlow()">
                Content Fragment Selector - Select Content Fragments with Ims Flow
            </button>
        </div>
        <dialog id="content-fragment-selector-dialog">
            <div
                id="content-fragment-selector"
                style="height: calc(100vh - 80px); width: calc(100vw - 60px); margin: -20px"
            ></div>
        </dialog>
    </body>
</html>
```

## Impossibile accedere all’archivio di consegna {#unable-to-access-delivery-repository}

Se hai integrato il selettore dei frammenti di contenuto utilizzando il flusso di lavoro Accedi, ma non riesci ancora ad accedere all’archivio di consegna, assicurati che i cookie del browser siano stati puliti.

In caso contrario, l&#39;errore `invalid_credentials All session cookies are empty` potrebbe venire visualizzato nella console.
