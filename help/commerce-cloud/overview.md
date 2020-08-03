---
title: Introduzione a AEM Commerce come Cloud Service
description: Novità in AEM Commerce come Cloud Service.
translation-type: tm+mt
source-git-commit: c5694cf8651cf8ba5331c730fa1b1180310dd35a
workflow-type: tm+mt
source-wordcount: '1331'
ht-degree: 1%

---


# Introduzione AEM Commerce come Cloud Service {#commerce-intro}

 Experience Manager Commerce come Cloud Service è costituito da Commerce Integration Framework (CIF), che è  Adobe modello raccomandato per integrare ed estendere i servizi commerciali da Magenti e altre soluzioni di commercio di terzi con il Experience Cloud . Questo consente  clienti di Adobe di offrire un&#39;esperienza di acquisto omnicanale straordinaria e personalizzata basata su tecnologie all&#39;avanguardia.

Commerce Integration Framework è un modulo aggiuntivo per  Experience Manager come Cloud Service e fornisce un set di strumenti di authoring, componenti e un negozio di riferimento per accelerare lo sviluppo di integrazioni tra  Experience Manager come Cloud Service e soluzioni di commercio.

## CIF Benefits {#cif-benefits}

I principali vantaggi sono:

* L&#39;integrazione è un livello di astrazione per standardizzare e incapsulare le integrazioni con più sistemi.

* CIF supporta esperienze headless/omnichannel:

   * Applicazioni a pagina singola e applicazioni a più pagine
   * Endpoint GraphQL

* CIF fornisce un livello di processo e logica aziendale basato su microservizi senza server per la personalizzazione e l&#39;estensione dei servizi commerciali.

* CIF offre integrazioni pronte all’uso con soluzioni di Adobe  come AEM e Magenti

## CIF Elements {#cif-elements}

![CIF Elements](/help/commerce-cloud/assets/cif-overview1.jpg)


### CIF add-On per gli strumenti di authoring {#add-on-authoring-tools}

Il componente aggiuntivo CIF consente di accedere a strumenti di authoring per il commercio come console prodotto, Pickers prodotto e categoria o alla ricerca di prodotti per consentire agli autori di creare esperienze avanzate con i contenuti di marketing e di e-commerce. Il componente aggiuntivo gestisce anche la connessione di back-end al Magento (o sistema di commercio alternativo) tramite GraphQL. Una volta effettuato il provisioning, il componente aggiuntivo viene distribuito automaticamente su AEM come ambienti di Cloud Service.

### Componenti di base CIF AEM {#aem-cif-core}

I componenti AEM CIF di base sono componenti lato server e lato client sottoposti a rendering con il supporto di GraphQL del Magento. Sono utilizzati per creare un negozio di commercio statico, cacheable e intuitivo basato su tecnologie AEM.

Sono disponibili componenti di base, comuni tra le implementazioni commerciali come Dettagli prodotto, Elenco prodotti, Navigazione, Ricerca, ecc. Possono essere utilizzati così come sono o possono essere estesi.

I componenti [di base](https://github.com/adobe/aem-core-cif-components) AEM CIF funzionano come i componenti [di base](https://github.com/adobe/aem-core-wcm-components) AEM Sites, ma sono dedicati a casi d’uso specifici del commercio.

I vantaggi principali di questi componenti sono:

* Sono facili da usare nei vostri progetti.
* Possono essere utilizzati così come sono o con modifiche minime.
* Forniscono le procedure ottimali per la connessione con il Magento tramite API GraphQL o REST

Componenti come Product Teaser e Product Carousel sono forniti per consentire agli AEM Author di creare pagine Experience in AEM, combinando contenuti di marketing e di e-commerce. Questi componenti possono essere facilmente trascinati e inseriti in una pagina di contenuto creata in AEM e collegati a prodotti o categorie specifici utilizzando gli strumenti di authoring CIF, come ad esempio il Selettore prodotto o categoria nel Cloud Service.

Tutti i componenti sono open-source su [GitHub](https://github.com/adobe/aem-core-cif-components). Questo mostra la completa trasparenza sulle modifiche apportate in futuro e consente di ottenere la versione più recente molto facilmente. È inoltre possibile includere richieste di pull per miglioramenti e correzioni di bug.

### AEM Venia Storefront {#aem-venia-storefront}

Il [AEM Venia Storefront](https://github.com/adobe/aem-cif-guides-venia) è un moderno negozio di riferimento pronto per la produzione che presenta un semplice percorso commerciale B2C. Può essere utilizzato per avviare progetti commerciali e accelerare i progetti utilizzando AEM, CIF e Magento. Mostra le procedure ottimali per l’integrazione di AEM e Magenti e mostra come utilizzare i componenti [core CIF](https://github.com/adobe/aem-core-cif-components) AEM componenti [e i componenti](https://github.com/adobe/aem-core-wcm-components) coreAEM Sites e supporta  endpoint Commerce GraphQL di Adobe. Offre inoltre un sito di riferimento per dimostrarne l&#39;integrazione tra AEM e Magento.

Il AEM Venia Storefront è un&#39;applicazione a pagina mista in cui AEM possiede il vetro e Magento potenzia il back-end commerciale in modo senza testa. Sia il rendering lato server che il rendering lato client vengono utilizzati nello storefront. Il rendering sul lato server viene utilizzato per fornire contenuto statico e il rendering sul lato client viene utilizzato per distribuire contenuto dinamico.

Le pagine di prodotto e catalogo sono relativamente statiche e vengono sottoposte a rendering sul lato server utilizzando i componenti core CIF AEM come Dettagli prodotto e Elenco prodotti su modelli generici creati in AEM. Questi componenti ottengono i dati dagli Magenti tramite le API GraphQL.
Queste pagine vengono create in modo dinamico, sottoposte a rendering sul server, memorizzate nella cache del dispatcher AEM e quindi distribuite al browser.
Per gli attributi più dinamici, ad esempio magazzino o prezzo, vengono invece utilizzati i componenti lato client. I componenti lato client o i componenti Web recuperano i dati direttamente dall&#39;Magento tramite le API GraphQL e il contenuto viene quindi rappresentato nel browser.

#### Estrai {#checkout}

Questo storefront di riferimento utilizza il componente Carrello lato client che esegue il rendering del carrello e del modulo di checkout per dimostrare un modello di integrazione dell&#39;esperienza completa, che consente di distribuire esperienze di e-commerce con Magento in esecuzione completamente senza precedenti e AEM proprietario del vetro. Si consiglia di utilizzare i metodi di pagamento astratti forniti. Questo mette il client browser in comunicazione diretta con il provider del gateway di pagamento in modo che né  Adobe né cloud di Magento detengano o trasmettano dati sensibili PCI.

#### Gestione account {#account-management}

La gestione dell&#39;account viene gestita dal Magento e il negozio di riferimento utilizza componenti basati su React lato client per consentire AEM eseguire il rendering dell&#39;esperienza per le seguenti funzionalità: Crea account, Accedi e Password dimenticata.

Il progetto AEM Venia Storefront è open source e per maggiori dettagli, fare riferimento a [AEM Venia Storefront](https://github.com/adobe/aem-cif-guides-venia).

### AEM Project Archetype {#aem-project-archtype}

The [AEM Project Archetype](https://docs.adobe.com/content/help/it-IT/experience-manager-core-components/using/developing/archetype/overview.html) can be used to create a minimal, best-practices-based Adobe Experience Manager project as a starting point for your own AEM projects. Facoltativamente, [AEM componenti](https://github.com/adobe/aem-core-cif-components) di base CIF possono essere inclusi in un progetto appena generato.

### CIF livello di estensione {#cif-extension}

Lo strato di estensione CIF è uno strato intermedio per ospitare complesse logiche aziendali. Viene eseguito sulla piattaforma Adobe I/O Runtime,  piattaforma senza server  Adobe. Consente di estendere le chiamate di servizio end-to-end inserendo logica di business e processo a livello di microservizio. La logica aziendale potrebbe essere ad esempio l&#39;utilizzo della posizione e del canale per determinare una strategia di inventario. La logica del processo sarebbe ad esempio quella di recuperare informazioni personalizzate.

### CIF livello di integrazione {#cif-integration-layer}

Il livello di integrazione CIF viene utilizzato per standardizzare le integrazioni con altre soluzioni di commercio. Viene eseguito sulla piattaforma Adobe I/O Runtime,  piattaforma senza server  Adobe e consente integrazioni a livello di microservizi mappando le API di terze parti rispetto alle API Adobe Commerce di . Per aiutarti a iniziare a creare integrazioni di terze parti con AEM, abbiamo creato un&#39;implementazione [di](https://github.com/adobe/commerce-cif-graphql-integration-reference) riferimento per dimostrare come un backend di commercio non di Magento possa essere integrato tramite  API Commerce di Adobe (API Magento GraphQL).

## Modelli di integrazione AEM Commerce {#aem-commerce-integration}

Alcuni dei modelli di integrazione di Commerce AEM comunemente implementati sono mostrati di seguito.

![Modelli di integrazione CIF AEM](/help/commerce-cloud/assets/aem-cif-integration-patterns-updated.JPG)


### Pattern di integrazione 1 {#integration-pattern-one}

Questo è il nostro modello di integrazione consigliato in cui AEM possiede l&#39;intero vetro e integra i servizi di commercio tramite  API Commerce GraphQL di Adobe. Questo pattern consente di AEM la massima flessibilità per adattare i progetti di siti multimediali su diversi dispositivi. Questo modello di integrazione è supportato da CIF come soluzione standard.


### Pattern di integrazione 2 {#integration-pattern-two}

Questo pattern rappresenta un modo senza precedenti di distribuire contenuti e attività commerciali. La consegna è completamente lato client. In questo pattern il contenuto viene distribuito tramite API e i dati HTML e Commerce tramite GraphQL. Questo pattern non è attualmente supportato da CIF out-of-the-box.


### Pattern di integrazione 3 {#integration-pattern-three}

In questo pattern, il Magento possiede il vetro e incorpora AEM contenuto creato. Il contenuto creato AEM può essere distribuito tramite frammenti esperienza o frammenti di contenuto. Questo pattern di integrazione richiederà un lavoro specifico per il progetto e non potrà essere implementato out-of-the-box con CIF.


### Pattern di integrazione 4 {#integration-pattern-four}

Si tratta di un pattern di integrazione comune in cui il livello di vetro o presentazione è diviso tra AEM e una soluzione Commerce. Solitamente, la soluzione Commerce distribuisce le pagine non di marketing come il checkout e il mio account e AEM fornisce le pagine di marketing e l&#39;esperienza di catalogo storefront. In questo pattern, è necessario assicurarsi che i carrelli e le sessioni utente siano gestiti correttamente tra i due sistemi per evitare un&#39;esperienza utente slegata. Ad Magento, memorizza il carrello e la sessione utente in un cookie, che può essere condiviso tra AEM e Magento. Questo pattern richiede un lavoro specifico per il progetto e non può essere implementato out-of-the-box con CIF.
