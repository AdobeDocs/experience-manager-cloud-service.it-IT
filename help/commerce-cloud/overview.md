---
title: Introduzione a AEM Commerce as a Cloud Service
description: ' Experience Manager Commerce as a Cloud Service è costituito da Commerce Integration Framework (CIF), il modello consigliato di Adobe per integrare ed estendere i servizi commerce da Magento e altre soluzioni di terze parti con Experience Cloud. '
thumbnail: introducing-aem-commerce.jpg
translation-type: tm+mt
source-git-commit: 72d98c21a3c02b98bd2474843b36f499e8d75a03
workflow-type: tm+mt
source-wordcount: '1357'
ht-degree: 100%

---


# Introduzione a AEM Commerce as a Cloud Service {#commerce-intro}

 Experience Manager Commerce as a Cloud Service è costituito da Commerce Integration Framework (CIF), il modello consigliato di Adobe per integrare ed estendere i servizi commerce da Magento e altre soluzioni di terze parti con Experience Cloud. Consente ai clienti Adobe di offrire un’esperienza di acquisto omnicanale straordinaria e personalizzata, basata su tecnologie all’avanguardia.

Commerce Integration Framework è un modulo aggiuntivo per Experience Manager as a Cloud Service e fornisce un set di strumenti per la creazione di contenuti, componenti e una vetrina per accelerare lo sviluppo di integrazioni tra Experience Manager as a Cloud Service e soluzioni commerce.

## Vantaggi di CIF {#cif-benefits}

I principali vantaggi sono i seguenti:

* L’integrazione è un livello di astrazione per standardizzare e incapsulare le integrazioni con più sistemi.

* CIF supporta esperienze headless/omnicanale:

   * Applicazioni a pagina singola e applicazioni a più pagine
   * Endpoint GraphQL

* CIF fornisce un livello di processo e logica di business senza server basato su microservizi per personalizzare ed estendere i servizi commerce.

* CIF offre integrazioni pronte all’uso con soluzioni Adobe, come AEM e Magento

## Elementi di CIF {#cif-elements}

![Elementi di CIF](/help/commerce-cloud/assets/cif-overview1.jpg)


### Componente aggiuntivo CIF per strumenti di creazione di contenuti {#add-on-authoring-tools}

Il componente aggiuntivo CIF consente di accedere a strumenti per la creazione di contenuti per l’e-commerce, come console dei prodotti, selettori di prodotti e categorie o ricerca di prodotti, per consentire agli autori di creare esperienze avanzate con contenuti di marketing e di e-commerce. Il componente aggiuntivo gestisce anche la connessione back-end a Magento (o altro sistema commerce) tramite GraphQL. Una volta effettuato il provisioning, il componente aggiuntivo viene implementato automaticamente negli ambienti di AEM as a Cloud Service.

### Componenti core CIF di AEM {#aem-cif-core}

I componenti core CIF di AEM sono componenti con rendering lato server e lato client che supportano GraphQL di Magento. Sono utilizzati per creare una vetrina di e-commerciale statica, memorizzabile nella cache, compatibile con SEO (Search Engine Optimization) e basata su tecnologie AEM.

Sono forniti componenti di base comuni a tutte le implementazioni commerce, come Dettagli prodotto, Elenco prodotti, Navigazione, Ricerca, ecc. Possono essere utilizzati così come sono o possono essere estesi.

I [componenti core CIF di AEM](https://github.com/adobe/aem-core-cif-components) funzionano come i [componenti core di AEM Sites](https://github.com/adobe/aem-core-wcm-components), ma sono dedicati a casi d’uso specifici per l’e-commerce.

Tali componenti offrono i seguenti vantaggi:

* Sono facili da usare nei progetti.
* Possono essere utilizzati così come sono o con modifiche minime.
* Forniscono best practice per la connessione con Magento tramite API GraphQL o REST

Componenti come Product Teaser e Product Carousel sono forniti per consentire agli autori di AEM di creare pagine di esperienze in AEM, combinando contenuti di marketing e di e-commerce. Questi componenti possono essere facilmente trascinati e inseriti in una pagina di contenuto creata in AEM e collegati a prodotti o categorie specifici utilizzando gli strumenti CIF per la creazione di contenuti, come ad esempio il Selettore prodotto o categoria in Cloud Service.

Tutti i componenti sono open source su [GitHub](https://github.com/adobe/aem-core-cif-components). Questo assicura la completa trasparenza sulle modifiche future e consente di ottenere molto facilmente la versione più recente. È inoltre possibile presentare richieste pull per miglioramenti e correzioni di bug da incorporare.

### AEM Venia Storefront {#aem-venia-storefront}

[AEM Venia Storefront](https://github.com/adobe/aem-cif-guides-venia) è una vetrina di riferimento pronta per la produzione che presenta un semplice percorso di e-commerce B2C. Può essere utilizzata per avviare progetti di e-commerce e accelerare i progetti utilizzando AEM, CIF e Magento. Questo progetto rappresenta una dimostrazione pratica delle best practice per l’integrazione di AEM e Magento e di come utilizzare i [componenti core CIF di AEM](https://github.com/adobe/aem-core-cif-components) e i [componenti core di AEM Sites](https://github.com/adobe/aem-core-wcm-components). Inoltre supporta gli endpoint GraphQL di Adobe Commerce. Offre anche un sito di riferimento per dimostrare l’integrazione tra AEM e Magento per casi d’uso pre-vendita.

AEM Venia Storefront è un’applicazione a pagine miste in cui AEM è responsabile dell’esperienza di marketing e Magento potenzia il back-end in modalità headless. Sia il rendering lato server che il rendering lato client vengono utilizzati nella vetrina. Il rendering lato server viene utilizzato per fornire contenuti statici; con il rendering lato client vengono invece forniti i contenuti dinamici.

Le pagine di prodotto e catalogo sono relativamente statiche e vengono sottoposte a rendering sul lato server utilizzando i componenti core CIF di AEM come Dettagli prodotto ed Elenco prodotti su modelli generici creati in AEM. Questi componenti ottengono i dati da Magento tramite API GraphQL.
Le pagine vengono create in modo dinamico, sottoposte a rendering sul server, memorizzate nella cache di AEM Dispatcher e quindi distribuite al browser.
Per gli attributi più dinamici, ad esempio inventario o prezzo, vengono invece utilizzati i componenti lato client. I componenti lato client o i componenti Web recuperano i dati direttamente da Magento tramite API GraphQL e il contenuto viene quindi rappresentato nel browser.

#### Pagamento {#checkout}

Questa vetrina utilizza il componente Carrello lato client che genera il carrello e il modulo di pagamento, per dimostrare un pattern di integrazione dell’esperienza completa: le esperienze e-commerce vengono distribuite tramite Magento che opera in modalità completamente headless, mentre AEM è responsabile dell’esperienza di e-commerce. Si consiglia di utilizzare i metodi di pagamento astratti forniti. In tal modo il client browser comunica direttamente con il provider del gateway dei pagamenti e i dati sensibili PCI non vengono trasmessi né memorizzati nel cloud di Adobe né di Magento.

#### Gestione account {#account-management}

La gestione account è effettuata da Magento e la vetrina utilizza componenti basati su React lato client per consentire ad AEM di eseguire il rendering dell’esperienza per le seguenti funzionalità: Crea account, Accedi e Password dimenticata.

Il progetto AEM Venia Storefront è open source; per maggiori dettagli consulta [AEM Venia Storefront](https://github.com/adobe/aem-cif-guides-venia).

### AEM Project Archetype {#aem-project-archtype}

[AEM Project Archetype](https://docs.adobe.com/content/help/it-IT/experience-manager-core-components/using/developing/archetype/overview.html) può essere usato per creare un progetto Adobe Experience Manager minimale basato su best practice come punto di partenza per i tuoi progetti AEM. Facoltativamente, i [componenti core CIF di AEM](https://github.com/adobe/aem-core-cif-components) possono essere inclusi in un progetto appena generato.

### Livello di estensione CIF {#cif-extension}

Il livello di estensione CIF è un livello intermedio per ospitare una logica di business complessa. Viene eseguito su Adobe I/O Runtime, una piattaforma senza server di Adobe. Consente di estendere le chiamate di servizio end-to-end inserendo logica di business e di processo a livello di microservizio. Un esempio di logica di business è l’utilizzo della posizione e del canale per determinare una strategia di inventario. Un esempio di logica di processo è il recupero di informazioni personalizzate.

### Livello di integrazione CIF {#cif-integration-layer}

Il livello di integrazione CIF viene utilizzato per standardizzare le integrazioni con altre soluzioni e-commerce. Viene eseguito su Adobe I/O Runtime, una piattaforma senza server di Adobe, e consente integrazioni a livello di microservizi mappando le API di terze parti rispetto alle API Commerce di Adobe. Per aiutarti a iniziare a creare integrazioni di terze parti con AEM, abbiamo creato un’[implementazione di riferimento](https://github.com/adobe/commerce-cif-graphql-integration-reference) per dimostrare come un back-end per e-commerce non Magento possa essere integrato tramite le API Commerce di Adobe (API Magento GraphQL).

## Modelli di integrazione con AEM Commerce {#aem-commerce-integration}

Alcuni dei modelli di integrazione con AEM Commerce comunemente implementati sono mostrati di seguito.

![Modelli di integrazione CIF per AEM](/help/commerce-cloud/assets/aem-cif-integration-patterns-updated.JPG)


### Modello di integrazione 1 {#integration-pattern-one}

Si tratta del modello di integrazione consigliato, in cui AEM è interamente responsabile dell’esperienza di e-commerce e integra i servizi commerce tramite API Commerce GraphQL di Adobe. Questo modello offre tutta la flessibilità di AEM per adattare i progetti di siti rich media per dispositivi diversi. Questo modello di integrazione è supportato da CIF come soluzione standard.


### Modello di integrazione 2 {#integration-pattern-two}

Questo modello rappresenta una modalità headless per la distribuzione di contenuti e attività commerce. La distribuzione è completamente lato client. In questo modello il contenuto viene distribuito tramite API e i dati HTML e Commerce tramite GraphQL. Questo modello non è attualmente supportato da CIF come standard.


### Modello di integrazione 3 {#integration-pattern-three}

In questo modello, Magento è responsabile dell’esperienza di e-commerce e integra i contenuti creati con AEM. I contenuti creati con AEM possono essere distribuiti tramite Frammenti di esperienza o Frammenti di contenuto. Questo modello di integrazione richiederà un lavoro specifico per il progetto e non può essere implementato come standard con CIF.


### Modello di integrazione 4 {#integration-pattern-four}

Si tratta di un pattern di integrazione comune in cui la presentazione dell’esperienza di e-commerce è divisa tra AEM e una soluzione Commerce. Solitamente, la soluzione Commerce distribuisce le pagine non di marketing (come quella per il pagamento e “Il mio account”), mentre AEM fornisce le pagine di marketing e l’esperienza del catalogo della vetrina. In questo modello, è necessario assicurarsi che i carrelli e le sessioni utente siano gestiti correttamente tra i due sistemi per evitare un’esperienza utente slegata. Ad esempio, Magento memorizza il carrello e la sessione utente in un cookie, che può essere condiviso tra AEM e Magento. Questo modello richiede un lavoro specifico per il progetto e non può essere implementato come standard con CIF.
