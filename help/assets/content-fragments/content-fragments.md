---
title: Utilizzo dei frammenti di contenuto (Assets - Frammenti di contenuto)
description: Scopri come i frammenti di contenuto in Adobe Experience Manager (AEM) as a Cloud Service ti consentono di progettare, creare, curare e utilizzare contenuti, ideali per l’authoring delle pagine e la distribuzione headless.
exl-id: db17eff1-4252-48d5-bb67-5e476e93ef7e
feature: Content Fragments
role: User
solution: Experience Manager Sites
source-git-commit: 5054b843a8bb6053bb6617e9efdfc16dd1eac6ca
workflow-type: tm+mt
source-wordcount: '2247'
ht-degree: 57%

---

# Utilizzo di frammenti di contenuto {#working-with-content-fragments}

Con Adobe Experience Manager (AEM) as a Cloud Service, i frammenti di contenuto ti consentono di progettare, creare, curare e [pubblicare contenuti indipendenti dalla pagina](/help/sites-cloud/authoring/fragments/content-fragments.md). Consentono di preparare contenuti pronti per l&#39;uso in più posizioni e su più canali, ideali per la distribuzione headless. Possono inoltre essere utilizzati insieme a [Gestione multisito per consentire di riutilizzare il contenuto](#reusing-content-fragments-with-msm).

I frammenti di contenuto contengono contenuto strutturato:

* Sono basati su un [Modello per frammenti di contenuto](/help/assets/content-fragments/content-fragments-models.md), che definisce la struttura del frammento risultante.
* La struttura può essere di tre tipi:
   * Base
      * Ad esempio, un singolo campo di testo su più righe.
      * Può essere utilizzato per preparare contenuti semplici da utilizzare nell’authoring delle pagine.
   * Complessa
      * Combinazione di molti campi di tipi di dati diversi, tra cui testo, numeri, dati booleani, dati e ora.
      * Può essere utilizzato per preparare contenuti più strutturati per l’authoring delle pagine o per la distribuzione all’applicazione.
   * Nidificata
      * I tipi di dati di riferimento disponibili consentono di nidificare il contenuto.
      * Questa struttura è spesso utilizzata per la consegna a un’applicazione.

I frammenti di contenuto possono essere consegnati anche in formato JSON, utilizzando le funzionalità di esportazione Sling Model (JSON) dei componenti core di AEM. Questo tipo di consegna:

* consente di utilizzare il componente per gestire gli elementi di un frammento da consegnare;
* consente la consegna in massa, aggiungendo più componenti core per frammenti di contenuto nella pagina utilizzata per la consegna API

>[!NOTE]
>
>I frammenti di contenuto sono una funzione di Sites, ma vengono memorizzati come **Risorse**.
>
>I frammenti di contenuto e i modelli di frammenti di contenuto ora sono gestiti principalmente con la console **[Frammenti di contenuto](/help/sites-cloud/administering/content-fragments/overview.md#content-fragments-console)**, anche se i frammenti di contenuto possono ancora essere gestiti dalla console **Assets** e i modelli di frammenti di contenuto dalla console **Strumenti**. Questa sezione riguarda la gestione dalle console **Assets** e **Tools**.
>
>Esistono due editor per l’authoring dei frammenti di contenuto; anche se la funzionalità di base è la stessa, esistono alcune differenze. Questa sezione tratta l&#39;editor originale, a cui si accede principalmente dalla console **Assets**. Per informazioni dettagliate sul nuovo editor, a cui si accede principalmente dalla console **Frammenti di contenuto**, consulta la documentazione di Sites [Frammenti di contenuto - Authoring](/help/sites-cloud/administering/content-fragments/authoring.md). Entrambi gli editor dispongono di un interruttore nella barra degli strumenti superiore per consentire un accesso rapido all’altro editor.

Questa pagina e quelle seguenti descrivono le attività di creazione, configurazione, manutenzione e utilizzo dei frammenti di contenuto:

* [Abilita funzionalità frammento di contenuto per la tua istanza](/help/assets/content-fragments/content-fragments-configuration-browser.md)
* [Modelli per frammenti di contenuto](/help/assets/content-fragments/content-fragments-models.md) - abilitazione, creazione e definizione dei modelli
* [Gestione dei frammenti di contenuto](/help/assets/content-fragments/content-fragments-managing.md): crea i frammenti di contenuto, quindi modifica, pubblica e fai riferimento a essi
* [Varianti: authoring dei contenuti di frammenti](/help/assets/content-fragments/content-fragments-variations.md): come creare il contenuto di un frammento e quindi varianti del contenuto principale
* [Markdown](/help/assets/content-fragments/content-fragments-markdown.md): come utilizzare la sintassi markdown per il frammento
* [Utilizzo di contenuti associati](/help/assets/content-fragments/content-fragments-assoc-content.md): come aggiungere contenuti associati
* [Metadati: proprietà dei frammenti](/help/assets/content-fragments/content-fragments-metadata.md): come visualizzare e modificare le proprietà dei frammenti
* Utilizzare [Frammenti di contenuto insieme a GraphQL per distribuire il contenuto](/help/assets/content-fragments/content-fragments-graphql.md) da utilizzare nelle applicazioni. Per facilitare questa fase, puoi visualizzare in anteprima [l&#39;output JSON](/help/assets/content-fragments/content-fragments-json-preview.md).
* [Riutilizzare frammenti di contenuto con MSM](#reusing-content-fragments-with-msm)

>[!NOTE]
>
>Queste pagine possono essere lette con:
>
>* [Authoring delle pagine con frammenti di contenuto](/help/sites-cloud/authoring/fragments/content-fragments.md).
>* [Personalizzazione ed estensione dei frammenti di contenuto](/help/implementing/developing/extending/content-fragments-customizing.md)
>* [Componenti di configurazione dei frammenti di contenuto per il rendering](/help/implementing/developing/extending/content-fragments-configuring-components-rendering.md)
>* [Supporto dei frammenti di contenuto nell’API HTTP di AEM Assets](/help/assets/content-fragments/assets-api-content-fragments.md)
>* [API GraphQL di AEM per l’utilizzo con Frammenti di contenuto](/help/headless/graphql-api/content-fragments.md)
>* [OpenAPI per il modello Frammento di contenuto e Frammento di contenuto](/help/headless/content-fragment-openapis.md)

Il numero di canali di comunicazione aumenta ogni anno. In genere i canali si distinguono in base al meccanismo di consegna, come segue:

* Canale fisico; ad esempio, desktop, dispositivi mobili.
* Forma di consegna in un canale fisico, ad esempio “pagina dei dettagli di un prodotto”, “pagina della categoria del prodotto” per desktop oppure “web mobile”, “app mobile” per dispositivi mobili.

Tuttavia, probabilmente non vorrai utilizzare lo stesso contenuto per tutti i canali, ma dovrai ottimizzarlo in base al canale specifico.

I frammenti di contenuto consentono di:

* valutare come raggiungere in modo efficiente il pubblico target su ciascun canale;
* creare e gestire contenuti editoriali indipendenti dal canale;
* creare pool di contenuti per una serie di canali;
* progettare varianti di contenuto per canali specifici;
* aggiungere immagini al testo inserendo delle risorse (frammenti con elementi multimediali diversi);
* Crea contenuti nidificati in modo da riflettere la complessità dei dati.

Questi frammenti di contenuto possono quindi essere assemblati per fornire esperienze su vari canali.

>[!NOTE]
>
>I **frammenti di contenuto** e i **[frammenti di esperienza](/help/sites-cloud/authoring/fragments/content-fragments.md)** sono funzioni diverse in AEM:
>* I **frammenti di contenuto** sono contenuti editoriali, con definizione e struttura, ma senza elementi visivi aggiuntivi di design e/o layout. Possono essere utilizzati per accedere a dati strutturati, tra cui testi, numeri e date.
>* I **frammenti di esperienza** sono contenuti completi di layout, frammenti di una pagina web.
>
>I frammenti esperienza possono includere contenuti sotto forma di frammenti di contenuto, ma non viceversa.
>
>Per ulteriori informazioni, vedere anche [Informazioni sui frammenti di contenuto e sui frammenti di esperienza in AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/content-fragments/understand-content-fragments-and-experience-fragments.html?lang=it#content-fragments).

## Frammenti di contenuto e Content Services {#content-fragments-and-content-services}

AEM Content Services è progettato per generalizzare la descrizione e la consegna dei contenuti in/da AEM, non limitandosi alle pagine web.

Fornisce contenuti a canali diversi dalle tradizionali pagine web di AEM, utilizzando metodi standardizzati utilizzabili da qualsiasi cliente. Questi canali possono includere:

* Applicazioni a pagina singola
* Applicazioni mobile native
* Altri canali e punti di contatto esterni ad AEM

La consegna viene effettuata in formato JSON utilizzando il modulo di esportazione JSON.

I frammenti di contenuto di AEM possono essere utilizzati per descrivere e gestire contenuti strutturati. Il contenuto strutturato è definito in modelli che possono contenere vari tipi di contenuto, tra cui testo, dati numerici, dati booleani, data e ora e altro ancora.

Insieme alle funzionalità di esportazione JSON dei componenti core di AEM, tali contenuti strutturati possono quindi essere utilizzati per consegnare contenuti AEM a canali diversi dalle pagine AEM.

>[!NOTE]
>
>Consulta [Headless e AEM](/help/headless/introduction.md) per un’introduzione allo sviluppo headless per AEM Sites as a Cloud Service.

>[!NOTE]
>
>AEM supporta anche la traduzione del contenuto dei frammenti. Per ulteriori informazioni, consulta [Traduzione ddelle risorse](/help/assets/translate-assets.md).

## Tipo di contenuto {#content-type}

I frammenti di contenuto sono:

* Memorizzati come **Risorse**:

   * I frammenti di contenuto (e le relative varianti) possono essere creati e gestiti dalla console **Assets**.
   * Vengono creati e modificati nell’Editor frammenti di contenuto.

* Utilizzato nell&#39;editor pagina [&#x200B; dal componente Frammento di contenuto](/help/sites-cloud/authoring/fragments/content-fragments.md) (componente di riferimento):

   * Il componente **Frammento di contenuto** è disponibile per gli autori delle pagine. Consente loro di fare riferimento e distribuire il frammento di contenuto richiesto in formato HTML o JSON.

* Accessibili tramite l’[API GraphQL di AEM](/help/headless/graphql-api/content-fragments.md).

I frammenti di contenuto sono una struttura di contenuto che:

* Non disporre di layout o progettazione (in modalità Testo formattato è possibile formattare del testo).
* Contiene una o più [parti costitutive](#constituent-parts-of-a-content-fragment).
* [Contengono immagini o possono essere connesse a esse](#fragments-with-visual-assets).
* È utilizzato [tra i contenuti](#in-between-content-when-page-authoring-with-content-fragments) quando vi si fa riferimento in una pagina.
* Sono indipendenti dal meccanismo di consegna (ovvero, pagina, canale).

### Frammenti con risorse visive {#fragments-with-visual-assets}

Per dare agli autori un maggiore controllo sui contenuti, le immagini possono essere aggiunte a e/o integrate con un frammento di contenuto.

Assets può essere utilizzato con un frammento di contenuto in diversi modi, ciascuno con i propri vantaggi:

* Tramite **Inserisci risorsa** per inserire una risorsa in un frammento (frammenti con elementi multimediali diversi)

   * Fanno parte del frammento (vedi [Parti costitutive di un frammento di contenuto](#constituent-parts-of-a-content-fragment)).
   * Viene definita la posizione della risorsa.
   * Per ulteriori informazioni consulta [Inserimento di risorse nel frammento](/help/assets/content-fragments/content-fragments-variations.md#inserting-assets-into-your-fragment) nell’editor di frammenti.

  >[!NOTE]
  >
  >Le risorse visive inserite nel frammento di contenuto stesso sono associate al paragrafo precedente. Quando il frammento viene aggiunto a una pagina, queste risorse vengono spostate in relazione a tale paragrafo quando viene aggiunto contenuto intermedio.

* **Contenuto associato**

   * Connesso a un frammento, ma non parte fissa del frammento (vedi [Parti costitutive di un frammento di contenuto](#constituent-parts-of-a-content-fragment)).
   * Ha una certa flessibilità per il posizionamento.
   * Facilmente disponibile per l’uso (come contenuto intermedio) quando si utilizza il frammento su una pagina.

  Per ulteriori informazioni vedi [Contenuto associato](/help/assets/content-fragments/content-fragments-assoc-content.md).

* Risorse disponibili nel **browser Risorse** dell’editor pagina

   * Offrono massima flessibilità nella selezione di una risorsa.
   * Ha una certa flessibilità per il posizionamento.
   * Non supportano il concetto di approvazione per un frammento specifico.

  Per ulteriori informazioni vedi [Browser risorse](/help/sites-cloud/authoring/page-editor/editor-side-panel.md#assets-browser).

### Parti costitutive di un frammento di contenuto {#constituent-parts-of-a-content-fragment}

Le risorse dei frammenti di contenuto sono composte dalle seguenti parti (direttamente o indirettamente):

* **Elementi del frammento**

   * Gli elementi sono correlati ai campi di dati che contengono il contenuto.
   * Per creare il frammento di contenuto, puoi utilizzare un modello di contenuto. Gli elementi (campi) specificati nel modello definiscono la struttura del frammento. Questi elementi (campi) possono essere di vari tipi di dati.

* **Paragrafi del frammento**

   * Blocchi di testo, spesso con più righe delimitate come singole entità.

   * Nelle modalità [Testo formattato](/help/assets/content-fragments/content-fragments-variations.md#rich-text) e [Markdown](/help/assets/content-fragments/content-fragments-variations.md#markdown), un paragrafo può essere formattato come intestazione, in tal caso appartiene a un’unica unità insieme al paragrafo seguente.

   * Consentono di controllare i contenuti durante l’authoring delle pagine.

* **Risorse inserite in un frammento (frammenti con elementi multimediali diversi)**

   * Risorse (immagini) inserite nel frammento effettivo e utilizzate come contenuto interno di un frammento.
   * Incorporato nel sistema paragrafo del frammento.
   * Possono essere formattate quando il [frammento viene utilizzato o inserito come riferimento in una pagina](/help/sites-cloud/authoring/fragments/content-fragments.md).
   * Possono solo essere aggiunte, eliminate o spostate all’interno di un frammento utilizzando l’editor di frammenti. Queste azioni non possono essere eseguite nell’editor pagina.
   * Possono essere aggiunte, eliminate o spostate all&#39;interno di un frammento solo utilizzando il formato [Rich Text nell&#39;editor frammenti](/help/assets/content-fragments/content-fragments-variations.md#inserting-assets-into-your-fragment).
   * Possono essere aggiunte solo a elementi di testo su più righe (qualsiasi tipo di frammento).
   * Sono associate al testo che precede (paragrafo).

     >[!CAUTION]
     >
     >Le risorse possono essere rimosse (inavvertitamente) da un frammento se si passa al formato Testo normale.

     >[!NOTE]
     >
     >È inoltre possibile aggiungere Assets come contenuto aggiuntivo (intermedio) quando si utilizza un frammento su una pagina, utilizzando [Contenuto associato](/help/assets/content-fragments/content-fragments-assoc-content.md) o risorse dal browser Assets.

* **Contenuto associato**

   * Contenuti esterni a un frammento, ma con rilevanza editoriale per esso. In genere si tratta di immagini, video o altri frammenti.
   * Le singole risorse all’interno di una raccolta sono disponibili per essere utilizzate con il frammento nell’editor pagina quando questo viene aggiunto a una pagina. Sono quindi elementi opzionali, a seconda dei requisiti del canale specifico.
   * Le risorse sono [associate a frammenti tramite raccolte](/help/assets/content-fragments/content-fragments-assoc-content.md); le raccolte associate consentono all&#39;autore di decidere quali risorse utilizzare durante l&#39;authoring della pagina.

      * Le raccolte possono essere associate ai frammenti come contenuto predefinito, oppure possono essere associate dagli autori durante la creazione dei frammenti.
      * Le [raccolte di risorse (DAM)](/help/assets/manage-collections.md) sono la base del contenuto associato dei frammenti.
   * Volendo, puoi anche aggiungere il frammento stesso a una raccolta per facilitare il tracciamento.

* **Metadati del frammento**

   * Utilizzano gli [schemi di metadati delle risorse](/help/assets/metadata-schemas.md).
   * È possibile creare i tag quando:

      * si crea e si effettua l’authoring del frammento;
      * oppure in un secondo tempo:

         * visualizzando e modificando le **Proprietà** del frammento dalla console;
         * modificando i **Metadati** nell’editor di frammenti

  >[!CAUTION]
  >
  >I profili di elaborazione dei metadati non sono applicabili ai frammenti di contenuto.

* **Principale**

   * Parte del frammento

      * Ogni frammento di contenuto dispone di un’istanza Principale.
      * L’elemento Principale non può essere eliminato.

   * L’elemento Principale è accessibile nella sezione **[Varianti](/help/assets/content-fragments/content-fragments-variations.md)** dell’editor di frammenti.
   * l’elemento Principale non è una variante in sé, ma è la base di tutte le varianti.

* **Varianti**

   * Sono rappresentazioni di testo di frammenti specifiche a scopo editoriale; possono essere relative a un canale ma non sono obbligatorie; possono anche essere utilizzate per modifiche locali ad hoc.
   * Vengono create come copie di **Master**, ma possono essere modificate in base alle esigenze. Esiste una sovrapposizione di contenuti tra le varianti stesse.
   * Possono essere definite durante l’authoring del frammento.
   * Sono memorizzate nel frammento, per evitare la dispersione delle copie del contenuto.
   * Le varianti possono essere [sincronizzate](/help/assets/content-fragments/content-fragments-variations.md#synchronizing-with-master) con l’elemento principale se il suo contenuto viene aggiornato.
   * Il testo può essere [riepilogato](/help/assets/content-fragments/content-fragments-variations.md#summarizing-text) per ridurlo rapidamente a una lunghezza predefinita.
   * Sono disponibili nella scheda [Varianti](/help/assets/content-fragments/content-fragments-variations.md) dell’editor di frammenti.

### Contenuto intermedio nell’authoring di pagine con frammenti di contenuto {#in-between-content-when-page-authoring-with-content-fragments}

Contenuto intermedio:

* Può essere utilizzato nell’Editor pagina quando si lavora con frammenti di contenuto.
* [Contenuto aggiuntivo aggiunto all&#39;interno del flusso di un frammento](/help/sites-cloud/authoring/fragments/content-fragments.md#adding-in-between-content) dopo che è stato utilizzato o inserito come riferimento in una pagina.
* Disponibile per l&#39;utilizzo nell&#39;[Editor pagina quando si lavora con frammenti di contenuto](/help/sites-cloud/authoring/fragments/content-fragments.md).
* Il contenuto intermedio può essere aggiunto a qualsiasi frammento, in cui è visibile un solo elemento.
* È possibile utilizzare il contenuto associato, così come le risorse e/o i componenti dal browser appropriato.

>[!CAUTION]
>
>Il contenuto intermedio è il contenuto della pagina. Non viene memorizzato nel frammento di contenuto.

### Elementi necessari per i frammenti {#required-by-fragments}

Per creare frammenti di contenuto, è necessario:

* **Modello di contenuto**

   * Viene [abilitato tramite il Browser configurazioni](/help/assets/content-fragments/content-fragments-configuration-browser.md).
   * Viene [creato utilizzando gli strumenti](/help/assets/content-fragments/content-fragments-models.md).
   * È necessario per [creare un frammento](/help/assets/content-fragments/content-fragments-managing.md#creating-content-fragments).
   * Definisce la struttura di un frammento (titolo, elementi di contenuto, definizioni tag).
   * La definizione di un modello di contenuto richiede un titolo e un elemento dati; tutto il resto è facoltativo.
   * Il modello può definire eventuale contenuto predefinito.
   * Durante l’authoring del contenuto di un frammento, gli autori non possono modificare la struttura definita.
   * Le modifiche apportate a un modello dopo la creazione dei frammenti di contenuto dipendenti possono influire su tali frammenti di contenuto.

Per utilizzare i frammenti di contenuto per l’authoring delle pagine, è inoltre necessario:

* **Componente Frammento di contenuto**

   * Essenziale per distribuire il frammento in formato HTML, JSON o entrambi.
   * Obbligatorio per [fare riferimento al frammento in una pagina](/help/sites-cloud/authoring/fragments/content-fragments.md).
   * Responsabile del layout e della distribuzione di un frammento, ovvero i canali.
   * I frammenti devono disporre di uno o più componenti dedicati per definire il layout e fornire alcuni o tutti gli elementi/varianti e i contenuti associati.
   * Quando si trascina un frammento su una pagina durante l’authoring, il componente richiesto viene associato automaticamente.

## Riutilizzo dei frammenti di contenuto con MSM {#reusing-content-fragments-with-msm}

Se si accede tramite la console **Assets**, è possibile utilizzare MSM e creare Live Copy per i frammenti.

Per ulteriori dettagli, consulta:

* [Riutilizzare frammenti di contenuto con MSM](/help/assets/content-fragments/content-fragments-msm.md)
* [Riutilizzare le risorse tramite MSM per Assets](/help/assets/reuse-assets-using-msm.md).

Questi abilitano l&#39;[ereditarietà](/help/assets/content-fragments/content-fragments-variations.md#inheritance) sia per le varianti che per i singoli campi dei frammenti.

>[!CAUTION]
>
>Se desideri utilizzare MSM (che crea copie dei frammenti di contenuto), tutti i vincoli **Unique** devono essere rimossi da qualsiasi tipo di dati utilizzato nei rispettivi [Modelli per frammenti di contenuto](/help/assets/content-fragments/content-fragments-models.md).

## Esempio di utilizzo {#example-usage}

Un frammento, con i relativi elementi e varianti, può essere utilizzato per creare contenuti coerenti per più canali. Durante la progettazione del frammento, considera cosa viene utilizzato e dove viene utilizzato.

### Esempio WKND {#wknd-sample}

Per apprendere a utilizzare AEM as a Cloud Service, viene fornito il [sito WKND](/help/implementing/developing/introduction/develop-wknd-tutorial.md) di esempio.

Il progetto WKND include:

* Modelli di Frammento di contenuto disponibili in:
  `http://<hostname>:<port>/libs/dam/cfm/models/console/content/models.html/conf/wknd`

* Frammenti di contenuto (e altro contenuto) disponibili in:
  `http://<hostname>:<port>/assets.html/content/dam/wknd/en`
