---
title: Personalizzazione ed estensione dei frammenti di contenuto
description: Un frammento di contenuto estende una risorsa standard.
translation-type: tm+mt
source-git-commit: 74db82093a358350e20f932446e78b779178e9f8

---


# Personalizzazione ed estensione dei frammenti di contenuto{#customizing-and-extending-content-fragments}

In Adobe Experience Manager come servizio Cloud un frammento di contenuto estende una risorsa standard; vedere:

* [Creazione e gestione di frammenti](/help/assets/content-fragments/content-fragments.md) di contenuto e creazione di [pagine con frammenti](/help/sites-cloud/authoring/fundamentals/content-fragments.md) di contenuto per ulteriori informazioni sui frammenti di contenuto.

* [Gestione delle risorse](/help/assets/manage-digital-assets.md) e [personalizzazione ed estensione dell’Editor](/help/assets/extend-asset-editor.md) risorse per ulteriori informazioni sulle risorse standard.

## Architettura {#architecture}

Le [parti](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment) costitutive di base di un frammento di contenuto sono:

* Un Frammento *Di* Contenuto,
* costituito da uno o più elementi *di* contenuto,
* e che può avere una o più varianti *di* contenuto.

A seconda del tipo di frammento, vengono utilizzati anche i modelli o il modello di frammento **** semplice:

>[!CAUTION]
>
>[Per la creazione di tutti i frammenti è ora consigliabile utilizzare modelli](/help/assets/content-fragments/content-fragments-models.md) di frammenti di contenuto.
>
>I modelli di frammento di contenuto vengono utilizzati per tutti gli esempi in WKND.

* Modelli per frammenti di contenuto:

   * Utilizzato per definire frammenti di contenuto contenenti contenuto strutturato.
   * I modelli di frammento di contenuto definiscono la struttura di un frammento di contenuto al momento della creazione.
   * Un frammento fa riferimento al modello; le modifiche apportate al modello possono quindi avere o avranno effetto su eventuali frammenti dipendenti.
   * I modelli sono composti di tipi di dati.
   * Le funzioni per aggiungere nuove varianti, ecc., devono aggiornare di conseguenza il frammento.
   >[!NOTE]
   >
   >Per visualizzare/eseguire il rendering di un frammento di contenuto, l&#39;account deve disporre delle autorizzazioni di lettura per il modello.

   >[!CAUTION]
   >
   >Qualsiasi modifica apportata a un modello di frammento di contenuto esistente può avere un impatto sui frammenti dipendenti; in questo modo è possibile creare proprietà orfane nei frammenti.

* Modello frammento di contenuto - Frammento **** semplice:

   * Utilizzato per definire frammenti di contenuto semplici.

   * Questo modello definisce la struttura (di base, solo testo) di un frammento di contenuto al momento della creazione.

   * Il modello viene copiato nel frammento al momento della creazione.

   * Le funzioni per aggiungere nuove varianti, ecc., devono aggiornare di conseguenza il frammento.

   * Il modello di frammento di contenuto (frammento **** semplice) funziona in modo diverso da quello di altri meccanismi di modellazione all’interno dell’ecosistema AEM (ad esempio, modelli di pagina, ecc.). Occorre pertanto considerarlo separatamente.

   * Se basato sul modello di frammento **** semplice, il tipo MIME del contenuto viene gestito sul contenuto effettivo; ciò significa che ogni elemento e ogni variante possono avere un tipo MIME diverso.

### Integrazione di Siti con Risorse {#integration-of-sites-with-assets}

Content Fragment Management (CFM) fa parte di AEM Assets come segue:

* I frammenti di contenuto sono risorse.
* Utilizzano la funzionalità Risorse esistente.
* Sono completamente integrati con le risorse (console di amministrazione, ecc.).

I frammenti di contenuto sono considerati una funzione Siti come:

* Vengono utilizzati per la creazione delle pagine.

#### Mapping di frammenti di contenuto strutturati a risorse {#mapping-structured-content-fragments-to-assets}

![frammento di contenuto in risorse strutturate](assets/content-fragment-to-assets-structured.png)

I frammenti di contenuto con contenuto strutturato (ovvero basato su un modello di frammento di contenuto) vengono mappati su una singola risorsa:

* Tutto il contenuto è memorizzato nel `jcr:content/data` nodo della risorsa:

   * I dati dell&#39;elemento vengono memorizzati sotto il nodo secondario principale:
      `jcr:content/data/master`

   * Le varianti sono memorizzate in un nodo secondario che contiene il nome della variante:
ad esempio `jcr:content/data/myvariation`

   * I dati di ciascun elemento vengono memorizzati nel rispettivo nodo secondario come proprietà con il nome dell&#39;elemento:
Ad esempio, il contenuto dell&#39;elemento `text` viene memorizzato come proprietà `text` in `jcr:content/data/master`

* I metadati e il contenuto associato sono memorizzati sotto `jcr:content/metadata`Eccetto il titolo e la descrizione, che non sono considerati metadati tradizionali e memorizzati in `jcr:content`

#### Mappatura di frammenti di contenuto semplici a risorse {#mapping-simple-content-fragments-to-assets}

![frammento di contenuto alle risorse](assets/content-fragment-to-assets-simple.png)

I frammenti di contenuto semplice (basati sul modello di frammento **** semplice) sono mappati su un composito costituito da una risorsa principale e (facoltativamente) da risorse secondarie:

* Tutte le informazioni non di contenuto di un frammento (ad esempio titolo, descrizione, metadati, struttura) vengono gestite esclusivamente sulla risorsa principale.
* Il contenuto del primo elemento di un frammento viene mappato sulla rappresentazione originale della risorsa principale.

   * Le varianti (se ce ne sono) del primo elemento sono mappate ad altre rappresentazioni della risorsa principale.

* Eventuali elementi aggiuntivi (se esistenti) sono mappati alle risorse secondarie della risorsa principale.

   * Il contenuto principale di questi elementi aggiuntivi viene associato alla rappresentazione originale della rispettiva sottorisorsa.
   * Altre variazioni (se applicabili) di eventuali elementi aggiuntivi sono associate ad altre rappresentazioni della rispettiva sub-attività.

#### Posizione risorsa {#asset-location}

Come per le risorse standard, un frammento di contenuto è memorizzato in:

`/content/dam`

#### Autorizzazioni risorsa {#asset-permissions}

Per ulteriori dettagli, vedere Frammento di [contenuto - Considerazioni](/help/assets/content-fragments/content-fragments-delete.md)sull&#39;eliminazione.

#### Integrazione delle funzionalità {#feature-integration}

Per integrare con il core Assets:

* La funzione Content Fragment Management (CFM) si basa sul core Assets.

* CFM fornisce le proprie implementazioni per gli elementi nelle viste scheda/colonna/elenco; questi plug-in nelle implementazioni di rendering dei contenuti di Assets.

* Diversi componenti Risorse sono stati estesi per gestire i frammenti di contenuto.

### Utilizzo di frammenti di contenuto nelle pagine {#using-content-fragments-in-pages}

>[!CAUTION]
>
>Il componente Frammento di [contenuto fa parte dei componenti](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/content-fragment-component.html)core. Per ulteriori informazioni, consulta [Sviluppo di componenti](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/developing.html) di base.

È possibile fare riferimento ai frammenti di contenuto dalle pagine AEM, come qualsiasi altro tipo di risorsa. AEM fornisce il componente **[di base](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/content-fragment-component.html)**Frammento di contenuto, un[componente che consente di includere frammenti di contenuto nelle pagine](/help/sites-cloud/authoring/fundamentals/content-fragments.md#adding-a-content-fragment-to-your-page). È inoltre possibile estendere questo componente di base**[ Frammento](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/developing.html)** di contenuto.

* Il componente utilizza la `fragmentPath` proprietà per fare riferimento al frammento di contenuto effettivo. La `fragmentPath` proprietà viene gestita allo stesso modo delle proprietà simili di altri tipi di risorse; ad esempio, quando il frammento di contenuto viene spostato in un&#39;altra posizione.

* Il componente consente di selezionare la variante da visualizzare.

* È inoltre possibile selezionare una serie di paragrafi per limitare l&#39;output; ad esempio, può essere utilizzato per l&#39;output a più colonne.

* Il componente permette il contenuto intermedio:

   * Qui il componente permette di inserire altre risorse (immagini, ecc.) tra i paragrafi del frammento a cui viene fatto riferimento.

   * Per il contenuto intermedio è necessario:

      * essere a conoscenza della possibilità di riferimenti instabili; il contenuto intermedio (aggiunto durante l’authoring di una pagina) non ha alcuna relazione fissa con il paragrafo a cui è posizionato accanto, inserendo un nuovo paragrafo (nell’editor dei frammenti di contenuto) prima che la posizione del contenuto intermedio possa perdere la posizione relativa

      * prendete in considerazione i parametri aggiuntivi (come i filtri per varianti e paragrafi) per configurare il rendering sulla pagina

>[!NOTE]
>
>**Modello per frammenti di contenuto:**
>
>Quando si utilizza un frammento di contenuto basato su un modello di frammento di contenuto in una pagina, viene fatto riferimento al modello. Questo significa che se il modello non è stato pubblicato al momento della pubblicazione della pagina, verrà contrassegnato e il modello verrà aggiunto alle risorse da pubblicare insieme alla pagina.
>
>**Modello frammento di contenuto - Frammento semplice:**
>
>Quando si utilizza un frammento di contenuto basato sul modello di frammento di contenuto **Frammento** semplice su una pagina, non è presente alcun riferimento in quanto il modello è stato copiato al momento della creazione del frammento.

### Integrazione con altri framework {#integration-with-other-frameworks}

I frammenti di contenuto possono essere integrati con:

* **Traduzioni**

   I frammenti di contenuto sono completamente integrati nel flusso di lavoro di traduzione di AEM. A livello architettonico, ciò significa:

   * Le singole traduzioni di un frammento di contenuto sono in realtà frammenti separati; ad esempio:

      * sono situati in radici linguistiche diverse; ma condividono esattamente lo stesso percorso relativo sotto la radice della lingua pertinente:

         `/content/dam/<path>/en/<to>/<fragment>`

         vs

         `/content/dam/<path>/de/<to>/<fragment>`
   * Oltre ai percorsi basati su regole, non esiste un&#39;ulteriore connessione tra le diverse versioni linguistiche di un frammento di contenuto; sono gestiti come due frammenti separati, anche se l’interfaccia utente fornisce i mezzi per spostarsi tra le varianti di lingua.
   >[!NOTE]
   >
   >Il flusso di lavoro di traduzione di AEM funziona con `/content`:
   >
   >* Poiché i modelli di frammento di contenuto risiedono in `/conf`, questi non sono inclusi in tali traduzioni. Potete internazionalizzare le stringhe di interfaccia.


* **Schemi metadati**

   * I frammenti di contenuto (re)utilizzano gli schemi [di](/help/assets/metadata-schemas.md)metadati, che possono essere definiti con risorse standard.

   * CFM fornisce uno schema specifico proprio:

      `/libs/dam/content/schemaeditors/forms/contentfragment`

      può essere esteso, se necessario.

   * Il modulo schema corrispondente è integrato con l&#39;editor frammento.

## API di gestione dei frammenti di contenuto - Lato server {#the-content-fragment-management-api-server-side}

È possibile utilizzare l&#39;API lato server per accedere ai frammenti di contenuto; vedere:

[com.adobe.cq.dam.cfm](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/ref/javadoc/com/adobe/cq/dam/cfm/package-frame.html)

>[!CAUTION]
>
>È vivamente consigliato utilizzare l&#39;API lato server invece di accedere direttamente alla struttura del contenuto.

### Interfacce chiave {#key-interfaces}

Le tre interfacce seguenti possono fungere da punti di ingresso:

* **Frammento** di contenuto ([ContentFragment](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/ref/javadoc/com/adobe/cq/dam/cfm/ContentFragment.html))

   Questa interfaccia consente di utilizzare un frammento di contenuto in modo astratto.

   L&#39;interfaccia fornisce i mezzi per:

   * Gestire i dati di base (ad es. get name; get/set title/description)
   * Accesso ai metadati
   * Elementi di accesso:

      * Elementi elenco
      * Ottieni elementi per nome
      * Creare nuovi elementi (vedere [Caveats](#caveats))

      * Dati degli elementi di accesso (vedere `ContentElement`)
   * Elenca le varianti definite per il frammento
   * Creare nuove varianti a livello globale
   * Gestire il contenuto associato:

      * Elenca raccolte
      * Aggiungere raccolte
      * Rimuovere le raccolte
   * Accesso al modello o al modello del frammento
   Le interfacce che rappresentano gli elementi primari di un frammento sono:

   * **Elemento** contenuto ([ContentElement](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/ref/javadoc/com/adobe/cq/dam/cfm/ContentElement.html))

      * Ottenere i dati di base (nome, titolo, descrizione)
      * Ottenere/impostare il contenuto
      * Accesso alle varianti di un elemento:

         * Varianti elenco
         * Ottieni varianti per nome
         * Creare nuove varianti (vedere [Caveats](#caveats))
         * Rimuovere le varianti (vedere [Caveats](#caveats))
         * Accedere ai dati delle varianti (vedere `ContentVariation`)
      * Tasti di scelta rapida per la risoluzione delle varianti (applicazione di una logica di fallback specifica per l&#39;implementazione, se la variante specificata non è disponibile per un elemento)
   * **Variazione** contenuto ([ContentVariation](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/ref/javadoc/com/adobe/cq/dam/cfm/ContentVariation.html))

      * Ottenere i dati di base (nome, titolo, descrizione)
      * Ottenere/impostare il contenuto
      * Sincronizzazione semplice, in base alle ultime informazioni modificate
   Tutte e tre le interfacce ( `ContentFragment`, `ContentElement`, `ContentVariation`) estendono l&#39; `Versionable` interfaccia, che aggiunge funzionalità di controllo delle versioni, necessarie per i frammenti di contenuto:

   * Creare una nuova versione dell&#39;elemento
   * Elenca versioni dell&#39;elemento
   * Ottenete il contenuto di una versione specifica dell’elemento con versione







### Adattamento - Utilizzo di adaptTo() {#adapting-using-adaptto}

È possibile adattare quanto segue:

* `ContentFragment` può essere adattato a:

   * `Resource` - la risorsa Sling sottostante; per aggiornare `Resource` direttamente il sottostante è necessario ricreare l&#39; `ContentFragment` oggetto.

   * `Asset` - l&#39; `Asset` astrazione DAM che rappresenta il frammento di contenuto; per aggiornare `Asset` direttamente l&#39;oggetto è necessario ricrearlo `ContentFragment` .

* `ContentElement` può essere adattato a:

   * `ElementTemplate` - per accedere alle informazioni strutturali dell&#39;elemento.

* `Resource` può essere adattato a:

   * `ContentFragment`

### Caveats {#caveats}

Va osservato che:

* L&#39;intera API è progettata per **non** mantenere le modifiche automaticamente (se non diversamente specificato nel JavaDoc API). Sarà quindi sempre necessario impegnare il risolutore delle risorse della rispettiva richiesta (o il risolutore che si sta utilizzando).

* Attività che potrebbero richiedere ulteriore sforzo:

   * La creazione e la rimozione di nuovi elementi non comporta l&#39;aggiornamento della struttura dati di frammenti semplici (basata sul modello di frammento **** semplice).

   * Crea nuove varianti da `ContentFragment` per aggiornare la struttura dei dati.

   * La rimozione delle varianti esistenti non aggiornerà la struttura dei dati.

## API di gestione dei frammenti di contenuto - Lato client {#the-content-fragment-management-api-client-side}

>[!CAUTION]
>
>L&#39;API lato client è interna.

### Informazioni aggiuntive {#additional-information}

Consulta:

* `filter.xml`

   La `filter.xml` gestione dei frammenti di contenuto è configurata in modo da non sovrapporsi al pacchetto di contenuto di base di Risorse.

## Modifica sessioni {#edit-sessions}

Una sessione di modifica viene avviata quando l&#39;utente apre un frammento di contenuto in una delle pagine dell&#39;editor. La sessione di modifica viene terminata quando l’utente esce dall’editor selezionando **Salva** o **Annulla**.

### Requisiti {#requirements}

Requisiti per il controllo di una sessione di modifica:

* La modifica di un frammento di contenuto, che può estendersi su più viste (= pagine HTML), deve essere atomica.

* L&#39;editing dovrebbe essere anche *transazionale*; alla fine della sessione di modifica, le modifiche devono essere salvate (salvate) o ripristinate (annullate).

* I casi Edge devono essere gestiti correttamente; tali situazioni includono situazioni come quelle in cui l’utente esce dalla pagina immettendo manualmente un URL o utilizzando la navigazione globale.

* Per evitare la perdita di dati, deve essere disponibile un salvataggio automatico periodico (ogni x minuti).

* Se un frammento di contenuto viene modificato da due utenti contemporaneamente, non devono sovrascrivere le modifiche l&#39;uno rispetto all&#39;altro.

<!--
#### Processes {#processes}

The processes involved are:

* Starting a session

  * A new version of the content fragment is created.

  * Auto save is started.

  * Cookies are set; these define the currently edited fragment and that there is an edit session open.

* Finishing a session

  * Auto save is stopped.

  * Upon commit:

    * The last modified information is updated.

    * Cookies are removed.

  * Upon rollback:

    * The version of the content fragment that was created when the edit session was started is restored.

    * Cookies are removed.

* Editing

  * All changes (auto save included) are done on the active content fragment - not in a separated, protected area.

  * Therefore, those changes are reflected immediately on AEM pages that reference the respective content fragment

#### Actions {#actions}

The possible actions are:

* Entering a page

  * Check if an editing session is already present; by checking the respective cookie.

    * If one exists, verify that the editing session was started for the content fragment that is currently being edited

      * If the current fragment, reestablish the session.

      * If not, try to cancel editing for the previously edited content fragment and remove cookies (no editing session present afterwards).

    * If no edit session exists, wait for the first change made by the user (see below).

  * Check if the content fragment is already referenced on a page and display appropriate information if so.

* Content change

  * Whenever the user changes content and there is no edit session present, a new edit session is created (see [Starting a session](#processes)).

-->

* Uscire da una pagina

   * Se è presente una sessione di modifica e le modifiche non sono state persistenti, viene visualizzata una finestra di dialogo di conferma modale per informare l’utente del contenuto potenzialmente perso e consentire loro di restare sulla pagina.

## Esempi {#examples}

### Esempio: Accesso a un frammento di contenuto esistente {#example-accessing-an-existing-content-fragment}

A tal fine, potete adattare la risorsa che rappresenta l&#39;API a:

`com.adobe.cq.dam.cfm.ContentFragment`

Esempio:

```java
// first, get the resource
Resource fragmentResource = resourceResolver.getResource("/content/dam/fragments/my-fragment");
// then adapt it
if (fragmentResource != null) {
    ContentFragment fragment = fragmentResource.adaptTo(ContentFragment.class);
    // the resource is now accessible through the API
}
```

### Esempio: Creazione di un nuovo frammento di contenuto {#example-creating-a-new-content-fragment}

Per creare un nuovo frammento di contenuto a livello di programmazione, è necessario utilizzare un frammento adattato`FragmentTemplate` da una risorsa modello o modello.

Esempio:

```java
Resource templateOrModelRsc = resourceResolver.getResource("...");
FragmentTemplate tpl = templateOrModelRsc.adaptTo(FragmentTemplate.class);
ContentFragment newFragment = tpl.createFragment(parentRsc, "A fragment name", "A fragment description.");
```

### Esempio: Specifica dell&#39;intervallo di salvataggio automatico {#example-specifying-the-auto-save-interval}

L’intervallo [di salvataggio](/help/assets/content-fragments/content-fragments-managing.md#save-cancel-and-versions) automatico (espresso in secondi) può essere definito utilizzando il gestore di configurazione (ConfMgr):

* Nodo: `<conf-root>/settings/dam/cfm/jcr:content`
* Nome proprietà: `autoSaveInterval`
* Tipo: `Long`

* Predefinito: `600` (10 minuti); è definito in `/libs/settings/dam/cfm/jcr:content`

Per impostare un intervallo di salvataggio automatico di 5 minuti è necessario definire la proprietà sul nodo; ad esempio:

* Nodo: `/conf/global/settings/dam/cfm/jcr:content`
* Nome proprietà: `autoSaveInterval`

* Tipo: `Long`

* Valore: `300` (5 minuti equivale a 300 secondi)

## Componenti per l’authoring delle pagine {#components-for-page-authoring}

Per ulteriori informazioni, consulta

* [Componenti di base - Componente](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/content-fragment-component.html) frammento di contenuto (consigliato)
