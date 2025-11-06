---
title: Materiali di riferimento API
description: AEM dispone di API estese e potenti che puoi utilizzare per il tuo progetto di esperienza digitale.
exl-id: d4ef3040-5a0a-4149-9e99-09eda9605038
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 4%

---

# Materiali di riferimento API {#api-reference-materials}

Adobe Experience Manager (AEM) fornisce molte API per lo sviluppo di applicazioni e l’estensione di AEM. AEM è basato su diverse tecnologie open-source, che possono anche essere utilizzate.

## API core di AEM {#core-aem-apis}

Le seguenti API sono core di AEM.

| API | Descrizione |
|---|---|
| [Adobe Experience Manager as a Cloud Service](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/index.html) | Astrazioni di prodotto come pagine, risorse, flussi di lavoro e così via. |
| [Interfaccia utente Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/index.html#) | Stack Open Web di Adobe, che fornisce vari componenti essenziali (i materiali 6.5 Granite si applicano ad AEMaaCS) |
| [Interfaccia utente Coral](https://opensource.adobe.com/coral-spectrum/documentation/) | Stile visivo di Adobe per le interfacce utente cloud, progettato per fornire coerenza nell’esperienza utente |

<!---
|Editor core JavaScript API reference|Provides all the base objects and concepts to support authoring of content resources|
--->

>[!NOTE]
>
>Per informazioni aggiornate sulle API di Experience Manager, visita anche [API di Adobe Experience Manager as a Cloud Service](https://developer.adobe.com/experience-cloud/experience-manager-apis/).

## Framework aggiuntivi {#additional-apis}

AEM si basa su diverse API open-source aggiuntive.

| API | Descrizione |
|---|---|
| [Sling Apache](https://sling.apache.org/apidocs/sling11/) | Framework web che utilizza un Java Content Repository (JCR) per archiviare e gestire i contenuti |
| [Apache Jackrabbit Oak](https://jackrabbit.apache.org/oak/docs/oak_api/overview.html) | Implementazione di un Java Content Repository (JCR) gerarchico scalabile e ad alte prestazioni da utilizzare come base per siti web moderni di prim’ordine |
| [Archivio contenuto Java](https://www.adobe.io/experience-manager/reference-materials/spec/javax.jcr/javadocs/jcr-2.0/index.html) | Specifiche per JCR versione 2.0 |
| [Apache Felix](https://felix.apache.org) | Implementazione del framework e della piattaforma di servizi Open Services Gateway (OSGi) |

## Linee guida sulle preferenze API {#guidelines}

AEM è basato sui seguenti quattro set di API Java primari in ordine decrescente di preferenza.

| Priorità | API | Descrizione |
|---|---|---|
| 1 | [Adobe Experience Manager as a Cloud Service](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/index.html) | Astrazioni di prodotto come pagine, risorse, flussi di lavoro e così via. |
| 2 | [Sling Apache](https://sling.apache.org/apidocs/sling11/) | Astrazioni REST e basate su risorse come risorse, mappe del valore e richieste HTTP. |
| 3 | [Apache Jackrabbit Oak](https://jackrabbit.apache.org/oak/docs/oak_api/overview.html) | Astrazioni di dati e contenuti come nodo, proprietà e sessioni. |
| 4 | [Apache Felix](https://felix.apache.org/) | Astrazioni dei contenitori di applicazioni OSGi come servizi e componenti (OSGi). |

Se un’API è fornita da AEM, preferiscila a Sling, JCR e OSGi. Se AEM non fornisce un’API, preferisci Sling rispetto a JCR e OSGi.

>[!TIP]
>
>Per informazioni dettagliate su queste linee guida, consulta il documento [Comprendere le best practice per le API Java](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/understand-java-api-best-practices.html?lang=it).

## Servizi e API di distribuzione e gestione dei contenuti di AEM {#delivery-apis}

AEM offre componenti personalizzabili e opzioni di distribuzione dei contenuti.

| Funzione | Descrizione |
|---|---|
| [Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=it) | Componenti WCM (Web Content Management) standardizzati per AEM per velocizzare i tempi di sviluppo e ridurre i costi di manutenzione dei siti Web |
| [Esportatore JSON](/help/implementing/developing/components/json-exporter.md) | Distribuisci il contenuto di qualsiasi pagina AEM in formato modello dati JSON |
| [Abilitazione dell’esportazione JSON per un componente](/help/implementing/developing/components/enabling-json-exporter.md) | Generare l’esportazione JSON di contenuto componente basato su un framework modeler |
| [OpenAPI per il modello Frammento di contenuto e Frammento di contenuto](/help/headless/content-fragment-openapis.md) | OpenAPI per frammenti di contenuto e modelli di frammenti di contenuto |
| [Distribuzione di frammenti di contenuto AEM con OpenAPI](/help/headless/aem-content-fragment-delivery-with-openapi.md) | API REST HTTP su AEM Edge Delivery Services, progettata per distribuire contenuti strutturati da frammenti di contenuto in formato JSON. |
| [API GraphQL per frammenti di contenuto](/help/headless/graphql-api/content-fragments.md) | Consentire la distribuzione efficiente dei frammenti di contenuto ai client JavaScript nelle implementazioni CMS headless |
|  |  |
| [API Assets](/help/assets/mac-api-assets.md) | Consente operazioni di creazione-lettura-aggiornamento-eliminazione (CRUD) sulle risorse, inclusi dati binari, metadati, rappresentazioni e commenti. Consulta API HTTP di AEM Assets |
| [API HTTP frammenti di contenuto](/help/assets/content-fragments/assets-api-content-fragments.md) | Accedere ai contenuti dei frammenti di contenuto direttamente tramite l’API HTTP tramite operazioni CRUD |
| [Frammenti di contenuto API HTTP Assets](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/assets/admin/mac-api-assets) | Formato esatto delle richieste di risorse HTTP supportate |

>[!NOTE]
>
>Consulta [API di AEM per la distribuzione e la gestione strutturata dei contenuti](/help/headless/apis-headless-and-content-fragments.md) per una panoramica delle varie API disponibili e un confronto di alcuni dei concetti coinvolti.

## API specifiche per applicazioni a pagina singola {#spa-apis}

Il framework SDK dell’editor di applicazioni a pagina singola di AEM fornisce riferimenti API specifici per JavaScript.

| API | Descrizione |
|---|---|
| [Mappatura componenti](https://www.npmjs.com/package/@adobe/aem-spa-component-mapping) | Consente all&#39;applicazione a pagina singola di mappare i componenti front-end ai tipi di risorse Adobe Experience Manager (componenti AEM) |
| [Gestione modelli pagine](https://www.npmjs.com/package/@adobe/aem-spa-page-model-manager) | Interprete tra Adobe Experience Manager Editor e Adobe Experience Manager Single Page Application (SPA) Editor |
| [Componenti modificabili React](https://www.npmjs.com/package/@adobe/aem-react-editable-components) | Fornisce i componenti React e il livello di integrazione per iniziare a utilizzare Adobe Experience Manager Site Editor |
| [Componenti modificabili di Angular](https://www.npmjs.com/package/@adobe/aem-angular-editable-components) | Fornisce i componenti e il livello di integrazione di Angular per iniziare a utilizzare l’Editor siti di Adobe Experience Manager |

>[!TIP]
>
>Per ulteriori informazioni sulle applicazioni a pagina singola, vedere [Introduzione e procedura dettagliata per applicazioni a pagina singola](/help/implementing/developing/hybrid/introduction.md).
