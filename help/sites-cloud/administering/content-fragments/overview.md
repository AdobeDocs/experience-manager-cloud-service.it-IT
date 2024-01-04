---
title: Panoramica sull’utilizzo dei frammenti di contenuto
description: Scopri come i frammenti di contenuto in AEM as a Cloud Service ti consentono di creare e utilizzare contenuti; ideali per la distribuzione headless e l’authoring delle pagine.
feature: Content Fragments
role: User, Developer, Architect
exl-id: ce9cb811-57d2-4a57-a360-f56e07df1b1a
source-git-commit: 19685cb952a890731bd7d75a2adf3cfd841a465f
workflow-type: tm+mt
source-wordcount: '1792'
ht-degree: 39%

---

# Panoramica sull’utilizzo dei frammenti di contenuto {#overview-working-with-content-fragments}

Con Adobe Experience Manager (AEM) as a Cloud Service, i frammenti di contenuto consentono di progettare, creare, curare e [pubblicare contenuti indipendenti dalla pagina](/help/sites-cloud/authoring/fundamentals/content-fragments.md). Consentono di preparare contenuti pronti per l’uso in più posizioni e su più canali, ideali per la distribuzione headless e l’authoring delle pagine.

>[!IMPORTANT]
>
>I frammenti di contenuto sono accessibili da due console: **Frammenti di contenuto** e **Risorse**.
>
>Sono inoltre disponibili due editor per i frammenti di contenuto. Entrambi gli editor sono accessibili da entrambe le console.
>
>Questa sezione tratta della **Frammenti di contenuto** e *nuovo* Editor frammento di contenuto. Questi sono stati sviluppati per la distribuzione di contenuti headless (anche se possono essere utilizzati in tutti gli scenari)
>
>Per ulteriori informazioni, consulta:
>
>* l&#39;uso del **Risorse** console per [gestione dei frammenti di contenuto](/help/assets/content-fragments/content-fragments-managing.md)
>* l&#39;uso del [*originale* Editor frammento di contenuto](/help/assets/content-fragments/content-fragments-variations.md),
>* utilizzo [Frammenti di contenuto per l’authoring delle pagine](/help/sites-cloud/authoring/fundamentals/content-fragments.md).


I frammenti di contenuto contengono contenuto strutturato:

* Ogni frammento è basato su un [Modello per frammenti di contenuto](/help/sites-cloud/administering/content-fragments/content-fragment-models.md).
   * Il modello per frammenti di contenuto definisce la struttura del frammento risultante.
* Ogni frammento è costituito da:
   * **[Principale](#main-and-variations)** - parte integrante del frammento che contiene il contenuto principale; esiste sempre, non può essere eliminato
   * **[Varianti](#main-and-variations)** - una o più permutazioni del contenuto, create dall’autore
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

I frammenti di contenuto possono essere consegnati anche in formato JSON, utilizzando le funzionalità di esportazione Sling Model (JSON) dei componenti core dell’AEM. Questo tipo di consegna:

* consente di utilizzare il componente per gestire gli elementi di un frammento da consegnare;
* consente la consegna in blocco; aggiungendo più [Componenti core Frammento di contenuto](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/content-fragment-component.html?lang=it) sulla pagina utilizzata per la consegna API

Il numero di canali di comunicazione aumenta ogni anno. In genere i canali si distinguono in base al meccanismo di consegna, come segue:

* Canale fisico; ad esempio, desktop, dispositivi mobili.
* Forma di consegna in un canale fisico, ad esempio “pagina dei dettagli di un prodotto”, “pagina della categoria del prodotto” per desktop oppure “web mobile”, “app mobile” per dispositivi mobili.

Tuttavia, probabilmente non vorrai utilizzare *esatto* stessi contenuti per tutti i canali: è necessario ottimizzare i contenuti in base al canale specifico.

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
>I **frammenti di contenuto** e i **[frammenti di esperienza](/help/sites-cloud/authoring/fundamentals/experience-fragments.md)** sono funzioni diverse in AEM:
>* I **frammenti di contenuto** sono contenuti editoriali, con definizione e struttura, ma senza elementi visivi aggiuntivi di design e/o layout. Possono essere utilizzati per accedere a dati strutturati, tra cui testi, numeri e date.
>* I **frammenti di esperienza** sono contenuti completi di layout, frammenti di una pagina web.
>
>I frammenti esperienza possono includere contenuti sotto forma di frammenti di contenuto, ma non viceversa.
>
>Per ulteriori informazioni, consulta [Frammenti di contenuto e frammenti di esperienza nell’AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/content-fragments/understand-content-fragments-and-experience-fragments.html?lang=it#content-fragments).

Questa pagina e quelle seguenti descrivono le attività di creazione, configurazione, manutenzione e utilizzo dei frammenti di contenuto:

* [Abilita funzionalità frammento di contenuto per la tua istanza](/help/sites-cloud/administering/content-fragments/setup.md)
* [Modelli per frammenti di contenuto](/help/sites-cloud/administering/content-fragments/content-fragment-models.md) : abilitazione, creazione e definizione dei modelli
* [Creare frammenti di contenuto](/help/sites-cloud/administering/content-fragments/managing.md#creating-a-content-fragment) (utilizzando la Console Frammenti di contenuto)

Dopo la creazione dei frammenti, puoi:

* [Utilizzare la console Frammenti di contenuto](/help/sites-cloud/administering/content-fragments/managing.md) : accesso, pubblicazione (anteprima o produzione) e riferimento ai frammenti
* [Utilizzare l’editor di frammenti di contenuto](/help/sites-cloud/administering/content-fragments/authoring.md) : per modificare, pubblicare (anteprima o produzione) e fare riferimento ai frammenti
* [Analizza](/help/sites-cloud/administering/content-fragments/analysis.md)  la struttura del frammento di contenuto, utilizzando l’editor
* [Accedi ai frammenti con GraphQL per la distribuzione headless nelle applicazioni](/help/sites-cloud/administering/content-fragments/content-delivery-with-graphql.md).
* [Oppure utilizza i tuoi frammenti per creare le pagine](/help/sites-cloud/authoring/fundamentals/content-fragments.md)

>[!NOTE]
>
>Queste pagine possono essere lette insieme a:
>
>* [Personalizzazione ed estensione dei frammenti di contenuto](/help/implementing/developing/extending/content-fragments-customizing.md)
>* [Componenti di configurazione dei frammenti di contenuto per il rendering](/help/implementing/developing/extending/content-fragments-configuring-components-rendering.md)
>* [Supporto dei frammenti di contenuto nell’API HTTP di AEM Assets](/help/assets/content-fragments/assets-api-content-fragments.md)
>* [API GraphQL di AEM per l’utilizzo con Frammenti di contenuto](/help/headless/graphql-api/content-fragments.md)
>* [Authoring delle pagine con frammenti di contenuto](/help/sites-cloud/authoring/fundamentals/content-fragments.md).

## Principale e varianti {#main-and-variations}

Le varianti sono una caratteristica significativa dei frammenti di contenuto dell’AEM. Consentono di creare e modificare copie del **Principale** contenuti da utilizzare su canali e scenari specifici, per rendere ancora più flessibili la distribuzione di contenuti headless e l’authoring delle pagine.

* **Principale**

   * **Principale** non è una variante in sé, ma è la base di tutte le varianti.
   * Parte integrante del frammento

      * Ogni frammento di contenuto ha un’istanza di **Principale**.
      * **Principale** non può essere eliminato.

   * **Principale** è accessibile nell’editor frammento in **[Varianti](/help/sites-cloud/administering/content-fragments/authoring.md#variations)**.

  >[!NOTE]
  >
  >Nell’editor disponibile da **Risorse** console, **Principale** è etichettato come **Principale**.

* **Varianti**

   * Sono rappresentazioni di testo dei frammenti a scopo editoriale; possono essere relative a un canale ma non necessariamente, e possono anche essere utilizzate per modifiche locali ad hoc.
   * Sono create come copie di **Principale**, ma possono essere modificati in base alle esigenze; spesso c’è una sovrapposizione di contenuti tra le varianti stesse.
   * Può essere definito durante la creazione del frammento, dal pannello a sinistra.
   * Sono memorizzate nel frammento, per evitare la dispersione delle copie del contenuto.
   * Le varianti possono essere [confronto e sincronizzazione](/help/sites-cloud/administering/content-fragments/authoring.md#compare-and-synchronize-rich-text) con **Principale**.
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

I frammenti di contenuto di AEM possono essere utilizzati per descrivere e gestire contenuti strutturati. Il contenuto strutturato è definito in modelli che possono contenere diversi tipi di contenuto, compresi testo, dati numerici, dati booleani, data e ora e altro ancora.

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

   * I frammenti di contenuto (e le relative varianti) possono essere creati e manutenuti dalla sezione [Console Frammenti di contenuto](/help/sites-cloud/administering/content-fragments/managing.md#content-fragments-console).
   * Creato e modificato in [Editor frammento di contenuto](/help/sites-cloud/administering/content-fragments/authoring.md).

* Accessibile per la distribuzione dei contenuti tramite [API GRAPHQL AEM](/help/headless/graphql-api/content-fragments.md).

* Disponibile in [Editor pagina utilizzando il componente Frammento di contenuto](/help/sites-cloud/authoring/fundamentals/content-fragments.md) (componente di riferimento):

   * Il [Componente core Frammento di contenuto](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/content-fragment-component.html?lang=it) è disponibile per gli autori di pagine. Consente loro di fare riferimento e distribuire il frammento di contenuto richiesto in formato HTML o JSON.

I frammenti di contenuto sono una struttura di contenuto che:

* Sono privi di layout o progettazione (la formattazione del testo è possibile per i campi di testo).
* È indipendente dal meccanismo di consegna (ad esempio la pagina o il canale).
* contiene una o più [parti costituenti](#constituent-parts-of-a-content-fragment);
* può [contenere immagini o essere connessa ad esse](#fragments-with-visual-assets);

### Frammenti con risorse visive {#fragments-with-visual-assets}

Per dare agli autori un maggiore controllo sui contenuti, le immagini possono essere aggiunte a e/o integrate con un frammento di contenuto.

Le risorse possono essere utilizzate con un frammento di contenuto in diversi modi, ciascuno con i propri vantaggi:

* as a **Riferimento contenuto**
* entro un **Testo su più righe** campo

### Parti costitutive di un frammento di contenuto {#constituent-parts-of-a-content-fragment}

Le risorse dei frammenti di contenuto sono composte dalle seguenti parti (direttamente o indirettamente):

* **Elementi del frammento**

   * Gli elementi sono correlati ai campi di dati che contengono il contenuto.
   * Utilizzi un [Modello per frammenti di contenuto](/help/sites-cloud/administering/content-fragments/content-fragment-models.md) per creare il frammento di contenuto. Gli elementi (campi) specificati nel modello definiscono la struttura del frammento. Questi elementi (campi) possono essere di diversi tipi di dati.

* **Paragrafi del frammento**

   * Blocchi di testo, spesso con più righe, delimitati come singole entità.

   * Consentono di controllare i contenuti durante l’authoring delle pagine.

* **Metadati del frammento**

   * Utilizzano gli [schemi di metadati delle risorse](/help/assets/metadata-schemas.md).
   * È possibile creare i tag quando:

      * si crea e si effettua l’authoring del frammento;
      * O più tardi, quando [visualizzare o modificare le proprietà](/help/sites-cloud/administering/content-fragments/authoring.md#view-properties-tags) nell’editor frammento

  >[!CAUTION]
  >
  >I profili di elaborazione dei metadati non sono applicabili ai frammenti di contenuto.

  >[!CAUTION]
  >
  >Spesso un modello per frammenti di contenuto può definire campi di dati denominati **Titolo** e **Descrizione**. Se questi due campi esistono, sono campi definiti dall’utente e possono essere aggiornati nell’area del contenuto dell’editor.
  >
  >Il frammento di contenuto e le relative varianti dispongono anche di campi di metadati (proprietà) denominati **Titolo** e **Descrizione**. Questi due campi di metadati sono parte integrante di qualsiasi frammento di contenuto e variante e sono inizialmente definiti al momento della creazione del frammento. Possono essere aggiornati nell’area proprietà/metadati dell’editor.

* **[Principale](#main-and-variations)**
* **[Varianti](#main-and-variations)**

### Elementi necessari per i frammenti {#required-by-fragments}

Per creare frammenti di contenuto sono necessari i seguenti elementi:

* **Modello di contenuto**

   * Viene [abilitato tramite il Browser configurazioni](/help/sites-cloud/administering/content-fragments/setup.md).
   * Viene [creato utilizzando gli strumenti](/help/sites-cloud/administering/content-fragments/content-fragment-models.md).
   * È necessario per [creare un frammento](/help/sites-cloud/administering/content-fragments/managing.md#creating-content-fragments).
   * Definisce la struttura di un frammento (titolo, elementi di contenuto, definizioni tag).
   * Le definizioni del modello per frammenti di contenuto richiedono un titolo e un elemento dati; tutto il resto è facoltativo.
   * Il modello può definire eventuale contenuto predefinito.
   * Gli autori non possono modificare la struttura definita durante l’authoring del contenuto di un frammento, anche se possono aprire l’editor modelli dall’editor frammenti.
   * Le modifiche apportate a un modello dopo la creazione dei frammenti di contenuto dipendenti possono influire su tali frammenti di contenuto.

Per utilizzare i frammenti di contenuto per la distribuzione di contenuti headless è inoltre necessario:

* a [Query GraphQL](/help/headless/graphql-api/content-fragments.md) per richiedere il contenuto richiesto
* questo contenuto può quindi essere utilizzato per sviluppare il proprio SPA per l’AEM; per ulteriori informazioni, consulta i seguenti documenti:

   * [Tutorial WKND per SPA](/help/implementing/developing/hybrid/wknd-tutorial.md)
   * [Guida introduttiva all’utilizzo di React](/help/implementing/developing/hybrid/getting-started-react.md)
   * [Guida introduttiva all’utilizzo di Angular](/help/implementing/developing/hybrid/getting-started-angular.md)

Per utilizzare i frammenti di contenuto nell’authoring delle pagine è inoltre necessario:

* A **Componente Frammento di contenuto**

   * Essenziale per la distribuzione del frammento in formato HTML e/o JSON.
   * Obbligatorio per [fare riferimento al frammento in una pagina](/help/sites-cloud/authoring/fundamentals/content-fragments.md).
   * Responsabile del layout e della distribuzione di un frammento, ad esempio i canali.
   * I frammenti devono disporre di uno o più componenti dedicati per definire il layout e fornire alcuni o tutti gli elementi/varianti e i contenuti associati.
   * Quando si trascina un frammento su una pagina durante l’authoring, il componente richiesto viene associato automaticamente.
   * Consulta la [Componente core Frammento di contenuto](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/content-fragment-component.html?lang=it).

## Esempio di utilizzo {#example-usage}

Un frammento, con i relativi elementi e varianti, può essere utilizzato per creare contenuti coerenti per più canali. Durante la progettazione del frammento è necessario considerare cosa verrà utilizzato e dove.

### Esempio WKND {#wknd-sample}

Il [Sito WKND e WKND condivisi](/help/implementing/developing/introduction/develop-wknd-tutorial.md) vengono forniti campioni per aiutarla a conoscere AEM as a Cloud Service.

<!-- CHECK: which links can/should be used these days? -->

Il progetto WKND include:

* Modelli di Frammento di contenuto disponibili in:

   * `.../libs/dam/cfm/models/console/content/models.html/conf/wknd`

   * `.../ui#/aem/libs/dam/cfm/models/console/content/models.html/conf/wknd-shared`

* Frammenti di contenuto (e altro contenuto) disponibili in:

   * `.../assets.html/content/dam/wknd/en`
