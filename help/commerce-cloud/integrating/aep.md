---
title: Componenti core AEM-CIF e integrazione con Adobe Experience Platform
description: Scopri come inviare i dati di un evento vetrina da una pagina di prodotto di cui è stato eseguito il rendering AEM all’Experience Platform utilizzando il connettore CIF - Experience Platform.
sub-product: Commerce
version: Cloud Service
activity: setup
feature: Commerce Integration Framework
topic: Commerce
role: Architect, Developer
level: Beginner
kt: 10834
thumbnail: 346811.jpeg
exl-id: 30bb9b2c-5f00-488e-ad5c-9af7cd2c4735
source-git-commit: 05e4adb0d7ada0f7cea98858229484bf8cca0d16
workflow-type: tm+mt
source-wordcount: '1866'
ht-degree: 1%

---


# Componenti core AEM-CIF e integrazione con Adobe Experience Platform {#aem-cif-aep-integration}

I [componenti principali di Commerce Integration Framework (CIF)](https://github.com/adobe/aem-core-cif-components) forniscono ai integrazione diretta Adobe Experience Platform [](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-overview.html?lang=en) per inoltrare gli eventi storefront e i relativi dati dalle interazioni lato client, ad esempio __Aggiungi al carrello__.

Il [progetto CIF Core Components](https://github.com/adobe/aem-core-cif-components) di AEM fornisce un connettore JavaScript libreria chiamato [Adobe Experience Platform per Adobe Systems Commerce](https://github.com/adobe/aem-core-cif-components/tree/master/extensions/experience-platform-connector) per raccogliere dati sugli eventi dallo storefront di Commerce. Tali dati di evento vengono inviati all&#39;Experience Platform in cui vengono utilizzati in altri prodotti Adobe Experience Cloud, come Adobe Analytics e Adobe Target per versione un profilo a 360 gradi che copre un percorso del cliente. Collegando i dati di Commerce ad altri prodotti nel Adobe Experience Cloud, puoi eseguire attività like analizzare utente comportamento sul tuo sito, eseguire test AB e creare campagne personalizzate.

Scopri ulteriori informazioni sulla [suite di tecnologie Experience Platform Data Collection](https://experienceleague.adobe.com/docs/experience-platform/collection/home.html) che consente di raccogliere dati esperienza del cliente da origini lato client.

## Inviare `addToCart` i dati dell&#39;evento al Experience Platform {#send-addtocart-to-aep}

I passaggi seguenti mostrano come inviare `addToCart` dati evento dalle pagine di prodotti sottoposte a rendering AEM all’Experience Platform utilizzando il connettore CIF - Experience Platform. Utilizzando l’estensione del browser Adobi Experience Platform Debugger, puoi verificare e rivedere i dati inviati.

![Rivedi i dati dell’evento addToCart in Adobe Experience Platform Debugger](../assets/aep-integration/EventData-AEM-AEP.png)

## Prerequisiti {#prerequisites}

Utilizza un ambiente di sviluppo locale per completare questa demo. Ciò include un istanza in esecuzione di AEM configurato e connesso a un istanza Commerce di Adobe Systems. Esamina i requisiti e i passaggi per [l&#39;impostazione dello sviluppo locale con AEM come SDK](../develop.md) Cloud Service.

È inoltre necessario accesso per Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-ui/ui-guide.html) e autorizzazioni per creare lo schema, il set di dati e i flussi di dati per [la raccolta di dati. Per ulteriori informazioni, vedere [Gestione delle](https://experienceleague.adobe.com/docs/experience-platform/collection/permissions.html) autorizzazioni.

## AEM Commerce come configurazione Cloud Service {#aem-setup}

Per fare in modo che AEM Commerce funzioni __come ambiente locale Cloud Service__ con il codice e la configurazione necessari, completa i passaggi seguenti.

### Configurazione locale

Segui le [Configurazione locale](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/content-and-commerce/storefront/developing/develop.html?#local-setup) per poter disporre di un ambiente as a Cloud Service per l’AEM Commerce funzionante.

### Configurazione del progetto

Segui le [Archetipo progetto AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/content-and-commerce/storefront/developing/develop.html?#project) per creare un nuovo progetto AEM Commerce (CIF).

>[!TIP]
>
>Nell&#39;esempio seguente viene denominato il progetto AEM Commerce: `My Demo Storefront`, tuttavia, è possibile scegliere il nome del progetto personalizzato.

![Progetto AEM Commerce](../assets/aep-integration/aem-project-with-commerce.png)


Crea e distribuire il progetto AEM Commerce creato all&#39;SDK AEM locale eseguendo il comando seguente dalla directory principale del progetto.

```bash
$ mvn clean install -PautoInstallSinglePackage
```

Il sito di eCommerce distribuito `My Demo StoreFront` localmente con codice e contenuto predefiniti si presenta like seguente:

![Sito di AEM Commerce predefinito](../assets/aep-integration/demo-aem-storefront.png)

### Installare le dipendenze dei connettori Peregrine e CIF-AEP

Per raccogliere e inviare i dati dell’evento dalle pagine delle categorie e dei prodotti di questo sito AEM Commerce, installa la chiave `npm` pacchetti in `ui.frontend` modulo del progetto AEM Commerce.

Accedi a `ui.frontend` e installare i pacchetti richiesti eseguendo i seguenti comandi dalla riga di comando.

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
>L&#39;argomento `--force` è talvolta obbligatorio in quanto [PWA Studio](https://developer.adobe.com/commerce/pwa-studio/) è restrittivo con le dipendenze peer supportate. Di solito, questo non dovrebbe causare alcun problema.


### Configura Maven per usare l&#39;argomento `--force`

Come parte del processo di versione Maven, viene attivata l&#39;installazione pulita npm (utilizzando `npm ci`). Questo richiede anche l&#39;argomento `--force` .

Individua il file `pom.xml` POM principale del progetto e individua il blocco di `<id>npm ci</id>` esecuzione. Aggiorna il blocco in modo che appaia like seguente:

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

Passa dal formato di file di configurazione relativo al formato predefinito `.babelrc` `babel.config.js` . Si tratta di un formato di configurazione a livello di progetto e consente di applicare i plug-in e i preset al con un `node_module` maggiore controllo.

1. Passare al `ui.frontend` modulo ed eliminare il file esistente `.babelrc` .

1. Crea un `babel.config.js` file che utilizza il `peregrine` predefinito.

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

### Configurare webpack per utilizzare Babel

Per tradurre i file JavaScript usando Babel loader (`babel-loader`) e webpack, modificate il `webpack.common.js` file.

Passare al `ui.frontend` modulo e aggiornare il `webpack.common.js` file in modo da poter avere i seguenti regola all&#39;interno del valore della `module` proprietà:

```javascript
{
    test: /\.jsx?$/,
    exclude: /node_modules\/(?!@magento\/)/,
    loader: 'babel-loader'
}
```

### Configurare Apollo Client

Il [Client Apollo](https://www.apollographql.com/docs/react/) viene utilizzato per gestire dati locali e remoti con GraphQL. Memorizza inoltre i risultati delle query GraphQL in una cache locale normalizzata in memoria.

Per [`InMemoryCache`](https://www.apollographql.com/docs/react/caching/cache-configuration/) per funzionare in modo efficace, è necessario `possibleTypes.js` file. Per generare questo file, vedere [Generazione automatica](https://www.apollographql.com/docs/react/data/fragments/#generating-possibletypes-automatically) di possibleTypes. Vedere anche il [implementazione](https://github.com/magento/pwa-studio/blob/1977f38305ff6c0e2b23a9da7beb0b2f69758bed/packages/pwa-buildpack/lib/Utilities/graphQL.js#L106-L120) di riferimento PWA Studio e un esempio di file [`possibleTypes.js`](../assets/aep-integration/possibleTypes.js) .


1. Passare al `ui.frontend` modulo e salvare il file come `./src/main/possibleTypes.js`

1. Aggiornare la sezione del `webpack.common.js` `DefinePlugin` file in modo da poter sostituire le variabili statiche richieste durante versione periodo.

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

Per inizializzare i componenti di base Peregrine e CIF basati su React, creare i file di configurazione e JavaScript richiesti.

1. Accedi a `ui.frontend` e crea la seguente cartella: `src/main/webpack/components/commerce/App`

1. Crea un `config.js` file con le seguenti contenuto:

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
   >Anche se potresti già avere familiarità con il [`config.js`](https://github.com/adobe/aem-cif-guides-venia/blob/main/ui.frontend/src/main/components/App/config.js) file di __AEM Guides - CIF Venia Project__, ci sono alcune modifiche che devi apportare a questo file. Innanzitutto, esamina qualsiasi __commenti TODO__ . Quindi, all&#39;interno della `eventsCollector` proprietà, individuare l&#39;oggetto `eventsCollector > aep` e aggiornare le `orgId` proprietà e `datastreamId` ai valori corretti. [Ulteriori informazioni](./aep.md#add-aep-values-to-aem).

1. Crea un `App.js` file con le seguenti contenuto. Questo file assomiglia a un tipico file del punto di partenza applicazione di React e contiene React e hook personalizzati e l&#39;utilizzo di React Context per facilitare l&#39;integrazione del Experience Platform.

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

   Il `EventCollectorContext` esporta il contesto React che:

   - carica la libreria commerce-events-sdk e commerce-events-collector,
   - li inizializza con una determinata configurazione, ad Experience Platform e/o ACDS
   - si abbona a tutti gli eventi da Peregrine e li inoltra all’SDK degli eventi

   Puoi rivedere i dettagli di implementazione di `EventCollectorContext` [qui](https://github.com/adobe/aem-core-cif-components/blob/3d4e44d81fff2f398fd2376d24f7b7019f20b31b/extensions/experience-platform-connector/src/events-collector/EventCollectorContext.js).

### Creare e distribuire il progetto AEM aggiornato

Per verificare che le modifiche di installazione, codice e configurazione del pacchetto di cui sopra siano corrette, ricompila e distribuisci il progetto Commerce dell’AEM aggiornato utilizzando il seguente comando Maven: `$ mvn clean install -PautoInstallSinglePackage`.

## Experience Platform configurazione {#aep-setup}

Per ricevere e store i dati degli eventi provenienti dalle pagine di AEM Commerce come categoria e prodotto, completa i seguenti passaggi:

>[!AVAILABILITY]
>
>Assicurati di far parte dei profili di prodotto corretti __in__ Raccolta __dati Adobe Experience Platform e__ Adobe Experience Platform __.__ Se necessario, collabora con l&#39;amministratore di sistema per creare, aggiornare o assegnare __profili__ di [prodotto in Admin Console](https://adminconsole.adobe.com/).

### Schema Crea con gruppo di campi Commerce

Per definire la struttura dei dati degli eventi commerciali, devi creare uno schema XDM (Experience Data Model). Uno schema è un insieme di regole che rappresentano e convalidano la struttura e il formato dei dati.

1. Nella browser, passate alla __home page del prodotto Adobe Experience Platform__ . Esempio: <https://experience.adobe.com/#/@YOUR-ORG-NAME/sname:prod/platform/home>.

1. Individua il __menu Schemi__ nella sezione navigazione sinistra, fai clic sul __pulsante Schema__ Crea nella sezione in alto a destra e seleziona __XDM ExperienceEvent__.

   ![Schema Crea AEP](../assets/aep-integration/AEP-Schema-EventSchema-1.png)

1. Denomina lo schema utilizzando __Proprietà schema > Nome visualizzato__ e aggiungere gruppi di campi utilizzando  __Composizione > Gruppi di campi > Aggiungi__ pulsante.

   ![Definizione schema AEP](../assets/aep-integration/AEP-Schema-Definition.png)

1. In __Aggiungi gruppi di campi__ finestra di dialogo, cerca `Commerce`, seleziona la __Dettagli Commerce__ e fai clic su __Aggiungi gruppi di campi__.

   ![Definizione schema AEP](../assets/aep-integration/AEP-Schema-Field-Group.png)


>[!TIP]
>
>Consulta la [Nozioni di base sulla composizione dello schema](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html) per ulteriori informazioni.

### Crea set di dati

Per memorizzare i dati dell’evento, è necessario creare un set di dati conforme alla definizione dello schema. Un set di dati è un costrutto di archiviazione e gestione per una raccolta di dati, in genere una tabella, che contiene uno schema (colonne) e dei campi (righe).

1. Nel browser, passa a __Adobe Experience Platform__ home page del prodotto. Esempio: <https://experience.adobe.com/#/@YOUR-ORG-NAME/sname:prod/platform/home>.

1. Individuare il __menu Dataset nella sezione navigazione sinistra e fare clic sulla__ pulsante del set di __dati__ Crea dalla sezione superiore destra.

   ![Set di dati AEP Crea](../assets/aep-integration/AEP-Datasets-Create.png)

1. Nella nuova pagina selezionare __Crea dataset da scheda schema__ .

   ![Opzione Schema set di dati AEP Crea](../assets/aep-integration/AEP-Datasets-Schema-Option.png)

   Nella nuova pagina ricerca __e selezionare__ lo schema creato nel passaggio precedente, quindi fare clic sulla __pulsante Successivo__ .

   ![Crea schema set di dati per selezione AEP](../assets/aep-integration/AEP-Datasets-Select-Schema.png)

1. Denomina il set di dati utilizzando __Configura set di dati > Nome__ e fare clic sul pulsante __Fine__ pulsante.

   ![Nome set di dati AEP Crea](../assets/aep-integration/AEP-Datasets-Name.png)

>[!TIP]
>
>Per ulteriori informazioni, consulta la [panoramica](https://experienceleague.adobe.com/docs/experience-platform/catalog/datasets/overview.html) dei set di dati.


### Crea Datastream

Tutte le applicazioni la procedura seguente per creare un flusso di dati nella Experience Platform.

1. Nella browser, passate alla __home page del prodotto Adobe Experience Platform__ . Esempio: <https://experience.adobe.com/#/@YOUR-ORG-NAME/sname:prod/platform/home>.

1. Individua il __menu Datastreams__ nella sezione navigazione sinistra e fai clic sul __pulsante Nuovo Datastream__ nella sezione in alto a destra.

   ![AEP Crea Datastreams](../assets/aep-integration/AEP-Datastream-Create.png)

1. Denomina il flusso di dati utilizzando il __campo Nome__ obbligatorio. __Nel campo Schema__ evento, selezionare lo schema creato e fare clic su __Salva__.

   ![AEP Define Datastreams](../assets/aep-integration/AEP-Datastream-Define.png)

1. Aprire il flusso di dati creato e fare clic su __Aggiungi servizio__.

   ![Servizio aggiuntivo flussi di dati AEP](../assets/aep-integration/AEP-Datastream-Add-Service.png)

1. Sotto il __campo Servizio__ , selezionare l&#39;opzione __Adobe Experience Platform__ . Nel __campo Set di dati evento selezionare il nome del set di dati__ dal passaggio precedente e fare clic su __Salva__.

   ![AEP Datastreams Aggiungi dettagli servizio](../assets/aep-integration/AEP-Datastream-Add-Service-Define.png)

>[!TIP]
>
>Consulta la [Panoramica sullo stream di dati](https://experienceleague.adobe.com/docs/experience-platform/datastreams/overview.html) per ulteriori informazioni.

## Aggiungere valore dello stream di dati nella configurazione Commerce dell’AEM {#add-aep-values-to-aem}

Dopo aver completato la configurazione del Experience Platform di cui sopra, dovresti avere `datastreamId` nella barra sinistra dei dettagli del Datastream e `orgId` nell&#39;angolo in alto a destra dell&#39;immagine del profilo > informazioni sull&#39;account __> modale Informazioni__ utente.

![ID flussi di dati AEP](../assets/aep-integration/AEP-Datastream-ID.png)

1. Nel modulo del progetto AEM Commerce aggiornare il `config.js` file e in particolare le proprietà dell&#39;oggetto.`ui.frontend` `eventsCollector > aep`

1. Creare e distribuire il progetto AEM Commerce aggiornato


## Attivare `addToCart` eventi e verificare i dati raccolta {#event-trigger-verify}

I passaggi precedenti completano la configurazione di AEM Commerce e Experience Platform. Ora puoi attivare un’ `addToCart` Evento e verifica della raccolta dati tramite l’estensione Google Chrome _Ispettore Snowplow_ e set di dati __Metriche e grafici__ nell’interfaccia utente del prodotto.

Per attivare l&#39;evento, è possibile utilizzare AEM autore o il servizio pubblicare dalla configurazione locale. Per questo esempio, utilizza AEM Author effettuando l’accesso al tuo account.

1. Da Sites pagina, seleziona la __pagina My Demo StoreFront > noi > en__ e fai clic su __Modifica__ nella barra delle azioni in alto.

1. Dalla barra delle azioni superiore, fai clic su Visualizza come pubblicato __, quindi fai clic su__ una categoria preferita dall&#39;navigazione della vetrina.

1. Fai clic su uno dei scheda di prodotto preferiti nel __Pagina__ prodotto, quindi seleziona __colore, dimensione__ per attivare la __pulsante Aggiungi al carrello__ .


1. Apri __Ispettore Snowplow__ dal pannello delle estensioni del browser e seleziona __Experienci Platform Wed SDK__ nella barra a sinistra.


1. Torna a __Pagina prodotto__ e fai clic su __Aggiungi al carrello__ pulsante. In questo modo vengono inviati dati all&#39;Experience Platform. L&#39;estensione __Adobe Experience Platform Debugger__ mostra i dettagli dell&#39;evento.

   ![AEP Debugger Add-To-Cart Event-Data](../assets/aep-integration/AEP-Debugger-AddToCart-EventData.png)



1. Nell’interfaccia utente di Experienci Platform, passa a __Set di dati > Il mio archivio demoFront__, sotto il __Attività set di dati__ scheda. Se __Metriche e grafici__ è attivato, vengono visualizzate le statistiche dei dati evento.

   ![Experience Platform di statistiche dei dati del set di dati](../assets/aep-integration/AEP-Dataset-AddToCart-EventData.png)



## Dettagli implementazione {#implementation-details}

Il [connettore CIF Experience Platform](https://github.com/adobe/aem-core-cif-components/tree/master/extensions/experience-platform-connector) è basato sulla [connessione dati per Adobe Systems Commerce](https://commercemarketplace.adobe.com/magento-experience-platform-connector.html), che fa parte del [progetto PWA Studio](https://developer.adobe.com/commerce/pwa-studio/) .

Il progetto PWA Studio ti consente di creare vetrine Progressive Web Application (PWA) basate su Adobe Systems Commerce o Magento Open Source. Il progetto contiene anche un libreria di componenti chiamato [Peregrin](https://developer.adobe.com/commerce/pwa-studio/api/peregrine/) per aggiungere logica ai componenti visivi. Il [libreria](https://developer.adobe.com/commerce/pwa-studio/api/peregrine/) Peregrin fornisce anche i ganci React personalizzati utilizzati dal [connettore](https://github.com/adobe/aem-core-cif-components/tree/master/extensions/experience-platform-connector) CIF Experience Platform per integrare con Experience Platform senza soluzione di continuità.


## Eventi supportati {#supported-events}

Al momento, sono supportati i seguenti eventi:

__Eventi Experience XDM:__

1. Aggiungi al carrello (AEM)
1. Visualizza Pagina (AEM)
1. Visualizza prodotto (AEM)
1. Richiesta di ricerca inviata (AEM)
1. Risposta di ricerca ricevuta (AEM)

Quando [Componenti peregrini](https://developer.adobe.com/commerce/pwa-studio/guides/packages/peregrine/) sono riutilizzati nel progetto Commerce dell’AEM:

__Eventi Experience XDM:__

1. Rimuovi dal carrello
1. Apri carrello
1. Visualizza carrello
1. Acquisto immediato
1. Avvia estrazione
1. Tutte le applicazioni checkout

__Eventi XDM del profilo:__

1. Accedi
1. Crea account
1. Modifica account


## Risorse aggiuntive {#additional-resources}

Per ulteriori informazioni, consulta le risorse seguenti:

- [PWA Studi](https://developer.adobe.com/commerce/pwa-studio/)
- [[!DNL Data Connection] Panoramica](https://experienceleague.adobe.com/docs/commerce-merchant-services/data-connection/overview.html)
- [[!DNL Data Connection] Eventi](https://experienceleague.adobe.com/docs/commerce-merchant-services/data-connection/event-forwarding/events.html)
- [Adobe Experience Platform panoramica](https://experienceleague.adobe.com/docs/experience-platform/landing/home.html)
