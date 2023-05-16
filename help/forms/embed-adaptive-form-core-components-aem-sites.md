---
title: Aggiungere un modulo adattivo (componenti core) nella pagina AEM Sites
seo-title: How to add an Adaptive Form (Core Components) to an AEM Sites page?
description: È possibile utilizzare il modulo adattivo (componenti core) in una pagina AEM Sites per compilare e inviare un modulo senza uscire dalle pagine AEM Sites.
feature: Adaptive Forms
hide: true
hidefromtoc: true
exl-id: 1046231f-787c-4e49-9ba0-e7dd59e41bce
source-git-commit: 0d21b4ba2e7ce7592e3f2c57e4d320adc0af1008
workflow-type: tm+mt
source-wordcount: '2207'
ht-degree: 2%

---

# Aggiungere Forms adattivo a una pagina AEM Sites {#add-an-adaptive-form-to-aem-sites-page}

## Panoramica {#overview}

È possibile creare o incorporare facilmente Adaptive Forms in una pagina AEM Sites per consentire agli utenti di compilare e inviare un modulo senza uscire dalla pagina Sites. Consente all’utente di rimanere nel contesto di altri elementi della pagina web e di interagire contemporaneamente con il modulo.

Per creare o incorporare un modulo adattivo in una pagina AEM Sites, puoi scegliere uno dei seguenti metodi:

* **Creare un modulo adattivo trascinando e rilasciando i componenti del modulo sul componente contenitore di Forms adattivo**: Utilizza la [Contenitore Forms adattivo](#af-container-component) per creare uno spazio all’interno della pagina web in cui è memorizzato il modulo adattivo. È possibile trascinare e rilasciare il componente Modulo adattivo in questo spazio per creare un modulo. Ad esempio, guarda il video seguente per scoprire come creare un modulo adattivo utilizzando [!UICONTROL Contenitore Forms adattivo] componente:

La [Contenitore di moduli adattivi](#af-container-component) Il componente ti consente di creare esperienze di iscrizione digitale utilizzando i componenti Forms adattivi direttamente nell’editor AEM Sites. Questa integrazione offre un’esperienza diretta agli autori di AEM Sites che desiderano creare e gestire moduli all’interno delle proprie pagine AEM Sites.

* **Incorporare un modulo adattivo esistente**: La [Forms adattivo - Incorporamento (V2)](#embed-existing-af) consente di incorporare facilmente un modulo adattivo preesistente in una pagina di AEM Sites. Ad esempio, incorporare un modulo adattivo utilizzando [!UICONTROL Forms adattivo - Incorporamento] nella pagina del sito come illustrato nel video seguente:

Questa funzione migliora l&#39;adattabilità e la riutilizzabilità di Adaptive Forms. Questa integrazione offre ai clienti un modo pratico per riutilizzare l&#39;Adaptive Forms già creato.

* **Creazione guidata Forms adattiva per creare un modulo**:

   Utilizza la [Forms adattivo - Incorporamento (v2)](#embed-new-af) per creare un modulo adattivo dall’interno dell’editor AEM Sites utilizzando la procedura guidata Creazione modulo. Il modulo viene salvato come entità esterna. È possibile riutilizzare il modulo anche in altre pagine di Sites e moduli indipendenti.
Ad esempio, guarda il video seguente per scoprire come creare e incorporare un nuovo modulo adattivo utilizzando [!UICONTROL Forms adattivo - Incorporamento] nella pagina del sito.

### Considerazione {#considerations}

È possibile utilizzare l’Editor regole per aggiungere o controllare il comportamento dinamico dei componenti Modulo adattivo. Ad esempio, nascondere o mostrare un componente. L’Editor regole non è disponibile per i componenti Modulo non adattivo. Utilizza quindi la tua diligenza quando utilizzi componenti modulo non adattivi nel componente Contenitore di AEM Forms.

## Creare un modulo adattivo utilizzando il componente contenitore di Forms adattivo {#af-container-component}

La [!UICONTROL Contenitore di moduli adattivi] Il componente consente di creare esperienze di iscrizione digitale utilizzando i componenti di Forms adattivi nell’editor AEM Sites. È possibile creare un modulo adattivo trascinando e rilasciando i componenti del modulo.

### Prerequisiti {#prerequisites-af-container}

+++ Abilita **[!UICONTROL Contenitore Forms adattivo]** nel criterio del modello associato.

Per abilitare [!UICONTROL Contenitore Forms adattivo] nel criterio del modello, esegui i seguenti passaggi:

1. Vai a [!UICONTROL Informazioni pagina] > [!UICONTROL Modifica modello]
1. Fai clic sul pulsante [!UICONTROL Criterio] e seleziona la **[!UICONTROL Contenitore Forms adattivo]**  sotto la casella di controllo **[Nome progetto Archetype AEM] - Modulo adattivo**.
1. Fai clic su **[!UICONTROL Fine]**.

>[!VIDEO](https://video.tv.adobe.com/v/3419370?quality=12&learn=on)

+++

+++ Includi le clientlibs nella pagina del sito

Per utilizzare i componenti Forms adattivi in una pagina AEM Sites, includi le librerie client Customheaderlibs e Customfooterlibs nella pagina AEM Sites utilizzando l’archivio Archetype/Git AEM e la pipeline di distribuzione.

1. Apri il tuo [Archivio AEM Forms Archetype o Git duplicato](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=it) in un editor di testo. Ad esempio, Codice di Visual Studio.
1. Accedi a `ui.apps/src/main/content/jcr_root/apps/corecomponents/components/page/.content.xml`.
1. Copia il valore di `sling:resourceSuperType`. Ad esempio, il valore è `core/wcm/components/page/v3/page`.

   ![risorsa sling](/help/forms/assets/slingresource.png)

1. Crea la struttura simile nella posizione `ui.apps/src/main/content/jcr_root/apps` uguale a `core/wcm/components/page/v3/page`.

   ![struttura sovrapposta](/help/forms/assets/overlaystructure.png)

1. Aggiungi `customheaderlibs.html` e `customfooterlibs.html` file.

   ```
   //Customheaderlibs.html
   <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html">
       <sly data-sly-call="${clientlib.css @ categories='core.forms.components.runtime.all'}"/>
   </sly> 
   
   //customfooterlibs.html
   <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html">
       <sly data-sly-test="${!wcmmode.edit}" data-sly-call="${clientlib.js @ categories='core.forms.components.runtime.all', async=true}"/>
   </sly> 
   ```

   Il customfooterlibs.html viene utilizzato per JavaScript e il customheaderlibs.html per il css.

1. [Eseguire la pipeline](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/site-creation/enable-front-end-pipeline.html) per distribuire le modifiche.

+++

### Creare un modulo adattivo utilizzando il componente contenitore di Forms adattivo {#create-af-using-af-container}


Per creare un modulo adattivo utilizzando [!UICONTROL Contenitore Forms adattivo] componente:

1. Apri la pagina AEM Sites in modalità di modifica.
1. Dal pannello del browser Componenti, trascina **[!UICONTROL Contenitore Forms adattivo]** nella pagina.
1. Crea un modulo adattivo utilizzando i componenti Forms adattivi.
1. Salva le impostazioni.

>[!VIDEO](https://video.tv.adobe.com/v/3419284?quality=12&learn=on)

Il modulo è pronto. Quando pubblichi la pagina AEM Sites, pubblica automaticamente un Modulo adattivo e le relative risorse di riferimento associate.

#### Configurare le proprietà dei contenitori di moduli adattivi {#configure-additional-settings-container}

Puoi personalizzare le impostazioni avanzate della [!UICONTROL Contenitore di moduli adattivi] componente. Ad esempio, è possibile configurare il servizio di precompilazione per caricare un modulo adattivo con valori precompilati sulla pagina di un sito. È possibile configurare le impostazioni del modello dati per associare il modulo adattivo a un modello dati. Se si desidera salvare i dati su OneDrive o SharePoint durante l’invio di un modulo adattivo, configurare le impostazioni per l’azione di invio. Puoi anche aggiungere un’azione di invio personalizzata per l’Adaptive Forms.

Per impostare le proprietà di **[!UICONTROL Contenitore Forms adattivo]** fai clic sul ![settings_icon](/help/forms/assets/Smock_Wrench_18_N.svg) sulla barra delle azioni. La **[!UICONTROL Modifica contenitore Forms adattivo]** viene visualizzata la finestra di dialogo .

![Finestra di dialogo per modifica](/help/forms/assets/adaptiveformcontainer-editdialog.png)

In [!UICONTROL Modifica contenitore Forms adattivo] è possibile specificare quanto segue.
* **Scheda Base**
   * **Servizio di precompilazione**: È possibile utilizzare il servizio di precompilazione per compilare automaticamente i campi di un modulo adattivo utilizzando i dati esistenti. Quando un utente apre un modulo, i valori relativi a tali campi vengono precompilati. Per informazioni sul servizio di precompilazione, vedi [Precompilare i campi del modulo adattivo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/prepopulate-adaptive-form-fields.html#configuring-prefill-service-using-configuration-manager)
   * **Categoria libreria client**: Specifica la [Funzioni JavaScript](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/add-rules-and-use-expressions-in-an-adaptive-form/rule-editor.html?lang=en#custom-functions) utilizzati nelle espressioni e supportati da Adaptive Forms.
* **Modello dati**: Un modello dati consente di integrare entità e servizi da origini dati diverse in un modulo adattivo. Scegli **[!UICONTROL Modello dati modulo]** se il modulo adattivo creato prevede il recupero e la scrittura di dati da e verso più origini dati.
   * **Modello dati modulo**: Un modello dati modulo consente a un modulo adattivo di comunicare con origini dati diverse. Per informazioni sulla configurazione di un’origine dati, consulta [Configura le origini dati.](/help/forms/configure-data-sources.md)
   * **Schema**: Lo schema rappresenta la struttura in cui i dati vengono prodotti o utilizzati dal sistema back-end della tua organizzazione. È possibile [associare lo schema a un modulo adattivo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/create-an-adaptive-form-on-forms-cs/adaptive-form-json-schema-form-model.html) e utilizza i relativi elementi per aggiungere contenuto dinamico a un modulo adattivo.

      >[!NOTE]
      >
      > Dopo aver configurato il modello dati Modulo, non è possibile modificare il modello di modulo associato. Tuttavia, è possibile modificare lo schema associato al modello dati del modulo.

* **Scheda Invio**

   * **Reindirizza all’URL**

      **URL/percorso di reindirizzamento**: Specifica l’URL o il percorso a cui viene reindirizzato un modulo adattivo dopo l’azione di invio.

      **Invia azione**: Un’azione di invio viene attivata quando l’utente fa clic sul pulsante Invia in un modulo adattivo. È possibile [configurare l’azione di invio nel modulo adattivo](/help/forms/configuring-submit-actions.md). I moduli adattivi forniscono alcune azioni predefinite per l’invio:
      * Invia all’endpoint REST
      * Invia e-mail
      * Invia usando il modello dati modulo
      * Richiamare un flusso di lavoro AEM
      * Invia a SharePoint
      * Invia a OneDrive
      * Invia ad Azure Blob Storage

   È inoltre possibile [estendere le azioni di invio predefinite](custom-submit-action-form.md) per creare un’azione di invio personalizzata.

* **Mostra messaggio**
   * **Contenuto del messaggio**: Scrivere un messaggio utilizzando l’editor Rich Text da visualizzare durante l’invio del modulo. Questa opzione è disponibile solo quando scegli di mostrare un messaggio di ringraziamento.

## Incorporare un modulo adattivo  {#aem-container-component}

Utilizzo **[!UICONTROL Forms adattivo - Incorporamento (V2)]** È possibile incorporare un nuovo modulo adattivo o un modulo adattivo esistente nella pagina del sito. La [!UICONTROL Forms adattivo - Incorporamento] component consente di:

* [Incorporare un modulo adattivo esistente](#embed-new-af)

* [Creare e incorporare un nuovo modulo adattivo](#embed-existing-af)

### Prerequisiti {#prerequisites}

+++ Abilita la **Forms adattivo - Incorporamento** nel criterio del modello associato.

Per abilitare [!UICONTROL Forms adattivo - Incorporamento (v2)] nel criterio del modello, esegui i seguenti passaggi:

1. Vai a [!UICONTROL Informazioni pagina] > [!UICONTROL Modifica modello]

1. Fai clic sul pulsante [!UICONTROL Criterio] e seleziona la **[!UICONTROL Modulo adattivo - Incorporamento (v2)]** sotto la casella di controllo **[!UICONTROL [Nome progetto Archetype AEM] - Forms]** gruppo .
1. Fai clic su **[!UICONTROL Fine]**.

>[!VIDEO](https://video.tv.adobe.com/v/3419369?quality=12&learn=on)

+++

+++ Includi le clientlibs nella pagina del sito

Quando il **[!UICONTROL Quando il modulo copre l’intera larghezza di una pagina]** è selezionata nella **[!UICONTROL Contenitori di moduli]** configura la finestra di dialogo e **Forms adattivo utilizzando i componenti core** vengono utilizzati, è necessario includere le clientlibs nella pagina del sito corrispondente.

![Gif sovrapposto](/help/forms/assets/overlaycorecomponent.gif)

Per utilizzare i componenti Forms adattivi in una pagina AEM Sites, includi le librerie client Customheaderlibs e Customfooterlibs nella pagina AEM Sites utilizzando l’archivio Archetype/Git AEM e la pipeline di distribuzione.

1. Apri il tuo [Archivio AEM Forms Archetype o Git duplicato](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=it) in un editor di testo. Ad esempio, Codice di Visual Studio.
1. Accedi a `ui.apps/src/main/content/jcr_root/apps/corecomponents/components/page/.content.xml`.
1. Copia il valore di `sling:resourceSuperType`. Ad esempio, il valore è `core/wcm/components/page/v3/page`.

   ![risorsa sling](/help/forms/assets/slingresource.png)

1. Crea la struttura simile nella posizione `ui.apps/src/main/content/jcr_root/apps` uguale a `core/wcm/components/page/v3/page`.

   ![struttura sovrapposta](/help/forms/assets/overlaystructure.png)

1. Aggiungi `customheaderlibs.html` e `customfooterlibs.html` file.

   ```
   //Customheaderlibs.html
   <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html"
       data-sly-use.form="com.adobe.cq.forms.core.components.models.aemform.AEMForm">
       <sly data-sly-test="${form.formVersion=='2.1' && !wcmmode.edit}" data-sly-call="${clientlib.css @ categories='core.forms.components.runtime.all'}"/>
   </sly>
   
   //customfooterlibs.html
   <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html"
     data-sly-use.form="com.adobe.cq.forms.core.components.models.aemform.AEMForm">
     <sly data-sly-test="${form.formVersion=='2.1' && !wcmmode.edit}" data-sly-call="${clientlib.js @ categories='core.forms.components.runtime.all', async=true}"/>
   </sly>
   ```

   Il file customfooterlibs.html viene utilizzato per JavaScript e il file customheaderlibs.html per i CSS.

1. [Eseguire la pipeline](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/site-creation/enable-front-end-pipeline.html) per distribuire le modifiche.

+++

### Incorpora nuovo modulo adattivo {#embed-new-af}

1. Apri la pagina AEM Sites in modalità di modifica.
1. Dal pannello del browser Componenti, trascina [!UICONTROL Forms adattivo - Incorporamento (v2)] nella pagina.
1. Fai clic sul pulsante **Plus** e si viene reindirizzati alla procedura guidata di creazione del modulo.

   ![Forms adattivo - Componente da incorporare](/help/forms/assets/aemformcontainer.png)

1. Creare un nuovo modulo adattivo da [!UICONTROL Creazione di moduli] procedura guidata.
1. La [!UICONTROL Percorso risorsa] include già il percorso di un modulo adattivo creato
1. Salva le impostazioni. Il modulo adattivo è ora incorporato nella pagina .

>[!VIDEO](https://video.tv.adobe.com/v/3419366/adaptive-form-aem-forms?quality=12&learn=on)

### Incorpora modulo adattivo esistente {#embed-existing-af}

1. Apri la pagina AEM Sites in modalità di modifica.
1. Dal pannello del browser Componenti, trascina [!UICONTROL Forms adattivo - Incorporamento] nella pagina.
1. Tocca [!UICONTROL Forms adattivo - Incorporamento] nella pagina Sites e tocca ![settings_icon](/help/forms/assets/Smock_Wrench_18_N.svg) sulla barra delle azioni. La **[!UICONTROL Modifica Forms adattivo - Incorpora]** viene visualizzata la finestra di dialogo .
1. Sfoglia e seleziona il modulo adattivo da incorporare nel [!UICONTROL Percorso risorsa].
1. Salva le impostazioni. Il modulo adattivo è ora incorporato nella pagina .

>[!VIDEO](https://video.tv.adobe.com/v/3419368?quality=12&learn=on)

#### Configurare le proprietà di incorporamento _ del modulo adattivo

Puoi personalizzare le impostazioni avanzate della [!UICONTROL Modulo adattivo - Incorporamento (v2)] componente. In [!UICONTROL Modifica Forms adattivo - Incorpora (v2)] è possibile specificare quanto segue.

* **Percorso risorsa**: Sfoglia e seleziona il modulo adattivo da incorporare. Viene compilato automaticamente se viene rilasciato dal browser Risorse.
* **Invia invio** : Selezionare l’azione da attivare all’invio del modulo. Puoi scegliere di mostrare un messaggio di ringraziamento o una pagina di ringraziamento.
   * **Mostra messaggio di ringraziamento**: Scrivere un messaggio utilizzando l’editor Rich Text da visualizzare durante l’invio del modulo. Questa opzione è disponibile solo quando scegli di mostrare un messaggio di ringraziamento.
   * **Mostra pagina di ringraziamento**: Individuare e selezionare la pagina da visualizzare durante l’invio del modulo. Questa opzione è disponibile solo quando scegli di mostrare una pagina di ringraziamento.
   * **Reindirizza alla pagina di ringraziamento**: Abilita l’opzione per sostituire la pagina contenente il modulo adattivo incorporato con la pagina di ringraziamento. In caso contrario, la pagina di ringraziamento sostituisce il Modulo adattivo nel [!UICONTROL Forms adattivo - Incorporamento] senza aggiornare i siti sottostanti la pagina. Questa opzione è disponibile solo quando scegli di mostrare una pagina di ringraziamento.
* **Usa lingua pagina**: Utilizza locale della pagina AEM Sites invece delle impostazioni internazionali del modulo adattivo.
* **Imposta lo stato attivo sul modulo**: Selezionare questa opzione per impostare lo stato attivo sul primo campo del modulo adattivo.
* **Il modulo copre l&#39;intera larghezza del frame**: Se questa opzione è selezionata, l’iframe non viene utilizzato per il rendering del modulo.
* **Altezza**: Specifica l’altezza del contenitore. Lascia vuoto per ridimensionare automaticamente il contenitore.
* **Libreria client CSS**: Specifica il percorso di una libreria client CSS.

### Pubblicare un modulo adattivo incorporato {#publishing-embedded-adaptive-form}

Consideriamo i seguenti scenari per pubblicare un modulo adattivo incorporato nella pagina AEM siti:

* Se pubblichi la pagina dei siti di AEM per la prima volta e include un modulo adattivo incorporato, pubblica la pagina dei siti e la risorsa incorporata.
* Se hai modificato solo il modulo adattivo incorporato in una pagina del sito pubblicata, pubblica la risorsa originale e le modifiche si riflettono nella pagina del sito pubblicata. La pagina del sito pubblicata include un riferimento alla risorsa e non richiede la ripubblicazione della pagina.
* Se hai modificato la pagina dei siti e il modulo adattivo incorporato , ripubblica la pagina dei siti e la risorsa incorporata.

### Modificare il modulo adattivo incorporato  {#modifying-embedded-adaptive-form}

Per modificare una configurazione o una proprietà del modulo adattivo incorporato, effettuare una delle operazioni seguenti.

* Apri il modulo originale in un modulo adattivo nel rispettivo editor e modificalo.
* Tocca Modulo adattivo dalla pagina del sito in modalità di modifica, quindi tocca **[!UICONTROL Modifica in una nuova finestra]**. Il modulo originale viene aperto in modalità di modifica che è possibile modificare.

>[!NOTE]
>
>Le modifiche apportate al modulo adattivo originale si riflettono automaticamente nel modulo incorporato. Tuttavia, ripubblica il modulo adattivo o la pagina del sito per riflettere le modifiche nella pagina pubblicata.

### Best practice {#best-practices}

* Le intestazioni e i piè di pagina nel modulo originale non sono inclusi nel modulo incorporato.
* Le bozze degli utenti e gli invii dei moduli incorporati sono supportati e visibili nelle schede Bozze e Inviate Forms sul portale Forms.

[Nella pagina AEM Sites, la modalità Layout](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/authoring/features/responsive-layout.html?#defining-layouts-layout-mode) consente di ridimensionare un modulo adattivo creato o incorporato in una pagina di un sito AEM.

![Supporto di layout AF](/help/forms/assets/afsite-layoutsupport.gif)

AEM pagina siti mantiene un riferimento al modulo adattivo. Quando traduci una pagina AEM Sites, traduce automaticamente un Modulo adattivo e le relative risorse di riferimento associate utilizzando [progetti di traduzione](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/reusing-content/translation/managing-projects.html?lang=en#adding-pages-assets-to-a-translation-job) in altre lingue.
