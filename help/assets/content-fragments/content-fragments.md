---
title: Utilizzo di frammenti di contenuto
description: Scoprite come i frammenti di contenuto consentono di progettare, creare, curare e utilizzare contenuti indipendenti dalla pagina.
translation-type: tm+mt
source-git-commit: bb3d90def8855e8dffdc584c0805da120faf7b12

---


# Utilizzo di frammenti di contenuto{#working-with-content-fragments}

Adobe Experience Manager (AEM) Content Fragments allow you to design, create, curate and [publish page-independent content](/help/sites-cloud/authoring/fundamentals/content-fragments.md). They allow you to prepare content ready for use in multiple locations/over multiple channels.

Content fragments can also be delivered in JSON format, using the Sling Model (JSON) export capabilities of AEM core components. This form of delivery:

* enables you to use the component to manage which elements of a fragment to deliver
* consente la distribuzione in blocco, mediante l&#39;aggiunta di più componenti core di frammenti di contenuto nella pagina utilizzata per la distribuzione API

This and the following pages cover the tasks for creating, configuring and maintaining your content fragments:

* [Managing Content Fragments](/help/assets/content-fragments/content-fragments-managing.md) - create your content fragments; then edit, publish and reference
* [Content Fragment Models](/help/assets/content-fragments/content-fragments-models.md) - enabling, creating and defining your models
* [Variations - Authoring Fragment Content](/help/assets/content-fragments/content-fragments-variations.md) - author the fragment content and create variations of the Master
* [Markdown](/help/assets/content-fragments/content-fragments-markdown.md) - using markdown syntax for your fragment
* [Using Associated Content](/help/assets/content-fragments/content-fragments-assoc-content.md) - adding associated content
* [Metadata - Fragment Properties](/help/assets/content-fragments/content-fragments-metadata.md) - viewing and editing the fragment properties

>[!NOTE]
>
>These pages should be read in conjunction with [Page Authoring with Content Fragments](/help/sites-cloud/authoring/fundamentals/content-fragments.md).

The number of communication channels is increasing annually. Typically channels refer to the delivery mechanism, either as the:

* canale fisico; ad esempio desktop, mobile.
* forma di consegna in un canale fisico; Ad esempio, &quot;pagina di dettaglio del prodotto&quot;, &quot;pagina di categoria del prodotto&quot; per desktop o &quot;web mobile&quot;, &quot;app mobile&quot; per dispositivi mobili.

Tuttavia, è probabile che non desideriate utilizzare esattamente lo stesso contenuto per tutti i canali; è necessario ottimizzare il contenuto in base al canale specifico.

I frammenti di contenuto consentono di:

* Considerate come raggiungere i tipi di pubblico target in modo efficiente tra i canali.
* Creazione e gestione di contenuti editoriali neutri per i canali.
* Creazione di pool di contenuti per una serie di canali.
* Progettare varianti di contenuto per canali specifici.
* Aggiungete immagini al testo inserendo risorse (frammenti multimediali diversi).

These content fragments can then be assembled to provide experiences over a variety of channels.

## Content Fragments and Content Services {#content-fragments-and-content-services}

AEM Content Services are designed to generalize the description and delivery of content in/from AEM beyond a focus on web pages.

They provide the delivery of content to channels that are not traditional AEM web pages, using standardized methods that can be consumed by any client. These channels can include:

* Single Page Applications
* Native Mobile Applications
* other channels and touch-points external to AEM

La consegna è realizzata in formato JSON.

I frammenti di contenuto AEM possono essere utilizzati per descrivere e gestire il contenuto strutturato. Il contenuto strutturato è definito in modelli che possono contenere diversi tipi di contenuto; tra cui testo, dati numerici, booleani, data e ora e altro.

Insieme alle funzionalità di esportazione JSON dei componenti core di AEM, questo contenuto strutturato può essere utilizzato per distribuire contenuti AEM a canali diversi dalle pagine AEM.

>[!NOTE]
>
>I **frammenti di contenuto** e i **[frammenti esperienza](/help/sites-cloud/authoring/fundamentals/experience-fragments.md)**sono funzioni diverse in AEM:
>* I **frammenti di contenuto** sono contenuti editoriali, in particolare testo e immagini correlate. Sono contenuti puri, privi di design e layout.
>* I **frammenti esperienza** sono contenuti con un layout completo, un frammento di una pagina Web.
>
>
I frammenti esperienza possono includere contenuti sotto forma di frammenti di contenuto, ma non viceversa.
>
>Per ulteriori informazioni, consultate anche [Informazioni sui frammenti di contenuto e i frammenti esperienza in AEM](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/content-fragments-experience-fragments-article-understand.html).

>[!CAUTION]
>
>I frammenti di contenuto non sono disponibili nell’interfaccia classica.
>
>Il componente Frammento di contenuto è visibile nella barra laterale dell’interfaccia classica, ma non sono disponibili ulteriori funzionalità.

>[!NOTE]
>
>AEM supporta anche la traduzione del contenuto del frammento. Per ulteriori informazioni, consulta Creazione di progetti di traduzione per i frammenti di contenuto.

<!--
>[!NOTE]
>
>AEM also supports the translation of fragment content. See [Creating Translation Projects for Content Fragments](/help/assets/creating-translation-projects-for-content-fragments.md) for further information.
-->

## Tipi di frammento di contenuto {#types-of-content-fragment}

I frammenti di contenuto possono essere:

* Frammenti semplici: non hanno una struttura predefinita. Contengono solo testo e immagini.
Si basano sul modello Frammento semplice.

* Frammenti contenenti contenuto strutturatoQuesti si basano su un modello [di frammento di](/help/assets/content-fragments/content-fragments-models.md)contenuto, che preimposta una struttura per il frammento risultante.
These can also be used to realize Content Services using the JSON Exporter.

## Tipo di contenuto {#content-type}

Content fragments are:

* Stored as **Assets**:

   * I frammenti di contenuto (e le relative varianti) possono essere creati e mantenuti dalla console **Risorse** .
   * Authored and edited in the Content Fragment Editor.

* Used in the [page editor by means of the Content Fragment component](/help/sites-cloud/authoring/fundamentals/content-fragments.md) (referencing component):

   * Il componente **Frammento** di contenuto è disponibile per gli autori delle pagine. It allows them to reference, and deliver, the required content fragment in either HTML or JSON format.

Content Fragments are a content structure that:

* Are without layout or design (some text formatting is possible in Rich Text mode).
* Contain one, or more, [constituent parts](#constituent-parts-of-a-content-fragment).
* Può [contenere o collegare immagini](#fragments-with-visual-assets).
* Può utilizzare contenuto [intermedio](#in-between-content-when-page-authoring-with-content-fragments) quando viene fatto riferimento a una pagina.

* Are independent from the delivery mechanism (i.e. page, channel).

### Fragments with Visual Assets {#fragments-with-visual-assets}

To give authors more control of their content, images can be added to and/or integrated with a content fragment.

Assets can be used with a content fragment in several ways; each with its own advantage(s):

* **Insert Asset** into a fragment (mixed-media fragments)

   * Are an integral part of the fragment (see [Constituent Parts of a Content Fragment](#constituent-parts-of-a-content-fragment)).
   * Define the position of the asset.
   * See [Inserting Assets into your Fragment](/help/assets/content-fragments/content-fragments-variations.md#inserting-assets-into-your-fragment) in the Fragment Editor for more information.
   >[!NOTE]
   >
   >Le risorse visive inserite nel frammento di contenuto stesso sono associate al paragrafo precedente. When the fragment is added to a page these assets are moved in relation to that paragraph when in-between content is added.

* **Contenuto associato**

   * Are connected to a fragment; but not a fixed part of the fragment (see [Constituent Parts of a Content Fragment](#constituent-parts-of-a-content-fragment)).
   * Allows some flexibility for positioning.
   * Are easily available for use (as in-between content) when using the fragment on a page.
   * See [Associated Content](/help/assets/content-fragments/content-fragments-assoc-content.md) for more information.

* Risorse disponibili nel **browser Risorse** dell’editor pagina

   * Allow full flexibility for selection of an asset.
   * Allows some flexibility for positioning.
   * Does not provide the concept of being approved for a specific fragment.
   * See [Assets Browser](/help/sites-cloud/authoring/fundamentals/environment-tools.md#assets-browser) for more information.

### Parti costitutive di un frammento di contenuto {#constituent-parts-of-a-content-fragment}

The content fragment assets are made up of the following parts (either directly or indirectly):

* **Fragment Elements**

   * Elements correlate to the data fields holding content.
   * For fragments with structured content, you use a content model to create the content fragment. The elements (fields) specified in the model define the structure of the fragment. These elements (fields) can be of a variety of data-types.
   * For simple fragments:

      * The content is held in one (or more) multi-line text field(s), or element(s).
      * The elements are defined in the fragment template (cannot be defined when authoring the fragment).

* **Paragrafi frammento**

   * Blocks of text, that are:

      * separated by vertical spaces (carriage return)
      * in multi-line text elements; in either simple or structured fragments
   * Nelle modalità [Rich Text](/help/assets/content-fragments/content-fragments-variations.md#rich-text) e [Markdown](/help/assets/content-fragments/content-fragments-variations.md#markdown), un paragrafo può essere formattato come intestazione, in tal caso appartiene a un’unica unità insieme al paragrafo seguente.

   * Attiva il controllo del contenuto durante l’authoring delle pagine.


* **Assets Inserted into a Fragment (Mixed-Media Fragments)**

   * Risorse (immagini) inserite nel frammento effettivo e utilizzate come contenuto interno di un frammento.
   * Are embedded in the paragraph system of the fragment.
   * Può essere formattato quando un [frammento viene utilizzato/a cui viene fatto riferimento in una pagina](/help/sites-cloud/authoring/fundamentals/content-fragments.md).
   * È possibile aggiungere, eliminare o spostare solo all&#39;interno di un frammento utilizzando l&#39;Editor frammento. Queste azioni non possono essere effettuate nell’editor pagina.
   * È possibile aggiungere, eliminare o spostare solo all’interno di un frammento utilizzando il formato [RTF nell’editor](/help/assets/content-fragments/content-fragments-variations.md#inserting-assets-into-your-fragment)frammento.
   * Può essere aggiunto solo a elementi di testo con più righe (qualsiasi tipo di frammento).
   * Sono allegati al testo precedente (paragrafo).
   >[!CAUTION]
   >
   >Può essere (inavvertitamente) rimosso da un frammento passando al formato Testo normale.

   >[!NOTE]
   >
   >Quando si utilizza un frammento in una pagina è inoltre possibile aggiungere risorse come contenuto [](/help/sites-cloud/authoring/fundamentals/content-fragments.md#using-associated-content) aggiuntivo (intermedio); utilizzando Contenuto associato o risorse dal browser Risorse.

* **Contenuto associato**

   * Si tratta di contenuto esterno a un frammento ma con rilevanza editoriale. In genere, immagini, video o altri frammenti.
   * The individual assets within the collection are available to be used with the fragment in the page editor, when it is added to a page. This means that they are optional, depending on the requirements of the specific channel.
   * The assets are [associated to fragments via collections](/help/assets/content-fragments/content-fragments-assoc-content.md); associated collections allow the author to decide which assets to use when they are authoring the page.

      * Collections can be associated to fragments via templates, as default content, or by authors during fragment authoring.
      * [Le raccolte](/help/assets/manage-collections.md) di risorse (DAM) sono la base per il contenuto associato dei frammenti.
   * Optionally you can also add the fragment itself to a collection to aid tracking.

* **Fragment Metadata**

   * Utilizzate gli schemi [di metadati delle](/help/assets/metadata-schemas.md)risorse.
   * Tags can be created when you:

      * Creazione e creazione del frammento
      * O successivo:

         * By viewing/editing the fragment **Properties** from the console
         * Modificando i **metadati** nell’editor frammento
   >[!CAUTION]
   >
   >Metadata processing profiles do not apply to Content Fragments.

* **Principale**

   * An integral part of the fragment

      * Every content fragment has one instance of Master.
      * Master cannot be deleted.
   * Master is accessible in the fragment editor under **[Variations](/help/assets/content-fragments/content-fragments-variations.md)**.
   * Master is not a variation as such, but is the basis of all variations.


* **Varianti**

   * Renditions of fragment text that are specific to editorial purpose; can be related to channel but is not compulsory, can also be for ad-hoc local modifications.
   * Are created as copies of **Master**, but can then be edited as required; there is usually content overlap between the variations themselves.
   * Può essere definito durante la creazione di frammenti o predefinito nei modelli di frammento.
   * Stored in the fragment, to help avoid scattering of content copies.
   * Variations can be [synchronized](/help/assets/content-fragments/content-fragments-variations.md#synchronizing-with-master) with Master if the Master content has been updated.
   * Può essere [sintetizzato](/help/assets/content-fragments/content-fragments-variations.md#summarizing-text) per troncare rapidamente il testo fino a una lunghezza predefinita.
   * Available under the [Variations](/help/assets/content-fragments/content-fragments-variations.md) tab of the fragment editor.

### Contenuto intermedio durante l’authoring della pagina con frammenti di contenuto {#in-between-content-when-page-authoring-with-content-fragments}

In-between content:

* Is available for use in the Page Editor when working with Content Fragments.
* Il contenuto [aggiuntivo viene aggiunto all’interno del flusso di un frammento](/help/sites-cloud/authoring/fundamentals/content-fragments.md#adding-in-between-content) una volta utilizzato/a cui è stato fatto riferimento in una pagina.
* È disponibile per l’uso nell’Editor [pagina quando si utilizzano i frammenti](/help/sites-cloud/authoring/fundamentals/content-fragments.md)di contenuto.
* In-between content can be added to any fragment, where there is only one element visible.
* È possibile utilizzare il contenuto associato, nonché risorse e/o componenti dal browser appropriato.

>[!CAUTION]
>
>Il contenuto intermedio è contento di pagina. Non viene memorizzato nel frammento di contenuto.

### Richiesto da frammenti {#required-by-fragments}

Per creare, modificare e utilizzare i frammenti di contenuto è inoltre necessario:

* **Modello di contenuto**

   * Vengono [abilitati e quindi creati utilizzando Strumenti](/help/assets/content-fragments/content-fragments-models.md).
   * Obbligatorio per [creare un frammento](/help/assets/content-fragments/content-fragments-managing.md#creating-content-fragments)strutturato.
   * Definisce la struttura di un frammento (titolo, elementi di contenuto, definizioni di tag).
   * Le definizioni dei modelli di contenuto richiedono un titolo e un elemento dati; tutto il resto è facoltativo. Il modello definisce un ambito minimo del frammento e, se applicabile, il contenuto predefinito. Gli autori non possono modificare la struttura definita durante la creazione del contenuto del frammento.

* **Modello frammento**

   * Obbligatorio per [creare un frammento](/help/assets/content-fragments/content-fragments-managing.md#creating-content-fragments)semplice.
   * Generalmente sviluppato durante l’implementazione del progetto; impossibile generarlo durante la creazione.
   * Definisce le proprietà di base di un frammento semplice (titolo, numero di elementi di testo, definizioni di tag).
   * Le definizioni dei modelli richiedono un titolo e un elemento di testo; tutto il resto è facoltativo. Il modello definisce un ambito minimo del frammento e, se applicabile, il contenuto predefinito. Gli autori possono in seguito estendere un frammento oltre a quanto definito nel modello.

* **Componente frammento di contenuto**

   * Strumenti per la distribuzione del frammento in formato HTML e/o JSON.
   * Obbligatorio per fare [riferimento al frammento in una pagina](/help/sites-cloud/authoring/fundamentals/content-fragments.md).
   * responsabile del layout e della consegna di un frammento; ad esempio canali.
   * I frammenti necessitano di uno o più componenti dedicati per definire il layout e fornire alcuni o tutti gli elementi/varianti e il contenuto associato.
   * Trascinando un frammento su una pagina durante l’authoring, il componente richiesto viene automaticamente associato.

## Esempio di utilizzo {#example-usage}

Un frammento, con i relativi elementi e varianti, può essere utilizzato per creare contenuti coerenti per più canali. Durante la progettazione del frammento è necessario considerare gli elementi da utilizzare in qualsiasi punto.

### Esempio WKND {#wknd-sample}

Gli esempi [WKND Site](/help/implementing/developing/introduction/develop-wknd-tutorial.md) sono forniti per aiutarti a conoscere AEM come servizio cloud. Include frammenti di esempio, che possono essere visualizzati in:

`hhttp://<host>:<port>/assets.html/content/dam/wknd/en/adventures`
