---
title: Best practice per la configurazione e l’utilizzo di AEM GraphQL con frammenti di contenuto
description: Scopri le best practice consigliate per la configurazione e l’utilizzo di AEM GraphQL con frammenti di contenuto.
source-git-commit: 9a544fb9d2494862efdb2263f3b9b61214c4b8b9
workflow-type: tm+mt
source-wordcount: '737'
ht-degree: 34%

---


# Best practice per la configurazione e l’utilizzo di AEM GraphQL con frammenti di contenuto{#best-practices-setup-use-aem-graphql-content-fragments}

Queste linee guida riepilogano le best practice consigliate per l’impostazione, la configurazione e l’utilizzo di AEM con GraphQL e Frammenti di contenuto.

## Guida introduttiva {#getting-started}

Per aiutarti a imparare a usare al meglio:

* [Cosa si intende con Headless?](/help/headless/what-is-headless.md)
* Panoramica dei diversi contesti del AEM [Architettura](/help/headless/deployment/architecture.md)

## Configurazione {#setup}

Per configurare in modo sicuro il GraphQL per l’AEM da utilizzare con i frammenti di contenuto e le app, è necessario configurare vari componenti.

### Creazione di endpoint GraphQL (inclusa la sicurezza) {#graphql-endpoint-creation}

L’endpoint è il percorso utilizzato per accedere a GraphQL per AEM. Questi endpoint devono essere creati e pubblicati in modo da essere accessibili in modo sicuro.

#### Dettagli {#details-graphql-endpoint-creation}

[Gestire gli endpoint GraphQL in AEM](/help/headless/graphql-api/graphql-endpoint.md)

#### Ambienti {#environments-graphql-endpoint-creation}

Gli endpoint devono essere configurati in:

* Autore
* Anteprima
* Pubblicazione

Per:

* Ambiente di sviluppo
* Test
* Produzione

### Memorizzazione in cache di AEM Dispatcher {#dispatcher-caching}

>[!NOTE]
>Se il caching in Dispatcher è abilitato, il [Configurazione CORS](#cors-setup) non è necessario, quindi può essere ignorato.

La memorizzazione nella cache delle query persistenti non è abilitata per impostazione predefinita in Dispatcher. L’abilitazione predefinita non è possibile perché i clienti che utilizzano CORS (Cross-Origin Resource Sharing) con più origini devono rivedere, e possibilmente aggiornare, la propria configurazione di Dispatcher.

#### Dettagli {#details-dispatcher-caching}

[Query persistenti GraphQL: abilitazione della memorizzazione nella cache in Dispatcher](/help/headless/deployment/dispatcher-caching.md)

#### Ambienti {#environments-dispatcher-caching}

Dispatcher è in genere configurato per:

* Pubblicazione: produzione

### Configurazione CORS {#cors-setup}

>[!NOTE]
>Se il caching in [Dispatcher AEM](#dispatcher-caching) è attivato, la configurazione CORS non è necessaria e quindi questa sezione può essere ignorata.

Per accedere all’endpoint GraphQL, è necessario configurare un criterio CORS e aggiungerlo a un progetto AEM implementato in AEM tramite Cloud Manager. Questo viene fatto aggiungendo un file di configurazione OSGi CORS appropriato per gli endpoint desiderati. 

#### Dettagli {#details-cors-setup}

[Configurazione di Cross-Origin Resource Sharing (CORS)](/help/headless/deployment/cross-origin-resource-sharing.md)

#### Ambienti {#environments-cors-setup}

CORS è in genere configurato per:

* Pubblicazione: produzione

### Autenticazione {#authentication}

Un caso d’uso principale per API GraphQL di Adobe Experience Manager as a Cloud Service (AEM) relativo alla distribuzione di frammenti di contenuto accetta query remote da applicazioni o servizi di terzi. Queste query remote possono richiedere l’accesso a API autenticate, per garantire la distribuzione di contenuti headless.

#### Dettagli {#details-authentication}

[Autenticazione per query GraphQL AEM remote su frammenti di contenuto](/help/headless/security/authentication.md)

#### Ambienti {#environments-authentication}

L’autenticazione è in genere configurata per:

* Anteprima
* Pubblicazione

Per:

* Ambiente di sviluppo
* Test
* Produzione

### Autorizzazioni {#permissions}

Con un’implementazione headless, è necessario affrontare diverse aree di sicurezza e autorizzazioni. Le autorizzazioni e gli utenti tipo possono essere considerati in generale in base all’ambiente AEM **Autore** o **Pubblica**. Ogni ambiente contiene utenti tipo diversi e con esigenze diverse.

#### Dettagli {#details-permissions}

[Considerazioni sulle autorizzazioni per contenuti headless](/help/headless/security/permissions.md)

#### Ambienti {#environments-permissions}

Le autorizzazioni sono generalmente configurate per:

* Autore
* Anteprima
* Pubblicazione

Per:

* Ambiente di sviluppo
* Test
* Produzione

### Utilizzare una rete per la distribuzione dei contenuti (CDN) {#cdn}

Le query GraphQL e le relative risposte JSON possono essere memorizzate nella cache se impostate come `GET` richieste quando si utilizza una rete CDN. Al contrario, le richieste non memorizzate nella cache possono essere molto (risorse) costose e lente da elaborare, con il potenziale di ulteriori effetti negativi sulle risorse dell’origine.

#### Dettagli {#details-cdn}

[CDN in AEM as a Cloud Service](/help/implementing/dispatcher/cdn.md)

#### Ambienti {#environments-cdn}

Una rete CDN è in genere configurata per:

* Pubblicazione: produzione

### Configurare e creare frammenti di contenuto {#cconfigure-create-content-fragments}

AEM GraphQL viene utilizzato per recuperare informazioni dai frammenti di contenuto. Prima di poter creare il contenuto, è necessario configurarlo, quindi definire una struttura e una posizione.

#### Dettagli {#details-content-fragments}

* [Creare una configurazione](/help/headless/setup/create-configuration.md)
* [Creare un modello per frammenti di contenuto](/help/headless/setup/create-content-model.md)
* [Creare una cartella di risorse](/help/headless/setup/create-assets-folder.md)
* [Creare e modificare i frammenti di contenuto](/help/headless/setup/create-content-fragment.md)

#### Ambienti {#eenvironments-content-fragments}

I frammenti di contenuto sono definiti, creati, testati, pubblicati e accessibili su:

* Autore
* Anteprima
* Pubblicazione

Per:

* Ambiente di sviluppo
* Test
* Produzione

## Utilizzo di AEM GraphQL {#use-aem-graphql}

### Ottimizzare le query GraphQL {#optimize-graphql-queries}

Queste linee guida servono a prevenire problemi di prestazioni con le query GraphQL.

#### Dettagli {#details-optimize-graphql-queries}

[Ottimizzazione delle query GraphQL](/help/headless/graphql-api/graphql-optimization.md)

>[!NOTE]
>
>Le linee guida per l’ottimizzazione riguardano la configurazione della cache, già trattata in [Configurazione](#setup).

### Accedere a GraphQL dalle app {#access-graphql-from-your-apps}

I CMS headless AEM offrono agli sviluppatori la libertà di creare e distribuire esperienze eccezionali utilizzando i linguaggi, i framework e gli strumenti che già conoscono.

#### Dettagli {#details-your-apps}

* [Installare e utilizzare l’SDK dell’AEM per lo sviluppo](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/how-to/aem-headless-sdk.html?lang=it)
* [Risorse per sviluppatori AEM headless](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html?lang=it)
* Esempi, tra cui [React](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/how-to/example-apps/react-app.html), [Next.js](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/how-to/example-apps/next-js.html), [Node.js](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/how-to/example-apps/server-to-server-app.html), tra gli altri

#### Ambienti {#environments-your-apps}

Le app vengono generalmente sviluppate, testate e utilizzate per:

* Anteprima
* Pubblicazione

Per:

* Ambiente di sviluppo
* Test
* Produzione

### Ulteriori risorse

Per ulteriori dettagli sul GraphQL dell’AEM e sui frammenti di contenuto consulta:

* [API GraphQL AEM per l’utilizzo con Frammenti di contenuto](/help/headless/graphql-api/content-fragments.md)
* [Utilizzo dell’IDE GraphiQL](/help/headless/graphql-api/graphiql-ide.md)
* [Risorse per sviluppatori AEM headless](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html?lang=it)
