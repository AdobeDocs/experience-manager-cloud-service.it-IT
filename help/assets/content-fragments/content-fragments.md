---
title: Utilizzo di frammenti di contenuto
description: Scopri come i frammenti di contenuto in Adobe Experience Manager (AEM) as a Cloud Service consentono di progettare, creare, curare e utilizzare contenuti indipendenti dalla pagina, ideali per la distribuzione headless.
feature: Content Fragments
role: User
exl-id: db17eff1-4252-48d5-bb67-5e476e93ef7e
source-git-commit: e592dd7a3a717259493f23943933fe3d0e71b7ab
workflow-type: tm+mt
source-wordcount: '2033'
ht-degree: 6%

---

# Utilizzo di frammenti di contenuto {#working-with-content-fragments}

Con Adobe Experience Manager (AEM) as a Cloud Service, i frammenti di contenuto ti consentono di progettare, creare, curare e [pubblicare contenuti indipendenti dalla pagina](/help/sites-cloud/authoring/fundamentals/content-fragments.md) Consentono di preparare i contenuti pronti per l’uso in più posizioni/su più canali, ideale per la distribuzione headless.

I frammenti di contenuto contengono contenuto strutturato:

* Sono basati su un [Modello per frammento di contenuto](/help/assets/content-fragments/content-fragments-models.md), che predefinisce una struttura per il frammento risultante.
* La struttura può variare tra:
   * Base
      * Ad esempio, un singolo campo di testo su più righe.
      * Può essere utilizzato per preparare contenuti semplici da utilizzare nella creazione delle pagine.
   * Complesso
      * Combinazione di numerosi campi di tipi di dati diversi, tra cui testo, numero, booleano, dati e ora.
      * Può essere utilizzato per preparare contenuti più strutturati per l’authoring delle pagine o per la distribuzione all’applicazione.
   * Nidificato
      * I tipi di dati di riferimento disponibili consentono di nidificare il contenuto.
      * Tende a essere utilizzato per la consegna all’applicazione.

I frammenti di contenuto possono essere consegnati anche in formato JSON, utilizzando le funzionalità di esportazione Sling Model (JSON) dei componenti core AEM. Questo tipo di consegna:

* consente di utilizzare il componente per gestire gli elementi di un frammento da distribuire
* consente la distribuzione in blocco, aggiungendo più componenti core dei frammenti di contenuto nella pagina utilizzata per la distribuzione API

Nelle pagine seguenti sono illustrate le attività di creazione, configurazione, manutenzione e utilizzo dei frammenti di contenuto:

* [Abilita funzionalità frammento di contenuto per la tua istanza](/help/assets/content-fragments/content-fragments-configuration-browser.md)
* [Modelli per frammenti di contenuto](/help/assets/content-fragments/content-fragments-models.md) - abilitazione, creazione e definizione dei modelli
* [Gestione dei frammenti di contenuto](/help/assets/content-fragments/content-fragments-managing.md) - creare i frammenti di contenuto; quindi modifica, pubblica e fai riferimento a
* [Varianti - Authoring dei contenuti di frammenti](/help/assets/content-fragments/content-fragments-variations.md) - Creazione del contenuto del frammento e creazione di varianti del master
* [Markdown](/help/assets/content-fragments/content-fragments-markdown.md) - uso della sintassi markdown per il frammento
* [Utilizzo di contenuti associati](/help/assets/content-fragments/content-fragments-assoc-content.md) - aggiunta di contenuto associato
* [Metadati - Proprietà dei frammenti](/help/assets/content-fragments/content-fragments-metadata.md) - visualizzazione e modifica delle proprietà del frammento
* Utilizzo [Frammenti di contenuto, insieme a GraphQL, per distribuire contenuti](/help/assets/content-fragments/content-fragments-graphql.md) da utilizzare nelle applicazioni. Per facilitare questa fase, puoi visualizzare un’anteprima [Output JSON](/help/assets/content-fragments/content-fragments-json-preview.md).

>[!NOTE]
>
>Queste pagine possono essere lette insieme a:
>
>* [Authoring delle pagine con frammenti di contenuto](/help/sites-cloud/authoring/fundamentals/content-fragments.md).
>* [Personalizzazione ed estensione dei frammenti di contenuto](/help/implementing/developing/extending/content-fragments-customizing.md)
>* [Componenti di configurazione dei frammenti di contenuto per il rendering](/help/implementing/developing/extending/content-fragments-configuring-components-rendering.md)
>* [Supporto dei frammenti di contenuto nell’API HTTP di AEM Assets](/help/assets/content-fragments/assets-api-content-fragments.md)
>* [AEM API GraphQL per l’utilizzo con frammenti di contenuto](/help/headless/graphql-api/content-fragments.md)


Il numero di canali di comunicazione aumenta ogni anno. In genere i canali si riferiscono al meccanismo di consegna, come segue:

* canale fisico; ad esempio desktop, mobile.
* forma di consegna in un canale fisico; Ad esempio, &quot;pagina di dettaglio del prodotto&quot;, &quot;pagina di categoria del prodotto&quot; per desktop o &quot;web mobile&quot;, &quot;app mobile&quot; per dispositivi mobili.

Tuttavia, probabilmente non desideri utilizzare esattamente lo stesso contenuto per tutti i canali: è necessario ottimizzare il contenuto in base al canale specifico.

I frammenti di contenuto consentono di:

* Valuta come raggiungere in modo efficiente i tipi di pubblico target tra i vari canali.
* Crea e gestisci contenuti editoriali neutri per il canale.
* Crea pool di contenuti per una serie di canali.
* Progetta varianti di contenuto per canali specifici.
* Aggiungi le immagini al testo inserendo le risorse (frammenti con file multimediali diversi).
* Crea contenuti nidificati per riflettere la complessità dei dati.

Questi frammenti di contenuto possono quindi essere assemblati per fornire esperienze su diversi canali.

>[!NOTE]
>
>I **frammenti di contenuto** e i **[frammenti esperienza](/help/sites-cloud/authoring/fundamentals/experience-fragments.md)** sono funzioni diverse in AEM:
>* **Frammenti di contenuto** sono contenuti editoriali che possono essere utilizzati per accedere a dati strutturati, tra cui testi, numeri e date. Sono contenuti puri, con definizione e struttura, ma senza design e/o layout visivi aggiuntivi.
>* I **frammenti esperienza** sono contenuti con un layout completo, un frammento di una pagina Web.
>
>I frammenti esperienza possono includere contenuti sotto forma di frammenti di contenuto, ma non viceversa.
>
>Per ulteriori informazioni consulta anche [Frammenti di contenuto e frammenti di esperienza in AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/content-fragments/understand-content-fragments-and-experience-fragments.html#content-fragments).

## Frammenti di contenuto e servizi di contenuto {#content-fragments-and-content-services}

AEM Content Services è progettato per generalizzare la descrizione e la distribuzione dei contenuti in/da AEM oltre l’attenzione sulle pagine web.

Forniscono contenuti a canali che non sono pagine web AEM tradizionali, utilizzando metodi standardizzati utilizzabili da qualsiasi cliente. Questi canali possono includere:

* Applicazioni a pagina singola
* Applicazioni mobile native
* altri canali e punti di contatto esterni a AEM

La consegna viene effettuata in formato JSON utilizzando l’esportatore JSON.

I frammenti di contenuto AEM possono essere utilizzati per descrivere e gestire contenuti strutturati. Il contenuto strutturato è definito in modelli che possono contenere diversi tipi di contenuto; compresi testo, dati numerici, booleano, data e ora e altro ancora.

Insieme alle funzionalità di esportazione JSON dei componenti di base AEM, questo contenuto strutturato può quindi essere utilizzato per distribuire contenuti AEM a canali diversi dalle AEM pagine.

>[!NOTE]
>
>Vedi [Senza testa e AEM](/help/headless/introduction.md) per un’introduzione a Headless Development per AEM Sites as a Cloud Service.

>[!NOTE]
>
>AEM supporta anche la traduzione del contenuto del frammento.

>[!NOTE]
>
>AEM supporta anche la traduzione del contenuto del frammento. Vedi [Traduzione di risorse](/help/assets/translate-assets.md) per ulteriori informazioni.

## Tipo di contenuto {#content-type}

I frammenti di contenuto sono:

* Memorizzato come **Risorse**:

   * I frammenti di contenuto (e le relative varianti) possono essere creati e mantenuti dal **Risorse** console.
   * Authoring e modifica nell’Editor frammento di contenuto.

* Utilizzato in [editor di pagine tramite il componente Frammento di contenuto](/help/sites-cloud/authoring/fundamentals/content-fragments.md) (componente di riferimento):

   * La **Frammento di contenuto** Il componente è disponibile per gli autori delle pagine. Consente loro di fare riferimento e distribuire il frammento di contenuto richiesto in formato HTML o JSON.

* Accessibile tramite [AEM API GraphQL](/help/headless/graphql-api/content-fragments.md).

I frammenti di contenuto sono una struttura di contenuto che:

* Sono prive di layout o design (in modalità RTF è possibile formattare del testo).
* Contenere uno o più [parti costituenti](#constituent-parts-of-a-content-fragment).
* Can [contenere immagini o essere connessi ad esse](#fragments-with-visual-assets).
* Può utilizzare [contenuto intermedio](#in-between-content-when-page-authoring-with-content-fragments) se a cui si fa riferimento in una pagina.

* Sono indipendenti dal meccanismo di consegna (ad esempio, pagina, canale).

### Frammenti con risorse visive {#fragments-with-visual-assets}

Per dare agli autori un maggiore controllo sui contenuti, le immagini possono essere aggiunte a e/o integrate con un frammento di contenuto.

Le risorse possono essere utilizzate con un frammento di contenuto in diversi modi; ciascuno con i propri vantaggi:

* **Inserisci risorsa** in un frammento (frammenti con file multimediali diversi)

   * Sono parte integrante del frammento (vedere [Parti costitutive di un frammento di contenuto](#constituent-parts-of-a-content-fragment)).
   * Definisci la posizione della risorsa.
   * Vedi [Inserimento di risorse nel frammento](/help/assets/content-fragments/content-fragments-variations.md#inserting-assets-into-your-fragment) nell’Editor frammento per ulteriori informazioni.

   >[!NOTE]
   >
   >Le risorse visive inserite nel frammento di contenuto stesso sono associate al paragrafo precedente. Quando il frammento viene aggiunto a una pagina, queste risorse vengono spostate in relazione a tale paragrafo quando viene aggiunto del contenuto intermedio.

* **Contenuto associato**

   * sono collegati a un frammento; ma non una parte fissa del frammento (vedere [Parti costitutive di un frammento di contenuto](#constituent-parts-of-a-content-fragment)).
   * Consente una certa flessibilità per il posizionamento.
   * Sono facilmente disponibili per l’uso (come nel contenuto intermedio) quando si utilizza il frammento su una pagina.
   * Vedi [Contenuto associato](/help/assets/content-fragments/content-fragments-assoc-content.md) per ulteriori informazioni.

* Risorse disponibili nel **browser Risorse** dell’editor pagina

   * Consenti flessibilità completa per la selezione di una risorsa.
   * Consente una certa flessibilità per il posizionamento.
   * Non fornisce il concetto di approvazione per un frammento specifico.
   * Vedi [Browser Risorse](/help/sites-cloud/authoring/fundamentals/environment-tools.md#assets-browser) per ulteriori informazioni.

### Parti costitutive di un frammento di contenuto {#constituent-parts-of-a-content-fragment}

Le risorse dei frammenti di contenuto sono composte dalle seguenti parti (direttamente o indirettamente):

* **Elementi frammento**

   * Gli elementi sono correlati ai campi di dati che contengono contenuto.
   * Puoi utilizzare un modello di contenuto per creare il frammento di contenuto. Gli elementi (campi) specificati nel modello definiscono la struttura del frammento. Questi elementi (campi) possono essere di diversi tipi di dati.

* **Paragrafi frammento**

   * Blocchi di testo, spesso con più righe, delimitati come singole entità.

   * Nelle modalità [Rich Text](/help/assets/content-fragments/content-fragments-variations.md#rich-text) e [Markdown](/help/assets/content-fragments/content-fragments-variations.md#markdown), un paragrafo può essere formattato come intestazione, in tal caso appartiene a un’unica unità insieme al paragrafo seguente.

   * Abilita il controllo dei contenuti durante la creazione delle pagine.

* **Risorse inserite in un frammento (frammenti di file multimediali diversi)**

   * Risorse (immagini) inserite nel frammento effettivo e utilizzate come contenuto interno di un frammento.
   * Sono incorporati nel sistema paragrafo del frammento.
   * Può essere formattato quando [frammento utilizzato/a cui si fa riferimento in una pagina](/help/sites-cloud/authoring/fundamentals/content-fragments.md).
   * È possibile aggiungere, eliminare o spostare solo all’interno di un frammento utilizzando l’editor frammenti. Queste azioni non possono essere eseguite nell’editor pagina.
   * È possibile aggiungere, eliminare o spostare solo all’interno di un frammento utilizzando [Formato RTF nell’editor frammento](/help/assets/content-fragments/content-fragments-variations.md#inserting-assets-into-your-fragment).
   * Può essere aggiunto solo a elementi di testo su più righe (qualsiasi tipo di frammento).
   * sono allegati al testo precedente (paragrafo).

      >[!CAUTION]
      >
      >Le risorse possono essere rimosse (inavvertitamente) da un frammento passando al formato Testo normale.

      >[!NOTE]
      >
      >È inoltre possibile aggiungere le risorse come [contenuto aggiuntivo (intermedio)](/help/sites-cloud/authoring/fundamentals/content-fragments.md#using-associated-content) quando si utilizza un frammento su una pagina; utilizzando Contenuto associato o risorse dal browser Risorse.

* **Contenuto associato**

   * Si tratta di contenuti esterni a un frammento, ma con rilevanza editoriale per esso. In genere immagini, video o altri frammenti.
   * Le singole risorse all’interno della raccolta sono disponibili per l’utilizzo con il frammento nell’editor di pagine quando viene aggiunto a una pagina. Ciò significa che sono opzionali, a seconda dei requisiti del canale specifico.
   * Le risorse sono [associati a frammenti tramite raccolte](/help/assets/content-fragments/content-fragments-assoc-content.md); le raccolte associate consentono all’autore di decidere quali risorse utilizzare durante la creazione della pagina.

      * Le raccolte possono essere associate ai frammenti come contenuto predefinito o dagli autori durante la creazione dei frammenti.
      * [Raccolte di risorse (DAM)](/help/assets/manage-collections.md) sono la base del contenuto associato dei frammenti.
   * Facoltativamente, puoi anche aggiungere il frammento stesso a una raccolta per facilitare il tracciamento.

* **Metadati frammento**

   * Utilizza la [Schemi di metadati delle risorse](/help/assets/metadata-schemas.md).
   * I tag possono essere creati quando:

      * Creare e creare il frammento
      * O successivo:

         * Visualizzazione/modifica del frammento **Proprietà** dalla console
         * Modificando il **Metadati** nell’editor frammenti

   >[!CAUTION]
   >
   >I profili di elaborazione dei metadati non si applicano ai frammenti di contenuto.

* **Principale**

   * Parte integrante del frammento

      * Ogni frammento di contenuto dispone di un’istanza di Master.
      * Impossibile eliminare il master.
   * Master è accessibile nell’editor frammenti in **[Variazioni](/help/assets/content-fragments/content-fragments-variations.md)**.
   * Master non è una variazione in quanto tale, ma è la base di tutte le variazioni.


* **Varianti**

   * rappresentazioni di testo di frammento specifiche per scopi editoriali; può essere correlato al canale ma non è obbligatorio, può anche essere per modifiche locali ad hoc.
   * Sono create come copie di **Master**, ma può essere modificato come necessario; di solito c&#39;è una sovrapposizione dei contenuti tra le varianti stesse.
   * Può essere definito durante la creazione dei frammenti.
   * Memorizzato nel frammento, per evitare la dispersione delle copie del contenuto.
   * Le varianti possono essere [sincronizzato](/help/assets/content-fragments/content-fragments-variations.md#synchronizing-with-master) con Master se il contenuto principale è stato aggiornato.
   * Può essere [Riepilogo](/help/assets/content-fragments/content-fragments-variations.md#summarizing-text) per troncare rapidamente il testo a una lunghezza predefinita.
   * Disponibile sotto [Variazioni](/help/assets/content-fragments/content-fragments-variations.md) scheda dell’editor frammenti.

### Contenuto intermedio durante l’authoring della pagina con frammenti di contenuto {#in-between-content-when-page-authoring-with-content-fragments}

Contenuto intermedio:

* È disponibile per l’utilizzo nell’Editor pagina quando si lavora con Frammenti di contenuto.
* Is [contenuto aggiuntivo aggiunto all’interno del flusso di un frammento](/help/sites-cloud/authoring/fundamentals/content-fragments.md#adding-in-between-content) una volta utilizzato/a come riferimento in una pagina.
* È disponibile per l’utilizzo in [Editor pagina quando si lavora con frammenti di contenuto](/help/sites-cloud/authoring/fundamentals/content-fragments.md).
* Il contenuto intermedio può essere aggiunto a qualsiasi frammento, in cui è visibile un solo elemento.
* È possibile utilizzare il contenuto associato, così come le risorse e/o i componenti dal browser appropriato.

>[!CAUTION]
>
>Il contenuto intermedio è contento di pagina. Non viene memorizzato nel frammento di contenuto.

### Obbligatorio per frammenti {#required-by-fragments}

Per creare frammenti di contenuto è necessario:

* **Modello di contenuto**

   * Sono [abilitato tramite il browser di configurazione](/help/assets/content-fragments/content-fragments-configuration-browser.md).
   * Sono [creato con Strumenti](/help/assets/content-fragments/content-fragments-models.md).
   * Obbligatorio per [creare un frammento](/help/assets/content-fragments/content-fragments-managing.md#creating-content-fragments).
   * Definisce la struttura di un frammento (titolo, elementi di contenuto, definizioni di tag).
   * Le definizioni dei modelli di contenuto richiedono un titolo e un elemento dati; tutto il resto è facoltativo.
   * Il modello può definire il contenuto predefinito, se applicabile.
   * Gli autori non possono modificare la struttura definita durante la creazione del contenuto di un frammento.
   * Le modifiche apportate a un modello dopo la creazione dei frammenti di contenuto dipendenti possono influire su tali frammenti di contenuto.

Per utilizzare i frammenti di contenuto per l’authoring delle pagine è inoltre necessario:

* **Componente Frammento di contenuto**

   * Strumentale per la distribuzione del frammento in formato HTML e/o JSON.
   * Obbligatorio per [fare riferimento al frammento in una pagina](/help/sites-cloud/authoring/fundamentals/content-fragments.md).
   * Responsabile del layout e della consegna di un frammento; ovvero canali.
   * I frammenti devono disporre di uno o più componenti dedicati per definire il layout e fornire alcuni o tutti gli elementi/varianti e i contenuti associati.
   * Quando si trascina un frammento su una pagina in fase di creazione, il componente richiesto viene associato automaticamente.

## Utilizzo di esempio {#example-usage}

Un frammento, con i relativi elementi e varianti, può essere utilizzato per creare contenuti coerenti per più canali. Durante la progettazione del frammento è necessario considerare gli elementi da utilizzare in che punto.

### Esempio WKND {#wknd-sample}

La [Sito WKND](/help/implementing/developing/introduction/develop-wknd-tutorial.md) vengono forniti esempi per conoscere AEM as a Cloud Service.

Il progetto WKND include:

* Modelli per frammenti di contenuto disponibili in:
   `http://<hostname>:<port>/libs/dam/cfm/models/console/content/models.html/conf/wknd`

* Frammenti di contenuto (e altro contenuto) disponibili in:
   `http://<hostname>:<port>/assets.html/content/dam/wknd/en`
