---
title: Utilizzo di frammenti di contenuto
description: Scoprite come i frammenti di contenuto in Adobe Experience Manager (AEM) come Cloud Service consentono di progettare, creare, curare e utilizzare contenuti indipendenti dalla pagina.
translation-type: tm+mt
source-git-commit: 468d6f6a87c9a4794d5187146f7d879433cafa6f
workflow-type: tm+mt
source-wordcount: '1997'
ht-degree: 6%

---


# Utilizzo di frammenti di contenuto{#working-with-content-fragments}

<!--
>[!CAUTION]
>
>Certain features for Content Fragments will be released in early 2021.
>
>The related documentation is already available for preview purposes.
>
>Please see the [Release Notes](/help/release-notes/release-notes-cloud/release-notes-current.md) for further details.
-->

>[!CAUTION]
>
>L&#39;API AEM GraphQL, per la distribuzione dei frammenti di contenuto, verrà rilasciata all&#39;inizio del 2021.
>
>La documentazione correlata è già disponibile a scopo di anteprima.

Con Adobe Experience Manager (AEM) come Cloud Service, i frammenti di contenuto consentono di progettare, creare, curare e [pubblicare contenuti indipendenti dalla pagina](/help/sites-cloud/authoring/fundamentals/content-fragments.md). Consentono di preparare i contenuti pronti per l’uso in più posizioni/su più canali.

I frammenti di contenuto contengono contenuto strutturato:

* Si basano su un [modello di frammento di contenuto](/help/assets/content-fragments/content-fragments-models.md) che preimposta una struttura per il frammento risultante.
* La struttura può essere compresa tra:
   * Base
      * Ad esempio, un singolo campo di testo su più righe.
      * Può essere utilizzato per preparare contenuti semplici da usare nell’authoring delle pagine.
   * Complesso
      * Combinazione di numerosi campi con diversi tipi di dati, tra cui testo, numero, valore booleano, dati e ora.
      * Può essere utilizzato per preparare contenuti più strutturati per l’authoring delle pagine o per la distribuzione all’applicazione.

<!--
  * Nested
    * The reference data types available allow you to nest your content.
    * Tends to be used for delivery to your application.
-->

I frammenti di contenuto possono essere consegnati anche in formato JSON, utilizzando le funzionalità di esportazione JSON (Sling Model) dei componenti core di AEM. Questo modulo di consegna:

* consente di utilizzare il componente per gestire gli elementi di un frammento da distribuire
* consente la distribuzione in blocco, mediante l&#39;aggiunta di più componenti core di frammenti di contenuto nella pagina utilizzata per la distribuzione API

In questa e nelle pagine seguenti sono illustrate le attività di creazione, configurazione, manutenzione e utilizzo dei frammenti di contenuto:

* [Abilitare la funzionalità frammento di contenuto per l’istanza](/help/assets/content-fragments/content-fragments-configuration-browser.md)
* [Modelli](/help/assets/content-fragments/content-fragments-models.md)  di frammenti di contenuto - attivazione, creazione e definizione dei modelli
* [Gestione dei frammenti](/help/assets/content-fragments/content-fragments-managing.md)  di contenuto: creazione dei frammenti di contenuto; quindi modifica, pubblicazione e riferimento
* [Variazioni - Creazione di contenuti](/help/assets/content-fragments/content-fragments-variations.md)  di frammento - Creazione di contenuti di frammento e creazione di varianti del contenuto principale
* [Markdown](/help/assets/content-fragments/content-fragments-markdown.md) : utilizzo della sintassi di marketing per il frammento
* [Utilizzo del contenuto](/help/assets/content-fragments/content-fragments-assoc-content.md)  associato - aggiunta del contenuto associato
* [Metadati - Proprietà](/help/assets/content-fragments/content-fragments-metadata.md)  frammento - visualizzazione e modifica delle proprietà del frammento
* Utilizzate [Frammenti di contenuto, insieme a GraphQL, per distribuire contenuti](/help/assets/content-fragments/content-fragments-graphql.md) da utilizzare nelle applicazioni. A questo scopo, è possibile visualizzare in anteprima l&#39;output [JSON](/help/assets/content-fragments/content-fragments-json-preview.md).

>[!NOTE]
>
>Queste pagine possono essere lette insieme a:
>
>* [Authoring delle pagine con frammenti di contenuto](/help/sites-cloud/authoring/fundamentals/content-fragments.md).
>* [Personalizzazione ed estensione dei frammenti di contenuto](/help/implementing/developing/extending/content-fragments-customizing.md)
>* [Componenti di configurazione dei frammenti di contenuto per il rendering](/help/implementing/developing/extending/content-fragments-configuring-components-rendering.md)
>* [Supporto dei frammenti di contenuto nell’API HTTP di AEM Assets](/help/assets/content-fragments/assets-api-content-fragments.md)
>* [AEM GraphQL API per l&#39;utilizzo con frammenti di contenuto](/help/assets/content-fragments/graphql-api-content-fragments.md)


Il numero di canali di comunicazione aumenta ogni anno. In genere i canali fanno riferimento al meccanismo di consegna, come:

* canale fisico; ad esempio desktop, mobile.
* forma di consegna in un canale fisico; ad esempio &quot;pagina di dettaglio del prodotto&quot;, &quot;pagina di categoria del prodotto&quot; per desktop o &quot;web mobile&quot;, &quot;app mobile&quot; per dispositivi mobili.

Tuttavia, è probabile che non desideriate utilizzare esattamente lo stesso contenuto per tutti i canali; è necessario ottimizzare il contenuto in base al canale specifico.

I frammenti di contenuto consentono di:

* Considerate come raggiungere i tipi di pubblico target in modo efficiente tra i canali.
* Creazione e gestione di contenuti editoriali neutri per i canali.
* Creazione di pool di contenuti per una serie di canali.
* Progettare varianti di contenuto per canali specifici.
* Aggiungete immagini al testo inserendo risorse (frammenti multimediali diversi).

<!--
* Create nested content to reflect the complexity of your data.
-->

Questi frammenti di contenuto possono quindi essere assemblati per fornire esperienze su diversi canali.

>[!NOTE]
>
>I **frammenti di contenuto** e i **[frammenti esperienza](/help/sites-cloud/authoring/fundamentals/experience-fragments.md)** sono funzioni diverse in AEM:
>* **I** frammenti di contenuto sono contenuti editoriali che possono essere utilizzati per accedere ai dati strutturati, ad esempio testi, numeri e date. Sono contenuti puri, con definizione e struttura, ma senza design e/o layout visivi aggiuntivi.
>* I **frammenti esperienza** sono contenuti con un layout completo, un frammento di una pagina Web.

>
>
I frammenti esperienza possono includere contenuti sotto forma di frammenti di contenuto, ma non viceversa.
>
>Per ulteriori informazioni, vedere anche [Informazioni sui frammenti di contenuto e i frammenti esperienza in AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/content-fragments/understand-content-fragments-and-experience-fragments.html?lang=en#content-fragments).

## Frammenti di contenuto e servizi di contenuto {#content-fragments-and-content-services}

AEM Content Services è progettato per rendere più generalizzata la descrizione e la distribuzione dei contenuti in/da AEM oltre l&#39;attenzione sulle pagine Web.

Forniscono contenuti a canali che non sono pagine Web AEM tradizionali, utilizzando metodi standardizzati utilizzabili da qualsiasi cliente. Questi canali possono includere:

* Applicazioni a pagina singola
* Applicazioni mobili native
* altri canali e punti di contatto esterni a AEM

La consegna viene effettuata in formato JSON utilizzando JSON Exporter.

AEM Frammenti di contenuto possono essere utilizzati per descrivere e gestire il contenuto strutturato. Il contenuto strutturato è definito in modelli che possono contenere diversi tipi di contenuto; tra cui testo, dati numerici, booleani, data e ora e altro.

Insieme alle funzionalità di esportazione JSON AEM componenti core, questo contenuto strutturato può essere utilizzato per distribuire contenuti AEM a canali diversi da AEM pagine.

>[!NOTE]
>
>Per un&#39;introduzione a Headless Development per  AEM Sites come Cloud Service, vedere [Headless and AEM](/help/implementing/developing/headless/introduction.md).

>[!NOTE]
>
>AEM supporta anche la conversione del contenuto del frammento.

<!--
>[!NOTE]
>
>AEM also supports the translation of fragment content. See [Creating Translation Projects for Content Fragments](/help/assets/creating-translation-projects-for-content-fragments.md) for further information.
-->

## Tipo di contenuto {#content-type}

I frammenti di contenuto sono:

* Memorizzato come **Risorse**:

   * I frammenti di contenuto (e le relative varianti) possono essere creati e mantenuti dalla console **Risorse**.
   * Authored and modified in Content Fragment Editor (Modifica e modifica nell’Editor frammento di contenuto).

* Utilizzato nell&#39;editor di [pagine tramite il componente Frammento di contenuto](/help/sites-cloud/authoring/fundamentals/content-fragments.md) (componente di riferimento):

   * Il componente **Frammento di contenuto** è disponibile per gli autori di pagine. Consente loro di fare riferimento e distribuire il frammento di contenuto richiesto in formato HTML o JSON.

* Accessibile utilizzando l&#39;API [AEM GraphQL API](/help/assets/content-fragments/graphql-api-content-fragments.md).

I frammenti di contenuto sono una struttura di contenuto che:

* Sono privi di layout o di design (in modalità RTF è possibile formattare parte del testo).
* Contiene una o più parti [costituenti](#constituent-parts-of-a-content-fragment).
* Può [contenere o essere collegato a immagini](#fragments-with-visual-assets).
* Può utilizzare [contenuto intermedio](#in-between-content-when-page-authoring-with-content-fragments) quando viene fatto riferimento a una pagina.

* Sono indipendenti dal meccanismo di consegna (ad es. pagina, canale).

### Frammenti con risorse visive {#fragments-with-visual-assets}

Per dare agli autori un maggiore controllo sul contenuto, è possibile aggiungere e/o integrare immagini con un frammento di contenuto.

Le risorse possono essere utilizzate con un frammento di contenuto in diversi modi; ciascuno con i propri vantaggi:

* **Inserisci** risorsa in un frammento (frammenti di supporti misti)

   * Sono parte integrante del frammento (vedere [Parti costitutive di un frammento di contenuto](#constituent-parts-of-a-content-fragment)).
   * Definite la posizione della risorsa.
   * Per ulteriori informazioni, vedere [Inserimento di risorse nel frammento](/help/assets/content-fragments/content-fragments-variations.md#inserting-assets-into-your-fragment) nell&#39;Editor frammento.

   >[!NOTE]
   >
   >Le risorse visive inserite nel frammento di contenuto stesso sono associate al paragrafo precedente. Quando il frammento viene aggiunto a una pagina, queste risorse vengono spostate in relazione a tale paragrafo quando viene aggiunto del contenuto intermedio.

* **Contenuto associato**

   * sono connessi a un frammento; ma non una parte fissa del frammento (vedere [Parti costitutive di un frammento di contenuto](#constituent-parts-of-a-content-fragment)).
   * Consente una certa flessibilità per il posizionamento.
   * Sono facilmente utilizzabili (come contenuto intermedio) quando si utilizza il frammento su una pagina.
   * Per ulteriori informazioni, vedere [Contenuto associato](/help/assets/content-fragments/content-fragments-assoc-content.md).

* Risorse disponibili nel **browser Risorse** dell’editor pagina

   * Consente la flessibilità totale per la selezione di una risorsa.
   * Consente una certa flessibilità per il posizionamento.
   * Non fornisce il concetto di approvazione per un frammento specifico.
   * Per ulteriori informazioni, vedere [Browser risorse](/help/sites-cloud/authoring/fundamentals/environment-tools.md#assets-browser).

### Parti costitutive di un frammento di contenuto {#constituent-parts-of-a-content-fragment}

Le risorse dei frammenti di contenuto sono composte dalle seguenti parti (direttamente o indirettamente):

* **Elementi frammento**

   * Gli elementi sono correlati ai campi di dati che contengono contenuto.
   * È possibile utilizzare un modello di contenuto per creare il frammento di contenuto. Gli elementi (campi) specificati nel modello definiscono la struttura del frammento. Questi elementi (campi) possono essere di diversi tipi di dati.

* **Paragrafi frammento**

   * Blocchi di testo, spesso a più righe, delimitati come singole entità.

   * Nelle modalità [Rich Text](/help/assets/content-fragments/content-fragments-variations.md#rich-text) e [Markdown](/help/assets/content-fragments/content-fragments-variations.md#markdown), un paragrafo può essere formattato come intestazione, in tal caso appartiene a un’unica unità insieme al paragrafo seguente.

   * Attiva il controllo del contenuto durante l’authoring delle pagine.

* **Risorse inserite in un frammento (frammenti di file multimediali diversi)**

   * Risorse (immagini) inserite nel frammento effettivo e utilizzate come contenuto interno di un frammento.
   * Sono incorporati nel sistema paragrafo del frammento.
   * Può essere formattato quando il frammento [viene utilizzato/a cui viene fatto riferimento in una pagina](/help/sites-cloud/authoring/fundamentals/content-fragments.md).
   * È possibile aggiungere, eliminare o spostare solo all&#39;interno di un frammento utilizzando l&#39;Editor frammento. Queste azioni non possono essere effettuate nell’editor pagina.
   * È possibile aggiungere, eliminare o spostare solo all&#39;interno di un frammento utilizzando il formato [RTF nell&#39;editor frammenti](/help/assets/content-fragments/content-fragments-variations.md#inserting-assets-into-your-fragment).
   * Può essere aggiunto solo a elementi di testo con più righe (qualsiasi tipo di frammento).
   * Sono allegati al testo precedente (paragrafo).

      >[!CAUTION]
      >
      >Le risorse possono essere (inavvertitamente) rimosse da un frammento passando al formato Testo normale.

      >[!NOTE]
      >
      >Le risorse possono essere aggiunte anche come contenuto aggiuntivo [intermedio](/help/sites-cloud/authoring/fundamentals/content-fragments.md#using-associated-content) quando si utilizza un frammento in una pagina; utilizzando Contenuto associato o risorse dal browser Risorse.

* **Contenuto associato**

   * Si tratta di contenuto esterno a un frammento ma con rilevanza editoriale. In genere, immagini, video o altri frammenti.
   * Le singole risorse all&#39;interno della raccolta possono essere utilizzate con il frammento nell&#39;Editor pagina, quando viene aggiunto a una pagina. Ciò significa che sono opzionali, a seconda dei requisiti del canale specifico.
   * Le risorse sono [associate ai frammenti tramite raccolte](/help/assets/content-fragments/content-fragments-assoc-content.md); le raccolte associate consentono all&#39;autore di decidere quali risorse utilizzare al momento della creazione della pagina.

      * Le raccolte possono essere associate ai frammenti come contenuto predefinito oppure dagli autori durante l&#39;authoring dei frammenti.
      * [Le ](/help/assets/manage-collections.md) raccolte risorse (DAM) sono la base per il contenuto associato dei frammenti.
   * Facoltativamente, è anche possibile aggiungere il frammento stesso a una raccolta per facilitare il tracciamento.

* **Metadati frammento**

   * Utilizzare gli schemi di metadati [Risorse](/help/assets/metadata-schemas.md).
   * I tag possono essere creati quando:

      * Creazione e creazione del frammento
      * O successivo:

         * Visualizzando/modificando il frammento **Proprietà** dalla console
         * Modificando i **metadati** nell&#39;editor frammento

   >[!CAUTION]
   >
   >I profili di elaborazione dei metadati non si applicano ai frammenti di contenuto.

* **Principale**

   * Parte integrante del frammento

      * Ogni frammento di contenuto ha un&#39;istanza Master.
      * Impossibile eliminare la Master.
   * Master è accessibile nell&#39;editor frammento in **[Variazioni](/help/assets/content-fragments/content-fragments-variations.md)**.
   * Master non è una variante in quanto tale, ma è la base di tutte le variazioni.


* **Varianti**

   * Rappresentazioni di testo di frammento specifiche per fini editoriali; può essere collegato al canale, ma non è obbligatorio, può essere anche per modifiche locali ad hoc.
   * Sono create come copie di **Master**, ma possono essere modificate come necessario; in genere esiste una sovrapposizione di contenuto tra le varianti stesse.
   * Può essere definito durante la creazione di frammenti.
   * Memorizzato nel frammento, per evitare la dispersione delle copie dei contenuti.
   * Le varianti possono essere [sincronizzate](/help/assets/content-fragments/content-fragments-variations.md#synchronizing-with-master) con Master se il contenuto principale è stato aggiornato.
   * Può essere [Summarized](/help/assets/content-fragments/content-fragments-variations.md#summarizing-text) per troncare rapidamente il testo fino a una lunghezza predefinita.
   * Disponibile nella scheda [Variazioni](/help/assets/content-fragments/content-fragments-variations.md) dell&#39;Editor frammento.

### Contenuto intermedio durante l’authoring della pagina con frammenti di contenuto {#in-between-content-when-page-authoring-with-content-fragments}

Contenuto intermedio:

* È disponibile nell’Editor pagina quando si utilizzano i frammenti di contenuto.
* È [contenuto aggiuntivo aggiunto all&#39;interno del flusso di un frammento](/help/sites-cloud/authoring/fundamentals/content-fragments.md#adding-in-between-content) una volta che è stato utilizzato/utilizzato come riferimento in una pagina.
* È disponibile per l&#39;uso in [Editor pagina quando si lavora con Frammenti di contenuto](/help/sites-cloud/authoring/fundamentals/content-fragments.md).
* È possibile aggiungere contenuto intermedio a qualsiasi frammento, in cui è visibile un solo elemento.
* È possibile utilizzare il contenuto associato, nonché risorse e/o componenti dal browser appropriato.

>[!CAUTION]
>
>Il contenuto intermedio è contento di pagina. Non viene memorizzato nel frammento di contenuto.

### Richiesto da frammenti {#required-by-fragments}

Per creare i frammenti di contenuto è necessario:

* **Modello di contenuto**

   * Sono [abilitati utilizzando il browser di configurazione](/help/assets/content-fragments/content-fragments-configuration-browser.md).
   * Vengono creati [utilizzando Tools](/help/assets/content-fragments/content-fragments-models.md).
   * Obbligatorio per [creare un frammento](/help/assets/content-fragments/content-fragments-managing.md#creating-content-fragments).
   * Definisce la struttura di un frammento (titolo, elementi di contenuto, definizioni di tag).
   * Le definizioni dei modelli di contenuto richiedono un titolo e un elemento dati; tutto il resto è facoltativo.
   * Il modello può definire il contenuto predefinito, se applicabile.
   * Gli autori non possono modificare la struttura definita durante la creazione del contenuto del frammento.
   * Le modifiche apportate a un modello dopo la creazione dei frammenti di contenuto dipendenti possono avere un impatto su tali frammenti di contenuto.

Per utilizzare i frammenti di contenuto per l’authoring delle pagine è inoltre necessario:

* **Componente frammento di contenuto**

   * Strumenti per la distribuzione del frammento in formato HTML e/o JSON.
   * Obbligatorio per [fare riferimento al frammento in una pagina](/help/sites-cloud/authoring/fundamentals/content-fragments.md).
   * responsabile del layout e della consegna di un frammento; ad esempio canali.
   * I frammenti necessitano di uno o più componenti dedicati per definire il layout e fornire alcuni o tutti gli elementi/varianti e il contenuto associato.
   * Trascinando un frammento su una pagina durante l’authoring, il componente richiesto viene automaticamente associato.

## Esempio di utilizzo {#example-usage}

Un frammento, con i relativi elementi e varianti, può essere utilizzato per creare contenuti coerenti per più canali. Durante la progettazione del frammento è necessario considerare gli elementi da utilizzare in qualsiasi punto.

### Esempio WKND {#wknd-sample}

Gli esempi [WKND Site](/help/implementing/developing/introduction/develop-wknd-tutorial.md) sono forniti per aiutarvi a conoscere AEM come Cloud Service. Include frammenti di esempio, che possono essere visualizzati in:

`hhttp://<host>:<port>/assets.html/content/dam/wknd/en/adventures`
