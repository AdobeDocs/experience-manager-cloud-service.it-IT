---
title: Come accedere ai contenuti tramite API di consegna AEM
description: In questa parte del Percorso di sviluppatori AEM Headless, scopri come utilizzare le query GraphQL per accedere al contenuto dei frammenti di contenuto.
hide: true
hidefromtoc: true
index: false
translation-type: tm+mt
source-git-commit: d17583399b6792583e3e210005b62d360b91d05a
workflow-type: tm+mt
source-wordcount: '764'
ht-degree: 2%

---


# Come accedere ai contenuti tramite le API di consegna AEM {#access-your-content}

>[!CAUTION]
>
>LAVORO IN CORSO - La creazione di questo documento è in corso e non deve essere inteso come completo o definitivo né deve essere utilizzato a fini di produzione.

In questa parte del [AEM Percorso di sviluppatori headless,](#overview.md) scopri come utilizzare le query GraphQL per accedere al contenuto dei frammenti di contenuto.

## La storia finora {#story-so-far}

Nel documento precedente del percorso AEM headless, [Come modellare il contenuto](model-your-content.md) hai appreso le nozioni di base sulla modellazione dei dati in AEM e ora devi:

* Comprendere importanti considerazioni sulla pianificazione per la progettazione dei contenuti.
* Comprendi i passaggi per implementare headless in base ai requisiti del livello di integrazione.
* Imposta gli strumenti e le configurazioni AEM necessarie.
* Scopri le best practice per semplificare il tuo percorso headless, garantire l’efficienza nella generazione dei contenuti e la distribuzione rapida dei contenuti.

Questo articolo si basa su questi elementi fondamentali per comprendere come accedere ai contenuti headless esistenti in AEM tramite API.

* **Pubblico**: Principiante
* **Obiettivo**: Scopri come accedere al contenuto dei frammenti di contenuto utilizzando AEM query GraphQL:
   * Introduzione a GraphQL.
   * Introduzione AEM API GraphQL.
   * Approfondisci i dettagli dell’API GraphQL AEM.
   * Osserva alcune query di esempio per vedere come funzionano le cose nella pratica.

Con Adobe Experience Manager (AEM) come Cloud Service, puoi utilizzare Frammenti di contenuto, insieme all’API GraphQL di AEM, per distribuire in modo headless contenuti strutturati da utilizzare nelle tue applicazioni. La possibilità di personalizzare un’unica query API ti consente di recuperare e fornire il contenuto specifico di cui desideri eseguire il rendering (come risposta alla singola query API).

>[!NOTE]
>AEM GraphQL API è un’implementazione personalizzata, basata su GraphQL standard.

## GraphQL - Introduzione {#graphql-introduction}

GraphQL è:

* &quot;*..un linguaggio di query per le API e un runtime per l&#39;esecuzione di tali query con i dati esistenti.*&quot;.

   Consulta *GraphQL*.

### GraphQL - Tipi {#graphql-types}

### GraphQL - Schemi {#graphql-schemas}

### GraphQL - Query {#graphql-queries}

## AEM e GraphQL {#aem-graphql}

GraphQL viene utilizzato in varie posizioni in AEM:

* Commerce
   * Segnaposto
* Frammenti di contenuto
   * Per questo caso d’uso è stata sviluppata un’API personalizzata.
   * Questa è l&#39;API GraphQL AEM.

## AEM API GraphQL {#aem-graphql-api}

Per Adobe Experience as a Cloud Experience è stata sviluppata un’implementazione personalizzata dell’API GraphQL standard.

L’API GraphQL AEM consente di eseguire query (complesse) sui frammenti di contenuto; con ogni query in base a un tipo di modello specifico. Il contenuto restituito può quindi essere utilizzato dalle applicazioni.

>[!NOTE]
>
>L’implementazione AEM dell’API GraphQL si basa sulle librerie Java GraphQL.

### AEM API GraphQL e frammenti di contenuto {#aem-graphql-content-fragments}

## Frammenti di contenuto da utilizzare con AEM API GraphQL {#content-fragments-use-with-aem-graphql-api}

I frammenti di contenuto possono essere utilizzati come base per GraphQL per query AEM come:

* Consentono di progettare, creare, curare e pubblicare contenuti indipendenti dalla pagina.
* I modelli per frammenti di contenuto forniscono la struttura richiesta tramite tipi di dati definiti.
* Il Riferimento frammento, disponibile quando si definisce un modello, può essere utilizzato per definire livelli di struttura aggiuntivi.

### Frammenti di contenuto {#content-fragments}

Frammenti di contenuto:

* Contenere contenuti strutturati.

* Si basano su un modello di frammento di contenuto, che predefinisce la struttura per il frammento risultante.

### Modelli per frammenti di contenuto {#content-fragments-models}

Questi Modelli Di Frammento Di Contenuto:

* Vengono utilizzati per generare gli schemi una volta **Abilitato**.

* Fornisci i tipi di dati e i campi richiesti per GraphQL. Assicurano che la tua applicazione richieda solo ciò che è possibile e riceva ciò che è previsto.

* Il tipo di dati **Riferimenti frammento** può essere utilizzato nel modello per fare riferimento a un altro frammento di contenuto e quindi introdurre livelli aggiuntivi di struttura.

### Riferimenti a frammento {#fragment-references}

Il **Riferimento al frammento**:

* È di particolare interesse in combinazione con GraphQL.

* È un tipo di dati specifico che può essere utilizzato durante la definizione di un modello di frammento di contenuto.

* Fa riferimento a un altro frammento, a seconda di un modello di frammento di contenuto specifico.

* Consente di recuperare dati strutturati.

   * Quando è definito come **multifeed**, è possibile fare riferimento a più frammenti secondari (recuperati) dal frammento principale.

### Anteprima JSON {#json-preview}

Per semplificare la progettazione e lo sviluppo dei modelli di frammenti di contenuto, puoi visualizzare in anteprima l’ [output JSON](/help/assets/content-fragments/content-fragments-json-preview.md).

## Novità {#whats-next}

[Scopri come utilizzare l’API REST per accedere e aggiornare il contenuto dei frammenti](/help/implementing/developing/headless-journey/update-your-content.md) di contenuto.

## Risorse aggiuntive {#additional-resources}

* [Guida introduttiva a AEM headless](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html) : breve serie di esercitazioni video che offre una panoramica dell’utilizzo di AEM funzioni headless, tra cui la modellazione dei dati e GraphQL
* [GraphQL.org](https://graphql.org)
   * [Schemi](https://graphql.org/learn/schema/)
   * [Librerie Java GraphQL](https://graphql.org/code/#java)
* [AEM API GraphQL per l’utilizzo con frammenti di contenuto](/help/assets/content-fragments/graphql-api-content-fragments.md)
   * [Imparare a utilizzare GraphQL con AEM - Contenuto di esempio e query](/help/assets/content-fragments/content-fragments-graphql-samples.md)
   * [Autenticazione per query GraphQL AEM remote su frammenti di contenuto](/help/assets/content-fragments/graphql-authentication-content-fragments.md)
* [Utilizzo di frammenti di contenuto](/help/assets/content-fragments/content-fragments.md)
   * [Modelli per frammenti di contenuto](/help/assets/content-fragments/content-fragments-models.md)
   * [Output JSON](/help/assets/content-fragments/content-fragments-json-preview.md)
