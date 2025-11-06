---
title: Componenti core AEM-CIF e integrazione con Adobe Experience Platform
description: Scopri come inviare i dati di un evento vetrina da una pagina di prodotto di cui è stato eseguito il rendering in AEM a Experience Platform utilizzando il connettore CIF - Experience Platform.
sub-product: Commerce
version: Experience Manager as a Cloud Service
activity: setup
feature: Commerce Integration Framework
topic: Commerce
role: Developer, Developer
level: Beginner
kt: 10834
thumbnail: 346811.jpeg
exl-id: 30bb9b2c-5f00-488e-ad5c-9af7cd2c4735
index: false
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1866'
ht-degree: 1%

---


# Componenti core AEM-CIF e integrazione con Adobe Experience Platform {#aem-cif-aep-integration}

I componenti core [Commerce integration framework (CIF)](https://github.com/adobe/aem-core-cif-components) forniscono un&#39;integrazione perfetta con [Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-overview.html?lang=it) per inoltrare gli eventi storefront e i relativi dati dalle interazioni lato client, ad esempio __aggiungi al carrello__.

Il progetto [AEM CIF Core Components](https://github.com/adobe/aem-core-cif-components) fornisce una libreria JavaScript denominata [Connettore Adobe Experience Platform per Adobe Commerce](https://github.com/adobe/aem-core-cif-components/tree/master/extensions/experience-platform-connector) per raccogliere i dati evento dalla vetrina Commerce. I dati dell’evento vengono inviati ad Experience Platform, dove vengono utilizzati in altri prodotti Adobe Experience Cloud, come Adobe Analytics e Adobe Target, per creare un profilo a 360 gradi che copre un percorso di clienti. Collegando i dati di Commerce ad altri prodotti in Adobe Experience Cloud, puoi eseguire attività come analizzare il comportamento degli utenti sul tuo sito, eseguire test AB e creare campagne personalizzate.

Ulteriori informazioni sulla suite di tecnologie [Raccolta dati di Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/collection/home.html?lang=it) che consente di raccogliere i dati sull&#39;esperienza del cliente da origini lato client.

## Invia dati evento `addToCart` ad Experience Platform {#send-addtocart-to-aep}

Nei passaggi seguenti viene illustrato come inviare i dati dell&#39;evento `addToCart` dalle pagine di prodotto di cui è stato eseguito il rendering in AEM ad Experience Platform utilizzando il connettore CIF - Experience Platform. Utilizzando l’estensione del browser Adobe Experience Platform Debugger, puoi testare e rivedere i dati inviati.

![Rivedi i dati evento addToCart in Adobe Experience Platform Debugger](../assets/aep-integration/EventData-AEM-AEP.png)

## Prerequisiti {#prerequisites}

Utilizza un ambiente di sviluppo locale per completare questa demo. Ciò include un’istanza in esecuzione di AEM configurata e connessa a un’istanza di Adobe Commerce. Rivedi i requisiti e i passaggi per [configurare lo sviluppo locale con AEM as a Cloud Service SDK.](/help/commerce-cloud/cif-storefront/develop.md)

È inoltre necessario accedere a [Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-ui/ui-guide.html?lang=it) e alle autorizzazioni per creare schemi, set di dati e flussi di dati per la raccolta dati. Per ulteriori informazioni, vedere [Gestione autorizzazioni.](https://experienceleague.adobe.com/docs/experience-platform/collection/permissions.html?lang=it)

## Configurazione di AEM Commerce as a Cloud Service {#aem-setup}

Per avere un ambiente locale di __AEM Commerce as a Cloud Service__ funzionante con il codice e la configurazione necessari, completa i passaggi seguenti.

### Configurazione locale

Segui i passaggi [Installazione locale](/help/commerce-cloud/cif-storefront/develop.md#local-setup) per avere un ambiente AEM Commerce as a Cloud Service funzionante.

### Configurazione del progetto

Segui i passaggi di [Archetipo progetto AEM](/help/commerce-cloud/cif-storefront/develop.md#project) per creare un nuovo progetto AEM Commerce (CIF).

>[!TIP]
>
>Nell&#39;esempio seguente, il progetto AEM Commerce è denominato: `My Demo Storefront`, tuttavia, è possibile scegliere il nome del progetto desiderato.

![Progetto AEM Commerce](../assets/aep-integration/aem-project-with-commerce.png)


Crea e distribuisci il progetto AEM Commerce creato nel SDK AEM locale eseguendo il seguente comando dalla directory principale del progetto.

```bash
$ mvn clean install -PautoInstallSinglePackage
```

Il sito di commerce `My Demo StoreFront` distribuito localmente con codice e contenuto predefiniti è simile al seguente:

![Sito Commerce predefinito di AEM](../assets/aep-integration/demo-aem-storefront.png)

### Installare le dipendenze dei connettori Peregrine e CIF-AEP

Per raccogliere e inviare i dati dell&#39;evento dalle pagine categoria e prodotto di questo sito AEM Commerce, installare i pacchetti chiave `npm` nel modulo `ui.frontend` del progetto AEM Commerce.

Passare al modulo `ui.frontend` e installare i pacchetti richiesti eseguendo i seguenti comandi dalla riga di comando.

```bash
npm i --save lodash.get@^4.4.2 lodash.set@^4.3.2
npm i --save apollo-cache-persist@^0.1.1
npm i --save redux-thunk@~2.3.0
npm i --save @adobe/apollo-link-mutation-queue@~1.1.0
npm i --save @magento/peregrine@~12.5.0
npm i --save @adobe/aem-core-cif-react-components --force
npm i --save-dev @magento/babel-preset-peregrine@~1.2.1
npm i --save @adobe/aem-core-cif-experience-platform-connector --force
```

>[!IMPORTANT]
>
>L&#39;argomento `--force` è obbligatorio a volte perché [PWA Studio](https://developer.adobe.com/commerce/pwa-studio/) è restrittivo con le dipendenze dei peer supportate. Di solito, questo non dovrebbe causare alcun problema.


### Configura Maven per utilizzare l’argomento `--force`

Come parte del processo di compilazione Maven, viene attivata l&#39;installazione npm clean (utilizzando `npm ci`). È necessario anche l&#39;argomento `--force`.

Passare al file POM radice del progetto `pom.xml` e individuare il blocco di esecuzione `<id>npm ci</id>`. Aggiorna il blocco come segue:

```xml
<execution>
    <id>npm ci</id>
    <goals>
    <goal>npm</goal>
    </goals>
    <configuration>
    <arguments>ci --force</arguments>
    </configuration>
</execution>
```

### Cambia il formato di configurazione di Babel

Passa dal formato predefinito del file di configurazione relativo `.babelrc` al formato `babel.config.js`. Si tratta di un formato di configurazione a livello di progetto che consente di applicare i plug-in e i predefiniti a `node_module` con un controllo maggiore.

1. Passare al modulo `ui.frontend` ed eliminare il file `.babelrc` esistente.

1. Creare un file `babel.config.js` che utilizza il predefinito `peregrine`.

   ```javascript
   const peregrine = require('@magento/babel-preset-peregrine');
   
   module.exports = (api, opts = {}) => {
       const config = {
           ...peregrine(api, opts),
           sourceType: 'unambiguous'
       } 
   
       config.plugins = config.plugins.filter(plugin => plugin !== 'react-refresh/babel');
   
       return config;
   }
   ```

### Configurare il webpack per l&#39;utilizzo di Babel

Per eseguire la transpilazione dei file JavaScript utilizzando Babel loader (`babel-loader`) e Webpack, modificare il file `webpack.common.js`.

Passare al modulo `ui.frontend` e aggiornare il file `webpack.common.js` in modo da poter avere la regola seguente all&#39;interno del valore della proprietà `module`:

```javascript
{
    test: /\.jsx?$/,
    exclude: /node_modules\/(?!@magento\/)/,
    loader: 'babel-loader'
}
```

### Configura client Apollo

Il [client Apollo](https://www.apollographql.com/docs/react/) viene utilizzato per gestire dati locali e remoti con GraphQL. Memorizza inoltre i risultati delle query GraphQL in una cache locale normalizzata in memoria.

Affinché [`InMemoryCache`](https://www.apollographql.com/docs/react/caching/cache-configuration/) funzioni correttamente, è necessario un file `possibleTypes.js`. Per generare questo file, vedere [Generazione automatica di possibleTypes.](https://www.apollographql.com/docs/react/data/fragments/#generating-possibletypes-automatically)

Vedere anche l&#39;implementazione di riferimento [PWA Studio](https://github.com/magento/pwa-studio/blob/1977f38305ff6c0e2b23a9da7beb0b2f69758bed/packages/pwa-buildpack/lib/Utilities/graphQL.js#L106-L120) e un esempio di un file [`possibleTypes.js`](../assets/aep-integration/possibleTypes.js).

1. Passare al modulo `ui.frontend` e salvare il file come `./src/main/possibleTypes.js`

1. Aggiornare la sezione `webpack.common.js` del file `DefinePlugin` in modo da poter sostituire le variabili statiche richieste durante il tempo di compilazione.

   ```javascript
   const { DefinePlugin } = require('webpack');
   const { POSSIBLE_TYPES } = require('./src/main/possibleTypes');
   
   ...
   
   plugins: [
       ...
       new DefinePlugin({
           'process.env.USE_STORE_CODE_IN_URL': false,
           POSSIBLE_TYPES
       })
   ]
   ```

### Inizializzare i componenti core Peregrine e CIF

Per inizializzare i componenti core Peregrine e CIF basati su React, crea la configurazione e i file JavaScript richiesti.

1. Passare al modulo `ui.frontend` e creare la cartella seguente: `src/main/webpack/components/commerce/App`

1. Crea un file `config.js` con il seguente contenuto:

   ```javascript
   // get and parse the CIF store configuration from the <head>
   const storeConfigEl = document.querySelector('meta[name="store-config"]');
   const storeConfig = storeConfigEl ? JSON.parse(storeConfigEl.content) : {};
   
   // the following global variables are needed for some of the peregrine features
   window.STORE_VIEW_CODE = storeConfig.storeView || 'default';
   window.AVAILABLE_STORE_VIEWS = [
       {
           code: window.STORE_VIEW_CODE,
           base_currency_code: 'USD',
           default_display_currency_code: 'USD',
           id: 1,
           locale: 'en',
           secure_base_media_url: '',
           store_name: 'My Demo StoreFront'
       }
   ];
   window.STORE_NAME = window.STORE_VIEW_CODE;
   window.DEFAULT_COUNTRY_CODE = 'en';
   
   export default {
       storeView: window.STORE_VIEW_CODE,
       graphqlEndpoint: storeConfig.graphqlEndpoint,
       // Can be GET or POST. When selecting GET, this applies to cache-able GraphQL query requests only.
       // Mutations will always be executed as POST requests.
       graphqlMethod: storeConfig.graphqlMethod,
       headers: storeConfig.headers,
   
       mountingPoints: {
           // TODO: define the application specific mount points as they may be used by <Portal> and <PortalPlacer>
       },
       pagePaths: {
           // TODO: define the application specific paths/urls as they may be used by the components
           baseUrl: storeConfig.storeRootUrl
       },
       eventsCollector: {
           eventForwarding: {
               acds: true,
               aep: false,
           }
       }
   };
   ```

   >[!IMPORTANT]
   >
   >È possibile che tu abbia già familiarità con il file [`config.js`](https://github.com/adobe/aem-cif-guides-venia/blob/main/ui.frontend/src/main/components/App/config.js) di __AEM Guides - CIF Venia Project__, ma è necessario apportare alcune modifiche a questo file. Rivedi innanzitutto eventuali commenti di __TODO__. Quindi, all&#39;interno della proprietà `eventsCollector`, trovare l&#39;oggetto `eventsCollector > aep` e aggiornare le proprietà `orgId` e `datastreamId` ai valori corretti. [Ulteriori informazioni.](#add-aep-values-to-aem)

1. Creare un file `App.js` con il contenuto seguente. Questo file è simile a un tipico file del punto di avvio dell’applicazione React e contiene gli hook React e personalizzati e l’utilizzo di React Context per facilitare l’integrazione con Experience Platform.

   ```javascript
   import config from './config';
   
   import React, { useEffect } from 'react';
   import ReactDOM from 'react-dom';
   import { IntlProvider } from 'react-intl';
   import { BrowserRouter as Router } from 'react-router-dom';
   import { combineReducers, createStore } from 'redux';
   import { Provider as ReduxProvider } from 'react-redux';
   import { createHttpLink, ApolloProvider } from '@apollo/client';
   import { ConfigContextProvider, useCustomUrlEvent, useReferrerEvent, usePageEvent, useDataLayerEvents, useAddToCartEvent } from '@adobe/aem-core-cif-react-components';
   import { EventCollectorContextProvider, useEventCollectorContext } from '@adobe/aem-core-cif-experience-platform-connector';
   import { useAdapter } from '@magento/peregrine/lib/talons/Adapter/useAdapter';
   import { customFetchToShrinkQuery } from '@magento/peregrine/lib/Apollo/links';
   import { BrowserPersistence } from '@magento/peregrine/lib/util';
   import { default as PeregrineContextProvider } from '@magento/peregrine/lib/PeregrineContextProvider';
   import { enhancer, reducers } from '@magento/peregrine/lib/store';
   
   const storage = new BrowserPersistence();
   const store = createStore(combineReducers(reducers), enhancer);
   
   storage.setItem('store_view_code', config.storeView);
   
   const App = () => {
       const [{ sdk: mse }] = useEventCollectorContext();
   
       // trigger page-level events
       useCustomUrlEvent({ mse });
       useReferrerEvent({ mse });
       usePageEvent({ mse });
       // listen for add-to-cart events and enable forwarding to the magento storefront events sdk
       useAddToCartEvent(({ mse }));
       // enable CIF specific event forwarding to the Adobe Client Data Layer
       useDataLayerEvents();
   
       useEffect(() => {
           // implement a proper marketing opt-in, for demo purpose you hard-set the consent cookie
           if (document.cookie.indexOf('mg_dnt') < 0) {
               document.cookie += '; mg_dnt=track';
           }
       }, []);
   
       // TODO: use the App to create Portals and PortalPlaceholders to mount the CIF / Peregrine components to the server side rendered markup
       return <></>;
   };
   
   const AppContext = ({ children }) => {
       const { storeView, graphqlEndpoint, graphqlMethod = 'POST', headers = {}, eventsCollector } = config;
       const { apolloProps } = useAdapter({
           apiUrl: new URL(graphqlEndpoint, window.location.origin).toString(),
           configureLinks: (links, apiBase) =>
               // reconfigure the HTTP link to use the configured graphqlEndpoint, graphqlMethod and storeView header
   
               links.set('HTTP', createHttpLink({
                   fetch: customFetchToShrinkQuery,
                   useGETForQueries: graphqlMethod !== 'POST',
                   uri: apiBase,
                   headers: { ...headers, 'Store': storeView }
               }))
       });
   
       return (
           <ApolloProvider {...apolloProps}>
               <IntlProvider locale='en' messages={{}}>
                   <ConfigContextProvider config={config}>
                       <ReduxProvider store={store}>
                           <PeregrineContextProvider>
                               <EventCollectorContextProvider {...eventsCollector}>
                                   {children}
                               </EventCollectorContextProvider>
                           </PeregrineContextProvider>
                       </ReduxProvider>
                   </ConfigContextProvider>
               </IntlProvider>
           </ApolloProvider>
       );
   };
   
   window.onload = async () => {
       const root = document.createElement('div');
       document.body.appendChild(root);
   
       ReactDOM.render(
           <Router>
               <AppContext>
                   <App />
               </AppContext>
           </Router>,
           root
       );
   };
   ```

   `EventCollectorContext` esporta il contesto di React che:

   - carica la libreria commerce-events-sdk e commerce-events-collector,
   - li inizializza con una determinata configurazione per Experience Platform e/o ACDS
   - si iscrive a tutti gli eventi da Peregrine e li inoltra al SDK degli eventi

   È possibile rivedere i dettagli di implementazione di `EventCollectorContext`. Vedi [aem-core-cif-components su GitHub.](https://github.com/adobe/aem-core-cif-components/blob/3d4e44d81fff2f398fd2376d24f7b7019f20b31b/extensions/experience-platform-connector/src/events-collector/EventCollectorContext.js)

### Creare e distribuire il progetto AEM aggiornato {#build-and-deploy}

Per verificare che l&#39;installazione del pacchetto, il codice e le modifiche di configurazione siano corretti, ricompilare e distribuire il progetto AEM Commerce aggiornato utilizzando il comando Maven seguente: `$ mvn clean install -PautoInstallSinglePackage`.

## Configurazione di Experience Platform {#aep-setup}

La procedura seguente illustra come ricevere e memorizzare i dati dell’evento provenienti dalle pagine di AEM Commerce, ad esempio categoria e prodotto:

>[!AVAILABILITY]
>
>Assicurati di far parte dei __profili di prodotto__ corretti in __Adobe Experience Platform__ e __Raccolta dati di Adobe Experience Platform__. Se necessario, contatta l&#39;amministratore di sistema per creare, aggiornare o assegnare __profili di prodotto__ in [Admin Console.](https://adminconsole.adobe.com/)

### Crea schema con gruppo di campi Commerce {#create-schema}

Per definire la struttura per i dati dell’evento Commerce, devi creare uno schema Experience Data Model (XDM). Uno schema è un insieme di regole che rappresentano e convalidano la struttura e il formato dei dati.

1. Nel browser passare alla home page del prodotto __Adobe Experience Platform__. Ad esempio, <https://experience.adobe.com/#/@YOUR-ORG-NAME/sname:prod/platform/home>.

1. Individua il menu __Schemi__ nella sezione di navigazione a sinistra, fai clic sul pulsante __Crea schema__ nella sezione in alto a destra e seleziona __XDM ExperienceEvent__.

   ![Crea schema di AEP](../assets/aep-integration/AEP-Schema-EventSchema-1.png)

1. Denomina lo schema utilizzando il campo __Proprietà schema > Nome visualizzato__ e aggiungi gruppi di campi utilizzando il pulsante __Composizione > Gruppi di campi > Aggiungi__.

   ![Definizione schema AEP](../assets/aep-integration/AEP-Schema-Definition.png)

1. Nella finestra di dialogo __Aggiungi gruppi di campi__, cerca `Commerce`, seleziona la casella di controllo __Dettagli Commerce__ e fai clic su __Aggiungi gruppi di campi__.

   ![Definizione schema AEP](../assets/aep-integration/AEP-Schema-Field-Group.png)


>[!TIP]
>
>Per ulteriori informazioni, vedere le [nozioni di base sulla composizione dello schema](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=it).

### Crea set di dati {#create-dataset}

Per memorizzare i dati dell’evento, è necessario creare un set di dati conforme alla definizione dello schema. Un set di dati è un costrutto di archiviazione e gestione per una raccolta di dati, in genere una tabella, che contiene uno schema (colonne) e dei campi (righe).

1. Nel browser passare alla home page del prodotto __Adobe Experience Platform__. Ad esempio, <https://experience.adobe.com/#/@YOUR-ORG-NAME/sname:prod/platform/home>.

1. Individua il menu __Set di dati__ nella sezione di navigazione a sinistra e fai clic sul pulsante __Crea set di dati__ nella sezione in alto a destra.

   ![Crea set di dati in AEP](../assets/aep-integration/AEP-Datasets-Create.png)

1. Nella nuova pagina, seleziona __Crea set di dati dalla scheda schema__.

   ![Opzione schema per creazione set di dati in AEP](../assets/aep-integration/AEP-Datasets-Schema-Option.png)

   Nella nuova pagina, __cerca e seleziona__ lo schema creato nel passaggio precedente, quindi fai clic sul pulsante __Successivo__.

   ![AEP - Crea set di dati - Seleziona schema](../assets/aep-integration/AEP-Datasets-Select-Schema.png)

1. Assegna un nome al set di dati utilizzando il campo __Configura set di dati > Nome__ e fai clic sul pulsante __Fine__.

   ![Nome set di dati di creazione AEP](../assets/aep-integration/AEP-Datasets-Name.png)

>[!TIP]
>
>Per ulteriori informazioni, vedere [Panoramica sui set di dati](https://experienceleague.adobe.com/docs/experience-platform/catalog/datasets/overview.html?lang=it).


### Crea stream di dati {#create-datastream}

Completa i passaggi seguenti per creare uno stream di dati in Experience Platform.

1. Nel browser passare alla home page del prodotto __Adobe Experience Platform__. Ad esempio, <https://experience.adobe.com/#/@YOUR-ORG-NAME/sname:prod/platform/home>.

1. Individua il menu __Datastreams__ nella sezione di navigazione a sinistra e fai clic sul pulsante __New Datastream__ nella sezione in alto a destra.

   ![AEP - Crea flussi di dati](../assets/aep-integration/AEP-Datastream-Create.png)

1. Denomina lo stream di dati utilizzando il campo obbligatorio __Name__. Nel campo __Schema evento__, seleziona lo schema creato e fai clic su __Salva__.

   ![AEP Definisci flussi di dati](../assets/aep-integration/AEP-Datastream-Define.png)

1. Aprire lo stream di dati creato e fare clic su __Aggiungi servizio__.

   ![Servizio di aggiunta flussi di dati AEP](../assets/aep-integration/AEP-Datastream-Add-Service.png)

1. Nel campo __Servizio__, seleziona l&#39;opzione __Adobe Experience Platform__. Nel campo __Set di dati evento__, seleziona il nome del set di dati del passaggio precedente e fai clic su __Salva__.

   ![Dettagli servizio aggiunta flussi di dati AEP](../assets/aep-integration/AEP-Datastream-Add-Service-Define.png)

>[!TIP]
>
>Per ulteriori informazioni, vedere [Panoramica sullo stream di dati](https://experienceleague.adobe.com/docs/experience-platform/datastreams/overview.html?lang=it).

## Aggiungere valore dello stream di dati nella configurazione di AEM Commerce {#add-aep-values-to-aem}

Dopo aver completato la configurazione di Experience Platform, dovresti disporre di `datastreamId` nella barra a sinistra dei dettagli dello stream di dati e di `orgId` nell&#39;angolo in alto a destra della finestra modale __Immagine profilo > Informazioni account > Informazioni utente__.

![ID flussi di dati AEP](../assets/aep-integration/AEP-Datastream-ID.png)

1. Nel modulo `ui.frontend` del progetto AEM Commerce, aggiorna il file `config.js` e in particolare le proprietà dell&#39;oggetto `eventsCollector > aep`.

1. Creare e distribuire il progetto Commerce aggiornato di AEM


## Attiva l&#39;evento `addToCart` e verifica la raccolta dati {#event-trigger-verify}

I passaggi precedenti completano la configurazione di AEM Commerce e Experience Platform. Ora puoi attivare un evento `addToCart` e verificare la raccolta dati utilizzando l&#39;estensione Google Chrome _Ispettore snowplow_ e il set di dati __Metriche e grafici__ nell&#39;interfaccia utente del prodotto.

Per attivare l’evento, puoi utilizzare AEM Author o il servizio di pubblicazione dalla configurazione locale. Per questo esempio, utilizza AEM Author effettuando l’accesso al tuo account.

1. Dalla pagina Sites, seleziona la pagina __My Demo StoreFront > us > en__ e fai clic su __Modifica__ nella barra delle azioni superiore.

1. Dalla barra delle azioni superiore, fai clic su __Visualizza come pubblicato__, quindi fai clic su una categoria preferita nell&#39;area di navigazione della vetrina.

1. Fai clic su una scheda prodotto preferita nella __pagina prodotto__, quindi seleziona __colore, dimensione__ per abilitare il pulsante __Aggiungi al carrello__.

1. Apri l&#39;estensione __Snowplow Inspector__ dal pannello delle estensioni del browser e seleziona __Experience Platform Wed SDK__ nella barra a sinistra.

1. Torna alla __pagina prodotto__ e fai clic sul pulsante __Aggiungi al carrello__. In questo modo i dati vengono inviati ad Experience Platform. L&#39;estensione __Adobe Experience Platform Debugger__ mostra i dettagli dell&#39;evento.

   ![Dati Evento Del Componente Aggiuntivo Del Debugger Di AEP](../assets/aep-integration/AEP-Debugger-AddToCart-EventData.png)

1. Nell&#39;interfaccia utente del prodotto Experience Platform, passa a __Set di dati > My Demo StoreFront__, nella scheda __Attività set di dati__. Se __Metriche e grafici__ è abilitato, vengono visualizzate le statistiche dei dati evento.

   ![Statistiche dei dati del set di dati di Experience Platform](../assets/aep-integration/AEP-Dataset-AddToCart-EventData.png)

## Dettagli di implementazione {#implementation-details}

Il [connettore Experience Platform di CIF](https://github.com/adobe/aem-core-cif-components/tree/master/extensions/experience-platform-connector) è basato sulla [connessione dati per Adobe Commerce](https://commercemarketplace.adobe.com/magento-experience-platform-connector.html), che fa parte del progetto [PWA Studio](https://developer.adobe.com/commerce/pwa-studio/).

Il progetto PWA Studio consente di creare vetrine di Progressive Web Application (PWA) con tecnologia Adobe Commerce o Magento Open Source. Il progetto contiene anche una libreria di componenti denominata [Peregrin](https://developer.adobe.com/commerce/pwa-studio/api/peregrine/) per l&#39;aggiunta di logica ai componenti visivi. La [libreria Peregrin](https://developer.adobe.com/commerce/pwa-studio/api/peregrine/) fornisce anche gli hook React personalizzati utilizzati da [Connettore Experience Platform di CIF](https://github.com/adobe/aem-core-cif-components/tree/master/extensions/experience-platform-connector) per l&#39;integrazione con Experience Platform senza problemi.

## Eventi supportati {#supported-events}

Al momento, sono supportati i seguenti eventi:

__Eventi Experience XDM :__

1. Aggiungi al carrello (AEM)
1. Visualizza pagina (AEM)
1. Visualizza prodotto (AEM)
1. Richiesta di ricerca inviata (AEM)
1. Risposta alla ricerca ricevuta (AEM)

Quando [Componenti peregrini](https://developer.adobe.com/commerce/pwa-studio/guides/packages/peregrine/) vengono riutilizzati nel progetto AEM Commerce:

__Eventi Experience XDM :__

1. Rimuovi dal carrello
1. Apri carrello
1. Visualizza carrello
1. Acquisto immediato
1. Avvia estrazione
1. Completa il checkout

__Eventi XDM del profilo :__

1. Accedi
1. Crea account
1. Modifica account

## Risorse aggiuntive {#additional-resources}

Per ulteriori informazioni, consulta le risorse seguenti:

- [PWA Studio](https://developer.adobe.com/commerce/pwa-studio/)
- [[!DNL Data Connection] panoramica](https://experienceleague.adobe.com/docs/commerce-merchant-services/data-connection/overview.html?lang=it)
- [[!DNL Data Connection] Eventi](https://experienceleague.adobe.com/docs/commerce-merchant-services/data-connection/event-forwarding/events.html?lang=it)
- [Panoramica di Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/landing/home.html?lang=it)
