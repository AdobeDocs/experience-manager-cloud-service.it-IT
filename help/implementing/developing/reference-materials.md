---
title: Materiali di riferimento API
description: AEM dispone di API estese e potenti che puoi sfruttare per il tuo progetto di esperienza digitale.
exl-id: d4ef3040-5a0a-4149-9e99-09eda9605038
source-git-commit: 08559417c8047c592f2db54321afe68836b75bd1
workflow-type: tm+mt
source-wordcount: '664'
ht-degree: 4%

---

# Materiali di riferimento API {#api-reference-materials}

Adobe Experience Manager (AEM) fornisce molte API per lo sviluppo di applicazioni e l’estensione di AEM. AEM si basa su una serie di tecnologie open-source, che possono anche essere sfruttate.

## API di base AEM {#core-aem-apis}

Le seguenti API sono di base per AEM.

| API | Descrizione |
|---|---|
| [Adobe Experience Manager as a Cloud Service](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/index.html) | astrazioni di prodotto come pagine, risorse, flussi di lavoro, ecc. |
| [Interfaccia Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/index.html#) | Lo stack Web aperto di Adobe, che fornisce vari componenti essenziali (i materiali Granite 6.5 si applicano ad AEMaaCS) |
| [Interfaccia Coral](https://opensource.adobe.com/coral-spectrum/documentation/) | Stile visivo di Adobe per le interfacce utente cloud, progettato per fornire coerenza nell’esperienza utente |

<!---
|Editor core JavaScript API reference|Provides all the base objects and concepts to support authoring of content resources|
--->

## Framework aggiuntivi {#additional-apis}

AEM si basa su una serie di API open-source aggiuntive.

| API | Descrizione |
|---|---|
| [Sling Apache](https://sling.apache.org/apidocs/sling11/) | Framework web che utilizza un Java Content Repository (JCR) per archiviare e gestire il contenuto |
| [Apache Jackrabbit Oak](http://jackrabbit.apache.org/oak/docs/oak_api/overview.html) | Implementazione di un archivio di contenuti Java (JCR) scalabile e gerarchico ad alte prestazioni per l&#39;utilizzo come base dei moderni siti web di livello mondiale |
| [Archivio dei contenuti Java](https://www.adobe.io/experience-manager/reference-materials/spec/javax.jcr/javadocs/jcr-2.0/index.html) | Specifiche per JCR versione 2.0 |
| [Apache Felix](https://felix.apache.org) | Implementazione del framework e della piattaforma di servizi dell&#39;iniziativa Open Services Gateway (OSGi) |

## Linee guida sulle preferenze API {#guidelines}

AEM è basato sui seguenti quattro set principali di API Java in ordine decrescente di preferenza.

| Priorità | API | Descrizione |
|---|---|---|
| 1 | [Adobe Experience Manager as a Cloud Service](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/index.html) | astrazioni di prodotto come pagine, risorse, flussi di lavoro, ecc. |
| 2 | [Sling Apache](https://sling.apache.org/apidocs/sling11/) | astrazioni REST e basate su risorse come risorse, mappe dei valori e richieste HTTP. |
| 3 | [Apache Jackrabbit Oak](http://jackrabbit.apache.org/oak/docs/oak_api/overview.html) | astrazioni di dati e contenuti quali nodo, proprietà e sessioni. |
| 4 | [Apache Felix](https://felix.apache.org/) | astrazioni del contenitore dell&#39;applicazione OSGi quali servizi e componenti (OSGi). |

Se un’API è fornita da AEM, preferiscila rispetto a Sling, JCR e OSGi. Se AEM non fornisce un’API, preferisci Sling rispetto a JCR e OSGi.

>[!TIP]
>
>Per informazioni dettagliate su queste linee guida, consulta il documento [Comprendere le best practice per le API Java.](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/understand-java-api-best-practices.html)

## Servizi di distribuzione AEM e gestione dei contenuti e API {#delivery-apis}

AEM offre componenti personalizzabili e opzioni di distribuzione dei contenuti.

| Funzione obsoleta | Descrizione |
|---|---|
| [Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=it) | Componenti WCM (Web Content Management) standardizzati per AEM per velocizzare i tempi di sviluppo e ridurre i costi di manutenzione dei siti web |
| [Esportatore JSON](/help/implementing/developing/components/json-exporter.md) | Consegnare il contenuto di qualsiasi pagina AEM in formato modello dati JSON |
| [Abilitazione dell’esportazione JSON per un componente](/help/implementing/developing/components/enabling-json-exporter.md) | Generare l’esportazione JSON del contenuto di componenti in base a un framework di modelli |
| [API di Assets](/help/assets/mac-api-assets.md) | Consente operazioni di creazione-lettura-aggiornamento-eliminazione (CRUD) sulle risorse, tra cui file binari, metadati, rappresentazioni e commenti. Consulta API HTTP AEM Assets |
| [API HTTP per frammenti di contenuto](/help/assets/content-fragments/assets-api-content-fragments.md) | Accedere ai contenuti dei frammenti di contenuto direttamente tramite l’API HTTP tramite operazioni CRUD |
| [API GraphQL per frammenti di contenuto](/help/assets/content-fragments/graphql-api-content-fragments.md) | Consentire la distribuzione efficiente di frammenti di contenuto ai client JavaScript in implementazioni CMS headless |
| [API HTTP per le risorse di frammenti di contenuto](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/admin/mac-api-assets.html) | Formato esatto delle richieste di risorse HTTP supportate |

## API specifiche per SPA {#spa-apis}

AEM framework SDK per l’editor di applicazioni a pagina singola (SPA) fornisce riferimenti API JavaScript specifici.

| API | Descrizione |
|---|---|
| [Mappatura dei componenti](https://www.npmjs.com/package/@adobe/aem-spa-component-mapping) | Consente all’applicazione a pagina singola di mappare i componenti front-end sui tipi di risorse Adobe Experience Manager (componenti AEM) |
| [Page Model Manager](https://www.npmjs.com/package/@adobe/aem-spa-page-model-manager) | Un interprete tra l’editor di Adobe Experience Manager e l’editor di applicazioni a pagina singola di Adobe Experience Manager (SPA) |
| [Reazione di componenti modificabili](https://www.npmjs.com/package/@adobe/aem-react-editable-components) | Fornisce i componenti React e il livello di integrazione per iniziare a utilizzare l’Editor siti di Adobe Experience Manager |
| [Angular - Componenti modificabili](https://www.npmjs.com/package/@adobe/aem-angular-editable-components) | Fornisce i componenti di Angular e il livello di integrazione per iniziare a utilizzare Adobe Experience Manager Site Editor |

>[!TIP]
>
>Per ulteriori informazioni sulle applicazioni a pagina singola, consulta [SPA Introduzione e Procedura dettagliata](/help/implementing/developing/hybrid/introduction.md) .
