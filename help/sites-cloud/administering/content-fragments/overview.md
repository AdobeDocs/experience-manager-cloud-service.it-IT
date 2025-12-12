---
title: Panoramica dei concetti e delle best practice per l’utilizzo dei frammenti di contenuto
description: Scopri come i frammenti di contenuto in Adobe Experience Manager (AEM) as a Cloud Service ti consentono di creare e utilizzare contenuti strutturati; ideali per la distribuzione headless e l’authoring delle pagine.
feature: Content Fragments
role: User, Developer
exl-id: ce9cb811-57d2-4a57-a360-f56e07df1b1a
solution: Experience Manager Sites
source-git-commit: 2449bc380268ed42b6c8d23ae4a4fecaf1736889
workflow-type: tm+mt
source-wordcount: '2357'
ht-degree: 30%

---

# Utilizzo dei frammenti di contenuto: concetti e best practice {#working-with-content-fragments-concepts-and-best-practices}

Con Adobe Experience Manager (AEM) as a Cloud Service, i frammenti di contenuto ti consentono di progettare, creare, curare e pubblicare contenuti indipendenti dalla pagina. Consentono di preparare contenuti pronti per l&#39;uso in più posizioni e su più canali, ideali per [distribuzione headless](/help/headless/what-is-headless.md) e [creazione pagine](/help/sites-cloud/authoring/fragments/content-fragments.md).

>[!IMPORTANT]
>
>Molte funzionalità descritte in questa sezione sono *solo* disponibili in [Unified Shell](/help/overview/aem-cloud-service-on-unified-shell.md); pertanto *online* Adobe Experience Manager (AEM) as a Cloud Service, non un&#39;istanza locale.

>[!IMPORTANT]
>
>È possibile accedere ai frammenti di contenuto da due console: **Frammenti di contenuto** e **Assets**.
>
>Esistono anche due editor per l’authoring dei frammenti di contenuto; sebbene la funzionalità di base sia la stessa, vi sono alcune differenze. Entrambi gli editor sono accessibili da entrambe le console.
>
>Questa sezione tratta la console **Frammenti di contenuto** e l&#39;editor frammenti di contenuto *new*. Questi sono stati sviluppati per la distribuzione di contenuti headless (anche se possono essere utilizzati in tutti gli scenari)
>
>Per ulteriori informazioni, consulta:
>
>* utilizzo della console **Assets** per [gestione dei frammenti di contenuto](/help/assets/content-fragments/content-fragments-managing.md)
>* utilizzo dell&#39;[*editor frammento di contenuto originale*](/help/assets/content-fragments/content-fragments-variations.md),
>* utilizzo di [Frammenti di contenuto per l&#39;authoring delle pagine](/help/sites-cloud/authoring/fragments/content-fragments.md).


I frammenti di contenuto contengono contenuti strutturati:

* Ogni frammento è basato su un [Modello per frammenti di contenuto](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md).
   * Il [Modello per frammenti di contenuto definisce la struttura](/help/sites-cloud/administering/content-fragments/content-fragment-models.md) del frammento risultante.
* Ogni frammento è costituito da:
   * **[Principale](#main-and-variations)**: parte integrante del frammento che contiene il contenuto principale. Esiste sempre e non può essere eliminata
   * **[Varianti](#main-and-variations)** - Una o più permutazioni del contenuto, create dall&#39;autore
* La struttura può essere di tre tipi:
   * Base
      * Ad esempio, un singolo campo di testo su più righe.
      * Può essere utilizzata per preparare contenuti semplici da utilizzare nell’authoring delle pagine.
      * Può essere utilizzato anche per la consegna headless all’applicazione.
   * Complessa
      * Combinazione di molti campi di tipi di dati diversi, tra cui testo, numeri, dati booleani e data e ora.
      * Può essere utilizzato per preparare contenuti più strutturati per l’authoring delle pagine o per la distribuzione headless all’applicazione.
   * Nidificata
      * I tipi di dati di riferimento disponibili consentono di nidificare il contenuto.
      * Tende a essere utilizzato per la consegna headless all’applicazione.

I frammenti di contenuto possono essere consegnati anche in formato JSON, utilizzando le funzionalità di esportazione Sling Model (JSON) dei componenti core di AEM. Questo tipo di consegna:

* consente di utilizzare il componente per gestire gli elementi di un frammento da consegnare;
* consente la distribuzione in blocco; aggiungendo più [componenti core Frammento di contenuto](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/content-fragment-component.html?lang=it) nella pagina utilizzata per la distribuzione API

Il numero di canali di comunicazione aumenta ogni anno. In genere i canali si distinguono in base al meccanismo di consegna, come segue:

* Canale fisico; ad esempio, desktop, dispositivi mobili.
* Forma di consegna in un canale fisico, ad esempio “pagina dei dettagli di un prodotto”, “pagina della categoria del prodotto” per desktop oppure “web mobile”, “app mobile” per dispositivi mobili.

Tuttavia, probabilmente non desideri utilizzare *esatto* stesso contenuto per tutti i canali. È necessario ottimizzare il contenuto in base al canale specifico.

I frammenti di contenuto consentono di:

* valutare come raggiungere in modo efficiente il pubblico target su ciascun canale;
* creare e gestire contenuti editoriali indipendenti dal canale;
* creare pool di contenuti per una serie di canali;
* progettare varianti di contenuto per canali specifici;
* Per aggiungere immagini al testo, inserisci le risorse.
* creare contenuti nidificati in base alla complessità dei dati.

Questi frammenti di contenuto possono quindi essere assemblati per fornire esperienze su diversi canali.

>[!NOTE]
>
>I **frammenti di contenuto** e i **[frammenti di esperienza](/help/sites-cloud/authoring/fragments/content-fragments.md)** sono funzioni diverse in AEM:
>
>* I **frammenti di contenuto** sono contenuti editoriali, con definizione e struttura, ma senza elementi visivi aggiuntivi di design e/o layout. Possono essere utilizzati per accedere a dati strutturati, tra cui testi, numeri e date.
>* I **frammenti di esperienza** sono contenuti completi di layout, frammenti di una pagina web.
>
>I frammenti esperienza possono includere contenuti sotto forma di frammenti di contenuto, ma non viceversa.
>
>Per ulteriori informazioni, vedere [Informazioni sui frammenti di contenuto e sui frammenti di esperienza in AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/content-fragments/understand-content-fragments-and-experience-fragments.html?lang=it#content-fragments).

Questa pagina e quelle seguenti descrivono le attività di creazione, configurazione, manutenzione e utilizzo dei frammenti di contenuto:

* [Abilita funzionalità frammento di contenuto per la tua istanza](/help/sites-cloud/administering/content-fragments/setup.md)
* [Modelli per frammenti di contenuto](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md) - abilitazione, creazione e [definizione](/help/sites-cloud/administering/content-fragments/content-fragment-models.md) dei modelli
* [Crea i tuoi frammenti di contenuto](/help/sites-cloud/administering/content-fragments/managing.md#creating-a-content-fragment) (utilizzando la console Frammenti di contenuto)

Dopo la creazione dei frammenti, puoi:

* [Utilizzare la console Frammenti di contenuto](/help/sites-cloud/administering/content-fragments/managing.md) per:
   * accedere ai frammenti, pubblicarli (per l’anteprima o la produzione) e farvi riferimento
* [Utilizza l&#39;editor frammenti di contenuto](/help/sites-cloud/administering/content-fragments/authoring.md) per:
   * modificare, pubblicare (per visualizzare in anteprima o produrre) e fare riferimento ai frammenti
   * collaborare con altri autori utilizzando Commenti
* [Analizza](/help/sites-cloud/administering/content-fragments/analysis.md) la struttura del frammento di contenuto, utilizzando l&#39;editor
* [Accedi ai tuoi frammenti con GraphQL per la consegna headless nelle tue applicazioni](/help/sites-cloud/administering/content-fragments/content-delivery-with-graphql.md).
* [Integrare e utilizzare i frammenti di contenuto in Adobe Journey Optimizer](/help/sites-cloud/administering/content-fragments/content-fragments-with-journey-optimizer.md)
* Crea e gestisci [Avvii per frammenti di contenuto](/help/sites-cloud/administering/content-fragments/launches-for-content-fragments.md)
* [Oppure utilizza i tuoi frammenti per creare le pagine](/help/sites-cloud/authoring/fragments/content-fragments.md)

>[!NOTE]
>
>Queste pagine possono essere lette insieme a:
>
>* [Personalizzazione ed estensione dei frammenti di contenuto](/help/implementing/developing/extending/content-fragments-customizing.md)
>* [Componenti di configurazione dei frammenti di contenuto per il rendering](/help/implementing/developing/extending/content-fragments-configuring-components-rendering.md)
>* [Supporto dei frammenti di contenuto nell’API HTTP di AEM Assets](/help/assets/content-fragments/assets-api-content-fragments.md)
>* [API GraphQL di AEM per l’utilizzo con Frammenti di contenuto](/help/headless/graphql-api/content-fragments.md)
>* [Authoring delle pagine con frammenti di contenuto](/help/sites-cloud/authoring/fragments/content-fragments.md).
>* Sono disponibili anche [OpenAPI per frammenti di contenuto e modelli di frammenti di contenuto](/help/headless/content-fragment-openapis.md).


## Principale e varianti {#main-and-variations}

Le varianti sono una funzione significativa dei Frammenti di contenuto di AEM. Consentono di creare e modificare copie del contenuto **Principale** da utilizzare su canali e scenari specifici, rendendo ancora più flessibile la distribuzione di contenuti headless e l&#39;authoring delle pagine.

* **Principale**

   * **Principale** non è una variante in quanto tale, ma è la base di tutte le varianti.
   * Parte integrante del frammento

      * Ogni frammento di contenuto ha un&#39;istanza di **Main**.
      * Impossibile eliminare **Main**.

   * **Principale** è accessibile nell&#39;editor frammenti in **[Varianti](/help/sites-cloud/administering/content-fragments/authoring.md#variations)**.

  >[!NOTE]
  >
  >Nell&#39;editor disponibile nella console **Assets**, **Main** è etichettato come **Master**.

* **Varianti**

   * Sono rappresentazioni di testo dei frammenti a scopo editoriale; possono essere relative a un canale ma non necessariamente, e possono anche essere utilizzate per modifiche locali ad hoc.
   * Sono create come copie di **Principale**, ma possono essere modificate in base alle esigenze. Spesso vi è una sovrapposizione di contenuto tra le varianti stesse.
   * Può essere definito durante la creazione del frammento, dal pannello a sinistra.
   * Sono memorizzate nel frammento, per evitare la dispersione delle copie del contenuto.
   * Le varianti possono essere [confrontate e sincronizzate](/help/sites-cloud/administering/content-fragments/authoring.md#compare-and-synchronize-rich-text) con **Principale**.
  <!--
  * Can be [Summarized](/help/sites-cloud/administering/content-fragments/authoring.md#summarizing-text) to quickly truncate the text to a predefined length.
  -->

## Frammenti di contenuto e Content Services {#content-fragments-and-content-services}

AEM Content Services è progettato per generalizzare la descrizione e la consegna dei contenuti in/da AEM, non limitandosi alle pagine web.

Fornisce contenuti a canali diversi dalle tradizionali pagine web di AEM, utilizzando metodi standardizzati utilizzabili da qualsiasi cliente. Questi canali possono includere:

* Applicazioni a pagina singola
* Applicazioni mobile native
* Altri canali e punti di contatto esterni ad AEM

La consegna viene effettuata in formato JSON utilizzando il modulo di esportazione JSON.

I frammenti di contenuto di AEM possono essere utilizzati per descrivere e gestire contenuti strutturati. I contenuti strutturati vengono definiti in modelli che possono contenere diversi tipi di contenuto, compresi testo, dati numerici, dati booleani, data e ora e altro ancora.

Insieme alle funzionalità di esportazione JSON dei componenti core di AEM, tali contenuti strutturati possono quindi essere utilizzati per consegnare contenuti AEM a canali diversi dalle pagine AEM.

>[!NOTE]
>
>Consulta [Headless e AEM](/help/headless/introduction.md) per un’introduzione allo sviluppo headless per AEM Sites as a Cloud Service.

>[!NOTE]
>
>AEM supporta anche la traduzione del contenuto dei frammenti. Per ulteriori informazioni, consulta [Traduzione ddelle risorse](/help/assets/translate-assets.md).

## Tipo di contenuto {#content-type}

I frammenti di contenuto sono:

* Una funzionalità di **Sites**.

* Memorizzati come **Risorse**:

   * I frammenti di contenuto (e le relative varianti) possono essere creati e gestiti dalla [console Frammenti di contenuto](#content-fragments-console).
   * Creato e modificato nell&#39;[Editor frammento di contenuto](/help/sites-cloud/administering/content-fragments/authoring.md).

* Accessibile per la distribuzione dei contenuti tramite l&#39;[API GraphQL di AEM](/help/headless/graphql-api/content-fragments.md).

* Disponibile nell&#39;editor di pagine [ tramite il componente Frammento di contenuto](/help/sites-cloud/authoring/fragments/content-fragments.md) (componente di riferimento):

   * Il [componente core Frammento di contenuto](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/content-fragment-component.html?lang=it) è disponibile per gli autori di pagine. Consente loro di fare riferimento e distribuire il frammento di contenuto richiesto in formato HTML o JSON.

I frammenti di contenuto sono una struttura di contenuto che:

* Sono privi di layout o progettazione (la formattazione del testo è possibile per i campi di testo).
* È indipendente dal meccanismo di consegna (ad esempio la pagina o il canale).
* contiene una o più [parti costituenti](#constituent-parts-of-a-content-fragment);
* può [contenere immagini o essere connessa ad esse](#fragments-with-visual-assets);

### Frammenti con risorse visive {#fragments-with-visual-assets}

Per dare agli autori un maggiore controllo sui contenuti, le immagini possono essere aggiunte a e/o integrate con un frammento di contenuto.

Assets può essere utilizzato con un frammento di contenuto in diversi modi, ciascuno con i propri vantaggi:

* as a **Riferimento contenuto**
* in un campo **Testo su più righe**

### Parti costitutive di un frammento di contenuto {#constituent-parts-of-a-content-fragment}

Le risorse dei frammenti di contenuto sono composte dalle seguenti parti (direttamente o indirettamente):

* **Elementi del frammento**

   * Gli elementi sono correlati ai campi di dati che contengono il contenuto.
   * Per creare il frammento di contenuto si utilizza un [modello per frammenti di contenuto](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md). Gli elementi (campi) [specificati nel modello definiscono la struttura del frammento](/help/sites-cloud/administering/content-fragments/content-fragment-models.md). Questi elementi (campi) possono essere di diversi tipi di dati.

* **Paragrafi del frammento**

   * Blocchi di testo, spesso con più righe, delimitati come singole entità.

   * Consentono di controllare i contenuti durante l’authoring delle pagine.

* **Metadati del frammento**

   * Utilizzano gli [schemi di metadati delle risorse](/help/assets/metadata-schemas.md).
   * È possibile creare i tag quando:

      * si crea e si effettua l’authoring del frammento;
      * Oppure in un secondo momento, quando [visualizzi o modifichi le proprietà](/help/sites-cloud/administering/content-fragments/authoring.md#view-properties-tags) nell&#39;editor frammenti

  >[!CAUTION]
  >
  >I profili di elaborazione dei metadati non sono applicabili ai frammenti di contenuto.

  >[!CAUTION]
  >
  >Un modello per frammenti di contenuto può spesso definire campi di dati denominati **Titolo** e **Descrizione**. Se questi due campi esistono, sono campi definiti dall’utente e possono essere aggiornati nell’area del contenuto dell’editor.
  >
  >Il frammento di contenuto e le relative varianti dispongono anche di campi di metadati (proprietà) denominati **Titolo** e **Descrizione**. Questi due campi di metadati sono parte integrante di qualsiasi frammento di contenuto e variante e sono inizialmente definiti al momento della creazione del frammento. Possono essere aggiornati nell’area proprietà/metadati dell’editor.

* **[Principale](#main-and-variations)**
* **[Varianti](#main-and-variations)**

### Elementi necessari per i frammenti {#required-by-fragments}

Per creare frammenti di contenuto sono necessari i seguenti elementi:

* **Modello di contenuto**

   * Viene [abilitato tramite il Browser configurazioni](/help/sites-cloud/administering/content-fragments/setup.md).
   * Sono [creati utilizzando la Console Frammenti di contenuto](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md#creating-a-content-fragment-model).
   * È necessario per [creare un frammento](/help/sites-cloud/administering/content-fragments/managing.md#creating-content-fragments).
   * Definisce la struttura di un frammento (titolo, elementi di contenuto, definizioni tag).
   * Le definizioni del modello per frammenti di contenuto richiedono un titolo e un elemento dati; tutto il resto è facoltativo.
   * Il modello può definire eventuale contenuto predefinito.
   * Gli autori non possono modificare la struttura definita durante l’authoring del contenuto di un frammento, anche se possono aprire l’editor modelli dall’editor frammenti.
   * Le modifiche apportate a un modello dopo la creazione dei frammenti di contenuto dipendenti possono influire su tali frammenti di contenuto.

Per utilizzare i frammenti di contenuto per la distribuzione di contenuti headless è inoltre necessario:

* una [query GraphQL](/help/headless/graphql-api/content-fragments.md) per richiedere il contenuto richiesto
* questo contenuto può quindi essere utilizzato per sviluppare applicazioni a pagina singola per AEM; per ulteriori informazioni, consulta i seguenti documenti:

   * [Tutorial WKND per SPA](/help/implementing/developing/hybrid/wknd-tutorial.md)
   * [Guida introduttiva all’utilizzo di React](/help/implementing/developing/hybrid/getting-started-react.md)
   * [Guida introduttiva all’utilizzo di Angular](/help/implementing/developing/hybrid/getting-started-angular.md)

Per utilizzare i frammenti di contenuto nell’authoring delle pagine è inoltre necessario:

* Un **componente Frammento di contenuto**

   * Essenziale per la distribuzione del frammento in formato HTML e/o JSON.
   * Obbligatorio per [fare riferimento al frammento in una pagina](/help/sites-cloud/authoring/fragments/content-fragments.md).
   * Responsabile del layout e della distribuzione di un frammento, ad esempio i canali.
   * I frammenti devono disporre di uno o più componenti dedicati per definire il layout e fornire alcuni o tutti gli elementi/varianti e i contenuti associati.
   * Quando si trascina un frammento su una pagina durante l’authoring, il componente richiesto viene associato automaticamente.
   * Consulta il [componente core Frammento di contenuto](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/content-fragment-component.html?lang=it).

## Console Frammenti di contenuto {#content-fragments-console}

La console Frammenti di contenuto è dedicata alla gestione, alla ricerca e alla creazione di [frammenti di contenuto](/help/sites-cloud/administering/content-fragments/managing.md), [modelli di frammenti di contenuto](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md) e [Assets](/help/sites-cloud/administering/content-fragments/assets-content-fragments-console.md). È stata ottimizzata per l’utilizzo in un contesto headless, ma viene utilizzata anche durante la creazione di frammenti di contenuto e modelli di frammenti di contenuto da utilizzare nell’authoring delle pagine.

È possibile accedere direttamente alla console dal livello superiore della navigazione globale.

![Navigazione globale - Console Frammenti di contenuto](assets/cf-managing-global-navigation.png)

Puoi utilizzare l’ultimo pannello a sinistra per selezionare il tipo di risorsa da visualizzare, sfogliare e gestire:

![Console Frammenti di contenuto - navigazione](/help/sites-cloud/administering/content-fragments/assets/cf-console-assets-navigation.png)

Per informazioni dettagliate, consulta:

* [Frammenti di contenuto](/help/sites-cloud/administering/content-fragments/managing.md)
* [Modelli per frammenti di contenuto](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md)
* [Risorse](/help/sites-cloud/administering/content-fragments/assets-content-fragments-console.md)

* Una selezione di [scelte rapide da tastiera](/help/sites-cloud/administering/content-fragments/keyboard-shortcuts.md) è disponibile per questa console

>[!CAUTION]
>
>Questa console è *solo* disponibile nell&#39;as a Cloud Service online di Adobe Experience Manager (AEM).

>[!NOTE]
>
>Se necessario, il team del progetto può personalizzare la console e l’editor. Per ulteriori dettagli, consulta [Personalizzazione della console e dell&#39;editor dei frammenti di contenuto](/help/implementing/developing/extending/content-fragments-console-and-editor.md).

## Esempio di utilizzo {#example-usage}

Un frammento, con i relativi elementi e varianti, può essere utilizzato per creare contenuti coerenti per più canali. Durante la progettazione del frammento è necessario considerare cosa verrà utilizzato e dove.

### Esempio WKND {#wknd-sample}

Per apprendere a utilizzare AEM as a Cloud Service, vengono forniti gli esempi [Sito WKND e Condiviso WKND](/help/implementing/developing/introduction/develop-wknd-tutorial.md).

<!-- CHECK: which links can/should be used these days? -->

Il progetto WKND include:

* Modelli di Frammento di contenuto disponibili in:

   * `.../libs/dam/cfm/models/console/content/models.html/conf/wknd`

   * `.../ui#/aem/libs/dam/cfm/models/console/content/models.html/conf/wknd-shared`

* Frammenti di contenuto (e altro contenuto) disponibili in:

   * `.../assets.html/content/dam/wknd/en`

## Best practice {#best-practices}

I frammenti di contenuto possono essere utilizzati per formare strutture complesse. Adobe offre consigli sulle best practice da seguire per la definizione e l’utilizzo di modelli e frammenti.

### Semplifica {#keep-it-simple}

Durante la modellazione di contenuti strutturati in AEM, utilizza strutture di contenuto quanto più semplici possibile per garantire prestazioni di sistema elevate e governance semplificata.

### Numero di modelli {#number-of-models}

Crea tutti i modelli di contenuto necessari, ma non più.

Troppi modelli complicano la governance e possono rallentare le query GraphQL. Di solito è sufficiente un piccolo insieme di modelli, massimo di decine basse. Se ti avvicini alle dieci o più alte, riconsidera la tua strategia di modellazione.

### Nidificazione di modelli e frammenti (molto importante) {#nesting-models-and-fragments}

Evita la nidificazione profonda o eccessiva dei frammenti di contenuto utilizzando i Riferimenti ai frammenti di contenuto, che consentono ai frammenti di fare riferimento ad altri frammenti, a volte su più livelli.

L’utilizzo intensivo dei riferimenti ai frammenti di contenuto può influire in modo significativo sulle prestazioni del sistema, sulla reattività dell’interfaccia utente e sull’esecuzione delle query GraphQL. Mirare a mantenere la nidificazione a non più di dieci livelli.

### Numero di campi e tipi di dati per modello {#number-of-data-fields-and-types-per-model}

Includi solo i campi di dati e i tipi di dati necessari per un modello.

Modelli eccessivamente complessi portano a frammenti eccessivamente complessi che possono rendere difficile l’authoring e ridurre le prestazioni dell’editor.

### Campi Rich Text {#rich-text-fields}

Utilizza i campi Rich Text (il tipo di dati **Testo su più righe**) in considerazione.

Limita il numero di campi Rich Text per modello. Inoltre, indica la quantità di testo memorizzata in ciascun frammento e la quantità di formattazione di HTML. Contenuti Rich Text di grandi dimensioni possono influire negativamente sulle prestazioni del sistema.

### Numero di varianti {#number-of-variations}

Crea tutte le varianti di frammento necessarie, ma non più.

Le varianti aggiungono tempo di elaborazione a un frammento di contenuto, nell’ambiente di authoring e alla consegna. Si consiglia di mantenere il numero di varianti al minimo gestibile.

Si consiglia di non superare le dieci varianti per frammento di contenuto.

### Test prima della produzione {#test-before-production}

In caso di dubbi, crea un prototipo delle strutture di contenuto previste prima di implementarle in produzione. Una verifica precoce dei concetti, unita a test adeguati, sia tecnici che di accettazione da parte dell’utente, può aiutare a evitare problemi in un secondo momento, quando si dovranno affrontare le scadenze di produzione.