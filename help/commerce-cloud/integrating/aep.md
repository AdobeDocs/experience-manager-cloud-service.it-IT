---
title: Componenti core CIF di AEM e integrazione Adobe Experience Platform
description: Scopri come inviare i dati dell’evento storefront da una pagina di prodotto di cui è stato eseguito il rendering AEM all’Experience Platform utilizzando CIF - Experience Platform Connector.
sub-product: Commerce
version: Cloud Service
activity: setup
feature: Commerce Integration Framework
topic: Commerce
role: Architect, Developer
level: Beginner
kt: 10834
thumbnail: 346811.jpeg
source-git-commit: 2ebe9ddccd0b657b8aaeaf005c0ecb5b16079dee
workflow-type: tm+mt
source-wordcount: '2010'
ht-degree: 1%

---


# Componenti core CIF di AEM e integrazione Adobe Experience Platform {#aem-cif-aep-integration}

La [Commerce Integration Framework (CIF)](https://github.com/adobe/aem-core-cif-components) i componenti core forniscono un’integrazione diretta con [Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-overview.html?lang=en) per inoltrare gli eventi storefront e i relativi dati dalle interazioni lato client, come __aggiungi al carrello__.

La [Componenti core CIF di AEM](https://github.com/adobe/aem-core-cif-components) Il progetto fornisce una libreria JavaScript denominata [Connettore Adobe Experience Platform per Adobe Commerce](https://github.com/adobe/aem-core-cif-components/tree/master/extensions/experience-platform-connector) per raccogliere i dati evento dalla tua vetrina Commerce. I dati dell’evento vengono inviati all’Experience Platform in cui vengono utilizzati in altri prodotti Adobe Experience Cloud, come Adobe Analytics e Adobe Target, per creare un profilo di 360 gradi che copre un percorso di clienti. Connettendo i dati Commerce ad altri prodotti in Adobe Experience Cloud, puoi eseguire attività come analizzare il comportamento degli utenti sul tuo sito, eseguire test AB e creare campagne personalizzate.

Ulteriori informazioni sulle [Raccolta dati di Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/collection/home.html) suite di tecnologie che ti consentono di raccogliere dati sull’esperienza del cliente da origini lato client.

## Invia `addToCart` dati dell’evento in Experience Platform {#send-addtocart-to-aep}

I passaggi seguenti mostrano come inviare `addToCart` i dati evento dalle pagine di prodotto sottoposte a rendering AEM all’Experience Platform utilizzando CIF - Experience Platform Connector. Utilizzando l’estensione del browser Adobe Experience Platform Debugger, puoi testare e rivedere i dati inviati.

![Esamina i dati dell’evento addToCart in Adobe Experience Platform Debugger](../assets/aep-integration/EventData-AEM-AEP.png)

## Prerequisiti {#prerequisites}

Devi utilizzare un ambiente di sviluppo locale per completare questa demo. Questo include un&#39;istanza in esecuzione di AEM configurata e connessa a un&#39;istanza Adobe Commerce. Rivedi i requisiti e le fasi per [configurazione dello sviluppo locale con AEM SDK as a Cloud Service](../develop.md).

È inoltre necessario accedere a [Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-ui/ui-guide.html) e le autorizzazioni per creare lo schema, il set di dati e i datastreams per la raccolta di dati. Per ulteriori informazioni, consulta [Gestione delle autorizzazioni](https://experienceleague.adobe.com/docs/experience-platform/collection/permissions.html).

## Configurazione as a Cloud Service di AEM Commerce {#aem-setup}

Per avere un lavoro __AEM Commerce as a Cloud Service__ ambiente locale con il codice e la configurazione necessari, completa i seguenti passaggi.

### Configurazione locale

Segui [Configurazione locale](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/content-and-commerce/storefront/developing/develop.html?#local-setup) procedura per disporre di un ambiente as a Cloud Service AEM Commerce funzionante.

### Configurazione del progetto

Segui [Archetipo di progetto AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/content-and-commerce/storefront/developing/develop.html?#project) per creare un nuovo progetto Commerce (CIF) AEM.

>[!TIP]
>
>Nell’esempio seguente, il progetto Commerce AEM è denominato: `My Demo Storefront`Tuttavia, puoi scegliere il nome del tuo progetto.

![Progetto Commerce AEM](../assets/aep-integration/aem-project-with-commerce.png)


Crea e distribuisci il progetto Commerce AEM appena creato nell’SDK AEM locale eseguendo il seguente comando dalla directory principale del progetto.

```bash
$ mvn clean install -PautoInstallSinglePackage
```

Distribuzione locale `My Demo StoreFront` il sito di e-commerce con codice e contenuto predefiniti si presenta come segue:

![Sito commerciale AEM predefinito](../assets/aep-integration/demo-aem-storefront.png)

### Installare le dipendenze dei connettori Peregrine e CIF-AEP

Per raccogliere e inviare i dati dell’evento dalle pagine delle categorie e dei prodotti di questo sito di AEM Commerce, devi installare la chiave `npm` i pacchetti `ui.frontend` modulo del progetto Commerce AEM.

Passa a `ui.frontend` e installare i pacchetti richiesti eseguendo i seguenti comandi dalla riga di comando.

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
>La `--force` l&#39;argomento è talvolta obbligatorio come [PWA Studi](https://developer.adobe.com/commerce/pwa-studio/) è restrittivo con le dipendenze peer supportate. Di solito, questo non dovrebbe causare problemi.


### Configurare Maven da utilizzare `--force` argomento

Come parte del processo di creazione Maven, l&#39;installazione npm clean (utilizzando `npm ci`) viene attivata. Ciò richiede anche `--force` argomento.

Passa al file POM principale del progetto `pom.xml` e individua le `<id>npm ci</id>` blocco di esecuzione. Aggiorna il blocco in modo che sia simile al seguente:

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

### Cambia formato di configurazione Babel

Passa dall&#39;impostazione predefinita `.babelrc` formato file di configurazione relativo a `babel.config.js` formato. Questo è un formato di configurazione a livello di progetto e consente di applicare i plug-in e i predefiniti al `node_module` con maggiore controllo.

1. Passa a `ui.frontend` e elimina il modulo esistente `.babelrc` file.

1. Crea un `babel.config.js` file che utilizza `peregrine` preimpostazione.

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

Per tradurre i file JavaScript utilizzando il caricatore Babel (`babel-loader`) e webpack, devi modificare il `webpack.common.js` file.

Passa a `ui.frontend` e aggiorna il `webpack.common.js` per avere la seguente regola all&#39;interno del `module` valore proprietà:

```javascript
{
    test: /\.jsx?$/,
    exclude: /node_modules\/(?!@magento\/)/,
    loader: 'babel-loader'
}
```

### Configurare il client Apollo

La [Client Apollo](https://www.apollographql.com/docs/react/) viene utilizzato per gestire i dati locali e remoti con GraphQL. Memorizza anche i risultati delle query GraphQL in una cache locale, normalizzata e in memoria.

Per [`InMemoryCache`](https://www.apollographql.com/docs/react/caching/cache-configuration/) per lavorare in modo efficace, è necessario un `possibleTypes.js` file. Per generare questo file, vedi [Generazione automatica di possibleTypes](https://www.apollographql.com/docs/react/data/fragments/#generating-possibletypes-automatically). Inoltre, consulta la sezione [Implementazione di riferimento di PWA Studi](https://github.com/magento/pwa-studio/blob/1977f38305ff6c0e2b23a9da7beb0b2f69758bed/packages/pwa-buildpack/lib/Utilities/graphQL.js#L106-L120) e un esempio di [`possibleTypes.js`](../assets/aep-integration/possibleTypes.js) file.


1. Passa a `ui.frontend` e salva il file come `./src/main/possibleTypes.js`

1. Aggiorna `webpack.common.js` file `DefinePlugin` per sostituire le variabili statiche richieste durante la generazione.

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

1. Passa a `ui.frontend` e crea la seguente cartella: `src/main/webpack/components/commerce/App`

1. Crea un `config.js` con il seguente contenuto:

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
           // Enable the Experience Platform Connector and define the org and datastream to use
           aep: {
               orgId: // TODO: add your orgId
               datastreamId: // TODO: add your datastreamId
           }
       }
   };
   ```

   >[!IMPORTANT]
   >
   >Mentre potresti già avere familiarità con il [`config.js`](https://github.com/adobe/aem-cif-guides-venia/blob/main/ui.frontend/src/main/components/App/config.js) file da __Guide AEM - Progetto CIF Venia__, sono necessarie alcune modifiche a questo file. Prima di tutto, controlla __TODO__ commenti. Quindi, all&#39;interno del `eventsCollector` trova la proprietà `eventsCollector > aed` e aggiorna `orgId` e `datastreamId` ai valori corretti. [Per saperne di più](./aep.md#add-aep-values-to-aem).

1. Crea un `App.js` con il seguente contenuto. Questo file è simile a un tipico file punto iniziale dell&#39;applicazione React e contiene hook personalizzati e un utilizzo del contesto React per facilitare l&#39;integrazione di Experience Platform.

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
           // implement a proper marketing opt-in, for demo purpose we hard-set the consent cookie
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

   La `EventCollectorContext` esporta il contesto React che:

   - carica la libreria commerce-events-sdk e commerce-events-Collector,
   - li inizializza con una determinata configurazione per Experience Platform e/o ACDS
   - si abbona a tutti gli eventi da Peregrine e li inoltra all’SDK degli eventi

   Puoi esaminare i dettagli di implementazione della `EventCollectorContext` [qui](https://github.com/adobe/aem-core-cif-components/blob/3d4e44d81fff2f398fd2376d24f7b7019f20b31b/extensions/experience-platform-connector/src/events-collector/EventCollectorContext.js).

### Crea e distribuisci il progetto AEM aggiornato

Per verificare che l’installazione, il codice e le modifiche alla configurazione del pacchetto di cui sopra siano corretti, rigenera e distribuisci il progetto AEM Commerce aggiornato utilizzando il seguente comando Maven: `$ mvn clean install -PautoInstallSinglePackage`.

## Configurazione Experience Platform {#aep-setup}

Per ricevere e memorizzare i dati dell’evento provenienti dalle pagine di Commerce AEM, ad esempio categoria e prodotto, completa i seguenti passaggi:

>[!AVAILABILITY]
>
>Assicurati di fare parte della __Profili di prodotto__ sotto __Adobe Experience Platform__ e __Raccolta dati Adobe Experience Platform__. Se necessario, rivolgiti all’amministratore di sistema per creare, aggiornare o assegnare __Profili di prodotto__ in [Admin Console](https://adminconsole.adobe.com/).

### Crea schema con gruppo di campi Commerce

Per definire la struttura dei dati dell’evento commerce, devi creare uno schema Experience Data Model (XDM). Uno schema è un insieme di regole che rappresentano e convalidano la struttura e il formato dei dati.

1. Nel browser, passa alla __Adobe Experience Platform__ home page del prodotto. Esempio: <https://experience.adobe.com/#/@YOUR-ORG-NAME/sname:prod/platform/home>.

1. Individua il __Schemi__ nella sezione di navigazione a sinistra, fai clic sul pulsante __Crea schema__ dalla sezione in alto a destra e seleziona __ExperienceEvent XDM__.

   ![AEP Crea schema](../assets/aep-integration/AEP-Schema-EventSchema-1.png)

1. Denomina lo schema utilizzando __Proprietà schema > Nome visualizzato__ e aggiungere gruppi di campi utilizzando  __Composizione > Gruppi di campi > Aggiungi__ pulsante .

   ![Definizione schema AEP](../assets/aep-integration/AEP-Schema-Definition.png)

1. In __Aggiungi gruppi di campi__ finestra di dialogo, cercare `Commerce`, seleziona __Dettagli Commerce__ e fai clic su __Aggiungi gruppi di campi__.

   ![Definizione schema AEP](../assets/aep-integration/AEP-Schema-Field-Group.png)


>[!TIP]
>
>Consulta la sezione [Nozioni di base sulla composizione dello schema](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html) per ulteriori informazioni.

### Crea set di dati

Per memorizzare i dati dell&#39;evento, devi creare un set di dati conforme alla definizione dello schema. Un set di dati è un costrutto di archiviazione e gestione per una raccolta di dati, in genere una tabella, che contiene uno schema (colonne) e campi (righe).

1. Nel browser, passa alla __Adobe Experience Platform__ home page del prodotto. Esempio: <https://experience.adobe.com/#/@YOUR-ORG-NAME/sname:prod/platform/home>.

1. Individua il __Set di dati__ nella sezione di navigazione a sinistra e fai clic sul pulsante __Creare un set di dati__ dalla sezione in alto a destra.

   ![Creare set di dati AEP](../assets/aep-integration/AEP-Datasets-Create.png)

1. Nella nuova pagina, seleziona __Creare un set di dati dallo schema__ il Card.

   ![Opzione schema Crea set di dati AEP](../assets/aep-integration/AEP-Datasets-Schema-Option.png)

- Nella nuova pagina, __cerca e seleziona__ lo schema creato nel passaggio precedente e fai clic sul pulsante __Successivo__ pulsante .

   ![AEP Crea set di dati Seleziona schema](../assets/aep-integration/AEP-Datasets-Select-Schema.png)

1. Denomina il set di dati utilizzando __Configura set di dati > Nome__ e fai clic sul campo __Fine__ pulsante .

   ![Nome set di dati AEP Create](../assets/aep-integration/AEP-Datasets-Name.png)

>[!TIP]
>
>Consulta la sezione [Panoramica dei set di dati](https://experienceleague.adobe.com/docs/experience-platform/catalog/datasets/overview.html) per ulteriori informazioni.


### Crea Datastream

Completa i seguenti passaggi per creare un Datastream nell’Experience Platform.

1. Nel browser, passa alla __Adobe Experience Platform__ home page del prodotto. Esempio: <https://experience.adobe.com/#/@YOUR-ORG-NAME/sname:prod/platform/home>.

1. Individua il __Datastreams__ nella sezione di navigazione a sinistra e fai clic sul pulsante __Nuovo Datastream__ dalla sezione in alto a destra.

   ![Creazione di Datastreams AEP](../assets/aep-integration/AEP-Datastream-Create.png)

1. Denomina il Datastream utilizzando __Nome__ campo obbligatorio. Sotto la __Schema evento__ selezionare lo schema appena creato e fare clic su __Salva__.

   ![AEP Definisce i Datastreams](../assets/aep-integration/AEP-Datastream-Define.png)

1. Apri il nuovo Datastream creato e fai clic su __Aggiungi servizio__.

   ![Servizio di aggiunta di AEP Datastreams](../assets/aep-integration/AEP-Datastream-Add-Service.png)

1. Sotto la __Servizio__ selezionare il campo __Adobe Experience Platform__ opzione . Sotto __Set di dati evento__ , seleziona il nome del set di dati dal passaggio precedente e fai clic su __Salva__.

   ![Dettagli del servizio Aggiungi reams di dati AEP](../assets/aep-integration/AEP-Datastream-Add-Service-Define.png)

>[!TIP]
>
>Consulta la sezione [Panoramica di Datastream](https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/overview.html) per ulteriori informazioni.

## Aggiungere il valore datastream nella configurazione AEM Commerce {#add-aep-values-to-aem}

Dopo aver completato l&#39;Experience Platform precedente, devi `datastreamId` nella barra a sinistra dei dettagli del Datastream e `orgId` nell&#39;angolo in alto a destra del __Immagine profilo > Informazioni account > Informazioni utente__ modale.

![ID di AEP Datastreams](../assets/aep-integration/AEP-Datastream-ID.png)

1. Nel progetto Commerce AEM `ui.frontend` modulo, aggiorna `config.js` e in particolare `eventsCollector > aep` proprietà dell&#39;oggetto.

1. Crea e distribuisci il progetto AEM Commerce aggiornato


## Trigger `addToCart` evento e verifica della raccolta dati {#event-trigger-verify}

I passaggi precedenti completano la configurazione di AEM Commerce ed Experience Platform. Ora puoi attivare un `addToCart` e verifica la raccolta dati utilizzando il debugger di Experience Platform e il set di dati __Metriche e grafici__ attiva l’interfaccia utente del prodotto.

Per attivare l’evento, puoi utilizzare AEM’autore o il servizio di pubblicazione dalla configurazione locale. Per questo esempio, utilizza AEM autore accedendo al tuo account.

1. Dalla pagina Sites , seleziona la __My Demo StoreFront > noi > it__ e fai clic su __Modifica__ nella barra delle azioni superiore.

1. Dalla barra delle azioni superiore, fai clic su __Visualizza come pubblicato__, quindi fai clic su qualsiasi categoria preferita dalla navigazione della vetrina.

1. Fai clic su qualsiasi scheda di prodotto preferita nel __Pagina di prodotto__, quindi seleziona __colore, dimensioni__ per abilitare __Aggiungi al carrello__ pulsante .


1. Apri __Debugger Adobe Experience Platform__ dal pannello delle estensioni del browser e seleziona __Experience Platform Wed SDK__ nella barra a sinistra.

   ![Debugger AEP](../assets/aep-integration/AEP-Debugger.png)


1. Torna a __Pagina di prodotto__ e fai clic su __Aggiungi al carrello__ pulsante . Questo invia i dati all’Experience Platform. La __Debugger Adobe Experience Platform__ L&#39;estensione mostra i dettagli dell&#39;evento.

   ![Dati evento del componente aggiuntivo AEP Debugger al carrello](../assets/aep-integration/AEP-Debugger-AddToCart-EventData.png)



1. Nell’interfaccia utente del prodotto di Experience Platform, passa a __Set di dati > My Demo StoreFront__, __Attività set di dati__ scheda . Se la __Metriche e grafici__ l’opzione è abilitata, vengono visualizzati gli stati dei dati dell’evento.

   ![Stato dei dati del set di dati di Experience Platform](../assets/aep-integration/AEP-Dataset-AddToCart-EventData.png)



## Dettagli di implementazione {#implementation-details}

La [Connettore Experience Platform CIF](https://github.com/adobe/aem-core-cif-components/tree/master/extensions/experience-platform-connector) è costruito sopra [Connettore di Experience Platform per Adobe Commerce](https://marketplace.magento.com/magento-experience-platform-connector.html), che fa parte del [PWA Studi](https://developer.adobe.com/commerce/pwa-studio/) progetto.

Il progetto PWA Studi consente di creare vetrine Progressive Web Application (PWA) basate su Adobe Commerce o Magenti Open Source. Il progetto contiene anche una libreria di componenti denominata [Peregrina](https://developer.adobe.com/commerce/pwa-studio/api/peregrine/) per aggiungere logica ai componenti visivi. La [Libreria di Peregrin](https://developer.adobe.com/commerce/pwa-studio/api/peregrine/) fornisce anche gli hook React personalizzati utilizzati da [Connettore Experience Platform](https://github.com/adobe/aem-core-cif-components/tree/master/extensions/experience-platform-connector) per integrarsi con Experience Platform senza soluzione di continuità.


## Eventi supportati {#supported-events}

Al momento, sono supportati i seguenti eventi:

- addToCart
- pageView
- customUrl
- referrerUrl

## Risorse aggiuntive {#additional-resources}

Per ulteriori informazioni, consulta le risorse seguenti:

- [PWA Studi](https://developer.adobe.com/commerce/pwa-studio/)
- [Panoramica del connettore di Experience Platform](https://experienceleague.adobe.com/docs/commerce-merchant-services/experience-platform-connector/overview.html)
- [Panoramica di Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/landing/home.html)

