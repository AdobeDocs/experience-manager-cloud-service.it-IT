---
title: Come accedere ai contenuti tramite API di consegna AEM
description: In questa parte del Percorso di sviluppatori AEM Headless, scopri come utilizzare le query GraphQL per accedere al contenuto dei frammenti di contenuto.
hide: true
hidefromtoc: true
index: false
exl-id: 5ef557ff-e299-4910-bf8c-81c5154ea03f
translation-type: tm+mt
source-git-commit: 861ef15a0060d51fd32e2d056871d1679f77a21e
workflow-type: tm+mt
source-wordcount: '1931'
ht-degree: 0%

---

# Come accedere ai contenuti tramite le API di consegna AEM {#access-your-content}

>[!CAUTION]
>
>LAVORO IN CORSO - La creazione di questo documento è in corso e non deve essere inteso come completo o definitivo né deve essere utilizzato a fini di produzione.

In questa parte del [AEM Percorso di sviluppatori headless,](overview.md) puoi imparare a utilizzare le query GraphQL per accedere al contenuto dei frammenti di contenuto.

## La storia finora {#story-so-far}

Nel documento precedente del percorso AEM headless [Come modellare il contenuto](model-your-content.md) hai appreso le nozioni di base sulla modellazione dei contenuti in AEM, quindi ora devi capire come modellare la struttura dei contenuti, quindi realizzare tale struttura utilizzando AEM Modelli di frammento di contenuto e Frammenti di contenuto:

* Riconoscere i concetti e la terminologia relativi alla modellazione dei contenuti.
* Scopri perché è necessaria la modellazione dei contenuti per la distribuzione di contenuti headless.
* Scopri come realizzare questa struttura utilizzando AEM modelli di frammenti di contenuto (e creare contenuti con frammenti di contenuto).
* Come modellare il contenuto; principi con campioni di base.

Questo articolo si basa su questi elementi fondamentali per comprendere come accedere al contenuto headless esistente in AEM utilizzando l’API GraphQL di AEM.

* **Pubblico**: Principiante
* **Obiettivo**: Scopri come accedere al contenuto dei frammenti di contenuto utilizzando AEM query GraphQL:
   * Introduce GraphQL e l&#39;API GraphQL AEM.
   * Approfondisci i dettagli dell’API GraphQL AEM.
   * Osserva alcune query di esempio per vedere come funzionano le cose nella pratica.

## Vuoi accedere ai tuoi contenuti? {#so-youd-like-to-access-your-content}

Quindi...hai tutto questo contenuto, ben strutturato (in Frammenti di contenuto) e in attesa di alimentare la tua nuova app. La domanda è: come arrivarci?

Ciò di cui hai bisogno è un modo per eseguire il targeting di contenuti specifici, seleziona ciò che ti serve e restituiscilo all’app per un’ulteriore elaborazione.

Con Adobe Experience Manager (AEM) come Cloud Service, puoi accedere in modo selettivo ai frammenti di contenuto, utilizzando l’API GraphQL di AEM, per restituire solo il contenuto necessario. Ciò significa che è possibile realizzare una distribuzione headless di contenuti strutturati da utilizzare nelle applicazioni.

>[!NOTE]
>
>AEM GraphQL API è un’implementazione personalizzata, basata sulle specifiche standard dell’API GraphQL.

## GraphQL - Introduzione {#graphql-introduction}

GraphQL è una specifica open source che fornisce:

* linguaggio di query che consente di selezionare contenuto specifico da oggetti strutturati.
* un runtime per eseguire queste query con il contenuto strutturato.

GraphQL è un&#39;API tipizzata *fortemente*. Questo significa che il contenuto *tutto* deve essere chiaramente strutturato e organizzato per tipo, in modo che GraphQL *comprenda* cosa accedere e come. I campi dati sono definiti all’interno degli schemi GraphQL, che definiscono la struttura degli oggetti contenuto.

Gli endpoint GraphQL forniscono quindi i percorsi che rispondono alle query GraphQL.

Ciò significa che l’app può selezionare in modo preciso, affidabile ed efficiente il contenuto necessario, esattamente ciò di cui hai bisogno quando viene utilizzata con AEM.

>[!NOTE]
>
>Consulta *GraphQL*.org e *GraphQL*.com.

## AEM e GraphQL {#aem-graphql}

GraphQL viene utilizzato in varie posizioni in AEM; ad esempio:

* Frammenti di contenuto
   * È stata sviluppata un’API personalizzata per questo caso d’uso (Distribuzione headless nell’app).
      * Questa è l&#39;API GraphQL AEM.
* Commerce
   * AEM Commerce consuma dati da una piattaforma Commerce tramite GraphQL.
   * Sono disponibili integrazioni GraphQL tra AEM e diverse soluzioni commerce di terze parti, utilizzate con gli hook di estensione forniti dai componenti core CIF.
      * Questo non utilizza l’API GraphQL AEM.

>[!NOTE]
>
>Questo passaggio del Percorso Headless riguarda solo l’API GraphQL AEM e i frammenti di contenuto.

## AEM API GraphQL {#aem-graphql-api}

L’API GraphQL di AEM è una versione personalizzata basata sulle specifiche standard dell’API GraphQL, appositamente configurata per consentire l’esecuzione di query (complesse) sui frammenti di contenuto.

I frammenti di contenuto vengono utilizzati, in quanto il contenuto è strutturato in base ai modelli di frammenti di contenuto . Questo soddisfa un requisito fondamentale di GraphQL.

* Un modello di frammento di contenuto è costituito da uno o più campi.
   * Ogni campo è definito in base a un tipo di dati.
* I modelli per frammenti di contenuto vengono utilizzati per generare gli schemi AEM GraphQL corrispondenti.

Per accedere effettivamente a GraphQL per AEM (e il contenuto) viene utilizzato un endpoint per fornire il percorso di accesso.

Il contenuto restituito, tramite l’API GraphQL di AEM, può quindi essere utilizzato dalle tue applicazioni.

>[!NOTE]
>
>L’implementazione AEM dell’API GraphQL si basa sulle librerie Java GraphQL.

### Casi d’uso per ambienti di authoring e pubblicazione {#use-cases-author-publish-environments}

I casi d’uso per l’API GraphQL AEM possono dipendere dal tipo di AEM come ambiente di Cloud Service:

* ambiente di pubblicazione; utilizzato per:
   * Contenuto della query per l’applicazione JS (caso d’uso standard)

* Ambiente di authoring; utilizzato per:
   * Query del contenuto a &quot;scopo di gestione dei contenuti&quot;:
      * GraphQL in AEM as a Cloud Service è attualmente un&#39;API di sola lettura.
      * L’API REST può essere utilizzata per le operazioni CR(u)D.

## Frammenti di contenuto da utilizzare con AEM API GraphQL {#content-fragments-use-with-aem-graphql-api}

I frammenti di contenuto possono essere utilizzati come base per GraphQL per AEM schemi e query come:

* Consentono di progettare, creare, curare e pubblicare contenuti indipendenti dalla pagina.
* Si basano su un modello di frammento di contenuto, che predefinisce la struttura del frammento risultante per mezzo di tipi di dati definiti.
* È possibile ottenere livelli aggiuntivi di struttura con il tipo di dati Riferimento frammento, disponibile quando si definisce un modello.

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

* Consente di creare e quindi recuperare dati strutturati.

   * Quando è definito come **multifeed**, è possibile fare riferimento a più frammenti secondari (recuperati) dal frammento principale.

### Anteprima JSON {#json-preview}

Per facilitare la progettazione e lo sviluppo di modelli di frammenti di contenuto, puoi visualizzare in anteprima l’output JSON nell’Editor frammento di contenuto.

## Generazione dello schema GraphQL da frammenti di contenuto {#graphql-schema-generation-content-fragments}

GraphQL è un’API fortemente tipizzata, il che significa che i contenuti devono essere chiaramente strutturati e organizzati per tipo. La specifica GraphQL fornisce una serie di linee guida su come creare una solida API per l’interrogazione dei contenuti su una determinata istanza. A questo scopo, un client deve recuperare lo schema, che contiene tutti i tipi necessari per una query.

Per i frammenti di contenuto, gli schemi GraphQL (struttura e tipi) si basano su **Modelli di frammento di contenuto abilitati** e i relativi tipi di dati.

>[!CAUTION]
>
>Tutti gli schemi GraphQL (derivati dai modelli di frammenti di contenuto che sono stati **abilitati**) sono leggibili tramite l’endpoint GraphQL.
>
>Questo significa che devi assicurarti che non sia disponibile alcun contenuto sensibile, per assicurarti che nessun dato sensibile sia esposto tramite gli endpoint GraphQL; ad esempio, include informazioni che potrebbero essere presenti come nomi di campo nella definizione del modello.

Ad esempio, se un utente ha creato un modello per frammenti di contenuto denominato `Article`, AEM genera l’oggetto `article` di tipo `ArticleModel`. I campi all’interno di questo tipo corrispondono ai campi e ai tipi di dati definiti nel modello.

1. Un Modello Di Frammento Di Contenuto:

   ![Modello per frammento di contenuto da utilizzare con ](assets/graphqlapi-cfmodel.png "GraphQLContent Fragment Model per l’utilizzo con GraphQL")

1. Lo schema GraphQL corrispondente (output dalla documentazione automatica GraphiQL):
   ![Schema GraphQL basato su schema ](assets/graphqlapi-cfm-schema.png "ModelGraphQL per frammenti di contenuto basato su modello di frammento di contenuto")

   Questo indica che il tipo generato `ArticleModel` contiene diversi [campi](#fields).

   * Tre di essi sono stati controllati dall’utente: `author`, `main` e `referencearticle`.

   * Gli altri campi sono stati aggiunti automaticamente da AEM e rappresentano metodi utili per fornire informazioni su un determinato frammento di contenuto; in questo esempio, `_path`, `_metadata`, `_variations`. Questi [campi helper](#helper-fields) sono contrassegnati con un `_` precedente per distinguere tra ciò che è stato definito dall&#39;utente e ciò che è stato generato automaticamente.

1. Dopo che un utente crea un frammento di contenuto basato sul modello di articolo, può essere interrogato tramite GraphQL. Ad esempio, consulta l’articolo sulle query di esempio .md#graphql-sample-query) (basate su una struttura di frammento di contenuto di esempio da utilizzare con GraphQL.

In GraphQL per AEM, lo schema è flessibile. Ciò significa che viene generato automaticamente ogni volta che viene creato, aggiornato o eliminato un modello di frammento di contenuto. Le cache dello schema dati vengono aggiornate anche quando si aggiorna un modello di frammento di contenuto.

Il servizio GraphQL di Sites ascolta (in background) le modifiche apportate a un modello di frammento di contenuto. Quando vengono rilevati aggiornamenti, viene rigenerata solo la parte dello schema. Questa ottimizzazione consente di risparmiare tempo e di garantire stabilità.

Ad esempio, se:

1. Installa un pacchetto contenente `Content-Fragment-Model-1` e `Content-Fragment-Model-2`:

   1. Verranno generati i tipi GraphQL per `Model-1` e `Model-2`.

1. Quindi modifica `Content-Fragment-Model-2`:

   1. Verrà aggiornato solo il tipo `Model-2` GraphQL.

   1. `Model-1` rimarrà invariato.

>[!NOTE]
>
>Questo è importante da notare nel caso in cui desideri eseguire aggiornamenti in blocco sui modelli di frammenti di contenuto tramite l’api REST o in altro modo.

Lo schema viene gestito attraverso lo stesso endpoint delle query GraphQL, con il client che gestisce il fatto che lo schema viene chiamato con l&#39;estensione `GQLschema`. Ad esempio, l’esecuzione di una semplice richiesta `GET` su `/content/cq:graphql/global/endpoint.GQLschema` darà luogo all’output dello schema con il tipo di contenuto: `text/x-graphql-schema;charset=iso-8859-1`.

### Generazione schema - Modelli non pubblicati {#schema-generation-unpublished-models}

Quando i frammenti di contenuto sono nidificati, può accadere che un modello di frammento di contenuto principale venga pubblicato, ma non lo è un modello di riferimento.

>[!NOTE]
>
>L’interfaccia utente AEM impedisce che ciò accada, ma se la pubblicazione viene effettuata a livello di programmazione o con pacchetti di contenuto può verificarsi.

In questo caso, AEM genera uno schema *incompleto* per il modello di frammento di contenuto principale. Ciò significa che il Riferimento frammento, che dipende dal modello non pubblicato, viene rimosso dallo schema.

## AEM Endpoint GraphQL {#aem-graphql-endpoints}

<!--
need details/examples
-->

Un endpoint è il percorso utilizzato per accedere a GraphQL per AEM. Utilizzando questo percorso (o la tua app) puoi:

* accedere agli schemi GraphQL,
* invia le query GraphQL,
* ricevere le risposte (alle query GraphQL).

AEM consente:

* Endpoint globale disponibile per tutti i siti.
* Endpoint tenant - che è possibile configurare, specifici per un sito o un progetto specifico.

## Autorizzazioni  {#permissions}

Le autorizzazioni sono quelle necessarie per accedere ad Assets.

## Interfaccia GraphiQL AEM {#aem-graphiql-interface}

Per facilitare l’input diretto e il test delle query, è disponibile per l’utilizzo con AEM GraphQL un’implementazione dell’interfaccia standard GraphiQL . Questo può essere installato con AEM.

Offre funzioni quali evidenziazione della sintassi, completamento automatico, suggerimento automatico, nonché una cronologia e una documentazione online.

![Interfaccia ](assets/graphiql-interface.png "GraphiQL")

## Utilizzo dell&#39;API GraphQL AEM {#using-aem-graphiql}

Per informazioni dettagliate sull’utilizzo dell’API GraphQL AEM e sulla configurazione degli elementi necessari, puoi fare riferimento a:

* Imparare a utilizzare GraphQL con AEM
* Struttura dei frammenti di contenuto di esempio
* Imparare a utilizzare GraphQL con AEM - Contenuto di esempio e query

## Novità {#whats-next}

Ora che hai imparato ad accedere ai contenuti headless e ad eseguire query tramite l’API GraphQL di AEM, ora [scopri come utilizzare l’API REST per accedere e aggiornare il contenuto dei frammenti di contenuto](/help/implementing/developing/headless-journey/update-your-content.md).

## Risorse aggiuntive {#additional-resources}

* [GraphQL.org](https://graphql.org)
   * [Schemi](https://graphql.org/learn/schema/)
   * [Variabili](https://graphql.org/learn/queries/#variables)
   * [Librerie Java GraphQL](https://graphql.org/code/#java)
* [GraphiQL](https://graphql.org/learn/serving-over-http/#graphiql)
* [Imparare a utilizzare GraphQL con AEM](/help/assets/content-fragments/graphql-api-content-fragments.md)
* [Struttura dei frammenti di contenuto di esempio](/help/assets/content-fragments/content-fragments-graphql-samples.md#content-fragment-structure-graphql)
* [Imparare a utilizzare GraphQL con AEM - Contenuto di esempio e query](/help/assets/content-fragments/content-fragments-graphql-samples.md)
   * [Query Di Esempio - Un Singolo Frammento Di Città Specifico](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-single-specific-city-fragment)
   * [Esempio di query per metadati - Elenco dei metadati per i riconoscimenti denominati GB](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-metadata-awards-gb)
   * [Query di esempio - Tutte le città con una variante denominata](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-cities-named-variation)
* [Abilitare la funzionalità dei frammenti di contenuto nel browser di configurazione](/help/assets/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser)
* [Utilizzo di frammenti di contenuto](/help/assets/content-fragments/content-fragments.md)
   * [Modelli per frammenti di contenuto](/help/assets/content-fragments/content-fragments-models.md)
   * [Output JSON](/help/assets/content-fragments/content-fragments-json-preview.md)
* [Comprendere la condivisione delle risorse tra le origini (CORS, Cross-Origin Resource Sharing)](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing.html?lang=en#understand-cross-origin-resource-sharing-(cors))
* [Generazione dei token di accesso per le API lato server](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md)
* [Guida introduttiva a AEM headless](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html)  - Una breve serie di esercitazioni video che offre una panoramica dell’utilizzo AEM funzioni headless, tra cui la modellazione dei contenuti e GraphQL.
